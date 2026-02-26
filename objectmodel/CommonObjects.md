---
title: Shared Models
parent: Object Models
nav_order: 4
---


## Common Shared Components
The following components are shared within the IRIS Object Model.

<a id="address"></a>
### ![alt text](/assets/structure.ico) Address (Object) 

| Property | Type | Description
| -- | -- | --
| Street1 | string | Line one of street address
| Street2 | string | Line two of street address
| City | string | City portion of address
| State | string (2) | State abbreviation of address
| PostalCode | string | Zip / Postal code


<a id="cpt"></a>
### ![alt text](/assets/structure.ico) CPT (Object)

A procedure code can be submitted in the order and echoed back in results

| Property | Type | Description
| -- | -- | -- 
| Code | string | Procedure Code as defined by CMS
| Description | string | Description as defined by CMS


<a id="name"></a>
### ![alt text](/assets/structure.ico) Name (Object)

| Property | Type | Description
| -- | -- | --
| First | string | Persons first (given) name
| Last | string | Persons last (family) name

<a id="persongender"></a>
### ![alt text](/assets/structure.ico) PersonGender (Object) 

Common structure used for storing gender designations

| Property | Type | Description | Options
| -- | -- | -- | --
| Context | options | Gender association | [GenderContext](/objectmodel/OptionEnums#-gendercontext) options 
| Gender | options | The gender for specified context | [Gender](/objectmodel/OptionEnums#-gender) options

<a id="requestprovider"></a>
### ![alt text](/assets/structure.ico) Provider (Object)

The RequestProvider structure allows you to specify various Providers associated with the exam. If the provider has previously been submitted and was done so with NPI, you only need to include the NPI value in the submission

| Property | Type | Description
| -- | -- | --
| NPI | string (10) | Providers National Identifier 
| Taxonomy | string | Optionally specify Taxonomy relevant to the action 
| Name | string | First, Last name
| Email | string | Optionally specify an email address 
| Degrees | string | Optionally supply degrees 
| Associations | string | Optionally supply associations 

