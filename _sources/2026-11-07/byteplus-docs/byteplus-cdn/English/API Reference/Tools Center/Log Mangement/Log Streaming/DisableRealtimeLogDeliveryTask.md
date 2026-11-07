---
title: "DisableRealtimeLogDeliveryTask"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/DisableRealtimeLogDeliveryTask_en-us"
---

Disables a log streaming task.

<span id="usage-limits"></span>
## Usage Limits

Throttling Limit: You can submit up to 20 API requests per second.

<span id="usage"></span>
## Usage


* Request Method: POST

* Request URL: https://cdn.byteplusapi.com/?Action=DisableRealtimeLogDeliveryTask&Version=2021\-03\-01


<span id="request-parameters"></span>
## Request Parameters

<span id="query-parameters"></span>
### Query Parameters


|Parameter |Data Type |Required |Description |
|---|---|---|---|
|Action |String |Yes |The action of this API operation. The action is: `DisableRealtimeLogDeliveryTask`. |
|Version |String |Yes |The version of this API operation. Current version: `2021-03-01`. |


<span id="request-body"></span>
### Request Body


|Parameter |Data Type |Required |Description |Value |
|---|---|---|---|---|
|TaskID |String |Yes |Indicates the ID of a task to be disabled. |`42de0332-b6e0-4fe1-9a5a-847bb7471def` |


<span id="response-parameters"></span>
## Response Parameters

<span id="samples"></span>
## Samples

<span id="sample-request"></span>
### Sample request

```json
POST https://cdn.byteplusapi.com/?Action=DisableRealtimeLogDeliveryTask&Version=2021-03-01
{
    "TaskID": "b23298e8-c262-4cb6-8138-2c311230b972"
}
```


&nbsp;
