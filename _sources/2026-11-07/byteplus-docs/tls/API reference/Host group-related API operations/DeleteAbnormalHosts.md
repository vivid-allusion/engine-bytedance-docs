---
title: "DeleteAbnormalHosts"
product: "Torch Log Service"
product_code: "tls"
source: "https://docs.byteplus.com/en/docs/tls/api-deleteabnormalhosts"
---

Call the DeleteAbnormalHosts interface to clean up all hosts with abnormal heartbeats in the host group at once.

<span id="usage-notes"></span>
## Usage notes

This interface is used for one\-click cleanup of abnormal hosts in the IP address type host group. After the abnormal host is cleaned up, if it recovers, it needs to be re\-added to the host group. Please modify the IP address list through ModifyHostGroup.

<span id="request-syntax"></span>
## Request syntax


* Request Method: **DELETE**

* Request URL: **https://tls\-{Region}.bytepluses.com/DeleteAbnormalHosts**


<span id="request-parameters"></span>
## Request parameters

The table below only lists the request parameters specific to this interface and some common parameters. For more information, please see [Common parameters](https://docs.byteplus.com/en/docs/tls/common-parameters).

<span id="body"></span>
### Body


|Name |Type |Required |Example |Description |
|---|---|---|---|---|
|HostGroupId |String |True |`30272ee8-36cc-49c2-812a-7881c0c6****` |The ID of the host group corresponding to the abnormal heartbeat host. |


<span id="responses"></span>
## Responses

The table below only lists the return parameters specific to this interface. For more information, please refer to the [Response message](https://docs.byteplus.com/en/docs/tls/response-message).

<span id="sample-request"></span>
## Sample Request

```json
DELETE https://tls-{Region}.bytepluses.com/DeleteAbnormalHosts HTTP/1.1
Content-Type: application/json
{
    "HostGroupId": "30272ee8-36cc-49c2-812a-7881c0c6****"
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
|500 |InternalServerError |We encountered an unexpected server error, please try again later. |Internal server error. |


&nbsp;
