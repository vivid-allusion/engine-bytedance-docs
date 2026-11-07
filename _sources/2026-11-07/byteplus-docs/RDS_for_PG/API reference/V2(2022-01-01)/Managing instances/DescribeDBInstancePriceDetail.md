---
title: "DescribeDBInstancePriceDetail"
product: "RDS for PostgreSQL"
product_code: "RDS_for_PG"
source: "https://docs.byteplus.com/en/docs/RDS_for_PG/describedbinstancepricedetail"
---

Call the DescribeDBInstancePriceDetail API to query instance price details.

<span id=".6K-35rGC57G75Z6L"></span>
## Request type

Synchronous request.

<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters


|**Parameter** |**Type** |**Required?**  |**Example** |**Description** |
|---|---|---|---|---|
|NodeInfo |Array of [NodeInfoObject](https://docs.byteplus.com/en/docs/61/15764#nodeinfoobject) |Yes |Refer to the request example. |Instance specification configuration. There is exactly one primary node and one secondary node, with 0 to 10 optional read\-only nodes. |
|StorageType |String |Yes |LocalSSD |Instance storage type. Fixed value `LocalSSD` (local SSD disk). |
|StorageSpace |Integer |Yes |100 |Instance storage space<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">Different specifications have different storage space value ranges. For detailed information on storage space value ranges, refer to <a href="https://docs.byteplus.com/en/docs/RDS_for_PG/product_specifications?lang=zh">Product specifications</a>. Unit in GB, step size of 10 GB.</div><br> |
|ChargeInfo |Object of [ChargeInfoObject](https://docs.byteplus.com/en/docs/61/15764#chargeinfoobject) |Yes |{<br><br>"ChargeType": "PostPaid"<br><br>} |Payment method. |


<span id="nodeinfoobject"></span>
### NodeInfoObject


|**Parameter** |**Type** |**Required?**  |**Example** |**Description** |
|---|---|---|---|---|
|NodeId |String |No |postgres\-ca7b7019\*\*\*\* |Node ID. You can call the [DescribeDBInstanceDetail](https://docs.byteplus.com/en/docs/RDS_for_PG/describedbinstancedetail) API to query.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">Required when modifying node specification and deleting nodes (ModifyDBInstancesSpec).</div><br> |
|ZoneId |String |Yes |cn\-beijing\-a |The availability zone where the node is located. You can call the [DescribeAvailabilityZones](https://docs.byteplus.com/en/docs/RDS_for_PG/describeavailabilityzones) API to query it.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="default">Required when creating an instance (CreateDBInstance), restoring to a new instance (RestoreToNewInstance), and adding or modifying nodes (ModifyDBInstancesSpec).</div><br><br><br>* <div data-tips="true" data-tips-type="default">Primary, secondary, and read\-only nodes can be deployed in different availability zones within the same region.</div><br> |
|NodeType |String |Yes |Primary |Node type, with values:<br><br><br>* `Primary`: Primary node.<br><br>* `Secondary`: indicates the secondary node.<br><br>* `ReadOnly`: Read\-only node. |
|NodeSpec |String |Yes |rds.postgres.1c2g |Node specification. Query specifications available for sale via [DescribeDBInstanceSpecs](https://docs.byteplus.com/en/docs/RDS_for_PG/describedbinstancespecs) API. |
|NodeOperateType |String |No |Create |Operation type. Range:<br><br><br>* `Create`: add.<br><br>* `Delete`: delete.<br><br>* `Modify`: modify.<br><br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="default">In the CreateDBInstance and RestoreToNewInstance APIs, this field can only be set to <code>Create</code>.</div><br><br><br>* <div data-tips="true" data-tips-type="default">When modifying instance configuration, the specified NodeOperateType must be passed in for the involved nodes.</div><br> |


<span id="chargeinfoobject"></span>
### ChargeInfoObject


|**Parameter** |**Type** |**Required?**  |**Example** |**Description** |
|---|---|---|---|---|
|ChargeType |String |Yes |PostPaid |Payment type. Values:<br><br><br>* `PostPaid`: pay\-as\-you\-go.<br><br>* `PrePaid`: subscription (default). |
|AutoRenew |Boolean |No |true |Is automatic renewal enabled for the prepaid scenario?<br><br><br>* `yes`: automatic renewal.<br><br>* `false`: no automatic renewal (default). |
|PeriodUnit |String |No |Month |Purchase period for prepaid scenarios.<br><br><br>* `Month`: monthly (default).<br><br>* `Year`: subscription. |
|Period |Integer |No |1 |Subscription duration in a prepaid scenario. default value: 1. |
|Number |Integer |No |1 |Instance purchase quantity. Acceptable integer values range from 1 to 20, with a default of 1.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">When ChargeInfoObject is referenced by the RestoreToNewInstance API, Number can only be set to 1.</div><br> |


<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters


|**Parameter** |**Type** |**Example** |**Description** |
|---|---|---|---|
|ChargeItemPrices |Array of [ChargeItemPriceObject](https://docs.byteplus.com/en/docs/61/15764#chargeitempriceobject) |Refer to the sample response. |Cost details. |
|Currency |String |RMB |Currency unit. |
|DiscountPrice |Double |1.125 |Instance discount price. |
|InstanceQuantity |Integer |3 |Number of instances. |
|OriginalPrice |Double |1.125 |Original instance price. |
|PayablePrice |Double |1.125 |Instance payable price. |


<span id="chargeitempriceobject"></span>
### ChargeItemPriceObject


|**Parameter** |**Type** |**Example** |**Description** |
|---|---|---|---|
|ChargeItemType |String |Primary |Billing item name, with values:<br><br><br>* `Primary`: Primary node.<br><br>* `Secondary`: indicates the secondary node.<br><br>* `ReadOnly`: Read\-only node.<br><br>* `Storage`: physical storage space. |
|ChargeItemKey |String |rds.pg.d1.1c2g |* If `ChargeItemKey` is set to `Primary`, `Secondary`, or `ReadOnly`, this parameter returns the instance specification, such as `rds.pg.d1.1c2g`.<br><br>* If `ChargeItemKey` is set to `Storage`, this parameter returns the storage key, such as `rds.pg.d1.localssd`. |
|ChargeItemValue |Integer |100 |* If `ChargeItemKey` is set to `Primary`, `Secondary`, or `ReadOnly`, this parameter returns the number of nodes, which is always 1.<br><br>* If `ChargeItemKey` is set to `Storage`, this parameter returns the storage capacity size in GB. |
|NodeNumPerInstance |Integer |3 |Number of nodes per instance. |
|OriginalPrice |Double |300 |Original price. |
|DiscountPrice |Double |200 |Discount price. |
|PayablePrice |Double |100 |Payable price. |


<span id=".56S65L6L"></span>
## Example

<span id=".6K-35rGC56S65L6L"></span>
### Sample request

```json
POST /?Action=DescribeDBInstancePriceDetail&Version=2022-01-01 HTTP/1.1
Content-Type: application/json
Host: rds-postgresql.cn-beijing.byteplusapi.com.cn
X-Date: 20231002T101010Z
Authorization: HMAC-SHA256 Credential=AKLTN2I0MmFiNzMxNWE5NDgzMzk4MmVjMTVkODlkZTZ****/20211202/cn-beijing/rds_postgresql/request,SignedHeaders=x-date, Signature=71d31fc7bcf990142851c9833c5656391486cda0ae2e0b8ada733b7c6458****
{
    "ChargeInfo": {
        "ChargeType": "PostPaid",
        "Number": 4
    },
    "StorageType": "LocalSSD",
    "StorageSpace": 100,
    "NodeInfo": [
        {
            "ZoneId": "cn-beijing-a",
            "NodeSpec": "rds.postgres.1c2g",
            "NodeType": "Primary",
            "NodeOperateType": "Create"
        },
        {
            "ZoneId": "cn-beijing-a",
            "NodeSpec": "rds.postgres.1c2g",
            "NodeType": "Secondary",
            "NodeOperateType": "Create"
        },
        {
            "ZoneId": "cn-beijing-a",
            "NodeSpec": "rds.postgres.1c2g",
            "NodeType": "ReadOnly",
            "NodeOperateType": "Create"
        }
    ]
}
```


<span id=".6L-U5Zue56S65L6L"></span>
### Sample response

```json
{
    "ResponseMetadata": {
        "RequestId": "20240321203800455D01FD2EA9F8DBDB22-973e03",
        "Action": "DescribeDBInstancePriceDetail",
        "Version": "2022-01-01",
        "Service": "rds_postgresql",
        "Region": "cn-beijing"
    },
    "Result": {
        "ChargeItemPrices": [
            {
                "ChargeItemKey": "rds.pg.d1.1c2g",
                "ChargeItemType": "Primary",
                "ChargeItemValue": 1,
                "DiscountPrice": 0.057499999999999996,
                "OriginalPrice": 0.25,
                "PayablePrice": 0.057499999999999996
            },
            {
                "ChargeItemKey": "rds.pg.d1.1c2g",
                "ChargeItemType": "Secondary",
                "ChargeItemValue": 1,
                "DiscountPrice": 0.057499999999999996,
                "OriginalPrice": 0.25,
                "PayablePrice": 0.057499999999999996
            },
            {
                "ChargeItemKey": "rds.pg.d1.1c2g",
                "ChargeItemType": "ReadOnly",
                "ChargeItemValue": 1,
                "DiscountPrice": 0.057499999999999996,
                "OriginalPrice": 0.25,
                "PayablePrice": 0.057499999999999996
            },
            {
                "ChargeItemKey": "rds.pg.d1.localssd",
                "ChargeItemType": "Storage",
                "ChargeItemValue": 100,
                "DiscountPrice": 0.08625,
                "NodeNumPerInstance": 3,
                "OriginalPrice": 0.375,
                "PayablePrice": 0.08625
            }
        ],
        "Currency": "人民币",
        "DiscountPrice": 1.035,
        "InstanceQuantity": 4,
        "OriginalPrice": 4.5,
        "PayablePrice": 1.035
    }
}
```
