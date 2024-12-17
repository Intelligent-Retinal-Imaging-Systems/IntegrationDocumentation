---
title: MSH Segment – Message Header
parent: HL7 Messages
---

## MSH Segment – Message Header

The message header segment includes information that defines the structure of the message.

**Sample MSH segment:**

MSH|^~\&|IRIS|IRIS|VENDOR|VENDOR|20170410145907||ORU^R01|170410145907|T|2.4

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




[Back to HL7 DFT Results Page](/docs/integration/DFT_Results/DFT_Results.md)