---
name: autopay-authenticate
description: Mint and cache an Autopay API access token with OAuth 2.0 client credentials, and attach it correctly to every subsequent Autopay call.
api: Autopay
provider: autopay
docs: https://developer.autopay.io/authentication/
generated: '2026-09-06'
method: generated
source: https://developer.autopay.io/authentication/
operations:
  - POST https://api-auth.autopay.io/oauth/token
---

# Authenticate against the Autopay API

Every Autopay API uses the same mechanism. Do this once per credential set, then reuse the token.

## Before you start

You need a `client_id` and `client_secret`. They are **not self-serve** — a human at Autopay
issues them, and they are bound to **one operator**. If you act for several operators, you hold
one pair per operator and must send the right pair for the facility you are touching. Using one
operator's credentials against another operator's facilities returns an error.

## Steps

1. **Request a token.**

   ```
   POST https://api-auth.autopay.io/oauth/token
   Content-Type: application/json

   {
     "client_id": "<your client id>",
     "client_secret": "<your client secret>",
     "audience": "https://api.autopay.io",
     "grant_type": "client_credentials"
   }
   ```

   The body is **JSON**, not `application/x-www-form-urlencoded`. A generic OAuth client
   configured for form encoding will fail here.

2. **Read the response.** You get `access_token`, `scope`, `expires_in` and `token_type`
   (`Bearer`). The `scope` string tells you which Autopay APIs this token can reach — for
   example `customer_club`.

3. **Cache the token for its full `expires_in`.** Autopay states that "generating excessive
   access tokens within the expiration time (i.e. requesting a new one for each request) may
   lead to termination of API access." Expiry is typically 10–24 hours. This is the single most
   important rule on this API: the penalty for over-minting is loss of access, not a 429.

4. **Attach it to every call.**

   ```
   Authorization: Bearer <access_token>
   ```

5. **Refresh on expiry, not on failure.** Track the expiry yourself. There is no refresh token
   in the client-credentials flow — request a fresh token the same way.

## Scopes

Some endpoints need a named scope on the token. The reference names three:

| Scope | Needed for |
|---|---|
| `permit_booking` | Booking API |
| `customer_club` | Customer Club API |
| `zone_status` | Status API |

Ask your Autopay representative for the scopes your integration needs at credential issue time;
there is no self-service way to add one.

## Errors

| What you see | What it means |
|---|---|
| `401` `{"error":"access_denied","error_description":"Unauthorized"}` | Bad `client_id` or `client_secret` at the token endpoint. |
| `401` `{"error_id":"authentication_error","message":"No access token present in header!"}` | You called `api.autopay.io` with no `Authorization` header. |
| `forbidden` | The token is valid but lacks the scope or operator context for this API. |
| `missing_operator_token_error` / `missing_tenant_id_token_error` / `missing_landlord_id_token_error` | The credential itself is misconfigured on Autopay's side — the tenancy claims are read from the token, not from your request. Contact partner-support@autopay.io. |

## Discovery

The authorization server publishes `https://api-auth.autopay.io/.well-known/openid-configuration`
(issuer, token endpoint, `jwks_uri`, RS256). It is a reduced machine-to-machine document — there
is no `authorization_endpoint`, because there is no user-facing flow.
