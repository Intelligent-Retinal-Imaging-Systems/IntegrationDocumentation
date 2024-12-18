---
title: DFT (DFT-P03)
parent: HL7 Messages
---

## Standard Charge (DFT-P03) Outbound Specifications
IRIS can push a single DFT message per order as a mechanism for dropping charges.

*We recommend dropping charges through your EMR/EHR Ambulatory workflow as a more reliable option to using a DFT Message. You have more information regarding the patient encounter in which to make this determination.*

### Table of Contents

- A. [Basic Interface Structure and Description](/IntegrationDocumentation/docs/integration/DFT_Results/Basic_Interface_Structure_and_Description)
- B. [MSH Segment – Message Header](/IntegrationDocumentation/docs/integration/DFT_Results/MSH_Segment_Message_Header)
- C. [EVN Segment – Event Type](/IntegrationDocumentation/docs/integration/DFT_Results/EVN_Segment_Event_Type)
- D. [PID Segment – Patient Identification](/IntegrationDocumentation/docs/integration/DFT_Results/PID_Segment_Patient_Identification)
- E. [PV1 Segment – Patient Visit](/IntegrationDocumentation/docs/integration/DFT_Results/PV1_Segment_Patient_Visit)
- F. [FT1 (Option 1) – Financial Transaction](/IntegrationDocumentation/docs/integration/DFT_Results/FT1_Option1_Financial_Transaction)
   - a. [Professional Charge](/IntegrationDocumentation/docs/integration/DFT_Results/FT1_Option1_Professional_Charge)
   - b. [CPT II Optional Extra FT1 segment](/IntegrationDocumentation/docs/integration/DFT_Results/FT1_Option1_CPT_II_Optional_Extra_FT1_segment)
- G. [FT1 (Option 2) – Financial Transaction](/IntegrationDocumentation/docs/integration/DFT_Results/FT1_Option2_Financial_Transaction)
   - a. [Professional Charge](/IntegrationDocumentation/docs/integration/DFT_Results/FT1_Option2_Professional_Charge)
   - b. [Technical Charge](/IntegrationDocumentation/docs/integration/DFT_Results/FT1_Option2_Technical_Charge)
- H. [Most Common Diagnoses](/IntegrationDocumentation/docs/integration/DFT_Results/Most_Common_Diagnoses)
- I. [Example Messages](/IntegrationDocumentation/docs/integration/DFT_Results/Example_Messages)

