---
name: buk-run-and-read-payroll
description: Drive a Buk payroll period — create and read processes, pull payroll detail and payslip PDFs, and export the accounting centralisation into a ledger.
api: buk:data-access-api
generated: '2026-08-08'
method: generated
source: openapi/buk-data-access-api-chile-openapi.yml
operations:
- GET /process_periods
- GET /process
- GET /process/{id}
- POST /process
- DELETE /process/{id}
- GET /payroll_detail/month
- GET /payroll_detail/semi_month
- GET /payroll_detail/week
- GET /employees/{employee_id}/payroll_detail
- GET /employees/{id}/statements/{year}-{month}.pdf
- GET /accounting
- GET /accounting/export
- GET /accounting/export_detail
- GET /accounting/export_period
- GET /accounting/export_process_differences
- GET /accounting_structure/structures
- GET /accounting_structure/assignments
- GET /accounting_structure/export
- GET /ledger_account
- GET /items
- POST /assigns
- PATCH /assigns/{id}
- DELETE /assigns/{id}
- POST /assigns/{id}/terminate
- GET /employees/{id}/assigns
- POST /employees/{employee_id}/payment_data/{period_id}
---

# Run and read a Buk payroll cycle

Payroll is the reason Buk is the system of record. This skill covers the monthly cycle from
period through settlement to the accounting export.

## Auth and scope

`auth_token` header with **Lectura y Modificación** on the process and item entities for the
write steps; **Lectura** is enough for everything under *Reading the results* and *Accounting*.

## The cycle

1. **Find the period.** `GET /process_periods` lists the payroll periods the tenant has open.
   Everything downstream is keyed on a period.
2. **List or create the process.** `GET /process` lists processes; `GET /process/{id}` reads
   one; `POST /process` creates one. `DELETE /process/{id}` only removes processes of type
   *Liquidación* — the contract documents a 409 for anything else, so do not build a generic
   delete.
3. **Load the variable inputs.** Recurring and one-off pay items are assignments:
   `POST /assigns` to create, `PATCH /assigns/{id}` to change, `POST /assigns/{id}/terminate`
   to end a recurring assignment, `DELETE /assigns/{id}` to remove one, and
   `GET /employees/{id}/assigns` to read what an employee currently carries. `GET /items` is the
   item catalogue those assignments reference.

## Reading the results

- `GET /payroll_detail/month`, `GET /payroll_detail/semi_month` and `GET /payroll_detail/week`
  return settlement detail at the tenant's pay frequency. Pick the one that matches the
  tenant — they are not interchangeable.
- `GET /employees/{employee_id}/payroll_detail` narrows it to one person.
- `GET /employees/{id}/statements/{year}-{month}.pdf` returns the payslip **as a PDF**. Note the
  contract's `produces` includes `application/pdf` — set `Accept` accordingly and do not try to
  JSON-decode the body.
- `POST /employees/{employee_id}/payment_data/{period_id}` synchronises payment data for a
  period.

## Accounting

- `GET /accounting` plus `GET /accounting/export`, `/export_detail` and `/export_period` produce
  the centralisation for the ledger.
- `GET /accounting/export_process_differences` and
  `GET /accounting_structure/export_process_differences` are the reconciliation endpoints —
  run them before you post to the ledger, not after.
- `GET /accounting_structure/structures`, `/assignments` and `/export` describe the mapping
  Buk uses; `GET /ledger_account` gives the chart of accounts.
- `GET /accounting/vacations/balance` gives the vacation provision, which usually needs to be
  booked alongside the payroll journal.

## Rules you must respect

- **No idempotency.** `POST /process` and `POST /assigns` retried after a timeout create
  duplicates that will land in someone's pay. Re-read with `GET /process` before every retry.
- **No status page and no SLA.** If Buk is down mid-cycle you will find out from your own
  monitoring, not theirs — see `lifecycle/buk-lifecycle.yml`. Build your own health check
  against a cheap read like `GET /versions`.
- **No 429 documented.** Do not parallelise the export endpoints.
- **The period is the boundary.** Once a settlement is closed, corrections go through
  retroactive items, not through re-running the process.
