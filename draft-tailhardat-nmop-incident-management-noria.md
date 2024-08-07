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



# Security Considerations

TODO Security

Multi hosting


# IANA Considerations

This document has no IANA actions.

# Open Issues

TBC ...


# References

## Normative references

TBC

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

--- back

# Acknowledgments
{:numbered="false"}

TBC
