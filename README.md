# Enphase Energy

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

Enphase Energy is a Petaluma, California home-energy technology manufacturer and the dominant supplier of solar microinverters in the United States, shipping IQ Microinverters, IQ Batteries, IQ EV Chargers and the Envoy/IQ Gateway that ties them together through the Enlighten cloud. It sits on the DER side of the energy value chain rather than the utility side: it does not own meters, sell electricity, or operate a grid, so no consumer energy data mandate reaches it — there is no Green Button, ESPI or NAESB implementation anywhere in its developer surface, and the United States has no compulsory retail energy data right to designate it under. Its API posture is nevertheless unusually open for this sector. The Enphase Developer Portal at developer-v4.enphase.com is a genuine self-serve 3scale portal where anyone can register, create an application and subscribe to a free Watt plan, and it publishes three complete, anonymously downloadable machine-readable contracts covering 124 paths and 148 operations. The split that defines Enphase is consumer-data-open, market-data-closed: a third-party developer can retrieve an individual homeowner's site production, consumption, battery and EV charger telemetry through documented OAuth 2.0 authorization-code flows with the system owner's explicit approval, but Enphase publishes no open grid, wholesale market or system-wide generation data of any kind. Access is tiered — self-serve for monitoring, application-approval for installer commissioning (10+ installations required), and partner-only for the Virtual Power Plant API, which is the one place a real standard appears: OCPP 1.6 for EV charger control against third-party CSMS platforms.

**Areas:** Energy · United States · Solar · DER · Renewables · Battery Storage · EV Charging · Demand Response · Virtual Power Plant · Grid Services · Microinverters · Home Energy Management

## Enphase Energy on APIs.io

Everything profiled for Enphase Energy is published on APIs.io rather than in this repository. Start at the provider page — **[apis.io/providers/enphase/](https://apis.io/providers/enphase/)** — or go straight to one of the APIs or properties below.

### APIs (31)

- [Enphase Energy Activations API](https://apis.io/apis/enphase/enphase-activations-api/) — The Activations API from Enphase Energy — 5 operation(s) for activations.
- [Enphase Energy Applications API](https://apis.io/apis/enphase/enphase-applications-api/) — Applications API
- [Enphase Energy Arrays API](https://apis.io/apis/enphase/enphase-arrays-api/) — The Arrays API from Enphase Energy — 1 operation(s) for arrays.
- [Enphase Energy Auth API](https://apis.io/apis/enphase/enphase-auth-api/) — Auth Controller
- [Enphase Energy Companies API](https://apis.io/apis/enphase/enphase-companies-api/) — The Companies API from Enphase Energy — 4 operation(s) for companies.
- [Enphase Energy Device Level Monitoring API](https://apis.io/apis/enphase/enphase-device-level-monitoring-api/) — The Device Level Monitoring API from Enphase Energy — 7 operation(s) for device level monitoring.
- [Enphase Energy Estimate API](https://apis.io/apis/enphase/enphase-estimate-api/) — The Estimate API from Enphase Energy — 1 operation(s) for estimate.
- [Enphase Energy EV Charger Control API](https://apis.io/apis/enphase/enphase-ev-charger-control-api/) — The EV Charger Control API from Enphase Energy — 2 operation(s) for ev charger control.
- [Enphase Energy EV Charger Monitoring API](https://apis.io/apis/enphase/enphase-ev-charger-monitoring-api/) — The EV Charger Monitoring API from Enphase Energy — 6 operation(s) for ev charger monitoring.
- [Enphase Energy Events API](https://apis.io/apis/enphase/enphase-events-api/) — Events API
- [Enphase Energy Forecast API](https://apis.io/apis/enphase/enphase-forecast-api/) — Forecast API (Contact us if you are interested in using this endpoint)
- [Enphase Energy Grid Profiles API](https://apis.io/apis/enphase/enphase-grid-profiles-api/) — The Grid Profiles API from Enphase Energy — 1 operation(s) for grid profiles.
- [Enphase Energy Home Owner API](https://apis.io/apis/enphase/enphase-home-owner-api/) — The Home Owner API from Enphase Energy — 1 operation(s) for home owner.
- [Enphase Energy Manage VPPs API](https://apis.io/apis/enphase/enphase-manage-vpps-api/) — Manage VPPs API
- [Enphase Energy Meters API](https://apis.io/apis/enphase/enphase-meters-api/) — The Meters API from Enphase Energy — 2 operation(s) for meters.
- [Enphase Energy Programs API](https://apis.io/apis/enphase/enphase-programs-api/) — Programs API
- [Enphase Energy Pv Manufacturers API](https://apis.io/apis/enphase/enphase-pvmanufacturers-api/) — The PvManufacturers API from Enphase Energy — 1 operation(s) for pvmanufacturers.
- [Enphase Energy Pv Models API](https://apis.io/apis/enphase/enphase-pvmodels-api/) — The PvModels API from Enphase Energy — 1 operation(s) for pvmodels.
- [Enphase Energy Site Level Consumption Monitoring API](https://apis.io/apis/enphase/enphase-site-level-consumption-monitoring-api/) — The Site Level Consumption Monitoring API from Enphase Energy — 11 operation(s) for site level consumption monitoring.
- [Enphase Energy Site Level Production Monitoring API](https://apis.io/apis/enphase/enphase-site-level-production-monitoring-api/) — The Site Level Production Monitoring API from Enphase Energy — 5 operation(s) for site level production monitoring.
- [Enphase Energy Streaming APIs API](https://apis.io/apis/enphase/enphase-streaming-apis-api/) — The Streaming APIs API from Enphase Energy — 1 operation(s) for streaming apis.
- [Enphase Energy System and Device Configuration API](https://apis.io/apis/enphase/enphase-system-and-device-configuration-api/) — System and Device Configuration API
- [Enphase Energy System Configurations API](https://apis.io/apis/enphase/enphase-system-configurations-api/) — The System Configurations API from Enphase Energy — 4 operation(s) for system configurations.
- [Enphase Energy System Details And Telemetry API](https://apis.io/apis/enphase/enphase-system-details-and-telemetry-api/) — System Details And Telemetry API
- [Enphase Energy System Details API](https://apis.io/apis/enphase/enphase-system-details-api/) — The System Details API from Enphase Energy — 12 operation(s) for system details.
- [Enphase Energy Tariff API](https://apis.io/apis/enphase/enphase-tariff-api/) — The Tariff API from Enphase Energy — 1 operation(s) for tariff.
- [Enphase Energy Users API](https://apis.io/apis/enphase/enphase-users-api/) — The Users API from Enphase Energy — 4 operation(s) for users.
- [Enphase Enlighten Commissioning API](https://apis.io/apis/enphase/enphase-enlighten-commissioning-api/) — The Commissioning API is the installer-facing companion to the Monitoring API. Available to Partner-plan customers (qualifying installers with 10+…
- [Enphase VPP API](https://apis.io/apis/enphase/enphase-enlighten-vpp-api/) — The Virtual Power Plant (VPP) API allows energy aggregators and utilities to create and manage VPPs that monitor, forecast, and control large fleets of…
- [Enphase Energy Device Level Production Monitoring API](https://apis.io/apis/enphase/enphase-device-level-production-monitoring-api/) — The Device Level Production Monitoring API from Enphase Energy — 1 operation(s) for device level production monitoring.
- [Enphase Energy Systems API](https://apis.io/apis/enphase/enphase-systems-api/) — The Systems API from Enphase Energy — 13 operation(s) for systems.

### Published properties

Each property below is a page on APIs.io carrying the machine-readable artifact and what it says.

#### AsyncAPI (1)

Event-driven and webhook contracts.

- [Enphase Enlighten Live Status Stream](https://apis.io/asyncapis/enphase/enphase-live-status-asyncapi/)

#### Event channels (1)

Individual events and webhooks the provider emits.

- [/api/v4/systems/{system_id}/live_data](https://apis.io/channels/enphase/api-v4-systems-system-id-live-data/)

#### MCP servers (1)

Model Context Protocol servers that expose the API to agents.

- [enphase-mcp.yml](https://apis.io/servers/enphase/enphase-mcp-yml/)

#### Agentic access (1)

Which operations an agent can call, which act, and which need a human in the loop.

- [Enphase Agentic Access](https://apis.io/agentic-access/enphase/enphase-agentic-access/)

#### Collections (3)

Postman and Open Collection request collections.

- [Commissioning API](https://apis.io/collections/enphase/open-enphase-commissioning-api/)
- [Monitoring API](https://apis.io/collections/enphase/open-enphase-monitoring-api/)
- [API Reference](https://apis.io/collections/enphase/open-enphase-vpp-api/)

#### Overlays (3)

OpenAPI overlays, including conversational phrasing for each operation.

- [Enphase Commissioning Overlay](https://apis.io/overlays/enphase/enphase-commissioning-overlay/)
- [Enphase Monitoring Overlay](https://apis.io/overlays/enphase/enphase-monitoring-overlay/)
- [Enphase Vpp Overlay](https://apis.io/overlays/enphase/enphase-vpp-overlay/)

#### Security (3)

Authentication, trust centre, and vulnerability disclosure.

- [Enphase Authentication](https://apis.io/security/enphase/enphase-authentication/)
- [Enphase Domain Security](https://apis.io/security/enphase/enphase-domain-security/)
- [Enphase Vulnerability Disclosure](https://apis.io/security/enphase/enphase-vulnerability-disclosure/)

#### OAuth scopes (1)

The permissions the API asks for.

- [Enphase Scopes](https://apis.io/scopes/enphase/enphase-scopes/)

#### Plans and pricing (1)

Published plans, tiers and prices.

- [Enphase Plans](https://apis.io/plans/enphase/enphase-plans/)

#### Rate limits (1)

Published request limits.

- [Enphase Rate Limits](https://apis.io/rate-limits/enphase/enphase-rate-limits/)

## Where to find this API

Links to the company's own pages. This repository publishes no copy of their specifications — the canonical document is theirs and lives at the URLs below.

- [Website](https://enphase.com)
- [Documentation](https://developer-v4.enphase.com/docs/quickstart.html)
- [Getting started](https://developer-v4.enphase.com/docs/quickstart.html)
- [API reference](https://developer-v4.enphase.com/docs/monitoring_api)
- [Pricing](https://developer-v4.enphase.com/developer-plans)
- [Sign up](https://developer-v4.enphase.com/signup)
- [Support](https://developer-v4.enphase.com/docs/support)
- [Changelog](https://developer-v4.enphase.com/docs/release_notes)
- [Blog](https://newsroom.enphase.com/newsroom)
- [Security](https://enphase.com/cybersecurity)
- [Terms of service](https://enphase.com/legal/terms-of-service)
- [Privacy policy](https://enphase.com/legal/privacy-policy)
- [GitHub](https://github.com/enphase)

## API Evangelist rating

**Kin Score 65.2** — strong · rubric 0.25.0 · scored 2026-10-23

| Facet | Score |
|---|---|
| Discoverability | 78.6 |
| Contract quality | 56.7 |
| Contract governance | 18.2 |
| Operational transparency | 68.4 |
| Developer ergonomics | 63.2 |
| Access clarity | 76.3 |

**Agent readiness 35.9** — agent-ready

| Agent-readiness dimension | Result |
|---|---|
| Spec Presence | yes |
| Agentic Access | derived (partial credit) |
| Reversibility Documented | verified |
| MCP Server | — |
| Auth Clarity | bearer (partial credit) |
| Idempotency | — |
| Error Semantics | verified |
| OpenAPI Examples | verified |
| Rate Limit Signal | documented (partial credit) |
| Event Surface Described | derived (partial credit) |
| Agent Skills | derived (partial credit) |
| Well Known Catalog | — |
| Consent Identity | — |
| Agent Card | — |
| Dry Run Mode | — |
| Delegated Identity | — |
| Protected Resource Metadata | — |
| Dynamic Client Registration | — |
| Agentic Commerce | — |
| Pagination Ratio | — |
| Operation Distinctiveness | mostly |

**Regulatory alignment 45.9** — Energy & Utilities

The rubric is published at [github.com/api-evangelist/kin-score](https://github.com/api-evangelist/kin-score). The per-check breakdown behind these numbers — which checks were earned, partial or missed — along with score history and how this provider compares to its peers, is available at [apis.io/providers/enphase/](https://apis.io/providers/enphase/).

## How this profile is made

API Evangelist profiles a company's public API surface the way a developer would find it: the website, developer portal and documentation, the specifications it publishes, its public repositories, and its pricing, status and changelog pages. From that it derives the properties above — contracts split per API, workflows, schemas, collections, governance rules, plans and rate limits — and scores them against the published [Kin Score rubric](https://github.com/api-evangelist/kin-score).

The artifacts are published on [APIs.io](https://apis.io), not in this repository. This repository is the public record for Enphase Energy: the place to say something is wrong, missing or out of date, and to ask for a re-score or a removal.

## Open an issue

- **Something about this listing** — a wrong description, a missing API, a stale artifact or a question about the rating: [open an issue on this repository](https://github.com/api-evangelist/enphase/issues/new).
- **A new API, or one that is not in the catalog yet** — [submit it on APIs.io](https://apis.io/add/).
- **Anything else** — [the APIs.io inbox](https://github.com/api-search/inbox/issues/new) or [info@apievangelist.com](mailto:info@apievangelist.com).
