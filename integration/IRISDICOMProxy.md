---
title: IRIS DICOM Proxy
parent: Camera Integration
---


# IRIS DICOM Proxy Application

## Overview
The IRIS DICOM Proxy is an application that can be installed on any system running the Windows operating system to provide integration between IRIS and DICOM compatible devices through the conventional DICOM socket communication stack.  

The application appears as a PACS to DICOM Devices. 

## Why is it necessary
Conventional DICOM communication is not encrypted as it was designed assuming a local PACS.  Because IRIS is a cloud based SAAS application, DICOM content must be encrypted in transport to the IRIS system.  This is the primary function of the IRIS DICOM Proxy.

## PACS Forwarding
In the event you want to store DICOM content on a  local PACS, the IRIS DICOM Proxy can forward to one or more PACS systems based on device identity.  Notify your onboarding liaison if you have this requirement.  

*Access to images are available through the IRIS Order Manager application therefore it is typically not necessary to duplicate on your PACS*

## Distributed Installations
As with all IRIS proxy applications, the DICOM Proxy is stateless providing versatility in more complex networking requirements.  

- Cold Standby
    - You may install another instance on a secondary application server that in manually activated.  
    - The DICOM Proxy runs as Windows service, starting automatically on system boot.  
- Context Switching / Load Balancing
    - You may install and run as many instances across as many application servers as you wish.
    - While this is a viable option in terms of redundancy, it would be superfluous in the context of availability as the application is very light on system resources.
- Edge Routing
    - For remote locations where you prefer to avoid backhauling traffic, you may install a proxy at the edge assuming the networking requirements are met.  
    - DICOM devices can be individually configured to match Proxy instances. 

## Who supplies the hardware?
As with all IRIS Proxy applications, you must install the application on your own equipment.

## Application Maintenance and Support
The Proxy application was designed to be simple, leaving all the complicated operations to IRIS Cloud services.  Because of this, updates are infrequent and there are no ongoing maintenance requirements to run it.  It is a Windows service that either runs or it doesn't.

You, as the owner of the equipment, are responsible for the upkeep of the Windows operating system.  

If there are issues with the application, you may reach out to IRIS support for troubleshooting assistance.  There is no initial or ongoing requirement for remote access however you may choose to provide it during a support call.  Most issues can be diagnosed without this access.

## System Requirements
Details for hardware and network requirements can be found at [IRIS Proxy Application Requirements and Specifications](/integration/EMRProxyReqAndSpecs/)