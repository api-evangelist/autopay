---
name: autopay-consume-parking-webhooks
description: Stand up an endpoint that safely receives Autopay's entry, payment and fleet callbacks — authentication, retry behaviour, duplicate handling and event correction.
api: Autopay Parking API, Autopay Payment API, Autopay Fleet API
provider: autopay
docs: https://developer.autopay.io/parking_api/
generated: '2026-09-06'
method: generated
source: https://developer.autopay.io/parking_api/, https://developer.autopay.io/payment_api/, https://developer.autopay.io/fleet-api/
operations:
  - 'CALLBACK POST <your parking entry webhook URL>'
  - 'CALLBACK POST <your payment success callback URL>'
  - 'CALLBACK POST <your payment cancel callback URL>'
  - 'CALLBACK POST <your fleet service webhook URL>'
  - PUT /parking/product/{parkingSessionId}
---

# Receive Autopay webhooks

Autopay's event surface is outbound HTTP POST to endpoints **you** host. There is no
subscription API, no event replay endpoint and no AsyncAPI document — every webhook is
configured out-of-band by an Autopay representative during onboarding.

## What Autopay needs from you at setup

| Surface | You provide |
|---|---|
| Parking entry webhook | HTTPS URL, an `Authorization` header value, facility code, zone code(s) or "all zones", landlord id |
| Payment callbacks | HTTPS success URL, HTTPS cancel URL, and the auth method + credentials for both |
| Fleet service webhook | HTTPS URL(s) and access token(s); entry and periodical notifications may use different ones. Requires an Enterprise fleet profile |

## Authenticating Autopay to you

Autopay authenticates itself to your endpoint. Supported methods differ per surface:

- Parking entry webhook: Basic, or Bearer token.
- Fleet service webhook: Bearer token in the `Authorization` header.
- Payment callbacks: Basic, Bearer, API key in `X-API-Key`, or OAuth2 (you give Autopay a client
  id, secret and token URL; Autopay reuses tokens while they are valid).

**There is no payload signature.** No HMAC header is published, so authenticity rests entirely
on the credential Autopay presents. Verify it on every request and reject anything else.

## Respond correctly

Return **2xx**. For the Payment callbacks a `404` is also treated as final and stops retries —
anything else starts the retry ladder.

| Surface | Retry behaviour |
|---|---|
| Payment callbacks | Exponential backoff from 1s, doubling to a 1-hour ceiling, then hourly until one week has passed, then abandoned |
| Parking entry webhook | Up to 50 attempts until a 2xx |
| Fleet service webhook | Not documented |

Return the 2xx fast and process asynchronously — a slow handler will earn you duplicates.

## Handle duplicates and corrections

- **Payment callbacks may be delivered more than once.** De-duplicate on `parking_id`. Autopay
  offers no idempotency mechanism; this is your job.
- **Entry events are corrected in place.** If a licence plate is re-read, the event is
  redelivered with the **same `event_id`** and the corrected plate. Upsert on `event_id`; do not
  append, or you will double-count entries and act on a plate Autopay has already retracted.

## The entry event payload

`event_id`, `parking_id`, `parking_session_id`, `time_in_utc`, `operator_id`,
`landlord{landlord_id,name}`, `zone{code,name}`, `facility{code,name,time_zone}`,
`plate{plate_number,country_alpha2_code,subdivision}`.

Note the two distinct handles: `parking_session_id` is what you pass to
`PUT /parking/product/{parkingSessionId}` to change what the session is charged; `parking_id` is
what the Payment API and its callbacks use. They are not interchangeable.

`facility.time_zone` is an IANA identifier such as `Europe/Oslo` — use it, do not assume the
operator's local time.

## Acting on an entry event

Two common reactions:

1. **Change the product** — `PUT /parking/product/{parkingSessionId}` with `facility_code`,
   `zone_code` and `product`, e.g. to grant a customer two hours free. Product ids must be
   agreed with Autopay in advance. Errors: `product_not_found`, `facility_or_zone_not_found`,
   `invalid_parking_session`, `invalid_status` (the session is in an error state),
   `invalid_operator_id`.
2. **Claim the session for payment** — the autostart path, `POST /payment/v1/connect_parking`.
   This is irreversible; see `autopay-take-payment-responsibility`.

## The fleet service event

`id`, `vehicle{license_plate_number,country_code,subdivision,created_at}`,
`facility{code,name}`, `zone{code,name}`, `start_time`, `operator_id`,
`type` (`PARKING` or `TOLL_ROAD`), `notification_period` (present only on the periodical
notification), and a free-form `service_data` map.

## Country-code inconsistency to normalise

Webhooks give you ISO 3166-1 **alpha-2** (`country_alpha2_code`, `country_code`). The Payment
API expects **alpha-3** (`plate_issuer`). Convert at the boundary.
