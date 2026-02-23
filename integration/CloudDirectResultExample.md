---
title: Order Result Example
parent: Cloud Direct
nav_order: 3
---

# Sample OrderResults Message
The following example is a JSON encoded Order Result.

> <small>To view details of fields in this example, copy this page into any editor capable of parsing the schema.  Visual Studio Code was used for building the example. </small>
 
```json
{
    "$schema": "https://cdn.retinalscreenings.com/hosts/iris/schemas/order-results.schema.2.3.1.json",
    "Version": "2.3.1",
    "Timestamp": "",
    "TransactionId": "",
    "ResultCode": "F",
    "Site": {
        "LocalId": "PC1234"
    },
    "ResultsDocument": {
        "Type": "PDF",
        "Encoding": "Base64",
        "Content": "..."
    },
    "ImageDetails": {
        "TotalCount": 0,
        "RightEyeCount": 0,
        "RightEyeOriginalCount": 0,
        "RightEyeEnhancedCount": 0,
        "LeftEyeCount": 0,
        "LeftEyeOriginalCount": 0,
        "LeftEyeEnhancedCount": 0,
        "SingleEyeOnly": false
    },
    "Images": [
        {
            "LocalId": null,
            "Taken": "2022-01-02T17:42:18.6936779+00:00",
            "Received": "2022-01-02T17:42:18.6936779+00:00",
            "FileName": "9298DA56-E516-40E3-A35D-41B5D238DC7D.jpg",
            "Laterality": "OD",
            "ImageContext": "Primary",
            "ParentLocalId": null,
            "GroupId": null,
            "GroupOrdinal": null,
            "Camera": {
                "LocalId": "REM-1000",
                "Location": null,
                "IPAddress": null,
                "MACAddress": null,
                "SerialNumber": "REM-1000",
                "Manufacturer": "Remidio",
                "Model": "NMFOP",
                "SoftwareVersion": "2.2.23"
            }
        },
        {
            "LocalId": null,
            "Taken": "2022-01-02T17:42:18.6936779+00:00",
            "Received": "2022-01-02T17:42:18.6936779+00:00",
            "FileName": "04211055-DFF7-41EF-9EF3-43FE61D10D43.jpg",
            "Laterality": "OS",
            "ImageContext": "Primary",
            "ParentLocalId": null,
            "GroupId": null,
            "GroupOrdinal": null,
            "Camera": {
                "LocalId": "REM-1000",
                "Location": null,
                "IPAddress": null,
                "MACAddress": null,
                "SerialNumber": "REM-1000",
                "Manufacturer": "Remidio",
                "Model": "NMFOP",
                "SoftwareVersion": "2.2.23"
            }
        }
    ],
    "Order": {
        "PatientOrderId": 1094030,
        "Status": "Complete",
        "LocalId": "ORD1234",
        "EvaluationTypes": [
            "DR"
        ],
        "ScheduledTime": null,
        "CreatedTime": "2022-01-01T12:42:18.6929481+00:00",
        "ServiceDate": "2022-01-04T12:42:18.6929481+00:00",
        "DepartmentId": null,
        "EncounterNumber": null,
        "StudyInstanceUniqueId": null,
        "OrderableIdentifier": null,
        "AdditionalInfo": null,
        "State": "FL",
        "SingleEyeOnly": false
    },
    "Patient": {
        "LocalId": "1234",
        "Name": {
            "First": "John",
            "Last": "Doe"
        },
        "Dob": "1/1/2000",
        "Gender": "U"
    },
    "OrderingProvider": {
        "NPI": "1234567890",
        "Taxonomy": "207W00000X",
        "Name": {
            "Title": "Dr",
            "First": "John",
            "Last": "Doe"
        },
        "Email": "John.Doe@providers.com",
        "Degrees": "MD",
        "Associations": null
    },
    "Gradings": {
        "Notes": [
            {
                "Date": "2022-01-03T12:42:18.6929481+00:00",
                "Text": null
            }
        ],
        "GradedTime": "2022-01-03T12:42:18.6929481+00:00",
        "QueuedTime": "2022-01-02T12:42:18+00:00",
        "CarePlanName": "Return in 6 months",
        "CarePlanDescription": "Have patient return in 6 months for a followup exam.",
        "Pathology": true,
        "Urgent": false,
        "Emergent": false,
        "OD": {
            "Gradable": true,
            "MissingEyeReason": null,
            "UngradableReasons": [],
            "Findings": [
                {
                    "Finding": "Diabetic Retinopathy",
                    "Result": "Mild"
                }
            ]
        },
        "OS": {
            "Gradable": true,
            "Findings": null
        },
        "DxCodes": [
            "E083211"
        ],
        "Provider": {
            "NPI": "1234567890",
            "Taxonomy": "207W00000X",
            "Name": {
                "Title": "Dr",
                "First": "John",
                "Last": "Doe"
            },
            "Email": "John.Doe@providers.com",
            "Degrees": "MD",
            "Associations": null
        }
    },
    "CameraOperator": {
        "UserName": "john.doe@primarycare.com",
        "Name": {
            "First": "John",
            "Last": "Doe"
        },
        "Notes": [
            {
                "Date": "2022-01-03T12:42:18.6929481+00:00",
                "Text": null
            }
        ]
    },
    "HealthPlan": {
        "LocalId": "1234",
        "Name": "ProviderA",
        "MemberId": "1234"
    },
    "Cpt": {
        "Code": "92250",
        "Description": "Fundus photography with interpretation and report"
    }
}

```
