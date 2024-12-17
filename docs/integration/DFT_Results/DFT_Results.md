---
title: DFT 
parent: HL7 Messages
---

## HL7 DFT Results Message

### Table of Contents

- A. [Basic Interface Structure and Description](/docs/integration/DFT_Results/Basic_Interface_Structure_and_Description.md)
- B. [MSH Segment – Message Header](/docs/integration/DFT_Results/MSH_Segment_Message_Header.md)
- C. [EVN Segment – Event Type](/docs/integration/DFT_Results/EVN_Segment_Event_Type.md)
- D. [PID Segment – Patient Identification](/docs/integration/DFT_Results/PID_Segment_Patient_Identification.md)
- E. [PV1 Segment – Patient Visit](/docs/integration/DFT_Results/PV1_Segment_Patient_Visit.md)
- F. [FT1 (Option 1) – Financial Transaction](/docs/integration/DFT_Results/FT1_Option1_Financial_Transaction.md)
   - a. [Professional Charge](/docs/integration/DFT_Results/FT1_Option1_Professional_Charge.md)
   - b. [CPT II Optional Extra FT1 segment](/docs/integration/DFT_Results/FT1_Option1_CPT_II_Optional_Extra_FT1_segment.md)
- G. [FT1 (Option 2) – Financial Transaction](/docs/integration/DFT_Results/FT1_Option2_Financial_Transaction.md)
   - a. [Professional Charge](/docs/integration/DFT_Results/FT1_Option2_Professional_Charge.md)
   - b. [Technical Charge](/docs/integration/DFT_Results/FT1_Option2_Technical_Charge.md)
- H. [Most Common Diagnoses](/docs/integration/DFT_Results/Most_Common_Diagnoses.md)
- I. [Example Messages](/docs/integration/DFT_Results/Example_Messages.md)

[Back to EMR Integrations page](/docs/integration/EMRIntegrations.md)

**Acknowledgments**

```
Interface specifications prepared by Adam Diaz. Please send any feedback to
support@irishelp.zendesk.com.
```
**Confidentiality and Proprietary Rights**

```
This document is the confidential property of Intelligent Retinal Imaging Systems (IRIS).
No part of this document may be reproduced in any form or incorporated into any
information retrieval system without the written permission of IRIS.
```
**Limitations and Conditions of Use**

```
Some fields noted in this document need the pre-defined values to be identified by the
receiving EMR. Those values will be covered in the Standard Orders (ORM-O01)
Interface document and used here. If there are any fields represented in this document
that are not populated but required by a receiving EMR, IRIS will populate these value(s)
as requested. IRIS uses HL7 v2.4 as a main protocol for message sharing. If the receiving
EMR requires a different version, IRIS will provide messages for the corresponding
version. This document will describe the standard IRIS DFT message by segments as they
appear in an HL7 message.
```
**Disclaimers**

```
Although unlikely, IRIS reserves the right to make changes in specifications and features
shown herein at any time without notice. This does not constitute a representation or
documentation regarding the service featured. Contact your IRIS Representative for the
most current information.
```
```
Intelligent Retinal Imaging Systems™
2 N Palafox Street, Suite 200
Pensacola, Florida 32502
1- 888-535-2574 | info@retinalscreenings.com
```
