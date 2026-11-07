---
title: "ResetCheckPoint"
product: "Torch Log Service"
product_code: "tls"
source: "https://docs.byteplus.com/en/docs/tls/api-resetcheckpoint"
---

Call the ResetCheckPoint interface to reset all consumption checkpoints for the specified consumer group.

<span id="usage-notes"></span>
## Usage notes


* This interface is used to reset the consumption checkpoints of the consumer group. The difference from the ModifyCheckPoint interface is that ModifyCheckPoint only supports resetting the consumption checkpoints recorded by the consumer group on the specified log shard, while ResetCheckPoint will reset all consumption checkpoints of the specified consumer group.

* The call frequency limit is 20 times/s, and exceeding the frequency limit will report an error ExceedQPSLimit.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Before resetting the consumption checkpoints, the corresponding consumption process should be shut down, otherwise, the consumption checkpoints reset will fail.</div>


<span id="request-syntax"></span>
## Request syntax


* Request Method：**PUT**

* Request URL：**https://tls\-{Region}.bytepluses.com/ResetCheckPoint**


<span id="request-parameters"></span>
## Request parameters

The table below only lists the request parameters specific to this interface and some common parameters. For more information, please see [Common parameters](https://docs.byteplus.com/en/docs/tls/common-parameters).

<span id="body"></span>
### Body


|Name |Type |Required |Example |Description |
|---|---|---|---|---|
|ProjectID |String |True |`c7******` |The project ID subscribed by the consumer group. |
|ConsumerGroupName |String |True |`my-consumer-group` |The name of the consumer group to which the checkpoint to be reset belongs. |
|Position |String |True |`begin` |The new consumption checkpoint, which indicates consumption of data from a specified location. It supports specifying as:<br><br><br>* begin: Start consuming from the earliest data in the topic.<br><br>* end: Skip all historical data and start consuming directly from the most recently written data in the topic.<br><br>* Unixtime 10\-digit second\-level timestamp. Start consuming from a specified point in the past, which is based on the data retention duration of the topic. When resetting the consumption point at a specified time, it does not support specifying a historical moment that exceeds the data retention duration or a future moment. |


<span id="responses"></span>
## Responses

There are no unique return parameters for this interface. For more information, please refer to the [Response message](https://docs.byteplus.com/en/docs/tls/response-message).

<span id="sample-request"></span>
## Sample Request

```json
PUT https://tls-{Region}.bytepluses.com/ResetCheckPoint HTTP/1.1
Content-Type: application/json
{
    "ProjectID": "c7************",
    "ConsumerGroupName": "my-consumer-group",
    "Position": "begin"
}
```


<span id="sample-response"></span>
## Sample Response

```json
HTTP/1.1 200 OK
Content-Type: application/json; charset=utf-8
```


<span id="error-code"></span>
## Error code

The following table lists the error codes related to the interface and business logic. For common error codes, please refer to the [Common error codes](https://docs.byteplus.com/en/docs/tls/common-error-codes).


|HTTP status code |Error code |Error message |Description |
|---|---|---|---|
|400 |InvalidArgument |Invalid argument key %s, value %s, please check argument. |The parameter is invalid. |
|500 |InternalServerError |We encountered an unexpected server error, please try again later. |Internal server error. |


&nbsp;
