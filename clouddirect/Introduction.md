<!-- ---
title: Cloud Direct 
parent: Order Processing Integration
nav_order: 2
has_toc: false
--- -->


# IRIS Cloud Direct Integrations
{: .no_toc }
 
This document provides details for integrations to the IRIS Platform using cloud provider resources directly accessing the IRIS 3.x platform.

<details markdown="block">
  <summary>
    Table of contents
  </summary>
  {: .text-delta }
- TOC
{:toc}
</details>


<style>
   table tr { text-align: left }
   table tr:nth-child(even) { background-color: #fafafa; }
   table tr:nth-child(odd)  { background-color: #ffffff; }
</style>


----

## Introduction

As an integration option, IRIS provides the ability to submit orders and receive results directly communicating with the cloud service of your preference (Azure, AWS or Google Cloud). 

*If you do not wish to use your own cloud service subscription, IRIS can also provide this functionality in the IRIS Azure subscription, referred to in this document as **IRIS Azure Cloud**.* 

In all cases, communication is accommodated using the cloud vendors APIs, SDKs or libraries. For many languages, IRIS provides native libraries,referred to as the IRIS Public libraries, to abstract the Cloud operations and to provide serialization and deserialization from the data models. 


## Integration Administrator

IRIS provides access to certain integration tools and configurations though the Integration Administrator role. The role is assigned to you either by IRIS support or an existing Organization Administrator for your organization. The term Integration Administrator will be referred to throughout this document thus mentioned here for clarity. 


## Developers

IRIS provides libraries for most of the popular programming languages on our [Developer Resources](/integration/DeveloperResources/) page.

## Order Submission

Orders are submitted to IRIS using an Azure Service Bus Queue

The process involves hydrating and sending a JSON encoded OrderRequest object to the orders queue

*If you are planning to use an IRIS Public library, the act of serializing and sending the data is reduced to a single step within the library.*

C# Example

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

### What you need to get started

Before you can submit an order using Cloud Direct services, the are several pieces of data you will need from IRIS:
1. Service Bus Connection String
2. Your Organization Identifier referred to as **ClientGuid**
3. Site identifier(s)

### Orders Service Bus Connection String 

Because orders are only submitted on a service bus that lives within the IRIS Azure subscription, you must obtain the connection string from IRIS. This connection string has write-only privileges. To obtain the connection string contact Contact <a href="mailto:support@irishelp.zendesk.com">IRIS Support</a>. 

### Organization Identifier

Created by IRIS during provisioning, this is a GUID value passed into all order submissions, uniquely identifying your organization.

### Site Identifiers

Depending on your specific needs you will have one to many sites within the IRIS system assigned to your organization.  Orders have a direct relationship to the site therefore an identifier for the site must be included in your submission.

If you operate within a brick and mortar type model, you typically will want to have one site in the IRIS system per physical location your cameras reside.  If you operate more in a mobile workflow, you typically have a single site.  In the multisite mode, the state where the exam is performed is assumed to be the state configured on the site record within IRIS.   If you operate in a single site mode, you must provide the state where the exam occurs in the order object.  

For single site workflows, IRIS will provide you with the identifier to supply for the Site.  This because it's not an identifier you established yourself.

For multisite workflows, you will provide IRIS with your identifiers for each site as they are added.  This can be done programmatically through this interface or through the Administrator application. If added from this interface you must include all the required properties for adding a new site in the Site structure.  This is described in full detail in the [Site structure](/integration/objectmodel/RequestObject).


### Requests, Events and Results
Regardless of which transport is chosen for your integration, the process of sending an order starts with setting the contents of the Order Request object. 
* [Request Object definition](/integration/objectmodel/RequestObject)
* [Request Object (JSON) example](/integration/clouddirect/RequestExample)

Events related to orders you have submitted are generated with availability dependent on the integration method chosen.
* [Event Objects definition](/integration/objectmodel/ResultObject)
* [Event Object (JSON) examples](/integration/clouddirect/EventExamples)


Results are returned in an Order Result object.
* [Result Object definition](/integration/objectmodel/ResultObject)
* [Result Object (JSON) example](/integration/clouddirect/ResultExample)


