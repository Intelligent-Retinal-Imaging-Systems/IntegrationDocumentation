---
title: Order Request Example
parent: Cloud Direct
nav_order: 2
---

# Sample OrderRequest Message
##### JSON encoded Order Request.


> ✨ <small>By including the schema reference (as shown in the example below) you can leverage tools such as Visual Studio Code to expose issues in your submission object.  The schema also provides detailed descriptions for each field including available options for enumerations.</small>

* <small>*Unused properties may be omitted from your object. Items hydrated with <span style="color:red;">null</span> below are for contextual display purposes only.* </small>

```json
{
  "$schema": "https://cdn.retinalscreenings.com/hosts/iris/schemas/order-submission.schema.2.3.1.json",
  "Version": "2.3.1", 	
  "UserNameSubmitting": "john.doe@primarycare.com", 
  "OrderControlCode": "NW",             
  "ClientGuid": "63E3C9EF-66AC-4154-B0C2-494515EB99A7",    
  "Site": {
    "LocalId": "PC1234",
    "Name": null,       
    "Address": {         
        "Street1": null,
        "Street2": null,
        "City":null,
        "State":null,
        "PostalCode":null
    }                     
  },
  "Camera": {           
    "LocalId": "1234",    
    "Location": null,   
    "IPAddress": null,  
    "MACAddress": null, 
    "SerialNumber": "1234",
    "Manufacturer": null,  
    "Model": null,         
    "SoftwareVersion": null,
    "Images": [            
      {
        "LocalId": "1234-1-1", 
        "Taken": "2022-01-01T17:42:18.6936779+00:00",       
        "AzureBlobStorage": {
          "Container": "PC1234",
          "FileName": "04211055-DFF7-41EF-9EF3-43FE61D10D43.dcm",
        },
        "Laterality": "OD",             
        "ImageContext": null,      
        "ParentLocalId": null,          
        "GroupId": null,                
        "GroupOrdinal": null            
      }
    ]
  },
  "Order": {
    "EvaluationTypes": ["DR"],          
    "ScheduledTime": "1/1/2025",              
    "LocalId": "ORD1234",               
    "DepartmentId": null,               
    "EncounterNumber": null,            
    "StudyInstanceUniqueId": null,      
    "OrderableIdentifier": null,         
    "CPTCode": "57554",                     
    "AdditionalInfo": null,             
    "State": "FL",                      
    "SingleEyeOnly": null,
    "MissingEyeReason": null,
    "Urgent": false                     
  },
  "Patient": {
    "LocalId": "1234",                  
    "Name": {
      "First": "John",
      "Last": "Doe"
    },
    "Dob": "1/1/2000",
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
    "Ethnicity": null, 
    "PrimaryLanguage": "en-US",            
    "MaritalStatus": null,              
    "Email": null,                      
    "AdditionalInfo": null,             
    "Phone": null,                      
    "Address": {                         
      "Street1": null,
      "Street2": null,
      "City":null,
      "State":null,
      "Zip":null
    },
    "DxCode": "E119"                      
  },
  "OrderingProvider": {                 
    "NPI": "1234567890",                
    "Taxonomy": null,
    "Name":  {                          
        "First": null,
        "Last": null
      },
    "Email": null,
    "Degrees": null,
    "Associations": null
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