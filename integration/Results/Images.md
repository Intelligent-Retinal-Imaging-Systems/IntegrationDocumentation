---
title: Images
parent: Results Generation
nav_order: 1
has_toc: false
---

# Images in Results

During the exam, Images are collected for one or more eyes.  For tabletop cameras, the result is generally the same: One image is captured per eye.

For handheld cameras things are different.  It is more difficult to capture images with a handheld camera due to the process of aligning the camera with the eye when both sides of the equation can move.  

IRIS typically receives multiple images per eye for exams using handheld cameras.

## Multi image considerations

When more than one image is submitted per eye, there are new complexities to consider for results:

- Findings 
  - There is no longer a one to one relationship between [finding](/integration/Results/Findings) and image.
  - A single finding could be determined from multiple images
  - A single trace of pathology found on any image could prevent an otherwise ungradable eye.
- Ungradable images
  - The context of gradeability moves from *the image* to *the eye*.
  - When providers mark an eye as ungradable, only a single reason is provided regardless of how many images were in the collection.  
- Results Report 
  - The standard report template provides one image per eye
  - IRIS employs several techniques to use the best available image from each eye
    - Image displayed at point of finding selection by Grader (works best when pathology is found)
    - Last image uploaded 
      - Assumption being the camera operator stopped taking images when a good one was taken
      - Only works when Metadata exists for the image indicating when the image was taken
    - A *Best Image* selection was made from [Camera Operator](https://camops.retinalscreenings.com) or [Order Manager](https://ordermanager.retinalscreenings.com)
    - AI selection
   
   *By default, AI selection is not enabled as there are costs associated with it.  Contact your IRIS sales representative if you wish to activate the AI Quality Image for report option.*

## Image Access

Depending on your camera selection and workflow, images may be acquired directly into the IRIS platform.  

While access is always available from the Order Manager application, you may have a requirement to store them yourself.  IRIS can support this through two image sharing options. 

- PACS Forwarding 
  - For scenarios with DICOM cameras operating within an organization with one or more PACS
  - Routing is configurable to either
    - Common PACS.  A single PACS endpoint for all images
    - AETitle mapped.  The source cameras AETitle maps to a PACS endpoint
- Cloud sharing 
  - Images are pushed to an Azure blob storage account during the Results Delivery process.  
  - Metadata is attached to each image using Azure Metadata key/value pairs to allow programmatic processing.
  - The target storage account can be within your own Azure subscription or within the IRIS Azure subscription 
    - Depending on volume, image size and duration of storage, there may be additional costs associated with sharing in the IRIS Azure subscription

In either scenario, contact your IRIS sales representative to have image sharing activated on your account.



