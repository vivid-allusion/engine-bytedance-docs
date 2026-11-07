---
title: "DescribeRecoverableTime"
product: "NDB for mysql"
product_code: "NDB_for_MySQL"
source: "https://docs.byteplus.com/en/docs/NDB_for_MySQL/DescribeRecoverableTime"
---

Call the DescribeRecoverableTime to query the recoverable time range for instance backups.

<span id=".6K-35rGC57G75Z6L"></span>
## Request type

Synchronous request.

<span id=".6LCD6K-V"></span>
## Debug

[去调试](https://api.byteplus.com/api-explorer/debug?action=DescribeRecoverableTime&serviceCode=vedbm&version=2022-01-01&groupName=)


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters


|**Name** |**Type** |**Required** |**Example** |**Description** |
|---|---|---|---|---|
|InstanceId |String |Yes |vedbm\-gzwdsf9b\*\*\*\* |Instance ID.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">You can call the <a href="https://docs.byteplus.com/en/docs/NDB_for_MySQL/DescribeDBInstances">DescribeDBInstances</a> API to query the Instance ID.</div><br> |


<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameter


|**Name** |**Type** |**Example** |**Description** |
|---|---|---|---|
|RecoverableTimeInfo |Array of [RecoverableTimeInfo](https://docs.byteplus.com/en/docs/265/57390#recoverabletimeinfo) |Refer to the return example. |The recoverable time range of the instance. An empty value indicates that the instance is currently not restorable. |


<span id="recoverabletimeinfo"></span>
### RecoverableTimeInfo


|**Name** |**Type** |**Example** |**Description** |
|---|---|---|---|
|EarliestRecoverableTime |String |2023\-07\-14T03:47:31Z |The earliest restorable time of the instance, in the format yyyy\-MM\-ddTHH:mm:ssZ (UTC time). An empty value indicates that the instance cannot be restored. |
|LatestRecoverableTime |String |2023\-07\-14T03:47:31Z |The latest time to which the instance can be restored, in yyyy\-MM\-ddTHH:mm:ssZ format (UTC). An empty value indicates that the instance cannot currently be restored. |


<span id=".56S65L6L"></span>
## Example

<span id=".6K-35rGC56S65L6L"></span>
### Request example

```JSON
POST /?Action=DescribeRecoverableTime&Version=2022-01-01 HTTP/1.1
Content-Type: application/json
Host:vedbm.cn-beijing.byteplusapi.com.cn
X-Date: 20220101T101010Z
Authorization: HMAC-SHA256 Credential=AKLTN2I0MmFiNzMxNWE5NDgzMzk4MmVjMTVkODlkZTZ****/20220101/cn-beijing/vedbm/request,SignedHeaders=x-date, Signature=71d31fc7bcf990142851c9833c5656391486cda0ae2e0b8ada733b7c645****
{
    "InstanceId": "vedbm-gzwdsf9b****"
}
```


<span id=".6L-U5Zue56S65L6L"></span>
### Response example

```JSON
{
    "ResponseMetadata": {
        "RequestId": "20230719152754EFE6CEA0AC4725D6FDA6",
        "Action": "DescribeRecoverableTime",
        "Version": "2022-01-01",
        "Service": "vedbm",
        "Region": "cn-beijing"
    },
    "Result": {
        "RecoverableTimeInfo": [
            {
                "EarliestRecoverableTime": "2023-07-14T03:47:31Z",
                "LatestRecoverableTime": "2023-07-19T07:21:09Z"
            }
        ]
    }
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error code

For details, refer to [Error codes](https://docs.byteplus.com/en/docs/NDB_for_MySQL/Error_codes).
