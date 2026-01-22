---
layout: page
title: Use Cases
nav_order: 1
parent: Specification
hide_hero: true
has_children: true
permalink: /spec/use-cases/
---

# Use Cases

*Use Case Overview*

![Use Case Overview](../images/usecases1.jpg)



## Use Cases for a Data Consumers

### subscribe a webhook

In order to retrieve data o his webhook(s) a data consumer needs to subscribe the webhook. The substription includes the url and credentials to allow the platform to send real time data to the webhook and defines filter criteria to restrict the data to be sent.

The data comsumer can provide a filter in the subscription to limit the notifications received:

- carrierFilterType:
  -	**INCLUDE**: selects services where ANY of the specified carriers serve any part of the service.
  -	**EXCLUSIVE**: selects services where ANY of the specified carriers serve all parts of the service. In this case, services run by multiple carriers are not included in the selection.
  -	**EXCLUDE**: selects services where NONE of the specified companies are the carrier for any part of the service.
- countryFilterType:
  -	**INCLUDE**: select services where ANY of these countries is part of the route of the service. In this case, international services running at least partly in any of those countries are included in the selection.
  -	**EXCLUSIVE**: select services where the route of the service is run completely inside ANY of these countries. In this case, international services across the provided countries are not included in the selection.
  -	**EXCLUDE**: select services where NONE of the specified countries are any part of the service.


![Actors](../images/filtercriteria1.png)`

*Filter criteria on carrier and country*

### manage subscriptions

A data consumer can manage its subscriptions via the API:

- Add a subscription
-	Change a subscription
-	Delete a subscription
-	Get a list of all subscriptions

### retrieving service runs

The service runs include the data received from the carriers. Additionally the following data elements are added by the platform:

| data element  | description                                                                                             |        
| ----- | --------------------------------------------------------------------------------------------------------------- |
| dataDelivery.contributingProviders  |  list of data providers that contributed to the service run by sending real time data  |
| serviceRunRef.serviceRunId |  id of the service run on the platform                                                          |
| serviceRunRef.providerServiceRunIds|  identification data of the service run by the contributing providers                   |
| serviceRunRef.timeTableReferences  | reference to the time tbale used to provide the time tabled times of the events         |
| replacedServiceRuns  | service run ids are those of the service runs on the platform                                         |
| replacingServiceRuns | service run ids are those of the service runs on the platform                                         |
| event.timeTabledTime | event time of the planned time table included in the platform. usually the latest MERITS time table   |
| event.consolidatedEstimatedTime | estimated time ciorrected by the platform to eliminate inconsistencies between multiple data providers. |
| event.cancellationType  | indication whether an event was cancelled because it was in the reference time table and is not included in a data provider delivery. |
| event.dataMaster  | data provider that provided data for this event as responsible data provider.                            |
|   |   |

#### retrieve real time data using the web hook

If there is real time data avialable that meet the filtercriteria of the data consumers description the data consumer will receive a notification on his webhook registered viy the subscription. The notification includes the id of the service run that has an update.

The data consumer needs to retrieve the service run via the id provided in the notification.

#### retrieve real time data using the search for service runs

The API provides a search for service runs. In order to retrieve the correct service run one of the involved carriers and the country need to be specified.

Using the search might be more efficient compared to retrieving all service runs via a web hook in case the number of requests is limited compared to the amount of updates from all service runs.

## Use Cases for a Data Providers

### Providing Service Runs

The service run includes:

| data element  | description                                                                                             |        
| ----- | --------------------------------------------------------------------------------------------------------------- |
| dataDelivery  |  metadata on the deliveryof the service run                                                             |
| serviceRunRef |  identification data of the service run                                                                 |
| replacedServiceRuns  | reference data to indicate the service runs that replaced the service run in case of replacement           |
| replacingServiceRuns | reference data to indicate the service runs that were replaced by this service run in case of replacement  |
| cancelled  | indication that the entire service run is cancelled  |
| facilities  | option to indicate the facilities available on the service run  |
|   |   |


The service run must include the events of Departure and arrival. Optionally alos pass throughs can be provided.

**Events:**

| data element of the event  | description                                                                                |
| ----- | --------------------------------------------------------------------------------------------------------------- |
| objectType | 'DEPARTURE'  / 'ARRIVAL' / 'PASS_THROUGH'	                                                                |
| location 	 | Location id and optional the name (for stations but extensible to other types of locations).	              |
| plannedTime 	 | Planned time for the event according to the responsible Data Provider	                                |
| estimatedTime 	| Estimated time according to the responsible                                                           |
| actualTime 	 | Time when the event actually happened	(only after the event has happened)                               |
| status	 | Status of the event (CANCELLED, DELAYED,...)	                                                                |
| cancelled | indication that the stop ofthis 'DEPARTURE' or 'ARRIVAL' event is cancelled.                                |
| reasonForDelay	 |  Reasons for a delay or cancellation of the event	                                                  |
| significance     |  Indication whether the event is provided originally by the data provider or whether it has been forwarded from other sources to provide a complete service run data set.                                                                                  |
| stopId           | unique identifier of a stop. The id must be stable accoross all deliveries of the service run and becomes important in the case of multiple stops at the same location.                                                                                      |
| occupancy | 'DEPARTURE' only, indication of the occupancyof the the service on departure                                |
| congestion | 'DEPARTURE' only, indication of a congestion occuring                                                      |
| vehicleGroups  | Vehicle groups in the event. This includes vegicle groups and coaches and can also provide platform sections per coach or indicate cancelled or unusable coaches.  |
| platform  | platform where the event happens                                                                            |
| track  | track where the event happens                                                                                  |
| connections  |  list of connections that are kept of missed or at risk.                                                 |
| fromIM  | 'PASS_THROUGH' only: indication of a change of the Infrastructure Manager  |
| toIM    | 'PASS_THROUGH' only: indication of a change of the Infrastructure Manager   |
|   |   |


#### Initial data delivery independent from service run changes

A data provider must provide each service run a reasonable time before the start of the service run (72 to 24 hours before the start) in order to have a synchronized baseline with the time table data on the platform. 

#### Providing updates on service runs

In case of a change on  the service run the data provider must send the entire service run including the changes.


### Retrieving service runs

A data provider should also retrieve service run data on trains including other carriers in order to take incoming delays into account. This follows the use case for data consumers. The subscription filter can be defined to provide service runs including additional carriers only.



