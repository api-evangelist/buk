---
name: buk-sync-employee-directory
description: Pull the full employee (Colaborador) directory out of Buk with its org structure, jobs and reporting lines, and keep a downstream system in sync.
api: buk:data-access-api
generated: '2026-08-08'
method: generated
source: openapi/buk-data-access-api-chile-openapi.yml
operations:
- GET /employees
- GET /employees/active
- GET /employees/{id}
- GET /employees/{id}/jobs
- GET /employees/{id}/subordinates
- GET /areas
- GET /areas/{id}
- GET /organization/areas/
- GET /organization/areas/{id}
- GET /companies
- GET /roles
- GET /role_families
- GET /people/{id}
- GET /users
---

# Sync the Buk employee directory

Buk is the HR system of record. This skill reads the directory and its org structure out of a
tenant so a downstream system (IdP, BI warehouse, ticketing, access provisioning) can mirror it.

## Before you start

- **Base URL** is tenant- and country-scoped: `https://{tenant}.buk.cl/api/v1/{country}` where
  `{country}` is one of `chile`, `colombia`, `peru`, `mexico`, `brasil`. There is no global host.
- **Auth** is an API key in the `auth_token` header. A tenant administrator issues it under
  *Configuración → Acceso API*. Read-only sync needs only the **Lectura** permission level on
  Employee; do not request *Lectura y Modificación* for a read job.
- The contracts declare `securityDefinitions.auth_token` but **do not apply it** to any
  operation, so a generated client will not send the header. Add it yourself.
- There are **no operationIds** in this contract. Address operations by method + path.

## Steps

1. **Page the roster.** `GET /employees` with `page` and `page_size`. Read
   `pagination.totalPages` and `pagination.next` from the response and keep going until
   `next` is null. Default page size is 25; do not assume a ceiling above 100.
2. **Filter on the server, not the client.** `GET /employees` accepts `status`
   (`active`, `inactive`, `pending`), `company_id`, `email`, `code_sheet`, `code_recinto`,
   `document_number` and `update_start_date`. For an incremental sync, drive it from
   `update_start_date` rather than re-reading the whole roster.
   `GET /employees/active` is the shortcut for the active-only roster.
3. **Read the org tree.** `GET /organization/areas/` for areas and sub-areas, then
   `GET /organization/areas/{id}` for a single node. `GET /areas` is the older flat listing —
   pick one and stay on it. `GET /companies` gives the legal entities inside the tenant, which
   matters because one Buk tenant commonly holds several.
4. **Attach employment.** `GET /employees/{id}/jobs` returns the job history for a person —
   this, not the employee record, is where contract type, cost centre and dates live. Use
   `GET /employees/{id}/subordinates` to build reporting lines.
5. **Resolve titles.** `GET /roles` and `GET /role_families` give the job-title taxonomy that
   the job records reference by id.

## Conventions that will bite you

- **Pagination**: `page` / `page_size` in, `pagination.{next,previous,count,page,totalPages}`
  out. See `conventions/buk-conventions.yml`.
- **No rate limit is documented** and no operation declares a `429`. Throttle yourself
  conservatively rather than discovering the limit in production.
- **Errors carry no code.** You get an HTTP status and a free-text message, in Spanish or
  English depending on the operation. Branch on status only — see `errors/buk-problem-types.yml`.
- **No idempotency.** This skill is read-only, so that does not apply here, but it does to the
  write skills.
- **Country variants differ in fields, not paths.** All five countries expose the same 151
  paths; the payload definitions differ. If you sync more than one country, hold a schema per
  country.

## Keeping it fresh

Do not poll the whole roster. Configure the Buk webhook URL and subscribe to
`employee_create`, `employee_update`, `job_hire`, `job_movement` and `job_termination`, then
re-read only the changed record. See `skills/buk-consume-buk-webhooks.md`.
