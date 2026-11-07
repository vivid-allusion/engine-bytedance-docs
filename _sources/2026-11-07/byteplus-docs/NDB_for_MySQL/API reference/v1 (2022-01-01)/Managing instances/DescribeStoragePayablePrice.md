---
title: "DescribeStoragePayablePrice"
product: "NDB for mysql"
product_code: "NDB_for_MySQL"
source: "https://docs.byteplus.com/en/docs/NDB_for_MySQL/DescribeStoragePayablePrice"
---

Call the DescribeStoragePayablePrice API to query the storage price.

## Request type

Synchronous request.

## Debug

[去调试](https://api.byteplus.com/api-explorer/debug?action=DescribeStoragePayablePrice&serviceCode=vedbm&version=2022-01-01&groupName=)

## Request parameters

|Name |Type |Required |Example |Description |
|---|---|---|---|---|
|StorageTypes |Array of String |Yes |Clusterpool |Storage type. The value can be:<br><br><br>* `Clusterpool`: Storage space.<br><br>* `ColdDataArchive`: Cold data storage space.<br><br>* `CompressClusterpool`: Compressed storage space. |
|ChargeType |String |No |PostPaid |Billing method.<br><br><br>* `PostPaid`: Pay\-as\-you\-go (default).<br><br>* `PrePaid`: Yearly or monthly subscription.<br><br><br>> **tip**<br><br><br>> When `StorageTypes` is set to `ColdDataArchive`, this parameter only supports `PostPaid`.<br> |
|Period |Integer |No |1 |The purchase duration for a subscription.<br><br>> **tip**<br><br><br>> This parameter is required when `ChargeType` is `PrePaid`.<br> |
|PeriodUnit |String |No |Month |The prepaid purchase duration.<br><br><br>* `Month`: Monthly subscription.<br><br>* `Year`: Yearly subscription.<br><br><br>> **tip**<br><br><br>> This parameter is required when `ChargeType` is `PrePaid`.<br> |
|PrePaidStorageInGB |Integer |No |1 |The storage space size in a subscription scenario.<br><br>> **tip**<br><br><br>> This parameter is required when `ChargeType` is `PrePaid`.<br> |

## Response parameter

|Name |Type |Example |Description |
|---|---|---|---|
|ChargeItemPrices |Array of [ChargeItemPriceObject](https://docs.byteplus.com/en/docs/265/69779#chargeitempriceobject) |Refer to the Sample response. |Details of each charge item for the specified configuration. |

### ChargeItemPriceObject

|Name |Type |Example |Description |
|---|---|---|---|
|ChargeItemCode |String |vedb.mysql.x4.medium_cn\-beijing |Charge item code. |
|OriginalPrice |Double |1.18 |Original total price for the specified configuration. |
|DiscountPrice |Double |0.2478 |The total discounted price for the specified configuration. |
|PayablePrice |Double |0.2478 |Total payable price for the specified configuration. |
|UnitPrice |Double |0.59 |Unit price of the billing item. |

## Example

### Request example

```json
POST /?Action=DescribeStoragePayablePrice&Version=2022-01-01 HTTP/1.1
Content-Type: application/json
Host:vedbm.cn-beijing.byteplusapi.com.cn
X-Date: 20220101T101010Z
Authorization: HMAC-SHA256 Credential=AKLTN2I0MmFiNzMxNWE5NDgzMzk4MmVjMTVkODlkZTZ****/20220101/cn-beijing/vedbm/request,SignedHeaders=x-date, Signature=71d31fc7bcf990142851c9833c5656391486cda0ae2e0b8ada733b7c645****
{
    "StorageTypes": [
        "ColdDataArchive",
        "Clusterpool"
    ]
}
```

### Response example

```json
{
    "ResponseMetadata": {
        "RequestId": "20250730144744BC794C9DC3607CD66FB9-65d7ac",
        "Action": "DescribeStoragePayablePrice",
        "Version": "2022-01-01",
        "Service": "vedbm",
        "Region": "cn-beijing"
    },
    "Result": {
        "ChargeItemPrices": [
            {
                "ChargeItemCode": "vedb.mysql.volume.cold.data.archive_cn-beijing",
                "DiscountPrice": 0.0000441,
                "OriginalPrice": 0.00021,
                "PayablePrice": 0.0000441,
                "UnitPrice": 0.00021
            },
            {
                "ChargeItemCode": "vedb.mysql.volume.clusterpool_cn-beijing",
                "DiscountPrice": 0.0010206,
                "OriginalPrice": 0.00486,
                "PayablePrice": 0.0010206,
                "UnitPrice": 0.00486
            }
        ]
    }
}
```

## Error code

For details, refer to [Error codes](https://docs.byteplus.com/en/docs/NDB_for_MySQL/Error_codes).
