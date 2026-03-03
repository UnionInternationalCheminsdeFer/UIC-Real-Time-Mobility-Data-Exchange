---
layout: page
title: Glossary
nav_order: 1
parent: Specification
hide_hero: true
has_children: true
permalink: /spec/glossary/
---

# Glossary


| Term                                 | Definition |
|---------------------------------------|------------|
| **Border Crossing**                   | Crossing the border between the areas of two Infrastructure managers. Border crossings between IMs are not related to borders between countries. |
| **Carrier**                           | Railway Undertaking (RU) concluding the transport contract with the passenger and is responsible for the transport towards the passenger. In this document, a Carrier is addressed as a Data Provider when the emphasis is on that fact that data is provided to the platform. (see also Actors – setting the scene) |
| **Consolidated Estimated Times**      | The estimated time by the platform for upcoming departures and arrivals is derived from applying consolidation business rules on the estimated times provided by the Data Provider. (See Figure 1 for the relation of the different time values) |
| **Data Consumer**                     | In this document, the Data Consumer is the party that collects real-time information to process this into travel information for the passenger. The words Data Consumers and the user are used interchangeably in this document. |
| **Data Provider**                     | A system that provides data (Service Runs) to the platform. In most cases, this will be a RU or a Carrier. |
| **Distributor**                       | Company combining transport contracts for a journey to a customer for passenger(s). The distributor might provide a travel companion and sales app to the passenger and/or customer. |
| **Estimated Times**                   | Estimations for upcoming departures and arrivals. There might be multiple estimates due to the involved parties (IMs, Carriers, Distributors, …) and the used algorithms. (See Figure 1 for the relation of the different time values) |
| **Infrastructure Manager (IM)**       | The party that is responsible for maintaining an operational rail infrastructure. The IM is subjected to TAP-TSI to provide real-time information on trains to Railway Undertakings (RUs). (see also Actors – setting the scene ) |
| **Master**                            | Responsible RU for stops of a service run. |
| **NAP**                               | National access points provide free available data. |
| **OAUTH 2**                           | Standard for authorization. https://oauth.net/2/ |
| **Actual Time**                       | Actual time of arrival or departure at a place. The Actual time from an IM perspective differs from the actual time from the passenger's perspective as defined in the Passenger Rights Regulation (PRR), which is the opening and closing of the access to the train service (e.g. opening of train doors). |
| **OMG**                               | Object Management Group (www.omg.org) |
| **OSDM**                              | Open Sales and Distribution Model (IRS 90918-10, https://osdm.io) (Ref see Bibliography ) OSDM includes Real-time Data in the trip data and provides mechanisms to push real-time data related to a booking. |
| **Planned Time**                      | The planned arrival and departure time in a Service Run provided by the Data Provider. (See Figure 1 for the relation of the different time values) |
| **Platform Admin**                    | Administrator with access and maintenance rights for the platform  (see also Actors – setting the scene ) |
| **Platform Data Manager**             | Person to validate the quality of the platform service and data accuracy. Send request to Data Provider when inconsistency need to be solved. |
| **Railway Undertaking (RU)**          | The term Railway Undertaking (RU) is used in TAP-TSI for undertakings managing train services. The RUs might have the role of Carrier, Distributor or Retailer. In the light of this document the role as Carrier is of importance. In this document the RU is in most cases addressed as Data Provider or Carrier. (see also Actors – setting the scene) |
| **Retailer**                          | Company selling transport offers from distributors to the customer.  For a real-time platform this is a consumer of real-time data. |
| **Service of the platform**           | A platform service is a task the platform can do like the service to send real-time messages |
| **TAP-TSI**                           | EU regulation on Telematics Application Passenger Traffic – Technical Specification for Interoperability. |
| **Timetabled Times**                  | Planned departure and arrival times according to a timetable. As there are multiple timetables the term planned time does not refer to a unique time. IMs usually reference a daily timetable for operations. Carriers and Distributors may refer to a defined timetable they compiled for their sales systems. (See Figure 1 for the relation of the different time values) |
| **TIS**                               | Train Information System provided by RNE (Rail Net Europe) implementing the TAP-TSI RU/IM data exchange. |
| **Train Service / Service Run**       | A train service or Service Run is a description of a train with amongst other origin, destination, stops and arrival and departure times. |
| **UML**                               | Unified Modelling Language. A specification defining a graphical language for visualizing, specifying, constructing, and documenting the artifacts of distributed object systems. OMG Unifier Modelling Language Superstructure v 2.1.2 |
| **UUID**                              | Universally Unique Identifier. Standard to create a unique id. The specification is published as ISO/IEC 9834-8:2005. |

