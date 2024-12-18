---
title: EVN Segment – Event Type 
parent: DFT (DFT-P03)
nav_order: 3
---
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

← [MSH Segment](/IntegrationDocumentation/docs/integration/DFT_Results/MSH_Segment_Message_Header) |
[PID Segment - Patient Identification](/IntegrationDocumentation/docs/integration/DFT_Results/PID_Segment_Patient_Identification) →