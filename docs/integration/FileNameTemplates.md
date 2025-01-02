---
title: File templates
parent: Basic Integrations
---

# Template Driven File Naming
There are several things to consider when using any file drop form of delivery.
1. You do not want results overwritten, so filenames need to be reasonably unique.
2. How do you intend on processing the files from the delivery?  
    - Do you need to identify the report from the name of the file?
    - Do you need to logically separate reports to the site/facility/department of the exam?
3. Should they be saved a way that can be searched from the operating system for troubleshooting?

For these and other potential reasons, file and path names can be customized from the details of an order.  This is accomplished by defining a template for specifying folders and file names for results.

A template (in this context) is a combination of static content and placeholders that are to be dynamically set at delivery time.


## Placeholders
A placeholder is a token encapsulated within curly brackets positioned in the template to be dynamically swapped at delivery. Tokens are predefined descriptive words or character combinations established by IRIS and listed below.

### Example
**patientId** is a token that becomes a placeholder **{patientId}** when encapsulated in brackets.

*Not all values are guaranteed to be available as certain fields are only available if you supply them on the submission of the order (e.g.: orderLocalId). Using unset values could result in a failed delivery especially if that value is used to establish a folder.*

| Token name | Description
| -- | --
| patientId | Patient Id as specified by IRIS
| patientLocalId | Patient Id as specified by the submitting organization
| orderId | Order Id as specified by IRIS
| orderLocalId | Order Id as specified by the submitting organization
| patientFirstName | Patients first name
| patientLastName | Patients last name
| clientLocalId | Id of the site/facility as specified by the submitting organization 
| departmentLocalId | Id of the department as specified by the submitting organization

### You may also supply date and time placeholders using the following tokens.

*Tokens are case sensitive and can only be used exactly as shown in this list (i.e.: You cannot substitute date/time components in your own combination).*

| Token name | Description | Result assuming delivery at: 9/1/2024 9:04:21
| -- | -- | --
| yyyy | Four digit year from date when result is delivered | 2024
| MM | Zero padded, two digit month from date when result is delivered | 09
| dd | Zero padded, two digit day of the month from date when result is delivered | 01
| yyyyMMdd_HHmmss | Julian Date (zero padded components) + _ + Zero padded Hour, minute and seconds from date/time when result is delivered | 20240901_090421
| yyyyMMdd | Julian Date (zero padded components) when result is delivered | 20240901
| MMddyyyy | Date (zero padded components) when result is delivered | 09012024
| YEST_yyyy | Four digit year from date when result is delivered minus one day | 2024
| YEST_MM | Zero padded, two digit month from date when result is delivered minus one day | 08
| YEST_dd | Zero padded, two digit day of the month from date when result is delivered minus one day | 31
| YEST_yyyyMMdd_HHmmss | Julian Date (zero padded components) + _ + Zero padded Hour, minute and seconds from date/time when result is delivered minus one day | 20240831_090421
| YEST_yyyyMMdd | Julian Date (zero padded components) when result is delivered minus one day | 20240831
| YEST_MMddyyyy | Date (zero padded components) when result is delivered minus one day | 08312024


## Field content considerations
When building a template keep in mind that certain values found in fields could be incompatible with file naming restrictions of the target system.

## Report identification on programmatic processing
As you decide on your file naming approach, consider that PDF files sent from IRIS include metadata that can be processed using standard PDF programming resources. 

Identifiers for the order and patient can be easily parsed from the document making it easy to process files programmatically.


## Template Example 
The following example assumes a local file system delivery with the following configuration:

- **Template**: C:\results\\{MMddyyyy}\\{clientLocalId}\\{orderLocalId}.pdf
- **Client Local Id**: HarborviewClinic
- **Order Local Id**: P0112X00123
- **Date of delivery**: 9/1/2024

#### Resulting Filename
 C:\results\09012024\HarborviewClinic\P0112X00123.pdf


#### The static portion of this example includes:
| Text | Comments
| -- | -- 
| C:\results\  | All results go to the C:\results folder
| \\ | Two levels of folder based on result content
| .pdf | You must specify the proper filename extension based on the data type of the content dropped

#### The dynamic portion of this example includes:
| Placeholder | Comments
| -- | --
| {MMddyyyy} | Separate folder for each days results
| {clientLocalId} | Separate folder for each site/facility
| {orderLocalId} | Name the file from the Id specified by the organization on creation


