---
layout: page
title: Requirements
nav_order: 1
parent: Specification
hide_hero: true
has_children: true
permalink: /spec/requirements/
---

#	Requirements
The aim of a real-time platform is one platform and one standard across Europe, so one-stop shopping is possible regarding real-time on-train services.  In this chapter, functional and non-functional requirements are listed. The requirements describe what the platform needs to do. How the platform could be built is not part of these requirements. The requirements need to provide freedom for experts and developers to technically specify and build the platform. In Requirements not in the scope for MVP there are requirements that are out of scope of the real-time platform, for a better understanding of what the platform will and will not do. 

## Functional requirements

- API to allow Data Providers to provide real-time information for passengers on trains.
- API to allow a Data Provider to send train replacement transport (e.g., busses).
- API to allow Data Consumers to receive push messages with real-time updates.
- API to allow Data Consumers to pull the status of individual trains or a set of trains.
- API for Data Consumers with filter functionality to allow the definition of filter conditions on the data to receive. A complete list of filters can be found in the API definition [see Bibliography]. For example, there must be filters on Country and Service brands and transport modes. More examples in paragraph Filter criteria:
- API must provide fields to exchange real-time information on trains. The message contains a complete state of a Service Run, so that Data Consumers do not need to combine information from multiple messages. A message includes:
  - Delays
  - Estimated times of arrival and departure
  - Time-tabled times of arrival and departure of a referenced timetable
  - Reason for Delay as a result of the reconciliation between RUs and IMs provided by RUs (PRR requirement)
  - Change of train composition (optional for Data Providers)
  - Train composition with track/platforms / coaches/platform sections
  - Replacement trains (PRR requirement)
  - Additional trains
  - Train replacing busses
  - Platform changes (PRR requirement)
  - Connections to other train services (optional for Data Providers)
  - Cancelled Trains (PRR requirement)
  - Cancelled Stops
  - Additional Stops
  - Geo-positions of a train (e.g., on passing CRD locations)
- The API needs to send the following information to Data Consumers so that Data Consumers can match the real-time information for passengers to their reference plan when their reference is different than the reference on the platform:
  - unique identification for a train provided by the platform
  - commercial train service number
  - operational train service numbers (optional, for future use)
  - line number
  - RUs of the train service
  - operational RUs of the train service if known
  - transport mode of the train service
  - vehicle IDs (European Vehicle Number) (optional)
  - planned arrival and departure times (as known in the real-time platform)
- The platform will only store one plan (integrated plan with all train Service Runs in Europe) that will be used for referencing and merging the real-time messages to keep the amount of data in the platform limited.
- Real-time platform service must pass on every real-time message from the Data Provider to the consumer, when it holds a change in relation to the last message sent for the same Service Run:
  - The first real-time message on a Service Run, regardless the time before departure or the information in the reference plan of the platform.
  - An update of previous received real-time information
- The platform will contain an integrator function that will combine partial information on trains into a real-time message with planned times and real-time on all stops. When part of the data is not yet available, then the platform will give an estimation for the missing information. (See for details Match and merge ServiceRun data from multiple RUs)
  - The integration of data from different providers on one service run will provide consolidated delay information showing the same delay on cooupled double tracktion parts.
  - The integration of data from different providers on one service run will provide consolidated delay information showing a reasonable delay across the route by correcting the delays to be ordered along the route with reasonable timings.
  - The integration of data from different providers on one service run will provide consolidated delay information in a transparent way so consumers can see the corrected delays separately.  
- An integrated timetable should be used by the integrator function of the platform to solve data issues, e.g., when the planned times of two real-time messages for a train service delivered by two different Data Providers cannot be connected.
- Possible to grant access to any consumers (not only RUs that provide input)
- Possible to process data on multimodal services when sent to the platform in the generic API standard of the platform.
- It should be visible to the Data Consumer whether the platform has consolidated data or simply passed them through.
- The platform must provide quality control measures. A minimal outline for monitoring of data quality:
  - Quality of the input. Per involved Data Provider:
    - Number of cases where a consolidation of delays was needed
    - Number of unmatched station codes
  - Quality of output. Per registered consumer:
    - Number of retries necessary
    - Number of published notifications vs. number of retrieved Service Runs
- The platform must provide monitoring of platform performance and load
  - Number of updates on Service Runs received (per provider)
  - Number of Service Runs published
  - Number of Service Run notifications published (per consumer)
  - Number of Service Runs retrieved (per consumer)

## Non-Functional requirements

-	Open Interfaces as API, API specification is open. API specification is published in REST OPEN-API 3.1
-	Easily extendable interface, so an increase in information items or adding of functionality can be done without a major redesign. The platform must be future-proof.
-	Extendable to hold all train services of all Data Providers in Europe. Resources should be scalable and flexible to accommodate for increase and decrease of the amount of data / number of integrations / number of requests / etc.
-	Date time values must be encoded according to RFC 3339, section 5.6.
-	Information exchange must support a state-of- the-art technology and architecture so that the system can handle the required number of messages and can be used for over a decade.
-	A real-time message should be processed in 10 seconds between receiving a message from a Data Provider to the sending of the notification.
-	The platform supports versioning by content negotiation. The client provides the version in the accept header. The objective is to support two versions, to be able to move from one version to a new upgraded version.

