---
name: autopay-export-invoices-and-statistics
description: Pull Autopay invoice and parking-statistics data into an accounting, ERP or BI system without gaps or double-counting.
api: Autopay Accounting API, Autopay Statistics API
provider: autopay
docs: https://developer.autopay.io/accounting/
generated: '2026-09-06'
method: generated
source: https://developer.autopay.io/accounting/, https://developer.autopay.io/statistics_api/
operations:
  - GET /accounting/v1/invoices
  - GET /statistics/v1/parking
---

# Export invoices and parking statistics

Both exports are read-only, both are paid services, and both share the same two traps: you must
choose one date-parameter pair, and you must chain windows so you neither skip nor re-import
rows.

## Choose your date axis — you may not use both

`GET /accounting/v1/invoices` accepts **either**:

- `from` / `to` — the time the data became available or was updated in the API. Use this to run
  continuously and pick up everything new.
- `invoice_date_from` / `invoice_date_to` — the invoice date itself. Use this to fetch a fixed
  accounting period, e.g. all invoices for March.

Sending both returns `accounting_service_invalid_date_error` ("Can search either by 'from' and
'to' OR 'updated_at_from' and 'updated_at_to'"). `GET /statistics/v1/parking` behaves the same
way and returns `search_param_error`. A `to_date` in the future returns
`accounting_service_invalid_to_date_error`.

All values are ISO 8601 and must be **URL-encoded** — `2016-02-02T12:15:00+0200` becomes
`2016-02-02T12:15:00%2B0200`. The `+` is the part people get wrong.

## Chain the windows

Carry the exact `to` (or `invoice_date_to`) value from the previous request forward as the next
request's `from`. This is Autopay's own instruction and it exists to prevent data loss at the
boundary.

**Do not run this in real time.** "Data is not propagated to the Accounting API in real-time;
therefore, all the queries should be delayed as well and not made in real-time." Run on a lag.

## Paginate with the cursor you were given

The large exports return an opaque `cursor`. Replay it verbatim on the next call. Constructing
or mutating one returns `cursor_decoding_error` / "Invalid cursor."

## Download the attachments, do not store their URLs

Invoice items carry receipts (for paid items) and ANPR entry/exit images (for unpaid items).
Since the deprecation that took effect **19 August 2026** these are JWT-protected: use
`receipt_url_with_auth` and `image_url_with_auth`. The old `receipt_url` / `image_url` fields
now literally return the string `"Use image_url_with_auth instead!"`.

"Downloadable items are only available for some time after the transaction, so it is recommended
to download receipts and event images you want to store when fetching the data. Only storing the
URL is not recommended."

## Access scoping

Accounting credentials are cut by invoice status — PAID only, UNPAID only, or both. Ask for what
you need at credential issue; using an endpoint outside your grant returns
`accounting_missing_scope_error`.

## Field change to watch

The Statistics API removes `parkings.payments.id` with effect from **5 November 2026**. Move to
`parkings.payments.payment_id` now.

## Errors

`accounting_service_invalid_date_error`, `accounting_service_invalid_to_date_error`,
`accounting_missing_scope_error`, `accounting_unexpected_error`, `search_param_error`,
`missing_updated_at_error`, `cursor_decoding_error`, `operator_not_found_error`, plus the shared
`forbidden` / `internal_server_error` / `missing_property` / `argument_type_mismatch` set.
