---
layout: page
title: JSON Schema
parent: Implementation and Testing
nav_order: 6
hide_hero: true
has_children: false
permalink: /spec/implementation-guide-json-schema/
---

# JSON Schema and Example Messages

This section provides information about the JSON schema, example messages, and datetime handling within RTMDE.

## JSON Schema

The latest JSON schema (v3) including example messages is available for download from the UIC GitHub:

[https://github.com/UnionInternationalCheminsdeFer/UIC-Real-Time-Mobility-Data-Exchange](https://github.com/UnionInternationalCheminsdeFer/UIC-Real-Time-Mobility-Data-Exchange)

## Scenarios for Development and Testing

UIC and Hit Rail have defined a series of functional scenarios to support both the testing of RTMDE and the development from partners.

It is recommended that implementing partners gradually implement and test those scenarios.

Example JSON files and Postman collections for each scenario are available from Hit Rail.

| Scenario | Description |
|----------|-------------|
| Scenario 1 | National train without delay |
| Scenario 2 | National train with delay |
| Scenario 3 | National train with delay which is not in MERITS |
| Scenario 4 | National train with track/platform change |
| Scenario 5 | National train with cancelled stop |
| Scenario 6 | National train cancelled |
| Scenario 7 | International train with delay |
| Scenario 7b | International train with "time travel" |
| Scenario 7c | International train with added delay |
| Scenario 8 | International train with cancelled stop |
| Scenario 8b | International train with cancelled pass-through station |
| Scenario 11 | Detour |
| Scenario 12 | Extended service |
| Scenario 13 | Replacing service |
| Scenario 14 | Replacing an international service with multiple data providers |

For detailed scenario descriptions, see the [Test Scenarios](test-scenarios) page.

## Use of Datetime within RTMDE

### For Service Runs

Service runs sent by the Data Provider and delivered to the Data Consumers:

- Data Provider provides the offset in the submitted serviceRun update
- RTMDE preserves the offset sent by the Data Provider

### For the logs/retrieve Service

**Only datetime in UTC+0 is supported.**

The offset provided in the payload of the requests will be **ignored** in the following properties:

```json
{
  "from_ts": "2025-01-17 11:00:00.000000+02:00",
  "to_ts": "2025-01-17 19:00:00.000000+02:00"
}
```

For example, `2025-01-16 11:00:00.000000+02:00` will be processed as `2025-01-16 11:00:00.000000+00:00`.

In the response, all technical datetime fields that have no offset are displayed in **UTC+0 format**.
