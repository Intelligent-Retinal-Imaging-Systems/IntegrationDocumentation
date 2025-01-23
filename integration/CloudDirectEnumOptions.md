---
title: Option Enumerations
parent: Cloud Direct
nav_order: 1
---

{: .no_toc }

# Option Enumerations

The following tables provide acceptable values for option properties.

## GenderContext

Specifies the context in which the Gender specification applies. 

| Value | Description | Numeric value
| -- | -- | --
| Unknown |  Not set | 0
| IdentityGender | Gender individual identifies as | 1
| BirthGender | Gender individual was designated at birth | 2

## Race 

You may use any of the HL7 Ethnicity codes listed on <a href="https://terminology.hl7.org/6.1.0/CodeSystem-v3-Race.html">Hl7 Coding: Race</a>

### Abbreviated list

| Value | Description
| -- | --
| 1002-5 | American Indian or Alaska Native 
| 2028-9 | Asian 
| 2054-5 | Black or African American 
| 2076-8 | Native Hawaiian or Other Pacific Islander 
| 2131-1 | Other Race 
| 2106-3 | White 


## Ethnicity 

You may use any of the HL7 Ethnicity codes listed on <a href="http://terminology.hl7.org/CodeSystem/v3-Ethnicity">Hl7 Coding: Ethnicity</a>

### Abbreviated list

| Value | Description
| -- | --
| 2137-8 | Spaniard 
| 2148-5 | Mexican
| 2155-0 | Central American 
| 2180-8 | Puerto Rican 
| 2182-4 | Cuban 
| 2149-3 | Mexican American 

## Language 

You may use any of the HL7 Language codes listed on <a href="https://www.hl7.org/fhir/valueset-languages.html">Hl7 Coding: Languages</a>

### Abbreviated list

| Value | Description
| -- | --
| en | English 
| en-US | US English 
| fr | French 
| es | Spanish
| it | Italian 
| pt | Portuguese 
| zh | Chinese 

## Gender  

| Value | Description | Numeric value
| -- | -- | --
| U | Unspecified | 0
| M | Male | 1
| F | Female | 2
| N | Non binary | 3
| O | Other | 4
| TM | Transgender Male | 5
| TF | Transgender Female | 6
| ND | Non disclosed | 7
| EQ | Exploring or Questioning | 8
| NL | Not listed | 9
| X | Not exclusively Male or Female | 10

## Marital Status  

Items in this list are based on the HL7 standard here: http://terminology.hl7.org/CodeSystem/v3-MaritalStatus 

| Value | Description | Numeric value
| -- | -- | --
| A | Annulled | 0
| D | Divorced | 1
| I | Interlocutory | 2
| L | Legally Separated | 3 
| M | Married | 4
| P | Polygamous | 5
| S | Never Married | 6
| T | Domestic partner | 7
| W | Widowed | 8

## Result Code

Identifies the context in which a result was sent.

| Value | Description
| -- | -- 
| A | Addendum 
| C | Correction 
| F | Final 
| P | Preliminary 
| R | Resend 

## Evaluation Types

Enumeration of IRIS Evaluation types

| Value | Description | Numeric Value
| -- | -- | --
| DR | Diabetic Retinopathy Exam | 1
| Glaucoma | Glaucoma Exam | 2
| HIV | HIV Exam | 3
| AMD | AMD Exam | 7 
| DR_AMD | DR and AMD combined exam | 8
