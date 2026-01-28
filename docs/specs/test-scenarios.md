---
layout: page
title: Test Scenarios
parent: Implementation and Testing
nav_order: 1
parent: Implementation and Testing
hide_hero: true
has_children: false
permalink: /spec/implementation-testing/
---

# Test Scenarios

This section presents the test scenarios used for development and testing of RTMDE. A Postman collection with sample messages for each scenario is provided separately.

## Definitions

**National Train**: A train service that runs within a single country, with no border crossing, which is reported by a single data provider across its whole journey.

**International Train**: A train which travels across more than one country and is reported by more than one data provider.

**MERITS Integration**: RTMDE uses MERITS data as part of its data quality processes. Scenarios differentiate services which have been included in the MERITS database from those which have not. It is important that data providers correctly list their services in MERITS and send frequent updates with any changes in their timetable.

## Scenario Overview

| Scenario | Type | Description |
|----------|------|-------------|
| 1 | National | Train without delay |
| 2 | National | Train with delay |
| 3 | National | Train not in MERITS |
| 4 | National | Platform/track change |
| 5 | National | Cancelled stop |
| 6 | National | Cancelled train |
| 7 | International | Train with delay (same delay) |
| 7b | International | Train with "time travel" |
| 7c | International | Train with added delay |
| 8 | International | Cancelled stops |
| 8b | International | Cancelled pass-through station |
| 11 | National | Detour |
| 12 | National | Extended service |
| 13 | National | Replacing service |
| 14 | International | Replacing service with multiple data providers |

---

## National Train Scenarios

### Scenario 1: National Train without Delay

A national train listed in MERITS operates according to its scheduled timetable, without any delays.

**Data Provider Actions:**
- Send the service run with the same time on `plannedTime` and `estimatedTime` (meaning no delay) for each event
- Update the `status` field to `ON_SCHEDULE` for every event in the service run
- Set `significance` to `MASTER` for all events (national train)

**System Processing:**
- RTMDE calculates the `consolidatedEstimatedTime`
- RTMDE adds the `timeTabledTime` from MERITS

**Expected Result:**
The Data Consumer retrieves the service run and verifies that all time-related fields reflect the same values since the train is running on time.

---

### Scenario 2: National Train with Delay

A national train listed in MERITS follows its scheduled route but experiences a delay at an intermediate stop.

**Data Provider Actions:**
- Set `estimatedTime` different from `plannedTime` for delayed events
- Set `status` to `DELAYED` for events that are going to be delayed
- Set `status` to `ON_SCHEDULE` for all other events

**Expected Result:**
The Data Consumer retrieves the service run and finds the delay represented by the difference between `consolidatedEstimatedTime` and `timeTabledTime`.

---

### Scenario 3: National Train Not in MERITS

The data provider reports a train which is not listed in the MERITS timetable.

**Data Provider Actions:**
- Assign the `serviceName` field to a value that does not exist in MERITS
- Fill the corresponding `plannedTime`, `estimatedTime`, `status`, and `significance`

**Expected Result:**
- The `timeTabledTime` field is set as `null` since the service is not part of MERITS
- The `consolidatedEstimatedTime` is computed correctly by the platform

This scenario tests how RTMDE handles non-MERITS services.

---

### Scenario 4: National Train with Platform/Track Change

The data provider reports a service run update with new platform and track numbers on a specific event.

**Data Provider Actions:**
- Send the service run indicating the new value in the `platform` or `track` fields

**Expected Result:**
The Data Consumer retrieves the service run and observes the updated platform or track associated with the event.

---

### Scenario 5: National Train with Cancelled Stop

The data provider sends a service run that includes a cancelled stop.

**Data Provider Actions (Option A):**
- Set `cancelled` to `true` for the event to be cancelled
- Fill `cancellationType` with the corresponding reason

**Data Provider Actions (Option B):**
- Omit the event from the service run entirely

**Expected Result:**
The RTMDE platform processes and reflects the cancellation when handling the service run to the Data Consumer.

---

### Scenario 6: National Train Cancelled

The data provider sends a service run indicating that the entire service is cancelled.

**Data Provider Actions:**
- Modify only the final `cancelled` and `cancellationType` fields at the end of the service run
- There is no need to cancel each individual event separately

**Expected Result:**
- All events will be automatically cancelled by RTMDE after the service run is sent
- The Data Consumer retrieves the service run with all events appearing as cancelled, as well as the entire service

---

## International Train Scenarios

### Scenario 7: International Train with Delay

An international train service involving two data providers. Each provider is Master for stations within their respective territories and acts as Forwarded for the remaining stations. Both data providers report the same exact delay.

**Data Provider 1 (DP1) Actions:**
- Introduce a delay by setting different values for `plannedTime` and `estimatedTime`
- Set `status` to `DELAYED` for affected events

**Data Provider 2 (DP2) Actions:**
- Reflect the same delay across its events

**Expected Result:**
The Data Consumer sees that the delay is consistent across both providers.

---

### Scenario 7b: International Train with "Time Travel"

An international train involving two data providers where DP2 incorrectly reports significantly shorter delay than DP1 ("time travel").

**Data Provider Actions:**
- DP1 reports a delay
- DP2 sends a significantly shorter delay

**Expected Result:**
- This scenario is **not allowed** to happen
- RTMDE does not update the service run with the information from DP2
- The Data Consumer only sees the data reported by DP1

---

### Scenario 7c: International Train with Added Delay

DP1 introduces a delay and DP2 reports an additional delay across the events under its control.

**Data Provider Actions:**
- DP1 reports a delay by setting `status` to `DELAYED` and introducing a discrepancy between `plannedTime` and `estimatedTime`
- DP2 applies an additional delay to its respective events

**Expected Result:**
The distinct delays introduced by each provider are accurately represented and can be observed by the Data Consumer.

This demonstrates that delay updates can be successfully coordinated and aggregated across multiple data providers for a single service.

---

### Scenario 8: International Train with Cancelled Stops

Different stops corresponding to specific data providers are cancelled. Each data provider cancels stops within their own territory.

**Data Provider Actions:**
- DP1 sends a cancelled event belonging to their country (using either method from Scenario 5)
- DP2 cancels the event corresponding to their country

**Expected Result:**
- The cancelled events appear as cancelled in the service run
- Each data provider can only cancel events for which they hold the Master role

---

### Scenario 8b: International Train with Cancelled Pass-Through Station

Similar to Scenario 8, but the cancelled stops are of `PASS-THROUGH` type.

**Data Provider Actions:**
- DP1 sends the service run as scheduled
- DP2 does not include the respective pass-through station (which is master in its data)

**Expected Result:**
The event appears as cancelled, same as in Scenario 8. Omitting the event from the message serves as an alternative method of cancellation.

---

## Route Change Scenarios

### Scenario 11: Detour

A national train experiences a route deviation and will not follow its initially planned path to reach its destination.

**Data Provider Actions:**

**Step 1 (Critical):** Transmit the original planned route first.

**Step 2:** Send a second service run with the updated route:
- Delete the events that are not going to happen
- Provide new events, adding 2 events for each new stop:
  - One with `objectType` = `ARRIVAL`
  - One with `objectType` = `DEPARTURE`

**Expected Result:**
- The Data Consumer sees the new events
- The original events that will not occur appear as cancelled

---

### Scenario 12: Extended Service

The data provider modifies the train's initial departure station.

**Data Provider Actions:**

**Step 1 (Essential):** Send the originally planned route first.

**Step 2:** Submit a second service run showing the updated departure station:
- Add the new initial departure event
- Add an `ARRIVAL` event for the original departure station

**Expected Result:**
The Data Consumer sees the new departure station added to the service run.

---

### Scenario 13: Replacing Service

An existing train service is replaced with another train that follows a different route but still connects the same origin and destination.

**Data Provider Actions:**

**Step 1:** Send the service run for the original train.

**Step 2:** Send the new train service:
- Fill the `replacedServiceRuns` field with `serviceRunId` and `serviceName` of the original route
- Include all new events

**Step 3:** Cancel the original service:
- Use the same events list as the first service run
- Fill `replacingServices` field with `serviceRunId` and `serviceName` of the new route
- Set `cancelled` and `cancellationType` fields
- Individual events do not need to be cancelled separately

**Expected Result:**
The original service appears as cancelled with reference to the replacing service, and the new service references the replaced service.

---

### Scenario 14: Replacing International Service with Multiple Data Providers

An existing international train service is replaced with another train following a different route, involving two data providers.

**Data Provider Actions:**

**Step 1:** Both DP1 and DP2 send the service run for the original train.

**Step 2:** Both data providers send the new train service:
- Fill `replacedServiceRuns` field with `serviceRunId` and `serviceName` of the original route

**Step 3:** Cancel the original service:
- Fill `replacingServices` field with `serviceRunId` and `serviceName` of the new route
- Set `cancelled` and `cancellationType` fields
- Each data provider cancels its own respective events

**Expected Result:**
Coordinated replacement of an international service across multiple data providers.
