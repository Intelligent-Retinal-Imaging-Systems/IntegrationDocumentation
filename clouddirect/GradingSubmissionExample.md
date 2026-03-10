---
title: Grading Submission
parent: Examples
nav_order: 6
---

## Submitting test gradings via Service Bus Examples

> ✨ <small>By including the schema reference (as shown in the example below) you can leverage tools such as Visual Studio Code to expose issues in your submission object.  The schema also provides detailed descriptions for each field including available options for enumerations and exposes invalid finding/result combinations.</small>


### ![alt text](/assets/example.ico) Example 1


* Evaluation: **DR+AMD**
* Findings:  **Normal** 


```json 
{
    "$schema": "https://cdn.retinalscreenings.com/hosts/iris/schemas/grading-submission.schema.2.3.1.json",
    "Version": "2.3.1",
    "OD": {
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
        "Gradable": true
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
    "LocalId": "1315535",
    "ClientGuid": "63E3C9EF-66AC-4154-B0C2-494515EB99A7",
    "Site": {
        "LocalId": "12345"
    }
}
```
---

### ![alt text](/assets/example.ico) Example 2
  
* Evaluation: **DR**
* Findings:  **Normal** Left, **Mild DR**, **Suspected Glaucoma** Right

```json 
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
                "Finding":"Suspected Glaucoma"
            }
        ],
        "Gradable": true
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
            }
        ],
        "Gradable": true,
        "UngradableReasons": null,
        "MissingEyeReason": null
    },
    "LocalId": "131553564",
    "ClientGuid": "63E3C9EF-66AC-4154-B0C2-494515EB99A7",
    "Site": {
        "LocalId": "434254"
    }
}
```
---

### ![alt text](/assets/example.ico) Example 3

* Evaluation: **DR**
* Findings:  Ungradable Left, **Normal** Right

```json 
{
    "$schema": "https://cdn.retinalscreenings.com/hosts/iris/schemas/grading-submission.schema.2.3.1.json",
    "Version": "2.3.1",
    "OD": {
        "Findings": [
            {
                "Finding": "Diabetic Retinopathy",
                "Result": "None"
            },
            {
                "Finding": "Macular Edema",
                "Result": "None"
            }
        ],
        "Gradable": true
    },
    "OS": {
        "Gradable": false,
        "UngradableReasons": ["Key anatomy missing or not clearly visible"]
    },
    "LocalId": "131553564",
    "ClientGuid": "63E3C9EF-66AC-4154-B0C2-494515EB99A7",
    "Site": {
        "LocalId": "434254"
    }
}
```
---

### ![alt text](/assets/example.ico) Example 4
  
* Evaluation: **DR** (Single Eye)
* Findings: **Normal**

```json 
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
                "Finding":"Suspected Glaucoma"
            }
        ],
        "Gradable": true
    },
    "OS": {
       "MissingEyeReason": "Enucleation"
    },
    "LocalId": "1315535634",
    "ClientGuid": "63E3C9EF-66AC-4154-B0C2-494515EB99A7",
    "Site": {
        "LocalId": "434254"
    }
}
```
