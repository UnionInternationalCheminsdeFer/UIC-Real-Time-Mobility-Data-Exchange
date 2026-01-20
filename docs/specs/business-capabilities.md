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



