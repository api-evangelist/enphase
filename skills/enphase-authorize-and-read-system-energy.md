---
name: Authorize a homeowner and read their system energy
description: Take an Enphase developer application from OAuth consent to production, consumption and battery data for one Enlighten system, respecting plan quotas and the 7-day telemetry window.
api: openapi/enphase-monitoring-api-openapi.json
operations:
  - GET /api/v4/systems
  - GET /api/v4/systems/{system_id}/summary
  - GET /api/v4/systems/{system_id}/energy_lifetime
  - GET /api/v4/systems/{system_id}/telemetry/production_meter
  - GET /api/v4/systems/{system_id}/telemetry/consumption_meter
  - GET /api/v4/systems/{system_id}/telemetry/battery
  - GET /api/v4/systems/{system_id}/devices
generated: '2026-07-27'
method: generated
---

# Authorize a homeowner and read their system energy

The Monitoring API is the only self-serve Enphase surface. Everything here works on the free Watt plan except the battery and device-level telemetry reads, which need Kilowatt or above.

## Before you start

- Register an application at https://developer-v4.enphase.com and note its **API key**, **client id** and **client secret**. Tick only the access controls you need — the tick list is the scope shown to the homeowner and it cannot be widened later without a new application.
- Every request needs **both** credentials: `Authorization: Bearer <access_token>` **and** `?key=<api_key>`. If they come from different applications you get `401 API Key -Client mismatch`.
- Use `https://api.enphaseenergy.com` — the published spec's `api-qa2.enphaseenergy.com` host is an Enphase QA host, not production.

## Steps

1. **Get consent.** Send the system owner to
   `https://api.enphaseenergy.com/oauth/authorize?response_type=code&client_id=<client_id>&redirect_uri=<your_uri>&state=<opaque>`.
   Use your own redirect URI so you receive the code yourself; the default
   `https://api.enphaseenergy.com/oauth/redirect_uri` forces you to ask the homeowner to read the code back to you. A rejection returns `access_denied` on the same redirect.
2. **Exchange the code.** `POST https://api.enphaseenergy.com/oauth/token?grant_type=authorization_code&redirect_uri=<same_uri>&code=<code>` with `Authorization: Basic base64(client_id:client_secret)`. Store `access_token` (1 day) and `refresh_token` (1 month). Refresh with `grant_type=refresh_token`; a new refresh token is issued each time, so persist it.
3. **Find the system.** `GET /api/v4/systems` (params `page`, `size` max 100, `sort_by=id|-id`). Read `system_id` from the `systems` array. `energy_lifetime`, `energy_today` and `system_size` are always `-1` here by design since 2023-07-03 — do not report them.
4. **Get the real numbers.** `GET /api/v4/systems/{system_id}/summary` for current status, lifetime energy, battery charge/discharge and capacity. Optional `summary_date` returns lifetime values as of that date.
5. **Pull a series.** `GET /api/v4/systems/{system_id}/energy_lifetime` for daily production with no range limit; `GET /api/v4/systems/{system_id}/telemetry/production_meter` and `/telemetry/consumption_meter` for 15-minute intervals; `/telemetry/battery` for battery intervals (Kilowatt+). Interval calls are capped at **7 days per request** and the start must be within **2 years** of now — page the window client-side, do not widen it.
6. **Enumerate hardware if you need it.** `GET /api/v4/systems/{system_id}/devices` lists microinverters, IQ Batteries, the IQ Gateway, IQ EV chargers and IQ collars with `product_name` and serials.

## Rules

- **Quota.** Watt is 10 hits/minute and 1,000 hits/month. A `429` body reads `Usage limit exceeded for plan <plan>`; there is **no** `Retry-After` header, so back off on your own clock (start at 60s) and cache aggressively. Daily series change once a day — do not poll them per minute.
- **Empty is not an error.** Telemetry returns `200` with an empty list when you ask for the window between the last reported interval and now.
- **Errors.** `401` missing/invalid key or token, `403` application not authorized for that system, `404` unknown system, `422` bad parameter (for example an unsupported `sort_by`), `501` for any method outside POST/PUT/GET/DELETE/HEAD/OPTIONS/PATCH. Full catalog in `errors/enphase-problem-types.yml`.
- **No idempotency keys and no request ids.** Reads are safe to retry; there is nothing to correlate a retry with, so keep your own client-side request log for support tickets.
