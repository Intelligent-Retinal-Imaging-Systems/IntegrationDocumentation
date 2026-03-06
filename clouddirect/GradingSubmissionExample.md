---
title: Grading Submission
parent: Examples
nav_order: 4
---

## Submitting test gradings via Service Bus Examples
##### JSON encoded Grading Request.


> ✨ <small>By including the schema reference (as shown in the example below) you can leverage tools such as Visual Studio Code to expose issues in your submission object.  The schema also provides detailed descriptions for each field including available options for enumerations and exposes invalid finding/result combinations.</small>
  

```json 
{
 {
    "$schema": "https://cdn.retinalscreenings.com/hosts/iris/schemas/grading-submission.schema.2.3.1.json",
    "Version": "2.3.1",
    "OD": {
        "Findings": [
            {
                "Finding": "Diabetic Retinopathy",
                "Result": "Mild"
            },
            {
                "Finding": "Macular Edema",
                "Result": "None"
            },
            {
                "Finding": "Wet AMD",
                "Result": "No Observable"
            },
            {
                "Finding": "Dry AMD",
                "Result": "No Observable"
            }
        ],
        "Gradable": true,
        "UngradableReasons": null,
        "MissingEyeReason": null
    },
    "OS": {
        "Findings": [
            {
                "Finding": "Diabetic Retinopathy",
                "Result": "None"
            },
            {
                "Finding": "Macular Edema",
                "Result": "None"
            },
            {
                "Finding": "Wet AMD",
                "Result": "No Observable"
            },
            {
                "Finding": "Dry AMD",
                "Result": "No Observable"
            }
        ],
        "Gradable": true,
        "UngradableReasons": null,
        "MissingEyeReason": null
    },
    "LocalId": "",
    "ClientGuid": "",
    "Site": {
        "Name": null,
        "Address": null,
        "LocalId": ""
    }
}
}
```