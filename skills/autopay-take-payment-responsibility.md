---
name: autopay-take-payment-responsibility
description: Claim billing responsibility for a live Autopay parking session as an external payment provider, receive the end-of-parking callback, and charge the customer.
api: Autopay Payment API
provider: autopay
docs: https://developer.autopay.io/payment_api/
generated: '2026-09-06'
method: generated
source: https://developer.autopay.io/payment_api/
operations:
  - POST /payment/v1/connect_parking
  - POST /payment/v1/manual_stop
  - 'CALLBACK POST <your success callback URL>'
  - 'CALLBACK POST <your cancel callback URL>'
---

# Take payment responsibility for a parking session

> **This skill contains the one irreversible call on the Autopay surface.**
> `POST /payment/v1/connect_parking` claims a live parking session for billing. There is no
> undo. Confirm the vehicle and the area code before you call it, and never retry it blindly.

Autopay detects the vehicle, tracks the session and calculates the cost. You identify the
customer, hold the payment relationship and charge them when the session ends. The licence
plate is the link between the two systems. Integration is **per operator** — one credential
pair, one setup, one set of area-code mappings per operator.

## Prerequisites (arranged with Autopay, not self-serve)

- A `client_id` / `client_secret` per operator.
- Your **success callback URL** and **cancel callback URL**, both HTTPS, plus the credential
  Autopay should present to them (Basic, Bearer, `X-API-Key`, or OAuth2 client credentials —
  Autopay reuses OAuth tokens while valid).
- Your **area codes** — your own facility/zone identifiers, in a format you choose. The
  operator maps them onto Autopay zones. Nothing works until this mapping exists.

There is no staging environment: "There is no formal staging environment for the Payment API at
present."

## Steps

1. **Learn the session exists.** Either the driver starts it in your app (manual start), or you
   listen to the Parking API entry webhook and trigger automatically (autostart — this needs a
   separate agreement and a separate Parking API integration).

2. **Claim it.**

   ```
   POST https://api.autopay.io/payment/v1/connect_parking
   Authorization: Bearer <token>
   Content-Type: application/json

   {
     "parking_area_code": "area1",
     "reference": "ref1",
     "vehicle_reg": "123ABC",
     "plate_issuer": "NOR",
     "plate_subdivision": null
   }
   ```

   `plate_issuer` is **ISO 3166-1 alpha-3** here — note that the Parking and Fleet webhooks use
   alpha-2 for the same concept. `reference` is your own primary key and is echoed back on every
   callback.

   You get `parking_id`, your `reference`, and `start_time`. From this moment the session is
   marked as paid in Autopay and **you** own the charge.

   If the session is already claimed you get `400` with
   `{"error_id": "server_communication_error", "message": "Payment provider already registered"}`.
   Treat that as "someone else owns it", not as a transient error to retry.

3. **Wait for the callback.** When the vehicle exits, Autopay POSTs to your success callback URL
   with `parking_id`, `reference`, `end_time` and a `cost` object carrying `currency`,
   `vat_percent`, `net_amount`, `vat_amount` and `gross_amount`. The currency is local to the
   country the parking took place in — handle multiple currencies and VAT rates if you operate
   across borders. **You never calculate the fee. Autopay tells you what to charge.**

4. **Charge the customer** with whatever payment method they have on file with you.

5. **Handle the cancel callback.** If the session went into an error state in Autopay, you get a
   cancel callback instead. Do not charge; release any authorisation you are holding.

## Callback endpoint requirements

- Return **2xx**. A `404` also stops retries; anything else triggers the retry ladder.
- Retry policy: exponential backoff from 1s, doubling to a 1-hour ceiling, then hourly until
  **one week** has passed, after which the callback is abandoned.
- **Callbacks may be delivered more than once.** De-duplicate on `parking_id` — Autopay's own
  guidance is to treat it as an idempotency key. This is your obligation; Autopay offers no
  idempotency mechanism of its own.

## Manual stop — read this before you use it

`POST /payment/v1/manual_stop` with `parking_id`, `reference` and `end_time` exists for **one**
case: Autopay missed an exit event (for example the operator's ANPR failed to read the vehicle
leaving). It is **not** a way to let a customer end their parking from your app, and it is
**not** an undo — Autopay closes the session, sends a success callback with a real cost up to
your `end_time`, and internally opens a follow-up session in case the vehicle is still on site.
If the vehicle really does leave later, Autopay handles that follow-up itself; you will not get
another callback and you must not charge again.

## Session states

| State | Meaning |
|---|---|
| Ended | Normal exit, finalised. You get a success callback and charge. |
| Cancelled | Errored in Autopay. Do not charge. |
| Manually stopped | You asked for a stop. Leads to Ended with a success callback. |

## Errors

`forbidden` (403), `missing_property` (400), `message_not_readable` (400),
`method_not_supported` (400), `argument_type_mismatch` (400), `server_communication_error`
(400), `operator_not_found_error` (400), `missing_operator_token_error` (400),
`internal_server_error` (500). The Payment API is the only page in the Autopay reference that
publishes an HTTP status per error id.
