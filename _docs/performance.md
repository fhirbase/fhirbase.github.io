---
layout: default
title:  "Performance"
id: performance
order: 3
---

# FHIRBase Performance

Blah-blah about performance reports.

## MacBook Air 1,7 GHz Intel Core i7, 8 GB 1600 MHz DDR3, SSD

| Operation                                                                                                           | Elapsed time (ms) |
|---------------------------------------------------------------------------------------------------------------------+------------------:|
| disk usage right after generation of seed data                                                                      |            21.885 |
| fhir.create called just one time                                                                                    |            25.243 |
| fhir.create called 1000 times in batch                                                                              |          1209.033 |
| fhir.read called just one time                                                                                      |             6.694 |
| fhir.read called 1000 times in batch                                                                                |           356.768 |
| Updating single patient with fhir.update()                                                                          |           218.599 |
| fhir.delete called one time                                                                                         |            13.135 |
| fhir.delete called 1000 times in batch                                                                              |          1182.448 |
| searching for non-existent name without index                                                                       |         97010.424 |
| building Patient.name index                                                                                         |        143934.523 |
| building Patient.gender index                                                                                       |        106689.734 |
| building Patient.address index                                                                                      |        249214.413 |
| building Patient.telecom index                                                                                      |        151158.313 |
| building Participant.name index                                                                                     |             5.616 |
| building Organization.name index                                                                                    |            64.074 |
| building Organization.address index                                                                                 |             6.180 |
| building Encounter.status index                                                                                     |        125611.808 |
| building Encounter.patient index                                                                                    |        249651.823 |
| building Encounter.participant index                                                                                |             8.256 |
| building Encounter.practitioner index                                                                               |             7.585 |
| building Patient.organization index                                                                                 |        105702.273 |
| running VACUUM ANALYZE on patient table                                                                             |         41941.426 |
| running VACUUM ANALYZE on encounter table                                                                           |         10796.692 |
| running VACUUM ANALYZE on organization table                                                                        |            89.839 |
| running VACUUM ANALYZE on practitioner table                                                                        |            17.554 |
| searching for patient with unique name                                                                              |            51.238 |
| searching for all Johns in database                                                                                 |           220.397 |
| searching Patient with name=John&gender=female&_count=100 (should have no matches at all)                           |           172.586 |
| searching Patient with name=John&gender=male&_count=100                                                             |            80.154 |
| searching Patient with name=John&gender=male&active=true&address=YALUMBA&_count=100                                 |            31.600 |
| searching Patient with name=John&gender=male&_count=100&_sort=name                                                  |           234.077 |
| searching Patient with name=John&gender=male&_count=100&_sort=active                                                |           209.552 |
| searching Encounter with patient:Patient.name=John&_count=100&status=finished&practitioner:Practitioner.name=Alex   |         34834.579 |
| searching Encounter with patient:Patient.name=John&_count=100&patient:Patient.organization:Organization.name=Mollis |           373.777 |
|---------------------------------------------------------------------------------------------------------------------|-------------------|
{: .table }
