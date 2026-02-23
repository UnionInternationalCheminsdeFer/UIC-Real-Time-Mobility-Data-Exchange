---
layout: page
title: Data Provider Guide
parent: Implementation and Testing
nav_order: 4
hide_hero: true
has_children: false
permalink: /spec/implementation-guide-data-provider/
---

# Data Provider Guide

This section covers how to use RTMDE as a Data Provider, including sending service runs and retrieving logs.

## Overview

The Data Provider sends service runs to the RTMDE.

### Push-Only Workflow

Data Provider doesn't need to check whether a Service Run already exists in RTMDE before sending data. The platform will decide whether to create a new Service Run or update an existing one.

### Automatic Creation

If the Service Run in the payload doesn't exist in the RTMDE database, the platform will create it automatically. If it already exists, it will be updated.

### Timing

It's recommended to send the first Service Run data **72-24 hours before** the scheduled departure. This gives Data Consumers enough time to start tracking and ensures the service is visible early. However, the platform accepts messages at any time before departure.

### Complete State Requirement

According to the IRS 90918-11 specification, every update message sent to the platform must contain the **complete state** of the Service Run.

**Important:**
- Do **not** send partial updates (a payload containing only the specific stop that is delayed)
- The platform expects the full list of events (stops), identifying codes, and service references in every POST request
- If a previously existing stop is omitted in a new message, the platform may interpret this as a cancellation of that stop or an intentional removal from the schedule

## Sending a Service Run to the RTMDE

You can send service runs using the services REST resource:

**POST** `[endpoint]/3_0_4/serviceruns`

To send a service run, the Data Provider needs to send a payload compliant with the *Service* item from the definition file of the JSON schema.

### Request Flow

```
┌─────────────────┐         ┌─────────────────┐         ┌─────────────────┐
│  Data Provider  │         │      RTMDE      │         │  Data Consumer  │
└────────┬────────┘         └────────┬────────┘         └────────┬────────┘
         │                           │                           │
         │  POST /3_0_4/serviceruns  │                           │
         │ ────────────────────────► │                           │
         │                           │                           │
         │      200 OK / Error       │                           │
         │ ◄──────────────────────── │                           │
         │                           │                           │
         │                           │   Webhook notification    │
         │                           │ ────────────────────────► │
         │                           │                           │
```

### Example Payload Structure

The service run payload must include:

- `dataDelivery` — Delivery metadata (id, provider, creationTime)
- `serviceRef` — Service reference (serviceId, serviceNumber, plannedStartDate, etc.)
- `events` — List of all events (arrivals, departures, pass-throughs)
- `cancelled` — Service cancellation status (optional)
- `facilities` — Service facilities (optional)

## Retrieve a Log Collection for a Service Run

You can see all events related to the service run update you made by using the logs REST resource:

**POST** `[endpoint]/1/logs/retrieve`

**Note:** The role UIC can retrieve logs from any service run, while a normal user can only retrieve logs for service runs sent by their own user.

### Request Payload

```json
{
  "query_id": "27d8fc95-2572-40f4-a97e-9104eadc7e8f",
  "query_type": "PROVIDER_UPDATE",
  "company_id": "9021",
  "from_ts": "2024-03-08 12:46:00.000000",
  "to_ts": "2024-03-08 13:47:00.000000",
  "do_merge": true
}
```

### Field Descriptions

| Field | Description |
|-------|-------------|
| `query_id` | A user-generated ID for this request |
| `query_type` | `PROVIDER_UPDATE` |
| `from_ts` | The first minute (inclusive) to search in. Example: `2024-03-08 11:56:00.000` |
| `to_ts` | The last minute (exclusive) of the search period |
| `company_id` | 4-digit RICS code of the provider |
| `do_merge` | Optional. For `PROVIDER_UPDATE`. Merge all feedback for clarity purposes |
