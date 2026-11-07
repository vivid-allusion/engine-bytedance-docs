---
title: "DescribeResourcePackagePrice"
product: "RDS for MySQL"
product_code: "RDS_for_MySQL"
source: "https://docs.byteplus.com/en/docs/RDS_for_MySQL/DescribeResourcePackagePrice"
---

Call the DescribeResourcePackagePrice interface to query the purchase price of the resource package.

## Request type

Synchronous request.

## Request parameters

|Name |Type |Required |Example |Description |
|---|---|---|---|---|
|PackageType |String |Yes |StoragePackage |The type of the resource package. Currently, only the value `StoragePackage` is supported, which means a storage package. |
|PackageSpec |String |Yes |100 |Resource package specifications. If the value of PackageType is StoragePackage, the valid values for PackageSpec are as follows:<br><br><br>* `100`: 100 GiB.<br><br>* `200`: 200 GiB.<br><br>* `300`: 300 GiB.<br><br>* `500`: 500 GiB.<br><br>* `1000`: 1000 GiB.<br><br>* `2000`: 2000 GiB.<br><br>* `5000`: 5000 GiB.<br><br>* `10000`: 10000 GiB. |
|ChargeInfo |Object |Yes |Please refer to the request example. |The purchase duration of the resource package. |
|ChargeType |String |Yes |PostPaid |Payment type. Value:<br><br><br>* `PostPaid`: Pay\-as\-you\-go (postpaid).<br><br>* `PrePaid`: Annual or monthly subscription (prepaid). |
|AutoRenew |Boolean |No |true |Whether to automatically renew upon expiration in the prepaid scenario. Value range:<br><br><br>* `true`: Automatically renew upon expiration.<br><br>* `false`: Do not automatically renew upon expiration.<br><br><br>tip<br><br><br>* When the value of ChargeType is PrePaid, this parameter is required.<br><br>* When the value of ChargeType is PostPaid, this parameter does not need to be passed in. |
|PeriodUnit |String |No |Month |The purchase cycle in the prepaid scenario. Value range:<br><br><br>* `Month`: The purchase cycle is monthly.<br><br>* `Year`: The purchase cycle is yearly.<br><br><br>tip<br><br><br>* When the value of ChargeType is PrePaid, this parameter is required.<br><br>* When the value of ChargeType is PostPaid, this parameter does not need to be passed in. |
|Period |Integer |No |1 |The purchase duration in the prepaid scenario. The value range of this parameter depends on the value of PeriodUnit:<br><br><br>* When the value of PeriodUnit is `Month`, the value of Period is 1~9.<br><br>* When the value of PeriodUnit is `Year`, the value of Period is 1~3.<br><br><br>tip<br><br><br>* When the value of ChargeType is PrePaid, this parameter is required.<br><br>* When the value of ChargeType is PostPaid, this parameter does not need to be passed in. |
|Number |Integer |No |1 |The number of instances purchased. The value range is 1~50. The default value is 1.<br><br>tip<br><br><br>* In the RestoreToNewInstance and RestoreToCrossRegionInstance interfaces, only the value 1 is supported for this field.<br><br>* It is not supported to specify names for instances separately when creating instances in batches. When creating instances in batches:<br><br>   * If the instance name is specified in the InstanceName parameter, the serial number will be added after the specified instance name to name the batch\-created instances.<br><br>   * If the instance name is not specified in the InstanceName parameter, the instance ID will be used to name the instance. |

## Response parameters

|Name |Type |Example |Description |
|---|---|---|---|
|OriginalPrice |Double |120 |Original total price. |
|DiscountPrice |Double |120 |Total price after discount. |
|PayablePrice |Double |120 |Total payable price. |
|Currency |String |Renminbi (RMB) |Currency unit. The default value is `Renminbi`. |
|ChargeItemPrices |Object[] |Please refer to the return example. |Cost details of configuration items |
|ChargeItemKey |String |rds.mysql.d1.1c2g_cn\-guangzhou |The Key of the billing item. |
|ChargeItemType |String |Proxy |Billing item names, with values:<br><br><br>* `Primary`: Primary node.<br><br>* `Secondary`: Secondary node.<br><br>* `ReadOnly`: Read\-only node.<br><br>* `Storage`: Physical storage space.<br><br>* `Proxy`: Database proxy. |
|ChargeItemValue |Long |6 |* If the value of ChargeItemType is `Primary`, `Secondary`, or `ReadOnly`, this field represents the number of nodes.<br><br>* If the value of ChargeItemType is `Proxy`, this field represents the number of CPU cores of the data proxy service.<br><br>* If the value of ChargeItemType is `Storage`, this field represents the storage space size of a single node, with the unit of GiB.<br><br>* If the value of ChargeItemType is `StoragePackage`, this field represents the size of the resource package, with the unit of GiB. |
|DiscountPrice |Double |0.3942 |The discount amount for this billing item. |
|OriginalPrice |Double |0.876 |The original price of this billing item. |
|PayablePrice |Double |0.3942 |The payable fee for this billing item. |
|Quantity |Integer |2 |Number. |
|HidePriceInfo |Boolean |false |Whether the price information is hidden. If set, the specific price will be replaced with `***`. Values:<br><br><br>* `true`: Yes.<br><br>* `false`: No. |

## Sample request

```json
POST /?Action=DescribeResourcePackagePrice&Version=2022-01-01
Host: open.ap-southeast-1.byteplusapi.com
Content-Type: application/json
X-Date: 20180614T114308Z
Authorization: HMAC-SHA256 Credential=AKIAIAGMBG4SXSQQ****/20180614/ap-southeast-1/rds_mysql/request, SignedHeaders=accept;content-type;host;x-date, Signature=6a593bf5f59e7c1109fb205c739d1cff4c672fe2d251963f4d48c8701d16****
{
    "PackageType": "StoragePackage",
    "PackageSpec": "100",
    "ChargeInfo": {
        "PeriodUnit": "Month",
        "Period": 1,
        "Number": 2
    }
}
```

## Sample response

```json
{
    "ResponseMetadata": {
        "RequestId": "20250922224931B99C6E39ED68C0631967-9216c5",
        "Action": "DescribeResourcePackagePrice",
        "Version": "2022-01-01",
        "Service": "rds_mysql",
        "Region": "cn-beijing"
    },
    "Result": {
        "ChargeItemPrices": [
            {
                "ChargeItemKey": "rds.mysql.storage.pkg100",
                "ChargeItemType": "StoragePackage",
                "ChargeItemValue": 100,
                "DiscountPrice": 120,
                "OriginalPrice": 120,
                "PayablePrice": 120,
                "UnitPrice": 0
            }
        ],
        "Currency": "",
        "DiscountPrice": 120,
        "HidePriceInfo": false,
        "OriginalPrice": 120,
        "PayablePrice": 120,
        "Quantity": 2
    }
}
```

## Error codes

For more details, refer to [Error codes](https://docs.byteplus.com/en/docs/RDS_for_MySQL/error_code).
