---
title: PID – Patient Identification
parent: DFT (DFT-P03)
nav_order: 4
---

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

[Back - EVN Segment - Event Type](/IntegrationDocumentation/docs/integration/DFT_Results/EVN_Segment_Event_Type) <->
[Next - PV1 Segment - Patient Visit](/IntegrationDocumentation/docs/integration/DFT_Results/PV1_Segment_Patient_Visit)
