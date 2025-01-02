---
title: File templates
parent: Basic Integrations
---

# Template Driven Filepath Naming
File names for delivery can be customized from the content from an order.  This is accomplished by providing a template containing placeholders that are dynamically set at delivery.

### Example
The following example assumes a local file system delivery with the following configuration:

- Template: C:\results\\{MMddyyyy}\\{clientLocalId}\\{orderLocalId}.pdf
- Client Local Id: HarborviewClinic
- Order Local Id: P0112X00123
- Date of delivery: 9/1/2024

Resulting Filename: C:\results\09012024\HarborviewClinic\P0112X00123.pdf


## Placeholders
Placeholders are any of the following list of reserved words contained with curly brackets: { }

*Note that not all values are guaranteed to be available as certain fields are only available if you supply them on the submission of the order (e.g.: orderLocalId).*

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

*Tokens are case sensitive and can only be used exactly as shown in this list (i.e.: You cannot substitute components in your own combination).*

| Token name | Description | Example Result assuming datetime  9/1/2024 9:04:21
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
