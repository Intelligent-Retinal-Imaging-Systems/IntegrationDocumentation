---
title: Report Template
parent: Results Generation
has_toc: false
---

## Report Template

Reports are generated from templates that can be customized and tested in the Administrator application. 

A template (in this context) is a combination of static content and placeholders that are to be dynamically set at generation time.

Report templates exist for all Evaluation types. For example, the report template for Diabetic Retinopathy evaluation types is called the *Standard DR/ME report template*.

The standard report template is encoded as HTML.  For EMR Integrations that support narratives, there are Line report templates for each evaluation type.  See the [Administration Application](#administrator-application) for more details.

## Placeholders
A placeholder is a token encapsulated within double square brackets [[]] positioned in the template to be dynamically swapped at delivery. Tokens are predefined entities established by IRIS with the following rules:

- All characters are upper case
- Words are separated with the _ character
- Left most word can be repeated for categories (e.g.: PATIENT) 

*The use of double square brackets to identify placeholders, as apposed to the single curly bracket, is to avoid conflicts in the content.  Curley brackets are preferred for ease of use and readability when the content would not otherwise contain them.*

### Example
**PATIENT_NAME** is a token that becomes a placeholder **\[[PATIENT_NAME]]** when encapsulated in double brackets.

*Not all values are guaranteed to be available as certain fields are only available if you supply them on the submission of the order (e.g.: HEALTHPLAN_MEMBERID). Using unset values could result in corrupted reports that may not render and may not convert properly to PDF.*

| Token name | Description
| -- | --
| PATIENT_NAME | Patients first and last name
| PATIENT_AGE | Patients age
| PATIENT_GENDER | Patients gender
| PATIENT_DOB | Patients birthdate
| PATIENT_MRN | Patient MRN (From Patient.LocalId) Option provided for readability
| PATIENT_LOCAL_ID | Id of patient as provided by submitting organization
| PATIENT_PHONE | Patients phone 
| HEALTHPLAN_MEMBERID | Patients health plan membership identifier
| HEALTHPLAN_POLICYNUMBER | Patients health plan policy number
| HEALTHPLAN_GROUPNUMBER | Patients health plan group number identifier
| HEALTHPLAN_GROUPNAME | Patients health plan group name
| HEALTHPLAN_INSURANCE_COMPANY_LOCALID | Patients health plan insurance carrier identifier as specified by submitting organization
| HEALTHPLAN_INSURANCE_PLAN_ID | Patients health plan id
| HEALTHPLAN_INSURANCE_PLAN_NAME | Patients health plan name
| CLINIC_NAME | Client/Site name
| ORDER_DATE | Date/Time when order was received on the IRIS Platform
| ORDER_SCHEDULED_DATE | Date/Time order was scheduled for
| GRADER_SIGNATURE | Contains name and details of grading provider
| CARE_PLAN | Care plan derived from findings
| RIGHT_EYE_FINDINGS | Findings for right eye.  This is a complex section and should not be altered
| LEFT_EYE_FINDINGS | Findings for left eye.  This is a complex section and should not be altered
| LEFT_EYE_ORIGINAL_IMAGE | Image for left eye.
| RIGHT_EYE_ORIGINAL_IMAGE | Image for right eye.
| ORDERING_PROVIDER_NAME | First, Last name of ordering provider
| REFERRING_PROVIDER_NAME | First, Last name of referring provider
| ENCOUNTER_NUMBER | Encounter number as supplied on order creation
| ORDER_LOCAL_ID | Id of order as specified by submitting organization
| PATIENT_ORDER_INFO | Submitting specified additional order information provided on submission
| ORDERABLE_IDENTIFIER | Value provided on order submission (typically from HL7 integrations)
| DEPARTMENT_LOCAL_ID | Id, as specified by submitting organization, of the department where the exam was performed
| DISCLAIMER | Disclaimer line which can be configured by site

*To maintain backward compatibility, there are a handful of placeholders you might find in your templates that are not listed above.  These Placeholders should only be altered by or under the supervision of IRIS support personnel.*

### Administrator Application
To see and/or customize any result template for your organization login to the IRIS [Admin](https://admin.retinalscreenings.com) application.  You can view/edit templates specified at the Organization level or the Client/Site level.

*If a template does not exist at the site level, the system checks for a template configured at the Organization level.  If a template does not exist there, the default template of that type is used.*

Most customers use default templates.  Of those who do customize, the majority are only changing the logo. 

*You should be proficient in HTML before updating HTML encoded templates.You could break something!*

#### Organization level templates

- Navigate to the Results section of the [Administrator](https://admin.retinalscreenings.com) application.
- A list of available templates is displayed including the encoding type.
- Click the line you wish to view or edit.

##### Administrator application - Select Template for Edit

![Org Admin Screenshot](/assets/adminresultssection.png)

- Once in the editor, make whatever changes you desire and hit preview to generate aa sample report with your changes. 
- Placeholders are easily identified by the double square brackets \[[REPORT_PLACEHOLDER]]. 
- Your template will not be used until the **Save Changes** button is pressed.

##### Administrator application - Template Editor

![Org Admin Screenshot 2](/assets/admintemplateedit1.png)


- Results are generated immediately after grading therefore changes you make in the template will not be visible for orders graded before your change.  
- It is possible to regenerate results but this can only be done by IRIS support personnel.  

 *The process of converting an HTML document to PDF does not always match the HTML rendering exactly so make sure to review a newly generated PDF once your changes have been saved.*