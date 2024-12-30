---
title: IRIS DICOM Proxy
parent: Camera Integration
---


# IRIS DICOM Proxy Application

## Overview
The IRIS DICOM Proxy is an application that can be installed on any system running the Windows operating system to provide integration between IRIS and DICOM compatible devices through the conventional DICOM socket communication stack.  

## Why is it necessary
Conventional DICOM communication is not encrypted as it was designed assuming a local PACS.  Because IRIS is a cloud based SAAS application, DICOM content must be encrypted in transport to the IRIS system.  This is the primary function of the IRIS DICOM Proxy.

## PACS Forwarding
In the event you will to store DICOM content on your own local PACS, the IRIS DICOM Proxy can forward to one or more PACS systems based on device identity.  Notify your onboarding liaison if you have this requirement.  

## Who supplies the hardware
As with all IRIS Proxy applications, you must install the application on your own equipment.  

## Support
The Proxy application was designed to be simple, leaving all the complicated operations to IRIS Cloud services.  Because of this, there are not frequent updates and no ongoing maintenance requirements for the application.  

You, as the owner of the equipment, are responsible for the upkeep of the Windows operating system.  

If there are issues with the application, you may reach out to IRIS support for troubleshooting assistance.  There is no initial or ongoing requirement for remote access however you may choose to provide it during a support call.  Most issues can be diagnosed without this access.

## System Requirements
Details for hardware and network requirements can be found at [IRIS Proxy Application Requirements and Specifications](/docs/integration/EMRProxyReqAndSpecs/)