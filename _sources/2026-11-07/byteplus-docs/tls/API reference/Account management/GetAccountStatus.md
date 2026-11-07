---
title: "GetAccountStatus"
product: "Torch Log Service"
product_code: "tls"
source: "https://docs.byteplus.com/en/docs/tls/GetAccountStatus"
---

This API is used to check whether TLS is enabled.

<span id=".6K-35rGC6K-05piO"></span>
## Request instructions


* Request method: GET

* Request URL: https://{tls\-endpoint}/GetAccountStatus


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters

This API does not have specific request or common parameters. For more information, see [Common Parameters](https://docs.byteplus.com/en/docs/tls/common-parameters).

<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters

The following table lists the response parameters unique to this API. For more information, see [Return Structure](https://docs.byteplus.com/en/docs/tls/response-message).


|**Parameters** |**Type** |**Example value** |**Description** |
|---|---|---|---|
|ArchVersion |String |`2.0` |TLS version:<br><br><br>* 2.0: New architecture<br><br>* 1.0: Legacy architecture |
|Status |String |`Activated` |Activated TLS:<br><br><br>* Activated: TLS is enabled<br><br>* NonActivated: TLS is not enabled |


<span id="FKdKzqU7"></span>
## Sample request

```JSON
GET https://{tls-endpoint}/GetAccountStatus HTTP/1.1
Content-Type: application/json
```


<span id="s5f2ssvH"></span>
## Sample response

```JSON
Content-Type: application/json; charset=utf-8
{
    "ArchVersion": "2.0",
    "Status": "Activated"
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error Code

For more error code details, see [Common Error Codes](https://docs.byteplus.com/en/docs/tls/common-error-codes).
