---
title: PV1 – Patient Visit
parent: DFT (DFT-P03)
nav_order: 5
---

## PV1 Segment – Patient Visit

The patient visit segment includes patient-specific visit information.

**Sample PV1 segment:**

PV1|1|O|POC01||||GR0001^DOE^JANE^^^MD^MD^^^^^^NPI|OP0001^DOE^JACK^^^MD^MD^^^^^^NPI|||||||||GR0001^DOE^JANE^^^MD^MD^^^^^^NPI|||||||||||||||||||||||||||20170410145803|20170410145803

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

[Back to HL7 DFT Results Page](/docs/integration/DFT_Results/DFT_Results.md)