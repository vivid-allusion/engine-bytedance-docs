---
title: "DeleteHostGroup"
product: "Torch Log Service"
product_code: "tls"
source: "https://docs.byteplus.com/en/docs/tls/api-deletehostgroup"
---

Call the DeleteHostGroup interface to delete the host group.

<span id="usage-notes"></span>
## Usage notes

The call frequency limit is 20 times/s, and exceeding the frequency limit will report an error ExceedQPSLimit.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">After deleting a host group, its corresponding hosts will stop collecting and reporting log data.</div>


* <div data-tips="true" data-tips-type="tip">If the collection configuration is associated with multiple host groups, after deleting one of them, the other host groups will continue to collect according to the specified rules.</div>



<span id="request-syntax"></span>
## Request syntax


* Request Method: **DELETE**

* Request URL: **https://tls\-{Region}.bytepluses.com/DeleteHostGroup**


<span id="request-parameters"></span>
## Request parameters

The table below only lists the request parameters specific to this interface and some common parameters. For more information, please see [Common parameters](https://docs.byteplus.com/en/docs/tls/common-parameters).

<span id="body"></span>
### Body


|Name |Type |Required |Example |Description |
|---|---|---|---|---|
|HostGroupId |String |True |`c7********` |The ID of the host group. |


<span id="responses"></span>
## Responses

There are no unique return parameters for this interface. For more information, please refer to the [Response message](https://docs.byteplus.com/en/docs/tls/response-message).

<span id="sample-request"></span>
## Sample Request

```json
DELETE https://tls-{Region}.bytepluses.com/DeleteHostGroup HTTP/1.1
Content-Type: application/json
{
    "HostGroupId": "c7**********"
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
|400 |InvalidArgument |Invalid argument key %s, value %s, please check argument. |Parameter is invalid. |
|404 |HostGroupNotExist |HostGroup %s does not exist |The host group does not exist |
|500 |InternalServerError |We encountered an unexpected server error, please try again later. |Internal server error. |


&nbsp;
