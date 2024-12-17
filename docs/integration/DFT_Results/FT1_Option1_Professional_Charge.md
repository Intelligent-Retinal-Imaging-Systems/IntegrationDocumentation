---
title: FT1 (Option 1) – Professional Charge
parent: HL7 Messages
---

## FT1 (Option 1) – Professional Charge

[Back to FT1 (Option 1) – Financial Transaction](/docs/integration/DFT_Results/FT1_Option1_Financial_Transaction.md)

**Sample FT1 segment (Professional Charge):**

FT1|1||273013|20170410145901|20170410151351|CG|92250^Fundus photography with interpretation and report^CPT||ITCC20170410|1|||POC01||IRIS|POC01|||E11.41^Type 2 diabetes mellitus with diabetic mononeuropathy^ICD-10-CM~E11.3592^Type 2 diabetes mellitus with proliferative diabetic retinopathy without macular edema, left eye^ICD-10-CM~H35.81^Retinal edema^ICD-10-CM|GR0001^DOE^JANE^^^MD^MD^^^^^^NPI|OP0001^DOE^JACK^^^MD^MD^^^^^^NPI||2017041006^EPIC||92250^Fundus photography with interpretation and report^CPT


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

[Back to HL7 DFT Results Page](/docs/integration/DFT_Results/DFT_Results.md)