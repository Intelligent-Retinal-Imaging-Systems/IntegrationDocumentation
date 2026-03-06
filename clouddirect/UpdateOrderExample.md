---
title: Update Order
parent: Examples
nav_order: 2
---

# Sample Update OrderRequest Message
##### JSON encoded OrderRequest.

> Updating an order uses the same OrderRequest object used on submission with a differing OrderControlCode (XO). 

Timing is crucial when sending updates to orders.  In some cases, your update request will be entirely ignored.  Other cases will result in the cancellation of the initial order and generation of a new one. The best case for your order getting the updates is before all images have been attached. 

The Order LocalId is the only value used to determine the order you are attempting to update.  If this value does not resolve to a live order in the system, the request is ignored.

The following fields are immutable and therefore ignored when sent differently from the original order:
* Order
  * LocalId
  * EvaluationTypes
* Patient
  * LocalId
 
*The following example results in a name and date of birth change*

```json
{
  "$schema": "https://cdn.retinalscreenings.com/hosts/iris/schemas/order-submission.schema.2.3.1.json",
  "Version": "2.3.1", 	
  "UserNameSubmitting": "john.doe@primarycare.com", 
  "OrderControlCode": "XO",             
  "ClientGuid": "63E3C9EF-66AC-4154-B0C2-494515EB99A7",    
  "Site": {
    "LocalId": "PC1234",
    }                     
  },
  "Camera": {           
    "LocalId": "1234"
    "SerialNumber": "1234",
    "Images": [            
      {
        "LocalId": "1234-1-1", 
        "Taken": "2022-01-01T17:42:18.6936779+00:00",       
        "AzureBlobStorage": {
          "Container": "PC1234",
          "FileName": "04211055-DFF7-41EF-9EF3-43FE61D10D43.dcm",
        },
        "Laterality": "OD"
      }
    ]
  },
  "Order": {
    "EvaluationTypes": ["DR"],          
    "ScheduledTime": "1/1/2025",              
    "LocalId": "ORD1234",               
    "CPTCode": "57554",                     
    "State": "FL"
  },
  "Patient": {
    "LocalId": "1234",                  
    "Name": {
      "First": "John",
      "Last": "Smith"
    },
    "Dob": "12/1/1961",
    "Genders": [
        {
            "Context" : "IdentityGender",
            "Gender" : "M"
        },
        {
            "Context" : "BirthGender",
            "Gender" : "M"
        }
    ],
    "Race": "2131-1",                       
    "PrimaryLanguage": "en-US",            
    "DxCode": "E119"                      
  },
  "OrderingProvider": {                 
    "NPI": "1234567890"
  },
  "CameraOperator" : {
    "NPI":"1234567890",
    "Name":{
      "First":"John",
      "Last":"Doe"
    },
    "Email":"john.doe@primarycare.com"    
  },  
  "HealthPlan":   {                     
    "LocalId": "1234",                  
    "Name": "ProviderA",                 
    "MemberId": "1234",                 
    "PrimaryCareProvider": {            
        "NPI": "1234567890",             
        "EmailAddress": null,           
        "Name":  {                          
            "First": null,
            "Last": null
        },
        "FaxNumber": "4444444444"      
    }
  }
}
```