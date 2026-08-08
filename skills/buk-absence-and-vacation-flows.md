---
name: buk-absence-and-vacation-flows
description: Create, read and reconcile vacations, medical leave, permissions and unexcused absences in Buk, including the vacation balance and policy definitions.
api: buk:data-access-api
generated: '2026-08-08'
method: generated
source: openapi/buk-data-access-api-chile-openapi.yml
operations:
- GET /vacations
- GET /vacations/{id}
- GET /vacations/requested
- GET /vacations/business_days
- POST /vacations
- DELETE /vacations
- GET /vacation_definitions
- GET /employees/{id}/vacation_definitions
- POST /employees/{id}/vacation_definitions
- DELETE /employees/{id}/vacation_definitions/{code}
- GET /employees/{id}/vacations_available
- GET /employees/{id}/earned_vacations
- GET /accounting/vacations/balance
- GET /absences
- GET /absences/absence
- GET /absences/absence/{id}
- POST /absences/absence
- DELETE /absences/absence/{id}
- GET /absences/absence/types
- POST /absences/absence/types
- GET /absences/licence
- GET /absences/licence/{id}
- POST /absences/licence
- DELETE /absences/licence/{id}
- GET /absences/licence/types
- GET /absences/permission
- GET /absences/permission/{id}
- POST /absences/permission
- DELETE /absences/permission/{id}
- GET /absences/permission/types
- POST /absences/permission/types
- GET /employees/absences/absences
- GET /employees/absences/licences
- GET /employees/absences/permissions
- GET /holidays
---

# Time off in Buk — vacations, leave, permissions and absences

Buk models four distinct things that a naive integration collapses into one. Keep them apart.

| Concept | Path family | What it is |
|---|---|---|
| Vacation | `/vacations` | Accrued paid leave, drawn against a balance |
| Licence (licencia) | `/absences/licence` | Medical leave, usually externally certified |
| Permission (permiso) | `/absences/permission` | Authorised time off that is not vacation |
| Absence (inasistencia) | `/absences/absence` | Unexcused absence |

`GET /absences` is the combined read across the leave families.

## Auth and scope

`auth_token` header. Reads need **Lectura** on the relevant entity; the `POST` and `DELETE`
flows need **Lectura y Modificación**.

## Vacations

1. **Check the balance before requesting.** `GET /employees/{id}/vacations_available` and
   `GET /employees/{id}/earned_vacations` give what the employee actually has.
2. **Compute the working days.** `GET /vacations/business_days` — do not calculate this
   yourself. Combine with `GET /holidays` for the tenant's holiday calendar.
3. **Create.** `POST /vacations`. **Read the pending queue** with `GET /vacations/requested`,
   and a single record with `GET /vacations/{id}`.
4. **Remove.** `DELETE /vacations`. Note this is a collection-level delete taking the target in
   the request, not `DELETE /vacations/{id}` — check the parameters before you call it.
5. **Policy.** `GET /vacation_definitions` is the tenant-wide policy set;
   `GET|POST /employees/{id}/vacation_definitions` and
   `DELETE /employees/{id}/vacation_definitions/{code}` attach or detach a policy per employee.
6. **Provision.** `GET /accounting/vacations/balance` gives the accounting-side vacation
   liability — the number finance cares about.

## Leave, permissions and absences

Each of the three families follows the same shape, which makes them easy to write once and
parameterise:

- `GET /absences/{family}` — list, `GET /absences/{family}/{id}` — read one
- `POST /absences/{family}` — create, `DELETE /absences/{family}/{id}` — remove one
- `GET /absences/{family}/types` — the type catalogue for that family
- `POST /absences/{family}/types` — create a type (permission and absence only)
- `DELETE /absences/{family}` — collection-level delete

where `{family}` is `licence`, `permission` or `absence`. The employee-scoped read is
`GET /employees/absences/{licences|permissions|absences}`.

## Rules you must respect

- **No idempotency.** A retried `POST /vacations` books the same leave twice against the same
  balance. Re-read `GET /vacations` for the employee and date range before retrying.
- **`vacation_status` only appears on the webhook**, in English (`approved`, `submitted`,
  `rejected`), not in the create response. If you need approval state, subscribe to the
  webhook — see `skills/buk-consume-buk-webhooks.md`.
- **The delete semantics are inconsistent** across the family: some are `/{id}`, some are
  collection-level. Read the parameters per operation rather than generalising.
- **Errors are free text** and mixed Spanish/English within the same contract. Branch on HTTP
  status; see `errors/buk-problem-types.yml`.
