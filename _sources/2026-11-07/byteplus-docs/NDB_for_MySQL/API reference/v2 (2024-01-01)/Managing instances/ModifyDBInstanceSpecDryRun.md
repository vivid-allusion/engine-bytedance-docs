---
title: "ModifyDBInstanceSpecDryRun"
product: "NDB for mysql"
product_code: "NDB_for_MySQL"
source: "https://docs.byteplus.com/en/docs/NDB_for_MySQL/ModifyDBInstanceSpecDryRun"
---

Call the ModifyDBInstanceSpecDryRun API to view the estimated impact of modifying the instance specification.

## Debug

[去调试](https://api.byteplus.com/api-explorer/debug?action=ModifyDBInstanceSpecDryRun&serviceCode=vedbm&version=2024-01-01&groupName=)

## Request parameters

|**Name** |**Type** |**Is it required?**  |**Example** |**Description** |
|---|---|---|---|---|
|InstanceId |String |Yes |vedbm\-ag4pnd3k\*\*\*\* |Instance ID. |
|NodeInfos |Array of [NodeInfoObject](https://docs.byteplus.com/en/docs/265/120431#nodeinfoobject) |Yes |See the request example |Specification and configuration of the instance node. |

### NodeInfoObject

|**Name** |**Type** |**Required** |**Example** |**Description** |
|---|---|---|---|---|
|NodeType |String |Yes |DBEngine |Node type. Value:<br><br>`DBEngine`: Primary node/Read\-only node. |
|NodeSpec |String |Yes |vedb.mysql.x4.large |The node specification code for the instance.<br><br>> **tip**<br><br><br>> For detailed information on instance node specifications, refer to [Product specifications](https://docs.byteplus.com/en/docs/NDB_for_MySQL/Product_specifications).<br> |
|NodeNumber |Integer |Yes |2 |Number of nodes.<br><br>When `NodeType` is set to `DBEngine` (Primary node/Read\-only node), the value of this parameter ranges from 2 to 16. |
|ZoneId |String |Yes |cn\-beijing\-a |Availability zone ID. |

## Response parameter

|**Name** |**Type** |**Example** |**Description** |
|---|---|---|---|
|InstanceId |String |vedbm\-ag4pnd3k\*\*\*\* |Instance ID. |
|Abilities |Array of String |["InplaceScale"] |The impact of the selected configuration change on the instance.<br><br><br>* If this parameter contains `InplaceScale`, the configuration change is expected to complete in a short time, and the Read/Write connection is usually not interrupted.<br><br>* If this parameter is empty, the configuration change will interrupt the Read/Write connection. Ensure that your service has a reconnection mechanism. |

## Example

### Request example

```JSON
POST /?Action=ModifyDBInstanceSpecDryRun&Version=2024-01-01 HTTP/1.1
Content-Type: application/json
Host: vedbm.cn-beijing.byteplusapi.com.cn
X-Date: 20220101T101010Z
Authorization: HMAC-SHA256 Credential=AKLTN2I0MmFiNzMxNWE5NDgzMzk4MmVjMTVkODlkZTZ****/20220101/cn-beijing/vedbm/request,SignedHeaders=x-date, Signature=71d31fc7bcf990142851c9833c5656391486cda0ae2e0b8ada733b7c645****
{
    "InstanceId": "vedbm-ag4pnd3k****",
    "NodeInfos": [
        {
            "ZoneId": "cn-beijing-a",
            "NodeSpec": "vedb.mysql.x4.large",
            "NodeType": "DBEngine",
            "NodeNumber": 2
        }
    ]
}
```

### Response example

```JSON
{
    "ResponseMetadata": {
        "RequestId": "20260827174056B096A62B8B56F54E782E-e87ded",
        "Action": "ModifyDBInstanceSpecDryRun",
        "Version": "2024-01-01",
        "Service": "vedbm",
        "Region": "cn-chongqing-sdv"
    },
    "Result": {
        "Abilities": [],
        "InstanceId": "vedbm-ag4pnd3k****"
    }
}
```

## Error code

For details, refer to [Error codes](https://docs.byteplus.com/en/docs/NDB_for_MySQL/Error_codes).
