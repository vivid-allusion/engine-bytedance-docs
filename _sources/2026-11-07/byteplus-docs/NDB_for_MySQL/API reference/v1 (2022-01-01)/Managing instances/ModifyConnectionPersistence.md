---
title: "ModifyConnectionPersistence"
product: "NDB for mysql"
product_code: "NDB_for_MySQL"
source: "https://docs.byteplus.com/en/docs/NDB_for_MySQL/ModifyConnectionPersistence"
---

Call the ModifyConnectionPersistence API to enable or disable connection persistence for the instance.

<span id=".6K-35rGC57G75Z6L"></span>
## Request type

Asynchronous request.

<span id=".6LCD6K-V"></span>
## Debug

[去调试](https://api.byteplus.com/api-explorer/debug?action=ModifyConnectionPersistence&serviceCode=vedbm&version=2022-01-01&groupName=)


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters


|**Name** |**Type** |**Required** |**Example** |**Description** |
|---|---|---|---|---|
|InstanceId |String |Yes |vedbm\-2pf2xk5v\*\*\*\* |Instance ID. |
|ConnectionPersistence |String |Yes |OFF |Sets the connection persistence state. For more information about the connection persistence feature, refer to [Connection persistent](https://docs.byteplus.com/en/docs/NDB_for_MySQL/Connection_persistence). Value range:<br><br><br>* `OFF`: Disable the connection persistence feature.<br><br>* `ON`: Enable the connection persistence feature. |


<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameter


|**Name** |**Type** |**Example** |**Description** |
|---|---|---|---|
|TaskId |String |202607101037450984EE1F455E57\*\*\*\*\-fd15ec |Task ID. |


<span id=".56S65L6L"></span>
## Example

<span id=".6K-35rGC56S65L6L"></span>
### Request example

```JSON
POST /?Action=ModifyConnectionPersistence&Version=2022-01-01 HTTP/1.1
Content-Type: application/json
Host: vedbm.cn-beijing.byteplusapi.com.cn
X-Date: 20220101T101010Z
Authorization: HMAC-SHA256 Credential=AKLTN2I0MmFiNzMxNWE5NDgzMzk4MmVjMTVkODlkZTZ****/20220101/cn-beijing/vedbm/request,SignedHeaders=x-date, Signature=71d31fc7bcf990142851c9833c5656391486cda0ae2e0b8ada733b7c645****
{
    "InstanceId": "vedbm-2pf2xk5v****",
    "ConnectionPersistence": "OFF"
}
```


<span id=".6L-U5Zue56S65L6L"></span>
### Response example

```JSON
{
    "ResponseMetadata": {
        "RequestId": "20260710103925FECBE294447732A5****-79f26d",
        "Action": "ModifyConnectionPersistence",
        "Version": "2022-01-01",
        "Service": "vedbm",
        "Region": "cn-beijing"
    },
    "Result": {
        "TaskId": "202607101037450984EE1F455E57****-fd15ec"
    }
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error code

For details, refer to [Error codes](https://docs.byteplus.com/en/docs/NDB_for_MySQL/Error_codes).
