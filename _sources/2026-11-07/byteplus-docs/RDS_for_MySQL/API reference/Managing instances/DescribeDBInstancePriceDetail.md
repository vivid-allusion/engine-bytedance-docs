---
title: "DescribeDBInstancePriceDetail"
product: "RDS for MySQL"
product_code: "RDS_for_MySQL"
source: "https://docs.byteplus.com/en/docs/RDS_for_MySQL/describedbinstancepricedetail"
---

Call the DescribeDBInstancePriceDetail API to query the price details of the MySQL instance.

<span id=".6K-35rGC57G75Z6L"></span>
## Request type

Synchronous request.

<span id=".6LCD6K-V"></span>
## Request parameters


|Parameter |Type |Is it required? |Sample value |Description |
|---|---|---|---|---|
|NodeInfo |Array of [NodeInfoObject](https://docs.byteplus.com/en/docs/40/15516#nodeinfoobject) |Yes |See the request example. |Node configuration of the instance. |
|StorageType |String |Yes |LocalSSD |The storage type of the instance. Range:<br><br><br>* `LocalSSD`: local SSD.<br><br>* `CloudESSD_FlexPL`: Cloud ESSD FlexPL.<br><br>* `CloudESSD_PL0`: Cloud ESSD PL0.<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">The StorageType parameter is required if you set the StorageSpace parameter.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">When the InstanceType is set to <code>SingleNode</code>, the StorageType can only be <code>CloudESSD_FlexPL</code> or <code>CloudESSD_PL0</code>.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">This parameter has different value ranges for different APIs. The rules are as follows:</div><br><br><br>   * <div data-tips="true" data-tips-type="tip">When used as a request parameter in the following APIs, StorageType can only be <code>LocalSSD</code>.</div><br><br><br>      * <div data-tips="true" data-tips-type="tip">RestoreToCrossRegionInstance</div><br><br><br>      * <div data-tips="true" data-tips-type="tip">RestoreToNewInstanceFromUserTos</div><br><br><br>* <div data-tips="true" data-tips-type="tip">When used as a request parameter for some API operations, the value range of this parameter is related to the storage type of the original instance. The specific rules are as follows:</div><br><br><br>   * <div data-tips="true" data-tips-type="tip">If the original instance storage type is <code>LocalSSD</code> or <code>CloudESSD_FlexPL</code>, changing the storage type is not supported.</div><br><br><br>   * <div data-tips="true" data-tips-type="tip">If the original instance storage type is <code>CloudESSD_PL0</code>, the value can be <code>CloudESSD_PL0</code> or <code>CloudESSD_FlexPL</code>.</div><br><br><br>      <div data-tips="true" data-tips-type="tip">The related APIs are:      </div><br>      <br><br>      * <div data-tips="true" data-tips-type="tip">RebuildDBInstance</div><br><br><br>      * <div data-tips="true" data-tips-type="tip">RestoreToNewInstance</div><br><br><br>      * <div data-tips="true" data-tips-type="tip">ModifyDBNodeSpec</div><br> |
|StorageSpace |Integer |Yes |100 |Different storage types and specifications have different storage space value ranges. For detailed information on storage space value ranges, see [Product specifications](https://docs.byteplus.com/en/docs/RDS_for_MySQL/product_specifications). The unit is GiB, and the step size is 10 GiB. |
|ChargeType |String |Yes |PostPaid |Billing method. Values:<br><br><br>* `PostPaid`: pay\-as\-you\-go (post\-paid).<br><br>* `PrePaid`: subscription (pre\-paid). |
|PeriodUnit |String |No |Month |Purchase period for prepaid scenarios.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">This parameter is not required when the value of ChargeType is <code>PostPaid</code>.</div><br><br><br><br>* `Month`: the purchase cycle is by month. Default.<br><br>* `Year`: the purchase cycle is by year. |
|Period |Integer |No |2 |The duration quantity for the prepaid mode. |
|Number |Integer |No |1 |Number of instances. |
|ProxyNodeCustom |Object of [ProxyNodeCustom](https://docs.byteplus.com/en/docs/40/15516#proxynodecustom) |No |See the request example. |The proxy configuration of the instance. |


<span id="nodeinfoobject"></span>
### NodeInfoObject


|Parameter |Type |Is it required? |Sample value |Description |
|---|---|---|---|---|
|NodeId |String |No |mysql\-050b3e08\*\*\*\*\-r6e25 |Node ID.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">This parameter is not required when you create an instance or add a node, but is required when you modify the node configuration or delete a node.</div><br> |
|NodeType |String |Yes |Primary |Node type, with values:<br><br><br>* `Primary`: primary node.<br><br>* `Secondary`: secondary node.<br><br>* `ReadOnly`: read\-only node.<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">This parameter is optional for the DescribeDBInstancePriceDetail API.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">When you add a node by calling the CreateDBNodes API, you can set this parameter only to <code>ReadOnly</code> for a double\-node instance or <code>Secondary</code> for a multiple\-node instance.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">A double\-node instance consists of one primary node, one secondary node, and 0 to 10 optional read\-only nodes.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">A multiple\-node instance consists of one primary node, and at least one and up to eight secondary nodes. We recommend that you reserve an independent secondary node that does not handle workloads. This allows you to switch it to the primary node when necessary. RDS for MySQL assumes no responsibility for any risks or losses incurred due to the failure to configure independent secondary nodes or the inability to complete the primary node switching due to excessive latency of all secondary nodes.</div><br> |
|NodeSpec |String |Yes |rds.mysql.1c2g |Node specification. For details on node specification, refer to [Product specification](https://docs.byteplus.com/en/docs/RDS_for_MySQL/product_specifications).<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">The specification of the secondary node must be the same as that of the primary node.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">The read\-only node specification can be lower than the primary node specification. However, when the read\-only node specification is lower than the primary node specification, the read\-only node may be delayed or even experience an OOM error due to the high load on the primary node. It is recommended that the read\-only node be selected with the same or higher specification as the primary node.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">If StorageType is set to <code>CloudESSD_FlexPL</code> or <code>CloudESSD_PL0</code>, only the general type can be passed for NodeSpec.</div><br> |
|ZoneId |String |Yes |cn\-beijing\-a |The availability zone where the node is located. You can call the [DescribeAvailabilityZones](https://docs.byteplus.com/en/docs/RDS_for_MySQL/describeavailabilityzones) API to query it. Required when creating an instance or adding a node. Optional when changing node configuration or deleting a node.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">The nodes of an instance can be distributed across a maximum of three availability zones.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">During a single configuration change, you can add or delete nodes in up to three availability zones.</div><br> |
|NodeOperateType |String |No |Modify |Operation type. This parameter is not required when you create an instance but is required when you modify the node configuration. Range:<br><br><br>* `Create`: add.<br><br>* `Modify`: modify.<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">When adding a node (CreateDBNodes), this field can only be <code>Create</code>.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">When you modify the configuration, the value of this field can only be <code>Modify</code>.</div><br> |


<span id="proxynodecustom"></span>
### ProxyNodeCustom


|Parameter |Type |Is it required? |Sample value |Description |
|---|---|---|---|---|
|CpuNum |Integer |No |4 |The number of CPU cores for the database proxy service of the instance. Range:<br><br><br>* Maximum: 1,024.<br><br>* For a multiple\-node instance,<br><br>   * The recommended number of proxy cores is the `total number of CPUs of all serviceable nodes of the instance * 0.25` (round up the result).<br><br>   * The minimum number of proxy cores is the greater of 2 and `the number of CPU cores of the primary node * 0.125`.<br><br>* For a double\-node instance,<br><br>   * The recommended number of proxy cores is `the total number of CPUs of all serviceable nodes of the instance * 0.5` (round up the result).<br><br>   * The minimum number of proxy cores is the greater of 2 and `the number of CPU cores of the primary node * 0.5`. |


<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters


|Parameter |Type |Sample value |Description |
|---|---|---|---|
|DescribeDBInstancePriceDetailStr |Object of [DescribeDBInstancePriceDetailStr](https://docs.byteplus.com/en/docs/40/15516#describedbinstancepricedetailstr) |Refer to the Sample response. |Detailed billing information of the specified configuration. |
|HidePriceInfo |Boolean |true |Whether the price information is hidden. If this parameter is set, the specific price is replaced with `***`. Values:<br><br><br>* `true`: yes.<br><br>* `false`: no. |


<span id="describedbinstancepricedetailstr"></span>
### DescribeDBInstancePriceDetailStr


|Parameter |Type |Sample value |Description |
|---|---|---|---|
|BillingMethod |String |fixed_price |Billing method. Values are:<br><br><br>* `configuration_hourly`: postpaid, i.e., pay\-as\-you\-go.<br><br>* `fixed_price`: prepaid, i.e., monthly/annual subscription. |
|ChargeItemPrices |Array of [ChargeItemPriceObjectStr](https://docs.byteplus.com/en/docs/40/15516#chargeitempriceobjectstr) |Refer to the Sample response. |Fee details for the specified configuration. |
|CouponAmount |String |0 |Amount deducted with a coupon. |
|Currency |String |RMB |Currency unit. Default value is `RMB`. |
|DiscountPrice |String |2160 |The total discounted price for the specified configuration. |
|OriginalPrice |String |2880 |The original total price of the specified configuration. |
|PayablePrice |String |2160 |The payable price for the specified configuration. |
|Quantity |Integer |1 |Number of instances. |
|RefundAmount |String |0 |Refundable amount. |


<span id="chargeitempriceobjectstr"></span>
### ChargeItemPriceObjectStr


|Parameter |Type |Sample value |Description |
|---|---|---|---|
|ChargeItemKey |String |rds.mysql.d1.1c2g_cn\-guangzhou |Key of the billing item. |
|ChargeItemType |String |Proxy |Name of the billing item. Value:<br><br><br>* `Primary`: primary node.<br><br>* `Secondary`: secondary node.<br><br>* `ReadOnly`: read\-only node.<br><br>* `Storage`: physical storage space.<br><br>* `Proxy`: database proxy. |
|ChargeItemValue |Long |6 |If ChargeItemType is set to `Primary`, `Secondary`, or `ReadOnly`, this field indicates the number of nodes.<br><br>If ChargeItemType is set to `Proxy`, this field indicates the number of proxy cores.<br><br>If ChargeItemType is set to `Storage`, this parameter returns the storage space size of a single node. |
|DiscountPrice |String |0.3942 |The discount amount for the billing item. |
|OriginalPrice |String |0.876 |The original price of the billing item. |
|PayablePrice |String |0.3942 |The payable price for this billing item. |


<span id=".56S65L6L"></span>
## Sample

<span id=".6K-35rGC56S65L6LLTE="></span>
### Sample request 1

Query the price of an instance in Pay\-as\-you\-go mode.

```json
POST /?Action=DescribeDBInstancePriceDetail&Version=2022-01-01 HTTP/1.1
Accept: application/json
Content-Type: application/json
Host: rds-mysql.cn-beijing.byteplusapi.com.cn
X-Date: 20211202T101010Z
Authorization: HMAC-SHA256 Credential=AKLTN2I0MmFiNzMxNWE5NDgzMzk4MmVjMTVkODlkZTZ****/20211202/cn-beijing/rds_mysql/request,SignedHeaders=x-date, Signature=71d31fc7bcf990142851c9833c5656391486cda0ae2e0b8ada733b7c6458****
{
    "StorageType": "LocalSSD",
    "StorageSpace": 100,
    "ChargeType": "PostPaid",
    "NodeInfo": [
        {
            "NodeSpec": "rds.mysql.4c8g",
            "NodeType": "Primary"
        },
        {
            "NodeSpec": "rds.mysql.4c8g",
            "NodeType": "Secondary"
        },
        {
            "NodeSpec": "rds.mysql.1c2g",
            "NodeType": "ReadOnly"
        },
        {
            "NodeSpec": "rds.mysql.1c2g",
            "NodeType": "ReadOnly"
        }
    ],
    "Number": 1,
    "ProxyNodeCustom": {
        "CpuNum": 4
    }
}
```


<span id=".6L-U5Zue56S65L6LLTE="></span>
### Sample response 1

```json
{
    "ResponseMetadata": {
        "RequestId": "2025060612093670AA7AD4D88A34BC51E7-708074",
        "Action": "DescribeDBInstancePriceDetail",
        "Version": "2022-01-01",
        "Service": "rds_mysql",
        "Region": "cn-beijing"
    },
    "Result": {
        "DescribeDBInstancePriceDetailStr": {
            "BillingMethod": "configuration_hourly",
            "ChargeItemPrices": [
                {
                    "ChargeItemKey": "rds.mysql.d1.4c8g_cn-beijing",
                    "ChargeItemType": "Primary",
                    "ChargeItemValue": 1,
                    "DiscountPrice": "0.45",
                    "OriginalPrice": "1.00",
                    "PayablePrice": "0.45",
                    "UnitPrice": ""
                },
                {
                    "ChargeItemKey": "rds.mysql.d1.4c8g_cn-beijing",
                    "ChargeItemType": "Secondary",
                    "ChargeItemValue": 1,
                    "DiscountPrice": "0.45",
                    "OriginalPrice": "1.00",
                    "PayablePrice": "0.45",
                    "UnitPrice": ""
                },
                {
                    "ChargeItemKey": "rds.mysql.d1.1c2g_cn-beijing",
                    "ChargeItemType": "ReadOnly",
                    "ChargeItemValue": 1,
                    "DiscountPrice": "0.11",
                    "OriginalPrice": "0.25",
                    "PayablePrice": "0.11",
                    "UnitPrice": ""
                },
                {
                    "ChargeItemKey": "rds.mysql.d1.1c2g_cn-beijing",
                    "ChargeItemType": "ReadOnly",
                    "ChargeItemValue": 1,
                    "DiscountPrice": "0.11",
                    "OriginalPrice": "0.25",
                    "PayablePrice": "0.11",
                    "UnitPrice": ""
                },
                {
                    "ChargeItemKey": "rds.mysql.d1.localssd_cn-beijing",
                    "ChargeItemType": "Storage",
                    "ChargeItemValue": 100,
                    "DiscountPrice": "0.23",
                    "OriginalPrice": "0.50",
                    "PayablePrice": "0.23",
                    "UnitPrice": ""
                },
                {
                    "ChargeItemKey": "rds.mysql.d1.proxy.rcu_cn-beijing",
                    "ChargeItemType": "Proxy",
                    "ChargeItemValue": 4,
                    "DiscountPrice": "0.1971",
                    "OriginalPrice": "0.438",
                    "PayablePrice": "0.1971",
                    "UnitPrice": ""
                }
            ],
            "CouponAmount": "",
            "Currency": "人民币",
            "DiscountPrice": "1.55",
            "OriginalPrice": "3.44",
            "PayablePrice": "1.55",
            "Quantity": 1,
            "RefundAmount": ""
        },
        "DiscountPrice": 1.55,
        "HidePriceInfo": false,
        "OriginalPrice": 3.44,
        "PayablePrice": 1.55,
        "Quantity": 1,
        "RefundAmount": 0
    }
}
```


<span id=".6K-35rGC56S65L6LLTI="></span>
### Sample request 2

Query the price of an instance in monthly/annual subscription mode.

```json
POST /?Action=DescribeDBInstancePriceDetail&Version=2022-01-01 HTTP/1.1
Accept: application/json
Content-Type: application/json
Host: rds-mysql.cn-beijing.byteplusapi.com.cn
X-Date: 20211202T101010Z
Authorization: HMAC-SHA256 Credential=AKLTN2I0MmFiNzMxNWE5NDgzMzk4MmVjMTVkODlkZTZ****/20211202/cn-beijing/rds_mysql/request,SignedHeaders=x-date, Signature=71d31fc7bcf990142851c9833c5656391486cda0ae2e0b8ada733b7c6458****
{
    "StorageType": "LocalSSD",
    "StorageSpace": 100,
    "ChargeType": "PrePaid",
    "PeriodUnit": "Month",
    "Period": 2,
    "NodeInfo": [
        {
            "NodeSpec": "rds.mysql.4c8g",
            "NodeType": "Primary"
        },
        {
            "NodeSpec": "rds.mysql.4c8g",
            "NodeType": "Secondary"
        },
        {
            "NodeSpec": "rds.mysql.1c2g",
            "NodeType": "ReadOnly"
        },
        {
            "NodeSpec": "rds.mysql.1c2g",
            "NodeType": "ReadOnly"
        }
    ],
    "Number": 1,
    "ProxyNodeCustom": {
        "CpuNum": 4
    }
}
```


<span id=".6L-U5Zue56S65L6LLTI="></span>
### Sample response 2

```json
{
    "ResponseMetadata": {
        "RequestId": "2025060611525303D5FB296DFA7FB77DD8-a8336d",
        "Action": "DescribeDBInstancePriceDetail",
        "Version": "2022-01-01",
        "Service": "rds_mysql",
        "Region": "cn-beijing2"
    },
    "Result": {
        "DescribeDBInstancePriceDetailStr": {
            "BillingMethod": "fixed_price",
            "ChargeItemPrices": [
                {
                    "ChargeItemKey": "rds.mysql.d1.4c8g_cn-beijing",
                    "ChargeItemType": "Primary",
                    "ChargeItemValue": 1,
                    "DiscountPrice": "720.00",
                    "OriginalPrice": "960.00",
                    "PayablePrice": "720.00",
                    "UnitPrice": ""
                },
                {
                    "ChargeItemKey": "rds.mysql.d1.4c8g_cn-beijing",
                    "ChargeItemType": "Secondary",
                    "ChargeItemValue": 1,
                    "DiscountPrice": "720.00",
                    "OriginalPrice": "960.00",
                    "PayablePrice": "720.00",
                    "UnitPrice": ""
                },
                {
                    "ChargeItemKey": "rds.mysql.d1.1c2g_cn-beijing",
                    "ChargeItemType": "ReadOnly",
                    "ChargeItemValue": 1,
                    "DiscountPrice": "180.00",
                    "OriginalPrice": "240.00",
                    "PayablePrice": "180.00",
                    "UnitPrice": ""
                },
                {
                    "ChargeItemKey": "rds.mysql.d1.1c2g_cn-beijing",
                    "ChargeItemType": "ReadOnly",
                    "ChargeItemValue": 1,
                    "DiscountPrice": "180.00",
                    "OriginalPrice": "240.00",
                    "PayablePrice": "180.00",
                    "UnitPrice": ""
                },
                {
                    "ChargeItemKey": "rds.mysql.d1.localssd_cn-beijing",
                    "ChargeItemType": "Storage",
                    "ChargeItemValue": 100,
                    "DiscountPrice": "360.00",
                    "OriginalPrice": "480.00",
                    "PayablePrice": "360.00",
                    "UnitPrice": ""
                },
                {
                    "ChargeItemKey": "rds.mysql.d1.proxy.rcu_cn-beijing",
                    "ChargeItemType": "Proxy",
                    "ChargeItemValue": 4,
                    "DiscountPrice": "0.1971",
                    "OriginalPrice": "0.438",
                    "PayablePrice": "0.1971",
                    "UnitPrice": ""
                }
            ],
            "CouponAmount": "0",
            "Currency": "",
            "DiscountPrice": "2160",
            "OriginalPrice": "2880",
            "PayablePrice": "2160",
            "Quantity": 1,
            "RefundAmount": ""
        },
        "DiscountPrice": 2160,
        "HidePriceInfo": false,
        "OriginalPrice": 2880,
        "PayablePrice": 2160,
        "Quantity": 1,
        "RefundAmount": 0
    }
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error code

For more details, refer to [Error codes](https://docs.byteplus.com/en/docs/RDS_for_MySQL/error_code).
