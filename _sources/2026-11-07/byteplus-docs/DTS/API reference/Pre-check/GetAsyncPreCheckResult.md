---
title: "GetAsyncPreCheckResult"
product: "Database Transmission Service"
product_code: "DTS"
source: "https://docs.byteplus.com/en/docs/DTS/getasyncprecheckresult"
---

Call the GetAsyncPreCheckResult API to view pre\-check results.

<span id=".6K-35rGC57G75Z6L"></span>
## Request type

Asynchronous request.

<span id=".5rOo5oSP5LqL6aG5"></span>
## Precautions

When calling the GetAsyncPreCheckResult API, `Version` must be set to `2018-01-01`.

<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters


|**Parameter** |**Type** |**Is it required?**  |**Sample** |**Description** |
|---|---|---|---|---|
|ID |String |Yes |174673313234787\*\*\*\* |Pre\-check ID.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">You can call the <a href="https://docs.byteplus.com/en/docs/DTS/precheckasync">PreCheckAsync</a> interface to query the pre\-check Task ID.</div><br> |
|Cancel |Boolean |No | |Cancel retry pre\-check |


<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameter


|**Parameter** |**Type** |**Sample** |**Description** |
|---|---|---|---|
|Pass |Boolean |true |Indicates whether the pre\-check is passed. the values are as follows:<br><br><br>* `true`: Indicates that the pre\-check is passed.<br><br>* `false`: Indicates that the pre\-check is failed. |
|PreChecks |Array of [Check](https://docs.byteplus.com/en/docs/57/47575#check) |```json```<br>```{```<br>```    "Desc": "运行环境检测",```<br>```    "Details": "",```<br>```    "Level": "Warning",```<br>```    "Name": "运行环境检测",```<br>```    "Pass": true```<br>```}```<br> |A detailed list of pre\-check items. |
|Progress |Long |100 |Pre\-check progress. |
|Status |String |Completed |Pre\-check status, the values are as follows:<br><br><br>* `Init`: Indicates that pre\-check is in initialization.<br><br>* `Running`: Indicates that pre\-check is in pre\-check.<br><br>* `Completed`: Indicates that pre\-check is completed.<br><br>* `Failed`: Indicates that pre\-check failed.<br><br>* `Stopped`: Indicates that pre\-check is terminated. |


<span id="check"></span>
### Check


|**Parameter** |**Type** |**Sample** |**Description** |
|---|---|---|---|
|Pass |Boolean |true |Whether the check item is passed. The values are as follows:<br><br><br>* `true`: Indicates that the pre\-check item is passed.<br><br>* `false`: Indicates that the pre\-check item failed. |
|Level |String |Error |Level of the pre\-check item when the pre\-check item fails. The values are as follows:<br><br><br>* `Error`: Indicates that if the pre\-check item fails, the pre\-check will not pass.Pre\-check.<br><br>* `Warning`: If it fails, it will not affect whether the entire pre\-check passes. |
|Name |String |Environment detection. |The name of the check item. |
|Desc |String |Environment detection. |Check content. |
|Details |String |Failed to connect to or expand the wildcard. Check the connectivity or retry. |The detailed information of the check item result. |


<span id=".56S65L6L"></span>
## Example

<span id=".6K-35rGC56S65L6L"></span>
## Request example

```JSON
POST /?Action=GetAsyncPreCheckResult&Version=2018-01-01 HTTP/1.1
Content-Type: application/json
Host: dts.cn-beijing.byteplusapi.com.cn
X-Date: 20221001T101010Z
Authorization: HMAC-SHA256 Credential=AKLTN2I0MmFiNzMxNWE5NDgzMzk4MmVjMTVkODlkZTZ****/20221001/cn-beijing/dts/request,SignedHeaders=x-date, Signature=71d31fc7bcf990142851c9833c5656391486cda0ae2e0b8ada733b7c645****
{
    "ID": "174673313234787****"
}
```


<span id=".6L-U5Zue56S65L6L"></span>
## Response example

```JSON
{
    "ResponseMetadata": {
        "RequestId": "202401152002228A5FC3FD4AC18045A3FB",
        "Action": "GetAsyncPreCheckResult",
        "Version": "2018-01-01",
        "Service": "dts",
        "Region": "cn-beijing"
    },
    "Result": {
        "Pass": false,
        "PreChecks": [
            {
                "Desc": "运行环境检测",
                "Details": "",
                "Level": "Warning",
                "Name": "运行环境检测",
                "Pass": true
            },
            {
                "Desc": "数据库和结构通配符规则检查",
                "Details": "连接或展开通配符失败，请检查连通性或重试",
                "Level": "Error",
                "Name": "数据库连接和结构通配符规则检查",
                "Pass": false
            }
        ],
        "Progress": 100,
        "Status": "Completed"
    }
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error code

For more details, see [Error code](https://docs.byteplus.com/en/docs/DTS/error_codes).
