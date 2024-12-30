---
title: DFT (DFT-P03)
parent: HL7 Messages
nav_order: 3
---

<details markdown="block">
  <summary>
    Table of contents
  </summary>
  {: .text-delta }
- TOC
{:toc}
</details>

## Standard Charge (DFT-P03) Outbound Specifications
IRIS can push a single DFT message per order as a mechanism for dropping charges.

*We recommend dropping charges through your EMR/EHR Ambulatory workflow as a more reliable alternative to an interface driven DFT Message. Your EMR has more points of information regarding the patient encounter in which to make this determination.*

## Basic Interface Structure and Description

This document outlines the values sent in an HL7 charge message (DFT-P03) from IRIS to a third-party system. This third-party system could be another application, an interface engine, or an EMR. For the purposes of this documentation, this third-party will be referred to an EMR.

IRIS has two different structural setups for the FT1 segment. This will be described in detail later in that section. The last section of this document contains an example HL7 message.

The following sections contain details of the DFT message content by HL7 Segment.  

## MSH Segment – Message Header

The message header segment includes information that defines the structure of the message.

**Sample MSH segment:**

```
MSH|^~\&|IRIS|IRIS|VENDOR|VENDOR|20170410145907||ORU^R01|170410145907|T|2.4
```

| Field   | Name and type | Sample value  | Description  |
|:---------------|:---------------|:---------------|:---------------
| MSH-1 | Field Separator (ST) | \| | Auto generated
| MSH-2 | Encoding Characters (ST) | ^~\& | Auto generated
| MSH-3 | Sending Application (HD) | IRIS | “IRIS” is used as the default value
| MSH-4 | Sending Facility (HD) | IRIS | “IRIS” is used as the default value; can reflect the value sent in the corresponding ORM message if used to identify a parent organization
| MSH-5 | Receiving Application (HD) | VENDOR | The name of the EMR. This need to be pre-defined
| MSH-6 | Receiving Facility (HD) | VENDOR | The name or id of clinic. This need to be pre-defined.
| MSH-7 | Date/Time of Message (TS) | yyyyMMddHHmmss format, e.g. "20190410145907" | Auto generated based off server time (UTC if hosted by Iris)
| MSH-8 | Security (ST) |  | Empty
| MSH-9 | Message Type (MSG) | ORU^R01 | Unchanging
| MSH-10 | Message Control ID (ST) | 1.9041E+11 | Auto generated from server time (UTC if hosted by Iris)
| MSH-11 | Processing ID (PT) | T | P (Production) or T (Test) will be used based on the system environment
| MSH-12 | Version ID (VID) | 2.4 | HL7 Version


## EVN Segment – Event Type


The event type segment will include information that defines the type of action that is being sent by IRIS. 


**Sample EVN segment:**

```
EVN|P03|20181005090316
```

| Field   | Name and type | Sample value  | Description  |
|:---------------|:---------------|:---------------|:---------------
| EVN-1 | Event Type Code (ID) | P03 | Always "P03"
| EVN-2 | Recorded Date/Time (TS) | yyyyMMddHHmmss format | Current time based on server time (UTC if hosted by Iris)
| EVN-3 | Date/Time Planned Event (TS) |  | Empty by default
| EVN-4 | Event Reason Code (IS) |  | Empty by default
| EVN-5 | Operator ID (XCN) |  | Empty by default
| EVN-6 | Event Occurred (TS) |  | Empty by default
| EVN-7 | Event Facility (HD) |  | Empty by default


## PID Segment – Patient Identification

The patient identification segment will include patient-specific demographic information.

**Sample PID segment:**

```
PID||ITCC20170410^^^^MRN|ITCC20170410||DOE^JOHN||19581012|M||||||||||1234|111-22-3333
```

| Field   | Name and type | Sample value  | Description  |
|:---------------|:---------------|:---------------|:---------------
| PID-1 | Set ID - PID (SI) |  | Empty by default
| PID-2 | Patient ID (CX) | ITCC20170410^^^^MRN | 
|  | PID-2.1 ID | ITCC20170410 | Related Patient's MRN value
|  | …. |  | PID-2.2 through PID-2.4 empty by default
|  | PID-2.5 Identifier Type Code | MRN | Related Patient's ID type if requested
| PID-3 | Patient Identifier List (CX) | ITCC20170410 | Reflects the same value as PID-2.1 by default
| PID-4 | Alternate Patient ID - PID (CX) |  | Empty by default
| PID-5 | Patient Name (XPN) | DOE^JOHN | Related Patient's family name & given name
| PID-6 | Mother's Maiden Name (XPN) |  | Empty by default
| PID-7 | Date/Time of Birth (TS) | 19581012 | Related Patient's Date of birth; YYYYMMDD format
| PID-8 | Administrative Sex (IS) | M | Related patient's sex (M or F)
| PID-9 | Patient Alias (XPN) |  | Empty by default
| PID-10 | Race (CE) |  | Empty by default
| PID-11 | Patient Address (XAD) |  | Empty by default
| PID-12 | County Code (IS) |  | Empty by default
| PID-13 | Phone Number - Home (XTN) |  | Empty by default
| PID-14 | Phone Number - Business (XTN) |  | Empty by default
| PID-15 | Primary Language (CE) |  | Empty by default
| PID-16 | Marital Status (CE) |  | Empty by default
| PID-17 | Religion (CE) |  | Empty by default
| PID-18 | Patient Account Number (CX) | 1234 | Related Patient's CSN/Account value/Encounter number
| PID-19 | SSN Number - Patient (ST) | 111-22-3333 | IRIS does store this value and will not send this value


## PV1 Segment – Patient Visit

The patient visit segment includes patient-specific visit information.

**Sample PV1 segment:**

```
PV1|1|O|POC01||||GR0001^DOE^JANE^^^MD^MD^^^^^^NPI|OP0001^DOE^JACK^^^MD^MD^^^^^^NPI|||||||||GR0001^DOE^JANE^^^MD^MD^^^^^^NPI|||||||||||||||||||||||||||20170410145803|20170410145803
```

| Field   | Name and type | Sample value  | Description  |
|:---------------|:---------------|:---------------|:---------------
| PV1-1 | Set ID - PV1 (SI) | 1 | Always 1
| PV1-2 | Patient Class (IS) | O | Always "O" (Outpatient)
| PV1-3 | Assigned Patient Location (PL) | POC01 | Point of care information; received from the ORM HL7 message; received from the ORM HL7 message
| PV1-4 | Admission Type (IS) |  | Empty by default
| PV1-5 | Preadmit Number (CX) |  | Empty by default
| PV1-6 | Prior Patient Location (PL) |  | Empty by default
| PV1-7 | Attending Doctor (XCN) | OP0001^DOE^JACK^^
| ^MD^MD^^^^^^NPI | This reflects the ordering provider received in the ORM HL7 message
|  | PV1-7.1 ID | OP0001 | Reflects the ORM HL7 message ORC-12.1 value
|  | PV1-7.2 Family Name | DOE | Reflects the ORM HL7 message ORC-12.2 value
|  | PV1-7.3 Given Name | JANE | Reflects the ORM HL7 message ORC-12.3 value
|  | ….. |  | PV1-7.4 & PV1-7.5 empty by default
|  | PV1-7.5 Prefix | MD | Credentials of the ordering physician if available
|  | PV1-7.6 Degree | MD | Credentials of the ordering physician if available
|  | ….. |  | PV1-7.7 through PV1-7.12 Empty by default
|  | PV1-7.13 Identifier Type Code | NPI | The literal value of “NPI” is used by default
| PV1-8 | Referring Doctor (XCN) | OP0001^DOE^JACK^^
| ^MD^MD^^^^^^NPI | This reflects the ordering provider received in the ORM HL7 message
|  | PV1-8.1 ID | OP0001 | Reflects the ORM HL7 message ORC-12.1 value
|  | PV1-8.2 Family Name | DOE | Reflects the ORM HL7 message ORC-12.2 value
|  | PV1-8.3 Given Name | JACK | Reflects the ORM HL7 message ORC-12.3 value
|  | ….. |  | PV1-8.4 & PV1-8.5 empty by default
|  | PV1-8.5 Prefix | MD | Credentials of the ordering physician if available
|  | PV1-8.6 Degree | MD | Credentials of the ordering physician if available
|  | ….. |  | PV1-8.7 through PV1-8.12 Empty by default
|  | PV1-8.13 Identifier Type Code | NPI | The literal value of “NPI” is used by default
| PV1-10 | Hospital Service (IS) |  | Empty by default
| PV1-11 | Temporary Location (PL) |  | Empty by default
| PV1-12 | Preadmit Test Indicator (IS) |  | Empty by default
| PV1-13 | Re-admission Indicator (IS) |  | Empty by default
| PV1-14 | Admit Source (IS) |  | Empty by default
| PV1-15 | Ambulatory Status (IS) |  | Empty by default
| PV1-16 | VIP Indicator (IS) |  | Empty by default
| PV1-17 | Admitting Doctor (XCN) | OP0001^DOE^JACK^^
| ^MD^MD^^^^^^NPI | This reflects the ordering provider received in the ORM HL7 message
|  | PV1-17.1 ID | OP0001 | Reflects the ORM HL7 message ORC-12.1 value
|  | PV1-17.2 Family Name | DOE | Reflects the ORM HL7 message ORC-12.2 value
|  | PV1-17.3 Given Name | JANE | Reflects the ORM HL7 message ORC-12.3 value
|  | ….. |  | PV1-17.4 & PV1-17.5 empty by default
|  | PV1-17.5 Prefix | MD | Credentials of the ordering physician if available
|  | PV1-17.6 Degree | MD | Credentials of the ordering physician if available
|  | ….. |  | PV1-17.7 through PV1-17.12 Empty by default
|  | PV1-17.13 Identifier Type Code | NPI | The literal value of “NPI” is used by default
| PV1-18 | Patient Type (IS) |  | Empty by default
| PV1-19 | Visit Number (CX) |  | Related Patient's CSN/Account value/Encounter number
| PV1-20 | Financial Class (FC) |  | Empty by default
| PV1-21 | Charge Price Indicator (IS) |  | Empty by default
| PV1-22 | Courtesy Code (IS) |  | Empty by default
| PV1-23 | Credit Rating (IS) |  | Empty by default
| PV1-24 | Contract Code (IS) |  | Empty by default
| PV1-25 | Contract Effective Date (DT) |  | Empty by default
| PV1-26 | Contract Amount (NM) |  | Empty by default
| PV1-27 | Contract Period (NM) |  | Empty by default
| PV1-28 | Interest Code (IS) |  | Empty by default
| PV1-29 | Transfer to Bad Debt Code (IS) |  | Empty by default
| PV1-30 | Transfer to Bad Debt Date (DT) |  | Empty by default
| PV1-31 | Bad Debt Agency Code (IS) |  | Empty by default
| PV1-32 | Bad Debt Transfer Amount (NM) |  | Empty by default
| PV1-33 | Bad Debt Recovery Amount (NM) |  | Empty by default
| PV1-34 | Delete Account Indicator (IS) |  | Empty by default
| PV1-35 | Delete Account Date (DT) |  | Empty by default
| PV1-36 | Discharge Disposition (IS) |  | Empty by default
| PV1-37 | Discharged to Location (DLD) |  | Empty by default
| PV1-38 | Diet Type (CE) |  | Empty by default
| PV1-39 | Servicing Facility (IS) |  | Empty by default
| PV1-40 | Bed Status (IS) |  | Empty by default
| PV1-41 | Account Status (IS) |  | Empty by default
| PV1-42 | Pending Location (PL) |  | Empty by default
| PV1-43 | Prior Temporary Location (PL) |  | Empty by default
| PV1-44 | Admit Date/Time (TS) | yyyyMMddHHmmss format | Date of image captured
| PV1-45 | Discharge Date/Time (TS) | yyyyMMddHHmmss format | Date of image captured
| PV1-46 | Current Patient Balance (NM) |  | Empty by default
| PV1-47 | Total Charges (NM) |  | Empty by default
| PV1-48 | Total Adjustments (NM) |  | Empty by default
| PV1-49 | Total Payments (NM) |  | Empty by default
| PV1-50 | Alternate Visit ID (CX) |  | Empty by default
| PV1-51 | Visit Indicator (IS) |  | Empty by default
| PV1-52 | Other Healthcare Provider (XCN) |  | Empty by default

# FT1 (Option 1) – Financial Transaction

The financial transaction segment contains the detailed data necessary to post charges, payments, adjustments, etc. to patient accounting records. IRIS has the capabilities of sending the FT1 segment by two different means. For the FT1 (Option 1) segment, IRIS sends professional charges (charging for the professional readers alone). There is an additional option for this ‘FT1 (Option 1)’ where IRIS can send an additional FT1 segment containing CPT II. For the FT1 (Option 2) segments, IRIS sends both the professional and technical charges in the HL7 message.


## FT1 (Option 1) – CPT II Optional Extra FT1 segment

This extra FT1 segment is CPT II data for the patient over 18 at the time of result and has normal result (Diabetic Retinopathy is None). This extra FT1 segment will only be sent upon demand.
 
**Example FT1 segment (CPT II):**

```
FT1|2||273013|20170410145803|20170410173627|CG|3072F^No evidence of retinopathy in the prior year||ITCC20170410|1|||POC01||IRIS|POC01|||E11.41^Type 2 diabetes mellitus with diabetic mononeuropathy^ICD-10-CM~E11.3592^Type 2 diabetes mellitus with proliferative diabetic retinopathy without macular edema, left eye^ICD-10-CM~H35.81^Retinal edema^ICD-10-CM|GR0001^DOE^JANE^^^MD^MD^^^^^^NPI|OP0001^DOE^JACK^^^MD^MD^^^^^^NPI||2017041006^EPIC||3072F^No evidence of retinopathy in the prior year
```


| Field   | Name and type | Sample value  | Description  |
|:---------------|:---------------|:---------------|:---------------
| FT1-1 | Set ID - FT1 (SI) | 2 | Always “2"
| FT1-2 | Transaction ID (ST) |  | Empty by default
| FT1-3 | Transaction Batch ID (ST) | 273013 | Iris’ internal order number. This number is unique value.
| FT1-4 | Transaction Date (TS) | yyyyMMddHHmmss format | Date of image capture
| FT1-5 | Transaction Posting Date (TS) | yyyyMMddHHmmss format | Current time based on server time (UTC if hosted by Iris)
| FT1-6 | Transaction Type (IS) | CG | Always "CG" (Charge)
| FT1-7 | Transaction Code (CE) | 3072F^No evidence of retinopathy in the prior year | This is the main difference from above FT1 segment*
| 
|  | FT1-7.1 Identifier | 3072F | CPT2 code; fixed value
|  | FT1-7.2 Text | No evidence of retinopathy in the prior year | CPT2 description; fixed value
|  | FT1-7.3 Name of Coding System |  | Empty by default
| FT1-8 | Transaction Description (ST) |  | Empty by default
| FT1-9 | Transaction Description - Alt (ST) | ITCC20170410 | Patient's MRN
| FT1-10 | Transaction Quantity (NM) | 1 | Always "1"
| FT1-11 | Transaction Amount - Extended (CP) |  | Empty by default
| FT1-12 | Transaction Amount - Unit (CP) |  | Empty by default
| FT1-13 | Department Code (CE) | POC01 | Point of care information; received from the ORM HL7 message; received from the ORM HL7 message
| FT1-14 | Insurance Plan ID (CE) |  | Empty by default
| FT1-15 | Insurance Amount (CP) | IRIS | “IRIS” is used as the default
| FT1-16 | Assigned Patient Location (PL) | POC01 | Point of care information; received from the ORM HL7 message
| FT1-17 | Fee Schedule (IS) |  | Empty by default
| FT1-18 | Patient Type (IS) |  | Empty by default
| FT1-19 | Diagnosis Code - FT1 (CE) | E11.41^Type 2 diabetes mellitus with diabetic mononeuropathy^ICD-10-CM~E11.3592^Type 2 diabetes mellitus with proliferative diabetic retinopathy without macular edema, left eye^ICD-10-CM~H35.81^Retinal edema^ICD-10-CM | This is populated based on the diagnoses found upon grading; configured as a repeatable field separated by “~”. Note: Iris only sends diagnoses related to the current patient visit.
|  | FT1-19.1 Identifier | E11.41 | [Diagnosis code in ICD 10 representation](/docs/integration/DFT_Results/Most_Common_Diagnoses.md)| 
|  | FT1-19.2 Text | Type 2 diabetes mellitus with diabetic mononeuropathy | Description of diagnosis code
|  | FT1-19.3 Name of Coding System | ICD-10-CM | The coding system; Iris is currently using ICD10
| FT1-20 | Performed by Code (XCN) | GR0001^DOE^JANE^^
| ^MD^MD^^^^^^NPI | This is an Interpreter (Grader, i.e. Signing user)
|  | FT1-20.1 ID | GR0001 | Interpreter ID in IRIS
|  | FT1-20.2 Family Name | DOE | Interpreter Family Name
|  | FT1-20.3 Given Name | JANE | Interpreter Given Name
|  | ….. |  | FT1-20.4 & FT1-20.5 Empty by default
|  | FT1-20.5 Prefix | MD | Prefix of the Interpreter if exists
|  | FT1-20.6 Degree | MD | Degree of the Interpreter if exists
|  | ….. |  | FT1-20.7 through FT1-20.12 Empty by default
|  | FT1-20.13 Identifier Type Code | NPI or NPI | Same as ORU-R01's ORC-12.13
| FT1-21 | Ordered By Code (XCN) | OP0001^DOE^JACK^^
| ^MD^MD^^^^^^NPI | This is Ordering Physician. See ORM's ORC-12
|  | FT1-21.1 ID | OP0001 | Same as ORU-R01's ORC-12.1
|  | FT1-21.2 Family Name | DOE | Same as ORU-R01's ORC-12.2
|  | FT1-21.3 Given Name | JACK | Same as ORU-R01's ORC-12.3
|  | ….. |  | FT1-21.4 & FT1-21.5 Empty by default
|  | FT1-21.5 Prefix | MD | Prefix of the Ordering Physician if exists
|  | FT1-21.6 Degree | MD | Degree of the Ordering Physician if exists
|  | ….. |  | FT1-21.7 through FT1-21.12 Empty by default
|  | FT1-21.13 Identifier Type Code | NPI or NPI | Same as ORU-R01's ORC-12.13
| FT1-22 | Unit Cost (CP) |  | Optional. May populate with what client want, otherwise empty
| FT1-23 | Filler Order Number (EI) | 2017041006^EPIC | Optional. Internal order number in EMR
|  | FT1-23.1 Entity Identifier | 2017041006 | Internal order number in EMR
|  | FT1-23.2 namespace ID | EPIC | Optional. Can be a predefined value or empty
| FT1-24 | Entered by Code (XCN) |  | Empty by default
| FT1-25 | Procedure Code (CE) | 3072F^No evidence of retinopathy in the prior year | This is the main difference from above FT1 segment
|  | FT1-25.1 Identifier | 3072F | CPT2 code. This is fixed value
|  | FT1-25.2 Text | No evidence of retinopathy in the prior year | CPT2 description. This is fixed value
|  | FT1-25.3 Name of Coding System |  | Empty by default
| FT1-26 | Procedure Code Modifier (CE) | Null, NC | Empty unless not charging for “Ungradable” exams. In such cases, the modifier “NC” can be sent.


## FT1 (Option 1) – Professional Charge

**Sample FT1 segment (Professional Charge):**

```
FT1|1||273013|20170410145901|20170410151351|CG|92250^Fundus photography with interpretation and report^CPT||ITCC20170410|1|||POC01||IRIS|POC01|||E11.41^Type 2 diabetes mellitus with diabetic mononeuropathy^ICD-10-CM~E11.3592^Type 2 diabetes mellitus with proliferative diabetic retinopathy without macular edema, left eye^ICD-10-CM~H35.81^Retinal edema^ICD-10-CM|GR0001^DOE^JANE^^^MD^MD^^^^^^NPI|OP0001^DOE^JACK^^^MD^MD^^^^^^NPI||2017041006^EPIC||92250^Fundus photography with interpretation and report^CPT
```

| Field   | Name and type | Sample value  | Description  |
|:---------------|:---------------|:---------------|:---------------
| FT1-1 | Set ID - FT1 (SI) | 1 | Always "1"
| FT1-2 | Transaction ID (ST) |  | Empty by default
| FT1-3 | Transaction Batch ID (ST) | 273013 | Iris’ internal order number. This number is unique value.
| FT1-4 | Transaction Date (TS) | yyyyMMddHHmmss format | Date of grading (signing)
| FT1-5 | Transaction Posting Date (TS) | yyyyMMddHHmmss format | Current time based on server time (UTC if hosted by Iris)
| FT1-6 | Transaction Type (IS) | CG | Always "CG" (Charge)
| FT1-7 | Transaction Code (CE) | 92250^Fundus photography with interpretation and report^CPT | CPT code followed by the OBR.4 fields from the ORM message
|  | FT1-7.1 Identifier | 92250 | CPT code
|  | FT1-7.2 Text | Fundus photography with interpretation and report | CPT description
|  | FT1-7.3 Name of Coding System | CPT | Always "CPT"
| FT1-8 | Transaction Description (ST) |  | Empty by default
| FT1-9 | Transaction Description - Alt (ST) | ITCC20170410 | Related Patient's MRN value
| FT1-10 | Transaction Quantity (NM) | 1 | Always "1"
| FT1-11 | Transaction Amount - Extended (CP) |  | Empty by default
| FT1-12 | Transaction Amount - Unit (CP) |  | Empty by default
| FT1-13 | Department Code (CE) | POC01 | Point of care information; received from the ORM HL7 message; received from the ORM HL7 message
| FT1-14 | Insurance Plan ID (CE) |  | Empty by default
| FT1-15 | Insurance Amount (CP) | IRIS | “IRIS” is used as the default value
| FT1-16 | Assigned Patient Location (PL) | POC01 | Point of care information; received from the ORM HL7 message
| FT1-17 | Fee Schedule (IS) |  | Empty by default
| FT1-18 | Patient Type (IS) |  | Empty by default
| FT1-19 | Diagnosis Code - FT1 (CE) | E11.41^Type 2 diabetes mellitus with diabetic mononeuropathy^ICD-10-CM~E11.3592^Type 2 diabetes mellitus with proliferative diabetic retinopathy without macular edema, left eye^ICD-10-CM~H35.81^Retinal edema^ICD-10-CM | This is populated based on the diagnoses found upon grading; configured as a repeatable field separated by “~”
|  | FT1-19.1 Identifier | E11.41 | [Diagnosis code in ICD 10 representation](/docs/integration/DFT_Results/Most_Common_Diagnoses.md)
|  | FT1-19.2 Text | Type 2 diabetes mellitus with diabetic mononeuropathy | Description of diagnosis code
|  | FT1-19.3 Name of Coding System | ICD-10-CM | The coding system; Iris is currently using ICD10
| FT1-20 | Performed by Code (XCN) | GR0001^DOE^JANE^^
| ^MD^MD^^^^^^NPI | This is an interpreter (Grader, i.e. Signing user)
|  | FT1-20.1 ID | GR0001 | Interpreter ID in IRIS
|  | FT1-20.2 Family Name | DOE | Interpreter Family Name
|  | FT1-20.3 Given Name | JANE | Interpreter Given Name
|  | ….. |  | FT1-20.4 & FT1-20.5 are empty by default
|  | FT1-20.5 Prefix | MD | Prefix of the Interpreter if exists
|  | FT1-20.6 Degree | MD | Degree of the Interpreter if exists
|  | ….. |  | FT1-20.7 through FT1-20.12 empty by default
|  | FT1-20.13 Identifier Type Code | NPI or NPI | Same as ORU-R01's ORC-12.13
| FT1-21 | Ordered By Code (XCN) | OP0001^DOE^JACK^^
| ^MD^MD^^^^^^NPI | This is Ordering Physician. See ORM's ORC-12
|  | FT1-21.1 ID | OP0001 | Same as ORU-R01's ORC-12.1
|  | FT1-21.2 Family Name | DOE | Same as ORU-R01's ORC-12.2
|  | FT1-21.3 Given Name | JACK | Same as ORU-R01's ORC-12.3
|  | ….. |  | FT1-21.4 & FT1-21.5 Empty by default
|  | FT1-21.5 Prefix | MD | Prefix of the Ordering Physician if exists
|  | FT1-21.6 Degree | MD | Degree of the Ordering Physician if exists
|  | ….. |  | FT1-21.7 through FT1-21.12 empty by default
|  | FT1-21.13 Identifier Type Code | NPI or NPI | Same as ORU-R01's ORC-12.13
| FT1-22 | Unit Cost (CP) |  | Empty by default
| FT1-23 | Filler Order Number (EI) | 2017041006^EPIC | 
|  | FT1-23.1 Entity Identifier | 2017041006 | Order number from ORM HL7 message
|  | FT1-23.2 namespace ID | EPIC | Receiving application from MSH segment
| FT1-24 | Entered by Code (XCN) |  | Empty by default
| FT1-25 | Procedure Code (CE) | 92250^Fundus photography with interpretation and report^CPT | 
|  | FT1-25.1 Identifier | 92250 | CPT code
|  | FT1-25.2 Text | Fundus photography with interpretation and report | CPT description. Can be redefined with other values
|  | FT1-25.3 Name of Coding System | CPT | Always "CPT"
| FT1-26 | Procedure Code Modifier (CE) | Null, NC | Empty unless not charging for “Ungradable” exams. In such cases, the modifier “NC” can be sent.


# FT1 (Option 2) – Financial Transaction

The financial transaction segment contains the detailed data necessary to post charges, payments, adjustments, etc. to patient accounting records. IRIS has the capabilities of sending the FT1 segment by two different means. For the FT1 (Option 1) segment, IRIS sends professional charges (charging for the professional readers alone). For the FT1 (Option 2) segment, IRIS sends both the professional and technical charges in the HL7 message.

## FT1 (Option 2) – Professional Charge

**Sample FT1 segment (Professional Charge):**

```
FT1|1||273013|20170410145901|20170410151630|CG|92250^Fundus photography with interpretation and report^CPT||ITCC20170410|1|||POC01||IRIS|POC01|||E11.41^Type 2 diabetes mellitus with diabetic mononeuropathy^ICD-10-CM~E11.3592^Type 2 diabetes mellitus with proliferative diabetic retinopathy without macular edema, left eye^ICD-10-CM~H35.81^Retinal edema^ICD-10-CM|GR0001^DOE^JANE^^^MD^MD^^^^^^NPI|OP0001^DOE^JACK^^^MD^MD^^^^^^NPI||2017041006||92250^Fundus photography with interpretation and report^CPT|26
```

| Field   | Name and type | Sample value  | Description  |
|:---------------|:---------------|:---------------|:---------------
| FT1-1 | Set ID - FT1 (SI) | 1 | Always "1"
| FT1-2 | Transaction ID (ST) |  | Empty by default
| FT1-3 | Transaction Batch ID (ST) | 273013 | Iris’ internal order number. This number is unique value.
| FT1-4 | Transaction Date (TS) | yyyyMMddHHmmss format | Date of grading(signing)
| FT1-5 | Transaction Posting Date (TS) | yyyyMMddHHmmss format | Current time based on server time (UTC if hosted by Iris)
| FT1-6 | Transaction Type (IS) | CG | Always "CG" (Charge)
| FT1-7 | Transaction Code (CE) |  | CPT code. Customizable with following possible values
|  |  | 92250^Fundus photography with interpretation and report^CPT | Sample
| FT1-8 | Transaction Description (ST) |  | Empty by default
| FT1-9 | Transaction Description - Alt (ST) | ITCC20170410 | Patient's MRN
| FT1-10 | Transaction Quantity (NM) | 1 | Always "1"
| FT1-11 | Transaction Amount - Extended (CP) |  | Empty by default
| FT1-12 | Transaction Amount - Unit (CP) |  | Empty by default
| FT1-13 | Department Code (CE) | POC01 | Point of care information; received from the ORM HL7 message
| FT1-14 | Insurance Plan ID (CE) |  | Empty by default
| FT1-15 | Insurance Amount (CP) | IRIS | “IRIS” is used as the default
| FT1-16 | Assigned Patient Location (PL) | POC01 | Point of care information; received from the ORM HL7 message
| FT1-17 | Fee Schedule (IS) |  | Empty by default
| FT1-18 | Patient Type (IS) |  | Empty by default
| FT1-19 | Diagnosis Code - FT1 (CE) | E11.41^Type 2 diabetes mellitus with diabetic mononeuropathy^ICD-10-CM~E11.3592^Type 2 diabetes mellitus with proliferative diabetic retinopathy without macular edema, left eye^ICD-10-CM~H35.81^Retinal edema^ICD-10-CM | This is populated based on the diagnoses found upon grading; configured as a repeatable field separated by “~”. Note: Iris only sends diagnoses related to the current patient visit.
|  | FT1-19.1 Identifier | E11.41 | [Diagnosis code in ICD 10 representation](/docs/integration/DFT_Results/Most_Common_Diagnoses.md)
|  | FT1-19.2 Text | Type 2 diabetes mellitus with diabetic mononeuropathy | Description of diagnosis code
|  | FT1-19.3 Name of Coding System | ICD-10-CM | The coding system; Iris is currently using ICD10
| FT1-20 | Performed by Code (XCN) |  | This is an Interpreter (Grader, i.e. Signing user)
|  | FT1-20.1 ID | GR0001 | Interpreter ID in IRIS
|  | FT1-20.2 Family Name | DOE | Interpreter Family Name
|  | FT1-20.3 Given Name | JANE | Interpreter Given Name
|  | ….. |  | FT1-20.4 & FT1-20.5 Empty by default
|  | FT1-20.5 Prefix | MD | Prefix of the Interpreter if exists
|  | FT1-20.6 Degree | MD | Degree of the Interpreter if exists
|  | ….. |  | FT1-20.7 through FT1-20.12 Empty by default
|  | FT1-20.13 Identifier Type Code | NPI or NPI | Same as ORU-R01's ORC-12.13
| FT1-21 | Ordered by Code (XCN) |  | This is Ordering Physician. See ORM's ORC-12
|  | FT1-21.1 ID | OP0001 | Same as ORU-R01's ORC-12.1
|  | FT1-21.2 Family Name | DOE | Same as ORU-R01's ORC-12.2
|  | FT1-21.3 Given Name | JACK | Same as ORU-R01's ORC-12.3
|  | ….. |  | FT1-21.4 & FT1-21.5 Empty by default
|  | FT1-21.5 Prefix | MD | Prefix of the Ordering Physician if exists
|  | FT1-21.6 Degree | MD | Degree of the Ordering Physician if exists
|  | ….. |  | FT1-21.7 through FT1-21.12 Empty by default
|  | FT1-21.13 Identifier Type Code | NPI or NPI | Same as ORU-R01's ORC-12.13
| FT1-22 | Unit Cost (CP) |  | Optional. May populate with what client want, otherwise empty
| FT1-23 | Filler Order Number (EI) | 2017041006 | Optional. Internal order number in EMR
| FT1-24 | Entered by Code (XCN) |  | Empty by default
| FT1-25 | Procedure Code (CE) |  | CPT code. Customizable with following possible values
|  |  | 92250^Fundus photography with interpretation and report^CPT | Sample 1. Could be used as a modifier
| FT1-26 | Procedure Code Modifier (CE) |  | Professional charge modifier (26). See below charge samples and matrix
|  |  | 26 | Sample 1: Chargeable
|  |  | 26~NC | Sample 2: Not Chargeable
|  |  | 26~52 | Sample 3: Chargeable
|  |  | (empty) | Sample 4: Chargeable. Identified by FT1.25 if 26 is not used
|  |  | NC | *Sample 5: Not Chargeable. Identified by FT1.25 if 26 is not used
|  |  | 52 | *Sample 6: Chargeable. Identified by FT1.25 if 26 is not used

*Basic NC and 52: NC will be used if ALL uploaded images are not gradable. 52 will be used if ONE of uploaded images is not gradable


## FT1 (Option 2) – Technical Charge

**Sample FT1 segment (Technical Charge):**

```
FT1|2||273013|20170410145803|20170410151630|CG|92000035^OPHTHALMOSCOPY W/ FUNDUS PHOTO||ITCC20170410|1|||POC01||IRIS|POC01|||E11.41^Type 2 diabetes mellitus with diabetic mononeuropathy^ICD-10-CM~E11.3592^Type 2 diabetes mellitus with proliferative diabetic retinopathy without macular edema, left eye^ICD-10-CM~H35.81^Retinal edema^ICD-10-CM|GR0001^DOE^JANE^^^MD^MD^^^^^^NPI|OP0001^DOE^JACK^^^MD^MD^^^^^^NPI||2017041006||92000035^OPHTHALMOSCOPY W/ FUNDUS PHOTO|TC
```


| Field   | Name and type | Sample value  | Description  |
|:---------------|:---------------|:---------------|:---------------
| FT1-1 | Set ID - FT1 (SI) | 2 | Always be "2"
| FT1-2 | Transaction ID (ST) |  | Empty by default
| FT1-3 | Transaction Batch ID (ST) | 273013 | Iris’ internal order number. This number is unique value.
| FT1-4 | Transaction Date (TS) | yyyyMMddHHmmss format | Date of image captured
| FT1-5 | Transaction Posting Date (TS) | yyyyMMddHHmmss format | Current time based on server time (UTC if hosted by Iris)
| FT1-6 | Transaction Type (IS) | CG | Always "CG" (Charge)
| FT1-7 | Transaction Code (CE) |  | CPT code. Customizable with following possible values
|  |  | 92000035^OPHTHALMOSCOPY W/ FUNDUS PHOTO | Sample
| FT1-8 | Transaction Description (ST) |  | Empty by default
| FT1-9 | Transaction Description - Alt (ST) | ITCC20170410 | Patient's MRN
| FT1-10 | Transaction Quantity (NM) | 1 | Always be "1"
| FT1-11 | Transaction Amount - Extended (CP) |  | Empty by default
| FT1-12 | Transaction Amount - Unit (CP) |  | Empty by default
| FT1-13 | Department Code (CE) | POC01 | Point of care information; received from the ORM HL7 message
| FT1-14 | Insurance Plan ID (CE) |  | Empty by default
| FT1-15 | Insurance Amount (CP) | IRIS | “IRIS” is used as the default
| FT1-16 | Assigned Patient Location (PL) | POC01 | Point of care information; received from the ORM HL7 message
| FT1-17 | Fee Schedule (IS) |  | Empty by default
| FT1-18 | Patient Type (IS) |  | Empty by default
| FT1-19 | Diagnosis Code - FT1 (CE) | E11.41^Type 2 diabetes mellitus with diabetic mononeuropathy^ICD-10-CM~E11.3592^Type 2 diabetes mellitus with proliferative diabetic retinopathy without macular edema, left eye^ICD-10-CM~H35.81^Retinal edema^ICD-10-CM | This is populated based on the diagnoses found upon grading; configured as a repeatable field separated by “~”. Note: Iris only sends diagnoses related to the current patient visit.
|  | FT1-19.1 Identifier | E11.41 | [Diagnosis code in ICD 10 representation](/docs/integration/DFT_Results/Most_Common_Diagnoses.md)
|  | FT1-19.2 Text | Type 2 diabetes mellitus with diabetic mononeuropathy | Description of diagnosis code
|  | FT1-19.3 Name of Coding System | ICD-10-CM | The coding system; Iris is currently using ICD10
| FT1-20 | Performed by Code (XCN) |  | This is an Interpreter (Grader, i.e. Signing user)
|  | FT1-20.1 ID | GR0001 | Interpreter ID in IRIS
|  | FT1-20.2 Family Name | DOE | Interpreter Family Name
|  | FT1-20.3 Given Name | JANE | Interpreter Given Name
|  | ….. |  | FT1-20.4 & FT1-20.5 Empty by default
|  | FT1-20.5 Prefix | MD | Prefix of the Interpreter if exists
|  | FT1-20.6 Degree | MD | Degree of the Interpreter if exists
|  | ….. |  | FT1-20.7 through FT1-20.12 Empty by default
|  | FT1-20.13 Identifier Type Code | NPI or NPI | Same as ORU-R01's ORC-12.13
| FT1-21 | Ordered By Code (XCN) |  | This is Ordering Physician. See ORM's ORC-12
|  | FT1-21.1 ID | OP0001 | Same as ORU-R01's ORC-12.1
|  | FT1-21.2 Family Name | DOE | Same as ORU-R01's ORC-12.2
|  | FT1-21.3 Given Name | JACK | Same as ORU-R01's ORC-12.3
|  | ….. |  | FT1-21.4 & FT1-21.5 Empty by default
|  | FT1-21.5 Prefix | MD | Prefix of the Ordering Physician if exists
|  | FT1-21.6 Degree | MD | Degree of the Ordering Physician if exists
|  | ….. |  | FT1-21.7 through FT1-21.12 Empty by default
|  | FT1-21.13 Identifier Type Code | NPI or NPI | Same as ORU-R01's ORC-12.13
| FT1-22 | Unit Cost (CP) |  | Optional. Customized value with IRIS order number
| FT1-23 | Filler Order Number (EI) | 2017041006 | Optional. Internal order number in EMR
| FT1-24 | Entered by Code (XCN) |  | Empty by default
| FT1-25 | Procedure Code (CE) |  | CPT code. Customizable with following possible values
|  |  | 92000035^OPHTHALMOSCOPY W/ FUNDUS PHOTO | Sample 1. Could be used as a modifier
| FT1-26 | Procedure Code Modifier (CE) |  | Technical charge modifier (TC). See below charge samples and matrix
|  |  | TC | Sample 1: Chargeable
|  |  | TC~NC | Sample 2: Not Chargeable
|  |  | TC~52 | Sample 3: Chargeable
|  |  | (empty) | Sample 4: Chargeable. Identified by FT1.25 if TC is not used
|  |  | NC | *Sample 5: Not Chargeable. Identified by FT1.25 if TC is not used
|  |  | 52 | *Sample 6: Chargeable. Identified by FT1.25 if TC is not used

*Basic NC and 52: NC will be used if ALL uploaded images are not gradable. 52 will be used if ONE of uploaded images is not gradable

