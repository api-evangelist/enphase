---
name: Monitor and control an Enphase IQ EV charger
description: Read IQ EV charger devices, sessions, schedules and energy, then start or stop a charge session on the Partner plan, treating the two control calls as physical actions.
api: openapi/enphase-monitoring-api-openapi.json
operations:
  - fetchChargersSummary
  - fetchEvents
  - fetchChargerSessionHistory
  - fetchSchedules
  - fetchDailyEnergyConsumptionData
  - fetchEnergyConsumptionData
  - startCharging
  - stopCharging
generated: '2026-07-27'
method: generated
---

# Monitor and control an Enphase IQ EV charger

EV charger **monitoring** is available on every plan including free Watt. EV charger **control** — `startCharging` and `stopCharging` — is **Partner plan only**.

Only Enphase IQ EV chargers are visible. Tesla Wall Connectors and third-party chargers do not appear, and a `404` from these operations usually means the site has no Enphase charger rather than a bad request.

## Steps

1. **Find the charger.** `fetchChargersSummary` — `GET /api/v4/systems/{system_id}/ev_charger/devices` — returns the chargers on the site with their serial numbers. Everything below is keyed by `{serial_no}`.
2. **Read state and history.**
   - `fetchEvents` — `GET /api/v4/systems/{system_id}/ev_charger/events` for charger events.
   - `fetchChargerSessionHistory` — `GET /api/v4/systems/{system_id}/ev_charger/{serial_no}/sessions` for completed charge sessions.
   - `fetchSchedules` — `GET .../{serial_no}/schedules` for the configured charging schedule.
   - `fetchDailyEnergyConsumptionData` — `GET .../{serial_no}/lifetime` for daily energy.
   - `fetchEnergyConsumptionData` — `GET .../{serial_no}/telemetry` for interval energy.
3. **Start a session.** `startCharging` — `POST /api/v4/systems/{system_id}/ev_charger/{serial_no}/start_charging`. It returns **202 Accepted**: the command has been queued to the charger, not completed.
4. **Stop a session.** `stopCharging` — `POST .../{serial_no}/stop_charging`, also `202`.
5. **Confirm.** After a `202`, poll `fetchChargerSessionHistory` or `fetchEnergyConsumptionData` until the state matches what you asked for. **Do not re-issue the command as a retry** — there is no idempotency key, and a duplicate start/stop can bounce a real charge session.

## Rules

- These are physical actions on someone's car and home circuit. `agentic-access/enphase-agentic-access.yml` classifies them as `acting`; treat them as human-approved, not autonomous, and never chain them into an unattended loop.
- The EV charger family uses a different error envelope from the rest of the Monitoring API: `400/401/403/405/500` with the `ErrorResponse` shape `{message, code, details}`. There is no `429` documented on these operations, but the plan quota still applies at the gateway.
- Schedules are read-only through this API — there is no schedule write operation. To change charging behaviour you start or stop explicitly, or change the schedule in the Enphase App.
- The system summary reports the min and max charge/discharge power of every EVSE at the site (since 2025-08-13), which is the cheapest way to size a session before you call anything.
