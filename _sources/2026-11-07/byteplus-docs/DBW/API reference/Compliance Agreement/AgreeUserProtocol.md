---
title: "AgreeUserProtocol"
product: "Database Workshop"
product_code: "DBW"
source: "https://docs.byteplus.com/en/docs/DBW/AgreeUserProtocol"
---

Call the AgreeUserProtocol API to agree to the Database Workshop DBW user agreement.

<span id="Jl12TKGg"></span>
## Request type

Synchronize request.

<span id="bSHi12Gh"></span>
## Request parameters

Null

<span id="bMoMCWwA"></span>
## Response parameters

Null

<span id="Eqnm7Pzs"></span>
## Request example

```Plain Text
POST /?Action=AgreeUserProtocol&Version=2018-01-01 HTTP/1.1
Content-Type: application/json
Host: dbw.cn-beijing.byteplusapi.com.cn
Authorization: HMAC-SHA256 Credential=AKLTN2I0MmFiNzMxNWE5NDgzMzk4MmVjMTVkODlkZTZ****/20211202/cn-beijing/dbw/request,SignedHeaders=x-date, Signature=71d31fc7bcf990142851c9833c5656391486cda0ae2e0b8ada733b7c645****
```


<span id="XAVnij5T"></span>
## Response example

```Plain Text
{
    "ResponseMetadata": {
        "RequestId": "20251230152702E7EB9CC48D8022C55502-654fa0",
        "Action": "AgreeUserProtocol",
        "Version": "2018-01-01",
        "Service": "dbw",
        "Region": "cn-beijing"
    },
    "Result": {}
}
```


<span id="NPZvLroG"></span>
## Error code

For details, refer to [Error codes](https://docs.byteplus.com/en/docs/DBW/error-codes).
