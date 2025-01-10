---
title: Results Generation
parent: Order Processing Integration
nav_order: 4
has_toc: false
---

## Results Generation

Once grading has been completed, the order moves into the results generation pipeline where details of the exam are compiled for subsequent delivery.  The content you receive is typically tied to the integration type but IRIS provides a variety of options to allow customization to fit your needs.

Before we move on to the topic of results content, there are a few components of any result that you should familiarize yourself with:

- [Images](/integration/Results/Images/)
- [Findings](/integration/Results/Findings/)
- [ICD-10 Codes](/integration//Results/ICD10CMResults)

### Results can be generated in one or more of several formats

- [RAW (JSON)](#raw) - Think of this as a data dump.  This is everything IRIS knows about the order provided in an hierarchical structure.
- [PDF](#pdf-report) - This is a report that would be presentable to the patient
- [HL7](/integration/hl7messages/) - Encoded results for EMR integrations
- HTML - Same as PDF just delivered as a single HTML encoded document.
- FAX - PDF report converted to a Fax
- [CSV](#csv) - Similar to RAW except using a smaller subset of data in a flat structure

#### PDF Report

The PDF report is the most commonly used results.  This is a compiled report containing the important details of the order in a easy to read report layout.

The PDF Report is generated using a template containing static content with embedded placeholders that are swapped at generation time.  You may customize and test your report template from the Administrator application to suit your needs.

##### Example PDF Report

![PDF Report Example](/assets/pdfreport.png)

#### RAW

RAW results refers to results that include all of the details of the order.  In simplest form, this content is delivered with JSON encoding.  When using public library options, the JSON content is deserialized into the Results object.

Raw results can, and usually do, include one of the other result types, typically the PDF.

Click [here](/integration/CloudDirectResultExample.md) for an example RAW result message in JSON format.

#### Fax Results

Results can be delivered to one or more fax numbers as well as for multiple purposes.  

You could choose fax as the method of receiving your results from IRIS as well as sending copies of the report to the patients PCP.

PCP delivery requires that details of the PCP are provided in the original order submission.

When using Fax as the delivery method for non-PCP purposes, you can establish a single number for all results for all sites or it can also be configured at the site level. If a number is configured for both, the system prefers Site over Organization. 

#### CSV

Within the Order Manager application, you can save the results of a search as CSV.  

*If you are configured to receive your results from Order Manager, one of the search options is for new results which are any results that have not been marked as retrieved.*

![Order Manager Example](/assets/OrderManagercsv.png)

The CSV file contains the following fields:
| Header | Description
| -- | --
| Order Id | Id of order as establish by IRIS 
| Scheduled Date | Date time exam was scheduled for
| Order Status  | Current state of the order (waiting images, completed, etc.)
| Evaluation Type(s)  | IRIS Eval type code (e.g.: DR)
| Exam Location	 | Name of the client/site where the images where taken
| Patient Name | Patients full name
| Patient Gender | Patients gender
| Patient DOB | Patients date of birth
| Patient MRN | Id of patient as specified by submitting organization
| Patient Phone Number | Patients phone
| Camera Operator | User who captured images
| Ordering Provider | Details of the ordering provider
| Interpreting Provider | Details of the grading provider
| Interpretation Date | Date of grading
| Findings | Pipe delimited findings
| Diagnoses	| ICD-10 Codes
| CPT | Procedure code submitted on order creation
| Care Plan	| Care plan derived from findings
| (Count of) Original images | Number of images submitted for all eyes
| Camera Operator Notes | Any notes that were entered for the order by the camera operator
| Interpreting Provider Notes | Any notes that were entered for the order by the Grading provider
| Results Sent Date | Date/time when results were sent (With multiple delivery endpoints this is the date/time when the system determined all items were delivered)
| Order State | US State where exam was performed
| Order Creation Source | Source of order submission. If Manual, indicates that a user created the order from a Device rather than it coming from Integration
