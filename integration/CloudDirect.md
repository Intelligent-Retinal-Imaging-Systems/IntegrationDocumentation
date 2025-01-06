---
title: Cloud Direct 
parent: Order Processing Integration
nav_order: 2
has_toc: false
---

# IRIS Cloud Direct Integrations
{: .no_toc }
 
This document provides details for integrations to the IRIS Platform using cloud provider resources directly accessing the IRIS 3.x platform.

<details markdown="block">
  <summary>
    Table of contents
  </summary>
  {: .text-delta }
- TOC
{:toc}
</details>

----

# Introduction

As an integration option, IRIS provides the ability to submit orders and receive results directly communicating with the cloud service of your preference (Azure, AWS or Google Cloud). 

*If you do not wish to use your own cloud service subscription, IRIS can also provide this functionality in the IRIS Azure subscription, referred to in this document as **IRIS Azure Cloud**.* 

In all cases, communication is accommodated using the cloud vendors APIs, SDKs or libraries. For many languages, IRIS provides native libraries,referred to as the IRIS Public libraries, to abstract the Cloud operations and to provide serialization and deserialization from the data models. 


# Integration Administrator

IRIS provides access to certain integration tools and configurations though the Integration Administrator role. The role is assigned to you either by IRIS support or an existing Organization Administrator for your organization. The term Integration Administrator will be referred to throughout this document thus mentioned here for clarity. 


# Developers                                                                                       
IRIS provides libraries for most of the popular programming languages on our [Developer Resources](/integration/DeveloperResources/) page.

# Order Submission

Orders are submitted to IRIS using an Azure Service Bus Queue

The process involves hydrating and sending a JSON encoded OrderRequest object to the orders queue

*If you are planning to use an IRIS Public library, the act of serializing and sending the data is reduced to a single step within the library.*

C# Example

```csharp
async Task Test()
{
    string connectionString = "Endpoint=sb://iris-organization…"; // abbreviated connection string 
    string queueName= "orders"; 
    string orderRequestMessage = "[JSON Encoded OrderRequest object]"
    await await var client = new ServiceBusClient(connectionString);
    ServiceBusSender sender = client.CreateSender(queueName);
    ServiceBusMessage message = new ServiceBusMessage(orderRequestMessage);
    await sender.SendMessageAsync(message); // Fire and forget
}
```

## What you need to get started
Before you can submit an order using Cloud Direct services, the are several pieces of data you will need from IRIS:
1. Service Bus Connection String
2. Your Organization Identifier referred to as **ClientGuid**
3. Site identifier(s)

### Orders Service Bus Connection String 

Because orders are only submitted on a service bus that lives within the IRIS Azure subscription, you must obtain the connection string from IRIS. This connection string has write-only privileges. To obtain the connection string contact Contact <a href="mailto:support@irishelp.zendesk.com">IRIS Support</a>. 

### Organization Identifier
Created by IRIS during provisioning, this is a GUID value passed into all order submissions, uniquely identifying your organization.

### Site Identifiers
Depending on your specific needs you will have one to many sites within the IRIS system assigned to your organization.  Orders have a direct relationship to the site therefore an identifier for the site must be included in your submission.

If you operate within a brick and mortar type model, you typically will want to have one site in the IRIS system per physical location your cameras reside.  If you operate more in a mobile workflow, you typically have a single site.  In the multisite mode, the state where the exam is performed is assumed to be the state configured on the site record within IRIS.   If you operate in a single site mode, you must provide the state where the exam occurs in the order object.  

For single site workflows, IRIS will provide you with the identifier to supply for the Site.  This because it's not an identifier you established yourself.

For multisite workflows, you will provide IRIS with your identifiers for each site as they are added.  This can be done programmatically through this interface or through the Administrator application. If added from this interface you must include all the required properties for adding a new site in the Site structure.  This is described in full detail [in the site structure section](#site-structure).

# OrderRequest Object Model 

The OrderRequest object model provides all the properties necessary to create an order in the IRIS system regardless of your workflow. Most workflows require using only a small subset of the available properties. Properties colored <span style='color: rgb(188, 13, 16);'>red</span> are required. 


| Property  | type  |  Description  | Options
| -- | -- | -- | -- |
| <span style='color:rgb(188, 13, 16);'>Version</span> | string |  Should be set to 2.3.1 unless otherwise directed.
| UserNameSubmitting | string | Optionally specify the username of a user that should be associated with the order creation. If your organization has been provided a service account for API direct operations, this is acceptable, otherwise it is not required. 
| <span style='color: rgb(188, 13, 16);'>OrderControlCode</span> | options | Specifies the operation that should be performed with the order data (add/change/cancel) | [OrderControlCode](#ordercontrolcode) options
| <span style='color: rgb(188, 13, 16);'>Site</span> | [Site](#site-structure) structure | Location order is associated with
| Camera | [Camera](#camera-structure) structure | Camera the order should be assigned to as well as optionally specifying the images associated with the order and camera
| <span style='color: rgb(188, 13, 16);'>Order</span> | [Order](#order-structure) structure | Details of order
| <span style='color: rgb(188, 13, 16);'>Patient</span> | [Patient](#patient-structure) structure | Patient details
| OrderingProvider | [Request Provider](#requestprovider-structure) structure | Medical provider who ordered the exam
| ReferringProvider | [Request Provider](#requestprovider-structure) structure | Medical provider who referred the patient for the exam
| CameraOperator | [Request Provider](#requestprovider-structure) structure | Medical provider assigned to perform the exam. This option is used when the Operator is a medical provider with a valid NPI 
| CameraOperatorUserName | string | UserName of the technician who should be assigned to the order. This option is used when the operator does not have an NPI 
| HealthPlan | [HealthPlan](#healthplan-structure) structure | If order is associated with a Health Plan

## OrderControlCode 

The OrderControlCode specifies which action to take

| Value | Description
| -- | -- 
| **NW** | Create New Order
| **XO** | Change Order 
| **CA** | Cancel Order 

Regardless of the control code, the same OrderRequest structure is used, however when using the CA code to cancel an order, you only need to populate the ClientGuid, Site LocalId and Order LocalId. 

Changing or Cancelling an order will not work if the target order is closed. 

## Order Model structures
The OrderRequest models contains the following properties

### Site structure

The Site structure is primarily used to identify the site the order is to be associated with. If your organization is configured as such, sites can be dynamically added, therefore additional properties are provided to supply the required information. If you don’t require automatic site additions, simply provide the LocalId. 


| Property | Type | Description 
| -- | -- | -- 
| LocalId | string | Id of site as specified by you, the submitting organization
| Name | string | Name of the site (Only required for automatic site additions)
| Address | [Address](#address-structure) structure | Address of site (Only required for automatic site additions)

### Camera structure 

When an order is to be assigned to a camera or Image directives are included with the order, populate this structure. If the camera already exists and you are not providing image directives, you only need to supply the LocalId. Other than the Images structure, the remaining properties are provided in the event your organization allows automatic Camera additions. 


| Property | Type | Description 
| -- | -- | -- 
| LocalId | string | Typically this is the serial number of the Camera. Because IRIS supports a wide variety of cameras, some of which do not identify within image metadata, you may have to consult with IRIS to find the proper value to supply here. 
| Location | string | Optionally specify a location where the camera is located. This is optional even when attempting to add a camera. 
| IPAddress | string | When specified, the camera is identified by the source IP Address as images are received. This is an atypical workflow and should only be used under direct request from IRIS 
| MACAddress | string | Optional identifier for informational purposes only 
| SerialNumber | string | Serial Number of Camera 
| Manufacturer | string | Name of camera manufacturer. Consult with IRIS for exact values you should use. 
| Model | string | Model name of camera. Consult with IRIS for exact values you should use.
| SoftwareVersion | string | Version of camera software. Consult with IRIS for exact values you should use.
| Images | Array of [Image](#image-structure) | Provide image directives. This field is used when the workflow is started with the simultaneous receipt of order and images. 

### Images array 

The Images array is an array of Image structures that provides details including the storage location of one or more images associated with the order. 

### Image structure 

The Image structure allows you to specify details including the storage location where an image file can be retrieved. At this time, image retrieval is only supported in Azure Blob Storage. 

| Property | Type | Description | Options
| -- | -- | -- | --
| LocalId | string | Id as specified by the submitting organization
| Taken | DateTimeOffset | When the image was taken
| AzureBlobStorage | structure | blob storage location information 
| Laterality | options | Left or right eye  | OD, OS 
| ImageContext | options | Unless otherwise directed, Primary should be used. Non-primary images are not prominently displayed throughout the workflow. | Primary, Secondary, Component, Aggregate, Enhancement   
| ParentLocalId | string | If the image is a child of another image in the set, this is the LocalId value for that parent image 
| GroupId | numeric | If this image is part of an overall group of images, specify the group id here 
| GroupOrdinal | numeric | If this image is part of a group (specified by GroupId) this is the relative position in that group. 

### AzureBlobStorage structure 

Files in Azure Blob storage are specified by a container and filename. The Blob Storage Location in Azure is specific to an Azure Blob Storage account.  The account can either be a resource in your own Azure subscription or may be provided to you by IRIS within the IRIS Azure subscription.  Contact <a href="mailto:support@irishelp.zendesk.com">IRIS Support</a> for more details on connection access. 


| Property | Type | Description
| -- | -- | --
| Container | string | Name of the container 
| FileName | string | name of file as found in the container 

### RequestProvider structure

The RequestProvider structure allows you to specify various Providers associated with the exam. If the provider has previously been submitted and was done so with NPI, you only need to include the NPI value in the submission


| Property | Type | Description
| -- | -- | --
| NPI | string (10) | Providers National Identifier 
| Taxonomy | string | Optionally specify Taxonomy relevant to the action 
| Name | string | First, Last name
| Email | string | Optionally specify an email address 
| Degrees | string | Optionally supply degrees 
| Associations | string | Optionally supply associations 

### Request Patient structure

IRIS allows submitting detailed information on a patient, however, in most workflows the only requirement is LocalId, Name, DOB and Gender. 

Providing the starting ICD-10 diagnosis establishes the ICD-10 code class for returned codes when pathology is found. See [ICD-10 Results](/integration/ICD10CMResults) for details.

| Property | Type | Description | Options
| -- | -- | -- | --
| <span style='color:rgb(188, 13, 16);'>LocalId</span> | string | Id of patient as specified by the submitting organization. (e.g.: Patient MRN). 
| <span style='color:rgb(188, 13, 16);'>Name</span> | [Name](#name-structure) structure | Patient first and last name
| <span style='color:rgb(188, 13, 16);'>Dob</span> | Date | Patient date of birth 
| Gender | options | (Obsolete: Use Genders) Patient Gender abbreviation | [Gender](/integration/CloudDirectEnumOptions) options
| <span style='color:rgb(188, 13, 16);'>Genders</span> | Array of [PersonGender](#persongender-structure) | Patient Gender assignment(s) 
| Race | options | Optional race identifier | [Race](/integration/CloudDirectEnumOptions) options
| Ethnicity | options | Optional ethnicity identifier | [Ethnicity](/integration/CloudDirectEnumOptions) options
| PrimaryLanguage | options | Optional language identifier | [Language](/integration/CloudDirectEnumOptions) options
| MaritalStatus | options | Optional marital status identifier | [Marital Status](/integration/CloudDirectEnumOptions) options
| Email | string | Optional email address for patient 
| Phone | string | Optional single phone number for patient
| AdditionalInfo | string | Optional free form data association with patient
| Address | [Address](#address-structure) structure | Optional patient address details 
| DxCode | string | ICD-10 code starting diagnosis (default: E08) as defined by CMS

*Genders replaces Gender: While the system will still accept a single unspecified gender assignment, it will eventually be phased out in favor of Genders* 


### Request Order structure 

What you provide in the Order structure is highly dependent on your workflow. While the only required field is the Evaluation Type to perform, other properties may be required in your workflow. For example, the State field is required for mobile type exams where the location of the exam (where the images are taken) is in a different state than the Site the exam is tied to. See the description of each field for more details. 

**It is highly recommended that you use Order.LocalId as this is the only value you can expect in a subsequent order event that you can cross reference to the order you submitted.**

The IRIS system allows only one open order per patient/evaluation type combination. When using the LocalId, previous (open) orders could automatically be cancelled in favor of the newer order. For this reason, it is recommended that you supply the LocalId field so the system can more clearly identify when cancellations are the desired outcome. 

| Property | Type | Description | Options
| -- | -- | -- | --
| <span style='color:rgb(188, 13, 16);'>EvaluationTypes</span> | array of option | Specifies which evaluations to perform. Typically, only one evaluation is performed in an order but the IRIS system can support multiple thus usage of an array for this field. | DR, Glaucoma, HIV, AMD, DR_AMD
| ScheduledTime | datetime | When orders are scheduled for a specific time, this should be that time local to the exam location. This is typically used for workflows where orders are pushed to Cameras as this determines which items show in a Camera worklist
| <span style='color:rgb(188, 13, 16);'>LocalId</span> | string | The Id of the order as specified by the submitting organization. This id is required for subsequent Change and Cancel operations as well as event notifications. 
| DepartmentId | string | Optional identifier for the submitting department. Some EMR integrations will require this. 
| EncounterNumber | string | Optional identifier for the encounter that generated the order. Some EMR integrations will require this field. 
| StudyInstanceUniqueId | DICOM unique id | Optional Identifier, typically used with DICOM integrated cameras 
| OrderableIdentifier | string | Optional identifier used by some EMR platforms
| CPTCode | options | Procedure code | <a href="https://www.cms.gov/medicare/regulations-guidance/physician-self-referral/list-cpt-hcpcs-codes">See CMS for options</a>
| AdditionalInfo | string |  Free form field for edge cases 
| State | string | US State where exam is to be performed. Required for mobile exams that will not be performed at the address specified in the Site. This takes either the State abbreviation or Full name | <a href="https://www.faa.gov/air_traffic/publications/atpubs/cnt_html/appendix_a.html">US State Abbreviations</a> 
| SingleEyeOnly | bool | Specifies that you expect the order to only have images on only one eye. Used in combination with MissingEyeReason. Impacts gradeability scoring.  Null=Follow configuration for gradeability with missing eyes, False=Expected but still considered in gradeability, True=Expected and ignore for gradeability  | null/true/false 
| MissingEyeReason | string | Specifies the reason the eye was missing.  If set, reason is provided in final results
| Urgent | bool |  If true the order is prioritized in the grading queue | true/false (default: false)

### HealthPlan structure 

If your workflow is based on a Health Plan, this structure may be included in the submission. This information is returned in results. 

If your workflow includes PCP results delivery, you may specify that Provider here.

| Property | Type | Description
| -- | -- | -- 
| LocalId | string | Id of Plan as specified by the submitting organization 
| Name | string | Name of the Health Plan 
| MemberId | string | Id for the HealthPlan member, typically as specified by the Health Plan itself 
| IndividualId | string | Id for the Individual person associated with the Member for the HealthPlan 
| PrimaryCareProvider | [PCP](#primary-care-provider-structure) structure | Contains Provider information for the PCP of the Member.This information can be used for results submission directly to that provider. 

### Primary Care Provider structure 

| Property | Type | Description
| -- | -- | -- 
| NPI | string(10) | National Id for Provider 
| EmailAddress | string | Email Address for the provider 
| Name | [Name](#name-structure) structure | Providers name
| FaxNumber | phone | If so configured, can be used in results delivery

# Order and Image Events
Because Service Bus based integrations are asynchronous, IRIS posts events on an events queue to keep you apprised of important operations as they occur.  

See [Sample Events](/integration/CloudDirectEventSample/) for examples of event messages.

All messages contain a common set of base properties 

| Property | Data type | Description
| -- | -- | --
| TransactionId | GUID | Uniquely identifies the message
| Timestamp | datetimeoffset | Datetime message was posted to the queue
| Success | bool | If true the operation succeeded
| ErrorMessage | string | If Success is false, this could contain details of the error
| ResultObjectType | string | Identifies the type of event object this is to establish additional properties 
| Version | string | Message version

## ResultObjectType Types 
Messages sent on the events queue can be of varying types all based on the common properties detailed above. 

### OrderCreationReceipt
Events with the ResultObjectType of OrderCreationReceipt contain details of an  order you recently posted to the service bus queue. 

*As with all ResultObjectTypes check the Success and ErrorMessage properties for the status of the operation*

#### OrderCreationReceipt Additional Properties

| Property | Data type | Description
| -- | -- | --
| IrisOrderId | int | Id of order as created and known by IRIS
| OrderLocalId | string | Id of order as specified by you on submission
| PatientLocalId | string | Id of the patient as specified by you on submission


### ImageReceipt
Events with the ResultObjectType of ImageReceipt contain details of an image submission operation.  

*As with all ResultObjectTypes check the Success and ErrorMessage properties for the status of the operation*

#### ImageReceipt Additional Properties

| Property | Data type | Description
| -- | -- | --
| IrisOrderId | int | Id of order as created and known by IRIS
| OrderLocalId | string | Id of order as specified by you on submission
| PatientLocalId | string | Id of the patient as specified by you on submission
| ImageLocalId | string | Id of the image as specified by you on submission
| IrisImageId | int | Id of image as created and known by IRIS 

### GradingReceipt
Events with the ResultObjectType of GradingReceipt contain details of a grading operation.

*As with all ResultObjectTypes check the Success and ErrorMessage properties for the status of the operation*

#### GradingReceipt Additional Properties

| Property | Data type | Description
| -- | -- | --
| IrisOrderId | int | Id of order as created and known by IRIS
| OrderLocalId | string | Id of order as specified by you on submission
| PatientLocalId | string | Id of the patient as specified by you on submission


# Order Results

Cloud direct results may be received in a variety of ways: 

## Queue Based Results 

- IRIS Cloud Service Bus – Receive complete results on a service bus queue maintained by IRIS
- Azure Service Bus – Receive complete results on a service bus queue in your own subscription 
- AWS Queue – Receive complete results on an AWS Queue in your own subscription
- Google Queue – Receive complete results on a Google Queue in your own subscription 
- Queue based notifications 
    - Receive a notification of ready results in which a subsequent call to the IRIS results API is required 
    - For IRIS Cloud Service Bus, this option Is required if message sizes exceed 256K bytes. Results do not typically exceed this size, except when high resolution cameras are used for images that are embedded in the report. 

### Azure Service Bus Results 
To receive an order using an Azure Service Bus Queue, you simply attach a notification handler to the Results queue. 


C# Example  

```csharp
async Task Test()
{
    string connectionString = "Endpoint=sb://iris-organization…"; // abbreviated connection string string queueName = "Results"; 

    await using ServiceBusProcessor processor = client.CreateProcessor(queueName, new ServiceBussProcessorOptions()); 

    processor.ProcessMessageAsync += MessageHandler;

    await processor.StartProcessingAsync();
}

async Task MessageHandler(ProcessMessageEventArgs args)
{
    string resultsJson = args.Message.Body.ToString();
    await args.CompleteMessageAsync(args.Message);
}
```

### AWS and Google Queues

It is assumed that the choice to use AWS or Google Queue indicates a preexisting knowledge of how those resources work, therefore no coding examples are provided here. Regardless of the transport mechanism, the payload (OrderResults Object) is the same. 

### Queue Authentication

Regardless of the cloud platform, some form of connection credentials are required for access to the resource. When using IRIS Azure Cloud resources, you must obtain the connection string from IRIS support or the Administrator application as a user with the Integration Administrator role. Otherwise you must supply the credentials in the Administrator application. 

### Obtaining IRIS Azure Service Bus Connection String 
Contact IRIS support

### Configuring AWS, Azure and Google Service Bus/Queue Connection
To configure results to be pushed to an AWS, Azure (In your subscription) or Google Queue, the Integration Administrator must perform the following actions: 

- Login to the IRIS Administrator application 
- Navigate to the EMR Integration page 
- Select the “Result Delivery” tab 
- Select “Cloud Queue” under primary delivery methods 
- Select AWS, AZURE or Google from the cloud service provider options

#### AWS Queue Settings
- Queue Name 
- Queue ARN 
- Queue URL
- Region Name 
- AWS Access Key Id 
- AWS Secret Access Key 

#### Azure Queue Settings
- Queue Name 
- Connection String 

#### GCP (Google) Queue Settings
- Queue Name 
- Connection JSON 

---

# OrderResults Object Model

## Root Properties 

| Property | Type | Description | Options
| -- | -- | -- | --
| Version | string | Version of the object model | 2.3.1
| Timestamp | datetimeoffset | Timestamp when item was posted to the Results Queue 
| TransactionId | Guid | unique identifier of the communication 
| ResultCode | options | type of result payload contains | [ResultCode](/integration/CloudDirectEnumOptions)
| Site | [Site](#site-structure) structure| Contains site information order was assigned to  
| ResultsDocument | [ResultsDocument](#resultsdocument-structure) structure
| ImageDetails | [ImageDetails](#imagedetails-structure) structure | Details of images submitted to the order
| Images | Array of [Result Image](#result-image-structure) | Metadata for each image submitted 
| Order | [Order](#results-order-structure) structure | Details of order most of which is echoed from submission
| Patient | [Patient](#results-patient-structure) structure | Details of patient echoed from submission 
| OrderingProvider | [Provider](#requestprovider-structure) structure | Details of provider who ordered the exam which is echoed from the Submission 
| Gradings | [Grading Results](#gradings-structure) structure | Details of grading operation on order 
| CameraOperator [Capturing User](#cameraoperator-structure) structure | Details of the user that captured images 
| HealthPlan | [HealthPlan association](#healthplan-structure) structure | Details of the Health Plan associated with the order

## ResultsDocument structure 

Depending on your workflow the IRIS system will provide a Report of the examination. The report is available in various formats.

| Property | Type | Description | Options
| -- | -- | -- | --
| Type | options | Identifier of the result format | PDF, HTML, ORU 
| Encoding | options | specifies the encoding format for the report content | Base64, ASCII or any specific encoding scheme 
| Content | string | Content relative to the Encoding and Type. For example, if PDF, this will most likely be a Base64 encoded string 

## Results Order structure 
Contains raw order detail from submission

| Property | Type | Description
| -- | -- | -- 
| PatientOrderId | int | Id as created by IRIS on creation
| ServicedTime | datetimeoffset | when the exam was performed
| Status | string | current status of order
| EvaluationTypes | string | Evaluation performed
| ScheduledTime | datetime | When order was scheduled
| LocalId | string | The Id of the order as specified by the submitting organization. 
| DepartmentId | string | Submitting department. 
| EncounterNumber | string | Encounter specified on order
| StudyInstanceUniqueId | DICOM unique id | DICOM submitted Id
| OrderableIdentifier | string | Optional identifier provided on submission
| AdditionalInfo | string |  Free form content from submission
| State | string | US State where exam was performed.
| SingleEyeOnly | bool | value set on submission
| MissingEyeReason | string | value set on submission
| Urgent | bool |  value set on submission


## ImageDetails structure 
This structure contains a summary of the images collected for the exam.

| Property | Type | Description | Options
| -- | -- | -- | --
| TotalCount |int | Total count of all images attached to the order 
| RightEyeCount | int | Total count of all right eye images attached to the order 
| RightEyeOriginalCount | int | Count of right eye images submitted to the order (from Camera Operator) 
| RightEyeEnhancedCount | int | Count of enhanced right eye images attached to the order 
| LeftEyeCount | int | Total count of all left eye images attached to the order 
| LeftEyeOriginalCount | int | Count of left eye images submitted to the order (from Camera Operator) 
| LeftEyeEnhancedCount | int | Count of enhanced left eye images attached to the order 
| Preferred | bool | If true this image was selected as preferred for the report | true/false
| SingleEyeOnly | bool | Returns single eye indicator based on configuration and submission values | true/false


## Results Patient structure
Raw patient details for exam

| Property | Type | Description | Options
| -- | -- | -- | --
| PatientId | int | Id as set by IRIS on patient creation
| LocalId | string | Id of patient as specified by the submitting organization. Typically this will the the Patient MRN. 
| Name | [Name](#name-structure) structure | Patient first and last name
| Dob | Date | Patient date of birth 
| Gender | options | (Obsolete: Use Genders) Patient Gender abbreviation | [Gender](/integration/CloudDirectEnumOptions/) options
| Genders | Array of [PersonGender](/integration/CloudDirectEnumOptions) | One or more gender specifications 
| Phone | [Address](#address-structure) structure | Raw patient address data


## Result Images array 

Array of Result Image structures that provides details of each image attached to the order. 

## Result Image structure 

Contains details of an individual image attached to the order.

| Property | Type | Description 
| -- | -- | -- 
| LocalId | string | Id as specified by the submitting organization 
| Taken | DateTimeOffset | When the image was taken 
| Received | DateTimeOffset | When the image was received to the IRIS system
| FileName | string | Name of file as stored 
| Laterality | options | which eye | OD, OS 
| ImageContext | options | Unless otherwise directed, Primary should be used. Non-primary images are not prominently displayed throughout the workflow |  Primary, Secondary, Component, Aggregate, Enhancement  
| ParentLocalId | string | If the image is a child of another image in the set, this is the LocalId value for that parent image 
| GroupId | Numeric | If this image is part of an overall group of images, specify the group id here 
| GroupOrdinal | Numeric | If this image is part of a group (specified by GroupId) this is the relative position in that group. 
| Camera | [Result Camera](#result-camera-structure) structure | Contains details of the Camera that took the image 

## Result Camera structure 
Details of the camera that took the image. 

| Property | Type | Description 
| -- | -- | -- 
| LocalId | string | Typically this is the serial number of the Camera. Because IRIS supports a wide variety of cameras, some of which do not identify within image metadata, you may have to consult with IRIS to find the proper value to supply here. 
| Location | string | Optionally specify a location where the camera is located. This is optional even when attempting to add a camera. 
| IPAddress | string | When specified, the camera is identified by the source IP Address as images are received. This is an atypical workflow and should only be used under direct request from IRIS. 
| MACAddress | string | Optional identifier for informational purposes only 
| SerialNumber | string | Serial Number of Camera 
| Manufacturer | string | Name of camera manufacturer. Consult with IRIS for exact values you should use. 
| Model | string | Model name of camera. Consult with IRIS for exact values you should use.
| SoftwareVersion | string | Version of camera software. Consult with IRIS for exact values you should use.

## Gradings structure 
Contains raw details of grading

| Property | Type | Description | Options
| -- | -- | -- | --
| Notes | array of [Note](#note-structure) | Notes added by the Grader 
| GradedTime | datetimeoffset | When grading was completed 
| CarePlanName | string | Name of Care Plan determined from findings 
| CarePlanDescription | string | Description/Instruction text related to care plan
| Pathology | bool | If true Pathology was found on one or more eyes | true/false
| Urgent | bool | If true, the grader has found pathology that requires urgent action | true/false
| OD | [EyeSideGrading](#eyesidegrading-structure) structure | Details of grading for right eye 
| OS | [EyeSideGrading](#eyesidegrading-structure) structure | Details of grading for left eye 
| DxCodes | array of string | ICD-10 Codes matched to findings 
| Provider | [Provider](#provider-structure) (structure) – Details of the Provider who performed the grading 

## CameraOperator structure
Details of the technician who captured the images for the order.

| Property | Type | Description 
| -- | -- | -- 
| UserName | string | UserName as known by IRIS system
| Name | [Name](#name-structure) structure | Name of performing operator
| Notes | Array of [Note](#note-structure) | notes added by the performing operator

## HealthPlan structure 

| Property | Type | Description 
| -- | -- | -- 
| LocalId | string | Id of plan as specified by submitting organization 
| Name | string | Name of HealthPlan 
| MemberId | string | Id of Member as specified by the HealthPlan

## Notes array 
Array containing zero or more notes added by the related user 

## Note structure 
Structure containing metadata and content of a free form note

| Property | Type | Description 
| -- | -- | -- 
| Date | datetime | When the note was entered
| Text | string | Content 

## EyeSideGrading structure 
Structure containing grading details for one eye side

| Property | Type | Description | Options
| -- | -- | -- | --
| Gradable | bool | If false the eye side was not able to be graded with the images provided | true/false
| UngradableReasons | array of string | Grader specified reason that eye could not be graded 
| Findings | Array of [Finding](#finding-structure) | Zero or more findings for the eye

## Findings array 
Array of the Finding structure containing findings from the grader for the specified eye. If the array is not present, it indicates, there was no pathology found for the eye. 

## Finding structure 
Structure containing details of finding

| Property | Type | Description 
| -- | -- | -- 
| Finding | string | Type of pathology noted (e.g.: Diabetic Retinopathy) 
| Result | string | Level of pathology (e.g.: Mild, Moderate, Positive, etc.)

# Common Shared Structures

## Name structure
Common structure used for storing names

| Property | Type | Description
| -- | -- | --
| First | string | Persons first (given) name
| Last | string | Persons last (family) name

## Address structure 
Common structure used for storing addresses

| Property | Type | Description
| -- | -- | --
| Street1 | string | Line one of street address
| Street2 | string | Line two of street address
| City | string | City portion of address
| State | string (2) | State abbreviation of address
| PostalCode | string | Zip / Postal code

## PersonGender structure 
Common structure used for storing gender designations

| Property | Type | Description | Options
| -- | -- | -- | --
| Context | options | Gender association | [GenderContext](/integration/CloudDirectEnumOptions/) options 
| Gender | options | The gender for specified context | [Gender](/integration/CloudDirectEnumOptions/) options
  




