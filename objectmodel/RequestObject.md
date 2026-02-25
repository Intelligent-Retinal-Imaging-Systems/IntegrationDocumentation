---
title: Order Request
parent: Object Models
nav_order: 1
---


## OrderRequest Object Model 

The OrderRequest object model provides all the properties necessary to perform order actions such as create, change or cancel. Most workflows require using only a small subset of the available properties. Properties colored <span style='color: rgb(188, 13, 16);'>red</span> are required. 

##### ![alt text](/assets/properties.ico) OrderRequest root properties

| Property  | type  |  Description  | Options
| -- | -- | -- | -- |
| <span style='color:rgb(188, 13, 16);'>Version</span> | string |  Should be set to 2.3.1 unless otherwise directed.
| UserNameSubmitting | string | Optionally specify the username of a user that should be associated with the order creation. If your organization has been provided a service account for API direct operations, this is acceptable, otherwise it is not required. 
| <span style='color: rgb(188, 13, 16);'>OrderControlCode</span> | options | Specifies the operation that should be performed with the order data (add/change/cancel) | [OrderControlCode](/objectmodel/OptionEnums#-ordercontrolcode) options
| <span style='color: rgb(188, 13, 16);'>Site</span> | [Site](#site) structure | Location order is associated with
| Camera | [Camera](#camera) structure | Camera the order should be assigned to as well as optionally specifying the images associated with the order and camera
| <span style='color: rgb(188, 13, 16);'>Order</span> | [Order](#order) structure | Details of order
| <span style='color: rgb(188, 13, 16);'>Patient</span> | [Patient](#patient) structure | Patient details
| OrderingProvider | [Request Provider](#requestprovider) structure | Medical provider who ordered the exam
| ReferringProvider | [Request Provider](#requestprovider) structure | Medical provider who referred the patient for the exam
| CameraOperator | [Request Provider](#requestprovider) structure | Medical provider assigned to perform the exam. This option is used when the Operator is a medical provider with a valid NPI 
| CameraOperatorUserName | string | *** DEPRECATED - Use CameraOperator Instead *** UserName of the technician who should be assigned to the order. This option is used when the operator does not have an NPI 
| HealthPlan | [HealthPlan](#healthplan) structure | If order is associated with a Health Plan


## OrderRequest children

<a id="site"></a>
### ![alt text](/assets/structure.ico) Site

The Site structure is primarily used to identify the site the order is to be associated with. If your organization is configured as such, sites can be dynamically added, therefore additional properties are provided to supply the required information. If you don’t require automatic site additions, simply provide the LocalId. 


| Property | Type | Description 
| -- | -- | -- 
| LocalId | string | Id of site as specified by you, the submitting organization
| Name | string | Name of the site (Only required for automatic site additions)
| Address | [Address](/objectmodel/CommonObjects#address-structure) structure | Address of site (Only required for automatic site additions)

<a id="camera"></a>
### ![alt text](/assets/structure.ico) Camera 

When an order is to be assigned to a camera or Image directives are included with the order, populate this structure. If the camera already exists and you are not providing image directives, you only need to supply the LocalId. Other than the Images structure, the remaining properties are provided in the event your organization allows automatic Camera additions.

##### ![alt text](/assets/properties.ico) Camera properties

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
| Images | Array of [Image](#image) | Provide image directives. This field is used when the workflow is started with the simultaneous receipt of order and images.

## Images

The Images array is an array of Image structures that provides details including the storage location of one or more images associated with the order. 

<a id="image"></a>
### ![alt text](/assets/structure.ico) Image

The Image structure allows you to specify details including the storage location where an image file can be retrieved. At this time, image retrieval is only supported in Azure Blob Storage. 

| Property | Type | Description | Options
| -- | -- | -- | --
| LocalId | string | Id as specified by the submitting organization
| Taken | DateTimeOffset | When the image was taken
| AzureBlobStorage | [structure](#blobstorage) | blob storage location information 
| Laterality | [options](/objectmodel/OptionEnums#-laterality) | Left or right eye  | OD, OS 
| ImageContext | options | Unless otherwise directed, Primary should be used. Non-primary images are not prominently displayed throughout the workflow. | Primary, Secondary, Component, Aggregate, Enhancement   
| ParentLocalId | string | If the image is a child of another image in the set, this is the LocalId value for that parent image 
| GroupId | numeric | If this image is part of an overall group of images, specify the group id here 
| GroupOrdinal | numeric | If this image is part of a group (specified by GroupId) this is the relative position in that group. 

<a id="blobstorage"></a>
### ![alt text](/assets/structure.ico) AzureBlobStorage  

Files in Azure Blob storage are specified by a container and filename. The Blob Storage Location in Azure is specific to an Azure Blob Storage account.  The account can either be a resource in your own Azure subscription or may be provided to you by IRIS within the IRIS Azure subscription.  Contact <a href="mailto:support@irishelp.zendesk.com">IRIS Support</a> for more details on connection access. 


| Property | Type | Description
| -- | -- | --
| Container | string | Name of the container 
| FileName | string | name of file as found in the container 

<a id="requestprovider"></a>
### ![alt text](/assets/structure.ico) RequestProvider

The RequestProvider structure allows you to specify various Providers associated with the exam. If the provider has previously been submitted and was done so with NPI, you only need to include the NPI value in the submission


| Property | Type | Description
| -- | -- | --
| NPI | string (10) | Providers National Identifier 
| Taxonomy | string | Optionally specify Taxonomy relevant to the action 
| Name | string | First, Last name
| Email | string | Optionally specify an email address 
| Degrees | string | Optionally supply degrees 
| Associations | string | Optionally supply associations 

<a id="patient"></a>
### ![alt text](/assets/structure.ico) Patient

IRIS allows submitting detailed information on a patient, however, in most workflows the only requirement is LocalId, Name, DOB and Gender. 

Providing the starting ICD-10 diagnosis establishes the ICD-10 code class for returned codes when pathology is found. See [ICD-10 Results](/integration/Results/ICD10CMResults) for details.

| Property | Type | Description | Options
| -- | -- | -- | --
| <span style='color:rgb(188, 13, 16);'>LocalId</span> | string | Id of patient as specified by the submitting organization. (e.g.: Patient MRN). 
| <span style='color:rgb(188, 13, 16);'>Name</span> | [Name](/objectmodel/CommonObjects.md#name-structure) structure | Patient first and last name
| <span style='color:rgb(188, 13, 16);'>Dob</span> | Date | Patient date of birth 
| Gender | options | (Obsolete: Use Genders) Patient Gender abbreviation | [Gender](/objectmodel/OptionEnums#-gender) options
| <span style='color:rgb(188, 13, 16);'>Genders</span> | Array of [PersonGender](/objectmodel/CommonObjects#persongender-structure) | Patient Gender assignment(s) 
| Race | options | Optional race identifier | [Race](/objectmodel/OptionEnums#-race) options
| Ethnicity | options | Optional ethnicity identifier | [Ethnicity](/objectmodel/OptionEnums#-ethnicity) options
| PrimaryLanguage | options | Optional language identifier | [Language](/objectmodel/OptionEnums#-language) options
| MaritalStatus | options | Optional marital status identifier | [Marital Status](/objectmodel/OptionEnums#-marital-status) options
| Email | string | Optional email address for patient 
| Phone | string | Optional single phone number for patient
| AdditionalInfo | string | Optional free form data association with patient
| Address | [Address](/objectmodel/CommonObjects#address-structure) structure | Optional patient address details 
| DxCode | string | ICD-10 code starting diagnosis (default: E08) as defined by CMS

*Genders replaces Gender: While the system will still accept a single unspecified gender assignment, it will eventually be phased out in favor of Genders* 

<a id="order"></a>
### ![alt text](/assets/structure.ico) Order 

What you provide in the Order structure is highly dependent on your workflow. While the only required field is the Evaluation Type to perform, other properties may be required in your workflow. For example, the State field is required for mobile type exams where the location of the exam (where the images are taken) is in a different state than the Site the exam is tied to. See the description of each field for more details. 

**It is highly recommended that you use Order.LocalId as this is the only value you can expect in a subsequent order event that you can cross reference to the order you submitted.**

The IRIS system allows only one open order per patient/evaluation type combination. When using the LocalId, previous (open) orders could automatically be cancelled in favor of the newer order. For this reason, it is recommended that you supply the LocalId field so the system can more clearly identify when cancellations are the desired outcome. 


##### ![alt text](/assets/properties.ico) **Order** root properties 

| Property | Type | Description | Options
| -- | -- | -- | --
| <span style='color:rgb(188, 13, 16);'>EvaluationTypes</span> | array of [Evaluation Type](/objectmodel/OptionEnums#-evaluation-types) | Specifies which evaluations to perform. Typically, only one evaluation is performed in an order but the IRIS system can support multiple thus usage of an array for this field. | DR, Glaucoma, HIV, AMD, DR_AMD, SP
| ScheduledTime | datetime | When orders are scheduled for a specific time, this should be that time local to the exam location. This is typically used for workflows where orders are pushed to Cameras as this determines which items show in a Camera worklist
| <span style='color:rgb(188, 13, 16);'>LocalId</span> | string | The Id of the order as specified by the submitting organization. This id is required for subsequent Change and Cancel operations as well as event notifications. 
| DepartmentId | string | Optional identifier for the submitting department. Some EMR integrations will require this. 
| EncounterNumber | string | Optional identifier for the encounter that generated the order. Some EMR integrations will require this field. 
| StudyInstanceUniqueId | DICOM unique id | Optional Identifier, typically used with DICOM integrated cameras 
| OrderableIdentifier | string | Optional identifier used by some EMR platforms
| CPTCode | [CPT Code structure](#cpt) | Procedure code | <a href="https://www.cms.gov/medicare/regulations-guidance/physician-self-referral/list-cpt-hcpcs-codes">See CMS for options</a>
| AdditionalInfo | string |  Free form field for edge cases 
| State | string | US State where exam is to be performed. Required for mobile exams that will not be performed at the address specified in the Site. This takes either the State abbreviation or Full name | <a href="https://www.faa.gov/air_traffic/publications/atpubs/cnt_html/appendix_a.html">US State Abbreviations</a> 
| SingleEyeOnly | bool | Specifies that you expect the order to only have images on only one eye. Used in combination with MissingEyeReason. Impacts gradeability scoring.  Null=Follow configuration for gradeability with missing eyes, False=Expected but still considered in gradeability, True=Expected and ignore for gradeability  | null/true/false 
| MissingEyeReason | string | Specifies the reason the eye was missing.  If set, reason is provided in final results

<a id="healthplan"></a>
### ![alt text](/assets/structure.png) HealthPlan 

If your workflow is based on a Health Plan, this structure may be included in the submission. This information is returned in results. 

If your workflow includes PCP results delivery, you may specify that Provider here.

| Property | Type | Description
| -- | -- | -- 
| LocalId | string | Id of Plan as specified by the submitting organization 
| Name | string | Name of the Health Plan 
| MemberId | string | Id for the HealthPlan member, typically as specified by the Health Plan itself 
| IndividualId | string | Id for the Individual person associated with the Member for the HealthPlan 
| PrimaryCareProvider | [PCP](#alt-text-primary-care-provider-structure) structure | Contains Provider information for the PCP of the Member.This information can be used for results submission directly to that provider. 

<a id="cpt"></a>
### ![alt text](/assets/structure.png) CPT

A procedure code can be submitted in the order and echoed back in results

| Property | Type | Description
| -- | -- | -- 
| Code | string | Procedure Code as defined by CMS
| Description | string | Description as defined by CMS

<a id="pcp"></a>
### ![alt text](/assets/structure.png) Primary Care Provider

You may associate a patient with their primary care provider in cases when you want to deliver a copy of the report to them.  PCP Results is a delivery option that must be configured by IRIS before this data is utilized.  Contact your IRIS sales representative to have this feature activated.

| Property | Type | Description
| -- | -- | --
| NPI | string(10) | National Id for Provider
| EmailAddress | string | Email (or [Direct Messaging](/integration/DirectMessaging.md)) address for the provider
| Name | [Name](/objectmodel/CommonObjects#name-structure) structure | Providers name
| FaxNumber | phone | Fax number that may be used in results delivery

