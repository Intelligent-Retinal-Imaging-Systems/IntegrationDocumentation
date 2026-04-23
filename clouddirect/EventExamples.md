---
title: Order Processing Events
parent: Examples
nav_order: 5
---

# Service Bus Event Examples

### ![alt text](/assets/example.ico) Example 1

Order Created 

```json
{
    "TransactionId": "CCB9F08D-29AA-446F-96F0-3018B20803E8",
    "Timestamp": "2022-01-02T17:42:18.6936779+00:00",
    "IrisOrderId": 1224035,
    "OrderLocalId": "a52b6bed-5b77-4e42-ad7c-203bc6d2ea16",
    "PatientLocalId": "35165564",
    "Success": true,
    "ErrorMessage": null,
    "ResultObjectType": "OrderCreationReceipt",
    "Version": "2.3.1"
}
```
### ![alt text](/assets/example.ico) Example 2

Order Cancelled 

```json
{
    "TransactionId": "CCB9F08D-29AA-446F-96F0-3018B20803E8",
    "Timestamp": "2022-01-02T17:42:18.6936779+00:00",
    "IrisOrderId": 1224035,
    "OrderLocalId": "a52b6bed-5b77-4e42-ad7c-203bc6d2ea16",
    "PatientLocalId": "35165564",
    "Success": true,
    "ErrorMessage": null,
    "ResultObjectType": "OrderCancelled",
    "Version": "2.3.1"
}
```
---

### ![alt text](/assets/example.ico) Example 3

Image Added

```json 
{
    "TransactionId": "DB816B37-07EC-43D0-9848-70BEC36F4024",
    "Timestamp": "2022-01-02T17:42:18.6936779+00:00",
    "ImageLocalId": "52737144-4ed2-42f8-8801-af9da52fcb28",
    "IrisImageId": 3677459,
    "IrisOrderId": 1225564,
    "OrderLocalId": "c448bd5c-d70a-44f7-ab2e-7396c39813db",
    "PatientLocalId": "c0eaed83-6812-ef11-9f8a-000d3a1f613d",
    "Success": true,
    "ErrorMessage": null,
    "ResultObjectType": "ImageReceipt",
    "Version": "2.3.1"
}
```