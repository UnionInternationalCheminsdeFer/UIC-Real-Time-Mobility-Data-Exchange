---
layout: page
title: Getting Started
nav_order: 1
parent: Specification
hide_hero: true
has_children: true
permalink: /spec/getting-started/
---

## Introduction

### Vision

This document is intended to support the vision of a more seamless passenger experience. A central platform according to this specification is: 
 -	providing high-quality real-time data relevant for passengers
 -	on all services in one place
 -	including multi-RU services
 -	including complex services (merged, split trains)
 -	to be provided to all parties serving the passenger
 -	for an entire journey
   
This document contributes to a solution that will provide high-quality quality integrated real-time passenger information for all European trains. The described platform provides one-stop-shopping for all interested consumers using an open API standard for communication. A Data Consumer can collect all real-time data from one platform. The platform needs to be adaptable to future requirements. And the aim is to have the platform in successful operation, providing valuable passenger information to Data Consumers for more than a decade.


### Current Situation of Real-time Data Exchange

IMs change a train or detect change in a train run. IMs provide this logistic data to RUs which turn this information in passenger information. Consumer of this data that already provide a European wide service collects this information from multiple sources, mostly directly from the Carrier, but also from platform services which already combine information on a few Carriers. 

There is legislation to improve the availability of real-time information. There is TAP-TSI data, but this is logistic information and not passenger information. And more recent channels are the National Access Points (NAP) every country needs to have. National Access Points are free in the format they use and an integrator functionality is not a required part of their platform. NAP’s can also be only the central location to direct consumers directly or indirectly to the actual sources of data.

To sum up: The current situation is that information must be collected from multiple sources. The consumer of data must unify the data and piece together full train services before they can present it to the passenger. 

### Methodology

This document follows the UML specification to define the solution. In this document, you will find:
- Actors
- Sequence diagrams
- Use Case diagrams
- Deployment diagrams

UML data models have been replaced by the graphical data description used for JSON data structures.

### Basic principles

The following basic principles are behind the solution in this document:
 -	The provided real-time data has aways priority over the reference timetable.
 -	Data changes or additions by the platform must be made visible to the Data Consumers.
