---
title: "UpdateSystemEvents - Modifies system event statuses"
product: "Elastic Compute Service"
product_code: "ecs"
source: "https://docs.byteplus.com/en/docs/ecs/UpdateSystemEvents"
---

Call the UpdateSystemEvents operation to modify system event status.

<span id=".6K-35rGC6K-05piO"></span>
## Request description


* Only for `"SystemMaintenance.Redeploy"` event authorization, the `OperatedStartAt` and `OperatedEndAt` parameters can be used to change the maintenance time window.

* `OperatedStartAt` and `OperatedEndAt` parameters only support passing in the following time periods:

   * Event occurrence time to event occurrence time + 12h

   * Event occurrence time + 12h to 24h

   * Event occurrence time + 24h to 36h

   * Event occurrence time + 36h to 48h

   * Event occurrence time + 48h to 60h

   * Event occurrence time + 60h to 72h


<span id=".6LCD6K-V"></span>
## Debugging

[去调试](https://api.byteplus.com/api-explorer/?action=UpdateSystemEvents&groupName=%E7%9B%91%E6%8E%A7&serviceCode=ecs&version=2020-04-01)


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters

Only the request parameters specific to this operation and some common parameters are listed below. For more information, refer to [Common parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).



**Action** <span data-label="purple">string</span> <span data-api-tag="require|erVSrC">必选</span> `Sample value: UpdateSystemEvents`

The action that you want to perform. Value: UpdateSystemEvents.



**Version** <span data-label="purple">string</span> <span data-api-tag="require|tlkbDn">必选</span> `Sample value: 2020-04-01`

The version of the API. Valid value: 2020\-04\-01.



**EventIds.N** <span data-label="purple">string[]</span> <span data-api-tag="require|1I0F4c">必选</span> `Sample value: EventIds.1=e-3ti9101aju3vj0****&EventIds.2=e-3tiegs1y963vj0****`

The event ID. A maximum of 100 event IDs are supported. You can use the [event notification](https://docs.byteplus.com/en/docs/ecs/Receiving-event-notifications) feature or call the [DescribeSystemEvents](https://docs.byteplus.com/en/docs/ecs/DescribeSystemEvents) operation to query and obtain the event ID.


* Argument \- N: specifies the serial number of the event ID.

* Separate multiple event IDs with `&`.



**OperatedEndAt** <span data-label="purple">string</span> `Optional` `Sample value: 2022-09-02T15:11:46+08:00`

The end time of the event O&M time window. Default value: request receipt time + 72h. Format: RCF3339.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Currently, you can change the O&M time only for a <code>"SystemMaintenance.Redeploy"</code> event. During event authorization, the parameter is required, and the parameter value cannot be earlier than the time specified for OperatedStartAt.</div>




**OperatedStartAt** <span data-label="purple">string</span> `Optional` `Sample value: 2022-08-30T15:11:46+08:00`

The start time of the event O&M time window. Default value: request receipt time + 60h. Format: RCF3339.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">You can change the O&M time only for a <code>"SystemMaintenance.Redeploy"</code> event. During event authorization, the parameter is required, and the parameter value cannot be later than the time specified for OperatedEndAt.</div>




**Status** <span data-label="purple">string</span> <span data-api-tag="require|XDlZWU">必选</span> `Sample value: Executing`

The system event status. Valid value:


* Executing: in progress



**UpdatedAt** <span data-label="purple">string</span> `Optional` `Sample value: 2021-06-28T18:29:38+08:00`

The event update time. Default value: the request receipt time. Format: RFC3339.



&nbsp;

<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters

Only the response parameters specific to this operation are listed below. For more information, refer to [Response structure](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response).

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">The following <a href="https://docs.byteplus.com/en/docs/ecs/UpdateSystemEvents#.6ZSZ6K-v56CB">error codes</a> for the operation are returned only when invalid values are specified for request parameters. If valid values are specified for the request parameters, no error code is displayed, and a status code of <code>200</code> is returned. However, this does not mean that the operation on all system events is successful. To view the operation result on one system event, see the information in the following response parameters.</div>




**OperationDetails** <span data-label="purple">object[]</span> `Sample value: --`

The operation details.


**Error** <span data-label="purple">object</span> `Sample value: --`

The error information for the failure to modify an event status.


**Code** <span data-label="purple">string</span> `Sample value: InvalidSubscription.NotFound`

The error code for the failure of a specific individual request during batch operations. Value:


* InvalidSystemEvent.NotFound: The specified system event does not exist.

* InvalidSystemEventStatus.TypeMismatch: The event status does not match the event type.

* InvalidSystemEventStatus.PreStatusMismatch: The event status does not match the prior event status.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Each <code>Code</code> corresponds to a <code>Message</code> in sequence.</div>




**Message** <span data-label="purple">string</span> `Sample value: The specified subscription does not exist.`

The error information for the failure of a specific individual request during batch operations. Value:


* `The specified system event does not exist.`: The specified system event does not exist.

* `The specified system event type does not match this status.`: Status and event type do not match.

* `The specified system event does not match pre-status.`: The event status does not match the event prior status.




**EventId** <span data-label="purple">string</span> `Sample value: e-3tiegs1y963vj0******`

The system event ID.




&nbsp;

<span id=".6K-35rGC56S65L6L"></span>
## Sample request

```text
GET /?Action=UpdateSystemEvents&Version=2020-04-01&EventIds.1=t-3ti9101aju3vj0******&Status=Executing HTTP/1.1
Host: ecs.cn-beijing.byteplusapi.com.cn
Region: cn-beijing
ServiceName: ecs
```


<span id=".6L-U5Zue56S65L6L"></span>
## Sample response

```json
{
    "ResponseMetadata": {
        "RequestId": "202106111445100102252431000052****",
        "Action": "UpdateSystemEvents",
        "Version": "2020-04-01",
        "Service": "ecs",
        "Region": "cn-beijing"
    },
    "Result": {
        "OperationDetails": [
            {
                "EventId": "e-ybq95rphkoawmb******",
                "Error": {
                    "Code": "InvalidSystemEvent.NotFound",
                    "Message": "The specified system event does not exist."
                }
            }
        ]
    }
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error codes

The table below lists the business\-related error codes of the operation. For more information, refer to [Common error codes](https://docs.byteplus.com/en/docs/ecs/Public-error-codes).


|Status code |Error code |Error message |Description |
|---|---|---|---|
|400 |InvalidOperatedEndAt.Malformed |The specified OperatedEndAt is malformed. |The specified value of OperatedEndAt is invalid. |
|400 |InvalidOperatedStartAt.Malformed |The specified OperatedStartAt is malformed. |The specified value of OperatedStartAt is invalid. |
|400 |InvalidStatus.Malformed |The specified Status is malformed. |The specified value of Status is invalid. |
|400 |InvalidSystemEventStatus.PreStatusMismatch |The specified system event does not match pre status. |The specified system event does not match the event status. |
|400 |InvalidSystemEventStatus.TypeMismatch |The specified system event type does not match this status. |The specified system event type does not match the event status. |
|400 |InvalidUpdatedAt.Malformed |The specified UpdatedAt is malformed. |The specified value of UpdatedAt is invalid. |
|400 |LimitExceeded.MaximumEventIds |You've reached the limit on the number of EventIds that you can set. |The specified number of event IDs exceeds the limit. |
|400 |MissingParameter.EventIds |The required parameter EventIds is not supplied. |The event ID is not provided. |
|400 |MissingParameter.Status |The required parameter Status is not supplied. |The parameter Status cannot be left empty. |
|404 |InvalidActionOrVersion |Could not find operation %s for version %s. |The operation does not exist. |
|500 |InternalError |An internal error has occurred. |An internal error occurred. Try again. If multiple attempts fail, submit a ticket. |
