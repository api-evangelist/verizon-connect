# Verizon Connect (verizon-connect)

Verizon Connect is the fleet management, telematics, and GPS vehicle tracking business of **Verizon**. It was built from Verizon's acquisitions of **Fleetmatics** (2016) and **Telogis**, and its developer/API infrastructure still runs under `fleetmatics.com` hostnames. Its flagship **Reveal** platform exposes a documented suite of REST APIs and webhooks - the Reveal Integration Services / Fleetmatics Integration Manager (FIM) APIs - covering vehicles, drivers, GPS positions and history, trips (segments), driver status and safety, hours-of-service logbooks, geofences (places), groups, work orders, non-powered asset tracking, fleet inspections, and dash-cam video events.

**APIs.json:** [https://raw.githubusercontent.com/api-evangelist/verizon-connect/refs/heads/main/apis.yml](https://raw.githubusercontent.com/api-evangelist/verizon-connect/refs/heads/main/apis.yml)

## Access model (important)

Verizon Connect's API is **real and documented, but gated** - it is not open, self-service, or free-signup:

- The API is available to active **Reveal customers** and their **approved integration partners**.
- A Reveal customer requests integration (**Reveal REST**) credentials through the Reveal marketplace; approved credentials are emailed.
- A developer additionally registers for **Integration Manager** (FIM) developer-portal credentials at [fim.us.fleetmatics.com](https://fim.us.fleetmatics.com).
- **Both** credential sets are required to make an API request.
- The API surface (names, base URLs, auth flow) is publicly documented; detailed per-endpoint request/response schemas live behind the credential-gated portal.

Because exact endpoint paths and schemas are behind that portal, the individual API entries in `apis.yml` are **modeled** from Verizon Connect's public API list and Developer Quick Start Guide (`endpointsModeled: true`). No OpenAPI was fabricated.

## Base URLs

- **US:** `https://fim.api.us.fleetmatics.com`
- **EU:** `https://fim.api.eu.fleetmatics.com`

## Authentication

Two-step token flow:

1. `GET /token` with an `Authorization: Basic <Base64 Reveal REST credentials>` header returns a bearer authorization token (valid ~20 minutes).
2. API calls send `Authorization: Atmosphere atmosphere_app_id=<Verizon Connect App ID>, Bearer <token>`.

## Real-time / WebSocket

**No public WebSocket API.** Near-real-time GPS and status is obtained by **polling** the Vehicle Update (Real-time Aggregated Data) API, or via outbound **Alert webhooks** and **GPS webhooks** that POST events to a customer-registered endpoint. See `review.yml`.

## Tags

- Fleet Management
- Telematics
- GPS Tracking
- Vehicle Tracking
- Fleet Tracking
- Verizon
- Fleetmatics

## Timestamps

- **Created:** 2026-07-04
- **Modified:** 2026-07-04

## APIs (modeled from the public Reveal API list)

- Verizon Connect Token Authorization API
- Verizon Connect Vehicle API (with Vehicle Update, Attribute)
- Verizon Connect Vehicle Location API (Real-time Aggregated Data poll)
- Verizon Connect Vehicle GPS History API
- Verizon Connect Vehicle Segment Data API (trips)
- Verizon Connect Driver API
- Verizon Connect Driver Status API (with Driver Status Options)
- Verizon Connect Driver Assignment API
- Verizon Connect Driver Safety API
- Verizon Connect Logbook API (hours-of-service / compliance)
- Verizon Connect Geofence API (Places)
- Verizon Connect Group API (with Group Relocation)
- Verizon Connect Work Order API (with Work Order Status, Work Order Type)
- Verizon Connect Non-Powered Assets API (with Update, GPS History)
- Verizon Connect Fleet Inspections API
- Verizon Connect Video Event API (dash cam)
- Verizon Connect User API
- Verizon Connect Webhooks (Alert + GPS)

## Pricing

Verizon Connect does not publish list pricing; Reveal and API access are sold via **contact sales** and custom quotes. Third-party reporting (2026) puts Reveal around **USD 20-45 per vehicle per month** on a typical **36-month (3-year)** contract, with integrated-video bundles higher. API/integration access is provisioned to existing Reveal customers rather than priced as a standalone metered product. See `plans/verizon-connect-plans-pricing.yml`.

## Common Properties

- [LinkedIn](https://www.linkedin.com/company/verizonconnect)
- [Website](https://www.verizonconnect.com)
- [Documentation](https://reveal-help.verizonconnect.com/hc/en-us/sections/5491620930451-API-integrations)
- [Developer Portal](https://fim.us.fleetmatics.com)
- [Sign Up / Contact](https://www.verizonconnect.com/services/api-integration/)
- [Plans](plans/verizon-connect-plans-pricing.yml)
- [Rate Limits](rate-limits/verizon-connect-rate-limits.yml)

## Maintainers

**FN:** Kin Lane
**Email:** kin@apievangelist.com
