---
title: Example Messages 
parent: ORU (ORU-R01)
---

## Example Messages

### Example A
```
MSH|^\~\&|IRIS|IRIS|Vendor|Vendor|20191220174508||ORU^R01|191220174508|T|2.3 
PID||Test2106462|Test2106462||TestLN^TestFN||19630130|M||||||||||293907374|
PV1|1|O|WRSIM||||FakeNPInum^DocLastName^ROBERT^^^MD^MD^^^^^^NPI|FakeNPInum^DocLastName^ROBERT^^^MD^MD^^^^^^NPI|||||||||FakeNPInum^DocLastName^ROBERT^^^MD^MD^^^^^^NPI||293907374|||||||||||||||||||||||||20191220054252|20191220054252 
ORC|RE|111997409|799248^IRIS||F||||20191220174508|||FakeNPInum^DocLastName^ROBERT^^^MD^MD^^^^^^NPI 
OBR|1|111997409|799248^IRIS|^FUNDUS PHOTOGRAPHY^EAP^^FUNDAL PHOTO|||20191220054252|||||||20191220054252||FakeNPInum^DocLastName^ROBERT^^^MD^M D^^^^^^NPI||||||20191220054412|||F|||||||adiaz@retinalscreenings.com^Diaz^Adam^^Adam Diaz, MD, NPI: NPI0987654, Taxonomy: 207W00000X 
OBX|1|ST|SEVERITY^^IRIS|1|NORMAL||||||F 
OBX|2|ST|RIGHTDIABRETIN^^IRIS|2|None||||||F 
OBX|3|ST|RIGHTMACEDEMA^^IRIS|3|None||||||F 
OBX|4|ST|RIGHTOTHERRETIN^^IRIS|4|None||||||F
OBX|5|ST|RIGHTQUALAPP^^IRIS|5|Gradable Image||||||F 
OBX|6|ST|LEFTDIABRETIN^^IRIS|6|None||||||F 
OBX|7|ST|LEFTMACEDEMA^^IRIS|7|None||||||F 
OBX|8|ST|LEFTOTHERRETIN^^IRIS|8|None||||||F 
OBX|9|ST|LEFTQUALAPP^^IRIS|9|Gradable Image||||||F 
OBX|10|FT|Result^^IRIS|001|Retinal Study Result for TestFN TestLN||||||F 
OBX|11|FT|Result^^IRIS|002|||||||F 
OBX|12|FT|Result^^IRIS|003|TestFN TestLN, a 56 y/o, M (DOB: 01-30-1963, MRN: Test2106462)||||||F 
OBX|13|FT|Result^^IRIS|004|presented to Iris Test Client on 12-20-2019 for a retinal imaging study of the left and right eyes.||||||F 
OBX|14|FT|Result^^IRIS|005|||||||F 
OBX|15|FT|Result^^IRIS|006|Based on the findings of the study, the following is recommended for TestFN TestLN||||||F TestFN TestLN||||||F 
OBX|16|FT|Result^^IRIS|007|Normal Scan: Please advise the patient to return for a scan in 12 months.||||||F 
OBX|17|FT|Result^^IRIS|008|||||||F
OBX|18|FT|Result^^IRIS|009|Interpreting Provider's Comments: No comments provided||||||F 
OBX|19|FT|Result^^IRIS|010|||||||F 
OBX|20|FT|Result^^IRIS|011|Right eye findings: Normal Result. Negative for Diabetic Retinopathy.||||||F 
OBX|21|FT|Result^^IRIS|012|||||||F
OBX|22|FT|Result^^IRIS|013|Left eye findings: Normal Result. Negative for Diabetic Retinopathy.||||||F 
OBX|23|FT|Result^^IRIS|014|||||||F
OBX|24|FT|Result^^IRIS|015|||||||F
OBX|25|FT|Result^^IRIS|016|This result was electronically signed by Diaz, Adam, on 12-20-2019 05:44:12 UTC time.||||||F 
OBX|26|FT|Result^^IRIS|017|||||||F
OBX|27|FT|Result^^IRIS|018|NOTE: Any pathology noted on this diabetic retinal evaluation should be confirmed by an appropriate ophthalmic examination.||||||F 
OBX|27|ED|||PDF^TEXT^^Base64^&#36;{ENCODED DOCUMENT REMOVED}||||||F 
```
### Example B
```
MSH|^\~\&|IRIS|IRIS|Vendor|Vendor|20191223193115||ORU^R01|191223193115|P|2.3 
PID||MRNtest123|MRNtest123||TESTB^IRIS||19391126|F||||||||||123456789|
PV1|1|O|WRSIM||||NPI5556666^DocLastName^MAZHAR^^^MD^MD^^^^^^NPI|NPI5556666^DocLastName^MAZHAR^^^MD^MD^^^^^^NPI|||||||||NPI5556666^DocLastName^MAZHAR^^^MD^MD^^^^^^NPI||123456789|||||||||||||||||||||||||20191223012424|20191223012424 
ORC|RE|12378912|799932^IRIS||F||||20191223193115|||NPI5556666^DocLastName^MAZHAR^^^MD^MD^^^^^^NPI 
OBR|1|12378912|799932^IRIS|^FUNDUS PHOTOGRAPHY^EAP^^FUNDAL PHOTO|||20191223012424|||||||20191223012424||NPI5556666^DocLastName^MAZHAR^^^MD^M D^^^^^^NPI||||||20191223012555|||F|||||||1234567890^Diaz^Adam^^^MD^MD^^^^^^NPI 
OBX|1|ST|SEVERITY^^IRIS|1|CRITICAL|||AA|||F 
OBX|2|ST|LEFTDIABRETIN^^IRIS|2|Severe|||AA|||F 
OBX|3|ST|LEFTMACEDEMA^^IRIS|3|Severe|||AA|||F 
OBX|4|ST|LEFTOTHERRETIN^^IRIS|4|Suspected Vein Occlusion|||A|||F 
OBX|5|ST|LEFTQUALAPP^^IRIS|5|Gradable Image||||||F 
OBX|6|ST|RIGHTDIABRETIN^^IRIS|6|Moderate|||A|||F 
OBX|7|ST|RIGHTMACEDEMA^^IRIS|7|Moderate|||A|||F
OBX|8|ST|RIGHTOTHERRETIN^^IRIS|8|Suspected Dry AMD|||A|||F 
OBX|9|ST|RIGHTQUALAPP^^IRIS|9|Gradable Image||||||F 
OBX|10|FT|Result^^IRIS|001|Retinal Study Result for IRIS TESTB||||||F 
OBX|11|FT|Result^^IRIS|002|||||||F 
OBX|12|FT|Result^^IRIS|003|IRIS TESTB, a 80 y/o, F (DOB: 11-26-1939, MRN: MRNtest123)||||||F 
OBX|13|FT|Result^^IRIS|004|presented to Southcoast Health - WRS Internal Medicine on 12-23-2019 for a retinal imaging study of the left and right eyes.||||||F 
OBX|14|FT|Result^^IRIS|005|||||||F 
OBX|15|FT|Result^^IRIS|006|Based on the findings of the study, the following is recommended for IRIS TESTB||||||F 
OBX|16|FT|Result^^IRIS|007|Next Available Appointment: Refer patient to a retina specialist, next available appointment.||||||F available appointment.||||||F 
OBX|17|FT|Result^^IRIS|008|||||||F
OBX|18|FT|Result^^IRIS|009|Interpreting Provider's Comments: No comments provided||||||F 
OBX|19|FT|Result^^IRIS|010|Diagnoses Present: E11.3311 - Type 2 diabetes mellitus with moderate nonproliferative diabetic retinopathy with macular edema, right eye||||||F 
OBX|20|FT|Result^^IRIS|011|E11.3412 - Type 2 diabetes mellitus with severe nonproliferative diabetic retinopathy with macular edema, left eye||||||F 
OBX|21|FT|Result^^IRIS|012|||||||F
OBX|22|FT|Result^^IRIS|013|Right eye findings: Diabetic Retinopathy: Moderate||||||F 
OBX|23|FT|Result^^IRIS|014|Macular Edema: Moderate||||||F 
OBX|24|FT|Result^^IRIS|015|Other: Suspected Dry AMD||||||F 
OBX|25|FT|Result^^IRIS|016|||||||F
OBX|26|FT|Result^^IRIS|017|Left eye findings: Diabetic Retinopathy: Severe||||||F 
OBX|27|FT|Result^^IRIS|018|Macular Edema: Severe||||||F 
OBX|28|FT|Result^^IRIS|019|Other: Suspected Vein Occlusion||||||F 
OBX|29|FT|Result^^IRIS|020|||||||F
OBX|30|FT|Result^^IRIS|021|||||||F
OBX|31|FT|Result^^IRIS|022|This result was electronically signed by Diaz, Adam, on 12-23-2019 07:25:55 UTC time.||||||F 07:25:55 UTC time.||||||F 
OBX|32|FT|Result^^IRIS|023|||||||F 
OBX|33|FT|Result^^IRIS|024|NOTE: Any pathology noted on this diabetic retinal evaluation should be confirmed by an appropriate ophthalmic examination.||||||F 
OBX|34|RP|LINK^^PDFLINK|34|https://api.retinalscreenings.com/api/PatientOrders/GetSingleResultFo rDisplayInEmr?patientOrderId=799932\T\asPdf=True\T\isPreliminary=False\T\auth=6DCAFF6AC2A555F 00F9E470D221B6A077C3497A668B1EEBBB4983C8D98672F8FBA00707190026B817325C2A088725B5A0E5D7AB659AC0790C1C1D22B2C50F897\T\asAddendum=False||||||F 
```

### Example C

```
MSH|^\~\&|IRIS|IRIS|Vendor|Vendor|20200103185623||ORU^R01|200103185623|T|2.3 
PID||15852|15852||Tester^Patient1||19990312|M|||||||||||
PV1|1|O|Iris Test Client||||aalderman@retinalscreenings.com^Alderman^Allan^^^PhD^PhD^^^^^^NPI|aalderman@reti nalscreenings.com^Alderman^Allan^^^PhD^PhD^^^^^^NPI|||||||||aalderman@retinalscreenings.co m^Alderman^Allan^^^PhD^PhD^^^^^^NPI||Encounter|||||||||||||||||||||||||20191218044543|20191218044543 
ORC|RE|7e39fa9b-27d6-4792-87692f9f422f187a|797619^IRIS||F||||20200103185623|||aalderman@retinalscreenings.com^Alderman^A llan^^^PhD^PhD^^^^^^NPI 
OBR|1|7e39fa9b-27d6-4792-8769-2f9f422f187a|797619^IRIS|92250^FUNDUS PHOTOGRAPHY^EAP^^FUNDAL PHOTO|||20191218044543|||||||20191218044543||aalderman@retinalscreenings.com^Alderman^A llan^^^PhD^PhD^^^^^^NPI||||||20191220023008|||F|||||||NPIorCredentials^LastName^Ryan^20191220023008^LastName Carter, MD, NPI: 1902127947, Taxonomy: 207W00000X 
OBX|1|ST|SEVERITY^^IRIS|1|NORMAL||||||F 
OBX|2|ST|LEFTDIABRETIN^^IRIS|2|None||||||F 
OBX|3|ST|LEFTMACEDEMA^^IRIS|3|None||||||F 
OBX|4|ST|LEFTOTHERRETIN^^IRIS|4|None||||||F 
OBX|5|ST|LEFTQUALAPP^^IRIS|5|Gradable Image||||||F 
OBX|6|ST|RIGHTDIABRETIN^^IRIS|6|None||||||F 
OBX|7|ST|RIGHTMACEDEMA^^IRIS|7|None||||||F 
OBX|8|ST|RIGHTOTHERRETIN^^IRIS|8|None||||||F 
OBX|9|ST|RIGHTQUALAPP^^IRIS|9|Gradable Image||||||F 
NTE|1|ST|Retinal Study Result for Patient1 Tester||||||||F
NTE|2|ST|||||||||F 
NTE|3|ST|Patient1 Tester, a 20 y/o, M (DOB: 03-12-1999, MRN: 15852)||||||||F
NTE|4|ST|presented to Iris Test Client on 12-18-2019 for a retinal imaging study of the left and right eyes.||||||||F 
NTE|5|ST|||||||||F 
NTE|6|ST|Based on the findings of the study, the following is recommended for Patient1 Tester||||||||F 
NTE|7|ST|Normal Scan: Please advise the patient to return for a scan in 12 months.||||||||F NTE|8|ST|||||||||F 
NTE|9|ST|Interpreting Provider's Comments: No comments provided||||||||F
NTE|10|ST|||||||||F 
NTE|11|ST|Right eye findings: Normal Result. Negative for Diabetic Retinopathy.||||||||F 
NTE|12|ST|||||||||F 
NTE|13|ST|Left eye findings: Normal Result. Negative for Diabetic Retinopathy.||||||||F 
NTE|14|ST|||||||||F 
NTE|15|ST|||||||||F 
NTE|16|ST|This result was electronically signed by LastName, Ryan, MD, NPI: NPIorCredentials, Taxonomy: 207W00000X on 12-20-2019 02:30:08 UTC time.||||||||F 
NTE|17|ST|||||||||F 
NTE|18|ST|NOTE: Any pathology noted on this diabetic retinal evaluation should be confirmed by an appropriate ophthalmic examination.||||||||F 
```
