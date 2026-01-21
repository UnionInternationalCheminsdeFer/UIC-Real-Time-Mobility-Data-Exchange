---
layout: page
title: Code Lists
nav_order: 1
parent: Specification
hide_hero: true
has_children: true
permalink: /spec/code-lists/
---

# Code Lists



## Using URNs

| Code List                  | Name Space and domain | CodeList          | Description                                                                                                                                                        | example                       | base path for relative references   |
|----------------------------|----------------------|-------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------|------------------------------|-------------------------------------|
| stations                   | urn:uic              | stn               | UIC station codes (TAP-TSI retail station codes)                                                                                                                   | urn:uic:stn:8512345          | urn:uic:stn:                       |
| stations                   | urn:rne              | stn               | CRD location codes (TAP-TSI infrastructure codes) <br>*Infrastructure codes must not be used if a corresponding retail code exists.*                               | urn:rne:stn:8512345          | urn:rne:stn:                       |
| service brands             | urn:uic              | sbc               | UIC service brand code (TAP-TSI B.4.7009 / https://uic.org/passenger/passenger-services-group/article/service-brand-code-list)                                     | urn:uic:sbc:17               | urn:uic:sbc:                       |
| companies                  | urn:uic              | rics:ac           | company code (TAP-TSI [ERA Register](https://www.era.europa.eu/registers/ocr_en) / [UIC RICS](https://uic.org/support-activities/it/rics))                        | urn:uic:rics:1080            | urn:uic:rics:                      |
| companies                  | urn:iata             | company           | company code IATA <br><br> *Note: iata namespace is not yet officially approved at IANA, there might be changes*                                                  | urn:iata:company:LH          |                                     |
| Companie association alias | urn:uic              | CompanyAlias      | An alias for a list of companies                                                                                                                                   | urn:uic:companyAlias:xyz     |                                     |
| countries                  | urn:iso              | std:iso:3166      | ISO Country Codes                                                                                                                                                  | urn:iso:std:iso:3166:CH      | urn:iso:std:iso:3166:              |
| currencies                 | urn:iso              | std:iso:4217      | ISO Currency Codes                                                                                                                                                 | urn:iso:std:iso:4217:CFR     | urn:iso:std:iso:4217:              |
| TAF reason for delay codes | urn:x-taf            | urn:x-taf:25      | TAF-TSI reason for delay codes defined by ERA <br><br> (Codelist defined in UIC Leaflet 450-2)                                                                     |                              |                                     |
| UIC Passenger related      | urn:uic              | prc               | Codes to display the reason for delay or cancellation <br> See: Delay Reason Codes 8.6.2                                                                           | urn:uic:prc                  | urn:uic:prc                        |


## Delay Reasons

| reason for delay or cancellation                 | description                                                         |
|--------------------------------------------------|---------------------------------------------------------------------|
| ACCIDENT                                         | Due to an accident                                                  |
| ACCIDENT_PERSON_HIT_BY_TRAIN                     |                                                                     |
| ACCIDENT_PERSON_ILL_ON_VEHICLE                   |                                                                     |
| ACCIDENT_PERSON_UNDER_TRAIN                      |                                                                     |
| BORDER_ISSUE                                     | Due to an issue at border crossing                                  |
| BORDER_CONTROL                                   | Due to a border control (not in SIRI)                               |
| BORDER_CUSTOM_ISSUE                              | Due to an issue at custom control                                   |
| EQUIPMENT_BREAK_DOWN                             |                                                                     |
| EQUIPMENT_BROKEN_RAIL                            |                                                                     |
| EQUIPMENT_CLOSED_FOR_MAINTENANCE                 |                                                                     |
| EQUIPMENT_DEFECTIVE_FIRE_ALARM_EQUIPMENT         |                                                                     |
| EQUIPMENT_DEFECTIVE_TRAIN                        |                                                                     |
| EQUIPMENT_DEICEING_WORK                          |                                                                     |
| EQUIPMENT_ENGINE_FAILURE                         |                                                                     |
| EQUIPMENT_FAILURE                                |                                                                     |
| EQUIPMENT_FUEL_PROBLEM                           |                                                                     |
| EQUIPMENT_FUEL_SHORTAGE                          |                                                                     |
| EQUIPMENT_GANGWAY_PROBLEM                        |                                                                     |
| EQUIPMENT_LACK_OF_OPERATIONAL_STOCK              |                                                                     |
| EQUIPMENT_LIGHTING_FAILURE                       |                                                                     |
| EQUIPMENT_LUGAGE_CAROUSEL_PROBLEM                |                                                                     |
| EQUIPMENT_MAINTENANCE_WORK                       |                                                                     |
| EQUIPMENT_POWER_PROBLEM                          |                                                                     |
| EQUIPMENT_REPAIR_WORK                            |                                                                     |
| EQUIPMENT_SWING_BRIDGE_FAILURE                   |                                                                     |
| EQUIPMENT_TECHNICAL_PROBLEM                      |                                                                     |
| EQUIPMENT_TRACTION_FAILURE                       |                                                                     |
| EQUIPMENT_TRAIN_DOOR_INCIDENT                    |                                                                     |
| EQUIPMENT_TRAIN_WARNING_SYSTEM_PROBLEM           |                                                                     |
| EQUIPMENT_WHEEL_PROBLEM                          |                                                                     |
| EQUIPMENT_OVERRUN                                | Due to too many passengers on a train                               |
| FATALITY_COLLISSION                              |                                                                     |
| FATALITY_EMERGENCY_SERVICES                      |                                                                     |
| FATALITY_LINE_SIDE_FIRE                          |                                                                     |
| FATALITY_TRAIN_STRUCK_ANIMAL                     |                                                                     |
| FATALITY_TRAIN_STRUCK_OBJECT                     |                                                                     |
| INFRASTRUCTURE                                   |                                                                     |
| INFRASTRUCTURE_BRIDGE_STRIKE                     |                                                                     |
| INFRASTRUCTURE_CONSTRUCTION_WORK                 |                                                                     |
| INFRASTRUCTURE_DEFECTIVE_PLATFORM_EDGE_DOORS     |                                                                     |
| INFRASTRUCTURE_DEFECTIVE_ANNOUNCEMENT_SYSTEM     |                                                                     |
| INFRASTRUCTURE_DERAILMENT                        |                                                                     |
| INFRASTRUCTURE_EMERGENCY_ENGINEERING_WORK        |                                                                     |
| INFRASTRUCTURE_LANDSLIDE                         |                                                                     |
| INFRASTRUCTURE_LATE_FINISH_TO_ENGINEERING_WORK   |                                                                     |
| INFRASTRUCTURE_LEVEL_CROSSING_FAILURE            |                                                                     |
| INFRASTRUCTURE_NEXT_TRACK_SECTION_BLOCKED        | (not in SIRI)                                                       |
| INFRASTRUCTURE_NEXT_STATION_ENTRY_BLOCKED        | (not in SIRI)                                                       |
| INFRASTRUCTURE_OVERHEAD_OBSTRUCTION              |                                                                     |
| INFRASTRUCTURE_OVERHEAD_WIRE_FAILURE             |                                                                     |
| INFRASTRUCTURE_POOR_RAIL_CONDITIONS              |                                                                     |
| INFRASTRUCTURE_ROAD_CLOSED                       |                                                                     |
| INFRASTRUCTURE_ROAD_WORKS                        |                                                                     |
| INFRASTRUCTURE_ROADSIDE_ISSUE                    |                                                                     |
| INFRASTRUCTURE_ROUTE_DIVERSION                   |                                                                     |
| INFRASTRUCTURE_ROUTE_BLOCKAGE                    |                                                                     |
| INFRASTRUCTURE_SERVICE_INDICATOR_FAILURE         |                                                                     |
| INFRASTRUCTURE_SIGNAL_AND_SWITCH_FAILURE         |                                                                     |
| INFRASTRUCTURE_SIGNAL_FAILURE                    |                                                                     |
| INFRASTRUCTURE_SIGNAL_PASSED_AT_DANGER           |                                                                     |
| INFRASTRUCTURE_SIGNAL_PROBLEM                    |                                                                     |
| INFRASTRUCTURE_SLIPPERY_TRACK                    |                                                                     |
| INFRASTRUCTURE_TRACK_CIRCUIT_PROBLEM             |                                                                     |
| INFRASTRUCTURE_TRACK_WORKS                       | (not in SIRI)                                                       |
| INFRASTRUCTURE_TRACKSIDE_ISSUE                   | (not in SIRI)                                                       |
| INFRASTRUCTURE_TRACKSIDE_WORKS                   | (not in SIRI)                                                       |
| INFRASTRUCTURE_TRAFFIC_MANAGEMENT_SYSTEM_FAILURE |                                                                     |
| OBSTRUCTION                                      |                                                                     |
| OBSTRUCTION_ANIMAL_ON_THE_LINE                   |                                                                     |
| OBSTRUCTION_DEMONSTRATION                        |                                                                     |
| OBSTRUCTION_FALLEN_TREE                          |                                                                     |
| OBSTRUCTION_LEVEL_CROSSING_INCIDENT              |                                                                     |
| OBSTRUCTION_MARCH                                | Due to a public event „march“                                       |
| OBSTRUCTION_OBJECT_ON_THE_LINE                   |                                                                     |
| OBSTRUCTION_OVERCROWDED                          |                                                                     |
| OBSTRUCTION_PERSON_ON_THE_LINE                   |                                                                     |
| OBSTRUCTION_PROCESSION                           |                                                                     |
| OBSTRUCTION_PUBLIC_DISTURBANCE                   |                                                                     |
| OBSTRUCTION_ROAD_WORKS                           |                                                                     |
| OBSTRUCTION_SIGHT_SEERS                          |                                                                     |
| OBSTRUCTION_SPECIAL_EVENT                        |                                                                     |
| OBSTRUCTION_STATION_OVERRUN                      |                                                                     |
| OBSTRUCTION_VEGETATION                           | Vegetation obstructing the line                                     |
| OBSTRUCTION_VEHICLE_ON_THE_LINE                  | Vehicle blocking the line                                           |
| OPERATOR_CEASED_TRADING                          |                                                                     |
| OPERATOR_INSUFFICIENT_DEMAND                     | Due to insufficient demand (on demand services)                     |
| OPERATOR_SUSPENDED                               |                                                                     |
| PERSONELL_ISSUE                                  |                                                                     |
| PERSONELL_STAFF_ABSENCE                          |                                                                     |
| PERSONELL_STAFF_IN_WRONG_PLACE                   |                                                                     |
| PERSONELL_STAFF_SHORTAGE                         |                                                                     |
| PERSONELL_STAFF_SICKNESS                         |                                                                     |
| PERSONELL_STRIKE                                 |                                                                     |
| PREVIOUS_DISTURBANCES                            |                                                                     |
| PREVIOUS_TRAIN_DELAY                             | (not in SIRI)                                                       |
| SECURITY                                         |                                                                     |
| SECURITY_AIR_RAID                                |                                                                     |
| SECURITY_ATTACK                                  |                                                                     |
| SECURITY_BMB_ALERT                               |                                                                     |
| SECURITY_BOMB_EXPLOSION                          |                                                                     |
| SECURITY_CIVIL_EMERGENCY                         |                                                                     |
| SECURITY_EMERGENCY_SERVICE_CALL                  |                                                                     |
| SECURITY_EVACUATION                              |                                                                     |
| SECURITY_EXPLOSION                               |                                                                     |
| SECURITY_EXPLOTION_HAZARD                        |                                                                     |
| SECURITY_FIRE                                    |                                                                     |
| SECURITY_FIRE_BRIGADE_ORDER                      |                                                                     |
| SECURITY_FIRE_BRIGADE_SAFETY_CHECKS              |                                                                     |
| SECURITY_FIRE_SAFETY_CHECKS                      | (not in SIRI)                                                       |
| SECURITY_GUNFIRE_ON_ROADWAY                      |                                                                     |
| SECURITY_POLICE_RECQUEST                         |                                                                     |
| SECURITY_SABOTAGE                                |                                                                     |
| SECURITY_SAFETY_VIOLATION                        |                                                                     |
| SECURITY_SECURITY_ALERT                          |                                                                     |
| SECURITY_SUSPECT_VEHICLE                         |                                                                     |
| SECURITY_TELEPHONED_THREAT                       |                                                                     |
| SECURITY_TERRORIST_INCIDENT                      |                                                                     |
| SECURITY_UNATTENDED_BAG                          |                                                                     |
| SERVICE_FAILURE                                  |                                                                     |
| UNDEFINED                                        | The delay reason is known but does not fit to any code.             |
| UNKNOWN                                          | The delay reason is unknown.                                        |
| VANDALISM                                        |                                                                     |
| VANDALISM_ALTERCATION                            |                                                                     |
| VANDALISM_ASSAULT                                |                                                                     |
| VANDALISM_PASSENGER_ACTION                       |                                                                     |
| VANDALISM_RAILWAY_CRIME                          |                                                                     |
| VANDALISM_STAFF_ASSAULT                          |                                                                     |
| VANDALISM_THEFT                                  |                                                                     |
| WAITING_FOR_DELAYED_PASSENGERS                   | (not in SIRI)                                                       |
| WEATHER                                          |                                                                     |
| WEATHER_FALLEN_LEAVES                            |                                                                     |
| WEATHER_FALLEN_TREE                              |                                                                     |
| WEATHER_FLOODING                                 |                                                                     |
| WEATHER_FOG                                      |                                                                     |
| WEATHER_FROZEN                                   |                                                                     |
| WEATHER_HAIL                                     |                                                                     |
| WEATHER_HEAVY_RAIN                               |                                                                     |
| WEATHER_HEAVY_SNOWFALL                           |                                                                     |
| WEATHER_HIGH_TEMPERATURES                        |                                                                     |
| WEATHER_HIGH_TIDE                                |                                                                     |
| WEATHER_HIGH_WATER_LEVEL                         |                                                                     |
| WEATHER_ICE                                      |                                                                     |
| WEATHER_LOW_TIDE                                 |                                                                     |
| WEATHER_LOW_WATER_LEVEL                          |                                                                     |
| WEATHER_ROUGH_SEA                                |                                                                     |
| WEATHER_STRONG_WINDS                             |                                                                     |
| WEATHER_TIDAL_RESTRICTIONS                       |                                                                     |
| WEATHER_WATER_LOGGED                             |                                                                     |



