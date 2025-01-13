---
title: Findings
parent: Results Generation
nav_order: 2
has_toc: false
---

# Findings

When an order is graded, the results are returned, including all findings. The findings that may return on an order are based on the evaluation type being performed.  The most common evaluation type for the IRIS platform is DR (Diabetic Retinopathy).

## Diagnosed vs Suspected

There are two classifications for findings: Diagnosed and Suspected.  

Diagnosed conditions return with explicit results.  For example a DR Evaluation, assuming it was gradable, will always return a finding for each eye evaluated, with one of the following:

- None
- Mild
- Moderate
- Severe
- Proliferative
- Indeterminable (see Ungradable Eyes for details)

## Suspected Conditions

Unless otherwise stated, suspected conditions are assumed not to exist.  In other words, an exam that is not graded with *Suspected Glaucoma* implies that Glaucoma was not suspected by the grader. Keep in mind, that the term suspected works in both directions.  It can no more be confirmed than excluded, therefore the absence of a suspected condition does not guarantee that the condition does not exist.


## Ungradable Eyes
In some cases, images taken for an eye are not sufficient for grading.  An individual eye may be marked as ungradable as well as the entire order.  For each eye not gradable, you will receive neither diagnosed, nor suspected conditions.  You will be provided with a general classification of why the images could not be graded.

There is another case that involves partially gradable images.  When it is not possible for the grader to make the diagnosis required on a specific evaluation type, but other pathology is found, the diagnosis is returned as Indeterminable.  You can only have an Indeterminable finding in combination with a suspected condition on the same eye.

## Raw Results with No Findings

Integration types receiving raw results will not contain any content for ungradable eyes therefore any programmatic processing of results should consider the ungradable flag before findings. This is most important when processing serialized JSON directly as some nodes of the object hierarchy may not exist.

## Multiple Images Per Eye

Depending on your workflow, orders could contain more than one image taken per eye.  In this scenario, always consider that grading is performed on the eye level and that findings could be determine from any combination of available images.  There is no direct linkage between an individual image and finding.  As well, an ungradable determination does not include the cause on an individual image level, meaning that the individual cause noted by the grader may not be exact (e.g.: Generally speaking the eye was ungradable because of a dirty lens). 

## Common Findings

When provided as raw result content, the following table contains the commonly returned values.

*Other suspected pathology finding types are submitted with free from text from the grader.  IRIS may also choose to add new Suspected Pathology options without advanced notification. For these reasons you must be able to process Finding/Qualifier combinations beyond what is listed in the table below.*


| Finding | Qualifier
| -- | --
| Diabetic Retinopathy	| Indeterminable
| Diabetic Retinopathy	| None
| Diabetic Retinopathy	| Moderate
| Diabetic Retinopathy	| Severe
| Diabetic Retinopathy	| Proliferative
| Diabetic Retinopathy	| Positive
| Dry AMD | Indeterminable
| Dry AMD | Intermediate Stage
| Dry AMD | No Observable
| Dry AMD | Adv. Atrophic w/o Subfoveal Involvement
| Dry AMD | Adv. Atrophic w/ Subfoveal Involvement
| Dry AMD | Early Stage
| Glaucoma | None
| Glaucoma | Positive
| HIV Retinopathy | None
| HIV Retinopathy | Positive
| Suspected HTN Retinopathy	| 
| Macular Edema | None
| Macular Edema | Positive
| Not Gradable |	
| Other  |  {Free form text}
| Suspected Bilateral Papilledema	|
| Suspected Cataract	|
| Suspected Diabetic Retinopathy - Mild Only	|
| Suspected Diabetic Retinopathy - Moderate to Proliferative	|
| Suspected Disc Edema |
| Suspected Dry AMD |
| Suspected Epiretinal Membrane |
| Suspected Geographic Atrophy |
| Suspected Glaucoma |
| Suspected Macular Edema |
| Suspected Macular Hole |
| Suspected Other Disease |
| Suspected Vein Occlusion |
| Suspected Wet AMD |
| Wet AMD	| Positive
| Wet AMD	| Indeterminable
| Wet AMD	| No Observable
    
    

 


 
