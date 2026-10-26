# Autopay (autopay)

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

Autopay is a Norwegian parking payment and management platform that provides APIs for parking operators, landlords, fleet managers, and third-party integrators. The platform enables automated parking permit management, payment processing, fleet tracking, and parking statistics with 13+ distinct API endpoints. All integrators must accept the Autopay API Usage Agreement before accessing the APIs.

**APIs.json:** [https://raw.githubusercontent.com/api-evangelist/autopay/refs/heads/main/apis.yml](https://raw.githubusercontent.com/api-evangelist/autopay/refs/heads/main/apis.yml)

## Scope

- **Type:** Index
- **Access:** 3rd-Party

## Tags

- Parking
- Parking Payments
- Fleet Management
- Permits
- Parking Operators
- Norway

## Timestamps

- **Created:** 2025-02-08
- **Modified:** 2026-04-19

## APIs

### Autopay Accounting API

The Autopay Accounting API provides Autopay invoicing data to external accounting and ERP systems, enabling automated reconciliation of parking revenue and invoice export.

- **Human URL:** [https://developer.autopay.io](https://developer.autopay.io)

#### Tags

- Accounting
- Invoicing
- Finance

#### Properties

- [Documentation](https://developer.autopay.io)
- [Authentication](https://developer.autopay.io)
- [Postman Collection](collections/autopay.postman_collection.json) — [Postman Collection 2.1](https://schema.getpostman.com/json/collection/v2.1.0/collection.json)
- [Open Collection](collections/autopay.opencollection.json) — [Open Collection 1.0](https://schema.opencollection.com/opencollection/v1.0.0.json)

### Autopay Booking API

The Autopay Booking API enables assignment of anonymous parking permits to vehicles, supporting short-term and pre-booked parking allocations in managed parking facilities.

- **Human URL:** [https://developer.autopay.io](https://developer.autopay.io)

#### Tags

- Booking
- Parking Permits
- Reservations

#### Properties

- [Documentation](https://developer.autopay.io)
- [Postman Collection](collections/autopay.postman_collection.json) — [Postman Collection 2.1](https://schema.getpostman.com/json/collection/v2.1.0/collection.json)
- [Open Collection](collections/autopay.opencollection.json) — [Open Collection 1.0](https://schema.opencollection.com/opencollection/v1.0.0.json)

### Autopay Parking API

The Autopay Parking API handles zone entry notifications and parking session modifications, enabling integration with parking gate systems, sensors, and barrier control equipment to track vehicle arrivals and departures in parking zones.

- **Human URL:** [https://developer.autopay.io](https://developer.autopay.io)

#### Tags

- Parking Sessions
- Zone Entry
- Gate Control

#### Properties

- [Documentation](https://developer.autopay.io)
- [Postman Collection](collections/autopay.postman_collection.json) — [Postman Collection 2.1](https://schema.getpostman.com/json/collection/v2.1.0/collection.json)
- [Open Collection](collections/autopay.opencollection.json) — [Open Collection 1.0](https://schema.opencollection.com/opencollection/v1.0.0.json)

### Autopay Payment API

The Autopay Payment API enables third-party systems to take payment responsibility for parking sessions, supporting employer-paid parking, fleet-billed parking, and visitor parking validation workflows.

- **Human URL:** [https://developer.autopay.io](https://developer.autopay.io)

#### Tags

- Payments
- Parking Payment
- Third-Party Billing

#### Properties

- [Documentation](https://developer.autopay.io)
- [Postman Collection](collections/autopay.postman_collection.json) — [Postman Collection 2.1](https://schema.getpostman.com/json/collection/v2.1.0/collection.json)
- [Open Collection](collections/autopay.opencollection.json) — [Open Collection 1.0](https://schema.opencollection.com/opencollection/v1.0.0.json)

### Autopay Permit Tenant API

The Autopay Permit Tenant API enables tenants in managed properties to manage their parking permits, including adding vehicles, modifying permit allocations, and tracking permit usage within their assigned quota.

- **Human URL:** [https://developer.autopay.io](https://developer.autopay.io)

#### Tags

- Permits
- Tenant Management
- Vehicle Permits

#### Properties

- [Documentation](https://developer.autopay.io)
- [Postman Collection](collections/autopay.postman_collection.json) — [Postman Collection 2.1](https://schema.getpostman.com/json/collection/v2.1.0/collection.json)
- [Open Collection](collections/autopay.opencollection.json) — [Open Collection 1.0](https://schema.opencollection.com/opencollection/v1.0.0.json)

### Autopay Fleet API

The Autopay Fleet API provides fleet information for company vehicle fleets, enabling fleet managers to track vehicle parking activity, costs, and permit usage across all fleet vehicles.

- **Human URL:** [https://developer.autopay.io](https://developer.autopay.io)

#### Tags

- Fleet Management
- Vehicle Tracking
- Corporate Parking

#### Properties

- [Documentation](https://developer.autopay.io)
- [Postman Collection](collections/autopay.postman_collection.json) — [Postman Collection 2.1](https://schema.getpostman.com/json/collection/v2.1.0/collection.json)
- [Open Collection](collections/autopay.opencollection.json) — [Open Collection 1.0](https://schema.opencollection.com/opencollection/v1.0.0.json)

### Autopay Statistics API

The Autopay Statistics API exports parking statistics for operators and landlords, providing data on occupancy rates, revenue, session volumes, and permit utilization for parking facility management and reporting.

- **Human URL:** [https://developer.autopay.io](https://developer.autopay.io)

#### Tags

- Analytics
- Statistics
- Reporting
- Occupancy

#### Properties

- [Documentation](https://developer.autopay.io)
- [Postman Collection](collections/autopay.postman_collection.json) — [Postman Collection 2.1](https://schema.getpostman.com/json/collection/v2.1.0/collection.json)
- [Open Collection](collections/autopay.opencollection.json) — [Open Collection 1.0](https://schema.opencollection.com/opencollection/v1.0.0.json)

### Autopay Vehicle API

The Autopay Vehicle API fetches data about a vehicle in a specific parking zone, providing real-time information on vehicle presence, active session status, and permit validity for enforcement and access control purposes.

- **Human URL:** [https://developer.autopay.io](https://developer.autopay.io)

#### Tags

- Vehicle Data
- Zone Status
- Enforcement

#### Properties

- [Documentation](https://developer.autopay.io)
- [Postman Collection](collections/autopay.postman_collection.json) — [Postman Collection 2.1](https://schema.getpostman.com/json/collection/v2.1.0/collection.json)
- [Open Collection](collections/autopay.opencollection.json) — [Open Collection 1.0](https://schema.opencollection.com/opencollection/v1.0.0.json)

### Autopay Tap and Park API

The Autopay Tap and Park API enables third-party applications to validate parking sessions in Autopay-managed zones, supporting contactless parking validation via NFC, mobile apps, or access control systems.

- **Human URL:** [https://developer.autopay.io](https://developer.autopay.io)

#### Tags

- Parking Validation
- NFC
- Mobile Payments
- Contactless

#### Properties

- [Documentation](https://developer.autopay.io)
- [Postman Collection](collections/autopay.postman_collection.json) — [Postman Collection 2.1](https://schema.getpostman.com/json/collection/v2.1.0/collection.json)
- [Open Collection](collections/autopay.opencollection.json) — [Open Collection 1.0](https://schema.opencollection.com/opencollection/v1.0.0.json)

## Common Properties

- [LinkedIn](https://www.linkedin.com/company/autopay)
- [Portal](https://developer.autopay.io)
- [Website](https://autopay.no)
- [Documentation](https://developer.autopay.io)
- [Authentication](https://developer.autopay.io)
- [Terms of Service](https://developer.autopay.io)
- [Features](undefined)
- [Use Cases](undefined)
- [Integrations](undefined)
- [L L Ms Txt](https://autopay.io/llms.txt)

## Maintainers

**FN:** Kin Lane
**Email:** kin@apievangelist.com
