---
title: Grading Submission Model
parent: Object Models
nav_order: 7
---


## GradingSubmission Model 
#### Test Environment Only

The GradingSubmission object model provides all the properties necessary to post a grading to an order in your test environment. 

> Grading submissions will be ignored in certain cases such as when an order is closed or when there are no images yet linked to it. Because this feature is only available for test environments, there are currently no events posted on grading failures.  Use the Order Manager application for debugging individual order issues.

##### ![alt text](/assets/properties.ico) Root properties

| Property  | type  |  Description  | Options
| -- | -- | -- | -- |
| <span style='color:rgb(188, 13, 16);'>Version</span> | string |  Should be set to 2.3.1 unless otherwise directed.
| OD | Right eye grading | Object containing choices for the right eye 
| OS | Left eye grading | Object containing choices for the left eye 
| LocalId | string | Id of Order as specified by submitting organization
| ClientGuid | string/GUID | Unique organization identifier as provided by IRIS required on all submission objects
| Site | Site object  | Specifies the site for the grading.  Only used the Site.LocalId property for grading submissions


## GradingSubmission Members

<a id="od"></a>
### ![alt text](/assets/structure.ico) (OD) EyeGrading (Object)

The **OD object** contains all grading selections specific to the right eye
 

<a id="os"></a>
### ![alt text](/assets/structure.ico) (OS) EyeGrading (Object)

The **OS object** contains all grading selections specific to the left eye
 

##### ![alt text](/assets/properties.ico) EyeGrading properties

| Property | Type | Description 
| -- | -- | -- 
| Findings | array of [Finding](#finding) | Grader findings 
| Gradable | bool | If true, the eye was gradable, otherwise not.  If true, Findings array must be empty or omitted
| UngradableReasons | array of string | Reasons why the eye was ungradable. This is an array for backward compatibility reasons and there should only ever be one item in this array and ONLY if the Gradable property is set to false
| MissingEyeReason | string | If the eye was omitted from the study, this can be used to specify a reason that excludes the eye from the study. When not supplied the eye could be marked as ungradable due to missing images

##### ![alt text](/assets/array.png) Findings (Array)
Use this array to add findings for the eye.  

*An eye submitted as ungradable should have no Findings.  You may either omit the collection entirely in this case.*

Add one or more Findings (condition/result combination) to be set for the eye.  

> For in depth details, see the [Findings](integration/Results/Findings) page within the Results section of this guide.

<a id="finding"></a>
##### ![alt text](/assets/structure.ico) Finding (Object)
Use this structure to submit an individual finding for an eye within the grading submission.  

As described in the [Findings](/integration/Results/Findings) page, some finding types are qualified and other are not.  Allowable combinations are specific to the evaluation type the order is submitted with.  
The grading submission schema (see :[Grading Submission Example](/clouddirect/GradingSubmissionExample)) can be used to provide guidance on allowable pairing.

Use the Admin applications Care Plan editor to see which evaluation types are available for your orders and the findings allowed on each. 






