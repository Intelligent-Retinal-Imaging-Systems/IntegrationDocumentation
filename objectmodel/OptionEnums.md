---
title: Enumerations
parent: Object Models
nav_order: 5
---

{: .no_toc }

# Enumerations (Option Lists)

The following tables provide acceptable values for option properties.  Always use the values found in the Code column when building your objects. 

### 📊 GenderContext

<small>Establishes whether the Gender specified is the patients **Birth** or **Identity** Gender</small>

{% assign rows = site.data.GenderContextLookup | sort: "Id" %}

| Id | Gender Context |
|---|---|---|
{% for r in rows -%}
| {{ r.Id }} | {{ r.GenderContext }} |
{% endfor %}

 
### 📊 Race 

<small>You may use any of the HL7 Ethnicity codes listed on <a href="https://terminology.hl7.org/6.1.0/CodeSystem-v3-Race.html">Hl7 Coding: Race</a></small>

{% assign rows = site.data.RaceLookup | sort: "Id" %}

| Id | Race | HL7 Code |
|---|---|---|
{% for r in rows -%}
| {{ r.Id }} | {{ r.Race }} | {{ r.HL7Code | escape }} |
{% endfor %}


### 📊 Ethnicity 

<small>You may use any of the HL7 Ethnicity codes listed on <a href="http://terminology.hl7.org/CodeSystem/v3-Ethnicity">Hl7 Coding: Ethnicity</a></small>

{% assign rows = site.data.EthnicityLookup | sort: "Id" %}

| Id | Ethnicity | HL7 Code |
|---|---|---|---|
{% for r in rows -%}
| {{ r.Id }} | {{ r.Ethnicity }} | {{ r.HL7Code | escape }} |
{% endfor %}

### 📊 Language 

<small>You may use any of the HL7 Language codes listed on <a href="https://www.hl7.org/fhir/valueset-languages.html">Hl7 Coding: Languages</a></small>

{% assign rows = site.data.LanguageLookup | sort: "Id" %}

| Id | Language | Language Code |
|---|---|---|
{% for r in rows -%}
| {{ r.Id }} | {{ r.Language }} | {{ r.LanguageCode | escape }} |
{% endfor %}

### 📊 Gender  

<small>Listing of accepted options for Gender.</small>

{% assign rows = site.data.GenderLookup | sort: "Id" %}

| Id | Gender Name | HL7 Code |
|---|---|---|
{% for r in rows -%}
| {{ r.Id }} | {{ r.GenderName }} | {{ r.HL7GenderCode | escape }} |
{% endfor %}

### 📊 Marital Status  

<small>Items in this list are based on the HL7 standard here: <a href=http://terminology.hl7.org/CodeSystem/v3-MaritalStatus>HL7 Coding: Marital Status</a></small>

{% assign rows = site.data.MaritalStatusLookup | sort: "Id" %}

| Id | Marital Status | Description | HL7 Code |
|---|---|---|---|
{% for r in rows -%}
| {{ r.Id }} | {{ r.MaritalStatus }} | {{ r.Description | escape }} | {{ r.HL7Code | escape }} |
{% endfor %}

### 📊 Result Code

| Code | Description
| -- | -- 
| A | Addendum 
| C | Correction 
| F | Final 
| P | Preliminary 
| R | Resend 

### 📊 Evaluation Types

<small>Types of evaluations (exams) IRIS performs. You can only use evaluation types that you have subscribed to.</small>

{% assign rows = site.data.EvaluationLookup | sort: "Id" %}

| Id | Name | Display name | Description |
|---|---|---|---|
{% for r in rows -%}
| {{ r.Id }} | {{ r.Name }} | {{ r.AppDisplayName | escape }} | {{ r.Description | escape }} |
{% endfor %}

### 📊 ImageContext

{% assign rows = site.data.ImageContextTypeLookup | sort: "Id" %}

| Id | Name | Description |
|---|---|---|
{% for r in rows -%}
| {{ r.Id }} | {{ r.Name }} | {{ r.Description | escape }} |
{% endfor %}

### 📊 Laterality

| Code | Description
| -- | --  
| OD | Right eye
| OS | Left eye
| OU | Both eyes


### 📊 OrderControlCode

<small>Specifies action to take for an OrderRequest submission</small>

| Code | Description
| -- | -- 
| NW | Create New Order
| XO | Change Order 
| CA | Cancel Order 
| ResendResult | Resend Results

* Regardless of the control code, the same OrderRequest structure is used, however when using the CA code to cancel an order or the **ResendResult** code, you only need to populate the **ClientGuid**, Site.**LocalId** and Order.**LocalId**. 
* Changing or Cancelling an order will not work if the target order is closed. 
* Resending Results both regenerates the results and sends to all configured delivery endpoints (with the exception of the DFT (HL7) message)