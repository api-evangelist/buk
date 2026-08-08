---
name: buk-consume-buk-webhooks
description: Receive Buk webhook notifications and reconcile each one back against the Data Access API — the only supported way to stay current without polling.
api: buk:data-access-api
generated: '2026-08-08'
method: generated
source: https://demo.buk.cl/apidocs (Webhooks tab) + openapi/buk-data-access-api-chile-openapi.yml
operations:
- GET /employees/{id}
- GET /employees/{id}/jobs
- GET /areas/{id}
- GET /organization/areas/{id}
- GET /vacations/{id}
- GET /absences/licence/{id}
- GET /absences/permission/{id}
- GET /absences/absence/{id}
- GET /docs/{id}
- GET /employees/{employee_id}/plans/{id}
- GET /employees/{employee_id}/family_responsibilities/{id}
---

# Consume Buk webhooks

Buk webhooks are **notification-only**. The body tells you *that* something changed and *which*
record — never *what* changed. Every handler ends with a read back against the API.

## Configuring the endpoint

An administrator or superadministrator sets this in the Buk UI, not over the API:
*Configuración → Acceso API → Urls Webhooks*. Two separate fields:

- **Webhook Url** — employees, areas, vacations, and licences/absences/permissions.
- **Webhook Documentos Url** — documents requiring signature.

Both must be public `https://` URLs. There is no subscription API and no way to register an
endpoint programmatically.

## The payload

Buk `POST`s JSON with a `data` object. Every event carries:

- `date` — ISO 8601 timestamp of the change
- `event_type` — the event name
- `tenant_url` — which tenant instance emitted it (**you need this**: one integration commonly
  serves many tenants and the payload is otherwise indistinguishable)

plus a resource id field and, on some events, `metadata`.

## The events

| Resource | id field | Events |
|---|---|---|
| Employee | `employee_id` | `employee_create`, `employee_update`, `employee_plan_update`, `employee_responsibility_update`, `job_hire`, `job_termination`, `job_movement` |
| Area | `area_id` | `area_create`, `area_update` |
| Vacation | `vacation_id` | `vacation_create`, `vacation_update`, `vacation_destroy` |
| Licence / Absence / Permission | `{tipo}_id` | `{tipo}_create`, `{tipo}_update`, `{tipo}_destroy` where `{tipo}` is `licence`, `absence` or `permission` |
| Document | `document_id` | `document_create` |

Employee events also carry `employment_status` (`activo`, `pendiente`, `terminado`) and, on
`employee_plan_update` and `employee_responsibility_update`, a `metadata.plan_id` or
`metadata.responsibility_id`. `metadata.relevant_for_bukas` flags whether the change matters to
Buk Asistencia. Vacation events carry `metadata.vacation_status` in English.

## The handler

1. Verify the `tenant_url` maps to a tenant you hold a token for. **This is your only
   authenticity check** — Buk documents no signature, no shared secret and no replay
   protection, so treat the payload as untrusted input and never act on its contents directly.
2. Ack fast (`2xx`), enqueue, and do the read out of band. No retry policy is documented, so
   assume none and do not rely on Buk re-delivering.
3. Read the record back:
   - `employee_*`, `job_*` → `GET /employees/{id}` and `GET /employees/{id}/jobs`
   - `employee_plan_update` → `GET /employees/{employee_id}/plans/{id}`
   - `employee_responsibility_update` → `GET /employees/{employee_id}/family_responsibilities/{id}`
   - `area_*` → `GET /organization/areas/{id}` (or `GET /areas/{id}`)
   - `vacation_*` → `GET /vacations/{id}`
   - `licence_* / permission_* / absence_*` → `GET /absences/{family}/{id}`
   - `document_create` → `GET /docs/{id}`
4. Diff against your own copy before writing downstream.

## Traps

- **`job_movement` fires on a no-op save.** The provider documents it explicitly: opening the
  job form, changing nothing and saving emits the event, as a *touch*. Never treat the event as
  evidence of change — always diff.
- **`{tipo}_destroy` is documented with the same wording as `{tipo}_update`** in the provider's
  own text. Confirm by re-reading: a `404` on the read is your real signal that the record is
  gone.
- **Deletes race the read.** A `*_destroy` followed by an immediate `GET /{id}` will return
  `404`; that is expected, not an error to alert on.
- **No delivery guarantee, no ordering guarantee.** Reconcile with a periodic sweep — an
  incremental `GET /employees?update_start_date=` pass — rather than assuming the stream is
  complete. See `skills/buk-sync-employee-directory.md`.
