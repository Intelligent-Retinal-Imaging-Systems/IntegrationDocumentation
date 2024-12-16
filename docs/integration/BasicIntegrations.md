---
title: Basic Integrations
nav_order: 2
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
IRIS can deliver results directly to a local file system within your network using the [IRIS EMR Proxy](/IntegrationDocumentation/docs/integration/IRISEMRProxy/). 

The typical payload for file system delivery is a PDF report with attached metadata.  Path names are template based and can include tokens dynamically swapped from details of the order. For example, you can configure the system to save the PDF as a file with the name including the MRN and date of service.  

Other payload options are available including files written with JSON encoded raw content.  

This option can be deployed standalone as the primary source of results or as a supplement to any other delivery mechanism. 

## SFTP 
Results can be delivered to an SFTP site you provide access to.  

- You can choose a payload type of PDF report or JSON encoded raw data that can include the PDF Report
- You may specify a single directory level that is used for all results
- File names are template based and can include tokens dynamically swapped from details of the order.  
- You must register an individual to be a contact point for delivery failures

To use SFTP Delivery, Contact <a href="mailto:support@irishelp.zendesk.com">IRIS Support</a>


## Fax
IRIS Can send your results to one or more fax numbers.

To setup fax delivery, contact <a href="mailto:support@irishelp.zendesk.com">IRIS Support</a>
