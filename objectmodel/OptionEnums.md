---
title: Option Enumerations
parent: Object Models
nav_order: 5
---

{: .no_toc }



# Option Enumerations

The following tables provide acceptable values for option properties.

### 📊 GenderContext

| Id | Value | Description 
| -- | -- | --
| 0 | Unknown |  Not set  
| 1 | IdentityGender | Gender individual identifies as 
| 2 | BirthGender | Gender individual was designated at birth 

 
### 📊 Race 

<small>You may use any of the HL7 Ethnicity codes listed on <a href="https://terminology.hl7.org/6.1.0/CodeSystem-v3-Race.html">Hl7 Coding: Race</a></small>

| Value | Description
| -- | --
| 1002-5 | American Indian or Alaska Native 
| 2028-9 | Asian 
| 2054-5 | Black or African American 
| 2076-8 | Native Hawaiian or Other Pacific Islander 
| 2131-1 | Other Race 
| 2106-3 | White 


### 📊 Ethnicity 

<small>You may use any of the HL7 Ethnicity codes listed on <a href="http://terminology.hl7.org/CodeSystem/v3-Ethnicity">Hl7 Coding: Ethnicity</a></small>

| Value | Description
| -- | --
| 2137-8 | Spaniard 
| 2148-5 | Mexican
| 2155-0 | Central American 
| 2180-8 | Puerto Rican 
| 2182-4 | Cuban 
| 2149-3 | Mexican American 

### 📊 Language 

<small>You may use any of the HL7 Language codes listed on <a href="https://www.hl7.org/fhir/valueset-languages.html">Hl7 Coding: Languages</a></small>

| Value | Description
| -- | --
| en | English 
| en-US | US English 
| fr | French 
| es | Spanish
| it | Italian 
| pt | Portuguese 
| zh | Chinese 

### 📊 Gender  

| Id | Value | Description  
| -- | -- | --
| 0 | U | Unspecified 
| 1 | M | Male
| 2 | F | Female 
| 3 | N | Non binary 
| 4 | O | Other 
| 5 | TM | Transgender Male 
| 6 | TF | Transgender Female 
| 7 | ND | Non disclosed 
| 8 | EQ | Exploring or Questioning 
| 9 | NL | Not listed 
| 10| X | Not exclusively Male or Female 

### 📊 Marital Status  

<small>Items in this list are based on the HL7 standard here: http://terminology.hl7.org/CodeSystem/v3-MaritalStatus </small>

| Id | Value | Description 
| -- | -- | --
| 0 | A | Annulled 
| 1 | D | Divorced 
| 2 | I | Interlocutory 
| 3 | L | Legally Separated 
| 4 | M | Married 
| 5 | P | Polygamous 
| 6 | S | Never Married 
| 7 | T | Domestic partner 
| 8 | W | Widowed 

### 📊 Result Code

| Value | Description
| -- | -- 
| A | Addendum 
| C | Correction 
| F | Final 
| P | Preliminary 
| R | Resend 

### 📊 Evaluation Types

| Id | Value | Exam Description | Reader
| -- | -- | -- | --
| 1 | DR | Diabetic Retinopathy | Human
| 2 | Glaucoma | Glaucoma | Human
| 3 | HIV | HIV  | Human
| 4 | DRME | DR & ME with extended care plan support | Human
| 6 | DR_REFNOREF | DR only with refer/no refer | AI
| 7 | AMD | AMD Exam | Human 
| 8 | DR_AMD | DR and AMD combined | Human
| 9 | SP | Suspected Pathology | Human
| 12 | DR_AREDS_GLAUC | DR, AMD (AREDS) Glaucoma | AI
| 13 | AI_Eyenuk_O1 | DR, AMD Glaucoma - Eyenuk | AI


### 📊 Laterality

| Value | Description
| -- | --  
| OD | Right eye
| OS | Left eye
| OU | Both eyes


### 📊 OrderControlCode

<small>Specifies action to take for an OrderRequest</small>

| Value | Description
| -- | -- 
| **NW** | Create New Order
| **XO** | Change Order 
| **CA** | Cancel Order 
| **ResendResult** | Resend Results

Regardless of the control code, the same OrderRequest structure is used, however when using the CA code to cancel an order or the ResendResult code, you only need to populate the ClientGuid, Site LocalId and Order LocalId. 

Changing or Cancelling an order will not work if the target order is closed. 

Resending Results both regenerates the results and sends to all configured delivery endpoints (with the exception of the DFT (HL7) message)