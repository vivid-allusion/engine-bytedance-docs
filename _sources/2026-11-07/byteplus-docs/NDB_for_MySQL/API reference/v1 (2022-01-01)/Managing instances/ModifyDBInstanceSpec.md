---
title: "ModifyDBInstanceSpec"
product: "NDB for mysql"
product_code: "NDB_for_MySQL"
source: "https://docs.byteplus.com/en/docs/NDB_for_MySQL/ModifyDBInstanceSpec"
---

Call the ModifyDBInstanceSpec to modify the node configuration of the instance.

<span id=".6K-35rGC57G75Z6L"></span>
## Request type

Asynchronous request.

<span id=".5rOo5oSP5LqL6aG5"></span>
## Precautions

The ModifyDBInstanceSpec interface has been upgraded to version 2024\-01\-01. Version 2022\-01\-01 will no longer be maintained. Please use version 2024\-01\-01. For details, please refer to [ModifyDBInstanceSpec](https://docs.byteplus.com/en/docs/NDB_for_MySQL/ModifyDBInstanceSpec_v2).

<span id=".6LCD6K-V"></span>
## Debug

[去调试](https://api.byteplus.com/api-explorer/debug?action=ModifyDBInstanceSpec&serviceCode=vedbm&version=2022-01-01&groupName=)


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters


|**Name** |**Type** |**Required** |**Example** |**Description** |
|---|---|---|---|---|
|InstanceId |String |Yes |vedbm\-h441603c68aaa\*\*\*\* |Instance ID.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">You can call the <a href="https://docs.byteplus.com/en/docs/NDB_for_MySQL/DescribeDBInstances">DescribeDBInstances</a> API to query the Instance ID.</div><br> |
|NodeSpec |String |Yes |vedb.mysql.x4.large |Node specification code.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">For details about instance node specifications, refer to <a href="https://docs.byteplus.com/en/docs/NDB_for_MySQL/Product_specifications">Product specification</a>.</div><br> |
|NodeNumber |Integer |Yes |6 |The number of nodes for the instance, with a value ranging from 2 to 16. |
|PrePaidStorageInGB |Integer |No |60 |* If the storage billing type is pay\-as\-you\-go, you do not need to select storage capacity. The storage capacity will automatically scale up and down as the amount of data increases or decreases, and will be billed on an hourly basis based on actual usage.<br><br>* If the storage billing type is yearly or monthly subscription, you need to enter the changed storage space size in steps of 10 GiB, with an increment of 10 GiB.<br><br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">The storage space range varies by node specification. For details, refer to <a href="https://docs.byteplus.com/en/docs/NDB_for_MySQL/Product_specifications">Product specification</a>.</div><br> |
|ScheduleType |String |No |Immediate |Execution method. Possible values:<br><br><br>* `Immediate`: Execute now (default).<br><br>* `MaintainTime`: Execute during the maintenance window. |


<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameter


|**Name** |**Type** |**Example** |**Description** |
|---|---|---|---|
|InstanceId |String |vedbm\-h441603c68aaa\*\*\*\* |Instance ID. |
|OrderId |String |Order707643373078888\*\*\*\* |Order ID. |


<span id=".56S65L6L"></span>
## Example

<span id=".6K-35rGC56S65L6L"></span>
### Request example

```JSON
POST /?Action=ModifyDBInstanceSpec&Version=2022-01-01 HTTP/1.1
Content-Type: application/json
Host: vedbm.cn-beijing.byteplusapi.com.cn
X-Date: 20220101T101010Z
Authorization: HMAC-SHA256 Credential=AKLTN2I0MmFiNzMxNWE5NDgzMzk4MmVjMTVkODlkZTZ****/20220101/cn-beijing/vedbm/request,SignedHeaders=x-date, Signature=71d31fc7bcf990142851c9833c5656391486cda0ae2e0b8ada733b7c645****
{
        "InstanceId": "vedbm-gzwdsf9b****",
        "NodeSpec": "vedb.mysql.x4.large",
        "NodeNumber": 2
}
```


<span id=".6L-U5Zue56S65L6L"></span>
### Response example

```JSON
{
    "ResponseMetadata": {
        "RequestId": "202307191557433BA18653C86F63A04B1B",
        "Action": "ModifyDBInstanceSpec",
        "Version": "2022-01-01",
        "Service": "vedbm",
        "Region": "cn-beijing"
    },
    "Result": {
        "InstanceId": "vedbm-gzwdsf9b****",
        "OrderId": "Order725743560891294****"
    }
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error code

For details, refer to [Error codes](https://docs.byteplus.com/en/docs/NDB_for_MySQL/Error_codes).
