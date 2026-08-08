---
name: buk-attendance-and-overtime
description: Read and write attendance across both Buk surfaces — overtime and unworked hours on the Data Access API, and clocking records, shifts and work sites on the Buk Asistencia API.
api: buk:asistencia-api
generated: '2026-08-08'
method: generated
source: openapi/buk-asistencia-api-openapi.yml + openapi/buk-data-access-api-chile-openapi.yml
  + openapi/buk-attendance-biometrics-api-openapi.yml
operations:
- GET /attendances/overtime
- GET /attendances/overtime/{id}
- GET /attendances/overtime/types
- POST /attendances/overtime
- PUT /attendances/overtime
- GET /attendances/non-worked-hours
- GET /attendances/non-worked-hours/{id}
- GET /attendances/non-worked-hours/types
- POST /attendances/non-worked-hours
- PUT /attendances/non-worked-hours
- DELETE /attendances/non-worked-hours/types/{id}
- GET /employees/overtimes
- GET /working_days
- POST /working_days
- DELETE /working_days/{employee_id}/{monthyear}
- GET /recintos
- POST /recintos
- PATCH /recintos/{code}
- GET /informacionRecinto (recinto)
- GET /obtenerNominaColaborador (nomina)
- GET /getAsignacionTurnos (asignacionTurnos)
- GET /obtenerInasistencias (inasistencia)
- GET /obtenerHorasExtras (horasExtras)
- GET /obtenerHorasNoTrabajadas (horasNoTrabajadas)
- GET /v2/asistencia-empresa (asistencia-empresa)
- GET /obtenerRegistroAsistencia (registroAsistencia)
- POST /v2/registrar (registrar)
- POST /inyectarRegistroAsistencia (registroAsistenciaPost)
- POST /v1/clockings (createClocking)
---

# Attendance in Buk — two APIs, two hosts, two header names

Attendance is split across two products with two separate contracts. Getting this wrong is the
most common integration mistake on the Buk surface.

| Surface | Host | Auth header | Contract |
|---|---|---|---|
| Data Access API (overtime, unworked hours, working days, recintos) | `https://{tenant}.buk.cl/api/v1/{country}` | `auth_token` | Swagger 2.0, served from the tenant |
| Buk Asistencia API (clockings, shifts, roster, absences) | `https://app.ctrlit.cl/ctrl/api` (and `app2.ctrlit.cl`) | `token` | OpenAPI 3.0.0 on SwaggerHub |
| Biometric ingestion | `https://zktc.prod.asis.buk.cl/rest` | `x-provider-name` + `x-provider-token` | OpenAPI 3.0.3 on SwaggerHub |

The Asistencia token is **not** self-service: it is requested from the Buk SAC (support) team,
unlike the Data Access token which a tenant administrator issues themselves.

## On the Data Access API

- **Overtime.** `GET /attendances/overtime` to list, `GET /attendances/overtime/{id}` for one,
  `GET /attendances/overtime/types` for the catalogue, `POST /attendances/overtime` to create
  and `PUT /attendances/overtime` to update. `GET /employees/overtimes` is the employee-scoped
  roll-up.
- **Unworked hours.** The same shape under `/attendances/non-worked-hours`, plus
  `DELETE /attendances/non-worked-hours/types/{id}` on the type catalogue.
- **Working days.** `GET /working_days`, `POST /working_days`, and
  `DELETE /working_days/{employee_id}/{monthyear}` — note the composite path key.
- **Work sites.** `GET /recintos`, `POST /recintos`, `PATCH /recintos/{code}` — keyed on
  `code`, not on `id`.

## On the Buk Asistencia API

These operations **do** carry operationIds, unlike the Data Access contract:

- `recinto` — `GET /informacionRecinto`, a paginated list of a company's work sites with name,
  address, comuna, region and country.
- `nomina` — `GET /obtenerNominaColaborador`, the collaborator roster.
- `asignacionTurnos` — `GET /getAsignacionTurnos`, shift assignments.
- `inasistencia` — `GET /obtenerInasistencias`.
- `horasExtras` — `GET /obtenerHorasExtras`; `horasNoTrabajadas` — `GET /obtenerHorasNoTrabajadas`.
- `asistencia-empresa` — `GET /v2/asistencia-empresa`, and `registrar` — `POST /v2/registrar`,
  the current attendance read/write pair.
- `registroAsistencia` / `registroAsistenciaPost` — `GET /obtenerRegistroAsistencia` and
  `POST /inyectarRegistroAsistencia`, the older read and inject pair. Prefer the `/v2/` pair for
  new work; the older two are still documented and still live.

Pagination on Asistencia is explicit: `page` and `page_size`, **maximum 100**, default 25, with
`pagination.{next,previous,count,page,totalPages}` in the response.

## Biometric device ingestion

`POST /v1/clockings` on `https://zktc.prod.asis.buk.cl/rest` is the vendor-agnostic entry point.
A device manufacturer's middleware normalises its own format to this one and posts clockings,
registers devices and syncs biometric templates. Authenticate with the header pair
`x-provider-name` and `x-provider-token`. This is a machine-to-machine endpoint — it is not a
surface to hand to an agent.

## Rules you must respect

- **Three different auth headers across three hosts.** `auth_token`, `token`, and the
  `x-provider-*` pair. Do not share a client.
- **The Asistencia contract documents a 403, not a 401,** for an invalid, expired or missing
  token. Handle both.
- **A 405 is documented** on the Asistencia read endpoints for a non-GET method.
- **No idempotency** on either surface. A retried clocking injection creates a duplicate
  attendance record, which changes someone's paid hours. Re-read
  `GET /obtenerRegistroAsistencia` for the employee and date before retrying.
- **`app.ctrlit.cl` and `app2.ctrlit.cl` send no HSTS** and sit on a domain with no SPF, DMARC,
  CAA or DNSSEC — see `security/buk-domain-security.yml`. Pin TLS on your side.
