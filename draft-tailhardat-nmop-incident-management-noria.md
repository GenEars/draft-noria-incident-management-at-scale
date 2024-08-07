---
title: "Knowledge Graphs for Enhanced Cross-Operator Incident Management and Network Design"
abbrev: "Knowledge Graphs & Incident Management"
category: info

docname: draft-tailhardat-nmop-incident-management-noria-latest
submissiontype: IETF
number: 00
date: 2024-06-27
consensus: true
v: 3
area: "Operations and Management"
workgroup: "Network Management Operations"
keyword:
 - knowledge graphs
 - incident management
 - anomaly detection

author:
 -
    fullname: Lionel Tailhardat
    organization: Orange
    email: "lionel.tailhardat@orange.com"
 -
    fullname: Raphaël Troncy
    organization: EURECOM
    email: raphael.troncy@eurecom.fr
 -
    fullname: Yoan Chabot
    organization: Orange
    email: yoan.chabot@orange.com

normative:

informative:

--- abstract

TBC

--- middle

# Status of this document

This document is experimental.  The main goal of this document is to
propose an iterative lifecycle process to network anomaly detection
by proposing a data model for metadata to be addressed at different
lifecycle stages.

The experiment consists of verifying whether the approach is usable
in real use case scenarios to support proper refinement and
adjustments of network anomaly detection algorithms.  The experiment
can be deemed successful if validated at least with an open-source
implementation sucessfully applied in real production networks.

# Introduction

TODO Introduction

* Learning and sharing failure mode & remediation actions on complex systems towards improved worldwide system design and cross operator operational efficiency
* Leveraging reasoning capabilities and data sharing capabilities intrinsic to SemWeb KGs
* Need to consider both the infras-service-ecosystem while preserving privacy
* Need to align / keep compatible with in-production net configuration (e.g. Yang-based) & monitoring tools (e.g. CMDB and net discovery related tools) while opening to externaly maintained knowledge bases (e.g. CTI using UCO,

* providing a knowledge representation that is both human & computer friendly to overcome current limitations network design practices (e.g. many white papers from vendors) and incident response/management (e.g. proprietary knowledge bases on failure modes and risks, cross-organisations coordination)
* connecting to in-production configuration management databases (e.g. YANG-based deployment systems)
* providing both the technical perspective of networks and their ecosystem (e.g. asset location, organization, operations, etc.) to enable comprehensive network behavior analysis
* enabling privacy-preserving knowledge sharing of network designs and behavior models through entities's classes and types instead of sharing the knowledge graph itself.

As ...


The envisionned use cases ...


Since ..., this document defines ...


# Conventions and Definitions

{::boilerplate bcp14-tagged}


This document makes use of the terms defined in
[I-D.ietf-nmop-terminology].

*  State

*  Problem

*  Event

*  Alarm

*  Symptom

# Proposal

Include TT descriptors
Track and tag the remediation actions through KG
Capture the incident context (SL, model-based)
Share the incident context, including the lifecycle.

[I.D.draft-netana-nmop-network-anomaly-lifecycle]
Network Anomaly Detection
Network Anomaly Validation
Network Anomaly Refinement

## NetOps perspective

## SecOps perspective

## NORIA-O / YANG KG mapping

## Stream vs KG



### The multi


### Hybrid KG/TSDB


```
               ┌──────────┐   ┌────────────────┐   ┌──────────┐   ┌───────────────┐   ┌────────┐
┌──────────┐   │          │   │                │   │          │   │               │   │┌──────┐│
│  Events  │──►│  E.S.B.  ├──►│ Stream mapping ├──►│  S.S.B.  ├──►│ Stream loader ├──►││ K.G. ││
└──────────┘   │          │   │                │   │          │   │               │   │└──────┘│
               └──────────┘   └────────────────┘   └────┬─────┘   └───────────────┘   └────────┘
                                                        │
                                    ┌───────────────────┴──────────────────────┐
                                    │(event/LOG_login_03)=>(object/RES/router1)│
                                    └─┌──────────────────────────────────────────┐
                                      │(event/LOG_login_03)=>(object/RES/router1)│
                                      └─┌──────────────────────────────────────────┐
                                        │(event/LOG_login_03)=>(object/RES/router1)│
                                        └──────────────────────────────────────────┘
```

```
                         <object/RES_router3>
<object/RES_router2>          │
               │              │            ┌────────┐
             <object/RES_router1>─rdf:type─┤Resource│
                       │                   └────────┘
                       │
          logOriginatingManagedObject
                       │
             <event/LOG_login_01>             ┌───────────┐
               <event/LOG_login_02>──rdf:type─┤EventRecord│
                 <event/LOG_login_03>         └───────────┘
```

```
                              ┌────────────────┐
                              │    Complex     │
                              │     Event      │
                              │   Processing   │
                              └───────┬┬───────┘
               ┌──────────┐   ┌───────┴┴───────┐   ┌──────────┐   ┌───────────────┐   ┌────────┐
┌──────────┐   │          │   │                │   │          │   │               │   │┌──────┐│
│  Events  │──►│  E.S.B.  ├──►│ Stream mapping ├──►│  S.S.B.  ├──►│ Stream loader ├──►││ K.G. ││
└──────────┘   │          │   │                │   │          │   │               │   │└──────┘│
               └────────┬─┘   └────────────────┘   └────┬─────┘   └───────────────┘   └────────┘
                        │                               │
                        │           ┌───────────────────┴──────────────────────┐
                        │           │(event/AIS_login_01)=>(object/RES/router1)│
                        │           └──────────────────────────────────────────┘
                        │
                        │                                         ┌───────────────┐   ┌────────┐
                        │                                         │               │   │┌──────┐│
                        └────────────────────────────────────────►│ Stream loader ├──►││ TSDB ││
                                                                  │               │   │└──────┘│
                                                                  └───────────────┘   └────────┘
```

```
                             <object/RES_router3>
    <object/RES_router2>          │
                   │              │            ┌────────┐
                 <object/RES_router1>─rdf:type─┤Resource│
                           │                   └────────┘
                           │
              logOriginatingManagedObject
                           │                    ┌───────────┐
                 <event/AIS_login_01>──rdf:type─┤EventRecord│
                  │              │ │            └───────────┘
              duration           │ │
                  │              │ │
"P0Y0M0DT0H3M30S"^^xsd:duration  │ └─dcterms:type─<Notification/EventType/inferredAlert>
                                 │                                │
                            loggingTime                        rdf:type
                                 │                          ┌─────┴──────┐
               "2024-02-07T16:22:42Z"^^xsd:dateTime         │skos:Concept│
                                                            └────────────┘
```

```
                                <object/RES_router3>
       <object/RES_router2>          │
                      │              │            ┌────────┐
                    <object/RES_router1>─rdf:type─┤Resource│
                              │                   └────────┘
                              │
                 logOriginatingManagedObject
                              │                    ┌───────────┐
┌──────────────────►<event/AIS_login_01>──rdf:type─┤EventRecord│
│                    │              │ │            └───────────┘
│                duration           │ │
│                    │              │ │
│  "P0Y0M0DT0H3M30S"^^xsd:duration  │ └─dcterms:type─<Notification/EventType/inferredAlert>
│                                   │                                │
│                              loggingTime                        rdf:type
│                                   │                          ┌─────┴──────┐
│                 "2024-02-07T16:22:42Z"^^xsd:dateTime         │skos:Concept│
│                                                              └────────────┘
│  KG knowledge representation
│  ========================================================================================
│  Time series database (TSDB) data representation
│
│
│  Timestamp             Origin                Event
│  2024-02-07T16:22:42Z  <object/RES_router1>  Login Attempt
│  2024-02-07T16:23:13Z  <object/RES_router1>  Login Attempt
│  2024-02-07T16:26:12Z  <object/RES_router1>  Login Attempt
│                                 ▲
└──shared─identifier──────────────┘
```


# Implementation status

This section provides pointers to existing open source implementations of this draft.

Note to the RFC-editor: Please remove this before publishing.

# Security Considerations

TODO Security

Multi hosting


```
Data domain &   ───On-premise────────────────────────────   ┌─┐  Scope-based querying
access policy   ┌───────┐                                   │ │
                │┌─────┐│  ┌──────┐           ┌─────────┐   │ │           ┌───────────┐
  Domain A ────►││ KG  ││◄─┤KGDBMS├───────────┤SPARQL EP├──►│ ├─Network &─┤  NetOps   │
   -   UG2      │└─────┘│  └──────┘           └─────────┘   │ ├─Usage─────┤Application│
                └───────┘                                   │ │           └───────────┘
                ┌───────┐                                   │ │           ┌───────────┐
                │┌─────┐│  ┌──────┐           ┌─────────┐   │ ├─Network &─┤  SecOps   │
  Domain B ────►││ KG  ││◄─┤KGDBMS├───────────┤SPARQL EP├──►│ ├─Security──┤Application│
  UG1   -       │└─────┘│  └──────┘           └─────────┘   │F│           └───────────┘
                └─────┬─┘                                   │E│
                      └─────────────────────────────────────│D│─────────────┐
                ───On-premise / public-cloud─────────────   │E│             │
                ┌───────┐                                   │R│             ▼  Usage
                │┌─────┐│  ┌──────┐ ┌───┐     ┌─────────┐   │A│           ┌────scope──┐
  Domain C ────►││ RDB ││◄─┤RDBMS ├─┤VKG├─────┤SPARQL EP├──►│T│           │*          │
  UG1 & UG2     │└─────┘│  └──────┘ └───┘     └─────────┘   │E│   Network │   *  *    │
                └───────┘                                   │D│   scope───│────────┐  │
                ┌───────┐                                   │ │       │   │ *  *   │  │
                │┌─────┐│  ┌──────┐ ┌───┐     ┌─────────┐   │Q│       │  *└───────────┘
  Domain D ────►││NoSQL││◄─┤RDBMS ├─┤VKG├─────┤SPARQL EP├──►│U│       │  ┌───────────┐
  UG1   -       │└─────┘│  └──────┘ └───┘     └─────────┘   │E│       │* │ *  *    │ │
                └───────┘                                   │R│       └──│─────────┘ │
                ┌───────┐                                   │I│        ▲ │     *     │
                │┌─────┐│  ┌──────┐ ┌───────┐ ┌─────────┐   │E│        │ │ *       * │
  Domain E ────►││ LPG ││◄─┤GDBMS ├─│QL tlt.├─┤SPARQL EP│──►│S│        │ └──Security─┘
   -   UG2      │└─────┘│  └──────┘ └───────┘ └─────────┘   │ │        │    scope ▲
                └───┬───┘                                   │ │        │          │
                    └───────────────────────────────────────│ │────────┼──────────┘
                                                            │ │        │
                ───Public-cloud──────────────────────────   │ │        │
                ┌───────┐                                   │ │        │
                │┌─────┐│  ┌──────┐           ┌─────────┐   │ │        │
  Domain F ────►││ KG  ││◄─┤KGDBMS├───────────┤SPARQL EP├──►│ │        │
  UG1 & UG2     │└─────┘│  └──────┘           └─────────┘   │ │        │
                └───┬───┘                                   └─┘        │
                    └──────────────────────────────────────────────────┘
```


# IANA Considerations

This document has no IANA actions.

# Open Issues

TBC ...


# References

## Normative references

[SPARQL11-QL]
  Steve Harris, and Andy Seaborne,
  "SPARQL 1.1 Query Language",
  W3C Recommendation,
  21 March 2013,
  <https://www.w3.org/TR/sparql11-query/>.

[SPARQL11-FQ]
  Eric Prud'hommeaux, and Carlos Buil-Aranda,
  "SPARQL 1.1 Federated Query",
  W3C Recommendation,
  21 March 2013,
  <https://www.w3.org/TR/sparql11-federated-query/>.

## Informative references

[I.D.draft-marcas-nmop-knowledge-graph-yang]
  I.D. Martinez-Casanueva, and L. Cabanillas,
  "Knowledge Graphs for YANG-based Network Management",
  Work in Progress,
  Internet-Draft,
  draft-marcas-nmop-knowledge-graph-yang-03,
  5 July 2024,
  <https://datatracker.ietf.org/doc/draft-marcas-nmop-knowledge-graph-yang/>.

[I.D.draft-netana-nmop-network-anomaly-lifecycle]
  A. Roberto, T. Graf, W. Du, and A. Huang Feng,
  "Experiment: Network Anomaly Lifecycle",
  Work in Progress,
  Internet-Draft,
  draft-netana-nmop-network-anomaly-lifecycle-03,
  8 July 2024,
  <https://datatracker.ietf.org/doc/draft-netana-nmop-network-anomaly-lifecycle/>.

[I.D.draft-netana-nmop-network-anomaly-semantics]
  T. Graf, W. Du, A. Huang Feng, V. Riccobene, and A. Roberto,
  "Semantic Metadata Annotation for Network Anomaly Detection",
  Work in Progress,
  Internet-Draft,
  draft-netana-nmop-network-anomaly-semantics-02,
  7 July 2024,
  <https://datatracker.ietf.org/doc/draft-netana-nmop-network-anomaly-semantics/>.

[NORIA-O-2024]
  Lionel TAILHARDAT, Raphaël TRONCY, and Yoan CHABOT.
  “NORIA-O: An Ontology for Anomaly Detection and Incident Management in ICT Systems”.
  In 21st European Semantic Web Conference (ESWC), Resources track, May 26-30, 2024, Hersonissos, Greece.
  2024.
  https://doi.org/10.1007/978-3-031-60635-9_2

[StatisticalLearningKG-2023]
  Lionel TAILHARDAT, Raphaël TRONCY, and Yoan CHABOT.
  “Leveraging Knowledge Graphs For Classifying Incident Situations in ICT Systems”.
  In The 18th International Conference on Availability, Reliability and Security (ARES 2023), August 29-September 1, 2023, Benevento, Italy.
  ACM, New York, NY, USA, 9 pages.
  2023.
  https://doi.org/10.1145/3600160.3604991

[bramsteenwinckelFLAGSMethodologyAdaptive2021]
  "FLAGS: A Methodology for Adaptive Anomaly Detection and Root Cause Analysis on Sensor Data Streams by Fusing Expert Knowledge with Machine Learning",
    author = {{Bram Steenwinckel} and {Dieter De Paepe} and {Sander Vanden Hautte} and {Pieter Heyvaert} and {Mohamed Bentefrit} and {Pieter Moens} and {Anastasia Dimou} and {Bruno Van Den Bossche} and {Filip De Turck} and {Sofie Van Hoecke} and {Femke Ongenae}},
    year = 2021,
    journal = {Future Generation Computer Systems},
    doi = {10.1016/j.future.2020.10.015}

[bramsteenwinckelAdaptiveAnomalyDetection2018]
    author = {{Bram Steenwinckel} and {Pieter Heyvaert} and {Dieter De Paepe} and {Olivier Janssens} and {Sander Vanden Hautte} and {Anastasia Dimou} and {Filip De Turck} and {Sofie Van Hoecke} and {Femke Ongenae}},
    "Towards Adaptive Anomaly Detection and Root Cause Analysis by Automated Extraction of Knowledge from Risk Analyses",
    booktitle = {9$^{th}$ International Semantic Sensor Networks Workshop (SSN)},
    year = {2018}

--- back

# Acknowledgments
{:numbered="false"}

TBC
