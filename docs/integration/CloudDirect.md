---
title: Cloud Direct 
---

# IRIS Cloud Direct Integrations

<div style="position:absolute;">

Intelligent Retinal Imaging Systems &#8482;

</div>

<div align="right" >

[Back to EMR Integrations page](/docs/integration/EMRIntegrations)

</div>

## Overview

This document provides details for integrations to the IRIS Platform using cloud provider resources directly accessing the IRIS 3.x platform.

### Acknowledgments 

Specifications version prepared by Lewis Tatham. Please send any feedback to support@irishelp.zendesk.com. 

### Confidentiality and Proprietary Rights 

This document is the confidential property of Intelligent Retinal Imaging Systems (IRIS). No part of this document may be reproduced in any form or incorporated into any information retrieval system without the written permission of IRIS. 

### Disclaimers 

Although unlikely, IRIS reserves the right to make changes in specifications and features shown herein at any time without notice. This does not constitute a representation or documentation regarding the service featured. Contact your IRIS Representative for the most current information. 

Intelligent Retinal Imaging Systems™

2 N Palafox Street, Suite 200 

Pensacola, Florida 32502 

1-888-535-2574 | info@retinalscreenings.com 

## Contents

Introduction ............................................................................................................................................ 3 

Integration Administrator ........................................................................................................................ 3 

Order Submission .................................................................................................................................... 3 

Orders Service Bus Connection String .................................................................................................. 3 

OrderRequest Object Model ................................................................................................................ 4 

OrderControlCode ........................................................................................................................... 4 

Site structure ................................................................................................................................... 4 

Camera structure ............................................................................................................................. 5 

Images array .................................................................................................................................... 5 

AzureBlobStorage structure ............................................................................................................. 6 

OrderingProvider structure .............................................................................................................. 6 

Patient structure .............................................................................................................................. 6 

Order structure ................................................................................................................................ 7 

HealthPlan structure ........................................................................................................................ 8 

PrimaryCareProvider structure ........................................................................................................ 8 

Order Results .......................................................................................................................................... 8 

Azure Service Bus Results .................................................................................................................... 8 

AWS and Google Queues ..................................................................................................................... 9 

Queue Authentication ......................................................................................................................... 9 

Obtaining Iris Azure Service Bus Connection String .......................................................................... 9 

AWS, Azure and Google Service Bus/Queue Connection .................................................................. 9 

OrderResults Object Model ............................................................................................................... 11

ResultsDocument structure ........................................................................................................... 11

ImageDetails structure ................................................................................................................... 11

Images array .................................................................................................................................. 12 

Camera structure ........................................................................................................................... 12 

Gradings structure ......................................................................................................................... 12 

CameraOperator structure............................................................................................................. 13 

HealthPlan structure ...................................................................................................................... 13 

Notes array .................................................................................................................................... 13 

EyeSideGrading structure .............................................................................................................. 13 

Findings array ................................................................................................................................ 13 

Common Shared Structures ................................................................................................................... 13 

Name structure.............................................................................................................................. 13 

Address structure .......................................................................................................................... 14 

Appendix A – Option Enumerations ....................................................................................................... 15 

Race Options ..................................................................................................................................... 15 

Ethnicity Options ............................................................................................................................... 15 

Language Options .............................................................................................................................. 15 

Gender Options ................................................................................................................................. 15 

Marital Status Options ....................................................................................................................... 16 

Result Code Options .......................................................................................................................... 16 

Appendix B – Sample OrderRequest Message ........................................................................................ 17 


# Introduction

As an integration option, Iris provides the ability to submit orders and receive results directly communicating with the cloud service of your preference (Azure, AWS or Google Cloud). If you do not wish to use your own cloud service subscription, Iris can also provide this functionality in the Iris Azure subscription, referred to in this document as Iris Azure Cloud. In all cases, communication is accommodated using the cloud vendors APIs, SDKs or libraries. 

# Integration Administrator

Iris provides access to certain integration tools and configurations though the Integration Administrator role. The role is assigned to you either by Iris support or an existing Organization Administrator for your organization. The term Integration Administrator will be referred to throughout this document thus mentioned here for clarity. 

# Order Submission

Orders are submitted to Iris using an Azure Service Bus Queue. See Azure Service Bus messaging - queues, topics, and subscriptions - Azure Service Bus | Microsoft Docs for an overview of that technology. 

To submit and order, simply send the Json encoded OrderRequest message to the Orders queue. 

C# Example - Get started with Azure Service Bus queues (.NET) - Azure Service Bus | Microsoft Docs 

```
string connectionString = "Endpoint=sb://iris-organization…"; // abbreviated connection string string queueName$= " o r d e r s ^ { \prime }$"; 

string orderRequestMessage = "{$\vert ^ { \prime \prime } V e r \sin \vert ^ { \prime \prime } : \cdots ) ^ { n }$; 11abbreviated OrderRequest message

await await var client = new ServiceBusClient(connectionString);

ServiceBusSender sender = client.CreateSender(queueName);

ServiceBusMessage message = new ServiceBusMessage(orderRequestMessage);

await sender.SendMessageAsync(message);11Fire and forget
```

## Orders Service Bus Connection String 

Because orders are only submitted on a service bus that lives within the Iris Azure subscription, you must obtain the connection string from Iris. This connection string has write-only privileges. To obtain the connection string the Integration Admistrator must perform the following actions: 

Note: If you are beginning in the Iris Test Environment, you will receive the connection string via support email and the following steps are not required. 

• Login the the Iris Administrator application 

Select the “Order Submission” tab 

Iris Cloud DIRECT Integration 

Select Cloud Direct Integration 

Press the “Create Order Submission Gateway” button 

After generating the resource, the connection string will be made available 

## OrderRequest Object Model 

The OrderRequest object model provides all the fields necessary to create an order in the Iris system regardless of your workflow. Most workflows require using only a small subset of the available fields.Fields colored red are required. 

Version (string) – Should be set to 2.3.1 unless otherwise directed.

UserNameSubmitting (string) – Optionally specify the username of a user that should be associated with the order creation. If your organization has been provided a service account for API direct operations, this is acceptable, otherwise it is not required. 

OrderControlCode (options) 

Site (structure) – Location order is associated with 

Camera (structure) – Camera the order should be assigned to 

• Order (structure) – Details of order 

Patient (structure) – Patient details 

OrderingProvider (structure) – Medical provider who ordered the exam 

• CameraOperatorUserName (string) – UserName of the technician who should be assigned to the order 

• HealthPlan (structure) – If order is associated with a Health Plan 

## OrderControlCode 

The OrderControlCode specifies which action to take (use the abbreviation only): 

1. NW – Create New Order 

2. XO – Change Order 

3. CA – Cancel Order 

Regardless of the control code, the same OrderRequest structure is used, however when using the CA code to cancel an order, you only need to populate the ClientGuid, Site LocalId and Order LocalId. 

Changing or Cancelling an order will not work if the target order is closed. Status updates will be supported in the 2022 Fall Release for the Events queue which will allow you to listen for events such as failed updates. 

### Site structure

The Site structure is primarily used to identify the site the order is to be associated with. If your organization is configured as such, sites can be dynamically added, therefore additional fields are provided to supply the required information. If you don’t require automatic site additions, simply provide the LocalId. 

Iris Cloud DIRECT Integration 

#### Site Fields

- LocalId – Id of site as specified by you, the submitting organization
- Name – Name of the site (Only required for automatic site additions)
- Address – Address for site (Only required for automatic site additions) 

### Camera structure 

When an order is to be assigned to a camera or Image directives are included with the order, populate this structure. If the camera already exists and you are not providing image directives, you only need to supply the LocalId. Other than the Images structure, the remaining fields are provided in the event your organization allows automatic Camera additions. 

#### Camera Fields: 

- LocalId – Typically this is the serial number of the Camera. Because Iris supports a wide variety of cameras, some of which do not identify within image metadata, you may have to consult with Iris to find the proper value to supply here. 
- Location – Optionally specify a location where the camera is located. This is optional even when attempting to add a camera. 
- IPAddress – When specified, the camera is identified by the source IP Address as images are received. This is an atypical workflow and should only be used under direct request from Iris. 
- MACAddress – Optional identifier for informational purposes only 
- SerialNumber – Serial Number of Camera 
- Manufacturer – Name of camera manufacturer. Consult with Iris for exact values you should use. 
- Model – Model name of camera. Consult with Iris for exact values you should use.
- SoftwareVersion – Version of camera software. Consult with Iris for exact values you should use.
- Images (array of Image structure) – Provide image directives. This field is used when the workflow is started with the simultaneous receipt of order and images. 

### Images array 

The Images array is an array of Image structures that provides details including the storage location of one or more images associated with the order. 

### Image structure 

The Image structure allows you to specify details including the storage location where an image file can be retrieved. At this time, image retrieval is only supported in Azure Blob Storage. 

The Image structure has the following fields: 

- LocalId – Id as specified by the submitting organization
- Taken – DateTimeOffset when the image was taken
- AzureBlobStorage – structure with blob storage location information 
- Laterality (options) – OD, OS 
- ImageContext (options) – Primary, Secondary, Component, Aggregate, Enhancement – Unless otherwise directed, Primary should be used. Non-primary images are not prominently displayed throughout the workflow. 
- ParentLocalId – If the image is a child of another image in the set, this is the LocalId value for that parent image 
- GroupId – If this image is part of an overall group of images, specify the group id here 
- GroupOrdinal – If this image is part of a group (specified by GroupId) this is the relative position in that group. 

### AzureBlobStorage structure 

Files in Azure Blob storage are specified by a container and filename. The Blob Storage Location in Azure is specific to an Azure Blob Storage resource of which connectivity access is specified in the Adminstrator application. The structure has the following fields: 

- Container – Name of the container 
- FileName – name of the file found in the container 

## OrderingProvider structure

The OrderingProvider structure allows you to specify the Provider ordering the exam. Previously submitted providers can be looked up by NPI, thus not requiring the full definition. If your workflow is configured to have a default ordering provider, it is not necessary to include this information. However, if you are not configured for a default ordering provider, the order will error. 

If you are providing an NPI that links to a previously used Provider, NPI is the only required field. Otherwise, Name is the only requiement. 

While NPI and Taxonomy are not required, it could have downstream effects on the order results if that information is expected. 

- NPI – Providers National Identifier 
- Taxonomy – Optionally specify Taxonomy relavant to the action 
- Name – First, Last name
- Email – Optionally specify an email address 
- Degrees – Optionally supply degrees 
- Associations – Optionall supply associations 

### Patient structure

Iris allows submitting detailed information on a patient, however, in most workflows the only requirement is Id, Name, DOB and Gender. 

Providing the starting DxCode (ICD-10) serves as the foundation for a fully qualified ICD-10 code when pathology is found. 

- LocalId – Id of patient as specified by the submitting organization. Typically this will the the Patient MRN. 
- Name – Patient first and last name
- Dob – Patient date of birth 
- Gender (options) – Patient Gender abbriation 
- Race (options) – Optional patient information
- Ethnicity (options) – Optional patient information 
- PrimaryLanguage (options) – Optional patient information 
- MaritalStatus (options) – Optional patient information 
- Email – Optional patient information 
- Address – Optional patient information 
- DxCode – ICD-10 starting diagnosis (default: E08) 

## Order structure 

What you provide in the Order structure is highly dependent on your workflow. While the only required field is the Evaluation Type to perform, other fields may be required in your workflow. For example, the State field is required for mobile type exams where the location of the exam (where the images are taken) is in a different state than the Site the exam is tied to. See the description of each field for more details. 

The Iris system allows only one open order per patient/evaluation type combination. When using the LocalId, previous (open) orders could automatically be cancelled in favor of the newer order. For this reason, it is recommended that you supply the LocalId field so the system can more clearly identify when cancellations are the desired outcome. 

EvaluationTypes (array of options) – Specifies which evaluations to perform. Typically, only one evaluation is performed in an order but the Iris system can support multiple thus usage of an array for this field. Options are : DR, Glaucoma, and HIV 

ScheduledTime – When orders are scheduled for a specific time, this should be that time local to the exam location. This is typically used for workflows where orders are pushed to Cameras as this determines which items show in a Camera worklist 

LocalId – The Id of the order as specified by the submitting organization. This id is required for subsequent Change and Cancel operations. 

• DepartmentId – Optional identifier for the submitting department. Some EMR integrations will require this. 

EncounterNumber - Optional identifier for the encounter that generated the order. Some EMR integrations will require this field. 

StudyInstanceUniqueId - Optional Identifier, typically used with DICOM integrated cameras 

OrderableIdentifier – Optional identifier 

CPTCode – Procedure code 

AdditionalInfo – Free form field for edge cases 

• State – US State where exam is to be performed. Required for mobile exams that will not be performed at the address specified in the Site. This takes either the State abbreviation or Full name 

• SingleEyeOnly (true/false) – If true, the order will not delay in the image pipeline after images are received on one eye. 

Urgent (true/false) – If true the order is prioritized in the grading queue 

## HealthPlan structure 

If your workflow is based on a Health Plan, this structure may be included in the submission. This information is returned in results. 

If your workflow includes PCP results delivery, you may specify that Provider here.

• LocalId – Id of Plan as specified by the submitting organization 

• Name – Name of the Health Plan 

•  MemberId –Id for the HealthPlan member, typically as specified by the Health Plan itself 

• IndividualId – Id for the Individual person associated with the Member for the HealthPlan 

PrimaryCareProvider (structure) – Contains Provider information for the PCP of the Member.This information can be used for results submission directly to that provider. 

## PrimaryCareProvider structure 

Provider details for PCP. 

• NPI – National Id for Provider 

• EmailAddress – Email Address for the provider 

• Name – First, Last 

FaxNumber – If so configured, number is an alternate delivery path for results

## Order Results

Cloud direct results may be received in a variety of ways: 

### Queue Based Results 

o Iris Azure Cloud Service Bus – Receive complete results on a service bus queue manintained by Iris 

o Azure Service Bus – Receive complete results on a service bus queue in your own subscription 

o AWS Queue – Receive complete results on an AWS Queue in your own subscription

o Google Queue – Receive complete results on a Google Queue in your own subscription • Queue based notifications 

o Receive a notification of ready results in which a subsequent call to the Iris results API is required 

o For Iris Azure Cloud Service Bus, this option Is required if message sizes exceed 256K bytes. Results do not typically exceed this size, except when high resolution cameras are used for images that are embedded in the report. 

### Azure Service Bus Results 

To receive an order using an Azure Service Bus Queue, you simply attach a notification handler to the Results queue. 

C# Example - Get started with Azure Service Bus queues (.NET) - Azure Service Bus | Microsoft Docs 

string connectionString = "Endpoint=sb://iris-organization…"; // abbreviated connection string string queueName = "Results"; 

Iris Cloud DIRECT Integration 

await using ServiceBusProcessor processor = client.CreateProcessor(queueName, new ServiceBussProcessorOptions()); 

processor.ProcessMessageAsync += MessageHandler;

await processor.StartProcessingAsync();

async Task MessageHandler(ProcessMessageEventArgs args)

{

string resultsJson = args.Message.Body.ToString();

await args.CompleteMessageAsync(args.Message);

}

### AWS and Google Queues

It is assumed that the choice to use AWS or Google Queue indicates a preexisting knowledge of how those resources work, therefore no coding examples are provided here. Regardless of the transport mechanism, the payload (OrderResults Object) is the same. 

### Queue Authentication

Regardless of the cloud platform, some form of connection credentials are required for access to the resource. When using Iris Azure Cloud resources, you must obtain the connection string from the Administrator application as a user with the Integration Administrator role. Otherwise you must supply the credentials in the Administrator application. 

Obtaining Iris Azure Service Bus Connection String 

Similar to Orders submiision the connection string for the Results Service Bus is obtained in the Adminstrator application. This connection string has read-only privileges. 

• Login the the Iris Administrator application 

• Navigate to the EMR integration page 

• Select the “Result Delivery” tab

Select “Cloud Queue” under primary delivery methods 

Select “IRIS Azure Cloud” from the cloud service provider options

Press the “Create Gateway” button 

After generating the resource, the connection string will be made available 

AWS, Azure and Google Service Bus/Queue Connection

To configure results to be pushed to an AWS, Azure (In your subscription) or Google Queue, the Integration Administrator must perform the following actions: 

Login to the Iris Administrator application 

Navigate to the EMR Integration page 

Select the “Result Delivery” tab 

• Select “Cloud Queue” under primary delivery methods 

• Select AWS, AZURE or Google from the cloud service provider options

• Configure the following fields for AWS 

o Queue Name 

o Queue ARN 

Queue Url 

Region Name 

AWS Access Key Id 

AWS Secret Access Key 

• Configure the following fields for AZURE 

o Queue Name 

o Connection String 

• Configure the following fields for Google 

 Queue Name 

o Connection JSON 

### OrderResults Object Model

The OrderResult object model has the following root level fields: 

Version (string) – Should be set to 2.3.1 unless otherwise directed. 

Timestamp – Timestamp when item was posted to the Results Queue 

TransactionId – Guid unique to the communication (resends will have a unique value) 

ResultCode (options) 

Site (structure) – Same structure as Submission 

ResultsDocument (structure) 

ImageDetails (structure) – Details on images submitted in the order

Images (array of Image structure) - Contains metadata for each image submitted 

Order (structure) – Details of order most of which is eched from the Submission

Patient (structure) – Details of patient which is echoled from the Submission 

OrderingProvider – Details of provider who ordered the exam which is echoed from the Submission 

• Gradings (structure) – Grading details of the order 

CameraOperator (structure) - Details of the user that captured images 

HealthPlan (structure) – Details of the Health Plan associated with the order

### ResultsDocument structure 

Depending on your workflow the Iris system will provide a Report of the examination. Iris provides this content in various formats: 

• Type (options) – PDF, HTML, ORU 

Encoding (options) – Base64, ASCII or any specific encoding scheme 

Content – Actual content relative to the Encoding and Type. For example, if PDF, this will most likely be a Base64 encoded string 

### ImageDetails structure 

This structure contains a summary of the images collected for the exam.

• TotalCount (int) – Total count of all images attached to the order 

RightEyeCount (int) – Total count of all right eye images attached to the order 

RightEyeOrginalCount (int) – Count of right eye images submitted to the order (from Camera Operator) 

• RightEyeEnhancedCount (int) – Count of enhanced right eye images attached to the order 

LeftEyeCount (int) – Total count of all left eye images attached to the order 

• LeftEyeOrginalCount (int) – Count of left eye images submitted to the order (from Camera Operator) 

• LeftEyeEnhancedCount (int) – Count of enhanced left eye images attached to the order 

• Preferred (true/false) – If true this image was selected as preferred for the report 

• SingleEyeOnly (true/false) – If true only one eye was captured for the exam. This is not bound to the SingleEyeOnly field in the submission. 

Iris Cloud DIRECT Integration 

#### Images array 

The Images array is an array of Image structures that provides details of each image attached to the order. 

#### Image structure 

The Image structure contains details of an individual image attached to the order.

The Image structure has the following fields: 

• LocalId – Id as specified by the submitting organization 

• Taken – DateTimeOffset when the image was taken 

Received – DateTimeOffset when the image was received to the Iris system

FileName – Name of file as stored 

Laterality (options) – OD, OS 

ImageContext (options) – Primary, Secondary, Component, Aggregate, Enhancement – Unless otherwise directed, Primary should be used. Non-primary images are not prominently displayed throughout the workflow. 

• ParentLocalId – If the image is a child of another image in the set, this is the LocalId value for that parent image 

• GroupId – If this image is part of an overall group of images, specify the group id here 

• GroupOrdinal – If this image is part of a group (specified by GroupId) this is the relative position in that group. 

• Camera (structure) – Contains details of the Camera that took the image 

#### Camera structure 

The Camera structure contains details of the camera that took the image. 

LocalId – Typically this is the serial number of the Camera. Because Iris supports a wide variety of cameras, some of which do not identify within image metadata, you may have to consult with Iris to find the proper value to supply here. 

• Location – Optionally specify a location where the camera is located. This is optional even when attempting to add a camera. 

• IPAddress – When specified, the camera is identified by the source IP Address as images are received. This is an atypical workflow and should only be used under direct request from Iris. 

• MACAddress – Optional identifier for informational purposes only 

SerialNumber – Serial Number of Camera 

• Manufacturer – Name of camera manufacturer. Consult with Iris for exact values you should use. 

• Model – Model name of camera. Consult with Iris for exact values you should use.

SoftwareVersion – Version of camera software. Consult with Iris for exact values you should use.

### Gradings structure 

• Notes (array of Note structure) – Notes added by the Grader 

• Graded – Timestamp when grading was completed 

• CarePlanName – Name of Care Plan determined from findings 

Iris Cloud DIRECT Integration 

• CarePlanDescription – Description/Instruction text related to care plan

Pathology (true/false) – If true Pathology was found on one or more eyes 

Urgent (true/false) – If true, the grader has found pathology that requires urgent action

OD (EyeSideGrading structure) – Details of grading for right eye 

OS (EyeSideGrading structure) – Details of grading for left eye 

DxCodes (array of string) – ICD-10 Codes matched to findings 

Provider (structure) – Details of the Provider who performed the grading 

### CameraOperator structure

Contains details of the technician who captured the images for the order.

• UserName – (Iris) UserName 

• Name – First/Last Name 

Notes (array of Note structure)

### HealthPlan structure 

• LocalId – Id of plan as specified by submitting organization 

Name – Name of HealthPlan 

MemberId - Id of Member as specified by the Healthplan

#### Notes array 

The notes array contains zero or more notes added by the related user 

#### Note structure 

Date – Date / Time value note was entered

Text – Content of note 

#### EyeSideGrading structure 

Gradable (true/false) – If false the eye side was not able to be graded with the images provided

UngradableReasons (array of string) – one or more reasons why the eye side could not be graded (This field is not guaranteed to be populated when an eye is ungradable). 

Findings (array of Finding structure)

#### Findings array 

Findings is an array of the Finding structure containing findings from the grader for the specified eye. If the array is not present, it indicates, there was no pathology found for the eye. 

#### Finding structure 

Finding – Type of pathology noted (e.g.: Diabetic Retinopathy) 

Result – Level of pathology (e.g.: Mild, Moderate, Positive, etc…)

### Common Shared Structures

Name structure 

• First 

Iris Cloud DIRECT Integration 

• Last 

Address structure 

• Street1

• Street2 

• City 

• State 

PostalCode 

### Appendix A – Option Enumerations 

#### Race Options

• 1002-5 - American Indian or Alaska Native 

• 2028-9 - Asian 

• 2054-5 - Black or African American 

• 2076-8 - Native Hawaiian or Other Pacific Islander 

• 2131-1 - Other Race 

• 2106-3 – White 

#### Ethnicity Options 

You may use any of the HL7 Ethnicity codes listed here: http://terminology.hl7.org/CodeSystem/v3-Ethnicity 

Specify the Code portion only when populating the Ethnicity field. 

Here is an abbreviated list: 

• 2137-8 - Spaniard 

• 2148-5 - Mexican

• 2155-0 - Central American 

• 2180-8 - Puerto Rican 

• 2182-4 - Cuban 

• 2149-3 - Mexican American 

#### Language Options

You may use any HL7 Language code as found here: Valueset-languages - FHIR v4.0.1 (hl7.org) 

Use the code portion only when populating the Language field. 

Here is an abbreviated listing: 

• en - English 

• en-US – US English 

• fr - French 

• es - Spanish

it - Italian 

pt - Portuguese 

• zh – Chinese 

##### Gender Options 

Use the abbreviated code only when populating the Gender field. 

• U – Unspecified 

• M – Male 

• F – Female 

• N – Non binary 

Iris Cloud DIRECT Integration 

O – Other 

• TM – Transgender Male 

TF – Transgender Femail 

ND – Non disclosed 

#### Marital Status Options 

Items in this list are based on the HL7 standared here: http://terminology.hl7.org/CodeSystem/v3-MaritalStatus 

Use the single letter code only when populating the Marital Status field. 

• A – Annulled 

D – Divorced 

C – Common Law 

I – Interlocutory 

L – Legally Separated 

M – Married 

P – Polygamous 

S – Never Married 

T – Domestic partner 

W – Widowed 

### Result Code Options

One of the following codes will be specified on the results which identifies the context in which it was sent: 

• A – Addendum 

• C – Correction 

• F – Final 

• P – Preliminary 

R - Resend 

### Appendix B – Sample OrderRequest Message

{ 

"Version": "2.3.1",

"UserNameSubmitting": "john.doe@primarycare.com",

"OrderControlCode": "NW",

"ClientGuid": "63E3C9EF-66AC-4154-B0C2-494515EB99A7",

"5ite":

"LocalId": "PC1234",

"Name": null,

$" A d d r e s s ^ { \prime \prime } : ($

"Street1": null,

"Street2": null,

"City":nul1,

"State":null,

"PostalCode":null

}

},

"Camera": {

"LocalId": null,

"Location": null,

"IPAddress": null,

"MACAddress": null,

"SerialNumber": "1234",

"Manufacturer": null,

"Model": null,

"SoftwareVersion": null,

"Images": [

{

"LocalId": "1234",

"Taken": "2022-01-01T17:42:18.6936779+00:00",

"AzureBlobStorage": { 

"Container": "PC1234",

"FileName": "04211055-DFF7-41EF-9EF3-43FE61D10D43.dcm"

},

"Laterality": "OD",

"ImageContext": "Primary",

"ParentLocalId": null,

"GroupId": null,

"GroupOrdinal": null

 }

]

},

"Order": {

"EvaluationTypes": ["DR"],

"ScheduledTime": null,

"CreatedTime": "2022-01-01T12:42:18.6929481-05:00",

"LocalId": "ORD1234",

"DepartmentId": null,

"EncounterNumber": null,

"StudyInstanceUniqueId": null,

"OrderableIdentifier": null,

"CPTCode": null,

"AdditionalInfo": null,

"State": "FL",

"SingleEyeOnly": false,

"Urgent": false

},

"Patient": {

"LocalId": "1234",

$N a m e ^ { n } : f$

$" F i r s t " : " j o h n ^ { n } ,$

"Last":"DOe"

}

"Dob":"1/1/2000",

"Gender":"U",

"Race": null,

"Ethnicity": null,

"PrimaryLanguage": null,

"MaritalStatus": null,

"Email": null,

"AdditionalInfo": null,

"Phone": null,

"Address": {

"Street1": null,

"Street2": null,

"City":null,

"State":null,

"PostalCode":null

},

"DxCode": null

},

"OrderingProvider": {

"NPI": "1234567890",

"Taxonomy": null,

"Name": { 

"First": null,

"Last": null

},

"Email": null,

"Degrees": null,

"Associations": null

},

"CameraOperatorUserName": "john.doe@primarycare.com",

"HealthPlan": {

"LocalId": "1234",

"Name": "ProviderA",

"MemberId": "1234",

"PrimaryCareProvider": {

"NPI": "1234567890",

"EmailAddress": null,

"Name": {

"First": null,

"Last": null

},

"FaxNumber": "4444444444"

 }

}

#### Appendix C – Sample OrderResults Message 


| {  |  |
| -- | -- |
|  "Version": " | 2.3.1", // Version of this structure  |
|  "Timestamp"  "Transaction | : "", Id": "",  |
|  "ResultCode" "Site": {  | : "F", // P=Preliminary, A=Addendum, F=Final, C=Correction, R=Resend  // Site/Location the Order is assigned to  |
|  "LocalId": },  |  "PC1234" // Id of site as defined by submitting organization  |
|  "ResultsDocu | ment": {  |
|  "Type":  "Encodin | "PDF", // PDF, HTML, ORU g": "Base64", // Base64, HL7 or specific encoding scheme  |
|  "Content },  | ": "..." // Actual Content  |
|  "ImageDetail "TotalCo | s" : { unt":0,  |
|  "RightEy | eCount": 0,  |
|  "RightEy "RightEy | eOriginalCount": 0, eEnhancedCount": 0,  |
|  "LeftEye "LeftEye | Count": 0, OriginalCount": 0,  |
|  "LeftEye "Preferr | EnhancedCount": 0, ed": true, // True, False If True the image is marked as being preferred for reports |
|  "SingleE },  | yeOnly": false // If true the order expects images from one eye side only  |
|  "Images": [{ |   |
|  "LocalId "Taken": | ": null, // Id of image as specified by submitting organization  "2022-01-02T17:42:18.6936779+00:00", // Timestamp when Image was taken  |
|  "Receive "FileNam | d": "2022-01-02T17:42:18.6936779+00:00", // Timestamp when image was received by Iris e": "9298DA56-E516-40E3-A35D-41B5D238DC7D.jpg", // Filename of image  |
|  "Lateral "ImageCo | ity": "OD", // OD, OS ntext": "Primary", // Primary, Secondary, Component, Aggregate, Enhancement  |
|  "ParentL | ocalId": null, // If child of other image, that image's LocalId  |
|  "GroupId "GroupOr | ": null, // Optional Grouping context dinal": null, // Optional Ordinal of image in group context by results receiving organization |
|  "Camera" "Loc | : { alId": "REM-1000", // Specifies Camera Id as defined by submitting organization  |
|  "Loc "IPA | ation": null, // Optional Camera location details ddress": null, // Optional IP Address assignment of camera  |
|  "MAC | Address": null, // Optional MAC Address of camera NIC  |
|  "Ser "Man | ialNumber": "REM-1000", // Serial Number of Camera ufacturer": "Remidio", // Manufacturer of Camera  |
|  "Mod "Sof | el": "NMFOP", // Model Name of Camera twareVersion": "2.2.23"  |
|  }  },  |  |
|  {  |  |
|  "LocalId "Taken": | ": null, // Id of image as specified by submitting organization  "2022-01-02T17:42:18.6936779+00:00", // Timestamp when Image was taken  |
|  "Receive "FileNam | d": "2022-01-02T17:42:18.6936779+00:00", // Timestamp when image was received by Iris e": "04211055-DFF7-41EF-9EF3-43FE61D10D43.jpg", // Filename of image  |
|  "Lateral "ImageCo | ity": "OS", // OD, OS ntext": "Primary", // Primary, Secondary, Component, Aggregate, Enhancement  |
|  "ParentL "GroupId | ocalId": null, // If child of other image, that image's LocalId ": null, // Optional Grouping context  |
|  "GroupOr | dinal": null, // Optional Ordinal of image in group context by results receiving organization |
|  "Camera" "Loc | : { alId": "REM-1000", // Specifies Camera Id as defined by submitting organization  |
|  "Loc "IPA | ation": null, // Optional Camera location details ddress": null, // Optional IP Address assignment of camera  |
|  "MAC "Ser | Address": null, // Optional MAC Address of camera NIC ialNumber": "REM-1000", // Serial Number of Camera  |
|  "Man | ufacturer": "Remidio", // Manufacturer of Camera  |
|  "Mod "Sof | el": "NMFOP", // Model Name of Camera twareVersion": "2.2.23"  |
|  }  }],  |  |
|  "Order": {  "Status":  | "Complete", // Awaiting Images, Queued Grading, Graded, Cancelled, Review, Error, Complet |
|  "LocalId": |  "ORD1234", // Id of Order as specified by submitting organization  |
|  "Evaluatio "Scheduled | nTypes": ["DR"], // DR, Glaucoma, HIV Time": null, // Scheduled Time for exam in local time  |
|  "CreatedTi "ServiceDa | me": "2022-01-01T12:42:18.6929481-05:00", // Timestamp when order was created te": "2022-01-04T12:42:18.6929481-05:00", // Timestamp when exam was performed  |
|  "Departmen "Encounter | tId": null, // Optional Department Id Number": null, // Optional Encounter Number  |
|  "StudyInst "Orderable | anceUniqueId": null, // Optional StudyInstanceUniqueId, typically with DICOM integrated cameras Identifier": null, // Optional OrderableIdentifier, typically  |
|  "Additiona | lInfo": null, // Optional additional information attached  |
|  "State": " "SingleEye | FL", // Optional US State of Order (Required for patient home exams) Only": false, // If true the order expects images from one eye side only  |
|  "Expedite" },  | : false // If true the order needs priority routing to next available grader  |
|  "Patient": { "LocalId": |   "1234", // Medical record number (or any Id unique to the patient for the submitting  |
|  "Name": {  "First": "Last":  },  |  "John",  |
|  "Name": {  "First": "Last":  },  | "Doe"  |


},

"Dob": "1/1/2000",

"Gender": "U"

 },

"OrderingProvider": {

 "NPI": "1234567890",

"Taxonomy": "207W00000X",

"Name": { 

"Title": "Dr"

"First": "John",

"Last":"Doe"

},

"Email": "John.Doe@providers.com",

"Degrees": "MD",

"Associations": null

},

"Gradings" : { 

"Notes" : [

 { 

"Date":"2022-01-03T12:42:18.6929481-05:00",

"Text": null 

 } 

],

"GradedTime": "2022-01-03T12:42:18.6929481-05:00", // Timestamp of grading

"CarePlanName":"Return in 6 months",

"CarePlanDescription": "Have patient return in 6 months for a followup exam.",

"Pathology": true,  // If true, pathology was found 

"Urgent": false,  // If true, grader found urgent pathology to act on immediately

"OD" : { 

"Gradable": true,  // If true the grader was able to make an assessment based on one or more of the provided images

"UngradableReasons" : [ // If ungradable, contains a list of reasons provided by the grader. These are not specific to any image

], "Findings" : [{

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

"Provider": {  // Provider who graded the order

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

"CameraOperator" : // Technician who captured images

{

"UserName": "john.doe@primarycare.com",

"Name": {

"First": "John",

"Last": "Doe"

},

"Notes" : [

"Date":"2022-01-03T12:42:18.6929481-05:00",

"Text": null 

 } 

 ] 

},

"HealthPlan":  { 

"LocalId": "1234", // Id of plan as specified by submitting organization 

"Name": "ProviderA", // Name of the healthplan

"MemberId": "1234"  // Id of Member as specified by the Healthplan

 }

 } 



