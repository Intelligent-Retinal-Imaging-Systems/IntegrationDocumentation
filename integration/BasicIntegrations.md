---
title: Basic Integrations
parent: Order Processing Integration
nav_order: 1
has_toc: false
---

# Basic Integrations
IRIS provides a variety of tools to allow basic integration services that may supplement or cover specific requirements.  

## Use case examples
- Receiving PDF reports as orders are completed
     - To your local file system
     - To an SFTP site
     - To a fax machine
- Adding a batch of orders from a CSV file


## Local File System Integration
IRIS can deliver results directly to a local file system within your network using the [IRIS EMR Proxy](/integration/IRISEMRProxy/). 

The typical payload for file system delivery is a PDF report with attached metadata.  Path names are [template based](/integration/FileNameTemplates/) and can include tokens dynamically swapped from details of the order. For example, you can configure the system to save the PDF as a file with the name including the MRN and date of service.  

Other payload options are available including files written with JSON encoded raw content.  

This option can be deployed standalone as the primary source of results or as a supplement to any other delivery mechanism. 

To implement local file systems integration, Contact <a href="mailto:support@irishelp.zendesk.com">IRIS Support</a>.  You may elect to perform the Integration administrator role yourself or IRIS can do this for you. 

## SFTP 
Results can be delivered to an SFTP site you provide access to.  

- You can choose a payload type of PDF report or JSON encoded raw data that can include the PDF Report
- You may specify a single directory level that is used for all results
- File names are [template based](/integration/FileNameTemplates/) and can include tokens dynamically swapped from details of the order.  
- You must register an individual to be a contact point for delivery failures

To use SFTP Delivery, Contact <a href="mailto:support@irishelp.zendesk.com">IRIS Support</a>


## Fax
IRIS Can send your results to one or more fax numbers.

To setup fax delivery, contact <a href="mailto:support@irishelp.zendesk.com">IRIS Support</a>

## Order Manager Application
You may use the IRIS Order Manager application to receive all of your results.  When configured for this type of results delivery, orders stay in a pending delivery state until you pick them up through the application.  Pending results are packaged into a single (.zip) file which you may download as often as you wish.  

#### Example Order Manager Screenshot
![OrderManagerResults](/assets/ordermanagerresults.png)


## CSV Bulk Import

IRIS supports bulk uploading of orders from a CSV file.   To enabled this feature, contact <a href="mailto:support@irishelp.zendesk.com">IRIS Support</a>

> The bulk upload process is facilitated through use of cloud storage and unless otherwise requested, is hosted in Azure. IRIS software monitors the storage container and as new files appear, they are parsed, loaded into the system and removed from the storage account.

Files are parsed using a mapping utility.  On initial setup you must supply the IRIS support team memeber with an example CSV file from which they initialize the mapping instructions.  Changes to mapping are then available from the upload utility in the IRIS portal.

See the order intake fields list below in order to determine which fields you wish to include in your bulk uploads.

### File submission

Files may be submitted to IRIS in a variety of ways depending on your requirements. 

- In cases where files are uploaded infrequently, the simpliest option is to use the <a href="https://portal.retinalscreenings.com">IRIS portal.</a> Only users that are given the role of Integration Administrator will see the upload option from the portal menu.
- If you are generating CSV files from a custom application, you can easiely upload them using an SDK for the cloud provider specific to your development environment. For Azure storage accounts, the connection string specific to your instance can be retrieved from portal import page.
- You may also use blob storage utilities such as Azure Storage Explorer.  This may be a good option if your are planning on writing custom software and you want to use the tool for debugging purposes (e.g.: Testing connection strings, watching files get pulled, etc...)
     
### Order Intake Fields

The following list of fields may be mapped to columns in your CSV file. 

| FieldName | Description | Required 
| -- | -- | --
| CameraOperatorEmail | Email address of the Camera operator | No
| CameraOperatorFirstName | First name of the camera operator | No
| CameraOperatorLastName | Last name of Camera operator | No
| CameraOperatorNPI | NPI of Camera Operator | No
| CameraOperatorUserName | CameraOperatorUserName | No
| ClientGuid | Globally unique identifier for the client | Yes
| CPTCode | CPTCode for the order | No
| DepartmentId | Identifier for the department | No
| DxCode | Diagnosis code for the patient | No
| EncounterNumber | Unique number identifying the patient encounter | No
| EvaluationType | Evaluation type to specify for orders. (This is only necessary if you are sending multiple eval types from a single CSV file.) | No
| HealthPlanEffectiveDate | Effective start date of the health plan | No
| HealthPlanExpirationDate | Expiration date of the health plan | No
| HealthPlanGroupName | Group name associated with the health plan | No
| HealthPlanGroupNumber | Group number associated with the health plan | No
| HealthPlanMemberId | Member ID for the health plan | No
| HealthPlanName | Name of the Health Plan | No
| HealthPlanPayerName | Name of the payer organization for the health plan | No
| HealthPlanPolicyNumber | Policy number for the health plan | No
| HealthPlanPrimaryCareProviderEmailAddress | Email address of the primary care provider | No
HealthPlanPrimaryCareProviderFaxNumber | Fax number of the primary care provider | No
| HealthPlanPrimaryCareProviderFirst | First name of the primary care provider | No
| HealthPlanPrimaryCareProviderLast | Last name of the primary care provider | No
| HealthPlanPrimaryCareProviderNPI | NPI (National Provider Identifier) of the primary care provider | No
| MissingEyeReason | Reason for the absence of an eye (if applicable) | No
| OrderAdditionalInfo | Freeform data to add at the order level | No
| OrderControlCode | Control code for the order | Yes
| OrderingProviderEmail | Email address of the ordering provider | No
| OrderingProviderFirstName | First name of the ordering provider | No
| OrderingProviderLastName | Last name of the ordering provider | No
| OrderingProviderNPI | NPI of provider who is the ordering provider | No
| OrderLocalId | The order ID as specified by the submitting organization	1
| OrderScheduledTime | Scheduled time for the order | No
| OrderState | US State where exam is performed | No
| PatientAdditionalInfo | Additional information about the patient | No
| PatientBirthGender | Patient gender assigned at birth | Yes
| PatientDob | Date of birth of the patient | Yes
| PatientFirstName | The patient first name | Yes
| PatientIdentityGender | Patient identifying gender | No
| PatientLastName | The patient last name | Yes
| PatientLocalId | The patient ID as specified by the submitting organization | Yes
| PatientPhone | Phone number of the patient | No
| ReferringProviderEmail | Email address of the referring provider | No
| ReferringProviderFirstName | First name of the referring provider | No
| ReferringProviderLastName | Last name of the referring provider | No
| ReferringProviderNPI | NPI of provider who is the referring provider | No
| SingleEyeOnly | Indicates if the patient only has one eye | No
| SiteLocalId | Local identifier for the site | Yes
| UserNameSubmitting | Username of the person submitting the data | No
| Version | Version of the record or system | Yes
