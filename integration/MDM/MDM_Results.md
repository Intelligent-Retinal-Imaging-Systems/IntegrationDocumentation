---
title: MDM (MDM-T02)
parent: HL7 Messages
---

<details markdown="block">
  <summary>
    Table of contents
  </summary>
  {: .text-delta }
- TOC
{:toc}
</details>

##  Original Document Notification with Content (MDM-T02) Outbound Specifications

IRIS can send results to your EMR as an MDM message.  By far, most EMR/EHR systems prefer an ORU result but in cases where your workflow is better suited to an MDM this can be used. 


## Basic Interface Structure and Description

This document outlines the values sent in an HL7 results message (MDM-T02) from IRIS to a third-party system. This third-party system could be another application, an interface engine, or an EMR. For the purposes of this documentation, this third-party will be referred to an EMR. 
 
The following sections contain details of the MDM message content by HL7 Segment.  

## MSH Segment - Message Header
The message header segment includes information that defines the structure of the message.

### Sample MSH segment: 

```
MSH|^\~\&|IRIS|IRIS|VENDOR|VENDOR|20170410145907||MDM^T02|170410145907|T|2.4 
```

| Field  | Name and type  | Sample value  | Description  |
| -- | -- | -- | -- |
| MSH-1  | Field Separator (ST)  | |  | Auto generated  |
| MSH-2  | Encoding Characters (ST)  | ^\~\&  | Auto generated  |
| MSH-3  | Sending Application (HD)  | IRIS  | “IRIS” is used as the default value  |
| MSH-4  | Sending Facility (HD)  | IRIS  | “IRIS” is used as the default value  |
| MSH-5  | Receiving Application (HD)  | VENDOR  | The name of the EMR. This need to be pre-defined  |
| MSH-6  | Receiving Facility (HD)  | VENDOR  | The name or id of clinic. This need to be pre-defined.  |
| MSH-7  | Date/Time of Message (TS)  | yyyyMMddHHmmss format, e.g. "20190410145907"  | Auto generated based off server time (UTC if hosted by IRIS)  |
| MSH-8  | Security (ST)  |   | Empty  |
| MSH-9  | Message Type (MSG)  | MDM^T02  | Unchanging  |
| MSH-10  | Message Control ID (ST)  | 190410145907  | Auto generated from server time (UTC if hosted by Iris)  |
| MSH-11  | Processing ID (PT)  | T  | P (Production) or T (Test) will be used based on the system environment  |
| MSH-12  | Version ID (VID)  | 2.4  | HL7 Version  |




## PID Segment - Patient Identification 

The patient identification segment will include patient-specific demographic information. 

### Sample PID segment: 

```
PID||ITCC20170410^^^^MRN|ITCC20170410||DOE^JOHN||19581012|M||||||||||1234|111-22-3333 
```

| Field  | Name and type  |  Sample value  | Description  |
| -- | -- | -- | -- |
| PID-1  | Set ID - PID (SI)  |  |  Empty by default  |
|  PID-2  | Patient ID (CX)  | ITCC20170410^^^^MRN  |  |
|   | PID-2.1 ID  |  ITCC20170410  | Related Patient's MRN value  |
|   | ….  |  | PID-2.2 through PID-2.4 empty by default  |
|  | PID-2.5 Identifier Type Code  | MRN  | Related Patient's ID type if requested  |
| PID-3  | Patient Identifier List (CX)  | ITCC20170410   | Reflects the same value as PID-2.1 by default  |
| PID-4  | Alternate Patient ID - PID (CX)  |  | Empty by default  |
| PID-5  | Patient Name (XPN)  | DOE^JOHN   | Related Patient's family name &given name  |
| PID-6  | Mother's Maiden Name (XPN)  |  | Empty by default  |
| PID-7  | Date/Time of Birth (TS)  | 19581012  | Related Patient's Date of birth; YYYYMMDD format  |
| PID-8  | Administrative Sex (IS)  |  M  | Related patient's sex (M or F)  |
| PID-9  | Patient Alias (XPN)  |   | Empty by default  |
| PID-10  | Race (CE)  |   | Empty by default  |
| PID-11  | Patient Address (XAD)  |   | Empty by default  |
| PID-12  | County Code (IS)  |   | Empty by default  |
| PID-13  | Phone Number - Home (XTN)  |   | Empty by default  |
| PID-14  | Phone Number - Business (XTN)  |   | Empty by default  |
| PID-15  | Primary Language (CE)  |   | Empty by default  |
| PID-16  | Marital Status (CE)  |   | Empty by default  |
| PID-17  | Religion (CE)  |  | Empty by default  |
| PID-18  | Patient Account Number (CX)  | 1234  | Related Patient's CSN/Account value/Encounter number  |
| PID-19  | SSN Number - Patient (ST)  | 111-22-3333  | Iris does not store SSN  |

## TXA Segment - Document Notification
Document identification

### Sample TXA Segment

```
TXA|1|92250^Retinal Imaging w Interpretation||200901151010||||||GR0001^DOE^JANE^^MD^DR^^^^^^^NPI||442B30D3-C963-434E-8886-3735CED1C5E8||124566|||F|
```

| Field  | Name and type  | Sample value  | Description  |
| -- | -- | -- | -- |
| TXA-1  | Set ID - TXA (SI)  | 1  | Always 1  |
| TXA-2.1  | Identifier  | 92250  | Procedure Code  |
| TXA-2.2  | Document description  | Retinal Imaging w Interpretation  | Procedure Code Description |
| TXA-4 | Date/Time | 200901151010 | Julian Date time 
| TXA-10.1 | Assigned Document Authenticator (ADA) Person Id | 0123456789 | Ordering Provider Id (NPI)
| TXA-10.2 | ADA Family Name | DOE | Ordering Provider Last name
| TXA-10.3 | ADA Given Name | JANE | Ordering Provider First name
| TXA-10.5 | ADA Name Suffix | MD | Ordering Provider Name Suffix
| TXA-10.6 | ADA Name Prefix | DR | Ordering Provider Name Prefix
| TXA-10.13 | ADA Identifier type | NPI | Ordering Provider Id type 
| TXA-12 | Unique Doc Number | 442B30D3-C963-434E-8886-3735CED1C5E8 | Unique identifier for this document 
| TXA-14 | Placer Order Number | 124566 | Order Number as originally created by EMR
| TXA-17 | Document Completion Status | F | Result report status ((F)inal, (C)orrection)

## PV1 Segment – Patient Visit 

The patient visit segment includes patient-specific visit information.

### Sample PV1 segment: 

```
PV1|1|O|POC01||||GR0001^DOE^JANE^^^MD^MD^^^^^^NPI|OP0001^DOE^JACK^^^MD^M D^^^^^^NPI|||||||||GR0001^DOE^JANE^^^MD^MD^^^^^^NPI|||||||||||||||||||||||||||20170410145803|20170410145803 
```

| Field  | Name and type  | Sample value  | Description  |
| -- | -- | -- | -- |
| PV1-1  | Set ID - PV1 (SI)  | 1  | Always 1  |
| PV1-2  | Patient Class (IS)  | O  | Always "O" (for outpatient)  |
| PV1-3  | Assigned Patient Location (PL)  | POC01  | Point of care information; received from the ORM HL7 message  |
| PV1-4  | Admission Type (IS)  |   | Empty by default  |
| PV1-5  | Preadmit Number (CX)  |   | Empty by default  |
| PV1-6  | Prior Patient Location (PL)  |   | Empty by default  |
| PV1-7  | Attending Doctor (XCN)  | OP0001^DOE^JACK^^ ^MD^MD^^^^^^NPI  | This reflects the ordering provider received in the ORM HL7 message  |
|   | PV1-7.1 ID  | OP0001  | Reflects the ORM HL7 messageORC-12.1 value  |
|   | PV1-7.2 Family Name  | DOE  | Reflects the ORM HL7 messageORC-12.2 value  |
|   | PV1-7.3 Given Name  | JANE  | Reflects the ORM HL7 messageORC-12.3 value  |
|   | …..  |   | PV1-7.4 & PV1-7.5 empty by default  |
|   | PV1-7.5 Prefix  | MD  | Credentials of the ordering physician if available  |
|   | PV1-7.6 Degree  | MD  | Credentials of the ordering physician if available  |
|   | …..  |   | PV1-7.7 through PV1-7.12 Empty by default  |
|   | PV1-7.13 Identifier Type Code  | NPI  | Provider type identifying code; typically “NPI”  |
| PV1-8  | Referring Doctor (XCN)  | OP0001^DOE^JACK^^ ^MD^MD^^^^^^NPI  | This reflects the ordering provider received in the ORM HL7 message  |
|   | PV1-8.1 ID  | OP0001  | Reflects the ORM HL7 messageORC-12.1 value  |
|   | PV1-8.2 Family Name  | DOE  | Reflects the ORM HL7 messageORC-12.2 value  |
| -- | -- | -- | -- |
|   | PV1-8.3 Given Name  | JACK  | Reflects the ORM HL7 messageORC-12.3 value  |
|   | …..  |   | PV1-8.4 & PV1-8.5 empty by default  |
|   | PV1-8.5 Prefix  | MD  | Credentials of the ordering physician if available  |
|   | PV1-8.6 Degree  | MD  | Credentials of the ordering physician if available  |
|   | …..  |   | PV1-8.7 through PV1-8.12 Empty by default  |
|   | PV1-8.13 Identifier Type Code  | NPI  | Provider type identifying code; typically “NPI”  |
| PV1-10  | Hospital Service (IS)  |   | Empty by default  |
| PV1-11  | Temporary Location (PL)  |   | Empty by default  |
| PV1-12  | Preadmit Test Indicator (IS)  |   | Empty by default  |
| PV1-13  | Re-admission Indicator (IS)  |   | Empty by default  |
| PV1-14  | Admit Source (IS)  |   | Empty by default  |
| PV1-15  | Ambulatory Status (IS)  |   | Empty by default  |
| PV1-16  | VIP Indicator (IS)  |   | Empty by default  |
| PV1-17  | Admitting Doctor (XCN)  | OP0001^DOE^JACK^^ ^MD^MD^^^^^^NPI  | This reflects the ordering provider received in the ORM HL7 message  |
|   | PV1-17.1 ID  | OP0001  | Reflects the ORM HL7 messageORC-12.1 value  |
|   | PV1-17.2 Family Name  | DOE  | Reflects the ORM HL7 messageORC-12.2 value  |
|   | PV1-17.3 Given Name  | JANE  | Reflects the ORM HL7 messageORC-12.3 value  |
|   | …..  |   | PV1-17.4 & PV1-17.5 empty bydefault  |
|   | PV1-17.5 Prefix  | MD  | Credentials of the ordering physician if available  |
|   | PV1-17.6 Degree  | MD  | Credentials of the ordering physician if available  |
|   | …..  |   | PV1-17.7 through PV1-17.12 Empty by default  |
|   | PV1-17.13 Identifier Type Code  | NPI  | Provider type identifying code; typically “NPI”  |
| PV1-18  | Patient Type (IS)  |   | Empty by default  |
| PV1-19  | Visit Number (CX)  |   | Related Patient's CSN/Account value/Encounter number  |
| PV1-20  | Financial Class (FC)  |   | Empty by default  |
| -- | -- | -- | -- |
| PV1-21  | Charge Price Indicator (IS)  |   | Empty by default  |
| PV1-22  | Courtesy Code (IS)  |   | Empty by default  |
| PV1-23  | Credit Rating (IS)  |   | Empty by default  |
| PV1-24  | Contract Code (IS)  |   | Empty by default  |
| PV1-25  | Contract Effective Date (DT)  |   | Empty by default  |
| PV1-26  | Contract Amount (NM)  |   | Empty by default  |
| PV1-27  | Contract Period (NM)  |   | Empty by default  |
| PV1-28  | Interest Code (IS)  |   | Empty by default  |
| PV1-29  | Transfer to Bad Debt Code (IS)  |   | Empty by default  |
| PV1-30  | Transfer to Bad Debt Date (DT)  |   | Empty by default  |
| PV1-31  | Bad Debt Agency Code (IS)  |   | Empty by default  |
| PV1-32  | Bad Debt Transfer Amount (NM)  |   | Empty by default  |
| PV1-33  | Bad Debt Recovery Amount (NM)  |   | Empty by default  |
| PV1-34  | Delete Account Indicator (IS)  |   | Empty by default  |
| PV1-35  | Delete Account Date (DT)  |   | Empty by default  |
| PV1-36  | Discharge Disposition (IS)  |   | Empty by default  |
| PV1-37  | Discharged to Location (DLD)  |   | Empty by default  |
| PV1-38  | Diet Type (CE)  |   | Empty by default  |
| PV1-39  | Servicing Facility (IS)  |   | Empty by default  |
| PV1-40  | Bed Status (IS)  |   | Empty by default  |
| PV1-41  | Account Status (IS)  |   | Empty by default  |
| PV1-42  | Pending Location (PL)  |   | Empty by default  |
| PV1-43  | Prior Temporary Location (PL)  |   | Empty by default  |
| PV1-44  | Admit Date/Time (TS)  | yyyyMMddHHmmss format  | Date of image captured |
| PV1-45  | Discharge Date/Time (TS)  | yyyyMMddHHmmss format  | Date of image captured |
| PV1-46  | Current Patient Balance (NM)  |   | Empty by default  |
| PV1-47  | Total Charges (NM)  |   | Empty by default  |
| PV1-48  | Total Adjustments (NM)  |   | Empty by default  |
| PV1-49  | Total Payments (NM)  |   | Empty by default  |
| PV1-50  | Alternate Visit ID (CX)  |   | Empty by default  |
| PV1-51  | Visit Indicator (IS)  |   | Empty by default  |
| PV1-52  | Other Healthcare Provider (XCN)  |   | Empty by default  |


## OBX – Observation Result Segment 
OBX contains the document content. It is used to transmit a single observation or observation fragment. OBX segments can repeat and each one contains following information. 

IRIS’ default OBX configuration contains the discrete results in the first 9 OBX segments, followed by the textual portion of the result findings, and then the document modality. The breakdown follows this configuration (the numbers refer to the Set ID): OBX 1 contains the overall severity for discrete findings of both eyes, OBX 2-5 contain details of the right eye, OBX 6-9 contain details of the left eye, OBX 10-30 grading results, and the last OBX is where either an encoded PDF or pointer link (static URL) is sent. 

### Sample Discrete Results (Default): 

```
OBX|1|ST|SEVERITY^^IRIS|1|NORMAL||||||F 
OBX|2|ST|RIGHTDIABRETIN^^IRIS|2|None||||||F 
OBX|3|ST|RIGHTMACEDEMA^^IRIS|3|None||||||F 
OBX|4|ST|RIGHTOTHERRETIN^^IRIS|4|None||||||F 
OBX|5|ST|RIGHTQUALAPP^^IRIS|5|Gradable Image||||||F 
OBX|6|ST|LEFTDIABRETIN^^IRIS|6|None||||||F 
OBX|7|ST|LEFTMACEDEMA^^IRIS|7|None||||||F 
OBX|8|ST|LEFTOTHERRETIN^^IRIS|8|None||||||F 
OBX|9|ST|LEFTQUALAPP^^IRIS|9|Gradable Image||||||F 
```

### Sample Discrete Results with Alternating OBX/NTE segments (Secondary Option): 

```
OBX|1|ST|^^IRIS|1|NORMAL|||
NTE|1|ST|SEVERITY 
OBX|2|ST|^^IRIS|2|None||||||F
NTE|1|ST|RIGHTDIABRETIN
OBX|3|ST|^^IRIS|3|None||||||F 
NTE|1|ST|RIGHTMACEDEMA 
OBX|4|ST|^^IRIS|4|None||||||F 
NTE|1|ST|RIGHTOTHERRETIN 
OBX|5|ST|RIGHTQUALAPP^^IRIS|5|Gradable Image||||||F 
OBX|6|ST|^^IRIS|6|None||||||F 
NTE|1|ST|LEFTDIABRETIN 
OBX|7|ST|^^IRIS|7|None||||||F 
NTE|1|ST|LEFTMACEDEMA 
OBX|8|ST|^^IRIS|8|None||||||F 
NTE|1|ST|LEFTOTHERRETIN 
OBX|9|ST|LEFTQUALAPP^^IRIS|9|Gradable Image||||||F 
```

## First OBX
Severity section

### Sample OBX segment: First OBX 
```
OBX|1|ST|SEVERITY^^IRIS|1|NORMAL||||||F
```

| Field  | Name and type  | Sample value  | Description  |
| -- | -- | -- | -- |
| OBX-1  | Set ID - OBX (SI)  | 1  | Increases sequentially by 1  |
| OBX-2  | Value Type (ID)  | ST  | The literal value "ST" (i.e. String for OBX-5)  |
|  OBX-3  | Observation Identifier (CE)  | SEVERITY^^IRIS  |  |
|  | OBX-3.1 Identifier  | SEVERITY  | The literal value “SEVERITY”  |
|    | OBX-3.2 Text  |   | Empty by default  |
|  | OBX-3.3 Name of Coding System  | IRIS  | The literal value “IRIS”  |
| OBX-4  | Observation Sub-Id (ST)  | 1  | Sequential counter that matches the Set ID  |
| OBX-5  | Observation Value (Varies)  | CRITICAL   | One of three values based on the result findings: NORMAL, ALERT, or CRITICAL  |
| OBX-6  | Units (CE)  |   | Empty by default  |
| OBX-7  | References Range (ST)  |  | Empty by default  |
| OBX-8  | Abnormal Flags (IS)  | AA   | One of three values based on the result findings: empty (Normal), A (ALERT), or AA (CRITICAL)  |
| OBX-9  | Probability (NM)  |   | Empty by default  |
| OBX-10  | Nature of Abnormal Test (ID)  |  | Empty by default  |
| OBX-11  | Observation Result Status (ID)  | F  | F = Final, C = Corrected*  |

## Second OBX

### Sample OBX segment: 
```
OBX|2|ST|RIGHTDIABRETIN^^IRIS|2|None||||||F
```

| Field  | Name and type  | Sample value  | Description  |
| -- | -- | -- | -- |
| OBX-1  | Set ID - OBX (SI)  | 2  | Increase sequentially by 1  |
| OBX-2  | Value Type (ID)  | ST  | Always "ST" (i.e. String for OBX- 5)  |
|  OBX-3  | Observation Identifier (CE)  | RIGHTDIABRETIN^^IRIS  |  |
|   | OBX-3.1 Identifier  | RIGHTDIABRETIN   | Always "RIGHTDIABRETIN"; stands for RIGHT eye diabetic retinopathy  |
|   | OBX-3.2 Text  |  | Empty by default  |
|  | OBX-3.3 Name of Coding System  | IRIS  | Always "IRIS"  |
| OBX-4  | Observation Sub-Id (ST)  | 2  | Sequential counter that matches the Set ID  |
| OBX-5  | Observation Value (Varies)  | None   | One of three values based on the result findings: None, Mild, Moderate, Severe, or Proliferative  |
| OBX-6  | Units (CE)  |   | Empty by default  |
| OBX-7  | References Range (ST)  |   | Empty by default  |
| OBX-8  | Abnormal Flags (IS)  |   | One of three values based on the result findings: empty (Normal), A (ALERT), or AA (CRITICAL)  |
| OBX-9  | Probability (NM)  |   | Empty by default  |
| OBX-10  | Nature of Abnormal Test (ID)  |  | Empty by default  |
| OBX-11  | Observation Result Status (ID)  | F  | F = Final, C = Corrected*  |


## Third OBX 

### Sample OBX segment: Third 
```
OBX|3|ST|RIGHTMACEDEMA^^IRIS|3|Severe|||AA|||F 
```

| Field  | Name and type  | Sample value  | Description  |
| -- | -- | -- | -- |
| OBX-1  | Set ID - OBX (SI)  | 3  | Increase sequentially by 1  |
| OBX-2  | Value Type (ID)  | ST  | Always "ST" (i.e. String for OBX- 5)  |
|  OBX-3  | Observation Identifier (CE)  | RIGHTMACEDEMA^^IRIS  |  |
|   | OBX-3.1 Identifier  | RIGHTMACEDEMA   | Always "RIGHTMACEDEMA"; stands for RIGHT eye macular edema  |
|   | OBX-3.2 Text  |  | Empty by default  |
|  | OBX-3.3 Name of Coding System  | IRIS  | Always "IRIS"  |
| OBX-4  | Observation Sub-Id (ST)  | 3  | Sequential counter that matches the Set ID  |
| OBX-5  | Observation Value (Varies)  | Severe   | One of three values based on the result findings: None, Mild, Moderate, or Severe  |
| OBX-6  | Units (CE)  |   | Empty by default  |
| OBX-7  | References Range (ST)  |  | Empty by default  |
| OBX-8  | Abnormal Flags (IS)  | AA   | One of three values based on the result findings: empty (Normal), A (ALERT), or AA (CRITICAL)  |
| OBX-9  | Probability (NM)  |   | Empty by default  |
| OBX-10  | Nature of Abnormal Test (ID)  |  | Empty by default  |
| OBX-11  | Observation Result Status (ID)  | F  | F = Final, C = Corrected*  |


## Fourth OBX 

### Sample OBX segment: 
```
OBX|4|ST|RIGHTOTHERRETIN^^IRIS|4|None||||||F
```

| Field  | Name and type  | Sample value  | Description  |
| -- | -- | -- | -- |
| OBX-1  | Set ID - OBX (SI)  | 4  | Increase sequentially by 1  |
| OBX-2  | Value Type (ID)  | ST  | Always "ST" (i.e. String for OBX- 5)  |
|  OBX-3  | Observation Identifier (CE)  | RIGHTOTHERRETIN^^IRIS  |  |
|   | OBX-3.1 Identifier  | RIGHTOTHERRETIN   | Always "RIGHTOTHERRETIN"; stands for RIGHT eye OTHER retinopathy  |
|   | OBX-3.2 Text  |  | Empty by default  |
|  | OBX-3.3 Name of Coding System  | IRIS  | Always "IRIS"  |
| OBX-4  | Observation Sub-Id (ST)  | 4  | Sequential counter that matches the Set ID  |
| OBX-5  | Observation Value (Varies)  | None, Suspected Glaucoma, Suspected Dry AMD, Suspected Wet AMD, Suspected Vein Occlusion, Suspected HTN Retinopathy, Suspected Epiretinal Membrane, Suspected Macular Hole, Suspected Cataracts, Suspected Geographic Atrophy, Other  based on result.  | Providers can choose to apply a predefined description (see Sample Value) or populate with a free-text note  |
| OBX-6  | Units (CE)  |   | Empty by default  |
| OBX-7  | References Range (ST)  |   | Empty by default  |
| OBX-8  | Abnormal Flags (IS)  |   | One of three values based on the result findings: empty (Normal), or A (ALERT)  |
| OBX-9  | Probability (NM)  |   | Empty by default  |
| OBX-10  | Nature of Abnormal Test (ID)  |  | Empty by default  |
| OBX-11  | Observation Result Status (ID)  | F  |  |


## Fifth OBX 

### Sample OBX segment: 
```
OBX|5|ST|RIGHTQUALAPP^^IRIS|5|Gradeable Image||||||F 
```

| Field  | Name and type  | Sample value  | Description  |
| -- | -- | -- | -- |
| OBX-1  | Set ID - OBX (SI)  | 5  | Increase sequentially by 1  |
| OBX-2  | Value Type (ID)  | ST  | Always "ST" (i.e. String for OBX- 5)  |
|  OBX-3  | Observation Identifier (CE)  | RIGHTQUALAPP^^IRIS  |  |
|   | OBX-3.1 Identifier  | RIGHTQUALAPP   | Always "RIGHTQUALAPP"; stands for RIGHT eye image quality.  |
|   | OBX-3.2 Text  |  | Empty by default  |
|  | OBX-3.3 Name of Coding System  | IRIS  | Always "IRIS"  |
| OBX-4  | Observation Sub-Id (ST)  | 5  | Sequential counter that matches the Set ID  |
| OBX-5  | Observation Value (Varies)  | Gradable Image   | Either “Gradable Image” or “Not Gradable Image” based on the image quality  |
| OBX-6  | Units (CE)  |   | Empty by default  |
| OBX-7  | References Range (ST)  |   | Empty by default  |
| OBX-8  | Abnormal Flags (IS)  |   | Empty by default  |
| OBX-9  | Probability (NM)  |   | Empty by default  |
| OBX-10  | Nature of Abnormal Test (ID)  |  | Empty by default  |
| OBX-11  | Observation Result Status (ID)  | F  |  |

## Sixth OBX 

### Sample OBX segment: 
```
OBX|6|ST|LEFTDIABRETIN^^IRIS|6|Proliferative|||AA|||F 
```

| Field  | Name and type  | Sample value  | Description  |
| -- | -- | -- | -- |
| OBX-1  | Set ID - OBX (SI)  | 6  | Increase sequentially by 1  |
| OBX-2  | Value Type (ID)  | ST  | Always “ST” (i.e. String for OBX- 5)  |
|  OBX-3  | Observation Identifier (CE)  | LEFTDIABRETIN^^IRIS  |  |
|   | OBX-3.1 Identifier  | LEFTDIABRETIN   | Always "LEFTDIABRETIN"; stands for LEFT eye diabetic retinopathy  |
|   | OBX-3.2 Text  |  | Empty by default  |
|  | OBX-3.3 Name of Coding System  | IRIS  | Always "IRIS"  |
| OBX-4  | Observation Sub-Id (ST)  | 6  | Sequential counter that matches the Set ID  |
| OBX-5  | Observation Value (Varies)  | Proliferative   | One of three values based on the result findings: None, Mild, Moderate, Severe, or Proliferative  |
| OBX-6  | Units (CE)  |   | Empty by default  |
| OBX-7  | References Range (ST)  |  | Empty by default  |
| OBX-8  | Abnormal Flags (IS)  | AA   | One of three values based on the result findings: empty (Normal), A (ALERT), or AA (CRITICAL)  |
| OBX-9  | Probability (NM)  |   | Empty by default  |
| OBX-10  | Nature of Abnormal Test (ID)  |  | Empty by default  |
| OBX-11  | Observation Result Status (ID)  | F  | F = Final, C = Corrected*  |


## Seventh OBX 

### Sample OBX segment: Seventh OBX 
```
OBX|7|ST|LEFTMACEDEMA^^IRIS|7|None||||||F 
```

| Field  | Name and type  | Sample value  | Description  |
| -- | -- | -- | -- |
| OBX-1  |  Set ID - OBX (SI)  | 7  | Increase sequentially by 1  |
| OBX-2  |  Value Type (ID)  | ST  | Always “ST” (i.e. String for OBX- 5)  |
|  OBX-3  |  Observation Identifier (CE)  | LEFTMACEDEMA^^IRIS  |  |
|   | OBX-3.1 Identifier  | LEFTMACEDEMA   | Always "LEFTMACEDEMA"; stands for LEFT eye macular edema  |
|   | OBX-3.2 Text  |  | Empty by default  |
|  | OBX-3.3 Name of Coding System  | IRIS  | Always "IRIS"  |
| OBX-4  |  Observation Sub-Id (ST)  | 7  | Sequential counter that matches the Set ID  |
| OBX-5  |  Observation Value (Varies)  | None   | One of three values based on the result findings: None, Mild, Moderate, or Severe  |
| OBX-6  |  Units (CE)  |   | Empty by default  |
| OBX-7  |  References Range (ST)  |   | Empty by default  |
| OBX-8  |  Abnormal Flags (IS)  |   | One of three values based on the result findings: empty (Normal), A (ALERT), or AA (CRITICAL)  |
| OBX-9  |  Probability (NM)  |   | Empty by default  |
| OBX-10  |  Nature of Abnormal Test (ID)  |  | Empty by default  |
| OBX-11  |  Observation Result Status (ID)  | F  | F = Final, C = Corrected*  |


## Eighth OBX 

### Sample OBX segment: 
```
OBX|8|ST|LEFTOTHERRETIN^^IRIS|8|None||||||F 
```

| Field  | Name and type  | Sample value  | Description  |
| -- | -- | -- | -- |
| OBX-1  | Set ID - OBX (SI)  | 8  | Increase sequentially by 1  |
| OBX-2  | Value Type (ID)  | ST  | Always “ST” (i.e. String for OBX-5)  |
|  OBX-3  | Observation Identifier (CE)  | LEFTOTHERRETIN^^IRIS  | Empty by default  |
|   | OBX-3.1 Identifier  | LEFTOTHERRETIN   | Always "LEFTOTHERRETIN". Identify this OBX as a Left eye other retinopathy.  |
|   | OBX-3.2 Text  |  | Empty by default  |
|  | OBX-3.3 Name of Coding System  | IRIS  | Always "IRIS"  |
| OBX-4  | Observation Sub-Id (ST)  | 8  | Sequential counter that matches the Set ID  |
| OBX-5  | Observation Value (Varies)  | None, Suspected Glaucoma, Suspected Dry AMD, Suspected Wet AMD, Suspected Vein Occlusion, Suspected HTN Retinopathy, Suspected Epiretinal Membrane, Suspected Macular Hole, Suspected Cataracts, Suspected Geographic Atrophy, Other  based on result.  | Providers can choose to apply a predefined description (see Sample Value) or populate with a free-text note  |
| OBX-6  | Units (CE)  |   | Empty by default  |
| OBX-7  | References Range (ST)  |   | Empty by default  |
| OBX-8  | Abnormal Flags (IS)  |   | One of three values based on the result findings: empty (Normal), or A (ALERT)  |
| OBX-9  | Probability (NM)  |   | Empty by default  |
| OBX-10  | Nature of Abnormal Test (ID)  |  | Empty by default  |
| OBX-11  | Observation Result Status (ID)  | F  |  |

## Ninth OBX 

### Sample OBX segment: 
```
OBX|9|ST|LEFTQUALAPP^^IRIS|9|Gradeable Image||||||F 
```

| Field  | Name and type  | Sample value  | Description  |
| -- | -- | -- | -- |
| OBX-1  | Set ID - OBX (SI)  | 9  | Increase sequentially by 1  |
| OBX-2  | Value Type (ID)  | ST  | Always “ST” (i.e. String for OBX- 5)  |
|  OBX-3  | Observation Identifier (CE)  | LEFTQUALAPP^^IRIS  |  |
|   | OBX-3.1 Identifier  | LEFTQUALAPP   | Always "LEFTQUALAPP"; stands for LEFT eye image quality  |
|   | OBX-3.2 Text  |  | Empty by default  |
|  | OBX-3.3 Name of Coding System  | IRIS  | Always "IRIS"  |
| OBX-4  | Observation Sub-Id (ST)  | 9  | Sequential counter that matches the Set ID  |
| OBX-5  | Observation Value (Varies)  | Gradable Image   | Either “Gradable Image” or “Not Gradable Image” based on the image quality  |
| OBX-6  | Units (CE)  |   | Empty by default  |
| OBX-7  | References Range (ST)  |   | Empty by default  |
| OBX-8  | Abnormal Flags (IS)  |   | Empty by default  |
| OBX-9  | Probability (NM)  |   | Empty by default  |
| OBX-10  | Nature of Abnormal Test (ID)  |  | Empty by default  |
| OBX-11  | Observation Result Status (ID)  | F  |  |

## Tenth Through Second-to-Last OBX 

Sample OBX segment (default): 
```

OBX|10|FT|Result^^IRIS|001|Retinal Study Result for DOE, JOHN||||||F 
OBX|11|FT|Result^^IRIS|002|||||||F 
OBX|12|FT|Result^^IRIS|003|DOE, JOHN, a 58 y/o, M (DOB: 10-12-1958, MRN:ITCC20170410)||||||F 
OBX|28|FT|Result^^IRIS|019|This result was electronically signed by DOE, JANE, MD on 04-102017 09:59:02 UTC time.||||||F 
OBX|29|FT|Result^^IRIS|020|||||||F 
OBX|30|FT|Result^^IRIS|021|NOTE: Any pathology noted on this diabetic retinal evaluation should be confirmed by an appropriate ophthalmic examination.||||||F 
```
Secondary Option (Single OBX): Iris can send the text results can be sent in a single OBX segment 

Tertiary Option (NTE Segments): Iris can send the text results as NTE segments instead of OBX segments 


| Field  | Name and type  | Sample value  | Description  |
| -- | -- | -- | -- |
| OBX-1  | Set ID - OBX (SI)  | 10  | Increase sequentially by 1  |
| OBX-2  | Value Type (ID)  | FT  | Formatted Text, but can be defined differently like "ST" if  necessary  |
|  OBX-3  | Observation Identifier (CE)  | Result^^IRIS  |  |
|   | OBX-3.1 Identifier  | Result   | "Result" but can be defined with other value if necessary  |
|   | OBX-3.2 Text  |  | Usually be empty but can be defined with any value if necessary  |
|  | OBX-3.3 Name of Coding System  | IRIS  | “IRIS” is used as the default value  |
| OBX-4  | Observation Sub-Id (ST)  | 001  | Grading specific identifier; this number increases sequentially by 1 for each additional OBX segment  |
| OBX-5  | Observation Value (Varies)  |   | All the text from the Iris report will be displayed here on its own OBX line. Carriage returns will also receive their own OBX segment.  |
| -- | -- | -- | -- |
| OBX-6  | Units (CE)  |   | Empty by default  |
| OBX-7  | References Range (ST)  |   | Empty by default  |
| OBX-8  | Abnormal Flags (IS)  |   | Empty by default  |
| OBX-9  | Probability (NM)  |   | Empty by default  |
| OBX-10  | Nature of Abnormal Test (ID)  |  | Empty by default  |
| OBX-11  | Observation Result Status (ID)  | F  |  |


## Last OBX 
*Reference Pointer Option*

### Sample OBX segment: 
```
OBX|31|RP|LINK^^PDFLINK|31|https://api.retinalscreenings.com/api/PatientOrders/GetSingleResultForDisplayInEmr?patientOrderId=273013&asPdf=True&isPreliminary=False&auth=257805B4B262A18271B60A62026671703D0F3F335DC9E0643662358952E7DCBA19C1C2CCC6C781A3444D651C0AC6695750DA87C9A5CE0F5976E8A206D9FB1915||||||F 
```

| Field  | Name and type  | Sample value  | Description  |
| -- | -- | -- | -- |
| OBX-1  | Set ID - OBX (SI)  | 31  | Increase sequentially by 1  |
| OBX-2  | Value Type (ID)  | RP  | Reference Pointer (RP): used when a pointer URL is configured  |
| OBX-3  | Observation Identifier (CE)  |   |   |
|   | Reference Pointer (RP) Configuration  | LINK^^PDFLINK  | This is the default delivery method  |
|   | OBX-3.1 Identifier  | LINK  | "LINK" is the default value  |
|   | OBX-3.2 Text  |   | Empty by default  |
|   | OBX-3.3 Name of Coding System  | PDFLINK  | "PDFLINK" is used as the default value  |
| OBX-4  | Observation Sub-Id (ST)  | 31  | Sequential counter that corresponds with the Set ID  |
| OBX-5  | Observation Value (Varies)  |   | This is a link to the PDF stored in Iris  |
|   | OBX-5.1 Reference Pointer  | See Note 1.0 Below  | See Note 1.1 Below  |
| OBX-6  | Units (CE)  |   | Empty by default  |
| OBX-7  | References Range (ST)  |   | Empty by default  |
| OBX-8  | Abnormal Flags (IS)  |   | Empty by default  |
| OBX-9  | Probability (NM)  |   | Empty by default  |
| OBX-10  | Nature of Abnormal Test (ID)  |   | Empty by default  |
| OBX-11  | Observation Result Status (ID)  | F  |   |


Note 1.0: 

## Example URL: 

https://api.retinalscreenings.com/api/PatientOrders/GetSingleResultForDisplayInEmr?patientOrderId=12345&asPdf=True&isPreliminary=False&auth=xxxxx

## Note 1.1: 

IRIS will populate "&" as a value instead of HL7 standard value "\T\" for client. Upon request, IRIS can populate “\T\” instead of"8". Example: 

o "…?patientOrderId=273013\T\asPdf..." to "…?patientOrderId=273013&asPdf..." 

Patient MRN is displayed here: 

o patientOrderId=12345

Document type: 

o  aspdf=True

Document status (will always be set to False) 

o isPreliminary=False

Document pointer 

o  auth=xxxxx

## Sample OBX segment (Encapsulated Data):
```
OBX|27|ED|||PDF^TEXT^^Base64^[ Base64 Encoded PDF]||||||F 
```

| Field  | Name and type  | Sample value  | Description  |
| -- | -- | -- | -- |
| OBX-1  | Set ID - OBX (SI)  | 27  | Increase sequentially by 1  |
| OBX-2  | Value Type (ID)  | ED  | Encapsulated Data (ED): used when an encoded PDF is configured; this configuration can be used in addition to or in lieu of the RP configuration  |
| OBX-3  | Observation Identifier (CE)  |   | Empty by default  |
| OBX-4  | Observation Sub-Id (ST)  |   | Empty by default  |
| OBX-5  | Observation Value (Varies)  |   |   |
|   | Encapsulated Data (ED)  | PDF^TEXT^^Base64^[Base64 Encoded PDF]  |   |
|   | OBX-5.1 Source application  | PDF  | This is the document type  |
|   | OBX-5.2 Type of data  | TEXT  | “TEXT” is the default value  |
|   | OBX-5.3 Data subtype  |   | Empty by default  |
|   | OBX-5.4 Encoding  | Base64  | Always "Base64" which matches the encoding  |
|   | OBX-5.4 Data (ST)  | See Note 2.0 Below  | Actual PDF data using base64 encoding mechanism  |
| OBX-6  | Units (CE)  |   | Empty by default  |
| OBX-7  | References Range (ST)  |   | Empty by default  |
| OBX-8  | Abnormal Flags (IS)  |   | Empty by default  |
| OBX-9  | Probability (NM)  |   | Empty by default  |
| OBX-10  | Nature of Abnormal Test (ID)  |   | Empty by default  |
| OBX-11  | Observation Result Status (ID)  | F  | F = Final, C = Corrected*  |

