---
title: Shared Models
parent: Object Models
nav_order: 3
---


## Common Shared Structures

### Name structure

Common structure used for storing names

| Property | Type | Description
| -- | -- | --
| First | string | Persons first (given) name
| Last | string | Persons last (family) name

### Address structure 

Common structure used for storing addresses

| Property | Type | Description
| -- | -- | --
| Street1 | string | Line one of street address
| Street2 | string | Line two of street address
| City | string | City portion of address
| State | string (2) | State abbreviation of address
| PostalCode | string | Zip / Postal code

### PersonGender structure 

Common structure used for storing gender designations

| Property | Type | Description | Options
| -- | -- | -- | --
| Context | options | Gender association | [GenderContext](./OptionEnums#-gendercontext) options 
| Gender | options | The gender for specified context | [Gender](./OptionEnums#-gender) options
  




