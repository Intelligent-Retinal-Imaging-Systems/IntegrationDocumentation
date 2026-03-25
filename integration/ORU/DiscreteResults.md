---
title: Discrete Results
parent: ORU (ORU-R01)
nav_order: 1
---

## Discrete Results (default observations)
Discrete results can be sent across a series of OBX segments.  IRIS provides a default set but these may be customized (See [Custom observations](#discrete-results-custom-observations)) to suite your specific needs. 

There are four general types of observation provided in discrete results:


| Type | (Default) Observation Identifier |  (Default) Observation Values | Description 
| -- | -- | -- | --
| Severity (Summary) | SEVERITY | NORMAL,ABNORMAL,CRITICAL | Severity based on most significant finding 
|  Diagnosis | {RIGHT/LEFT}{FINDINGTYPE} | Unique per finding | Finding for specific condition for each eye (one OBX per eye and finding type)
| Suspected Conditions | {RIGHT/LEFT}{OTHERRETIN} | None OR comma delimited list of suspected conditions | Suspected conditions noted by grader (per eye)
| Image quality | {RIGHT/LEFT}{QUALAPP} | Gradable Image,Ungradable Image | Specifies if images were sufficient for grading (per eye)

##### ![alt text](/assets/hl7sample.png) Default Discrete Results OBX Series Example
```
OBX|1|ST|SEVERITY^^IRIS|1|NORMAL||||||F 
OBX|2|ST|RIGHTDIABRETIN^^IRIS|2|None||||||F 
OBX|3|ST|RIGHTMACEDEMA^^IRIS|3|None||||||F 
OBX|4|ST|RIGHTOTHERRETIN^^IRIS|4|None||||||F 
OBX|5|ST|RIGHTQUALAPP^^IRIS|5|Gradable Image||||||F 
OBX|6|ST|LEFTDIABRETIN^^IRIS|6|None||||||F 
OBX|7|ST|LEFTMACEDEMA^^IRIS|7|None||||||F 
OBX|8|ST|LEFTOTHERRETIN^^IRIS|8|None||||||F 
OBX|9|ST|LEFTQUALAPP^^IRIS|9|Gradable Image||||||F 
```
*The Sub-ID field is unique within the context of IRIS Discrete results*


### Severity Observation
The Severity observation is provided in a single OBX segment and establishes the overall severity of the exam based on the most significant finding.

*If an order is deemed ungradable, the Severity observation is omitted by default however this may be customized to be included with a specific observation value for that scenario.*

>* Identifier: **SEVERITY**
>* Values: **NORMAL**,**ABNORMAL**,**CRITICAL**
>* Coding Flag: ABNORMAL=**A**,CRITICAL=**AA**

<small>*By default, a normal finding does not resolve to a value in the Coding Flag field as per the HL7 V2 field definition: **Abnormal** Flags.*</small>


##### ![alt text](/assets/hl7sample.png) Severity OBX Segment Example 
```
OBX|1|ST|SEVERITY^^IRIS|1|NORMAL||||||F
```
 
### Diagnosis Observation(s) 
Depending on the exam type, you may have one or more diagnosis observations.  A **diagnosis** is a finding type that must be explicitly answered for in an exam grading.  This differs from suspected findings in that suspected findings are implied negative unless otherwise noted by a grader.

The most common exam type is DR which carries with it two distinct diagnosis requirements: Diabetic Retinopathy and Macular Edema.

#### DR Observation Identifier
* Observation Identifiers: **RIGHTDIABRETIN**,**LEFTDIABRETIN**
* Values: **None**,**Mild**,**Moderate**,**Severe**,**Proliferative**,**Indeterminable**
* Abnormal Coding Flag: 
    * **A** : Indeterminable,Mild,Moderate,Severe
    * **AA** : Proliferative

##### ![alt text](/assets/hl7sample.png) Diabetic Retinopathy OBX Example
```
OBX|2|ST|RIGHTDIABRETIN^^IRIS|2|Moderate|||A|||F 
OBX|6|ST|LEFTDIABRETIN^^IRIS|6|None||||||F 
```    

#### ME Observation Identifier
* Observation Identifiers: **RIGHTMACEDEMA**,**LEFTMACEDEMA**
* Values: **None**,**Positive**
* Abnormal Coding Flag: Positive=**AA**  

##### ![alt text](/assets/hl7sample.png) Macula Edema OBX Example
```
OBX|3|ST|RIGHTMACEDEMA^^IRIS|3|Positive|||AA|||F 
OBX|7|ST|LEFTMACEDEMA^^IRIS|7|None||||||F 
```    

#### HIV Observation Identifier
* Observation Identifiers: **RIGHTHIVRETIN**,**LEFTHIVRETIN**
* Values: **None**,**Mild**,**Moderate**,**Severe**,**Proliferative**,**Indeterminable**
* Abnormal Coding Flag: 
    * **A** : Indeterminable,Mild,Moderate,Severe
    * **AA** : Proliferative

##### ![alt text](/assets/hl7sample.png) HIV Retinopathy OBX Example
```
OBX|2|ST|RIGHTHIVRETIN^^IRIS|2|Moderate|||A|||F 
OBX|6|ST|LEFTHIVRETIN^^IRIS|6|None||||||F 
```    
 
#### AMD Observation Identifier
* Observation Identifiers: **RIGHTAMD**,**LEFTAMD**,**RIGHTDRYAMD**,**LEFTDRYAMD**,**RIGHTWETAMD**,**LEFTWETAMD**
* Values: **No Observable**,**Indeterminable**,**Early Stage**,**Intermediate Stage**,**Adv. Atrophic w/ Subfoveal Involvement**,**Adv. Atrophic w/o Subfoveal Involvement**,**Advanced**,**Positive**
* Abnormal Coding Flag: 
    * **A** : Dry / Less than Advanced
    * **AA** : Wet/Advanced

##### ![alt text](/assets/hl7sample.png) AMD OBX Example
```
OBX|2|ST|LEFTDRYAMD^^IRIS|2|Early Stage|||A|||F 
OBX|3|ST|LEFTWETAMD^^IRIS|3|Positive|||AA|||F 
OBX|7|ST|RIGHTDRYAMD^^IRIS|7|No Observable||||||F 
OBX|8|ST|RIGHTWETAMD^^IRIS|8|No Observable||||||F 
```    

 
### Suspected Findings Observation
Depending on grading type selection, you may have an observation finding for other suspected conditions on the left or right eye.

By default all suspected findings are provided in the single observation segment as a comma delimited list.


#### Suspected Pathology Observation Identifier
* Observation Identifiers: **RIGHTOTHERRETIN**,**LEFTOTHERRETIN**
* Values: Comma delimited list of noted suspected pathologies.
* Abnormal Coding Flag: 
    * **A** : Referrable suspected pathologies
    * **AA** : Urgent and Emergent suspected pathologies

##### ![alt text](/assets/hl7sample.png) Suspected Pathology OBX Example

Referrable
```
OBX|4|ST|RIGHTOTHERRETIN^^IRIS|4|Suspected Glaucoma,Suspected Macular Hole|||A|||F 
OBX|8|ST|LEFTOTHERRETIN^^IRIS|8|Suspected Choroidal Nevus||||||F 
```    

Emergent
```
OBX|4|ST|RIGHTOTHERRETIN^^IRIS|4|Suspected Bilateral Papilledema|||AA||F 
OBX|8|ST|LEFTOTHERRETIN^^IRIS|8|Suspected Bilateral Papilledema|||AA|||F 
```    

 
### Image Quality (Gradeability)
By default, an observation segment is added to provide gradeability for the images taken, one per eye.  
If the entire order is considered ungradable, no other discrete result segments will be included.  By configuration, you may choose to include a SEVERITY segment with an Abnormal Coding Flag.



#### Image Quality Observation Identifier
* Observation Identifiers: **RIGHTQUALAPP**,**LEFTQUALAPP**
* Values: **Gradable Image**, **Not Gradable Image**
* Coding Flag: Not used
    

##### ![alt text](/assets/hl7sample.png) Image Quality OBX Example

```
OBX|5|ST|RIGHTQUALAPP^^IRIS|5|Gradable Image||||||F 
OBX|9|ST|LEFTQUALAPP^^IRIS|9|Not Gradable Image||||||F 
```
 

## Discrete Results (custom observations)

The IRIS system is designed with the flexibility to explicitly define observation findings.  

* Specify your own observation identifiers
* Assign coding flags specific to individual findings
* Customize SEVERITY observation values
* Customize observation identifiers and values for gradeability scenarios
* Override coding system

Building a custom observation set is a complex and tedious task as it requires you to map every possibility you wish to accommodate.  Software is currently in development to support building your own custom observation set.  To use the functionality today you must create a spreadsheet that includes the entire matrix of Observation identifier, values, and coding flags based on the exam types you will be performing.  

##### ![alt text](/assets/hl7sample.png) Custom Discrete Results OBX Series Example

The follow example takes advantage of custom observation identifiers, individual suspected findings by severity, coding system and alternate coding flags

```
OBX|1|ST|EXAMSUMMARY^^IRIS31|1|Emergent Findings|||AA|||F 
OBX|2|ST|DIABETICRETINOPATHY_OD^^IRIS31|2|None||||||F 
OBX|3|ST|SUSPECTEDCONDITION_REFERRABLE_OD^^IRIS31|3|Suspected Glaucoma|||A|||F 
OBX|4|ST|SUSPECTEDCONDITION_REFERRABLE_OD^^IRIS31|4|Suspected Cataract|||A|||F 
OBX|5|ST|SUSPECTEDCONDITION_EMERGENT_OD^^IRIS31|5|Suspected Bilateral Papilledema|||AA|||F 
OBX|6|ST|FUNDUSIMAGEQUALITY_OD^^IRIS31|6|Sufficient|||N|||F 
OBX|11|ST|FUNDUSIMAGEQUALITY_OS^^IRIS31|11|Insufficient|||L|||F  
```

