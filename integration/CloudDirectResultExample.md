---
title: Order Result Example
parent: Cloud Direct
nav_order: 3
---

# Sample OrderResults Message
The following is an example of a JSON encoded representation of an Order Result.  
*Values set in this example are intended to display data types only and may contradict actual values found in other parts of the document (e.g.: Date Time values).*
  
 
```javascript
{
    "Version": "2.3.1",                  // Version of this structure
    "Timestamp" : "",
    "TransactionId": "",
    "ResultCode": "F",                   // P=Preliminary, A=Addendum, F=Final, C=Correction, R=Resend
    "Site": {                            // Site/Location the Order is assigned to
      "LocalId": "PC1234"                // Id of site as defined by submitting organization    
    },
    "ResultsDocument": {
        "Type": "PDF",                  // PDF, HTML, ORU
        "Encoding": "Base64",           // Base64, HL7 or specific encoding scheme
        "Content": "..."                // Actual Content
    },
    "ImageDetails" : {
        "TotalCount":0,
        "RightEyeCount": 0,
        "RightEyeOriginalCount": 0,
        "RightEyeEnhancedCount": 0,
        "LeftEyeCount": 0,
        "LeftEyeOriginalCount": 0,
        "LeftEyeEnhancedCount": 0,
        "Preferred": true,                   //  True, False If True the image is marked as being preferred for reports
        "SingleEyeOnly": false             // If true the order expects images from one eye side only    
    },
    "Images": [{
        "LocalId": null,                // Id of image as specified by submitting organization
        "Taken": "2022-01-02T17:42:18.6936779+00:00",       // Timestamp when Image was taken
        "Received": "2022-01-02T17:42:18.6936779+00:00",    // Timestamp when image was received by Iris
        "FileName": "9298DA56-E516-40E3-A35D-41B5D238DC7D.jpg",     // Filename of image
        "Laterality": "OD",             // OD, OS
        "ImageContext": "Primary",      // Primary, Secondary, Component, Aggregate, Enhancement
        "ParentLocalId": null,          // If child of other image, that image's LocalId
        "GroupId": null,                // Optional Grouping context
        "GroupOrdinal": null,           // Optional Ordinal of image in group context by results receiving organization
        "Camera": {
            "LocalId": "REM-1000",      // Specifies Camera Id as defined by submitting organization
            "Location": null,           // Optional Camera location details
            "IPAddress": null,                  // Optional IP Address assignment of camera
            "MACAddress": null,                 // Optional MAC Address of camera NIC
            "SerialNumber": "REM-1000",         // Serial Number of Camera
            "Manufacturer": "Remidio",          // Manufacturer of Camera 
            "Model": "NMFOP",                   // Model Name of Camera
            "SoftwareVersion": "2.2.23"
        }
    },
    {
        "LocalId": null,                // Id of image as specified by submitting organization
        "Taken": "2022-01-02T17:42:18.6936779+00:00",       // Timestamp when Image was taken
        "Received": "2022-01-02T17:42:18.6936779+00:00",    // Timestamp when image was received by Iris        
        "FileName": "04211055-DFF7-41EF-9EF3-43FE61D10D43.jpg",   // Filename of image
        "Laterality": "OS",             // OD, OS
        "ImageContext": "Primary",      // Primary, Secondary, Component, Aggregate, Enhancement
        "ParentLocalId": null,          // If child of other image, that image's LocalId
        "GroupId": null,                // Optional Grouping context
        "GroupOrdinal": null,           // Optional Ordinal of image in group context by results receiving organization
        "Camera": {
            "LocalId": "REM-1000",      // Specifies Camera Id as defined by submitting organization
            "Location": null,           // Optional Camera location details
            "IPAddress": null,                  // Optional IP Address assignment of camera
            "MACAddress": null,                 // Optional MAC Address of camera NIC
            "SerialNumber": "REM-1000",         // Serial Number of Camera
            "Manufacturer": "Remidio",          // Manufacturer of Camera 
            "Model": "NMFOP",                   // Model Name of Camera
            "SoftwareVersion": "2.2.23"
        }
    }],
    "Order": {
      "PatientOrderId": 1094030,          // Order Id as created by IRIS        
      "Status": "Complete",               // Awaiting Images, Queued Grading, Graded, Cancelled, Review, Error, Complete
      "LocalId": "ORD1234",               // Id of Order as specified by submitting organization              
      "EvaluationTypes": ["DR"],          // DR, Glaucoma, HIV
      "ScheduledTime": null,              // Scheduled Time for exam in local time
      "CreatedTime": "2022-01-01T12:42:18.6929481+00:00",     // Timestamp when order was created
      "ServiceDate": "2022-01-04T12:42:18.6929481+00:00",     // Timestamp when exam was performed
      "DepartmentId": null,               // Optional Department Id
      "EncounterNumber": null,            // Optional Encounter Number
      "StudyInstanceUniqueId": null,      // Optional StudyInstanceUniqueId, typically with DICOM integrated cameras
      "OrderableIdentifier": null,        // Optional OrderableIdentifier, typically 
      "AdditionalInfo": null,             // Optional additional information attached
      "State": "FL",                      // Optional US State of Order (Required for patient home exams)
      "SingleEyeOnly": false,             // If true the order expects images from one eye side only
      "Expedite": false                   // If true the order needs priority routing to next available grader
    },
    "Patient": {
      "LocalId": "1234",                  // Medical record number (or any Id unique to the patient for the submitting organization)
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
      "Name":  {                          
          "Title": "Dr",
          "First": "John",
          "Last": "Doe"	
        },
      "Email": "John.Doe@providers.com",
      "Degrees": "MD",
      "Associations": null
    },
    "Gradings" : {
        "Notes" : [
            {
                "Date":"2022-01-03T12:42:18.6929481+00:00", 
                "Text": null
            }
        ],
        "GradedTime": "2022-01-03T12:42:18.6929481+00:00",  // Timestamp of grading
        "QueuedTime": "2022-01-02T12:42:18+00:00",          // Timestamp when the order was queued to grading
        "CarePlanName":"Return in 6 months",            
        "CarePlanDescription": "Have patient return in 6 months for a followup exam.",
        "Pathology": true,          // If true, pathology was found
        "Urgent": false,            // If true, grader noted urgent pathology to act on immediately
        "Emergent": false,          // If true, the grader noted life threatening pathology that requires immediate ER care.  
        "OD" : {
            "Gradable": true,       // If true the grader was able to make an assessment based on one or more of the provided images
            "MissingEyeReason": null,   // If the order was submitted with a specified reason for no images on an eye, this is that reason
            "UngradableReasons" : [ // If ungradable, contains a list of reasons provided by the grader.  These are not specific to any image
            ],
            "Findings" : [{
                "Finding": "Diabetic Retinopathy",
                "Result": "Mild"
            }]
        },
        "OS": {
            "Gradable": true,
            "Findings" : null
        },
        "DxCodes" : [
            "E083211"
        ],
        "Provider": {                   // Provider who graded the order
            "NPI": "1234567890",                
            "Taxonomy": "207W00000X",
            "Name":  {                          
                "Title": "Dr",
                "First": "John",
                "Last": "Doe"
              },
            "Email": "John.Doe@providers.com",
            "Degrees": "MD",
            "Associations": null
          } 
    },
    "CameraOperator" :  // Technician who captured images
    {
        "UserName": "john.doe@primarycare.com",   
        "Name": {
            "First": "John",
            "Last": "Doe"
        },
        "Notes" : [
            {
                "Date":"2022-01-03T12:42:18.6929481+00:00", 
                "Text": null
            }
        ]
    },
    "HealthPlan":   {  
      "LocalId": "1234",                  // Id of plan as specified by submitting organization
      "Name": "ProviderA",                // Name of the healthplan 
      "MemberId": "1234"                  // Id of Member as specified by the Healthplan
    },
    "Cpt" : {
      "Code" : "92250",
      "Description" : "Fundus photography with interpretation and report"
    }
  }
 
```
