# Autopay (autopay)

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
