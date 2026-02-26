---
title: Cloud Direct 
parent: Order Processing Integration
nav_order: 2
has_toc: false
---

# IRIS Cloud Direct Integrations

This document describes how to integrate with the IRIS 3.x Platform by interacting directly with cloud provider resources.

---

## Introduction

As an integration option, IRIS supports direct interaction through the cloud provider of your choice (Azure, AWS, or Google Cloud).

*If you do not wish to use your own cloud subscription, IRIS can host all required resources within the **IRIS Azure Cloud**.*

All communication occurs using each cloud vendor’s APIs, SDKs, or libraries. For many languages, IRIS provides native **IRIS Public Libraries**, which offer Cloud operations as well as serialization utilities for IRIS JSON request/response objects.

---

## Cloud Resources

While terminology differs between cloud providers, IRIS uses two primary resource types:

- **Message brokers** – for submitting and receiving messages  
- **Storage services** – for handling files such as images

IRIS is hosted in Azure, where these correspond to **Service Bus** (message broker) and **Storage Accounts**.

Message brokers handle **JSON message objects**, while storage handles **file assets** (e.g., images).

---

## Resource Provisioning

Cloud resource provisioning generally follows this pattern:

1. A unique cloud resource is created within the respective subscription.
2. The resource owner provides **write-only** credentials for endpoints the integrator sends to.
3. The resource owner provides **read-only** credentials for endpoints the integrator consumes from.

Example:  
If all cloud resources are provisioned by IRIS in the IRIS Azure subscription, IRIS will supply:
- **Write-only** access to order submission queues  
- **Read-only** access to event and result delivery queues  

*The most common pattern is IRIS providing an Azure Service Bus queue for order submission.*

---

## Keys / Connection Strings

The party that does **not** own the cloud resource is provided credentials defined by the cloud vendor.  
In Azure, these are delivered as **connection strings**.

---

## Integration Administrator

IRIS grants access to integration tools and configuration through the **Integration Administrator** role.  
This role is assigned by IRIS Support or by your organization’s Administrator. Anyone holding this role gains access to Cloud Direct configuration and credential management.

---

## Developers

IRIS provides language‑specific client libraries on the [Developers](/integration/DeveloperResources/) page.  
These libraries provide a strongly typed version of the IRIS Object model as well as simplifying Cloud operations.

---

## General Workflow

1. An order is submitted, including patient data.
2. Images are uploaded and associated to the order.
3. The order enters the grading queue.
4. The grading process completes.
5. Result artifacts are generated.
6. All configured recipients receive their artifacts.

### Corresponding Cloud Interactions
- An order is created by constructing an **OrderRequest object** and sending it to the message broker.
- A series of **event messages** are published as the order moves through each processing stage.
- Images are uploaded and event messages are published for each image.
- When grading completes, artifacts are delivered to the configured endpoints.

---

## Order Submission

To submit an order, you must construct an **OrderRequest JSON object** and send it to your configured cloud endpoint—typically an **Azure Service Bus Queue**.

This involves:
- Creating a JSON-encoded **OrderRequest object**
- Sending it as the message body to the *orders* queue

*If you are using an IRIS Public Library, serialization and message sending are abstracted into a single method call.*

##### <small>C# Example</small>

```csharp
async Task Test()
{
    string connectionString = "Endpoint=sb://iris-organization…"; // abbreviated connection string 
    string queueName= "orders"; 
    string orderRequestMessage = "[JSON Encoded OrderRequest object]"
    await await var client = new ServiceBusClient(connectionString);
    ServiceBusSender sender = client.CreateSender(queueName);
    ServiceBusMessage message = new ServiceBusMessage(orderRequestMessage);
    await sender.SendMessageAsync(message); // Fire and forget
}
```

> ## Getting started
>
> Before you can submit an order using Cloud Direct services, the are several pieces of data you will need from IRIS:
> 1. Service Bus Connection String
> 2. Your Organization's unique identifier referred to as **ClientGuid**
> 3. Site identifier(s)
> ##### Orders - Connection String 
> Because orders are only submitted on a service bus that lives within the IRIS Azure subscription, you must obtain the connection string from IRIS. This connection string has write-only privileges.  Access to integration credentials are provided in the IRIS Administrator application, however the process starts through request to the <a href="mailto:support@irishelp.zendesk.com">IRIS support team</a>. 
> ##### Organization Identifier
> Created by IRIS during provisioning, this is a GUID value passed into all order submissions, uniquely identifying your organization.  If this Identifier is not properly placed in the message, you will not receive any event related to the order submission failure. 
> ##### Site Identifiers
> Depending on your specific needs you will have one to many sites within the IRIS system assigned to your organization.  Orders have a direct relationship to the site therefore an identifier for the site must be included in your submission.
>
> If you operate within one or more medical facilities, you will want to configure one site in the IRIS system per physical location your cameras reside.  If you operate in a mobile workflow, such as home health care, you typically configure a single site.  In the multisite mode, the state where the exam is performed is assumed to be the state configured on the site record within IRIS.   If you operate in a single site mode, you must provide the state where the exam occurs in the OrderRequest object.  
>
> For single site workflows, IRIS will provide you with the identifier to supply for the Site.  This because it's not an identifier you established yourself.
>
> For multisite workflows, you will provide IRIS with your identifiers for each site as they are added.  This can be done programmatically through this interface or through the Administrator application. If added from this interface you must include all the required properties for adding a new site in the [site](/objectmodel/RequestObject#site) structure.  

##### Next -> [IRIS Object Models](/objectmodel/Objectmodels)
 

