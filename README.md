# Verizon Connect (verizon-connect)

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
