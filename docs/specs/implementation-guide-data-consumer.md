---
layout: page
title: Data Consumer Guide
parent: Implementation and Testing
nav_order: 5
hide_hero: true
has_children: false
permalink: /spec/implementation-guide-data-consumer/
---

# Data Consumer Guide

This section covers how to use RTMDE as a Data Consumer, including creating subscriptions, receiving notifications, and retrieving service runs.

## Overview

The Data Consumer subscribes to receive data from RTMDE.

In the subscription request, there is a set of filters that allow the Data Consumer to specify the countries or carriers it wants to receive data from. A Data Consumer can combine filters or have more than one subscription.

### Workflow

1. Data Consumer receives real-time notifications from RTMDE (every time there is an event: departure, arrival, or pass-through)
2. The notification includes the UUID of the service run
3. Data Consumer uses the UUID to retrieve (GET) the service run from RTMDE

## Process to Receive Service Run Updates

The RTMDE uses a webhook (created after a subscription) to provide a stream of notifications to the Data Consumer.

Data Consumers using the full REST API need to set up a webhook URL and link it with the RTMDE.

### Creating a Subscription

To create a subscription (one-time process), use the subscription REST resource:

**POST** `[endpoint]/3_0_4/subscriptions`

```json
{
  "id": "identifierOfYourSubscriptionOnTestingTool",
  "company": "company code",
  "hook": "webhookURL",
  "user": "subscription_name",
  "accessToken": "token",
  "acceptedDelayTime": 60000,
  "filters": [
    {
      "name": "subscription-all",
      "carriers": [],
      "carrierFilterType": "INCLUDE",
      "countries": [],
      "countryFilterType": "INCLUDE",
      "countryBorderCrossings": [],
      "multiCarrierServiceRunsOnly": false,
      "countryCrossBorderOnly": false
    }
  ]
}
```

### Subscription Field Descriptions

| Field | Description |
|-------|-------------|
| `id` | Needs to be unique per subscription |
| `company` | Username |
| `hook` | The endpoint URL on your side to receive notifications |
| `user` | Required. Choose the name for the subscription |
| `accessToken` | Required. Strong password between 12 and 512 characters |
| `acceptedDelayTime` | Accepted delay time in milliseconds |
| `filters.name` | Required. Name for the filter |
| `filters.carriers` | Fill the list with carriers: `urn:uic:rics:XXXX` |
| `filters.carrierFilterType` | `INCLUDE`, `EXCLUSIVE`, or `EXCLUDE` |
| `filters.countries` | Fill the list with country abbreviations |
| `filters.countryFilterType` | `INCLUDE`, `EXCLUSIVE`, or `EXCLUDE` |
| `filters.countryBorderCrossings` | Country abbreviations for border crossings |
| `filters.multiCarrierServiceRunsOnly` | `true` or `false` |
| `filters.countryCrossBorderOnly` | `true` or `false` |

### Notification Format

RTMDE will send notifications regarding updated service runs using this format:

```json
{
  "data_delivery_id": "[uuid delivery id]",
  "data_delivery_provider": "[RICS Data Provider]",
  "event_type": "MODIFY",
  "last_notification_time": "2024-03-08 12:45:40.563509",
  "service_id": "[uuid service id]"
}
```

### Notification Retry Policy

The notification request will be repeated until it is confirmed:
- Repetition times will be doubled with each retry
- Repetition ends after 7 days
- RTMDE confirms acceptance as soon as a **200 HTTP response** has been received

### Authentication Methods

The username/accessToken is added in the header under the authorization key:

```
authorization: Basic QkVSVFJBTkQ6VE9LRU4=
```

This uses the Basic authentication method, and the couple `username:password` is encoded in Base64.

**Alternative methods** (can be set up on demand):
- OAuth Client Credentials
- API Key authentication

## Retrieving a Service Run

You can request the notified service run using the `serviceruns` REST resource and including the `serviceId` found in the notification:

**GET** `[endpoint]/3_0_4/serviceruns/{serviceId}`

The response is compliant with the *Service* item from the definition file of the JSON schema.

## Retrieve Service by Search

The Data Consumer can retrieve a specific service run for inspection (e.g., to check the latest update) by using several fields.

**POST** `[endpoint]/3_0_4/serviceruns/retrievebysearch`

To get the service run, the Data Consumer needs to send a payload compliant with the *ServiceSearchParams* item from the definition file of the JSON schema.

## Receiving Webhook Notifications Without an API

To support your Data Consumer development and test the RTMDE integration before having an API ready on your side, it is possible to temporarily use **Pipedream**: [https://pipedream.com](https://pipedream.com)

The basic feature (free of charge) offers you the possibility to build and run workflows using the HTTP/Webhook API. Once deployed, your workflow runs on requests made by the RTMDE to a generated endpoint (e.g., `https://eohfsdggsgd8xel.m.pipedream.net`).

This endpoint can be used as a webhook URL when creating the Data Consumer subscription in the RTMDE. After the subscription is made, any notification expected by the Data Consumer will be visible in the inspector section.

Once you have the notification, you can use the `service_id` element to retrieve the Service Run.

## Consulting the Logs

You can see what happened to an update or service run using the logs REST resource:

**POST** `[endpoint]/1/logs/retrieve`

### Request Payload

```json
{
  "query_id": "3f347975-eca1-4d54-bfbe-1b35659bfa0b",
  "query_type": "CONSUMER_SUBSCRIPTION",
  "company_id": "9021",
  "from_ts": "2024-02-20 09:00:00.000000",
  "to_ts": "2024-02-20 09:20:00.000000",
  "subscription_id": "",
  "subscription_action_list": [
    "CREATE", "GET", "UPDATE", "DELETE", "DAILY"
  ]
}
```

### Field Descriptions

| Field | Description |
|-------|-------------|
| `query_id` | A user-generated ID for this request |
| `query_type` | `CONSUMER_GET`, `CONSUMER_QUERY`, or `CONSUMER_SUBSCRIPTION` |
| `from_ts` | First minute (inclusive) to search in. Example: `2024-03-08 11:56:00.000` |
| `to_ts` | After last minute (exclusive) of search period |
| `company_id` | 4-digit RICS code of provider or consumer |
| `subscription_id` | Optional. To filter on a specific subscription ID |
| `subscription_action_list` | Optional. To filter on specific subscription actions: `CREATE`, `UPDATE`, `GET`, `DELETE`, `DAILY` |
