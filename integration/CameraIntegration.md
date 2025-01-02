---
title: Camera Integration
nav_order: 2
has_toc: false
---


# Camera Integration with IRIS
IRIS supports a variety of intake workflows in order to submit images and have them applied to orders. 

While the approach varies widely between camera types, there are just two basic functions we are trying to achieved with any integration.  
- At minimum, we must be able to extract images to the IRIS platform
- For more reliable workflows we want to push worklists to the device. 

## Pushing images to the IRIS Platform
Depending on the camera's capabilities, pushing images from an exam to the platform can occur in one of many ways. 

- The most basic form of integration is directly assigning images from a file system to an order using the [IRIS Camera Operator application](https://camops.retinalscreenings.com).  *You must be a registered user in order to access this application*
- In cases where the image contains embedded meta data (e.g.: Exif), that can be used to link the image to an order, image submission can be performed in a more automated fashion.  
- In the case of fully integrated solutions such as DICOM, images are pushed seamlessly from the device to the IRIS platform. 
    - DICOM integration is provided through the [IRIS DICOM Proxy](/docs/integration/IRISDICOMProxy/).
- Other devices such as the Remidio Camera, are tightly integrated to IRIS out of the box.

## The Worklist function
A workflow that uses the camera worklist function can be summarized in three steps:
1. Orders are submitted to IRIS via Order Processing Integration
2. Cameras, linked to Site/Departments or Operators, present the patient list on request from the camera UI. 
3. Images are submitted to IRIS linked to the original worklist item. 

This workflow insures that the order created on your platform is linked to the images taken from the camera without the possibility of user entry error on the device. 

The primary and preferred form of camera integration is through **DICOM**.  Generally speaking, you will find DICOM support on most desktop cameras.  When DICOM is not available, desktop cameras typically provide some form of file system sharing.  

Handheld cameras are integrated in a variety of ways.

For specific details on all cameras go to our [IRIS Supported Devices](/docs/integration/IRISSupportedDevices/) page.

### OCT Cameras
IRIS provides integration with OCT Cameras via **DICOM**. For information on specific OCT devices contact IRIS sales support.
