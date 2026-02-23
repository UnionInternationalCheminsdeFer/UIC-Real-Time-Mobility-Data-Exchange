---
layout: page
title: Getting Started
parent: Implementation and Testing
nav_order: 3
hide_hero: true
has_children: false
permalink: /spec/implementation-guide-getting-started/
---

# Getting Started

This section covers the essential steps to begin implementing RTMDE, including sign-up, connection details, authentication, and validation.

## RTMDE Sign Up

Every company intending to use RTMDE ACC must be first:

1. Allowed by UIC
2. Registered by RTMDE administrators (Hit Rail)

### Requesting Access

The company user must be requested by opening a case on the Testing 2004-25 Service Desk:

[https://hitrail.atlassian.net/servicedesk/customer/portal/10](https://hitrail.atlassian.net/servicedesk/customer/portal/10)

When you sign up for the Service Desk, please use the email address that you wish to receive answers and support ticket notifications. Normally this will be a group email.

A summary and a description are required for your request on the Service Desk. Please specify your company role(s): whether it will be a Data Provider, a Data Consumer, or both.

**Note:** User credentials are different for the Data Consumer and Data Provider APIs. If you want to sign up for both roles, you will receive two sets of credentials.

## Description of Environments

| Environment | Description |
|-------------|-------------|
| ACC | Acceptance - meant to support testing and implementation |
| PROD | Production |

## REST API

### Authentication

JWT (JSON Web Token) is used for Authentication implementing the OAuth 2.0 specification.

TLS version is 1.2.

### Endpoint URLs

RTMDE web services endpoints are provided separately by Hit Rail:

- Acceptance - Provider API
- Acceptance - Consumer API
- Production - Provider API
- Production - Consumer API

### Available Services per API

| Endpoint | Provider API | Consumer API |
|----------|:------------:|:------------:|
| `/login` (POST) | ✓ | ✓ |
| `3_0_4/serviceruns` (POST) | ✓ | |
| `3_0_4/serviceruns/retrievebysearch` (POST) | | ✓ |
| `3_0_4/subscriptions` (GET) | | ✓ |
| `3_0_4/subscriptions` (POST) | | ✓ |
| `3_0_4/subscriptions/{id}` (DELETE) | | ✓ |
| `3_0_4/subscriptions/{id}` (PATCH) | | ✓ |
| `1/logs/retrieve` (POST) | ✓ | ✓ |

### API Response Codes

The API call will return different responses based on the availability of the service and the quality of the request:

| Code | Description |
|------|-------------|
| 200 | POST – Data received successfully; GET – Returns requested data |
| 204 | OK (No Content - PATCH/DELETE request only) |
| 400 | Bad request |
| 401 | Unauthorized (e.g., user is not authenticated) |
| 403 | Forbidden (e.g., lack of credentials) |
| 404 | Not found |
| 406 | None of the provided content versions in the profile are supported |
| 409 | Conflict - event already received |
| 422 | Unprocessable entry - same idempotency key but different event |
| 500 | Internal error |
| 501 | Not implemented |
| 503 | Unavailable / Feedback from the validator |

## Login

To be able to use the API, the user needs to log in and request a token. This token can be used as a bearer token in subsequent API calls.

For login, the user needs a username and password provided by Hit Rail. These can be requested through the RTMDE Service Desk.

**Important:** The first password provided is temporary and must be changed within 24 hours. Otherwise, the account is blocked, and the access must be created again.

### Changing Password

To change the password, use the login endpoint with the following request:

**POST** `[endpoint]/login`

```json
{
  "username": "testing-user",
  "password": "actualPassword",
  "newPassword": "newPassword"
}
```

### Requesting a Token

To request a token, use the login REST resource:

**POST** `[endpoint]/login`

```json
{
  "username": "testing-user",
  "password": "MySecretPassword!"
}
```

If authorized, you will receive the tokens. From the JSON response, use the `IdToken` as a Bearer token in subsequent requests to the RTMDE REST interface endpoint.

**Example response:**

```json
{
  "AccessToken": "eyJraWQiOiI2MTV...",
  "ExpiresIn": 3600,
  "TokenType": "Bearer",
  "RefreshToken": "eyJjdHkiOiJKV1QiL...",
  "IdToken": "eyJraWjh..."
}
```

## Validation of Service Runs

Service runs sent to the RTMDE are validated against the specification according to the following rules:

- Checks if all required fields are present
- Checks the data type

If the service run does not pass the validation:
- The service run will **not** be updated by the RTMDE
- The service run will **not** be forwarded to the Data Consumer
- The Data Provider will receive feedback: a direct HTTP response with error code **503** and description of the error

**Example feedback:**

```json
{
  "type": "SCHEMA_VIOLATION",
  "time": "2024-03-08T12:59:22.860Z",
  "severity": "ERROR",
  "dataPayload": "eyJ0b3lvIjogInRhIiwgImRhdGFEZWxpdmVye...",
  "description": "1 validation error for ServiceRun\ndataDelivery.provider\n String should match pattern '^\\d{4}$' [type=string_pattern_mismatch, input_value='90211', input_type=str]\n For further information visit https://errors.pydantic.dev/2.4/v/string_pattern_mismatch",
  "correlationId": "f3cb0fa6-199a-4a6f-bb58-060de6b4ea80"
}
```
