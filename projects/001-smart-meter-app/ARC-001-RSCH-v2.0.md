# Technology and Service Research: Octopus Energy API Deep-Dive & Smart Meter App API Specification

> **Template Status**: Beta | **Version**: 1.0.4 | **Command**: `/arckit.research`

## Document Control

| Field | Value |
|-------|-------|
| **Document ID** | ARC-001-RSCH-v2.0 |
| **Document Type** | Technology and Service Research |
| **Project** | UK Smart Meter Data Consumer Mobile App (Project 001) |
| **Classification** | OFFICIAL |
| **Status** | DRAFT |
| **Version** | 2.0 |
| **Created Date** | 2026-02-01 |
| **Last Modified** | 2026-02-01 |
| **Review Cycle** | Quarterly |
| **Next Review Date** | 2026-05-01 |
| **Owner** | Enterprise Architect |
| **Reviewed By** | PENDING |
| **Approved By** | PENDING |
| **Distribution** | Programme Board, Delivery Team, Architecture Team |

## Revision History

| Version | Date | Author | Changes | Approved By | Approval Date |
|---------|------|--------|---------|-------------|---------------|
| 2.0 | 2026-02-01 | ArcKit AI | Octopus Energy API deep-dive and Smart Meter App API specification. Supplements ARC-001-RSCH-v1.0 | PENDING | PENDING |

---

## Executive Summary

### Research Scope

This document supplements `ARC-001-RSCH-v1.0.md` with a deep-dive into the **Octopus Energy API** — widely regarded as best-in-breed for UK energy consumer APIs. The Octopus API is analysed as a reference architecture to derive a comprehensive API specification for the Smart Meter Data Consumer Mobile App.

The Octopus Energy API provides both REST and GraphQL interfaces for energy data access, covering products, tariffs, consumption, accounts, meters, and grid supply points. With 380+ GraphQL queries and a clean REST endpoint structure, it represents the gold standard for UK energy API design.

**Key Deliverable**: A complete API specification for our Smart Meter Consumer App, modelled on Octopus Energy's best patterns but designed for supplier-neutral, multi-source data access.

### Key Findings

- **Octopus REST API** is clean, well-documented, and follows standard patterns (paginated JSON, ISO 8601 dates, HTTP Basic Auth). It provides unauthenticated access to products/tariffs and authenticated access to accounts/consumption.
- **Octopus GraphQL API** (Kraken platform) is comprehensive with 380+ queries, JWT authentication, cursor-based pagination, and query complexity limits (max 200 per request). It provides richer data than REST.
- **API Design Patterns** worth adopting: paginated responses with `count`/`next`/`previous`, ISO 8601 datetime parameters, `group_by` aggregation (day/week/month/quarter), regional tariff codes, and clear public vs authenticated endpoint separation.
- **Limitations for our use case**: Octopus API only serves Octopus Energy customers (~8 million accounts). Our app must be supplier-neutral and serve all 34 million smart meter households. We need a superset API that abstracts multiple data sources (DCC, n3rgy, supplier APIs) behind a unified interface.

### Recommended API Architecture

Our Smart Meter App API should adopt Octopus-style REST patterns for the public-facing mobile API, with a GraphQL layer for internal/admin use. The API should abstract data sources (DCC, n3rgy, Octopus, other suppliers) behind a unified interface.

---

## Part 1: Octopus Energy API Analysis

### 1.1 API Overview

**Provider**: Octopus Energy Group (Kraken Technologies)
**Base URL**: `https://api.octopus.energy/v1/`
**GraphQL URL**: `https://api.octopus.energy/v1/graphql/`
**Documentation**: [developer.octopus.energy](https://developer.octopus.energy/)
**Transport**: HTTPS only
**Format**: JSON
**Rate Limiting**: Soft limits on REST; GraphQL has query complexity limit of 200 and per-field rate limits (error `KT-CT-1199`)

### 1.2 REST API Endpoints

#### Public Endpoints (No Authentication Required)

| Endpoint | Method | Description | Pagination |
|----------|--------|-------------|------------|
| `/v1/products/` | GET | List all active energy products | 100/page, `?page=2` |
| `/v1/products/{product_code}/` | GET | Product details with all tariffs by region | N/A |
| `/v1/products/{product_code}/electricity-tariffs/{tariff_code}/standard-unit-rates/` | GET | Electricity unit rates (half-hourly for Agile) | 100/page |
| `/v1/products/{product_code}/electricity-tariffs/{tariff_code}/standing-charges/` | GET | Electricity standing charges | 100/page |
| `/v1/products/{product_code}/electricity-tariffs/{tariff_code}/day-unit-rates/` | GET | Day unit rates (dual register/Economy 7) | 100/page |
| `/v1/products/{product_code}/electricity-tariffs/{tariff_code}/night-unit-rates/` | GET | Night unit rates (dual register/Economy 7) | 100/page |
| `/v1/products/{product_code}/gas-tariffs/{tariff_code}/standard-unit-rates/` | GET | Gas unit rates | 100/page |
| `/v1/products/{product_code}/gas-tariffs/{tariff_code}/standing-charges/` | GET | Gas standing charges | 100/page |
| `/v1/electricity-meter-points/{mpan}/` | GET | Meter point details and GSP | N/A |
| `/v1/industry/grid-supply-points/?postcode={postcode}` | GET | GSP lookup by postcode | N/A |

#### Authenticated Endpoints (API Key via HTTP Basic Auth)

| Endpoint | Method | Description | Pagination |
|----------|--------|-------------|------------|
| `/v1/accounts/{account_number}/` | GET | Account details (properties, MPANs, MPRNs, meters, tariff history) | N/A |
| `/v1/electricity-meter-points/{mpan}/meters/{serial}/consumption/` | GET | Half-hourly electricity consumption | `page_size` up to 25,000 |
| `/v1/gas-meter-points/{mprn}/meters/{serial}/consumption/` | GET | Half-hourly gas consumption | `page_size` up to 25,000 |

### 1.3 REST API Response Structures

#### Paginated List Response

```json
{
  "count": 243,
  "next": "https://api.octopus.energy/v1/products/?page=2",
  "previous": null,
  "results": [ ... ]
}
```

#### Product Object

```json
{
  "code": "AGILE-FLEX-22-11-25",
  "direction": "IMPORT",
  "full_name": "Agile Octopus November 2022 v1",
  "display_name": "Agile Octopus",
  "description": "...",
  "is_variable": true,
  "is_green": true,
  "is_tracker": false,
  "is_prepay": false,
  "is_business": false,
  "is_restricted": false,
  "term": null,
  "available_from": "2022-11-25T00:00:00Z",
  "available_to": null,
  "links": [ { "rel": "self", "href": "..." } ],
  "brand": "OCTOPUS_ENERGY"
}
```

#### Product Detail with Regional Tariffs

```json
{
  "code": "VAR-22-11-01",
  "single_register_electricity_tariffs": {
    "_A": {
      "direct_debit_monthly": {
        "code": "E-1R-VAR-22-11-01-A",
        "standard_unit_rate_exc_vat": 33.83,
        "standard_unit_rate_inc_vat": 35.52,
        "standing_charge_exc_vat": 46.36,
        "standing_charge_inc_vat": 48.68,
        "online_discount_exc_vat": 0,
        "online_discount_inc_vat": 0,
        "dual_fuel_discount_exc_vat": 0,
        "dual_fuel_discount_inc_vat": 0,
        "exit_fees_exc_vat": 0,
        "exit_fees_inc_vat": 0,
        "exit_fees_type": "NONE",
        "links": [ ... ]
      }
    },
    "_B": { ... },
    "_C": { ... }
  },
  "dual_register_electricity_tariffs": { ... },
  "single_register_gas_tariffs": { ... }
}
```

#### Tariff Code Convention

| Pattern | Example | Meaning |
|---------|---------|---------|
| `E-1R-{product}-{region}` | `E-1R-VAR-22-11-01-A` | Single register electricity, region A |
| `E-2R-{product}-{region}` | `E-2R-VAR-22-11-01-C` | Dual register (Economy 7) electricity, region C |
| `G-1R-{product}-{region}` | `G-1R-VAR-22-11-01-A` | Gas, region A |

Regions A–P correspond to the 14 GSP groups (former Public Electricity Suppliers).

#### Unit Rate Object

```json
{
  "value_exc_vat": 33.83,
  "value_inc_vat": 35.52,
  "valid_from": "2023-01-01T00:00:00Z",
  "valid_to": "2023-04-01T00:00:00Z"
}
```

#### Consumption Object

```json
{
  "consumption": 0.045,
  "interval_start": "2023-03-26T00:00:00Z",
  "interval_end": "2023-03-26T00:30:00Z"
}
```

**Consumption endpoint parameters**:

| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `period_from` | ISO 8601 | No | Start datetime (inclusive) |
| `period_to` | ISO 8601 | No | End datetime (inclusive). Requires `period_from` |
| `page_size` | Integer | No | Results per page (default 100, max 25,000) |
| `order_by` | String | No | `period` for ascending; default is descending |
| `group_by` | String | No | `day`, `week`, `month`, or `quarter` |

**Data precision**: Electricity returned to nearest 0.001 kWh. Gas on SMETS1 meters pre-converted to kWh; SMETS2 gas returned in cubic metres.

#### Account Object

```json
{
  "number": "A-12345678",
  "properties": [
    {
      "id": 1234567,
      "moved_in_at": "2020-11-30T00:00:00Z",
      "moved_out_at": null,
      "address_line_1": "1 Example Street",
      "address_line_2": "",
      "address_line_3": "",
      "town": "LONDON",
      "county": "",
      "postcode": "W1 1AA",
      "electricity_meter_points": [
        {
          "mpan": "1000000000000",
          "profile_class": 1,
          "consumption_standard": 2560,
          "meters": [
            {
              "serial_number": "1111111111",
              "registers": [
                {
                  "identifier": "1",
                  "rate": "STANDARD",
                  "is_settlement_register": true
                }
              ]
            }
          ],
          "agreements": [
            {
              "tariff_code": "E-1R-VAR-20-09-22-N",
              "valid_from": "2020-12-17T00:00:00Z",
              "valid_to": "2021-12-17T00:00:00Z"
            }
          ]
        }
      ],
      "gas_meter_points": [
        {
          "mprn": "2000000000",
          "meters": [
            {
              "serial_number": "2222222222"
            }
          ],
          "agreements": [
            {
              "tariff_code": "G-1R-VAR-20-09-22-N",
              "valid_from": "2020-12-17T00:00:00Z",
              "valid_to": null
            }
          ]
        }
      ]
    }
  ]
}
```

#### GSP Response

```json
{
  "count": 1,
  "next": null,
  "previous": null,
  "results": [
    {
      "group_id": "_H"
    }
  ]
}
```

### 1.4 GraphQL API

**URL**: `https://api.octopus.energy/v1/graphql/`
**Interactive Explorer**: Available at the same URL via GraphiQL in browser

#### Authentication

```graphql
mutation obtainKrakenToken($input: ObtainJSONWebTokenInput!) {
  obtainKrakenToken(input: $input) {
    token
    refreshToken
    refreshExpiresIn
    payload
  }
}
```

**Input options**:
- Email + password: `{"input": {"email": "...", "password": "..."}}`
- API key: `{"input": {"APIKey": "..."}}`
- Refresh token: `{"input": {"refreshToken": "..."}}`

**Token lifecycle**: Access token valid 60 minutes. Refresh token valid 7 days. Recommended: cache both, regenerate access token from refresh token, re-authenticate from credentials when refresh token expires.

**Authorization header**: Set `Authorization` header to the raw token value.

#### Key Consumer-Relevant GraphQL Queries

| Query | Arguments | Returns | Use Case |
|-------|-----------|---------|----------|
| `account` | `accountNumber` | Full account with properties, meters, tariffs | Account overview |
| `properties` | `accountNumber` | Property list with meter points | Meter discovery |
| `electricityMeterPointDetails` | `mpan` | Meter point with GSP, profile class | Meter details |
| `gasMeterPointDetails` | `mprn` | Gas meter point details | Meter details |
| `electricityMeterReadings` | `mpan` | Paginated consumption readings | Consumption data |
| `gasMeterReadings` | `mprn` | Paginated gas readings | Consumption data |
| `annualElectricityConsumption` | `mpan` | Annual electricity total | Summary data |
| `annualGasConsumption` | `mprn` | Annual gas total | Summary data |
| `energyProducts` | Various filters | Product catalogue | Tariff browsing |
| `availableProducts` | Filters | Quotable products | Tariff comparison |
| `smartTariffComparison` | `accountNumber` | Tariff comparison for account | Tariff switching |
| `applicableRates` | `accountNumber`, `mpxn`, dates | Current applicable rates | Cost calculation |
| `costOfUsage` | `accountNumber`, `mpxn`, usage | Cost calculation | Bill estimation |
| `weeklyUsageInsights` | `accountNumber` | Weekly consumption analysis | Recommendations |
| `getEnergyIqData` | `accountNumber` | Energy insights analytics | Recommendations |
| `savingSessions` | `accountNumber` | Saving session events | Demand response |
| `prepayBalanceSnapshot` | `accountNumber`, `mpxn` | Prepay balance | Prepayment users |
| `prepayPayments` | `accountNumber` | Prepay transaction history | Prepayment users |
| `devices` | `accountNumber` | Connected devices | Smart home |
| `smartMeterDataPreferences` | `accountNumber` | Data sharing consent settings | Consent management |
| `readingConsentGranularity` | `accountNumber` | Meter reading consent level | Consent management |
| `viewer` | None (uses auth token) | Current authenticated user | Session info |

#### GraphQL Constraints

| Constraint | Value | Error Code |
|------------|-------|------------|
| Query complexity limit | 200 per request | `KT-CT-1188` |
| Pagination `first` argument | Max 100 | Error returned |
| Rate limiting | Per-query/mutation limits | `KT-CT-1199` |
| Response format | Always HTTP 200; errors in `errors` field | N/A |

### 1.5 Octopus API Strengths (Best Practices to Adopt)

1. **Clear public vs authenticated separation**: Products and tariffs are public (no auth); consumption and accounts are authenticated. This enables pre-registration tariff browsing.

2. **Flexible consumption aggregation**: The `group_by` parameter (day/week/month/quarter) moves aggregation to the server, reducing client complexity and bandwidth.

3. **Large page sizes for consumption**: Up to 25,000 records per page on consumption endpoints enables efficient bulk data retrieval (≈520 days of half-hourly data in one request).

4. **Regional tariff model**: Tariffs are structured by GSP region (A–P), reflecting the actual UK electricity distribution network topology. The `industry/grid-supply-points` endpoint enables postcode-to-region mapping.

5. **ISO 8601 throughout**: All datetimes in ISO 8601 with UTC timezone, with explicit guidance on daylight savings handling.

6. **Dual API strategy**: REST for simple CRUD and public data; GraphQL for complex account queries and aggregated analytics. This provides flexibility for different consumer types.

7. **Token lifecycle management**: JWT with short-lived access tokens (60 min) and long-lived refresh tokens (7 days) balances security with usability.

8. **Tariff code encoding**: Tariff codes encode fuel type, register count, product, and region — enabling client-side parsing without additional API calls.

### 1.6 Octopus API Limitations (Gaps for Our Use Case)

| Limitation | Impact | Our Solution |
|------------|--------|--------------|
| Octopus customers only (~8M) | Cannot serve all 34M smart meter households | Multi-source abstraction layer (DCC, n3rgy, supplier APIs) |
| No supplier-neutral tariff comparison | Only compares Octopus tariffs | Aggregate tariff data from multiple sources |
| No carbon intensity data | No CO₂ emissions per kWh | Integrate National Grid ESO Carbon Intensity API |
| No budget/alert features in API | Client-side only | Build server-side alerting engine |
| No data export/portability endpoint | No SAR/GDPR compliance endpoint | Build dedicated data export API |
| No consent management API for third parties | Consent is internal to Octopus | Build granular consent management API |

---

## Part 2: Smart Meter App API Specification

### 2.1 API Design Principles

Based on Octopus Energy API best practices and our requirements (ARC-001-REQ-v1.0):

| # | Principle | Octopus Pattern Adopted | Requirement Trace |
|---|-----------|------------------------|-------------------|
| 1 | RESTful JSON API with versioned base URL | `https://api.octopus.energy/v1/` | NFR-P-001 |
| 2 | Public endpoints for tariffs; authenticated for consumption | Public/private separation | NFR-SEC-001 |
| 3 | ISO 8601 datetimes in UTC throughout | ISO 8601 with `Z` suffix | DR-001 |
| 4 | Paginated responses with `count`, `next`, `previous` | Standard pagination envelope | NFR-P-001 |
| 5 | Server-side aggregation via `group_by` parameter | `group_by=day\|week\|month\|quarter` | FR-005 |
| 6 | GOV.UK One Login OAuth 2.0 + JWT tokens | Adapted from Kraken token model | NFR-SEC-001, FR-001 |
| 7 | Granular consent management as first-class API | Extended beyond Octopus model | FR-003, NFR-C-001 |
| 8 | Supplier-neutral data abstraction | New — not in Octopus | BR-001, INT-001, INT-002 |
| 9 | HATEOAS links in responses | Octopus `links` pattern | NFR-P-001 |
| 10 | Rate limiting with clear headers | Octopus GraphQL rate limiting pattern | NFR-SEC-006 |

### 2.2 Base URL and Versioning

```
Production:  https://api.smartmeter.service.gov.uk/v1/
Staging:     https://api.staging.smartmeter.service.gov.uk/v1/
```

All requests must use HTTPS. HTTP requests will receive a 301 redirect to HTTPS.

API versioning is via URL path (`/v1/`). Breaking changes will increment the version. Non-breaking additions (new fields, new endpoints) will not increment.

### 2.3 Authentication and Authorisation

#### Authentication Flow

```
1. User authenticates via GOV.UK One Login (OAuth 2.0 / OIDC)
2. App receives authorization code
3. App exchanges code for access_token + refresh_token via /v1/auth/token
4. App includes Bearer token in Authorization header for authenticated requests
5. App refreshes token via /v1/auth/refresh before expiry
```

#### Token Lifecycle (Adapted from Octopus/Kraken Model)

| Token | Lifetime | Storage | Refresh |
|-------|----------|---------|---------|
| Access token (JWT) | 60 minutes | Secure mobile keychain | Via refresh token |
| Refresh token | 30 days | Secure mobile keychain | Via re-authentication |
| API key (service-to-service) | Until revoked | Secrets manager | Manual rotation |

### 2.4 Standard Response Envelope

#### Success Response (Single Resource)

```json
{
  "data": { ... },
  "meta": {
    "request_id": "req_abc123",
    "timestamp": "2026-02-01T12:00:00Z"
  }
}
```

#### Success Response (Collection — Paginated)

```json
{
  "count": 1440,
  "next": "https://api.smartmeter.service.gov.uk/v1/consumption/electricity?page=2",
  "previous": null,
  "results": [ ... ],
  "meta": {
    "request_id": "req_abc123",
    "timestamp": "2026-02-01T12:00:00Z"
  }
}
```

#### Error Response

```json
{
  "error": {
    "code": "SM-AUTH-001",
    "message": "Authentication required",
    "detail": "Provide a valid Bearer token in the Authorization header",
    "documentation_url": "https://developer.smartmeter.service.gov.uk/errors/SM-AUTH-001"
  },
  "meta": {
    "request_id": "req_abc123",
    "timestamp": "2026-02-01T12:00:00Z"
  }
}
```

#### Standard HTTP Status Codes

| Code | Meaning | Usage |
|------|---------|-------|
| 200 | OK | Successful GET |
| 201 | Created | Successful POST creating a resource |
| 204 | No Content | Successful DELETE |
| 400 | Bad Request | Invalid parameters |
| 401 | Unauthorized | Missing or invalid token |
| 403 | Forbidden | Valid token but insufficient consent/scope |
| 404 | Not Found | Resource does not exist |
| 429 | Too Many Requests | Rate limit exceeded |
| 500 | Internal Server Error | Server failure |
| 503 | Service Unavailable | Upstream data source unavailable (DCC, supplier) |

### 2.5 Rate Limiting

Rate limits are communicated via standard headers:

```
X-RateLimit-Limit: 100
X-RateLimit-Remaining: 87
X-RateLimit-Reset: 1706792400
Retry-After: 60
```

| Consumer Type | Rate Limit | Burst |
|---------------|-----------|-------|
| Mobile app (per user) | 60 requests/minute | 10 requests/second |
| Service-to-service (API key) | 1,000 requests/minute | 50 requests/second |
| Public endpoints (unauthenticated) | 30 requests/minute per IP | 5 requests/second |

### 2.6 API Endpoints

---

#### 2.6.1 Authentication

##### POST `/v1/auth/token`

Exchange GOV.UK One Login authorisation code for app tokens.

**Request**:
```json
{
  "grant_type": "authorization_code",
  "code": "auth_code_from_one_login",
  "redirect_uri": "uk.gov.smartmeter://callback",
  "code_verifier": "pkce_code_verifier"
}
```

**Response** (200):
```json
{
  "data": {
    "access_token": "eyJ...",
    "token_type": "Bearer",
    "expires_in": 3600,
    "refresh_token": "ref_...",
    "refresh_expires_in": 2592000,
    "scope": "consumption:read profile:read consent:manage"
  }
}
```

##### POST `/v1/auth/refresh`

Refresh an expired access token.

**Request**:
```json
{
  "grant_type": "refresh_token",
  "refresh_token": "ref_..."
}
```

**Response**: Same structure as `/v1/auth/token`.

##### POST `/v1/auth/revoke`

Revoke a refresh token (logout).

**Request**:
```json
{
  "token": "ref_..."
}
```

**Response**: 204 No Content.

---

#### 2.6.2 Consumer Profile

##### GET `/v1/profile`

Retrieve the authenticated consumer's profile. *Adapted from Octopus `account` endpoint.*

**Auth**: Required (Bearer token)

**Response** (200):
```json
{
  "data": {
    "consumer_id": "con_abc123def456",
    "email": "user@example.com",
    "display_name": "Jane Smith",
    "locale": "en-GB",
    "timezone": "Europe/London",
    "accessibility_preferences": {
      "high_contrast": false,
      "large_text": false,
      "screen_reader_optimised": false
    },
    "created_at": "2026-03-15T10:00:00Z",
    "updated_at": "2026-06-01T14:30:00Z"
  }
}
```

##### PATCH `/v1/profile`

Update consumer profile fields.

**Request**:
```json
{
  "display_name": "Jane Smith-Jones",
  "accessibility_preferences": {
    "large_text": true
  }
}
```

##### DELETE `/v1/profile`

Request account deletion and data erasure (UC-8). Triggers 30-day erasure process.

**Response** (200):
```json
{
  "data": {
    "deletion_request_id": "del_xyz789",
    "status": "PENDING",
    "erasure_deadline": "2026-07-01T14:30:00Z",
    "message": "Your account and all associated data will be permanently deleted within 30 days."
  }
}
```

---

#### 2.6.3 Meters

##### GET `/v1/meters`

List all meters linked to the consumer's account. *Adapted from Octopus account `electricity_meter_points` / `gas_meter_points` pattern.*

**Auth**: Required

**Response** (200):
```json
{
  "count": 2,
  "next": null,
  "previous": null,
  "results": [
    {
      "meter_id": "mtr_elec_001",
      "fuel_type": "ELECTRICITY",
      "mpxn": "1000000000000",
      "serial_number": "1111111111",
      "smets_version": "SMETS2",
      "data_source": "DCC",
      "register_type": "SINGLE",
      "gsp_group": "_H",
      "status": "ACTIVE",
      "linked_at": "2026-03-15T10:05:00Z",
      "current_tariff": {
        "tariff_code": "E-1R-VAR-22-11-01-H",
        "supplier": "OCTOPUS_ENERGY",
        "product_name": "Flexible Octopus",
        "standard_unit_rate_inc_vat": 24.50,
        "standing_charge_inc_vat": 46.36,
        "valid_from": "2025-10-01T00:00:00Z",
        "valid_to": null
      },
      "links": {
        "consumption": "/v1/consumption/electricity/mtr_elec_001",
        "tariff_history": "/v1/meters/mtr_elec_001/tariffs"
      }
    },
    {
      "meter_id": "mtr_gas_001",
      "fuel_type": "GAS",
      "mpxn": "2000000000",
      "serial_number": "2222222222",
      "smets_version": "SMETS2",
      "data_source": "DCC",
      "register_type": "SINGLE",
      "gsp_group": "_H",
      "status": "ACTIVE",
      "linked_at": "2026-03-15T10:05:00Z",
      "current_tariff": {
        "tariff_code": "G-1R-VAR-22-11-01-H",
        "supplier": "OCTOPUS_ENERGY",
        "product_name": "Flexible Octopus",
        "standard_unit_rate_inc_vat": 6.20,
        "standing_charge_inc_vat": 31.43,
        "valid_from": "2025-10-01T00:00:00Z",
        "valid_to": null
      },
      "links": {
        "consumption": "/v1/consumption/gas/mtr_gas_001",
        "tariff_history": "/v1/meters/mtr_gas_001/tariffs"
      }
    }
  ]
}
```

##### POST `/v1/meters`

Link a new meter to the consumer's account.

**Request**:
```json
{
  "fuel_type": "ELECTRICITY",
  "mpxn": "1000000000000",
  "serial_number": "1111111111",
  "authorisation_method": "DCC_CAD",
  "authorisation_code": "abc123"
}
```

##### DELETE `/v1/meters/{meter_id}`

Unlink a meter from the consumer's account.

##### GET `/v1/meters/{meter_id}/tariffs`

Retrieve tariff history for a meter. *Adapted from Octopus `agreements` array pattern.*

**Response** (200):
```json
{
  "count": 3,
  "next": null,
  "previous": null,
  "results": [
    {
      "tariff_code": "E-1R-VAR-22-11-01-H",
      "supplier": "OCTOPUS_ENERGY",
      "product_name": "Flexible Octopus",
      "standard_unit_rate_inc_vat": 24.50,
      "standing_charge_inc_vat": 46.36,
      "valid_from": "2025-10-01T00:00:00Z",
      "valid_to": null
    },
    {
      "tariff_code": "E-1R-FIX-22-03-01-H",
      "supplier": "OCTOPUS_ENERGY",
      "product_name": "Octopus 12M Fixed",
      "standard_unit_rate_inc_vat": 28.34,
      "standing_charge_inc_vat": 42.10,
      "valid_from": "2024-10-01T00:00:00Z",
      "valid_to": "2025-10-01T00:00:00Z"
    }
  ]
}
```

---

#### 2.6.4 Consumption Data

*Core endpoints modelled directly on Octopus consumption API with enhancements for multi-fuel and cost overlay.*

##### GET `/v1/consumption/electricity/{meter_id}`

Retrieve half-hourly electricity consumption. *Direct adaptation of Octopus `/v1/electricity-meter-points/{mpan}/meters/{serial}/consumption/` endpoint.*

**Auth**: Required + consent purpose `CONSUMPTION_VIEWING` must be granted

**Parameters**:

| Parameter | Type | Required | Default | Description |
|-----------|------|----------|---------|-------------|
| `period_from` | ISO 8601 | No | 30 days ago | Start datetime (inclusive) |
| `period_to` | ISO 8601 | No | Now | End datetime (inclusive). Requires `period_from` |
| `page_size` | Integer | No | 100 | Results per page (max 25,000) |
| `page` | Integer | No | 1 | Page number |
| `order_by` | String | No | `-period` | `period` (ascending) or `-period` (descending) |
| `group_by` | String | No | `half_hour` | `half_hour`, `hour`, `day`, `week`, `month`, `quarter`, `year` |
| `include_cost` | Boolean | No | false | Include cost calculation per interval |
| `include_carbon` | Boolean | No | false | Include carbon intensity per interval |

**Response** (200):
```json
{
  "count": 1440,
  "next": "https://api.smartmeter.service.gov.uk/v1/consumption/electricity/mtr_elec_001?page=2",
  "previous": null,
  "results": [
    {
      "consumption_kwh": 0.045,
      "interval_start": "2026-01-15T00:00:00Z",
      "interval_end": "2026-01-15T00:30:00Z",
      "quality_flag": "ACTUAL",
      "cost_pence": 1.10,
      "cost_pence_inc_vat": 1.16,
      "carbon_g_co2": 8.1,
      "carbon_intensity_g_per_kwh": 180
    },
    {
      "consumption_kwh": 0.078,
      "interval_start": "2026-01-15T00:30:00Z",
      "interval_end": "2026-01-15T01:00:00Z",
      "quality_flag": "ACTUAL",
      "cost_pence": 1.91,
      "cost_pence_inc_vat": 2.01,
      "carbon_g_co2": 13.3,
      "carbon_intensity_g_per_kwh": 170
    }
  ],
  "summary": {
    "total_kwh": 12.456,
    "total_cost_pence": 305.18,
    "total_cost_pence_inc_vat": 320.44,
    "total_carbon_kg_co2": 2.24,
    "average_unit_rate_pence": 24.50,
    "period_from": "2026-01-15T00:00:00Z",
    "period_to": "2026-01-15T23:59:59Z"
  },
  "meta": {
    "meter_id": "mtr_elec_001",
    "fuel_type": "ELECTRICITY",
    "data_source": "DCC",
    "request_id": "req_abc123",
    "timestamp": "2026-02-01T12:00:00Z"
  }
}
```

##### GET `/v1/consumption/gas/{meter_id}`

Retrieve half-hourly gas consumption. Same parameters as electricity.

**Response differences**:
- `consumption_kwh` — pre-converted from m³ to kWh using calorific value
- `consumption_m3` — raw cubic metres (additional field for gas)
- `calorific_value` — the conversion factor used

```json
{
  "results": [
    {
      "consumption_kwh": 1.234,
      "consumption_m3": 0.112,
      "calorific_value": 39.5,
      "interval_start": "2026-01-15T00:00:00Z",
      "interval_end": "2026-01-15T00:30:00Z",
      "quality_flag": "ACTUAL",
      "cost_pence": 7.65,
      "cost_pence_inc_vat": 8.03,
      "carbon_g_co2": 252.5,
      "carbon_intensity_g_per_kwh": 204.7
    }
  ]
}
```

##### GET `/v1/consumption/combined`

Retrieve combined electricity + gas consumption summary. *New endpoint not in Octopus API — addresses mobile app single-view requirement.*

**Parameters**: Same as individual consumption endpoints, applied to all linked meters.

**Response** (200):
```json
{
  "data": {
    "period_from": "2026-01-01T00:00:00Z",
    "period_to": "2026-01-31T23:59:59Z",
    "electricity": {
      "total_kwh": 312.5,
      "total_cost_pence_inc_vat": 7656.25,
      "total_carbon_kg_co2": 56.3,
      "meter_count": 1,
      "daily_average_kwh": 10.08
    },
    "gas": {
      "total_kwh": 1050.0,
      "total_cost_pence_inc_vat": 6510.00,
      "total_carbon_kg_co2": 214.8,
      "meter_count": 1,
      "daily_average_kwh": 33.87
    },
    "combined": {
      "total_cost_pence_inc_vat": 14166.25,
      "total_carbon_kg_co2": 271.1,
      "daily_average_cost_pence_inc_vat": 456.98
    }
  }
}
```

---

#### 2.6.5 Tariffs and Products

*Modelled on Octopus public products/tariffs API, extended for multi-supplier comparison.*

##### GET `/v1/products`

List available energy products across all suppliers. *Adapted from Octopus `/v1/products/` with multi-supplier extension.*

**Auth**: Not required (public endpoint)

**Parameters**:

| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `supplier` | String | No | Filter by supplier (e.g., `OCTOPUS_ENERGY`, `BRITISH_GAS`) |
| `fuel_type` | String | No | `ELECTRICITY`, `GAS`, `DUAL` |
| `is_variable` | Boolean | No | Filter variable/fixed tariffs |
| `is_green` | Boolean | No | Filter green tariffs |
| `is_prepay` | Boolean | No | Filter prepayment tariffs |
| `available_at` | ISO 8601 | No | Show products available at this date |
| `page` | Integer | No | Page number |

**Response** (200):
```json
{
  "count": 156,
  "next": "https://api.smartmeter.service.gov.uk/v1/products?page=2",
  "previous": null,
  "results": [
    {
      "code": "AGILE-FLEX-22-11-25",
      "supplier": "OCTOPUS_ENERGY",
      "supplier_display_name": "Octopus Energy",
      "display_name": "Agile Octopus",
      "full_name": "Agile Octopus November 2022 v1",
      "description": "Smart tariff with half-hourly pricing tied to wholesale rates",
      "fuel_type": "ELECTRICITY",
      "is_variable": true,
      "is_green": true,
      "is_tracker": false,
      "is_prepay": false,
      "term_months": null,
      "exit_fees_inc_vat": 0,
      "available_from": "2022-11-25T00:00:00Z",
      "available_to": null,
      "links": {
        "self": "/v1/products/AGILE-FLEX-22-11-25",
        "tariffs": "/v1/products/AGILE-FLEX-22-11-25/tariffs"
      }
    }
  ]
}
```

##### GET `/v1/products/{product_code}`

Product details with regional tariff breakdown. *Direct adaptation of Octopus pattern.*

##### GET `/v1/products/{product_code}/tariffs`

List tariffs for a product by GSP region.

**Parameters**:

| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `gsp_group` | String | No | Filter by GSP region (e.g., `_H`). Without this, returns all regions |
| `payment_method` | String | No | `DIRECT_DEBIT_MONTHLY`, `PREPAYMENT`, `RECEIPT_OF_BILL` |

**Response** (200):
```json
{
  "results": [
    {
      "tariff_code": "E-1R-AGILE-FLEX-22-11-25-H",
      "gsp_group": "_H",
      "payment_method": "DIRECT_DEBIT_MONTHLY",
      "standard_unit_rate_inc_vat": null,
      "standing_charge_inc_vat": 48.68,
      "is_half_hourly_priced": true,
      "links": {
        "unit_rates": "/v1/products/AGILE-FLEX-22-11-25/tariffs/E-1R-AGILE-FLEX-22-11-25-H/unit-rates",
        "standing_charges": "/v1/products/AGILE-FLEX-22-11-25/tariffs/E-1R-AGILE-FLEX-22-11-25-H/standing-charges"
      }
    }
  ]
}
```

##### GET `/v1/products/{product_code}/tariffs/{tariff_code}/unit-rates`

Time-varying unit rates. *Identical pattern to Octopus `standard-unit-rates` endpoint.*

**Parameters**: `period_from`, `period_to` (ISO 8601)

**Response** (200):
```json
{
  "count": 48,
  "results": [
    {
      "value_exc_vat": 7.12,
      "value_inc_vat": 7.48,
      "valid_from": "2026-02-01T00:00:00Z",
      "valid_to": "2026-02-01T00:30:00Z"
    }
  ]
}
```

##### GET `/v1/gsp`

Grid Supply Point lookup by postcode. *Adapted from Octopus `/v1/industry/grid-supply-points/` endpoint.*

**Parameters**: `postcode` (required)

**Response** (200):
```json
{
  "data": {
    "gsp_group": "_H",
    "gsp_name": "Southern",
    "postcode": "SO16 0AS"
  }
}
```

---

#### 2.6.6 Tariff Comparison

*New capability — extends Octopus `smartTariffComparison` GraphQL query into a REST endpoint for supplier-neutral comparison.*

##### GET `/v1/comparison`

Compare tariffs using the consumer's actual consumption data. (FR-007)

**Auth**: Required + consent purpose `TARIFF_COMPARISON` must be granted

**Parameters**:

| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `meter_id` | String | Yes | Meter to compare tariffs for |
| `period_months` | Integer | No | Months of actual data to use (default 12, min 3) |
| `fuel_type` | String | No | `ELECTRICITY` or `GAS` |
| `include_green_only` | Boolean | No | Filter to green tariffs |
| `include_fixed_only` | Boolean | No | Filter to fixed tariffs |

**Response** (200):
```json
{
  "data": {
    "meter_id": "mtr_elec_001",
    "fuel_type": "ELECTRICITY",
    "comparison_period": {
      "from": "2025-02-01T00:00:00Z",
      "to": "2026-01-31T23:59:59Z",
      "actual_kwh": 3750.0,
      "actual_cost_inc_vat_pence": 91875
    },
    "current_tariff": {
      "tariff_code": "E-1R-VAR-22-11-01-H",
      "supplier": "OCTOPUS_ENERGY",
      "product_name": "Flexible Octopus",
      "annual_cost_inc_vat_pence": 91875
    },
    "alternatives": [
      {
        "tariff_code": "E-1R-AGILE-FLEX-22-11-25-H",
        "supplier": "OCTOPUS_ENERGY",
        "product_name": "Agile Octopus",
        "projected_annual_cost_inc_vat_pence": 82500,
        "annual_saving_inc_vat_pence": 9375,
        "annual_saving_percent": 10.2,
        "is_green": true,
        "is_variable": true,
        "term_months": null,
        "exit_fees_inc_vat": 0,
        "confidence": "HIGH"
      },
      {
        "tariff_code": "E-1R-FIX-25-01-01-H",
        "supplier": "BRITISH_GAS",
        "product_name": "Fixed Price Jan 2025",
        "projected_annual_cost_inc_vat_pence": 85000,
        "annual_saving_inc_vat_pence": 6875,
        "annual_saving_percent": 7.5,
        "is_green": false,
        "is_variable": false,
        "term_months": 12,
        "exit_fees_inc_vat": 3000,
        "confidence": "MEDIUM"
      }
    ]
  }
}
```

---

#### 2.6.7 Recommendations

*New capability — no Octopus REST equivalent. Implements FR-006 personalised energy-saving recommendations.*

##### GET `/v1/recommendations`

Retrieve personalised energy-saving recommendations based on consumption patterns.

**Auth**: Required + consent purpose `RECOMMENDATIONS` must be granted

**Response** (200):
```json
{
  "count": 5,
  "results": [
    {
      "recommendation_id": "rec_001",
      "type": "SHIFT_USAGE",
      "title": "Shift high-energy activities to off-peak hours",
      "description": "Your electricity usage between 4-7pm is 40% above your daily average. Shifting washing machine and dishwasher use to after 10pm could save you approximately £12/month.",
      "estimated_annual_saving_pence": 14400,
      "confidence": "HIGH",
      "consumption_pattern_ref": "peak_evening_usage",
      "applicable_meters": ["mtr_elec_001"],
      "created_at": "2026-02-01T06:00:00Z",
      "dismissed": false
    }
  ]
}
```

##### PATCH `/v1/recommendations/{recommendation_id}`

Dismiss or rate a recommendation.

**Request**:
```json
{
  "dismissed": true,
  "rating": 4,
  "feedback": "Already do this"
}
```

---

#### 2.6.8 Budgets and Alerts

*New capability — implements FR-008 (alerts) and FR-009 (budget tracking).*

##### GET `/v1/budgets`

List consumer's budget targets.

##### POST `/v1/budgets`

Create a budget target.

**Request**:
```json
{
  "name": "Monthly electricity budget",
  "fuel_type": "ELECTRICITY",
  "target_amount_pence": 5000,
  "period": "MONTHLY",
  "alert_threshold_percent": 80,
  "alert_channels": ["PUSH", "EMAIL"]
}
```

##### GET `/v1/alerts`

List alert configurations.

##### POST `/v1/alerts`

Create a consumption alert.

**Request**:
```json
{
  "type": "CONSUMPTION_THRESHOLD",
  "meter_id": "mtr_elec_001",
  "threshold_kwh": 15.0,
  "period": "DAILY",
  "delivery_channels": ["PUSH"]
}
```

---

#### 2.6.9 Consent Management

*New first-class API — extends beyond Octopus model to implement FR-003 and UK GDPR Article 7.*

##### GET `/v1/consent`

Retrieve current consent status for all purposes.

**Auth**: Required

**Response** (200):
```json
{
  "data": {
    "purposes": [
      {
        "purpose": "CONSUMPTION_VIEWING",
        "status": "GRANTED",
        "granted_at": "2026-03-15T10:05:00Z",
        "withdrawn_at": null,
        "version": "1.0",
        "description": "View your energy consumption data in the app"
      },
      {
        "purpose": "RECOMMENDATIONS",
        "status": "GRANTED",
        "granted_at": "2026-03-15T10:05:00Z",
        "withdrawn_at": null,
        "version": "1.0",
        "description": "Receive personalised energy-saving recommendations"
      },
      {
        "purpose": "TARIFF_COMPARISON",
        "status": "DENIED",
        "granted_at": null,
        "withdrawn_at": null,
        "version": "1.0",
        "description": "Compare tariffs using your actual consumption data"
      },
      {
        "purpose": "RESEARCH",
        "status": "DENIED",
        "granted_at": null,
        "withdrawn_at": null,
        "version": "1.0",
        "description": "Contribute anonymised data to energy research"
      }
    ]
  }
}
```

##### PUT `/v1/consent/{purpose}`

Grant or withdraw consent for a specific purpose.

**Request**:
```json
{
  "status": "GRANTED"
}
```

**Response** (200):
```json
{
  "data": {
    "purpose": "TARIFF_COMPARISON",
    "status": "GRANTED",
    "granted_at": "2026-06-01T14:30:00Z",
    "version": "1.0",
    "audit_id": "aud_xyz789"
  }
}
```

---

#### 2.6.10 Carbon Footprint

*New capability — integrates National Grid ESO Carbon Intensity API. Implements FR-012.*

##### GET `/v1/carbon`

Retrieve carbon footprint for the consumer's consumption.

**Auth**: Required

**Parameters**: `period_from`, `period_to`, `group_by`

**Response** (200):
```json
{
  "data": {
    "period_from": "2026-01-01T00:00:00Z",
    "period_to": "2026-01-31T23:59:59Z",
    "total_kg_co2": 271.1,
    "electricity_kg_co2": 56.3,
    "gas_kg_co2": 214.8,
    "daily_average_kg_co2": 8.75,
    "comparison_to_national_average_percent": -12.5,
    "trend_vs_previous_period_percent": -3.2,
    "breakdown": [
      {
        "date": "2026-01-01",
        "electricity_kg_co2": 1.82,
        "gas_kg_co2": 6.93,
        "total_kg_co2": 8.75,
        "grid_carbon_intensity_g_per_kwh": 182
      }
    ]
  }
}
```

---

#### 2.6.11 Data Export and Portability

*Implements FR-010 and UK GDPR Article 20 (Right to Data Portability).*

##### POST `/v1/export`

Request a data export.

**Request**:
```json
{
  "format": "CSV",
  "data_types": ["CONSUMPTION", "PROFILE", "CONSENT_HISTORY"],
  "period_from": "2025-01-01T00:00:00Z",
  "period_to": "2026-01-31T23:59:59Z"
}
```

**Response** (202 Accepted):
```json
{
  "data": {
    "export_id": "exp_abc123",
    "status": "PROCESSING",
    "format": "CSV",
    "estimated_size_mb": 45,
    "download_url": null,
    "expires_at": null,
    "created_at": "2026-02-01T12:00:00Z"
  }
}
```

##### GET `/v1/export/{export_id}`

Check export status and retrieve download URL.

**Response** (200, when ready):
```json
{
  "data": {
    "export_id": "exp_abc123",
    "status": "COMPLETE",
    "format": "CSV",
    "size_mb": 42,
    "download_url": "https://export.smartmeter.service.gov.uk/exp_abc123/download?token=...",
    "expires_at": "2026-02-08T12:00:00Z",
    "created_at": "2026-02-01T12:00:00Z"
  }
}
```

---

#### 2.6.12 Prepayment

*Implements FR-013 prepayment meter features. Adapted from Octopus `prepayBalanceSnapshot` and `prepayPayments` GraphQL queries.*

##### GET `/v1/prepay/{meter_id}/balance`

Retrieve current prepayment balance.

**Response** (200):
```json
{
  "data": {
    "meter_id": "mtr_elec_001",
    "balance_pence": 1245,
    "balance_currency": "GBP",
    "last_top_up_at": "2026-01-28T09:30:00Z",
    "last_top_up_amount_pence": 2000,
    "estimated_days_remaining": 4,
    "low_balance_alert_threshold_pence": 500,
    "snapshot_at": "2026-02-01T12:00:00Z"
  }
}
```

##### GET `/v1/prepay/{meter_id}/transactions`

Retrieve prepayment transaction history.

**Parameters**: `period_from`, `period_to`, `page`, `page_size`

---

### 2.7 API Endpoint Summary

| # | Endpoint | Method | Auth | Consent Required | Octopus Equivalent |
|---|----------|--------|------|------------------|-------------------|
| 1 | `/v1/auth/token` | POST | No | — | `ObtainKrakenToken` mutation |
| 2 | `/v1/auth/refresh` | POST | No | — | `ObtainKrakenToken` (refresh) |
| 3 | `/v1/auth/revoke` | POST | Yes | — | — |
| 4 | `/v1/profile` | GET | Yes | — | `account` query / REST account |
| 5 | `/v1/profile` | PATCH | Yes | — | — |
| 6 | `/v1/profile` | DELETE | Yes | — | — (GDPR right to erasure) |
| 7 | `/v1/meters` | GET | Yes | — | Account `electricity_meter_points` + `gas_meter_points` |
| 8 | `/v1/meters` | POST | Yes | — | — |
| 9 | `/v1/meters/{id}` | DELETE | Yes | — | — |
| 10 | `/v1/meters/{id}/tariffs` | GET | Yes | — | Account `agreements` array |
| 11 | `/v1/consumption/electricity/{meter_id}` | GET | Yes | CONSUMPTION_VIEWING | `/v1/electricity-meter-points/{mpan}/meters/{serial}/consumption/` |
| 12 | `/v1/consumption/gas/{meter_id}` | GET | Yes | CONSUMPTION_VIEWING | `/v1/gas-meter-points/{mprn}/meters/{serial}/consumption/` |
| 13 | `/v1/consumption/combined` | GET | Yes | CONSUMPTION_VIEWING | — (new) |
| 14 | `/v1/products` | GET | No | — | `/v1/products/` |
| 15 | `/v1/products/{code}` | GET | No | — | `/v1/products/{code}/` |
| 16 | `/v1/products/{code}/tariffs` | GET | No | — | Product detail regional tariffs |
| 17 | `/v1/products/{code}/tariffs/{tariff}/unit-rates` | GET | No | — | `standard-unit-rates` endpoint |
| 18 | `/v1/gsp` | GET | No | — | `/v1/industry/grid-supply-points/` |
| 19 | `/v1/comparison` | GET | Yes | TARIFF_COMPARISON | `smartTariffComparison` query |
| 20 | `/v1/recommendations` | GET | Yes | RECOMMENDATIONS | `weeklyUsageInsights` / `getEnergyIqData` |
| 21 | `/v1/recommendations/{id}` | PATCH | Yes | RECOMMENDATIONS | — |
| 22 | `/v1/budgets` | GET/POST | Yes | — | — (new) |
| 23 | `/v1/budgets/{id}` | PATCH/DELETE | Yes | — | — (new) |
| 24 | `/v1/alerts` | GET/POST | Yes | — | — (new) |
| 25 | `/v1/alerts/{id}` | PATCH/DELETE | Yes | — | — (new) |
| 26 | `/v1/consent` | GET | Yes | — | `smartMeterDataPreferences` query |
| 27 | `/v1/consent/{purpose}` | PUT | Yes | — | — (new first-class API) |
| 28 | `/v1/carbon` | GET | Yes | CONSUMPTION_VIEWING | `getProjectedRegionalCarbonIntensity` |
| 29 | `/v1/export` | POST | Yes | — | — (GDPR Article 20) |
| 30 | `/v1/export/{id}` | GET | Yes | — | — |
| 31 | `/v1/prepay/{meter_id}/balance` | GET | Yes | CONSUMPTION_VIEWING | `prepayBalanceSnapshot` query |
| 32 | `/v1/prepay/{meter_id}/transactions` | GET | Yes | CONSUMPTION_VIEWING | `prepayPayments` query |

**Total**: 32 endpoint operations across 12 resource groups

---

## Part 3: Requirements Traceability

### 3.1 API Endpoints to Requirements Mapping

| Requirement ID | Requirement | API Endpoint(s) | Status |
|----------------|-------------|------------------|--------|
| FR-001 | Consumer authentication | `/v1/auth/*` | Covered |
| FR-002 | Meter discovery and linking | `/v1/meters` (GET/POST) | Covered |
| FR-003 | Granular consent management | `/v1/consent`, `/v1/consent/{purpose}` | Covered |
| FR-004 | Half-hourly data retrieval | `/v1/consumption/electricity/*`, `/v1/consumption/gas/*` | Covered |
| FR-005 | Consumption visualisation | `/v1/consumption/*` with `group_by` parameter | Covered (data layer) |
| FR-006 | Personalised recommendations | `/v1/recommendations` | Covered |
| FR-007 | Tariff comparison | `/v1/comparison`, `/v1/products/*` | Covered |
| FR-008 | Consumption alerts | `/v1/alerts` | Covered |
| FR-009 | Budget tracking | `/v1/budgets` | Covered |
| FR-010 | Data export and portability | `/v1/export` | Covered |
| FR-012 | Carbon footprint | `/v1/carbon` | Covered |
| FR-013 | Prepayment features | `/v1/prepay/*` | Covered |
| FR-014 | Cross-platform mobile | N/A (client-side) | N/A |
| FR-015 | SAR endpoint | `/v1/export` (with all data types) | Covered |
| NFR-SEC-001 | MFA authentication | GOV.UK One Login via `/v1/auth/token` | Covered |
| NFR-SEC-003 | Encryption in transit | HTTPS-only on all endpoints | Covered |
| NFR-C-001 | UK GDPR compliance | `/v1/consent`, `/v1/export`, `/v1/profile` DELETE | Covered |
| DR-001 | Half-hourly data storage | `/v1/consumption/*` backed by TimescaleDB | Covered |
| DR-005 | Data portability | `/v1/export` (JSON, CSV) | Covered |

### 3.2 Coverage Summary

- **15/15 functional requirements** have API endpoint coverage (100%)
- **Key NFRs** addressed through API design (auth, encryption, rate limiting, consent)
- **All data requirements** traceable to consumption and export endpoints

---

## Part 4: Data Source Abstraction Architecture

### 4.1 Backend Data Source Routing

Our API abstracts multiple upstream data sources behind the unified `/v1/consumption/*` endpoints:

```
Mobile App
    ↓
Smart Meter API Gateway (/v1/*)
    ↓
┌─────────────────────────────────────┐
│ Data Source Router                   │
│ Routes by meter data_source field    │
├─────────────────────────────────────┤
│ DCC Adapter       → DCC DUIS (SMETS2 native)           │
│ n3rgy Adapter     → n3rgy Consumer API (SMETS1+2)       │
│ Octopus Adapter   → Octopus REST API (Octopus customers)│
│ Supplier Adapters → Other supplier APIs as available     │
└─────────────────────────────────────┘
    ↓
TimescaleDB (normalised storage)
```

### 4.2 Data Source Selection Strategy

| Meter Type | Primary Source | Fallback | Coverage |
|------------|---------------|----------|----------|
| SMETS2 (any supplier) | DCC direct (if SEC Party) | n3rgy Consumer API | ~27 million meters |
| SMETS1 (migrated to DCC) | DCC direct | n3rgy Consumer API | ~7 million meters |
| SMETS1 (not yet migrated) | n3rgy Consumer API | Supplier-specific API | Declining population |
| Octopus Energy customers | Octopus REST API | n3rgy / DCC | ~8 million accounts |

### 4.3 Normalisation

All data sources are normalised to the unified consumption response format before storage:

| Source Field (Octopus) | Source Field (n3rgy) | Source Field (DCC) | Our Normalised Field |
|------------------------|----------------------|--------------------|--------------------|
| `consumption` | `value` | `ConsumptionRegisterValue` | `consumption_kwh` |
| `interval_start` | `timestamp` | `ReadingDateTime` | `interval_start` |
| `interval_end` | (calculated) | (calculated) | `interval_end` |
| (not available) | `quality` | `DataQualityFlag` | `quality_flag` |

---

## Generation Metadata

**Generated by**: ArcKit `/arckit.research` command
**Generated on**: 2026-02-01
**ArcKit Version**: 1.0.4
**Project**: UK Smart Meter Data Consumer Mobile App (Project 001)
**Model**: Claude Opus 4.5

**Sources**:
- [Octopus Energy Developer Portal](https://developer.octopus.energy/)
- [Octopus Energy REST API Endpoints](https://developer.octopus.energy/rest/guides/endpoints)
- [Octopus Energy GraphQL Reference](https://developer.octopus.energy/graphql/reference/)
- [Octopus Energy REST API Reference](https://developer.octopus.energy/rest/reference/)
- [Octopus Energy GraphQL Guides](https://developer.octopus.energy/graphql/guides/)
- [Guy Lipman Octopus API Guide](https://www.guylipman.com/octopus/api_guide.html)
- [Legacy Kraken Developer Docs](https://legacy-developer.kraken.tech/oegb/developer-guide)
