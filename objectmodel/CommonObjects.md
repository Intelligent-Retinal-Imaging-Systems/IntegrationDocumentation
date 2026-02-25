---
title: Shared Models
parent: Object Models
nav_order: 3
---


## Common Shared Components

### Name

Common structure used for storing names

| Property | Type | Description
| -- | -- | --
| First | string | Persons first (given) name
| Last | string | Persons last (family) name

### Address 

Common structure used for storing addresses

| Property | Type | Description
| -- | -- | --
| Street1 | string | Line one of street address
| Street2 | string | Line two of street address
| City | string | City portion of address
| State | string (2) | State abbreviation of address
| PostalCode | string | Zip / Postal code

### PersonGender 

Common structure used for storing gender designations

| Property | Type | Description | Options
| -- | -- | -- | --
| Context | options | Gender association | [GenderContext](./OptionEnums#-gendercontext) options 
| Gender | options | The gender for specified context | [Gender](./OptionEnums#-gender) options
  


### RequestProvider

The RequestProvider structure allows you to specify various Providers associated with the exam. If the provider has previously been submitted and was done so with NPI, you only need to include the NPI value in the submission

| Property | Type | Description
| -- | -- | --
| NPI | string (10) | Providers National Identifier 
| Taxonomy | string | Optionally specify Taxonomy relevant to the action 
| Name | string | First, Last name
| Email | string | Optionally specify an email address 
| Degrees | string | Optionally supply degrees 
| Associations | string | Optionally supply associations 


### CPT

A procedure code can be submitted in the order and echoed back in results

| Property | Type | Description
| -- | -- | -- 
| Code | string | Procedure Code as defined by CMS
| Description | string | Description as defined by CMS

