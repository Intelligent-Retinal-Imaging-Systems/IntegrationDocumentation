---
title: Workflows
parent: Cloud Direct
nav_order: 2
---


## Order Processing Workflows

IRIS is built on optionality and at the center of those options, is camera selection.  Images can be submitted to an order in a variety of ways, primarily based on the camera type.

1. Direct Integration to the IRIS platform - Cameras communicate directly to IRIS 
2. DICOM through an IRIS Proxy - Cameras communicate to an IRIS Proxy which in turn delivers DICOM images to the IRIS Platform
3. Camera Operator application - Images are passed through a file system and uploaded through the IRIS Camera Operator web application.
4. Cloud storage drop - You write images to an Azure Blob Storage container with two alternatives here.
    * **Before** the order is submitted
    * **After** the order is submitted


Option 4 is a Cloud Direct integration feature and the focus of this section.

### Image/Order Coordination
The timing in which images are dropped depends on your camera and workflow.  If your patient worklist is predictable, you would typically follow the Order First workflow.

##### Order First Workflow
This workflow starts with an order submission before the exam is to take place.  Images are written to blob storge in a prespecified container as they are taken.  The camera used in this workflow must be capable of attaching metadata to identify the image destination primarily through patient identifier.  This can either be Exif data or DICOM.

*When selecting this workflow, a listener is attached to the blob storage container and images are processed as they are received*

##### Image First Workflow
This workflow starts with uploading images with unique file names to a specified blob storage container.

When building the OrderRequest object, you include the Image array node which uniquely identifies each image used in the order.  Because you are identifying all the attributes of an image in this manner, the image itself does not require attached metadata.

The Image object allows you to specify both the blob storage container and filename.  In most cases, a single container is sufficient however you may use multiple containers if you gain convenience from that.  The primary concern is that the filenames are always unique within the container itself.

![alt text](/assets/important.png) Images that are identified in the OrderRequest object **must** be present in the specified location before the order is submitted.

##### <small>Example OrderRequest fragment</small>

<small>

```json
 "Camera": {           
    "LocalId": "1234",    
    "SerialNumber": "1234",
    "Images": [            
      {
        "LocalId": "1234-1-1", 
        "Taken": "2022-01-01T17:42:18.6936779+00:00",       
        "AzureBlobStorage": {
          "Container": "images",
          "FileName": "04211055-DFF7-41EF-9EF3-43FE61D10D43.jpg"
        },
        "Laterality": "OD"
      }
    ]
  },
```

</small>

*Including the LocalId (your image identifier) allows you to track Image events as they are posted.*

### Accessing Blob Storage
As mentioned in the Introduction, access to your blob storage account is provided to you through a connection string.

* The blob storage account is provision on request to the IRIS Support team.
* A blob storage account provided to you is **not** a shared resource, it is provisioned for you and you alone.
* The connection string is provided to you from the Administrator application on the **Integration** tab.
* The connection string has **write-only** access.

