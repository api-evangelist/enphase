---
name: Read and change battery, storm guard and load control settings
description: Safely inspect and modify an Enphase IQ Battery site's operating mode, storm guard and load control, on the Megawatt or Partner plan, where every write changes physical equipment behaviour with no undo.
api: openapi/enphase-monitoring-api-openapi.json
operations:
  - GET /api/v4/systems/config/{system_id}/battery_settings
  - PUT /api/v4/systems/config/{system_id}/battery_settings
  - GET /api/v4/systems/config/{system_id}/storm_guard
  - PUT /api/v4/systems/config/{system_id}/storm_guard
  - GET /api/v4/systems/config/{system_id}/grid_status
  - GET /api/v4/systems/config/{system_id}/load_control
  - PUT /api/v4/systems/config/{system_id}/load_control
  - GET /api/v4/systems/{system_id}/latest_telemetry
generated: '2026-07-27'
method: generated
---

# Read and change battery, storm guard and load control settings

These are the **System Configurations** access-control endpoints. They require the **Megawatt** plan or the **Partner** plan, and the system owner must have approved that access control when they authorized your application.

## Safety contract

Every `PUT` here changes how a real home behaves — how a battery charges and discharges, whether storm guard pre-charges before weather, which loads stay energised during an outage.

- There is **no idempotency key** and **no undo**. Read the current value first, diff it, and write only what changed.
- Confirm the write by reading the setting back; do not assume a `200` means the site has converged.
- Treat these as human-in-the-loop operations. `agentic-access/enphase-agentic-access.yml` classifies the battery writes as `acting` / `physical` with a 300-second token ceiling.

## Steps

1. **Read the current state.** `GET /api/v4/systems/config/{system_id}/battery_settings`, `/storm_guard`, `/grid_status` and `/load_control`. `GET /api/v4/systems/{system_id}/latest_telemetry` gives the last reported PV, consumption and battery power plus heat-pump and EVSE operational mode, so you can tell whether the site is even reporting before you write.
2. **Check the site can honour the change.** `GET /api/v4/systems/{system_id}/devices` — battery settings apply only to sites with an Enphase IQ Battery. On a PV-only site the Commissioning battery-mode endpoint returns `422` with `errorMessages: ["This is a PV only site..."]`.
3. **Write one setting.** `PUT /api/v4/systems/config/{system_id}/battery_settings` for mode and reserve, `PUT .../storm_guard` to arm or disarm, `PUT .../load_control` for controlled loads. Send the full documented body — these are replacements, not patches.
4. **Verify.** Re-`GET` the same path, then watch `latest_telemetry` for the mode to take effect on the gateway. Propagation is not instant.

## Rules

- **Savings Mode has history.** Setting battery mode to Savings Mode used to reset the account's tariff settings and fail the write; fixed 2024-12-18. If you support older behaviour, re-read the tariff via the Commissioning API (`GET /api/v4/systems/config/{system_id}/tariff`) after the write.
- **Grid Services wins.** During an active grid-services demand-response event the live status reports battery mode `DR Event Active` regardless of the homeowner setting. Do not "correct" it — the VPP event owns the asset for the duration.
- **Quota.** Megawatt is 100 hits/minute and 300,000/month; Partner is 300/minute and 1,500,000/month. `429` carries no `Retry-After`.
- **Errors.** `401` credential problem, `403` your application lacks the System Configurations access control, `404` unknown system, `422` the site cannot accept the setting, `429` quota. See `errors/enphase-problem-types.yml`.
