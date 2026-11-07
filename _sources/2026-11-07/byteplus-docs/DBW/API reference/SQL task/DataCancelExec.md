---
title: "DataCancelExec"
product: "Database Workshop"
product_code: "DBW"
source: "https://docs.byteplus.com/en/docs/DBW/datacancelexec"
---

Call the DataCancelExec API to cancel SQL execution.

<span id=".6K-35rGC57G75Z6L"></span>
## Request type

Synchronize request.

<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters


|**Name** |**Type** |**Required?**  |**Sample** |**Description** |
|---|---|---|---|---|
|SessionId |String |Yes |MTU4MDg2NDA4MTAyNjM2NzQ4OC8xNTgwODY0MDgxMDUxNTM3\*\*\*\* |Session ID.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">You can call the <a href="https://docs.byteplus.com/en/docs/DBW/dataconnectinstance">DataConnectInstance</a> API to connect to an instance and obtain the session ID.</div><br> |


<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters

None

<span id=".6K-35rGC56S65L6L"></span>
## Request example

```json
POST /?Action=DataCancelExec&Version=2018-01-01 HTTP/1.1
Content-Type: application/json
Host: dbw.cn-beijing.byteplusapi.com.cn
Authorization: HMAC-SHA256 Credential=AKLTN2I0MmFiNzMxNWE5NDgzMzk4MmVjMTVkODlkZTZ****/20211202/cn-beijing/dbw/request,SignedHeaders=x-date, Signature=71d31fc7bcf990142851c9833c5656391486cda0ae2e0b8ada733b7c645****

{
      "SessionId": "MTU4MDg2NDA4MTAyNjM2NzQ4OC8xNTgwODY0MDgxMDUxNTM3****"
}
```


<span id=".6L-U5Zue56S65L6L"></span>
## Response example

```json
{
    "ResponseMetadata": {
        "RequestId": "202210141812360101742511840201D834",
        "Action": "DataCancelExec",
        "Version": "2018-01-01",
        "Service": "dbw",
        "Region": "cn-beijing"
    },
    "Result": {}
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error code

For details, refer to [Error codes](https://docs.byteplus.com/en/docs/DBW/error-codes).
