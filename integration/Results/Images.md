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
    - Image viewed at point of finding selection (works best when pathology is found)
    - Last image uploaded (Assumption being the camera operator stopped taking images when a good one was taken)
    - Best image selected from Camops or Order Manager
    - Marked on order submission 
    - AI selection
   
   *By default, AI selection is not enabled as there are costs associated with it.  Contact your IRIS sales representative if you wish to activate the AI Quality Image for report option.*

## Image Access

Depending on your camera selection and workflow, images may be acquired directly into the IRIS platform.  

While access is always available from the Order Manager application, you may have a requirement to store them yourself.  IRIS can support this through two image sharing options. 

- PACS Forwarding - For scenarios with DICOM cameras operating within an organization with an existing PACS, IRIS can forward all incoming images to one or more PACS.
- Cloud sharing - IRIS can also share images at the point of results delivery in an Azure blob storage account.  If this is provided within the IRIS Azure subscription, there may be costs associate with it. 

In either scenario, contact your IRIS sales representative to have image sharing activated on your account.



