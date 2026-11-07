---
title: "DeleteRule"
product: "Torch Log Service"
product_code: "tls"
source: "https://docs.byteplus.com/en/docs/tls/api-deleterule"
---

Call the DeleteRule interface to delete the collection configuration.

<span id="usage-notes"></span>
## Usage notes

The call frequency limit for this interface is 20 times/s, exceeding the frequency limit will result in an ExceedQPSLimit error.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">After deleting the collection configuration, it cannot be recovered, please proceed with caution.</div>


* <div data-tips="true" data-tips-type="tip">After the collection configuration is deleted, the corresponding machine group no longer collects and reports log data according to the specified collection rules, but the collected data will not be deleted before it expires.</div>



<span id="request-syntax"></span>
## Request syntax


* Request Method：**DELETE**

* Request URL：**https://tls\-{Region}.bytepluses.com/DeleteRule**


<span id="request-parameters"></span>
## Request parameters

The table below only lists the request parameters specific to this interface and some common parameters. For more information, please see [Common parameters](https://docs.byteplus.com/en/docs/tls/common-parameters).

<span id="body"></span>
### Body


|Name |Type |Required |Example |Description |
|---|---|---|---|---|
|RuleId |String |True |`fa******` |The ID of the collection configuration. |


<span id="responses"></span>
## Responses

There are no unique return parameters for this interface. For more information, please refer to the [Response message](https://docs.byteplus.com/en/docs/tls/response-message).

<span id="sample-request"></span>
## Sample Request

```json
DELETE https://tls-{Region}.bytepluses.com/DeleteRule HTTP/1.1 Content-Type: application/json
{
    "RuleId": "faf*******"
}
```


<span id="sample-response"></span>
## Sample Response

```json
HTTP/1.1 200 OK Content-Type: application/json; charset=utf-8
```


<span id="error-code"></span>
## Error code

The following table lists the error codes related to the interface and business logic. For common error codes, please refer to the [Common error codes](https://docs.byteplus.com/en/docs/tls/common-error-codes).


|HTTP status code |Error code |Error message |Description |
|---|---|---|---|
|400 |InvalidArgument |Invalid argument key %s, value %s, please check argument |The parameter is invalid. |
|404 |RuleNotExist |Rule %s does not exist |The collection configuration does not exist. |
|500 |InternalServerError |We encountered an unexpected server error, please try again later. |Internal server error. |


&nbsp;
