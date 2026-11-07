---
title: "DeleteDBInstance"
product: "NDB for mysql"
product_code: "NDB_for_MySQL"
source: "https://docs.byteplus.com/en/docs/NDB_for_MySQL/DeleteDBInstance"
---

Call the DeleteDBInstance to delete a pay\-as\-you\-go instance.

<span id=".6K-35rGC57G75Z6L"></span>
## Request type

Asynchronous request.

<span id=".5rOo5oSP5LqL6aG5"></span>
## Precautions


* You can only delete instances in the **Running** or **Error** state. When calling the [DescribeDBInstanceDetail](https://docs.byteplus.com/en/docs/NDB_for_MySQL/DescribeDBInstanceDetail) API, the returned `InstanceStatus` must be `Running` or `Error`.

* You can only delete pay\-as\-you\-go instances by calling the DeleteDBInstance API. You can only unsubscribe from yearly/monthly subscription instances through the console. For detailed steps, refer to [Unsubscribe from yearly/monthly subscription instance](https://docs.byteplus.com/en/docs/NDB_for_MySQL/Deleting_or_unsubscribing_an_instance#.6YCA6K6i5YyF5bm05YyF5pyI5a6e5L6L).


<span id=".6LCD6K-V"></span>
## Debug

[去调试](https://api.byteplus.com/api-explorer/debug?action=DeleteDBInstance&serviceCode=vedbm&version=2022-01-01&groupName=)


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters


|**Name** |**Type** |**Required** |**Example** |**Description** |
|---|---|---|---|---|
|InstanceId |String |Yes |vedbm\-r3xq0zdl\*\*\*\* |Instance ID.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">You can call the <a href="https://docs.byteplus.com/en/docs/NDB_for_MySQL/DescribeDBInstances">DescribeDBInstances</a> API to query the Instance ID.</div><br> |
|DataKeepPolicy |String |否 |Last |The backup retention policy that is applied when the instance is deleted. The only supported value is `Last`, which means a final backup file is created and retained.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="default">If this parameter is not specified, no backups are retained.</div><br><br><br>* <div data-tips="true" data-tips-type="default">When deleting the instance, even if this parameter is set to <code>All</code>, the system converts it to <code>Last</code>.</div><br> |


<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameter

null

<span id=".56S65L6L"></span>
## Example

<span id=".6K-35rGC56S65L6L"></span>
### Request example

```JSON
POST /?Action=DeleteDBInstance&Version=2022-01-01 HTTP/1.1
Content-Type: application/json
Host:vedbm.cn-beijing.byteplusapi.com.cn
X-Date: 20220101T101010Z
Authorization: HMAC-SHA256 Credential=AKLTN2I0MmFiNzMxNWE5NDgzMzk4MmVjMTVkODlkZTZ****/20220101/cn-beijing/vedbm/request,SignedHeaders=x-date, Signature=71d31fc7bcf990142851c9833c5656391486cda0ae2e0b8ada733b7c645****
{
    "InstanceId": "vedbm-r3xq0zdl****",
    "DataKeepPolicy": "Last"
}
```


<span id=".6L-U5Zue56S65L6L"></span>
### Response example

```JSON
{
    "ResponseMetadata": {
        "RequestId": "202204102303580102111952291A4E84AB",
        "Action": "DeleteDBInstance",
        "Version": "2022-01-01",
        "Service": "vedbm",
        "Region": "cn-beijing"
    },
    "Result": null
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error code

For details, refer to [Error codes](https://docs.byteplus.com/en/docs/NDB_for_MySQL/Error_codes).
