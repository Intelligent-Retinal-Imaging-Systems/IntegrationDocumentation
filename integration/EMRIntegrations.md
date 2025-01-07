---
title: EMR Integrations
parent: Order Processing Integration
nav_order: 3
has_toc: false
---

# EMR Integrations

IRIS Provides integration services to *on-premise* and SAAS (cloud based) EMR/EHR platforms. 

## On Premise EMR/EHR systems
*See [Technical Architecture Diagram](/assets/TEC%20014%20Rev%20A%20-%20EMR%20Integration%20Technical%20Diagram.pdf) for an illustration of how the IRIS system fits within your network.*

There are two basic components to an on-premise integration: 
- **Transport** - Software / Networking components that provide the path between IRIS and the target EMR/EHR
- **Content** - Data that is passed between the systems

The primary piece of software that supports *Transport* is the [IRIS EMR Proxy application](/integration/IRISEMRProxy/).
*Content* is encoded as [HL7](/integration/hl7messages/) messages.

Integration to On-premise systems require use of the IRIS EMR Proxy application.  



#### IRIS EMR Proxy application
IRIS is a SAAS service hosted in the Azure cloud environment.  In order to provide secure integration to your on-premise system the EMR Proxy application must be installed on a Windows application server (or virtual) connected on the same Intranet where your EMR/EHR resides. The EMR Proxy provides a secure path between your integration engine and IRIS cloud services.

Details can be found at [IRIS EMR Proxy Application Requirements and Specifications](/integration/EMRProxyReqAndSpecs/)


## Cloud based EMR/EHR systems
Cloud based EMRs have unique integration requirements involving the provider but can typically be setup quickly. 

Examples of Cloud EMR systems include: Athena, OCHIN and ECW.  Details can be found at [Cloud EMR/EHR Providers](/integration/IRISEMRCloudProviders/).


 




