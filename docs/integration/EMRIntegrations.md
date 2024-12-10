---
title: EMR Integrations
---

<<<<<<< HEAD:integration/EMRIntegrations.md
## EMR Integrations
IRIS Provides integration services to  *on premise* amd most cloud based EMR platforms. 

## On Premise EMR/EHR systems
There are two basic components to a on premise integration: 
- Transport - Software / Networking components that provide the path between IRIS and the target EMR/EHR
- Content - Data that is passed between the systems

The primary piece of software that supports *Transport* is the [IRIS EMR Proxy application](#iris-emr-proxy-application).
*Content* is encoded as [HL7](#hl7) messages.
=======
# EMR Integrations
IRIS Provides integration services to  *on premise* amd most cloud based EMR systems.  

### On Premise EMR/EHR systems
On Premise systems are supported by the IRIS EMR Proxy application.  
>>>>>>> ae8824d0780693e6f2607394b456c9d8a8dcff85:docs/integration/EMRIntegrations.md

### IRIS EMR Proxy application
IRIS is a SAAS service hosted in the Azure cloud environment.  In order to provide seamless integration to your on premise system the EMR Proxy application must be installed on a Windows application server (or virtual) connected on the same Intranet where your EMR/EHR resides. The EMR Proxy provides a secure path between your integration engine and the IRIS cloud services.

Complete details can be found at [IRIS EMR Proxy Application Requirements and Specifications](./EMRProxyReqAndSpecs.html)


### Cloud based EMR/EHR systems
Cloud based EMRs have unique integration requirements involving the provider but can typically be setup quickly. 

Examples of Cloud EMR systems include: Athena, OCHIN and ECW.  A complete list with setup details can be found at [Cloud EMR/EHR Providers](IRISEMRCloudProviders.html).



<<<<<<< HEAD:integration/EMRIntegrations.md
## HL7
*Content* is provided between IRIS and your system through standard HL7 encoded messages for receiving orders and returning results.
=======
### HL7
Integration to your EMR system is accomodated by using standard HL7 messages for receiving orders and returning results.
>>>>>>> ae8824d0780693e6f2607394b456c9d8a8dcff85:docs/integration/EMRIntegrations.md

Orders are submitted from your system using the standard [HL7 ORM Message](ORMSpecifications.html).

Results are returned as one or more [HL7 ORU Messages](./TEC_007_Rev_B_Standard_Results.html).
IRIS also supports sending [DFT](DFT_Results.html) and [MDM](MDM_Results.html) messages on completed results. 





