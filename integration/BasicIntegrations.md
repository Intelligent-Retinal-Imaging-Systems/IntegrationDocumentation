---
title: Basic Integrations
parent: Order Processing Integration
has_toc: false
---

# Basic Integrations
IRIS provides a variety of tools to allow basic integration services that may supplement or cover specific requirements.  

## Use case examples
- Receiving PDF reports as orders are completed
     - To your local file system
     - To an SFTP site
     - To a Fax machine
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