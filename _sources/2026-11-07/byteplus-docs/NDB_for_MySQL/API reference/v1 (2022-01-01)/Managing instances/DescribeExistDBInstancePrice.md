---
title: "DescribeExistDBInstancePrice"
product: "NDB for mysql"
product_code: "NDB_for_MySQL"
source: "https://docs.byteplus.com/en/docs/NDB_for_MySQL/DescribeExistDBInstancePrice"
---

Call the DescribeExistDBInstancePrice to query the price details of an existing instance.

<span id=".6K-35rGC57G75Z6L"></span>
## Request type

Synchronous request.

<span id=".6LCD6K-V"></span>
## Debug

[去调试](https://api.byteplus.com/api-explorer/debug?action=DescribeExistDBInstancePrice&serviceCode=vedbm&version=2022-01-01&groupName=)


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters


|Name |Type |Required |Example |Description |
|---|---|---|---|---|
|Instances |Array of [InstanceInfo](https://docs.byteplus.com/en/docs/265/69781#instanceinfo) |Yes |See the request example. |Instance information. |
|UserAction |String |No |ModifyDBInstanceSpec |The action type. Valid values are:<br><br><br>* `ModifyDBInstanceSpec`: change instance configuration.<br><br>* `ModifyDBInstanceChargeType`: change billing method.<br><br>* `ModifyDBInstanceStorageType`: Change storage type. |
|ChargeType |String |No |PostPaid |Calculate billing type. Value:<br><br><br>* `PostPaid`: Pay\-as\-you\-go.<br><br>* `PrePaid`: Yearly or monthly subscription. |
|PeriodUnit |String |No |Month |The prepaid purchase duration.<br><br><br>* `Month`: Monthly subscription.<br><br>* `Year`: Yearly subscription.<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">This parameter is required when ChargeType (Calculate billing type) is set to PrePaid (Subscription).</div><br> |
|Period |Integer |No |1 |The purchase duration for a subscription.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">This parameter is required when ChargeType (Calculate billing type) is set to PrePaid (Subscription).</div><br> |


<span id="instanceinfo"></span>
### InstanceInfo


|Name |Type |Required |Example |Description |
|---|---|---|---|---|
|InstanceId |String |Yes |vedbm\-6subnyth\*\*\*\* |Instance ID. |
|StorageChargeType |String |No |PostPaid |Storage billing type. Value:<br><br><br>* PostPaid: Pay\-as\-you\-go.<br><br>* PrePaid: Yearly or monthly subscription. |
|PrePaidStorageInGB |Integer |No |50 |The storage space size in a subscription scenario.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">This parameter is required when StorageChargeType (Storage billing type) is set to PrePaid (Subscription).</div><br> |
|NodeSpecs |Array of [SpecObject](https://docs.byteplus.com/en/docs/265/69781#specobject) |No |Refer to the Sample response. |Node configuration of the instance. |
|StorageType |String |No |IOOptimizedStorage |Storage type. Value range:<br><br><br>* `IOOptimizedStorage`: IO performance type.<br><br>* `SmartCompressedStorage`: Intelligent compression type. |


<span id="specobject"></span>
### SpecObject


|Name |Type |Required |Example |Description |
|---|---|---|---|---|
|NodeType |String |Yes |DBEngine |Node type. Value:<br><br>`DBEngine`: Primary node/Read\-only node. |
|NodeNumber |Integer |No |2 |Number of nodes. |
|NodeSpec |String |No |vedb.mysql.x4.large |Node specification code. |


<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameter


|Name |Type |Example |Description |
|---|---|---|---|
|OriginalPrice |Double |1.18 |Original total price for the specified configuration. |
|DiscountPrice |Double |0.2478 |The total discounted price for the specified configuration. |
|PayablePrice |Double |0.2478 |Total payable price for the specified configuration. |
|ChargeType |String |configuration_hourly |Billing method. Values:<br><br><br>* `configuration_hourly`: postpaid, i.e., pay\-as\-you\-go.<br><br>* `fixed_price`: prepaid, i.e., monthly/annual subscription. |
|Currency |String |USD |Currency unit. Default value is RMB. |
|ChargeItemPrices |Array of [ChargeItemPriceObject](https://docs.byteplus.com/en/docs/265/69781#chargeitempriceobject) |Refer to the Sample response. |Details of each charge item for the specified configuration. |
|ConfigItemPrices |Array of [ConfigItemPriceObject](https://docs.byteplus.com/en/docs/265/69781#configitempriceobject) |Refer to the Sample response. |Detailed billing information for the specified configuration. |


<span id="chargeitempriceobject"></span>
### ChargeItemPriceObject


|Name |Type |Example |Description |
|---|---|---|---|
|ChargeItemCode |String |vedb.mysql.x4.medium_cn\-beijing |Charge item code. |
|OriginalPrice |Double |1.18 |Original total price for the specified configuration. |
|DiscountPrice |Double |0.2478 |The total discounted price for the specified configuration. |
|PayablePrice |Double |0.2478 |Total payable price for the specified configuration. |
|UnitPrice |Double |0.59 |Unit price of the billable item. |


<span id="configitempriceobject"></span>
### ConfigItemPriceObject


|Name |Type |Example |Description |
|---|---|---|---|
|InstanceID |String |vedbm\-6subnyth\*\*\*\* |Instance ID. |
|ConfigurationCode |String |\- |Configuration code. |
|DiscountPrice |Double |0.2478 |The total discounted price for the specified configuration. |
|PayablePrice |Double |0.2478 |Total payable price for the specified configuration. |
|OriginalPrice |Double |1.18 |Original total price for the specified configuration. |
|RefundAmount |Double |0 |Refundable amount. |
|CouponAmount |Double |0 |Amount deducted with a coupon. |
|Quantity |Long |1 |Number of instances. |
|ChargeItemPrices |Array of [ChargeItemPriceObject](https://docs.byteplus.com/en/docs/265/69781#chargeitempriceobject) |Refer to the Sample response. |Details of each charge item for the specified configuration. |


<span id=".56S65L6L"></span>
## Example

<span id=".6K-35rGC56S65L6L"></span>
### Request example

```json
POST /?Action=DescribeExistDBInstancePrice&Version=2022-01-01 HTTP/1.1
Content-Type: application/json
Host:vedbm.cn-beijing.byteplusapi.com.cn
X-Date: 20220101T101010Z
Authorization: HMAC-SHA256 Credential=AKLTN2I0MmFiNzMxNWE5NDgzMzk4MmVjMTVkODlkZTZ****/20220101/cn-beijing/vedbm/request,SignedHeaders=x-date, Signature=71d31fc7bcf990142851c9833c5656391486cda0ae2e0b8ada733b7c645****
{
    "Instances": [
        {
            "InstanceId": "vedbm-arjlc5di****",
            "NodeSpecs": [
                {
                    "NodeType": "DBEngine",
                    "NodeNumber": 2,
                    "NodeSpec": "vedb.mysql.x4.medium"
                }
            ],
            "StorageChargeType": "PostPaid"
        }
    ],
    "UserAction": "ModifyDBInstanceSpec",
    "ChargeType": "PostPaid"
}
```


<span id=".6L-U5Zue56S65L6L"></span>
### Response example

```json
{
    "ResponseMetadata": {
        "RequestId": "202507301524453E9B2D926A0B88DA9C34-0c1c87",
        "Action": "DescribeExistDBInstancePrice",
        "Version": "2022-01-01",
        "Service": "vedbm",
        "Region": "cn-beijing"
    },
    "Result": {
        "ChargeItemPrices": [
            {
                "ChargeItemCode": "vedb.mysql.x4.medium_cn-beijing",
                "DiscountPrice": 0.2478,
                "OriginalPrice": 1.18,
                "PayablePrice": 0.2478,
                "UnitPrice": 0.59
            },
            {
                "ChargeItemCode": "vedb.mysql.volume.clusterpool_cn-beijing",
                "DiscountPrice": 0,
                "OriginalPrice": 0,
                "PayablePrice": 0,
                "UnitPrice": 0.00486
            }
        ],
        "ChargeType": "configuration_hourly",
        "ConfigItemPrices": [
            {
                "ChargeItemPrices": [
                    {
                        "ChargeItemCode": "vedb.mysql.x4.medium_cn-beijing",
                        "DiscountPrice": 0.2478,
                        "OriginalPrice": 1.18,
                        "PayablePrice": 0.2478,
                        "UnitPrice": 0.59
                    },
                    {
                        "ChargeItemCode": "vedb.mysql.volume.clusterpool_cn-beijing",
                        "DiscountPrice": 0,
                        "OriginalPrice": 0,
                        "PayablePrice": 0,
                        "UnitPrice": 0.00486
                    }
                ],
                "ConfigurationCode": "",
                "CouponAmount": 0,
                "DiscountPrice": 0.2478,
                "InstanceID": "vedbm-arjlc5di****",
                "OriginalPrice": 1.18,
                "PayablePrice": 0.2478,
                "Quantity": 1,
                "RefundAmount": 0
            }
        ],
        "Currency": "USD",
        "DiscountPrice": 0.2478,
        "OriginalPrice": 1.18,
        "PayablePrice": 0.2478
    }
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error code

For details, refer to [Error codes](https://docs.byteplus.com/en/docs/NDB_for_MySQL/Error_codes).
