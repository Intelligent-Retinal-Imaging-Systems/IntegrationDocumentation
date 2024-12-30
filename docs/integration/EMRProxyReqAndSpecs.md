---
title: IRIS Proxy Requirements
has_toc: false
---

# IRIS Proxy Application Requirements and Specifications
This document contains details for installing and maintaining IRIS Proxy applications.

## Hardware/Server Platform
ALL IRIS Proxy applications require minimal resources in terms of the hardware platform they are installed on.  If your organization has virtual server resources readily available, this is generally a good choice.  In this case IRIS recommends using your preferred Windows image as the software has no special requirements.

## Operating System

Windows Server 2012 and up or Windows 10, 11

*IRIS operates within a continuous development cycle maintaining close compatibility with Windows release cycles*

## Virtual Specs

1-2 virtual processors 

A minimum of 8 GB of RAM 

• OS Drive with at least 10 Gb of free space (can be sized per your organization’s standard for OS drives) 

## Other Important Information

Even though the IRIS application is not considered life critical, IRIS will provide support for application in PROD as needed or defined by your standards for supporting internal applications. 

• There is no PHI cached or written to the server as part of the Transport process. 

• Local admin account on the server (for install and troubleshooting issues). This is typically a domain account that has access. 

• The server can be encrypted per your standards (hard drive encryption). 

The server can be patched, upgraded and monitored as needed or as defined by your standards. 

## IRIS Proxy Installation

IRIS provides a secure mechanism for installing Proxy applications. The process generally takes less than 15 minutes. 

- Identify the individual in your organization that will be responsible for this action. IRIS refers to this individual as the Integration Administrator (You may have multiple individuals with this role). 

    - Must have access to the computer it will be installed on 
    - Should have general knowledge of Windows and Windows Services 
    - Should understand the necessity to use a domain level service account should security policies dictate 
    - Should understand local policies that could prevent the application from being installed 
- Provide the email address of Integration Administrator to your IRIS onboarding liaison. *Due to the security requirements for Integration, only authorized IRIS employees can invite an Integration Administrator into the IRIS system.*
    - The Integration Administrator will receive an invitation to the IRIS system in an email coming from Microsoft. This is the same process used for onboarding all users into the IRIS system. 
- Once registered, Access to the Proxy installation files are available from the IRIS Portal from the Integration Files link (see screen shots below).
    - Integration Installation files contained here are specific to your environment
    - Installation files are packaged as MSI.
- Download the installation file and run it. The only option you will have is whether or not to specify a service account. If not explicitly set, the default NT Service Account (local) is used.

### Test Environment Installations

For customers who wish to create a test environment (typically for EMR Proxy integration), notify your onboarding liaison of this requirement.

- Following the same procedures outlined above, the Integration Administrator must first register in the IRIS production system.
- The Integration Administrator should then email IRIS support and request setup within the Test environment
- Once the IRIS Support Team has completed the request, the Integration Administrator can then login to the IRIS test portal using https://portal-qa.retinalscreenings.com

Follow the same procedures outlined above for Production installations.

## Install Screen shots

### Login to Portal
![LoginToPortal](/docs/assets/integrationappsinstallss1.png)

### Navigate to apps
![LoginToPortal](/docs/assets/integrationappsinstallss.png)


## Internet Access /  Firewall rules
IRIS Proxies must communication to specific resources in the IRIS cloud without Firewall and/or Web Proxy restrictions. 

## Outbound IP Ports 
The following IP ports should **not** be blocked from the Proxy application(s) to the Internet: 

| Port | Use | Comments
| -- | -- | -- | 
| 443 | Standard HTTPS | TLS 1.3
| 5671 | AMQP | Azure Service Bus Queue


## Address/endpoint exceptions
The following addresses must be accessible from the IRIS Proxy application(s).

### Web Proxy Systems
If your company uses a Web Proxy application to monitor web traffic, you MUST add all of the following addresses to that systems whitelist so that it does not attempt to reroute the traffic in a "Man in the Middle" manner.  

### Production Environment
The following addresses are required for production:

| Endpoint | Usage |
| -- | -- | 
| irisicdprodb.blob.core.windows.net | Azure blob storage - Files dropped from Proxy to IRIS
| iris-clientresults-prodb.servicebus.windows.net | Azure Service Bus - Queue used for signaling results ready for pickup
| iris-organization-notification-prod.servicebus.windows.net | Azure Service Bus - Queue used for Proxy Management
| config-proxy-prodb.azconfig.io | Azure App Settings container - Proxy Configuration settings
| login.microsoftonline.com | Authentication and Authorization
| icd-api.retinalscreenings.com | IRIS API for DICOM/Image related activities
| icemr-api.retinalscreenings.com | IRIS API FOR EMR/System Integration activities

### Test  Environment 
The following addresses are required for the Test environment.

| Endpoint | Usage |
| -- | -- | 
| irisicdqa.blob.core.windows.net | Azure blob storage - Files dropped from Proxy to IRIS
| iris-clientresults-qa.servicebus.windows.net | Azure Service Bus - Queue used for signaling results ready for pickup
| iris-organization-notification-qa.servicebus.windows.net | Azure Service Bus - Queue used for Proxy Management
| config-proxy-qa.azconfig.io | Azure App Settings container - Proxy Configuration settings
| icd-api-test.retinalscreenings.com | IRIS API for DICOM/Image related activities
| icemr-api-test.retinalscreenings.com | IRIS API FOR EMR/System Integration activities

### REMIDIO CAMERAS ONLY 
If you are using Remidio cameras within your network, the following endpoints must be whitelisted.

- intapi.retinalscreenings.com 
- intapi2.retinalscreenings.com 


 



