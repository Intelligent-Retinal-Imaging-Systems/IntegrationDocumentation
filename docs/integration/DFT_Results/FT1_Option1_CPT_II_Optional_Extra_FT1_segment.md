---
title: DFT 
parent: HL7 Messages
---

## FT1 (Option 1) – CPT II Optional Extra FT1 segment

This extra FT1 segment is CPT II data for the patient over 18 at the time of result and has normal result (Diabetic Retinopathy is None). This extra FT1 segment will only be sent upon demand.

[Back to FT1 (Option 1) – Financial Transaction](/docs/integration/DFT_Results/FT1_Option1_Financial_Transaction.md)

**Example FT1 segment (CPT II):**

FT1|2||273013|20170410145803|20170410173627|CG|3072F^No evidence of retinopathy in the prior year||ITCC20170410|1|||POC01||IRIS|POC01|||E11.41^Type 2 diabetes mellitus with diabetic mononeuropathy^ICD-10-CM~E11.3592^Type 2 diabetes mellitus with proliferative diabetic retinopathy without macular edema, left eye^ICD-10-CM~H35.81^Retinal edema^ICD-10-CM|GR0001^DOE^JANE^^^MD^MD^^^^^^NPI|OP0001^DOE^JACK^^^MD^MD^^^^^^NPI||2017041006^EPIC||3072F^No evidence of retinopathy in the prior year

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

*Effective 10/2019, 2022F has been modified and there is a new code also added on:
```
2022F: Dilated retinal eye exam with interpretation by an ophthalmologist or optometrist documented and reviewed; with evidence of retinopathy.
2023F: Dilated retinal eye exam with interpretation by an ophthalmologist or optometrist documented and reviewed; without evidence of retinopathy. 
```

Additionally, 3072F has been used when the patient had a normal exam the year prior: 3072F:
```
Low risk for retinopathy (no evidence of retinopathy in the prior year)
```

Note –this code has been used to close the care gap when results are “Negative for Retinopathy” for two years

[Back to HL7 DFT Results Page](/docs/integration/DFT_Results/DFT_Results.md)