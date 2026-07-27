---
name: Dispatch and manage a VPP demand-response event
description: Authenticate as an Enphase Grid Services partner, enumerate programs and enrolled sites, forecast available capacity, dispatch a demand-response event, then track, amend or cancel it.
api: openapi/enphase-vpp-api-openapi.json
operations:
  - getToken
  - getAllPrograms
  - getProgramByKey
  - getSystems
  - getForecast
  - createEvent
  - getEvents
  - getEventDetails
  - updateEvent
  - optOutOptInEvent
  - cancelEvent
generated: '2026-07-27'
method: generated
---

# Dispatch and manage a VPP demand-response event

The VPP API is partner-only — utilities, aggregators, DERMS providers and third-party owners registered as Enphase Grid Services partners. Base URL `https://vpp.enphaseenergy.com`. There is no self-serve signup and no published pricing.

## Authentication

`getToken` — `POST /auth/oauth2/token?grant_type=client_credentials` with:
- `Authorization: <base64(clientId:clientSecret)>`
- `Content-Type: application/x-www-form-urlencoded`
- `Accept: application/json`

Tokens last **3600 seconds** and there is **no refresh token** — regenerate through the same call. Every subsequent request carries `Authorization: Bearer <access_token>` **and** the `x-api-key` header.

## Steps

1. **List programs.** `getAllPrograms` — `GET /api/v1/programs` — then `getProgramByKey` — `GET /api/v1/programs/{program_id}` — for season definitions and program rules.
2. **See who is enrolled.** `getSystems` — `GET /api/v1/systems/search/{program_id}` — returns the sites enrolled in that program. Enrolment itself runs through the Applications resource (`getApplications`, `createApplication`, `updateApplication`, `withdrawApplication`).
3. **Forecast the fleet.** `getForecast` — `POST /api/v1/forecast` — returns a `ForecastResponse` time series so you can size the event against real available capacity before you dispatch. (Enphase gates this endpoint: "Contact us if you are interested in using this endpoint.")
4. **Dispatch.** `createEvent` — `POST /api/v2/events` — is the current events surface; `createEvent_1` on `/api/v1/events` is the older one. Send the `EventCreateRequestV2` body. Keep your own external reference for the event; the API does not de-duplicate a repeated create.
5. **Track it.** `getEvents` — `GET /api/v2/events` — and `getEventDetails` — `GET /api/v2/events/{event_id}`. Per-site state also shows up in `getSiteEvents` and `getSiteOpenEvents` on the site telemetry surface, and the homeowner's live status reports battery mode `DR Event Active` for the duration.
6. **Amend, opt out, or cancel.** `updateEvent` — `PUT /api/v1/events/{event_id}`; `optOutOptInEvent` — `PUT /api/v1/events/optout/{event_id}` for a single participant; `cancelEvent` — `DELETE /api/v2/events/{event_id}`.

## Rules

- **Dispatch is a grid action.** It moves stored energy in hundreds of real homes. There is no idempotency key: always read `getEvents` for an overlapping event before creating a new one, and cancel rather than re-create when correcting a mistake.
- **v1 and v2 coexist.** Events exist on both `/api/v1/events` and `/api/v2/events` with distinct operationIds (`createEvent` vs `createEvent_1`, `cancelEvent` vs `cancelEvent_1`). Pick v2 and stay on it; do not mix the two for one event's lifecycle.
- **Errors are uniform.** Every VPP operation documents `400`, `401`, `403`, `404`, `422` — and `409 Conflict` on `createApplication`. There are no rate-limit headers and no published VPP quota; limits are contractual.
- **Device control is separate.** `registerEvse` and `resetEvse` configure an IQ EV charger against your own OCPP 1.6 CSMS, and `generateLocalApiToken` mints a gateway-local token. These are the only standards-based interoperability points in the Enphase surface — see `conformance/enphase-conformance.yml`.
