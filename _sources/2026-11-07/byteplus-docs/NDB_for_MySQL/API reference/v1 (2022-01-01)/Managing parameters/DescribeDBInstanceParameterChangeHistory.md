---
title: "DescribeDBInstanceParameterChangeHistory"
product: "NDB for mysql"
product_code: "NDB_for_MySQL"
source: "https://docs.byteplus.com/en/docs/NDB_for_MySQL/DescribeDBInstanceParameterChangeHistory"
---

Call the DescribeDBInstanceParameterChangeHistory interface to query the parameter modification history of an instance.

<span id=".6K-35rGC57G75Z6L"></span>
## Request type

Synchronous request.

<span id=".6LCD6K-V"></span>
## Debug

[去调试](https://api.byteplus.com/api-explorer/debug?action=DescribeDBInstanceParameterChangeHistory&serviceCode=vedbm&version=2022-01-01&groupName=)


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters


|**Name** |**Type** |**Required** |**Example** |**Description** |
|---|---|---|---|---|
|InstanceId |String |Yes |vedbm\-gzwdsf9b\*\*\*\* |Instance ID. |
|ParameterName |String |No |auto_increment_increment |Parameter name. |
|StartTime |String |No |2020\-03\-01T00:00:00Z |Start time. Format: yyyy\-MM\-ddTHH:mm:ssZ (UTC time). |
|EndTime |String |No |2020\-03\-01T00:00:00Z |The end time of the query. Format: yyyy\-MM\-ddTHH:mm:ssZ (UTC time). |
|PageSize |Integer |Yes |10 |Number of records per page. The value range is 1 to 1,000, with a default of 10. |
|PageNumber |Integer |Yes |1 |The page number, which must be greater than or equal to 1 and not exceed the maximum value of an Integer. The default is 1. |


<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameter


|**Name** |**Type** |**Example** |**Description** |
|---|---|---|---|
|Total |Integer |1 |The total number of returned results. |
|ParameterChangeHistory |Array of [ParameterChangeHistoryObject](https://docs.byteplus.com/en/docs/265/69775#parameterchangehistoryobject) |Refer to the return example.<br><br> |A list of parameter modification records. |


<span id="parameterchangehistoryobject"></span>
### ParameterChangeHistoryObject


|**Name** |**Type** |**Example** |**Description** |
|---|---|---|---|
|ParameterName |String |auto_increment_increment |Parameter name. |
|NewParameterValue |String |2 |The parameter value after modification. |
|OldParameterValue |String |1 |The parameter value before modification. |
|Status |String |Applied<br><br> |Parameter state. Value:<br><br><br>* `Applied`: Effective.<br><br>* `Syncing`: Modifying and not yet effective. |
|ModifyTime |String |2020\-03\-01T00:00:00Z |Parameter modification time. Format: `yyyy-MM-ddTHH:mmZ` (UTC time). |


<span id=".56S65L6L"></span>
## Example

<span id=".6K-35rGC56S65L6L"></span>
### Request example

```JSON
POST /?Action=DescribeDBInstanceParameterChangeHistory&Version=2022-01-01 HTTP/1.1
Content-Type: application/json
Host:vedbm.cn-beijing.byteplusapi.com.cn
X-Date: 20220101T101010Z
Authorization: HMAC-SHA256 Credential=AKLTN2I0MmFiNzMxNWE5NDgzMzk4MmVjMTVkODlkZTZ****/20220101/cn-beijing/vedbm/request,SignedHeaders=x-date, Signature=71d31fc7bcf990142851c9833c5656391486cda0ae2e0b8ada733b7c645****
{
    "InstanceId": "vedbm-bs2wxpl****",
    "PageSize": 10,
    "PageNumber": 1
}
```


<span id=".6L-U5Zue56S65L6L"></span>
### Response example

```JSON
{
    "ResponseMetadata": {
        "RequestId": "202502251610142B01003E8DC8410F1AF8-8fd580",
        "Action": "DescribeDBInstanceParameterChangeHistory",
        "Version": "2022-01-01",
        "Service": "vedbm",
        "Region": "cn-beijing"
    },
    "Result": {
        "ParameterChangeHistory": [
            {
                "ModifyTime": "2025-02-25T07:46:06Z",
                "NewParameterValue": "4",
                "OldParameterValue": "5",
                "ParameterName": "auto_increment_increment",
                "Status": "Applied"
            },
            {
                "ModifyTime": "2025-02-25T07:16:06Z",
                "NewParameterValue": "3",
                "OldParameterValue": "1",
                "ParameterName": "auto_increment_offset",
                "Status": "Applied"
            }
        ],
        "Total": 2
    }
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error code

For details, refer to [Error codes](https://docs.byteplus.com/en/docs/NDB_for_MySQL/Error_codes).
