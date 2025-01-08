---
title: Order Processing Integration
nav_order: 3
has_toc: false
---

## Order Processing with IRIS

While the IRIS platform is fully operable through a rich suite of <a href="https://portal.retinalscreenings.com">web based tools</a>, a more seamless workflow can be achieved through integration to your own platform. There are two main points of integration: Submission and Delivery.

- **Order Submission** is the process of submitting patients/orders to IRIS from your system.  This can be as simple as the uploading of a spreadsheet, or as detailed as the implementation of an HL7 interface.
  - Patients can be submitted to IRIS making them available for future orders
  - Orders can be created from existing patients or submitted with patient information embedded all in one call.  
- **Results Delivery** is the process of returning the result of an exam to your system (and/or related endpoints).  As with Submissions, there are a wide breadth of options available to meet your specific needs.

### Organizations, Sites, Patients and Orders

Before moving on to the different integration options, it is helpful to understand a few important concepts and terms related to the data hierarchy.  While there are a variety of workflows they all eventually funnel down to the following basic entities.  

- **Organizations**: You as a customer are considered an *Organization* within the IRIS platform (e.g.: My Organization is Standard Healthcare with clinics across three states)
  - Users can be members of one and only one *Organization*
  - An *Organization* is uniquely identified by ClientGuid which is assigned by IRIS and provided to you when required for certain integration types.
- **Clients/Sites**: *Organizations* have one to many *Clients* assigned to them.  
  - *Client* is the internal designation for this entity, whereas Site is more commonly referred to.
  - Utilization is dependent on your workflow.  
    - It could be a site, clinic, office or other type of facility
    - It could be a department that is or isn't physically located in the same facility as other departments.
    - It could be an event or other form of temporal scope
    - It could exist purely as a logical separation of patients
  - *Clients* have a single address to establish physical location
  - A *Client* may be assigned a LocalId based on your internal identifier (e.g.: The LocalId of Riverside Clinic is Riverside123)
  - Devices are assigned to *Clients*
- **Patients**: *Clients* contain *Patients* (e.g.: Patient with MRN 1234 was added to Riverside123)
  - Patient Identifiers are unique within a *Client* (e.g.: You can have one and only one patient with the MRN of 1234 assigned to Riverside123)
  - By configuration, *Patients* can be treated as unique across an *Organization* allowing them to float across *Clients*.
- **Orders**: *Orders* are created for *Patients*.  
  - An *Order* is an exam of a specific evaluation type (Diabetic Retinopathy, Glaucoma, etc.)
  - A *Patient* may have zero to many *Orders* but only one order may be open (not completed and not cancelled) at a time.
  - *Orders* must establish a US State where the exam is performed.  
    - *Orders* must be graded by providers licensed in that State (except when using AI grading)
    - By default, the State established for the *Client* of the *Patient* of the *Order* is assumed to be the State where the exam is performed
    - The US State may be overridden on order submission

### Which integration option is best for me?

#### By Business Sector

- Primary Care (small)
  - See [Cloud EMR Providers](/integration/IRISEMRCloudProviders) if you are using a Cloud EMR/EHR service.
  - See [Basic Integrations](/integration/BasicIntegrations) page
- Primary Care (large), IDN, FQHC see [EMR Integrations](/integration/EMRIntegrations) page
- Home Health Care see [Cloud Direct Integrations](/integration/CloudDirect) page
- Retail / Kiosk 
  - See [Cloud Direct Integrations](/integration/CloudDirect) for transactional submissions and results
  - See [Direct Messaging](/integration/DirectMessaging) for PCP notifications
- Payers 
  - See [Cloud Direct Integrations](/integration/CloudDirect) for options submitting patients/orders
  - See [Basic Integrations](/integration/BasicIntegrations) for batch results
  - See [Direct Messaging](/integration/DirectMessaging) for PCP notifications

#### By Technology

- For basic integrations revolving around file drops, SFTP or options that supplement manual workflows, navigate to the [Basic Integrations](/integration/BasicIntegrations) page
- If you are using a mainstream EMR/EHR (HL7 integrations) navigate to the [EMR Integrations](/integration/EMRIntegrations) page
- If you are using a Cloud based EMR/EHR Provider (Athena, OCHIN,etc...) navigate to the [SAAS (Cloud) EMR Integrations](/integration/IRISEMRCloudProviders) page
- If you are considering developing software, using batch oriented operations from your platform, using tools from a cloud based platform such as Salesforce, or any other custom type integration navigate to the [Cloud Direct Integrations](/integration/CloudDirect) page

### Is there a public API for IRIS?

In short, the answer is No.  IRIS does however provide other publicly accessible integration methods found on the [Cloud Direct Integrations](/integration/CloudDirect) page that are more reliable than conventional Rest APIs. The problem with APIs is that they combine the functions of transport, authentication, authorization and execution into a single call.  While this is convenient in a world where everything works perfectly, it also exposes the caller to any changes that may occur in any of those areas.  By isolating the delivery of requests (transport, authentication and authorization) to the Cloud Provider, the experience from the callers perspective is consistent and highly reliable.
