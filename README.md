# Enphase Energy (enphase)

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
> **On a security or compliance team?** Email
> [info@apievangelist.com](mailto:info@apievangelist.com) with *security* in the subject line and
> you will get a person, not a form. We will tell you exactly which public URLs this profile was
> built from so your team can see the same surface we did, and we will take the listing down on
> request while you work through it.
>
> Full detail: **[Where this data comes from](https://apievangelist.com/about/where-our-data-comes-from)**
<!-- API-EVANGELIST-PROVENANCE:END -->

Enphase Energy is a Petaluma, California home-energy technology manufacturer and the dominant supplier of solar microinverters in the United States, shipping IQ Microinverters, IQ Batteries, IQ EV Chargers and the Envoy/IQ Gateway that ties them together through the Enlighten cloud. It sits on the DER side of the energy value chain rather than the utility side, so no consumer energy data mandate reaches it — there is no Green Button, ESPI or NAESB implementation anywhere in its developer surface. Its API posture is nevertheless unusually open for this sector: a genuine self-serve 3scale developer portal with three complete, anonymously downloadable contracts covering 124 operations. The defining split is consumer-data-open, market-data-closed.

**APIs.json:** [https://raw.githubusercontent.com/api-evangelist/enphase/refs/heads/main/apis.yml](https://raw.githubusercontent.com/api-evangelist/enphase/refs/heads/main/apis.yml)

## Tags

- Energy
- United States
- Solar
- DER
- Renewables
- Battery Storage
- EV Charging
- Demand Response
- Virtual Power Plant
- Grid Services
- Microinverters
- Home Energy Management
- Smart Metering
- Telemetry

## Timestamps

- **Created:** 2026-07-27
- **Modified:** 2026-07-27

## APIs

### Enphase Monitoring API

The Monitoring API is the consumer-data surface of the Enphase platform and the only self-serve one. Documented across 48 paths and eight tags, it lets a registered application retrieve an individual system owner's solar production, household consumption, IQ Battery telemetry and microinverter-level data after that owner approves the application through an OAuth 2.0 authorization-code grant. The free Watt plan covers system details, site-level production, site-level consumption and EV charger monitoring; device-level production monitoring requires the paid Kilowatt or Megawatt plans.

- **Human URL:** [https://developer-v4.enphase.com/docs/monitoring_api](https://developer-v4.enphase.com/docs/monitoring_api)
- **Base URL:** `https://api.enphaseenergy.com/api/v4`

#### Tags

- Energy
- Solar
- Monitoring
- Consumption
- Production
- Battery Storage
- EV Charging
- Telemetry

#### Properties

- [OpenAPI](openapi/enphase-monitoring-api-openapi.json) — [OpenAPI Specification](https://spec.openapis.org/oas/latest.html)
- [Documentation](https://developer-v4.enphase.com/docs/monitoring_api)
- [Documentation](https://developer-v4.enphase.com/docs/quickstart.html)
- [Plans](https://developer-v4.enphase.com/developer-plans)
- [Sign Up](https://developer-v4.enphase.com/signup)

### Enphase Commissioning API

The Commissioning API is the installer-facing administrative surface, documented across 21 paths and eleven tags. It creates and updates site activations, manages installer companies and users, sets grid profiles, and updates the utility tariff and rate-plan data attached to a site. It is not self-serve: the Partner plan is restricted to registered Enphase installers with at least ten installations, requires a credit card on file, and authenticates through an OAuth 2.0 password grant against Enphase cloud credentials.

- **Human URL:** [https://developer-v4.enphase.com/docs/commissioning_api](https://developer-v4.enphase.com/docs/commissioning_api)
- **Base URL:** `https://api.enphaseenergy.com/api/v4`

#### Tags

- Energy
- Solar
- Commissioning
- Installer
- Activations
- Tariffs
- Grid Profiles

#### Properties

- [OpenAPI](openapi/enphase-commissioning-api-openapi.json) — [OpenAPI Specification](https://spec.openapis.org/oas/latest.html)
- [Documentation](https://developer-v4.enphase.com/docs/commissioning_api)
- [Documentation](https://developer-v4.enphase.com/docs/quickstart.html)
- [Plans](https://developer-v4.enphase.com/installer-plans)

### Enphase VPP API

The Virtual Power Plant API is the grid-services surface, sold only to utilities, aggregators, DERMS providers and third-party owners registered as Enphase Grid Services partners. Documented as an OpenAPI 3.0.1 contract across 55 paths and eight tags, it creates and operates VPP programs, enrols homes, dispatches demand-response events, forecasts fleet capacity, and steers PV, battery, EVSE, heat pump and HVAC assets. It is the only Enphase API that implements a recognised interoperability standard: OCPP 1.6 for EV charger control against a partner's own CSMS.

- **Human URL:** [https://developer-v4.enphase.com/docs/vpp_api](https://developer-v4.enphase.com/docs/vpp_api)
- **Base URL:** `https://vpp.enphaseenergy.com`

#### Tags

- Energy
- Virtual Power Plant
- DER
- Demand Response
- Grid Services
- EV Charging
- OCPP
- Forecasting

#### Properties

- [OpenAPI](openapi/enphase-vpp-api-openapi.json) — [OpenAPI Specification](https://spec.openapis.org/oas/latest.html)
- [Documentation](https://developer-v4.enphase.com/docs/vpp_api)
- [Plans](https://developer-v4.enphase.com/vpp-plans)

## Common Properties

- [Website](https://enphase.com)
- [Developer Portal](https://developer-v4.enphase.com)
- [Sign Up](https://developer-v4.enphase.com/signup)
- [Login](https://developer-v4.enphase.com/login)
- [Documentation](https://developer-v4.enphase.com/docs/quickstart.html)
- [Getting Started](https://developer-v4.enphase.com/docs/quickstart.html)
- [Authentication](https://developer-v4.enphase.com/docs/quickstart.html)
- [Plans](https://developer-v4.enphase.com/developer-plans)
- [Pricing](https://developer-v4.enphase.com/developer-plans)
- [Rate Limits](https://developer-v4.enphase.com/developer-plans)
- [Change Log](https://developer-v4.enphase.com/docs/release_notes)
- [Support](https://developer-v4.enphase.com/docs/support)
- [Community](https://community.enphase.com/)
- [Terms of Service](https://enphase.com/legal/terms-of-service)
- [License Agreement](https://enphase.com/api-license-agreement-v4)
- [Privacy Policy](https://enphase.com/legal/privacy-policy)
- [About](https://developer-v4.enphase.com/aboutproduct.html)
- [Blog](https://newsroom.enphase.com/newsroom)
- [Investor Relations](https://investor.enphase.com/)
- [Email](mailto:api@enphaseenergy.com)

## Maintainers

- **Kin Lane** — kin@apievangelist.com
