---
title: "DeleteHost"
product: "Torch Log Service"
product_code: "tls"
source: "https://docs.byteplus.com/en/docs/tls/api-deletehost"
---

Call the DeleteHost interface to delete the host with the IP specified by the host group.

<span id="usage-notes"></span>
## Usage notes

The call frequency limit for this interface is 20 times/s, and exceeding the frequency limit will result in an ExceedQPSLimit error.

<span id="request-syntax"></span>
## Request syntax


* Request Method: **DELETE**

* Request URL: **https://tls\-{Region}.bytepluses.com/DeleteHost**


<span id="request-parameters"></span>
## Request parameters

The table below only lists the request parameters specific to this interface and some common parameters. For more information, please see [Common parameters](https://docs.byteplus.com/en/docs/tls/common-parameters).

<span id="body"></span>
### Body


|Name |Type |Required |Example |Description |
|---|---|---|---|---|
|HostGroupId |String |True |`c7********` |The ID of the host group. |
|Ip |String |True |`1.1.1.1` |The IP address of the host. |


<span id="responses"></span>
## Responses

There are no unique return parameters for this interface. For more information, please refer to the [Response message](https://docs.byteplus.com/en/docs/tls/response-message).

<span id="sample-request"></span>
## Sample Request

```json
DELETE https://tls-{Region}.bytepluses.com/DeleteHost HTTP/1.1
Content-Type: application/json
{
    "HostGroupId": "c7e*******",
    "Ip": "1.1.1.1"
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
|404 |HostGroupNotExist |HostGroup %s does not exist |The host group does not exist. |
|500 |InternalServerError |We encountered an unexpected server error, please try again later. |Internal server error. |


&nbsp;
