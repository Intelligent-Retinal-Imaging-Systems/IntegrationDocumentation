
## Order and Image Events

Because Service Bus based integrations are asynchronous, IRIS posts events on an events queue to keep you apprised of important operations as they occur.  

✨ See [Sample Events](/integration/CloudDirectEventSample/) for examples of event messages.

##### ![alt text](properties.png) Base properties
<small>All events contain this common set of base properties</small>

| Property | Data type | Description
| -- | -- | --
| TransactionId | GUID | Uniquely identifies the message
| Timestamp | datetimeoffset | Datetime message was posted to the queue
| Success | bool | If true the operation succeeded
| ErrorMessage | string | If Success is false, this could contain details of the error
| ResultObjectType | string | Identifies the type of event object this is to establish additional properties 
| Version | string | Message version

## ResultObjectType Types

Messages sent on the events queue can be of varying types all based on the common properties detailed above. 

### OrderCreationReceipt

Events with the ResultObjectType of OrderCreationReceipt contain details of an  order you recently posted to the service bus queue. 

*As with all ResultObjectTypes check the Success and ErrorMessage properties for the status of the operation*

##### ![alt text](properties.png) Additional Properties

| Property | Data type | Description
| -- | -- | --
| IrisOrderId | int | Id of order as created and known by IRIS
| OrderLocalId | string | Id of order as specified by you on submission
| PatientLocalId | string | Id of the patient as specified by you on submission


### ![alt text](structure.png) ImageReceipt

Events with the ResultObjectType of ImageReceipt contain details of an image submission operation.  

*As with all ResultObjectTypes check the Success and ErrorMessage properties for the status of the operation*

##### ![alt text](properties.png) Additional Properties

| Property | Data type | Description
| -- | -- | --
| IrisOrderId | int | Id of order as created and known by IRIS
| OrderLocalId | string | Id of order as specified by you on submission
| PatientLocalId | string | Id of the patient as specified by you on submission
| ImageLocalId | string | Id of the image as specified by you on submission
| IrisImageId | int | Id of image as created and known by IRIS 

### ![alt text](structure.png) ReadyForGradingEvent

Events with the ResultObjectType of ReadyForGradingEvent contain details of an order moving into the grading queue

This event fires when order image requirements have been satisfied for an order.

##### ![alt text](properties.png) Additional Properties

| Property | Data type | Description
| -- | -- | --
| IrisOrderId | int | Id of order as created and known by IRIS
| OrderLocalId | string | Id of order as specified by you on submission
| PatientLocalId | string | Id of the patient as specified by you on submission


### ![alt text](structure.png) GradingReceipt

Events with the ResultObjectType of GradingReceipt contain details of a grading submission.  

This event fires when a grading has been submitted for an order

*As with all ResultObjectTypes check the Success and ErrorMessage properties for the status of the operation*

##### ![alt text](properties.png) Additional Properties

| Property | Data type | Description
| -- | -- | --
| IrisOrderId | int | Id of order as created and known by IRIS
| OrderLocalId | string | Id of order as specified by you on submission
| PatientLocalId | string | Id of the patient as specified by you on submission

### ![alt text](structure.png) OrderGradedEvent

Events with the ResultObjectType of OrderGradedEvent contain details of an order that has been graded

This event will post when an order is graded.  This differs from the GradingReceipt in that the grading has been applied establishing the order as graded.

##### ![alt text](properties.png) Additional Properties

| Property | Data type | Description
| -- | -- | --
| IrisOrderId | int | Id of order as created and known by IRIS
| OrderLocalId | string | Id of order as specified by you on submission
| PatientLocalId | string | Id of the patient as specified by you on submission

### ![alt text](structure.png) ResultsDeliveryReceipt

Events with the ResultObjectType of ResultsDeliveryReceipt contain details of results delivered to any endpoint other than the standard Cloud Direct result (e.g.: You won't get a message to tell you the message you just received was received).  This message is provided for customers who have configured multiple destinations for results such as fax results to PCP.  


##### ![alt text](properties.png) Additional Properties

| Property | Data type | Description
| -- | -- | --
| IrisOrderId | int | Id of order as created and known by IRIS
| OrderLocalId | string | Id of order as specified by you on submission
| TimeDelivered | DateTimeOffset | date/time when delivery was executed
| DeliveryType | string/options | type of delivery from list below
| Endpoint | string | Endpoint relative to the delivery type 
| TransmissionStatus | Transmission Status [Values](#transmission-status-values)| Status on delivery types that occur asynchronously (i.e.: Fax)
