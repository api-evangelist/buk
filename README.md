# Buk

<!-- API-EVANGELIST-PROVENANCE:BEGIN -->
> ### About this repository
>
> **This is not our API.** This repository is an independent, third-party profile of a company's
> **publicly available** API surface, maintained by [API Evangelist](https://apievangelist.com).
> API Evangelist does not operate, host, resell, or support this company's APIs, and is not
> affiliated with or endorsed by the company unless stated on the profile.
>
> **Where the information came from.** Everything here is assembled from material a member of the
> public can reach with a browser and no credentials — the company's own website, developer portal
> and documentation, the specifications it publishes for public use (OpenAPI, AsyncAPI, JSON Schema,
> `apis.json`, `llms.txt` and similar), its public repositories, and its public status, pricing and
> changelog pages. **Nothing here is obtained by breaching a system, defeating an access control, or
> using credentials of any kind.**
>
> **The rating is an independent assessment.** The Kin Score and Agent Readiness rating are
> independently calculated scores of a company's *public* API artifacts, produced by API Evangelist
> against a published rubric. They are not certifications, endorsements, security assessments, or
> audits, and they score published artifacts — not the quality, safety, or security of the software.
>
> **Corrections, re-scores, and removal are free.** No partnership, contract, or purchase is
> required, and you do not need to justify the request.
>
> - **Something wrong?** Open an issue on this repository, or email
>   [info@apievangelist.com](mailto:info@apievangelist.com).
> - **Published something new?** Ask for a re-score and we will re-run the rating.
> - **Want the listing taken down?** Say so and we will honor it. The profile is reduced to your
>   company name, a factual description, and a link to your own site, and the company is recorded as
>   **unrated** — never scored zero for having asked.
>
> **Response times.** Acknowledgement within **one business day**; removal or restriction within
> **two business days**; corrections and re-scores within **five business days**.
>
> **Not from the company, and here with a question?** You are welcome here — we would rather be the
> front line and point you the right way than have a good report go nowhere. What this repository
> can answer is narrow, though, so it is worth knowing who you are actually looking for:
>
> - **A question about how the API works, an account, billing, or a bug in the service** — that is
>   the company's own support, not us. We profile this API; we do not operate it and cannot see
>   your account.
> - **A bug in an open-source project we only catalog** — file it on that project's own repository.
>   This has happened with a real and correct bug report that reached us instead of the people who
>   could fix it, which helped nobody.
> - **Anything about this listing itself** — the description, the tags, the rating, a missing or
>   wrong artifact — is ours. Open an issue here.
> - **Not sure, or something general about API Evangelist or APIs.io** — open an issue on the
>   [APIs.io Inbox](https://github.com/api-search/inbox) and we will route it.
>
> **This repository contains no software, and we will never ask you to download anything.** There is
> no build, release, installer, or binary here — only text and machine-readable API descriptions, so
> there is nothing here that can be "corrupt" or need "repairing". Any issue, comment, or email
> claiming otherwise and offering a download link is not from us and is hostile. Do not follow the
> link; it is a lure. Report it to GitHub and, if you like, tell us at
> [info@apievangelist.com](mailto:info@apievangelist.com) so we can take it down.
>
> **On a security or compliance team?** Email
> [info@apievangelist.com](mailto:info@apievangelist.com) with *security* in the subject line and
> you will get a person, not a form. We will tell you exactly which public URLs this profile was
> built from so your team can see the same surface we did, and we will take the listing down on
> request while you work through it.
>
> Full detail: **[Where this data comes from](https://apievangelist.com/about/where-our-data-comes-from)**
<!-- API-EVANGELIST-PROVENANCE:END -->

Buk (Buk SpA, Santiago, Chile) is a Latin American HR and payroll platform — "software de gestión de personas" — covering payroll and settlement calculation, employee records, contracts and digital signature, time and attendance, absence and vacation management, benefits and salary advances, recruitment, onboarding, training and performance. Founded in 2017 and bootstrapped for its first five years, it raised a $50M Series A led by Greenoaks and SoftBank in 2021 and a further $50M Series B in 2024, and now operates country editions for Chile, Peru, Mexico, Colombia and Brazil. Its API posture is unusual for the region and unusually good in one specific way: every customer tenant serves a complete, unauthenticated, machine-readable Swagger 2.0 contract for the Buk Data Access API at https://{tenant}.buk.cl/api/{country}/{language}/api_docs — 151 paths and 206 operations, in five country variants and three languages — behind a Swagger UI at /apidocs, alongside a documented webhook catalog. Two further contracts for Buk Asistencia (attendance) and its vendor-agnostic biometric clocking ingestion endpoint are published publicly on SwaggerHub under the BUKASISTENCIA account. What is missing is the developer-program scaffolding around those contracts: there is no developer portal, no first-party SDK, no CLI, no Postman workspace, no status page, no sandbox, no /.well-known/ surface, no MCP server, no operationId on any of 206 operations, and no documented rate limit or 429 response. The contract is public; the program around it is not built yet.

**Areas:** Human Resources · Payroll · Time and Attendance · Benefits · Recruiting · Performance Management · Employee Records · Latin America · Chile · Software-as-a-Service · Webhook · Employee Benefits

## Buk on APIs.io

Everything profiled for Buk is published on APIs.io rather than in this repository. Start at the provider page — **[apis.io/providers/buk/](https://apis.io/providers/buk/)** — or go straight to one of the APIs or properties below.

### APIs (63)

- [Buk Absences requests API](https://apis.io/apis/buk/buk-absences-requests-api/) — The Absences requests API from Buk — 4 operation(s) for absences requests.
- [Buk Accounting Structures API](https://apis.io/apis/buk/buk-accounting-structures-api/) — The Accounting Structures API from Buk — 4 operation(s) for accounting structures.
- [Buk Applicant API](https://apis.io/apis/buk/buk-applicant-api/) — The Applicant API from Buk — 1 operation(s) for applicant.
- [Buk Application API](https://apis.io/apis/buk/buk-application-api/) — The Application API from Buk — 2 operation(s) for application.
- [Buk Benefits API](https://apis.io/apis/buk/buk-benefits-api/) — The Benefits API from Buk — 3 operation(s) for benefits.
- [Buk Capacitaciones API](https://apis.io/apis/buk/buk-capacitaciones-api/) — The Capacitaciones API from Buk — 2 operation(s) for capacitaciones.
- [Buk Cargos API](https://apis.io/apis/buk/buk-cargos-api/) — The Cargos API from Buk — 1 operation(s) for cargos.
- [Buk Centralized accounting API](https://apis.io/apis/buk/buk-centralized-accounting-api/) — The Centralized accounting API from Buk — 7 operation(s) for centralized accounting.
- [Buk Centro de costo API](https://apis.io/apis/buk/buk-centro-de-costo-api/) — The Centro de costo API from Buk — 4 operation(s) for centro de costo.
- [Buk Clockings API](https://apis.io/apis/buk/buk-clockings-api/) — Attendance clocking ingestion from biometric devices.
- [Buk Colaboradores API](https://apis.io/apis/buk/buk-colaboradores-api/) — The Colaboradores API from Buk — 23 operation(s) for colaboradores.
- [Buk Créditos API](https://apis.io/apis/buk/buk-cr-ditos-api/) — The Créditos API from Buk — 5 operation(s) for créditos.
- [Buk Days worked API](https://apis.io/apis/buk/buk-days-worked-api/) — The Days worked API from Buk — 2 operation(s) for days worked.
- [Buk Documents API](https://apis.io/apis/buk/buk-documents-api/) — The Documents API from Buk — 5 operation(s) for documents.
- [Buk Empresas API](https://apis.io/apis/buk/buk-empresas-api/) — The Empresas API from Buk — 1 operation(s) for empresas.
- [Buk Empresas Variable Records API](https://apis.io/apis/buk/buk-empresas-variable-records-api/) — The Empresas Variable Records API from Buk — 1 operation(s) for empresas variable records.
- [Buk Evaluations API](https://apis.io/apis/buk/buk-evaluations-api/) — The Evaluations API from Buk — 3 operation(s) for evaluations.
- [Buk Feriados API](https://apis.io/apis/buk/buk-feriados-api/) — The Feriados API from Buk — 1 operation(s) for feriados.
- [Buk Grupo Familiar API](https://apis.io/apis/buk/buk-grupo-familiar-api/) — The Grupo Familiar API from Buk — 1 operation(s) for grupo familiar.
- [Buk Grupos API](https://apis.io/apis/buk/buk-grupos-api/) — The Grupos API from Buk — 2 operation(s) for grupos.
- [Buk Horas extras API](https://apis.io/apis/buk/buk-horas-extras-api/) — The Horas extras API from Buk — 1 operation(s) for horas extras.
- [Buk Horas no trabajadas API](https://apis.io/apis/buk/buk-horas-no-trabajadas-api/) — The Horas no trabajadas API from Buk — 3 operation(s) for horas no trabajadas.
- [Buk Inasistencia API](https://apis.io/apis/buk/buk-inasistencia-api/) — The Inasistencia API from Buk — 1 operation(s) for inasistencia.
- [Buk Items API](https://apis.io/apis/buk/buk-items-api/) — The Items API from Buk — 4 operation(s) for items.
- [Buk Job Titles API](https://apis.io/apis/buk/buk-job-titles-api/) — The Job Titles API from Buk — 3 operation(s) for job titles.
- [Buk Jobs API](https://apis.io/apis/buk/buk-jobs-api/) — The Jobs API from Buk — 6 operation(s) for jobs.
- [Buk KP Is API](https://apis.io/apis/buk/buk-kpis-api/) — The KPIs API from Buk — 3 operation(s) for kpis.
- [Buk Labores API](https://apis.io/apis/buk/buk-labores-api/) — The Labores API from Buk — 1 operation(s) for labores.
- [Buk Leaves API](https://apis.io/apis/buk/buk-leaves-api/) — The Leaves API from Buk — 4 operation(s) for leaves.
- [Buk Localidades API](https://apis.io/apis/buk/buk-localidades-api/) — The Localidades API from Buk — 2 operation(s) for localidades.
- [Buk Lugares de Trabajo API](https://apis.io/apis/buk/buk-lugares-de-trabajo-api/) — The Lugares de Trabajo API from Buk — 1 operation(s) for lugares de trabajo.
- [Buk Nómina Colaborador API](https://apis.io/apis/buk/buk-n-mina-colaborador-api/) — The Nómina Colaborador API from Buk — 1 operation(s) for nómina colaborador.
- [Buk Non-Worked Hours API](https://apis.io/apis/buk/buk-non-worked-hours-api/) — The Non-Worked Hours API from Buk — 2 operation(s) for non-worked hours.
- [Buk Notas API](https://apis.io/apis/buk/buk-notas-api/) — The Notas API from Buk — 1 operation(s) for notas.
- [Buk Overtime API](https://apis.io/apis/buk/buk-overtime-api/) — The Overtime API from Buk — 3 operation(s) for overtime.
- [Buk Payment documents API](https://apis.io/apis/buk/buk-payment-documents-api/) — The Payment documents API from Buk — 5 operation(s) for payment documents.
- [Buk People API](https://apis.io/apis/buk/buk-people-api/) — The People API from Buk — 1 operation(s) for people.
- [Buk Períodos API](https://apis.io/apis/buk/buk-per-odos-api/) — The Períodos API from Buk — 1 operation(s) for períodos.
- [Buk Postulante API](https://apis.io/apis/buk/buk-postulante-api/) — The Postulante API from Buk — 5 operation(s) for postulante.
- [Buk Procesos API](https://apis.io/apis/buk/buk-procesos-api/) — The Procesos API from Buk — 2 operation(s) for procesos.
- [Buk Productos API](https://apis.io/apis/buk/buk-productos-api/) — The Productos API from Buk — 1 operation(s) for productos.
- [Buk Áreas API](https://apis.io/apis/buk/buk-reas-api/) — The Áreas API from Buk — 5 operation(s) for áreas.
- [Buk Recintos API](https://apis.io/apis/buk/buk-recintos-api/) — The Recintos API from Buk — 3 operation(s) for recintos.
- [Buk Registro de asistencia API](https://apis.io/apis/buk/buk-registro-de-asistencia-api/) — The Registro de asistencia API from Buk — 4 operation(s) for registro de asistencia.
- [Buk Registros de Trabajo API](https://apis.io/apis/buk/buk-registros-de-trabajo-api/) — The Registros de Trabajo API from Buk — 2 operation(s) for registros de trabajo.
- [Buk Selection process API](https://apis.io/apis/buk/buk-selection-process-api/) — The Selection process API from Buk — 1 operation(s) for selection process.
- [Buk Substitutions API](https://apis.io/apis/buk/buk-substitutions-api/) — The Substitutions API from Buk — 2 operation(s) for substitutions.
- [Buk Synchronization of payment data API](https://apis.io/apis/buk/buk-synchronization-of-payment-data-api/) — The Synchronization of payment data API from Buk — 1 operation(s) for synchronization of payment data.
- [Buk Tarifas API](https://apis.io/apis/buk/buk-tarifas-api/) — The Tarifas API from Buk — 1 operation(s) for tarifas.
- [Buk Ítems API](https://apis.io/apis/buk/buk-tems-api/) — The Ítems API from Buk — 1 operation(s) for ítems.
- [Buk Termination processes API](https://apis.io/apis/buk/buk-termination-processes-api/) — The Termination processes API from Buk — 1 operation(s) for termination processes.
- [Buk Time Off Leaves API](https://apis.io/apis/buk/buk-time-off-leaves-api/) — The Time Off Leaves API from Buk — 1 operation(s) for time off leaves.
- [Buk Turnos API](https://apis.io/apis/buk/buk-turnos-api/) — The Turnos API from Buk — 1 operation(s) for turnos.
- [Buk Unexcused absence API](https://apis.io/apis/buk/buk-unexcused-absence-api/) — The Unexcused absence API from Buk — 4 operation(s) for unexcused absence.
- [Buk Unidades API](https://apis.io/apis/buk/buk-unidades-api/) — The Unidades API from Buk — 1 operation(s) for unidades.
- [Buk Unions API](https://apis.io/apis/buk/buk-unions-api/) — The Unions API from Buk — 3 operation(s) for unions.
- [Buk Users and profiles API](https://apis.io/apis/buk/buk-users-and-profiles-api/) — The Users and profiles API from Buk — 2 operation(s) for users and profiles.
- [Buk Usuarios y perfiles API](https://apis.io/apis/buk/buk-usuarios-y-perfiles-api/) — The Usuarios y perfiles API from Buk — 1 operation(s) for usuarios y perfiles.
- [Buk Vacaciones API](https://apis.io/apis/buk/buk-vacaciones-api/) — The Vacaciones API from Buk — 4 operation(s) for vacaciones.
- [Buk Vacation Policies API](https://apis.io/apis/buk/buk-vacation-policies-api/) — The Vacation Policies API from Buk — 1 operation(s) for vacation policies.
- [Buk Variables of the Empresas API](https://apis.io/apis/buk/buk-variables-of-the-empresas-api/) — The Variables of the Empresas API from Buk — 1 operation(s) for variables of the empresas.
- [Buk Versions API](https://apis.io/apis/buk/buk-versions-api/) — The Versions API from Buk — 1 operation(s) for versions.
- [Buk Workflows API](https://apis.io/apis/buk/buk-workflows-api/) — The Workflows API from Buk — 1 operation(s) for workflows.

### Published properties

Each property below is a page on APIs.io carrying the machine-readable artifact and what it says.

#### AsyncAPI (1)

Event-driven and webhook contracts.

- [Buk Webhooks](https://apis.io/asyncapis/buk/buk-webhooks/)

#### MCP servers (1)

Model Context Protocol servers that expose the API to agents.

- [Candidate MCP tool surface derived from the contracts (Buk publishes no MCP server)](https://apis.io/servers/buk/candidate-mcp-tool-surface-derived-from-the-contracts-buk-publishes-no-mcp-server/)

#### Collections (66)

Postman and Open Collection request collections.

- [Buk Absences requests API](https://apis.io/collections/buk/open-buk-absences-requests-api/)
- [Buk Accounting Structures API](https://apis.io/collections/buk/open-buk-accounting-structures-api/)
- [Buk Applicant API](https://apis.io/collections/buk/open-buk-applicant-api/)
- [Buk Application API](https://apis.io/collections/buk/open-buk-application-api/)
- [Buk Benefits API](https://apis.io/collections/buk/open-buk-benefits-api/)
- [Buk Capacitaciones API](https://apis.io/collections/buk/open-buk-capacitaciones-api/)
- [Buk Cargos API](https://apis.io/collections/buk/open-buk-cargos-api/)
- [Buk Centralized accounting API](https://apis.io/collections/buk/open-buk-centralized-accounting-api/)
- [Buk Centro de costo API](https://apis.io/collections/buk/open-buk-centro-de-costo-api/)
- [Buk Attendance — Biometric Integration Clockings API](https://apis.io/collections/buk/open-buk-clockings-api/)
- [Buk Colaboradores API](https://apis.io/collections/buk/open-buk-colaboradores-api/)
- [Buk Créditos API](https://apis.io/collections/buk/open-buk-cr-ditos-api/)
- [Buk Days worked API](https://apis.io/collections/buk/open-buk-days-worked-api/)
- [Buk Dismissal API](https://apis.io/collections/buk/open-buk-dismissal-api/)
- [Buk Documents API](https://apis.io/collections/buk/open-buk-documents-api/)
- [Buk Empresas API](https://apis.io/collections/buk/open-buk-empresas-api/)
- [Buk Empresas Variable Records API](https://apis.io/collections/buk/open-buk-empresas-variable-records-api/)
- [Buk Evaluations API](https://apis.io/collections/buk/open-buk-evaluations-api/)
- [Buk Feriados API](https://apis.io/collections/buk/open-buk-feriados-api/)
- [Buk Grupo Familiar API](https://apis.io/collections/buk/open-buk-grupo-familiar-api/)
- [Buk Grupos API](https://apis.io/collections/buk/open-buk-grupos-api/)
- [Buk Horas extras API](https://apis.io/collections/buk/open-buk-horas-extras-api/)
- [Buk Horas no trabajadas API](https://apis.io/collections/buk/open-buk-horas-no-trabajadas-api/)
- [Buk Inasistencia API](https://apis.io/collections/buk/open-buk-inasistencia-api/)
- [Buk Items API](https://apis.io/collections/buk/open-buk-items-api/)
- …and 41 more published on APIs.io

#### Overlays (7)

OpenAPI overlays, including conversational phrasing for each operation.

- [Buk Asistencia Api Overlay](https://apis.io/overlays/buk/buk-asistencia-api-overlay/)
- [Buk Attendance Biometrics Api Overlay](https://apis.io/overlays/buk/buk-attendance-biometrics-api-overlay/)
- [Buk Data Access Api Brasil Overlay](https://apis.io/overlays/buk/buk-data-access-api-brasil-overlay/)
- [Buk Data Access Api Chile Overlay](https://apis.io/overlays/buk/buk-data-access-api-chile-overlay/)
- [Buk Data Access Api Colombia Overlay](https://apis.io/overlays/buk/buk-data-access-api-colombia-overlay/)
- [Buk Data Access Api Mexico Overlay](https://apis.io/overlays/buk/buk-data-access-api-mexico-overlay/)
- [Buk Data Access Api Peru Overlay](https://apis.io/overlays/buk/buk-data-access-api-peru-overlay/)

#### Security (3)

Authentication, trust centre, and vulnerability disclosure.

- [Buk Authentication](https://apis.io/security/buk/buk-authentication/)
- [Buk Domain Security](https://apis.io/security/buk/buk-domain-security/)
- [Buk Trust Center](https://apis.io/security/buk/buk-trust-center/)

## Where to find this API

Links to the company's own pages. This repository publishes no copy of their specifications — the canonical document is theirs and lives at the URLs below.

- [Website](https://www.buk.cl/)
- [Documentation](https://demo.buk.cl/apidocs)
- [Getting started](https://supportcenter.buk.cl/hc/es-419/articles/36657679009307-C%C3%B3mo-integrarse-a-Buk-a-trav%C3%A9s-de-API)
- [API reference](https://demo.buk.cl/apidocs)
- [Pricing](https://www.buk.cl/precios)
- [Sign up](https://www.buk.cl/starter)
- [Support](https://supportcenter.buk.cl/hc/es-419)
- [Blog](https://www.buk.cl/blog)
- [Terms of service](https://www.buk.cl/starter/terminos-y-condiciones)
- [Privacy policy](https://www.buk.cl/privacidad)
- [GitHub](https://github.com/bukhr)

## API Evangelist rating

**Kin Score 51.6** — developing · rubric 0.25.0 · scored 2026-10-23

| Facet | Score |
|---|---|
| Discoverability | 78.6 |
| Contract quality | 53.7 |
| Contract governance | 18.2 |
| Operational transparency | 31.6 |
| Developer ergonomics | 49.4 |
| Access clarity | 60.5 |

**Agent readiness 47.0** — agent-ready (gated down from agent-native)

| Agent-readiness dimension | Result |
|---|---|
| Spec Presence | yes |
| Agentic Access | — |
| Reversibility Documented | documented (partial credit) |
| MCP Server | — |
| Auth Clarity | served (partial credit) |
| Idempotency | — |
| Error Semantics | verified |
| OpenAPI Examples | partial |
| Rate Limit Signal | — |
| Event Surface Described | yes |
| Agent Skills | derived (partial credit) |
| Well Known Catalog | — |
| Consent Identity | — |
| Agent Card | — |
| Dry Run Mode | — |
| Delegated Identity | served (partial credit) |
| Protected Resource Metadata | verified |
| Dynamic Client Registration | yes |
| Agentic Commerce | — |
| Pagination Ratio | partial |
| Operation Distinctiveness | mostly |

**Regulatory alignment 29.4** — Employment & Payroll

The rubric is published at [github.com/api-evangelist/kin-score](https://github.com/api-evangelist/kin-score). The per-check breakdown behind these numbers — which checks were earned, partial or missed — along with score history and how this provider compares to its peers, is available at [apis.io/providers/buk/](https://apis.io/providers/buk/).

## How this profile is made

API Evangelist profiles a company's public API surface the way a developer would find it: the website, developer portal and documentation, the specifications it publishes, its public repositories, and its pricing, status and changelog pages. From that it derives the properties above — contracts split per API, workflows, schemas, collections, governance rules, plans and rate limits — and scores them against the published [Kin Score rubric](https://github.com/api-evangelist/kin-score).

The artifacts are published on [APIs.io](https://apis.io), not in this repository. This repository is the public record for Buk: the place to say something is wrong, missing or out of date, and to ask for a re-score or a removal.

## Open an issue

- **Something about this listing** — a wrong description, a missing API, a stale artifact or a question about the rating: [open an issue on this repository](https://github.com/api-evangelist/buk/issues/new).
- **A new API, or one that is not in the catalog yet** — [submit it on APIs.io](https://apis.io/add/).
- **Anything else** — [the APIs.io inbox](https://github.com/api-search/inbox/issues/new) or [info@apievangelist.com](mailto:info@apievangelist.com).
