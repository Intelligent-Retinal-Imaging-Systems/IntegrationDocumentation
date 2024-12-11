---
title: HL7 Messages
---

# HL7 Messages

*Content* is passwed between IRIS and your system through standard HL7 encoded messages for receiving orders and returning results.

Orders are submitted from your system using the standard HL7 [ORM (ORM-001)](./TEC_005_Rev_C_Standard_Orders.html) message.

Results are returned as one or more standard HL7 [ORU (ORU-R01)](./TEC_007_Rev_C_Standard_Results.html) messages.
IRIS also supports sending [DFT](./DFT_Results.html) and [MDM](./MDM_Results.html) messages on completed results. 

