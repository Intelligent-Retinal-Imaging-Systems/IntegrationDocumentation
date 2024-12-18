---
title: FT1 (Option 2) – Technical Charge
parent: FT1 (Option 2) – Financial Transaction
---

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


<< [FT1 (Option 2) Financial Transaction](/IntegrationDocumentation/docs/integration/DFT_Results/FT1_Option2_Financial_Transaction) |
[FT1 (Option 2) Professional Charge](/IntegrationDocumentation/docs/integration/DFT_Results/FT1_Option2_Professional_Charge) >>