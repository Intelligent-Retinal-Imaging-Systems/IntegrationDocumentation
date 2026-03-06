---
title: Cancel Order
parent: Examples
nav_order: 3
---

# Sample Cancel OrderRequest Message
##### JSON encoded OrderRequest.

> Cancelling an order uses the same OrderRequest object used on submission with a different OrderControlCode (CA). 

Timing is crucial when cancelling orders.  In some cases, your cancellation request will be entirely ignored.  

*If the order is **not** cancelled before grading, you will be billed for the transaction.*

The Order LocalId is the only value used to determine the order you are attempting to cancel.  If this value does not resolve to a live order in the system, the request is ignored.


```json
{
  "$schema": "https://cdn.retinalscreenings.com/hosts/iris/schemas/order-submission.schema.2.3.1.json",
  "Version": "2.3.1", 	
  "OrderControlCode": "CA",             
  "ClientGuid": "63E3C9EF-66AC-4154-B0C2-494515EB99A7",    
  "Order": {
    "LocalId": "ORD1234"
  }
}
```