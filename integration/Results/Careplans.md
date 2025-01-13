---
title: Care Plans
parent: Results Generation
nav_order: 4
has_toc: false
---

# Care Plans

Every finding, including no finding at all, resolves to a care plan.  A care plan consists of a title, instructions and relative priority.  When an order is graded, the care plan with the highest priority is assigned.  All attributes of care plans can be customized within the Administrator application.  You must establish all of your care plans before going live on the IRIS platform.

## Other Suspected Conditions

As described in the Findings section, *Other suspected conditions* are free text findings a grader may enter, when that finding is not available for selection in the Grader application. There are four distinct subsets of *Other suspected conditions*: **Not referable**, **Referable**, **Severe** and **Urgent**.  The care plan chosen is based on the subset of suspected condition selected by the grader before entering the finding.  Keep in mind that the grader is provided with content of your care plan when making this determination, thus they are intentionally providing indication of what they consider the most appropriate care plan.   

## Emergent Care Plans

If a grader finds pathology that requires immediate attention, the Emergent care plan is automatically selected and all emergency contacts are notified. You must establish Emergency contacts before going live on the IRIS platform.


## Care Plan Administration

Care plans can be established at the Organization level or any combination of Organization and Site/Client.  For example, you could have your standard care plan established at the Organization level and customize a single site for the Suspected Glaucoma finding. 

- Care plans follow an inheritance hierarchy (e.g.: Site A inherits all care plans from the organization, which inherits from the host default).
- Care plans are segmented by Evaluation type but can be shared.  For example, Suspected Macular Hole can be the same care plan in Glaucoma and DR evaluations although its relative priority will change as there are different options to prioritize within.
- Care plans are prioritized relative to other care plans.
- Care plans are grouped into care levels: Emergent, Urgent, Referable and Not Referable.
- Care plans may be shared for one or more findings or you may have a different plan for each.
- Care plans are derived at grading submission therefore changes you make now do not apply retroactively.
 


### Administrator application screen shot

![OrgLevelCarePlanEdit](/assets/careplanss1.png)