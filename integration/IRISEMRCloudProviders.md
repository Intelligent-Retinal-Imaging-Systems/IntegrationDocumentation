---
title: Cloud Systems
parent: EMR Integrations
nav_order: 2
---

# SAAS (Cloud based) EMR Systems

As IRIS is also a SAAS application, Integrating to SAAS based EMR/EHR systems is a natural progression. We do not take the approach of "build it and they will come" rather we engage the vendor at which point a customer using that system enters into a relationship with IRIS. In the majority of cases, the vendor already supports an HL7 feed for such operations and the process of  integrating is routine. Generally speaking, the amount of time it takes to complete an integration is dependent on that vendors availability.

## How do these integrations work
As with conventional EMR Integrations there are two components: **Transport** and **Content**.

Transport is facilitated with a dedicated VPN connection between IRIS and the vendor.

Content is encoded as HL7 messages.

The main difference in this environment is that the transport is shared for all clients using that provider.  Header content in the HL7 messaging allows the segmentation needed to identify the associated customer and location. 

## How does IRIS decide when to integrate with a Cloud Provider?
As a general position, IRIS embraces the trend towards SAAS based options in healthcare and will make every effort possible to provide integration where such options are available in a secure and cost effective manner. 

## Vendor Fees
Cloud providers may charge transaction fees associated with orders on the IRIS platform.  Make sure to check with your IRIS sales representative to determine how that could effect your cost.


## Currently Supported SAAS systems
- [Athena](/assets/Athena.pdf)
- OCHIN
- ECW