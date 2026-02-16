---
layout: page
title: Implementation Guide
parent: Implementation and Testing
nav_order: 2
hide_hero: true
has_children: false
permalink: /spec/implementation-guide/
---

# RTMDE Implementation Guide

This guide provides orientation on how to implement, connect, and use the Real-Time Mobility Data Exchange (RTMDE) service.

## Overview

RTMDE Real-Time Mobility Data Exchange is a UIC service providing a one-stop-shop for the gathering and distribution of real-time passenger train status information. It is based on UIC IRS 90918-11.

In order to implement RTMDE, either as Data Provider or Data Consumer, it is necessary to obtain UIC IRS 90918-11 directly from UIC. This document is complementary to the IRS.

## Environments

| Environment | Description | Availability |
|-------------|-------------|--------------|
| ACC | Acceptance - meant to support testing and implementation from connected partners | Available |
| PROD | Production - as close as possible to ACC environment | Available since December 2025 |

## Data Provider and Data Consumer Roles

A company using RTMDE can act in the role of Data Provider, Data Consumer, or both. There are separate API endpoints and user pools for each role.

**Data Provider** — Data Providers push service runs to RTMDE using REST API to deliver service run updates.

**Data Consumer** — Data Consumers retrieve updated service runs from RTMDE. The Data Consumer creates one or more subscriptions, each containing a filter specifying the services of interest (e.g., services running in France, or services run by Renfe).

Data Consumer implementation:
- Uses a webhook to receive notifications from RTMDE
- Uses REST API to retrieve updated service runs from RTMDE

## Documentation Structure

This implementation guide is organized into the following sections:

- **[Getting Started](implementation-guide-getting-started)** — Sign up process, environments, REST API basics, login, and validation
- **[Data Provider Guide](implementation-guide-data-provider)** — How to send service runs and retrieve logs as a Data Provider
- **[Data Consumer Guide](implementation-guide-data-consumer)** — How to subscribe, receive notifications, and retrieve service runs as a Data Consumer
- **[JSON Schema](implementation-guide-json-schema)** — JSON schema reference, example messages, and datetime handling
- **[Support](implementation-guide-support)** — Support channels, change requests, and contacts

## Glossary

Use glossary from UIC IRS 90918-11.
