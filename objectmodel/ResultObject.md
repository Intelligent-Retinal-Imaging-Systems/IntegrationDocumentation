
## OrderResults Object Model

### Root Properties 

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
| Cpt | [CPT Code](#cpt-structure) structure | Procedure Code and Description

### ResultsDocument structure 

Depending on your workflow the IRIS system will provide a Report of the examination. The report is available in various formats.

| Property | Type | Description | Options
| -- | -- | -- | --
| Type | options | Identifier of the result format | PDF, HTML, ORU 
| Encoding | options | specifies the encoding format for the report content | Base64, ASCII or any specific encoding scheme 
| Content | string | Content relative to the Encoding and Type. For example, if PDF, this will most likely be a Base64 encoded string 

### Results Order structure 

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



### ImageDetails structure 

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


### Results Patient structure

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


### Result Images array 

Array of Result Image structures that provides details of each image attached to the order. 

#### Result Image structure 

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

### Result Camera structure

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

### Gradings structure

Contains raw details of grading

| Property | Type | Description | Options
| -- | -- | -- | --
| Notes | array of [Note](#note-structure) | Notes added by the Grader 
| GradedTime | datetimeoffset | When grading was completed 
| QueuedTime | datetimeoffset | When order was queued to grading 
| CarePlanName | string | Name of Care Plan determined from findings 
| CarePlanDescription | string | Description/Instruction text related to care plan
| Pathology | bool | If true Pathology was noted on one or more eyes | true/false
| Urgent | bool | If true, the grader has noted pathology that requires urgent action | true/false
| Emergent | bool | If true, the grader has noted life threatening pathology that requires immediate ER care | true/false
| OD | [EyeSideGrading](#eyesidegrading-structure) structure | Details of grading for right eye 
| OS | [EyeSideGrading](#eyesidegrading-structure) structure | Details of grading for left eye 
| DxCodes | array of string | ICD-10 Codes matched to findings 
| Provider | [Provider](#provider-structure) (structure) – Details of the Provider who performed the grading 

### CameraOperator structure

Details of the technician who captured the images for the order.

| Property | Type | Description 
| -- | -- | -- 
| UserName | string | UserName as known by IRIS system
| Name | [Name](#name-structure) structure | Name of performing operator
| Notes | Array of [Note](#note-structure) | notes added by the performing operator

### HealthPlan structure 

| Property | Type | Description 
| -- | -- | -- 
| LocalId | string | Id of plan as specified by submitting organization 
| Name | string | Name of HealthPlan 
| MemberId | string | Id of Member as specified by the HealthPlan

### Notes array 

Array containing zero or more notes added by the related user 

#### Note structure 

Structure containing metadata and content of a free form note

| Property | Type | Description 
| -- | -- | -- 
| Date | datetime | When the note was entered
| Text | string | Content 

### EyeSideGrading structure 

Structure containing grading details for one eye side

| Property | Type | Description | Options
| -- | -- | -- | --
| Gradable | bool | If false the eye side was not able to be graded with the images provided | true/false
| MissingEyeReason | If the order was submitted specifying a reason for not having images for an eye, this is that reason. 
| UngradableReasons | array of string | Grader specified reason that eye could not be graded 
| Findings | Array of [Finding](#finding-structure) | Zero or more findings for the eye

### Findings array 

Array of the Finding structure containing findings from the grader for the specified eye. If the array is not present, it indicates, there was no pathology found for the eye. 

#### Finding structure 

Structure containing details of finding

| Property | Type | Description 
| -- | -- | -- 
| Finding | string | Type of pathology noted (e.g.: Diabetic Retinopathy) 
| Result | string | Level of pathology (e.g.: Mild, Moderate, Positive, etc.)

## Common Shared Structures

### Name structure

Common structure used for storing names

| Property | Type | Description
| -- | -- | --
| First | string | Persons first (given) name
| Last | string | Persons last (family) name

### Address structure 

Common structure used for storing addresses

| Property | Type | Description
| -- | -- | --
| Street1 | string | Line one of street address
| Street2 | string | Line two of street address
| City | string | City portion of address
| State | string (2) | State abbreviation of address
| PostalCode | string | Zip / Postal code

### PersonGender structure 

Common structure used for storing gender designations

| Property | Type | Description | Options
| -- | -- | -- | --
| Context | options | Gender association | [GenderContext](/integration/objectmodel/OptionEnums) options 
| Gender | options | The gender for specified context | [Gender](/integration/objectmodel/OptionEnums) options
  




