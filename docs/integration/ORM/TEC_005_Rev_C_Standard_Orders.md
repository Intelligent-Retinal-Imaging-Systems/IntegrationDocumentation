---
title: ORM (ORM-001) 
parent: HL7 Messages
nav_order: 1
---

## Standard Orders (ORM-001) Inbound Specifications

Interface content encoding from HL7 Integration Engines submitted to IRIS v3.x  

<details markdown="block">
  <summary>
    Table of contents
  </summary>
  {: .text-delta }
- TOC
{:toc}
</details>

## Basic Interface Structure and Description

This document outlines the values sent in an HL7 order message (ORM-O01) from IRIS to a third-party system. This third-party system could be another application, an interface engine, or an EMR. For the purposes of this documentation, this third-party will be referred to an EMR. 

IRIS uses HL7 v2.4 as a main protocol for message sharing. If there are any fields represented in this document that are not populated but required by a receiving EMR, IRIS will populate these value(s) as requested. If the receiving EMR requires a different version, IRIS can provide messages for the corresponding version. If the EMR expects messages to be delivered in a format other than HL7, this will need to be discussed with an IRIS Interface Engineer as this will not be covered in the scope of this document – please contact IRIS support for more information. 

Following this section, the rest of the document will be divided by HL7 segment types as they would appear in a delivered HL7 message. Throughout the document will refer to the ‘client’ which will correspond with the facility, clinic, hospital, or medical center. The required fields will be notated in red and special notes will be in blue. Specific details will be provided in each section of this document. 


## MSH Segment – Message Header 

The message header segment includes information that defines the structure of the message.Please note that required fields will be notated in red and special notes will be in blue. 

### Sample MSH segment: 
```
MSH|^\~\&|EPIC|ANCL||IRIS|20170410102836|HJ123|ORM^O01|254|T|2.4||||||||
```

| Field  | Name and type  | Sample value  | Description  |
| -- | -- | -- | -- |
| MSH-1  | Field Separator (ST)  | |  | Auto generate  |
| MSH-2  | Encoding Characters (ST)  | ^\~\&  | Auto generate  |
| MSH-3  | Sending Application (HD)  | Your app name, e.g. "EPIC"  | Populated by EMR  |
| MSH-4  | Sending Facility (HD)  | Your facility name, e.g. "ANCL"  | Populated by EMR; This field canalso be used to identify parent entities for the case of the sending body serving as a hub for multiple facilities. See Note 1.0 below  |
| MSH-5  | Receiving Application (HD)  |   | Optional  |
| MSH-6  | Receiving Facility (HD)  | IRIS  | Optional  |
| MSH-7  | Date/Time Of Message (TS)  |   | Auto generate  |
| MSH-8  | Security (ST)  | Security value, e.g. initials of signer "HJ123"  | Optional See ORC-10.1  |
| MSH-9  | Message Type (MSG)  | ORM^O01  | Auto generate. If required, set as "ORM^O01^ORM_O01"  |
| MSH-10  | Message Control ID (ST)  | 252  | Auto generate  |
| MSH-11  | Processing ID (PT)  | P (Production) or T(Test)  | Required  |
| MSH-12  | Version ID (VID)  | Your system's HL7 version, e.g. "2.4"  | IRIS will send the results with this version  |


Note 1.0: If this is to be utilized, a crosswalk will need to be discussed during implementation and will therefore make this field required. 


## PID Segment – Patient Identification 

The patient identification segment will include patient-specific demographic information. Please note that required fields will be notated in red and special notes will be in blue. 

### Sample PID segment: 

```
PID|1|ITCC20170410^^^^MRN|ITCC20170410||DOE^JOHN||19581012|M||W|100 FOAMY WAY^APT A^BELLEVUE^WA^98104^US^^^KING|KING|(425)4445555^^PH^^^425^4445555|||M||1234|111-22-3333|||
```

| Field  | Name and type  | Sample value  | Description  |
| -- | -- | -- | -- |
| PID-1  | Set ID - PID (SI)  | 1  | Optional  |
| PID-2  | Patient ID (CX)  | ITCC20170410^^^^MRN  | Can repeat separated by "\~" like T1234^^^ ^MRN\~M001^^^CHMRN^CHMRN |
|   | PID-2.1 (ID)  | MRN value, e.g. "ITCC20170410"  | Required  |
|   | PID-2.2  |   | Not necessary  |
|   | PID-2.3  |   | Not necessary  |
|   | PID-2.4  |   | Not necessary  |
|   | PID-2.5 (Identifier Type Code) (ID)  | MRN  | Required if the field repeats. Client must provide which one to use. PID.3.1 will be picked accordingly, e.g. MRN in this example.  |
| PID-3  | Patient Identifier List (CX)  |   | If client uses this field for MRN, please notify IRIS. See PID.2 for detail  |
| PID-4  | Alternate Patient ID - PID (CX)  |   | Not necessary  |
| PID-5  | Patient Name (XPN)  | DOE^JOHN  | Required  |
|   | PID-5.1  | DOE  | Last name  |
|   | PID-5.2  | JOHN  | First name  |
| PID-6  | Mother's Maiden Name (XPN)  |   | Not necessary  |
| PID-7  | Date/Time of Birth (TS)  | YYYYMMDD format e.g. "19581012"  | Required  |
| PID-8  | Administrative Sex (IS)  | M or F  | Required  |
| PID-18  | Patient Account Number (CX)  | 1234  | Optional CSN/Account value/Encounter Number  |
| PID-19  | SSN Number - Patient (ST)  | e.g. 111-22-3333  | Iris does not store SSN  |


[(back to Table of Contents)](#table-of-contents)

 
## PV1 Segment – Patient Visit 

The patient visit segment includes patient-specific visit information. IRIS uses the PV1 segment to distinguish which clinic the patient will visit. Please note that required fields will be notated in red and special notes will be in blue. 

### Sample PV1 segment: 
```
PV1||O|POC01|||||||||||||||||||||||||||||||||||||||||20170410082742|||||
```

| Field  | Name and type  | Sample value  | Description  |
| -- | -- | -- | -- |
| PV1-1  | Set ID - PV1 (SI)  |   | Not necessary  |
| PV1-2  | Patient Class (IS)  | O  | Outpatient See Note 1.0 Below  |
| PV1-3  | Assigned Patient Location (PL)  | POC01  | Point of care information  |
|   | PV1-3.1  | POC01  | Required. ID or abbreviation ofthe clinic.  |


Note 1.0 Below: See https://www.hl7.org/fhir/v2/0004/index.html 

[(back to Table of Contents)](#table-of-contents)

 
### ORC – Common Order

The Common Order segment is used to transmit fields that are common to all orders. The ORC segment is required in the Order (ORM) message. Please note that required fields will be notated in red and special notes will be in blue. 

### Sample ORC segment: 
```
ORC|NW|2017041006^EPC|||||^^^20170410^^R||20170410150905|HJ123^HOPKINS^JOHN S||OP0001^DOE^JACK^^^^^^SERDOTON^^^^SERDOTON|DFM^^^20403^^^^^TEST CLINIC|(425)123-4567^^^^^425^1234567||||H48033^H48033^^20403001^TEST CLINIC|||||||||||O||| 
```

| Field  | Name and type  | Sample value  | Description  |
| -- | -- | -- | -- |
| ORC-1  | Order Control (ID)  | NW or CA  | "Required. New Order (NW) or Cancellation (CA) Client must provide if other value (XO, XR, and CR) will be sent to IRIS for  above cases"  |
|  ORC-2  | Placer Order Number (EI)  | 2017041006^EPC  |  |
|   | ORC-2.1 Entity Identifier  | 2017041006  | Required. Auto generate by EMR  |
|  | ORC-2.2 Namespace ID  | EPC  | Optional Name or abbreviation of the system (EMR) like EPC or EPIC.  |
| ORC-3  | Filler Order Number (EI)  |   | Not necessary  |
| ORC-4  | Placer Group Number (EI)  |   | Optional Auto generate by EMR |
| ORC-5  | Order Status (ID)  |   | Not necessary  |
| ORC-6  | Response Flag (ID)  |   | Not necessary  |
| ORC-7  | Quantity/Timing (TQ)  |   | Not necessary  |
| ORC-8  | Parent Order (EIP)  |   | Not necessary  |
| ORC-9  | Date/Time of Transaction (TS)  | yyyyMMddHHmmss format  | Required. Generated by EMR asorder scheduled time  |
| ORC-10  | Entered By (XCN)  |   |   |
|   | ORC-10.1 ID Number  | HJ123  | Optional This can be used for MSH-8.  |
|   | ORC-10.2 Family Name  | HOPKINS  | Optional  |
|   | ORC-10.3 Given Name  | JOHNS  | Optional  |
|   | ORC-10.4 Second and Further Given Names or Initials Thereof  |   | Not necessary  |
|   | ORC-10.5 Suffix  |   | Not necessary  |
| ORC-11  | Verified By (XCN)  |   |   |
| -- | -- | -- | -- |
| ORC-12  | Ordering Provider (XCN)  | OP0001^DOE^JACK ^^^^^^SERDOTON ^^^^SERDOTON\~ 868^DOE^JACK^^^ ^^^PACS^^^^PACS  | If this field repeats, client must notify IRIS which component and value to use and if the NPI will not be the value used.  |
|   | ORC-12.1 ID  | OP0001  | Required. Accept only if ORC-12.13 is met. In this case, "SERDOTON" will be accepted.  |
|   | ORC-12.2 Family Name  | DOE  | Required  |
|   | ORC-12.3 Given Name  | JACK  | Required  |
|   | …..  |   | ORC-12.4 through ORC-12.11 not necessary  |
|   | ORC-12.13 Identifier Type Code  | Name or type of your system, e.g. SERDOTON, NPI  | Required if field repeats. Client may populate identifier in ORC.12.9 instead  |
| ORC-13  | Enterer's Location (PL)  | DFM^^^20403^^^^^TEST CLINIC  | Optional If client uses this instead of PV1.3, please notify IRIS.  |
|   | ORC-13.1 Point Of Care  | DFM  | Optional ID or abbreviation of the clinic.  |
|   | ORC-13.2 Room  |   | Not necessary  |
|   | ORC-13.3 Bed  |   | Not necessary  |
|   | ORC-13.4 Facility  | 20403  | Optional Internal facility id  |
|   | …..  |   | ORC-13.5 through ORC-13.7 notnecessary  |
|   | ORC-13.8 Location Description  | TEST CLINIC  | Optional  |
| ORC-14  | Call Back Phone Number (XTN)  | (425)123-4567^^^^^425^1234567  | Optional  |
| ORC-15  | Order Effective Date/Time (TS)  |   | Not necessary  |
| ORC-16  | Order Control Code Reason (CE)  |   | Not necessary  |
| ORC-17  | Entering Organization (CE)  |   | Not necessary  |
| ORC-18  | Entering Device (CE)  | H48033^H48033^ ^20403001^TEST CLINIC  | Optional  |
| ORC-19  | Action By (XCN)  |   | Not necessary  |
| ORC-20  | Advanced Beneficiary Notice Code (CE)  |   | Not necessary  |
| ORC-21  | Ordering Facility Name (XON)  |   | Not necessary  |
| ORC-22  | Ordering Facility Address (XAD)  |   | Not necessary  |
| ORC-23  | Ordering Facility Phone Number (XTN)  |   | Not necessary  |
| ORC-24  | Ordering Provider Addre(XAD)  | ss  | Not necessary |
| -- | -- | -- | -- |
| ORC-25  | Order Status Modifier (C | WE)  | Not necessary |


[(back to Table of Contents)](#table-of-contents)

## OBR – Observation Request 

The observation request segment transmits information about an exam, diagnostic study, or assessment that is specific to an order or result. Please note that required fields will be notated in red and special notes will be in blue. 

### Sample OBR segment: 
```
OBR|1|2017041006^EPC||92250^FUNDUS PHOTOGRAPHY^EAP^^FUNDAL PHOTO||20170410|||||L|||||OP0001^DOE^JACK^^^^^^SERDOTON^^^^SERDOTON|(425)598-6900^^^^^425^5986900|||||||OPHTHALMOLOG|||^^^20170410^^R|||||||||20170410||||||||
```

| Field  | Name and type  | Sample value  | Description  |
| -- | -- | -- | -- |
| OBR-1  | Set ID - OBR (SI)  | 1  | Always "1"  |
| OBR-1  | Set ID - OBR (SI)  | 1  | Optional. Auto generate by EMR |
| OBR-2   | Placer Order Number (EI)  | 2017041006^EPC  | Optional. ORC.2.1 will be used for order tracking  |
|   | OBR-2.1 Entity Identifier  | 2017041006  | Internal order number in EMR  |
|  | OBR-2.2 Namespace ID  | EPC  | Name or ID of EMR  |
| OBR-3  | Filler Order Number (EI)  |   | Not necessary  |
| OBR-4   | Universal Service Identifier (CE)   | 92250^FUNDUS PHOTOGRAPHY^EAP^^FUNDAL PHOTO  | Optional. This is CPT code for IRIS services and WILL be used in DFT. Please notify IRIS if the different value is used. See ‘Sample Value’.  |
|   |   | EAP777357^Ophthalmology Retinal Scan  | Sample 1  |
|   |   | 57554^DIABETIC EYE EXAM IN OFFICE^IRISEAP^^DIABETIC EYE EXAM IN OFFICE  | Sample 2  |
|  |   | IMG0555^DIABETIC RETINAL SCREENING (IRIS CAMERA)^MRGECP^^DIABETIC RETINAL SCREENING  | Sample 3  |
|   |  | OPH112^IRIS RETINAL  ASSESSMENT^LAB^^OPH94  | Sample 4  |
| OBR-5  | Priority (ID)  |  | Not necessary  |
| OBR-6  | Requested Date/Time (TS)  |  YYYYMMDD format  | Optional. Auto generate by EMR |
| OBR-7  | Observation Date/Time # (TS)  |   | Not necessary  |
| OBR-8  | Observation End Date/Time # (TS)  |  | Not necessary  |
| OBR-9  | Collection Volume * (CQ)  |   | Not necessary  |
| -- | -- | -- | -- |
| OBR-10  | Collector Identifier * (XCN)  |  | Not necessary  |
| OBR-11  | Specimen Action Code * (ID)  |  L  | Optional  |
| OBR-12  | Danger Code (CE)  |   | Not necessary  |
| OBR-13  | Relevant Clinical Info. (ST)  |   | Not necessary  |
| OBR-14  | Specimen Received Date/Time * (TS)  |   | Not necessary  |
| OBR-15  | Specimen Source (SPS)  |  | Not necessary  |
| OBR-16  | Ordering Provider (XCN)  | OP0001^DOE^JACK^^^^^^ SERDOTON^^^^SERDOTON  | Optional. Same value with ORC-12.  |
| OBR-17  | Order Callback Phone Number (XTN)  | (425)598- 6900^^^^^425^5986900  | Optional  |
| OBR-18  | Placer Field 1 (ST)  |   | Not necessary  |
| OBR-19  | Placer Field 2 (ST)  |   | Not necessary  |
| OBR-20  | Filler Field 1 + (ST)  |  | Not necessary  |
| OBR-21  | Filler Field 2 + (ST)  |    | Not necessary  |
| OBR-22  | Results Report/Status Change - Date/Time + (TS)  |   | Not necessary  |
| OBR-23  | Charge to Practice + (MOC)  |  | Not necessary  |
| OBR-24  | Diagnostic Serv Sect ID (ID)  | OPHTHALMOLOGY   | Optional. Can be defined by EMR  |
| OBR-25  | Result Status + (ID)  |   | Not necessary  |
| OBR-26  | Parent Result + (PRL)  |  | Not necessary  |
| OBR-27  | Quantity/Timing (TQ)  |  ^^^20170404^^R  | Optional  |
| OBR-28  | Result Copies To (XCN)  |   | Not necessary  |
| OBR-29  | Parent Number (EIP)  |   | Not necessary  |
| OBR-30  | Transportation Mode (ID)  |   | Not necessary  |
| OBR-31  | Reason for Study (CE)  |   | Not necessary  |
| OBR-32  | Principal Result Interpreter + (NDL)  |   | Not necessary  |
| OBR-33  | Assistant Result Interpreter + (NDL)  |   | Not necessary  |
| OBR-34  | Technician + (NDL)  |   | Not necessary  |
| OBR-35  | Transcriptionist + (NDL)  |  | Not necessary  |
| OBR-36  | Scheduled Date/Time + (TS)  |  YYYYMMDD format  | Optional. Auto generate by EMR |
| OBR-37  | Number of Sample Containers * (NM)  |   | Not necessary  |
| OBR-38  | Transport Logistics of Collected Sample * (CE)  |   | Not necessary  |
| OBR-39  | Collector's Comment * (CE)  |   | Not necessary  |
| OBR-40  | Transport Arrangement Responsibility (CE)  |  | Not necessary  |
| OBR-41  | Transport Arranged (ID)  |   | Not necessary  |
| -- | -- | -- | -- |
| OBR-42  | Escort Required (ID)  |   | Not necessary  |
| OBR-43  | Planned Patient TranspoComment (CE)  | rt   | Not necessary  |
| OBR-44  | Procedure Code (CE)  |   | Not necessary  |
| OBR-45  | Procedure Code Modifie | r (CE)  | Not necessary  |
| OBR-46  | Placer Supplemental SerInformation (CE)  | vice   | Not necessary  |
| OBR-47  | Filler Supplemental ServInformation (CE)  | ice  | Not necessary  |

[(back to Table of Contents)](#table-of-contents)

## DG1 – Diagnosis Segment

The diagnosis segment contains patient diagnosis information. The DG1 segment is optional and can be repeated. IRIS supports ICD-10 codes. Please note that required fields will be notated in red and special notes will be in blue. 

### Sample DG1 segments: 

```
DG1|1|ICD-10|E11.41^Type 2 diabetes mellitus with diabetic mononeuropathy^I10|Type 2 diabetes mellitus with diabetic mononeuropathy 
```

| Field  | Name and type  | Sample value  | Description  |
| -- | -- | -- | -- |
| DG1-1  | Set ID - DG1 (SI)  | 1  | Required if sent. Increasedsequentially by 1.  |
| DG1-2  | Diagnosis Coding Method (ID)  | 10 or ICD10  | Required if sent. Iris only accepts ICD-10 codes.  |
| DG1-3  | Diagnosis Code - DG1 (CE)  | 250.1, E11.41  | Required if sent. Id of the diagnosis  |
| DG1-4  | Diagnosis Description (ST)  | DIABETES MELLITUS WITHOUT MENTION OF COMPLICATION, TYPE II OR UNSPECIFIED TYPE, NOT STATED AS UNCONTROLLED  | Required if sent.  |

 


## Revision History: 


| Row No.  | Revision Date  | Version Update  | Revision Notes  |
| -- | -- | -- | -- |
| 1  | Sept. 26, 2018  | Version 1.0  | Initial documentation creation Updated version  |
| 2  | Oct. 3, 2018  | Version 2.0  | Corrected typos in several segment section descriptions Added footnotes to some sections to add additionaldescriptions (where applicable) Added “Examples” section Added color-coding notes to each segment section Updated version  |
| 3  | Jan. 8, 2019  | Version 2.1  | Added a “Revision History” section Updated version  |
| 4  | Mar. 3, 2020  | Version 2.2  | Updated Diagnoses and altered formatting slightly Updated version  |
| 5  | Jun. 6, 2021  | Version 2.3  | Slight formatting changes Updated version  |
| 6  | Aug 31, 2021  | OBS  | Moving to OBS and will re-implement under TEC documents  |
| 7  | Aug 31, 2021  | TECH 005 Rev A  | Re implemented as TEC document  |
| 7  | Sep. 14, 2023  | TEC 005 REV B - Version 2.4  | Removed version from Acknowledgement section. Updated MSH.4 description/requirements. Updated PID.19 description. Updated ORC.12 description. Altered DG1 section to exclude ICD-9 code requirements and wording on all descriptions. Updated Version  |






