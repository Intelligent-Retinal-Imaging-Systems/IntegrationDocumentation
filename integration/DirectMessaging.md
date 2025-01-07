---
title: Direct Messaging
parent: EMR Integrations
has_toc: false
---

# Direct Messaging
Direct Messaging, also known as Direct Secure Messaging, is a secure method to exchange health information from within certified EMR/EHRs or other technology. It allows for simple, HIPAA-compliant, encrypted transmission of Protected Health Information to or from any Direct address.

## Results
IRIS has the ability to send exam results to one or more recipients through Direct Messaging assuming one of the following criteria is met:
- Delivery instructions are specified with each order 
    - A target direct address is supplied on order submission.
    - A target NPI is supplied on order submission and that NPI is found in the Direct Messaging directory. 
- Delivery instructions are set for org/site
    - A target direct address is configured on the organization level (all sites)
    - A target direct address is configured per site for all related results 


Results are delivered as a PDF report encapsulated in an Unstructured (CDA) Document.  At minimum the document is hydrated with patient name, birthdate and gender as those are required fields for any IRIS order.  If supplied on order submission, the document can contain the following additional items related to the patient:

- Address
- Phone
- Marital Status
- Race
- Ethnicity
- Language 

*IRIS does accept nor provide SSN numbers thus no patientRole.Id node is supplied with the Unstructured document.*

Parsing and assignment of the results to a patient chart is a function of the target EMR system.

## When would I want to use Direct Messaging?
This is highly dependent on the function of your organization.  

If you are a Payer or operating on behalf of Payers, you could use this option for delivering the results to the patients Primary Care Provider. 

This may also be used as an interim solution to a full HL7 integration when resources are not available for a quick implementation.  Direct Messaging only requires a Direct Address that is being monitored by the target EMR/EHR system. 

Unstructured documents could potentially be used for any other application where IRIS is notifying the submitting organization of an event.  Just consider that linking to a patient is not as precise as other options such as an HL7 MDM message.   

## Transaction Fees
There are transaction fees associated with each message sent through this mechanism and those fees are passed on to you the client.  Work with your IRIS sales representative in order to identify your responsibilities and any costs associated with its use.