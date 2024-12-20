---
title: HL7 Messages
parent: EMR Integrations
has_toc: false
---

# HL7 Messaging

*Content* is passed between IRIS and your system through standard HL7 encoded messages.

IRIS uses HL7 v2.4 as a main protocol for message sharing.  If the receiving EMR requires a different version, IRIS can customize messages for the corresponding version. 

IRIS Supports the following HL7 Messaging

| Message type | Default | Usage
| -- | -- | -- |
| [ORM](/IntegrationDocumentation/docs/integration/ORM/TEC_005_Rev_C_Standard_Orders) | ORM-O01 | Orders sent from EMR to IRIS
| [ORU](/IntegrationDocumentation/docs/integration/ORU/TEC_007_Rev_C_Standard_Results) | ORU-R01 | Results sent from IRIS to EMR
| [DFT](/IntegrationDocumentation/docs/integration/DFT_Results/DFT_Results.md) | DFT-P03 | Drop charges to EMR from IRIS
| [MDM](/IntegrationDocumentation/docs/integration/MDM_Results) | MDM-T02 | From IRIS to EMR: Results, Update documents


### Customization
Variations of messages typically involve the use of the same common message segments with alternate positioning.  IRIS builds all HL7 content from mapping instructions therefore making adaptations to these variations possible through configuration.  

Contact IRIS Support if such changes are needed. 