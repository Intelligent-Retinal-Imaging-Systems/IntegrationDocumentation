---
title: IRIS Proxy Requirements
parent: EMR Integrations
---

# IRIS EMR Proxy Application Requirements and Specifications
IRIS Content Transport facilitator for Order Submission and/or Results

# Best Practice

The following requirements outline the best practice for deploying the IRIS EMR Proxy application in your environment. 

## Hardware/Server Platform
ALL IRIS Proxy applications require minimal resources in terms of the hardware platform they are installed on.  If your organization has virtual server resources readily available, this is generally a good choice.  In this case IRIS recommends using your preferred Windows image as the software has no special requirements.

## Operating System

Windows Server 2012 and up or Windows 10, 11

*IRIS operates within a continuous development cycle maintaining close compatibility with Windows release cycles*

## Virtual Specs

1-2 virtual processors 

A minimum of 8 GB of RAM 

• OS Drive with at least 10 gb of free space (can be sized per your organization’s standard for OS drives) 

## Other Important Information

Even though the IRIS application is not considered life critical, IRIS will provide support for application in PROD as needed or defined by your standards for supporting internal applications. 

• There is no PHI cached or written to the server as part of the Transport process. 

• Local admin account on the server (for install and troubleshooting issues). This is typically a domain account that has access. 

• The server can be encrypted per your standards (hard drive encryption). 

The server can be patched, upgraded and monitored as needed or as defined by your standards. 

## IRIS Proxy Installation

IRIS provides a secure mechanism for installing Proxy applications. The process generally takes less than 15 minutes. 

Identify the individual in your organization that will be responsible for this action. IRIS refers to this individual as the Integration Administrator (You may have multiple individuals with this role). 

Must have access to the computer it will be installed on 

o Should have general knowledge of Windows and Windows Services 

Should understand the necessity to use a domain level service account should security policies dictate 

o Should understand local policies that could prevent the application from being installed 

Provide the email address of Integration Administrator to your IRIS onboarding liaison. 

o Due to the security requirements for Integration, only authorized IRIS employees can invite an Integration Administrator into the IRIS system. 

• The Integration Administrator will receive an invitation to the IRIS system in an email coming from Microsoft. This is the same process used for onboarding all users into the IRIS system. 

TEC 001 Rev F  CN0059

CONFIDENTIAL  Effective

010/06/2023 

。Once registered, Access to the Proxy installation files are available from the IRIS Portal from the Integration Files link (see screen shots below).

O Integration Installation files contained here are specific to your environment

Installation files are packaged as MSI.

Download the installation file and run it. The only option you will have is whether or not to specify a service account. If not explicitlyset, the default NT Service Account (local) is used.

### Test system installations

For customers who wish to create a test environment (typically for EMR Proxy integration), notify your onboarding liaison of this requirement.

Following the same procedures outlined above, the Integration Administrator must first register in the IRIS production system.

. The Integration Administrator should then email IRIS support and request setup within the Test environment

- Once the IRIS Support Team has completed the request, the Integration Administrator can then login to the IRIS test portal using https://portal-qa.retinalscreenings.com

. Follow the same procedures outlined above for Production installations.


| IrIsHome | My Apps |  | MR TATHAN |
| -- | -- | -- | -- |
| My ProfileLicensesPermissions |  |  |  |
| NotificationsDocumentationFormsRelease Notes | Reading Center | Admin | Gre |
| Integration Files | Camera Operator | r Check-In | Order A |



| Home | Integration Files |  |
| -- | -- | -- |
| My Profile | Name |  |
| LicensesPermissions | DICOM Proxy-Iris | DOWNLOAD |
| Notifications Documentation | EMR Proxy-Iris | DOWNLOAD |
| Forms |  |  |
| Release Notes |  |  |
| Integration Files |  |  |


### URLs to Whitelist:

### PROD

irisicdprodb.blob.core.windows.net 

iris-clientresults-prodb.servicebus.windows.net 

iris-organization-notification-prod.servicebus.windows.net 

config-proxy-prodb.azconfig.io 

login.microsoftonline.com 

PROD API

order-api.retinalscreenings.com 

icd-api.retinalscreenings.com 

icemr-api.retinalscreenings.com 

results-api.retinalscreenings.com 

### TEST 

irisicdqa.blob.core.windows.net 

iris-clientresults-qa.servicebus.windows.net 

iris-organization-notification-qa.servicebus.windows.net 

config-proxy-qa.azconfig.io 

### TEST API

order-api-test.retinalscreenings.com 

icd-api-test.retinalscreenings.com 

icemr-api-test.retinalscreenings.com 

results-api-test.retinalscreenings.com 

# REMIDIO CAMERAS ONLY 

intapi.retinalscreenings.com 

intapi2.retinalscreenings.com 

## Outbound IP Ports 

The following IP ports should not be blocked to the Internet: 

443 – Standard HTTPS traffic 

5671 – AMQP 

TEC 001 Rev F  CN0059 

CONFIDENTIAL  Effective 

010/06/2023 



