---
title: HL7 Messages
parent: EMR Integrations
nav_order: 1
has_toc: false
---

# HL7 Messaging

*Content* is passed between IRIS and your system through standard HL7 encoded messages.

IRIS starts with HL7 v2.4 as a main protocol for message sharing.  If the receiving EMR requires a different version, IRIS can customize messages for the corresponding version. 

### Common HL7 Message types
While IRIS is capable of any HL7 communication, the following list contains the commonly used messages.

| Message type | Default | Usage
| -- | -- | -- |
| [ORM](/integration/ORM/TEC_005_Rev_C_Standard_Orders/) | ORM-O01 | Orders sent from EMR to IRIS
| [ORU](/integration/ORU/TEC_007_Rev_C_Standard_Results/) | ORU-R01 | Results sent from IRIS to EMR
| [DFT](/integration/DFT_Results/DFT_Results/) | DFT-P03 | Drop charges to EMR from IRIS
| [MDM](/integration/MDM/MDM_Results/) | MDM-T02 | From IRIS to EMR: Results, Update documents

## Messages Sent To Your EMR

Typical for HL7 transmissions, all messages sent to your EMR are encapsulated in Minimal Lower Layer Protocol (MLLP) and expect a corresponding HL7 ACK message signaling the receipt of the message.  

### ACK Message

In the event an ACK message is malformed or contains a negative control code, the IRIS system could resend the original message.  The most notable exception to this is the DFT message. Because of the potential for duplicating charges, IRIS will send the DFT message a maximum of one time per order regardless of the response.

### ADT Messages

On occasion, we are asked if ADT messaging is supported and for our existing services the answer is no.  The primary reason for this is due to the HIPAA minimum necessary rule standard. PHI exposed via ADT messaging is superfluous to our needs therefore we do not support it.

## Customization

Variations of messages typically involve the use of the same common message segments with alternate positioning.  IRIS builds all HL7 content from mapping instructions therefore making adaptations to these variations possible through configuration.  

Contact IRIS Support if such changes are needed.

