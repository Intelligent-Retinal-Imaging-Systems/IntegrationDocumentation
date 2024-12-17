---
title: HL7 Messages
parent: EMR Integrations
---

# HL7 Messages

*Content* is passwed between IRIS and your system through standard HL7 encoded messages for receiving orders and returning results.

Orders are submitted from your system using the standard [HL7 ORM Message](/IntegrationDocumentation/docs/integration/TEC_005_Rev_C_Standard_Orders).

Results are returned as one or more [HL7 ORU Messages](/IntegrationDocumentation/docs/integration/TEC_007_Rev_C_Standard_Results).
IRIS also supports sending [DFT](/IntegrationDocumentation/docs/integration/DFT_Results/DFT_Results.md) and [MDM](/IntegrationDocumentation/docs/integration/MDM_Results) messages on completed results. 


