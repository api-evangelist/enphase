---
name: Commission a site as an Enphase installer
description: Create and complete an activation through the Partner-plan Commissioning API - company and user setup, grid profile, PV catalog, tariff and estimate - without paying twice for a duplicate activation.
api: openapi/enphase-commissioning-api-openapi.json
operations:
  - GET /api/v4/partner/users/self
  - GET /api/v4/companies/self/branches
  - GET /api/v4/partner/activations
  - POST /api/v4/partner/activations
  - GET /api/v4/partner/activations/{activation_id}
  - PUT /api/v4/partner/activations/{activation_id}
  - POST /api/v4/activations/{activation_id}/users/{user_id}
  - GET /api/v4/partner/grid_profiles
  - GET /api/v4/pv_manufacturers
  - GET /api/v4/pv_manufacturers/{pv_manufacturer_id}/pv_models
  - GET /api/v4/systems/config/{system_id}/tariff
  - GET /api/v4/activations/{activation_id}/estimate
  - PUT /api/v4/activations/{activation_id}/estimate
generated: '2026-07-27'
method: generated
---

# Commission a site as an Enphase installer

The Commissioning API is **Partner plan only**: a self-installer, or a member of an installer company with at least ten installed systems, with a credit card on file. Applications start pending and are enabled after Enphase verifies the Enlighten credentials.

## Authentication

The password grant, not the consent redirect:
`POST https://api.enphaseenergy.com/oauth/token?grant_type=password&username=<enlighten_email>&password=<enlighten_password>` with `Authorization: Basic base64(client_id:client_secret)`. The credentials are the installer's **Enphase cloud (Enlighten)** login, not the developer portal login. Every call also carries `?key=<api_key>`.

## Steps

1. **Confirm who you are.** `GET /api/v4/partner/users/self` and `GET /api/v4/companies/self/branches`. `GET /api/v4/companies/self/authorized_subcontractors` shows which sites you can act on as a subcontractor — authorized subcontractors get Partner access to a site's endpoints.
2. **Check the site is not already activated.** `GET /api/v4/partner/activations`, filtering by your `reference` / `other_references` strings. **Creating an activation costs $2 per call and is not de-duplicated** — this read is the only guard.
3. **Gather the catalog values first.** `GET /api/v4/partner/grid_profiles` for the grid profile, `GET /api/v4/pv_manufacturers` then `GET /api/v4/pv_manufacturers/{pv_manufacturer_id}/pv_models` for the module. Assemble the whole body before you POST.
4. **Create it.** `POST /api/v4/partner/activations`. Required fields depend on jurisdiction:
   - A **United States** site must carry an address, or you get "Address is mandatory for sites created in the United States."
   - `grid_connection_type` is required in **California** (1 Net Billing Tariff / NEM 3.0, 2 Net Metering, 3 Net Feed-in tariff, 4 Gross Feed-in tariff).
   - `battery_grid_mode` (1 Import Only, 2 Export Only) applies only to battery sites with `grid_connection_type` 1.
   - If the PTO flag is true, `interconnection_date` is required, must be in epoch format, cannot be in the future, and must be after 2023-04-14.
5. **Attach people.** `POST /api/v4/activations/{activation_id}/users/{user_id}` to add the homeowner or a company user; `PUT`/`DELETE` on the same path to change or remove. Third-party-owner companies can set maintainers and subcontractors at any stage 1-5.
6. **Finish the commercial detail.** `PUT /api/v4/activations/{activation_id}/estimate` for the production estimate, and read `GET /api/v4/systems/config/{system_id}/tariff` for the rate plan attached to the resulting system.
7. **Verify.** `GET /api/v4/partner/activations/{activation_id}`, then confirm the system appears in the Monitoring API — an approved activation becomes the Enlighten system you can then read with `skills/enphase-authorize-and-read-system-energy.md`.

## Rules

- **The $2 charge is the whole risk model.** No idempotency key exists. Search before you create; on a timeout, re-`GET` the activations list before retrying the POST.
- **Retired Envoys are allowed.** An activation cannot use an Envoy that belongs to an active site, but a retired Envoy can be reused (since 2024-12-18).
- **Error envelope is the array form:** `{"reason":"422","message":["..."]}`, with `422` responses sometimes using `{"errorMessages":[...], "errorCode":"..."}`. `429` reads `Usage limit exceeded for plan Partner (custom)`; the Partner quota is 300/minute and 1,500,000/month with 10,000 free hits then $0.005/hit.
- No operation in this spec declares an `operationId` — reference every call by method and path.
