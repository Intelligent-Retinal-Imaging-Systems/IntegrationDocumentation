---
title: Option Enumerations
parent: Cloud Direct
nav_order: 4
---

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

| Value | Description
| -- | --
| U | Unspecified 
| M | Male 
| F | Female 
| N | Non binary 
| O | Other 
| TM | Transgender Male 
| TF | Transgender Female 
| ND | Non disclosed 
| EQ | Exploring or Questioning
| NL | Not listed
| X | Not exclusively Male or Female

## Marital Status  

Items in this list are based on the HL7 standard here: http://terminology.hl7.org/CodeSystem/v3-MaritalStatus 

| Value | Description
| -- | --
| A | Annulled 
| D | Divorced 
| C | Common Law 
| I | Interlocutory 
| L | Legally Separated 
| M | Married 
| P | Polygamous 
| S | Never Married 
| T | Domestic partner 
| W | Widowed 

## Result Code 
Identifies the context in which a result was sent.

| Value | Description
| -- | --
| A | Addendum 
| C | Correction 
| F | Final 
| P | Preliminary 
| R | Resend 
