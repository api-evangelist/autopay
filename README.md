# Autopay (autopay)

Autopay is a Norwegian parking payment and management platform that provides APIs for parking operators, landlords, fleet managers, and third-party integrators. The platform enables automated parking permit management, payment processing, fleet tracking, and parking statistics with 13+ distinct API endpoints. All integrators must accept the Autopay API Usage Agreement before accessing the APIs.

**URL:** [https://developer.autopay.io](https://developer.autopay.io)

**Run:** [Capabilities Using Naftiko](https://github.com/naftiko/fleet?utm_source=api-evangelist&utm_medium=readme&utm_campaign=company-api-evangelist&utm_content=repo)

## Tags

 - Parking, Parking Payments, Fleet Management, Permits, Parking Operators, Norway

## Timestamps

- **Created:** 2025-02-08
- **Modified:** 2026-04-19

## APIs

### Autopay Accounting API

Provides Autopay invoicing data to external accounting and ERP systems, enabling automated reconciliation of parking revenue and invoice export.

**Human URL:** [https://developer.autopay.io](https://developer.autopay.io)

#### Tags

 - Accounting, Invoicing, Finance

#### Properties

- [Documentation](https://developer.autopay.io)

### Autopay Booking API

Enables assignment of anonymous parking permits to vehicles, supporting short-term and pre-booked parking allocations in managed parking facilities.

**Human URL:** [https://developer.autopay.io](https://developer.autopay.io)

#### Tags

 - Booking, Parking Permits, Reservations

#### Properties

- [Documentation](https://developer.autopay.io)

### Autopay Parking API

Handles zone entry notifications and parking session modifications, enabling integration with parking gate systems and sensor equipment.

**Human URL:** [https://developer.autopay.io](https://developer.autopay.io)

#### Tags

 - Parking Sessions, Zone Entry, Gate Control

#### Properties

- [Documentation](https://developer.autopay.io)

### Autopay Payment API

Enables third-party systems to take payment responsibility for parking sessions, supporting employer-paid parking and fleet-billed parking workflows.

**Human URL:** [https://developer.autopay.io](https://developer.autopay.io)

#### Tags

 - Payments, Parking Payment, Third-Party Billing

#### Properties

- [Documentation](https://developer.autopay.io)

### Autopay Permit Tenant API

Enables tenants in managed properties to manage their parking permits, including adding vehicles and modifying permit allocations within their assigned quota.

**Human URL:** [https://developer.autopay.io](https://developer.autopay.io)

#### Tags

 - Permits, Tenant Management, Vehicle Permits

#### Properties

- [Documentation](https://developer.autopay.io)

### Autopay Fleet API

Provides fleet information for company vehicle fleets, enabling fleet managers to track vehicle parking activity, costs, and permit usage.

**Human URL:** [https://developer.autopay.io](https://developer.autopay.io)

#### Tags

 - Fleet Management, Vehicle Tracking, Corporate Parking

#### Properties

- [Documentation](https://developer.autopay.io)

### Autopay Statistics API

Exports parking statistics for operators and landlords, providing data on occupancy rates, revenue, session volumes, and permit utilization.

**Human URL:** [https://developer.autopay.io](https://developer.autopay.io)

#### Tags

 - Analytics, Statistics, Reporting, Occupancy

#### Properties

- [Documentation](https://developer.autopay.io)

### Autopay Vehicle API

Fetches data about a vehicle in a specific parking zone, providing real-time information on vehicle presence, active session status, and permit validity.

**Human URL:** [https://developer.autopay.io](https://developer.autopay.io)

#### Tags

 - Vehicle Data, Zone Status, Enforcement

#### Properties

- [Documentation](https://developer.autopay.io)

### Autopay Tap and Park API

Enables third-party applications to validate parking sessions in Autopay-managed zones, supporting contactless parking validation via NFC or mobile apps.

**Human URL:** [https://developer.autopay.io](https://developer.autopay.io)

#### Tags

 - Parking Validation, NFC, Mobile Payments, Contactless

#### Properties

- [Documentation](https://developer.autopay.io)

## Common Properties

- [Developer Portal](https://developer.autopay.io)
- [Website](https://autopay.no)
- [Documentation](https://developer.autopay.io)
- [Authentication](https://developer.autopay.io)
- [Terms of Service](https://developer.autopay.io)

## Features

| Name | Description |
|------|-------------|
| OAuth Authentication | All Autopay APIs use OAuth for secure authentication and authorization. Integrators must obtain API credentials and accept the Usage Agreement before accessing production endpoints. |
| Permit Management | Comprehensive parking permit lifecycle management for landlords, operators, and tenants including allocation, assignment, modification, and expiration. |
| Real-Time Zone Status | Real-time counts of active parking sessions in parking zones via the Status API, enabling dynamic pricing and occupancy monitoring. |
| Fleet Parking Integration | Corporate fleet parking management with automatic billing to fleet accounts and vehicle-level tracking across parking facilities. |
| Parking Validation | Tap and Park API for third-party validation of parking sessions in Autopay zones, supporting retail validation and visitor parking workflows. |

## Use Cases

| Name | Description |
|------|-------------|
| Property Parking Management | Landlords manage tenant parking permits and allocations through the Permit Landlord and Tenant APIs for residential and commercial properties. |
| Corporate Fleet Parking | Companies manage fleet vehicle parking costs and permits using the Fleet API with automatic billing to corporate accounts. |
| Parking Revenue Reporting | Parking operators export revenue and occupancy statistics from the Statistics API into accounting and BI systems for reporting. |
| Visitor Parking Validation | Retail, hospitality, and office tenants validate visitor parking through the Tap and Park API integrated with access control or POS systems. |

## Integrations

| Name | Description |
|------|-------------|
| Accounting Systems | Export Autopay invoicing data to external ERP and accounting systems via the Accounting API for automated reconciliation. |
| Building Access Control | Integration with building access control and gate systems via the Parking API for automated entry/exit tracking. |
| Fleet Management Platforms | Connect corporate fleet management software with Autopay for parking cost tracking and vehicle permit assignment. |

## Maintainers

**FN:** Kin Lane

**Email:** kin@apievangelist.com
