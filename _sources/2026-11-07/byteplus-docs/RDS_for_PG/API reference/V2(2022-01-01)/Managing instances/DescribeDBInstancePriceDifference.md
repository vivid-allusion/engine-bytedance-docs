---
title: "DescribeDBInstancePriceDifference"
product: "RDS for PostgreSQL"
product_code: "RDS_for_PG"
source: "https://docs.byteplus.com/en/docs/RDS_for_PG/describedbinstancepricedifference"
---

Call the DescribeDBInstancePriceDifference API to query instance price difference.

<span id=".6K-35rGC57G75Z6L"></span>
## Request type

Synchronous request.

<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters


|**Parameter** |**Type** |**Required?**  |**Example** |**Description** |
|---|---|---|---|---|
|InstanceId |String |Yes |postgres\-5aeb3f0b\*\*\*\* |Instance ID.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">When ModifyType is set to <code>Temporary</code>, the instance specified by InstanceId can only be a prepaid (subscription) instance.</div><br> |
|NodeInfo |Array of [NodeInfoObject](https://docs.byteplus.com/en/docs/61/15773#nodeinfoobject) |Yes |Refer to the request example. |Instance specification configuration. There is exactly one primary node and one secondary node, with 0 to 10 optional read\-only nodes.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">When ModifyType value is <code>Temporary</code>, NodeID must be specified.</div><br> |
|StorageType |String |Yes |LocalSSD |Instance storage type. Fixed value `LocalSSD` (local SSD disk). |
|StorageSpace |Integer |Yes |100 |Instance storage space. Unit is GB, with a step size of 10 GB.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="default">Different specifications have different storage space value ranges. For detailed information on storage space value ranges, refer to <a href="https://docs.byteplus.com/en/docs/RDS_for_PG/product_specifications?lang=zh">Product specifications</a>.</div><br><br><br>* <div data-tips="true" data-tips-type="default">This field is required when ModifyType is <code>Temporary</code>, and its value can only be the current storage space size of the instance.</div><br> |
|ChargeInfo |Object of [ChargeInfoObject](https://docs.byteplus.com/en/docs/61/15773#chargeinfoobject) |Yes |{<br><br>"ChargeType": "PostPaid"<br><br>} |Payment method.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">When ModifyType is set to <code>Temporary</code>, ChargeType can only be <code>PrePaid</code>.</div><br> |
|ModifyType |String |No |Temporary |Modification method. Values are:<br><br><br>* `Usually`: regular modification of specification, which takes effect immediately. Default value.<br><br>* `Temporary`: elastic upgrade, that is, temporary upgrade.<br><br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">Only instances with the billing method of subscription support the parameter value <code>Temporary</code>. You can query the instance's billing method by calling the <a href="https://docs.byteplus.com/en/docs/RDS_for_PG/describedbinstancedetail">DescribeDBInstanceDetail</a> API.</div><br> |
|RollbackTime |String |No |2023\-12\-16T03:59:10.000Z |Restoration time. The time format is `yyyy-MM-ddTHH:mm:ss.sssZ` (UTC time).<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="default">This parameter is required when ModifyType is <code>Temporary</code>.</div><br><br><br>* <div data-tips="true" data-tips-type="default">This parameter is effective only when ModifyType is <code>Temporary</code>.</div><br><br><br>* <div data-tips="true" data-tips-type="default">The set restoration time should not differ from the API call time by more than 2 minutes. The actual restoration time is based on the API call time.</div><br><br><br>* <div data-tips="true" data-tips-type="default">Temporary upgrades can be initiated multiple times to extend the temporary upgrade period, but the total duration cannot exceed 30 days (based on the time of the first temporary upgrade initiation).</div><br><br><br>* <div data-tips="true" data-tips-type="default">Multiple temporary upgrades can be initiated, but their duration cannot be shortened. If the instance is already in the temporary upgrade period:</div><br><br><br>   * <div data-tips="true" data-tips-type="default">The new restoration date cannot be earlier than the effective restoration date.</div><br><br><br>   * <div data-tips="true" data-tips-type="default">When the subscription instance is within five days of expiration, initiating another temporary upgrade is not allowed.</div><br> |


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


|**Parameter** |**Type** |**Is it required?**  |**Example** |**Description** |
|---|---|---|---|---|
|ChargeType |String |Yes |PostPaid |Payment type. Values:<br><br><br>* `PostPaid`: pay\-as\-you\-go.<br><br>* `PrePaid`: subscription (default). |
|AutoRenew |Boolean |No |true |Is automatic renewal enabled for the prepaid scenario?<br><br><br>* `yes`: automatic renewal.<br><br>* `false`: no automatic renewal (default). |
|PeriodUnit |String |No |Month |purchase period for prepaid scenarios.<br><br><br>* `Month`: monthly (default).<br><br>* `Year`: subscription. |
|Period |Integer |No |1 |Subscription duration in a prepaid scenario. Default value: 1. |
|Number |Integer |No |1 |Instance purchase quantity. Acceptable integer values range from 1 to 20, with a default of 1.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">When ChargeInfoObject is referenced by the RestoreToNewInstance API, Number can only be set to 1.</div><br> |


<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters


|**Parameter** |**Type** |**Example** |**Description** |
|---|---|---|---|
|Currency |String |RMB |Currency unit. Default is RMB. |
|OriginalPrice |Double |\-17.5 |Original instance price. |
|DiscountPrice |Double |\-17.5 |Instance discount price. |
|PayablePrice |Double |\-17.5 |Instance payable price. |
|ChargeItemPrices |Array of [ChargeItemPriceObject](https://docs.byteplus.com/en/docs/61/15773#chargeitempriceobject) |refer to return example |Cost details. |


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

<span id=".6K-35rGC56S65L6LLTE="></span>
### Sample request 1 Query price difference for regular modification of specification on instance

```json
POST /?Action=DescribeDBInstancePriceDifference&Version=2022-01-01 HTTP/1.1
Content-Type: application/json
Host: rds-postgresql.cn-beijing.byteplusapi.com.cn
X-Date: 20231002T101010Z
Authorization: HMAC-SHA256 Credential=AKLTN2I0MmFiNzMxNWE5NDgzMzk4MmVjMTVkODlkZTZ****/20211202/cn-beijing/rds_postgresql/request,SignedHeaders=x-date, Signature=71d31fc7bcf990142851c9833c5656391486cda0ae2e0b8ada733b7c6458****
{
    "InstanceId": "postgres-5aeb3f0b****",
    "NodeInfo": [
        {
            "NodeSpec": "rds.postgres.1c2g",
            "NodeType": "Primary"
        },
        {
            "NodeSpec": "rds.postgres.1c2g",
            "NodeType": "Secondary"
        }
    ],
    "StorageType": "LocalSSD",
    "StorageSpace": 100,
    "ChargeInfo": {
        "ChargeType": "PrePaid"
    }
}
```


<span id=".6L-U5Zue56S65L6LLTE="></span>
### Sample response 1

```json
{
    "ResponseMetadata": {
        "RequestId": "202306192156254A900086CBECA123D60F",
        "Action": "DescribeDBInstancePriceDifference",
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
                "DiscountPrice": 120.345,
                "OriginalPrice": 120.345,
                "PayablePrice": 120.345
            },
            {
                "ChargeItemKey": "rds.pg.d1.1c2g",
                "ChargeItemType": "Secondary",
                "ChargeItemValue": 1,
                "DiscountPrice": 120.345,
                "OriginalPrice": 120.345,
                "PayablePrice": 120.345
            },
            {
                "ChargeItemKey": "rds.pg.d1.localssd",
                "ChargeItemType": "Storage",
                "ChargeItemValue": 100,
                "DiscountPrice": 0.05368034,
                "NodeNumPerInstance": 2,
                "OriginalPrice": 0.25,
                "PayablePrice": 0.05368034
            }
        ],
        "Currency": "人民币",
        "DiscountPrice": -17.5,
        "OriginalPrice": -17.5,
        "PayablePrice": -17.5
    }
}
```


<span id=".6K-35rGC56S65L6LLTI="></span>
### Sample request 2 Query price difference for temporary upgrade of an instance (upgrade node specification)

```json
POST /?Action=DescribeDBInstancePriceDifference&Version=2022-01-01 HTTP/1.1
Content-Type: application/json
Host: rds-postgresql.cn-beijing.byteplusapi.com.cn
X-Date: 20231002T101010Z
Authorization: HMAC-SHA256 Credential=AKLTN2I0MmFiNzMxNWE5NDgzMzk4MmVjMTVkODlkZTZ****/20211202/cn-beijing/rds_postgresql/request,SignedHeaders=x-date, Signature=71d31fc7bcf990142851c9833c5656391486cda0ae2e0b8ada733b7c6458****
{
    "InstanceId": "postgres-3461581d****",
    "NodeInfo": [
        {
            "NodeId": "postgres-3461581d****",
            "NodeSpec": "rds.postgres.2c4g",
            "NodeType": "Primary"
        },
        {
            "NodeId": "postgres-3461581d****-wjrh",
            "NodeSpec": "rds.postgres.2c4g",
            "NodeType": "Secondary"
        },
        {
            "NodeId": "postgres-3461581d****-ro6bf6",
            "NodeSpec": "rds.postgres.2c4g",
            "NodeType": "ReadOnly"
        }
    ],
    "ChargeInfo": {
        "ChargeType": "PrePaid"
    },
    "StorageType": "LocalSSD",
    "StorageSpace": 20,
    "ModifyType": "Temporary",
    "RollbackTime": "2023-12-16T03:49:10.000Z"
}
```


<span id=".6L-U5Zue56S65L6LLTI="></span>
### Sample response 2

```json
{
    "ResponseMetadata": {
        "RequestId": "202306192156254A900086CBECA123D60F",
        "Action": "DescribeDBInstancePriceDifference",
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
                "DiscountPrice": 120.345,
                "OriginalPrice": 120.345,
                "PayablePrice": 120.345
            },
            {
                "ChargeItemKey": "rds.pg.d1.1c2g",
                "ChargeItemType": "Secondary",
                "ChargeItemValue": 1,
                "DiscountPrice": 120.345,
                "OriginalPrice": 120.345,
                "PayablePrice": 120.345
            },
            {
                "ChargeItemKey": "rds.pg.d1.localssd",
                "ChargeItemType": "Storage",
                "ChargeItemValue": 100,
                "DiscountPrice": 0.05368034,
                "NodeNumPerInstance": 2,
                "OriginalPrice": 0.25,
                "PayablePrice": 0.05368034
            }
        ],
        "Currency": "人民币",
        "DiscountPrice": -17.5,
        "OriginalPrice": -17.5,
        "PayablePrice": -17.5
    }
}
```
