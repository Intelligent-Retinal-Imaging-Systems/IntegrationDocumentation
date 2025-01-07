---
title: Order Processing Integration
nav_order: 3
has_toc: false
---

# Order Processing with IRIS

While the IRIS platform is fully operable through a rich suite of <a href="https://portal.retinalscreenings.com">web based tools</a>, a more seamless workflow can be achieved through integration to your own platform. There are two main points of integration: Submission and Delivery.

> Order Submission is the process of submitting patients/orders to IRIS from your system.  This can be as simple as the uploading of a spreadsheet, or as detailed as the implementation of an HL7 interface.  

> Results Delivery is the process of returning the result of an exam to your system (and/or related endpoints).  As with Submissions, there are a wide breadth of options available to meet your specific needs.

### Which integration option is best for me?

#### By Business Sector 


- Primary Care (small) 
    - See [Cloud EMR Providers](/integration/IRISEMRCloudProviders.md) if you are using a Cloud EMR/EHR service.
    - See [Basic Integrations](/integration/BasicIntegrations) page
    
- Primary Care (large), IDN, FQHC see [EMR Integrations](/integration/EMRIntegrations) page
- Home Health Care see [Cloud Direct Integrations](/integration/CloudDirect) page
- Retail / Kiosk 
    - See [Cloud Direct Integrations](/integration/CloudDirect) for transactional submissions and results
    - See [Direct Messaging](/integration/DirectMessaging.md) for PCP notifications
- Payers 
    - See [Cloud Direct Integrations](/integration/CloudDirect) for options submitting patients/orders
    - See [Basic Integrations](/integration/BasicIntegrations) for batch results
    - See [Direct Messaging](/integration/DirectMessaging.md) for PCP notifications

#### By Technology 

- For basic integrations revolving around file drops, SFTP or options that supplement manual workflows, navigate to the [Basic Integrations](/integration/BasicIntegrations) page
- If you are using a mainstream EMR/EHR (HL7 integrations) navigate to the [EMR Integrations](/integration/EMRIntegrations) page
- If you are using a Cloud based EMR/EHR Provider (Athena, OCHIN,etc...) navigate to the [SAAS (Cloud) EMR Integrations](/integration/IRISEMRCloudProviders) page
- If you are considering developing software, using batch oriented operations from your platform, using tools from a cloud based platform such as Salesforce, or any other custom type integration navigate to the [Cloud Direct Integrations](/integration/CloudDirect) page