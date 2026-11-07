---
title: "DescribeDBInstanceParameters"
product: "NDB for mysql"
product_code: "NDB_for_MySQL"
source: "https://docs.byteplus.com/en/docs/NDB_for_MySQL/DescribeDBInstanceParameters"
---

Call the DescribeDBInstanceParameters to query the instance parameter list.

<span id=".6K-35rGC57G75Z6L"></span>
## Request type

Synchronous request.

<span id=".6LCD6K-V"></span>
## Debug

[去调试](https://api.byteplus.com/api-explorer/debug?action=DescribeDBInstanceParameters&serviceCode=vedbm&version=2022-01-01&groupName=)


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters


|**Name** |**Type** |**Required** |**Example** |**Description** |
|---|---|---|---|---|
|InstanceId |String |Yes |vedbm\-gzwdsf9b\*\*\*\* |Instance ID.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">You can call the <a href="https://docs.byteplus.com/en/docs/NDB_for_MySQL/DescribeDBInstances">DescribeDBInstances</a> API to query the Instance ID.</div><br> |


<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameter


|**Name** |**Type** |**Example** |**Description** |
|---|---|---|---|
|InstanceId |String |vedbm\-gzwdsf9b\*\*\*\* |Instance ID. |
|Parameters |Array of [ParameterObject](https://docs.byteplus.com/en/docs/265/57394#parameterobject) |Refer to the return example. |Parameter list of the instance. |


<span id="parameterobject"></span>
### ParameterObject


|**Name** |**Type** |**Example** |**Description** |
|---|---|---|---|
|ParameterName |String |auto_increment_increment |Parameter name. |
|ParameterValue |String |1 |Parameter running value. |
|ParameterDisplayValue |String |1 |The displayed value for the parameter. If the target parameter value is set as an expression, this field shows the actual running value after the expression is calculated. |
|CheckingCode |String |[1\-65535] |Parameter value range. |
|NeedRestart |Boolean |false |Does modifying this parameter require restarting the instance? |
|ParameterDefaultValue |String |1 |Parameter default value. |
|ParameterDescription |String |Auto\-increment columns are incremented by this |The parameter description. |
|Modifiable |Boolean |true |Whether the parameter can be modified. |
|Status |String |Applied |The state of the parameter. The possible values are:<br><br><br>* `Applied`: Effective.<br><br>* `Syncing`: Modifying and not yet effective. |
|DataType |String |INT |The data type of the parameter. Value:<br><br><br>* `INT`: integer.<br><br>* `FLOAT`: float.<br><br>* `STRING`: string. |


<span id=".56S65L6L"></span>
## Example

<span id=".6K-35rGC56S65L6L"></span>
### Request example

```JSON
POST /?Action=DescribeDBInstanceParameters&Version=2022-01-01 HTTP/1.1
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
        "RequestId": "2025021216380940A3519600F9A7798F0E-9be055",
        "Action": "DescribeDBInstanceParameters",
        "Version": "2022-01-01",
        "Service": "vedbm",
        "Region": "cn-beijing"
    },
    "Result": {
        "InstanceId": "vedbm-gzwdsf9b****",
        "Parameters": [
            {
                "CheckingCode": "[1-65535]",
                "DataType": "INT",
                "Modifiable": true,
                "NeedRestart": false,
                "ParameterDefaultValue": "1",
                "ParameterDescription": "Auto-increment columns are incremented by this",
                "ParameterDisplayValue": "4",
                "ParameterName": "auto_increment_increment",
                "ParameterValue": "4",
                "Status": "Applied"
            },
            {
                "CheckingCode": "[1-65535]",
                "DataType": "INT",
                "Modifiable": true,
                "NeedRestart": false,
                "ParameterDefaultValue": "1",
                "ParameterDescription": "Offset added to Auto-increment columns. Used when auto-increment-increment != 1",
                "ParameterDisplayValue": "3",
                "ParameterName": "auto_increment_offset",
                "ParameterValue": "3",
                "Status": "Applied"
            }
        ]
    }
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error code

For details, refer to [Error codes](https://docs.byteplus.com/en/docs/NDB_for_MySQL/Error_codes).
