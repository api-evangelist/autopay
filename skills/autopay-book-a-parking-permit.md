---
name: autopay-book-a-parking-permit
description: Reserve a parking permit for a vehicle through the Autopay Booking API — check availability, create the booking, amend it, and cancel it while it is still cancellable.
api: Autopay Booking API
provider: autopay
docs: https://developer.autopay.io/booking_api/
generated: '2026-09-06'
method: generated
source: https://developer.autopay.io/booking_api/
operations:
  - GET /booking/v3/permit_definitions
  - GET /booking/v3/availability
  - POST /booking/v3
  - GET /booking/v3/{id}/status
  - PUT /booking/v3/{id}
  - DELETE /booking/v3/{id}
---

# Book a parking permit

Requires a token with scope `permit_booking` — see `autopay-authenticate`. Booking is a paid
service; access is granted by the operator under Operator mode → Landlords → Tenants → API
Accesses.

## Steps

1. **List what you can book.** `GET /booking/v3/permit_definitions` returns the permit
   definitions available to your tenant, with their joint access limit. Keep the
   `permit_definition_id` (a UUID since v3).

2. **Check availability before you commit.** `GET /booking/v3/availability?valid_from={URL-encoded ISO 8601}`.
   This is the only rehearsal this API offers — there is no dry-run mode and no sandbox. If you
   skip it you will find out by receiving `availability_limit_error` ("Concurrent booking limit
   exceeded for that time period") after the fact.

3. **Create the booking.** `POST /booking/v3` with `Content-Type: application/json`. Pick the
   type first, because the two types have mutually exclusive fields:

   - `type: "FIXED"` — `valid_from` **and** `valid_to` are required, `duration` must be null,
     `expiration_time` must be null.
   - `type: "ENTRY"` — `valid_from` must be null, and one of `valid_to` or `duration` must be
     set. `expiration_time` is optional and defaults to **one year** after creation; the client
     must take the booking into use before it.

   Other fields: `license_plate_number` (required unless `anonymous_booking` is true),
   `permit_definition_id`, `usable_once` (default false — when false the vehicle may re-enter
   during the validity period), `comment`, and `operator_data` for operator-specific payload
   such as payment, client or flight information.

   Use `anonymous_booking: true` when you do not know the vehicle yet; the customer links a
   plate later at a kiosk.

4. **Poll status sparingly.** `GET /booking/v3/{id}/status` returns one of `NOT_USED`,
   `IN_USE`, `USED` or `EXPIRED`. **You get one query per 900 seconds per booking per client**
   (`query_limit_error`). There is no booking webhook, so 15 minutes is the floor on how fresh
   your view of a booking can be. Do not build a tight polling loop.

5. **Amend, within the rules.** `PUT /booking/v3/{id}`:
   - `id`, `type` and the anonymous flag can **never** change.
   - `valid_from` and `license_plate_number` cannot change once the booking is `IN_USE`.
   - `USED` and `EXPIRED` bookings cannot be changed at all.

6. **Cancel while you still can.** `DELETE /booking/v3/{id}` works only while the booking has
   not been used. Once used you get `delete_booking_error_booking_used` — "Booking is already
   used, cannot delete". Check the status first if the cancellation matters.

## Conventions that bite here

- All v3 parameters are snake_case (`valid_from`, not `validFrom`) and all v3 response
  timestamps are UTC (`2023-03-17T00:00:00+0000`).
- There is **no idempotency key**. A retried `POST /booking/v3` creates a second booking. If a
  create times out, list or check before retrying.
- Booking v1 and v2 are deprecated with effect from **5 November 2026**. Use v3.

## Errors worth branching on

`invalid_type_error`, `invalid_fixed_type_error`, `invalid_entry_type_error`,
`invalid_expiration_time_error`, `invalid_permit_definition_error`, `availability_limit_error`,
`query_limit_error`, `booking_not_found_error`, `delete_booking_error_booking_used`,
`invalid_booking_error` / `invalid_booking_update_error` (the `message` says why validation
failed), `invalid_tenant_error`. Full catalog: `errors/autopay-problem-types.yml`.
