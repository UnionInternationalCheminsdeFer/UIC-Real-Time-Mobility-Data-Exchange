---
layout: page
title: Business Capabilities
nav_order: 1
parent: Specification
hide_hero: true
has_children: true
permalink: /spec/business-capabilities/
---

## Business Objects

The real-time data platform deals with the following business objects only: 

-	The Service Run, the entity of information on a train. The data components that are part of the Service Run can be found in the API description. (See Service Run)
-	The reference timetable of the platform. The reference timetable will be used by the platform to send out consistent planned times at stops. The timetable is used to merge real-time data from different RUs on the same Service Run.

The scope is all Service Runs in Europe operated by train or train-replacing transport.

## Business Capabilities

The basic objective of the real-time exchange here is to enable the following business capabilities:

 -	Allow a Carrier responsible for a train service to provide real-time information on a Service Run so that it will be part of integrated passenger information. 
  -	Provide a solution for combining data for multiple Carrier services and cover all rail-related specifics
    -	Combine real-time data from multiple Data Providers for the same service in a transparent way
    -	Delay information, platform information, connections
    -	Manage complex split and / or merged Service Runs
 -	Provide a specified open data format for real-time exchange for travel information purposes, so that:
    -	Data Providers and Data Consumers do not make unnecessary costs on many convertors or on fee to standardization organisations
    -	It enables the community to be compliant with competition law 
 -	Provide integrated and consolidated output data in the specified format
    -	Consistent delay information on an entire Service Run
    -	One output for a service covering data provided by multiple providers
    -	Transparency on the consolidation done by the platform
 -	Provide a centralized access point fit for collecting all real-time of all RUs in Europe.
 -	Provide a lean platform service so that the platform is attractive as source for consumers preparing passenger information.
    -	only exchange valuable data
    -	provide filtered data
    -	provide services focused on the use case
 -	Provide an extensible specification open for future new requirements, to adapt to new or changing requirements when the API and platform are in production.


### Consolidations by the platform

#### Comparison to a time table

The plattform uses the latest MERITS time table to identify and compare service runs delivered by data providers.

- The used MERITS time table is references in the service run as refereced time table
- The planned time from the MERITS time table is added t the service run events in timeTableReference.
- Events on the MERITS time table that are not included in the data delivery are marked as cancelled and 'MISSING_FROM_CARRIER'.
- Events in the data delivery of a data provider that are not included on the MERITS time table are marked as 'MISSING_FROM_TIMETABLE'.
- Events on the MERITS time table that are marked in the data delivery as cancelled are marked as cancelled and 'CANCELLED_BY_CARRIER'.

#### Calculation of the consolidated time estimates

The consolidated delay estimates are made consistent by moving the impossible real-time on stops so far in time that the following rules apply:

-	Delay times must be consecutive along the route. (No time travel back in time)
-	Delay times must not indicate a decrease of travel time between two stops of more than 10% (value to be evaluated and configurable) compared to the planned travel-time between two stations.
-	Delay times on departure at one stop must not be later than the delay estimate at the arrival on the same stop.
-	The stop at station can be reduced to configurable minimal number of minutes. It must be allowed to set the value to no adaption of the stop time. (e.g. any stop longer than 10 minutes is reduced to 10 minutes)

Consolidated estimated times are never reduced compared tio the estimation of the data providers.  


#### Transfering estimated times in case of through coaches and double traction trains

In case of through coaches and double traction trains the estimated times on the coppled sections of the route are identical for all involved train parts.

The platform evaluates these cases and provides a consistent view on these times for all involved service runs.

In order to get a reliable estimation the data provides need to include the vehicle groups into their data deliveries.











