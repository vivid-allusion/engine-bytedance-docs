---
title: "DescribeDBProxyPriceDetail"
product: "RDS for MySQL"
product_code: "RDS_for_MySQL"
source: "https://docs.byteplus.com/en/docs/RDS_for_MySQL/describedbproxypricedetail"
---

Call the DescribeDBProxyPriceDetail API to query the billing information of the database proxy service for an instance.

## Request type

Synchronous request.

## Request parameters

|Name |Type |Required |Example |Description |
|---|---|---|---|---|
|InstanceId |String |Yes |mysql\-25651c34\*\*\*\* |Instance ID. |
|ProxyNodeCustom |Object |No |Please refer to the request example. |Database proxy configuration of the instance. |
|CpuNum |Integer |No |4 |The number of CPU cores of the instance database proxy service. Value range:<br><br><br>* Upper limit: 1024.<br><br>* For multi\-node instances,<br><br>   * The recommended number of proxy cores is `the total number of CPUs of all serviceable nodes of the instance * 0.25`, and the result is rounded up.<br><br>   * The lower limit of the number of proxy cores is the larger value between 2 and `the number of CPU cores of the master node * 0.125`.<br><br>* For dual\-node instances,<br><br>   * The recommended number of proxy cores is `the total number of CPUs of all serviceable nodes of the instance * 0.5`, and the result is rounded up.<br><br>   * The lower limit of the number of proxy cores is the larger value between 2 and `the number of CPU cores of the master node * 0.5`. |

## Response parameters

|Name |Type |Example |Description |
|---|---|---|---|
|ChargeItemPrices |Object[] |Please refer to the response example. |Specify the cost details of the database proxy configuration. |
|ChargeItemKey |String |rds.mysql.d1.1c2g_cn\-guangzhou |The Key of the billing item. |
|ChargeItemType |String |Proxy |Billing item names, with values:<br><br><br>* `Primary`: Primary node.<br><br>* `Secondary`: Secondary node.<br><br>* `ReadOnly`: Read\-only node.<br><br>* `Storage`: Physical storage space.<br><br>* `Proxy`: Database proxy. |
|ChargeItemValue |Long |6 |* If the value of ChargeItemType is `Primary`, `Secondary`, or `ReadOnly`, this field represents the number of nodes.<br><br>* If the value of ChargeItemType is `Proxy`, this field represents the number of CPU cores of the data proxy service.<br><br>* If the value of ChargeItemType is `Storage`, this field represents the storage space size of a single node, with the unit of GiB.<br><br>* If the value of ChargeItemType is `StoragePackage`, this field represents the size of the resource package, with the unit of GiB. |
|DiscountPrice |Double |0.3942 |The discount amount for this billing item. |
|OriginalPrice |Double |0.876 |The original price of this billing item. |
|PayablePrice |Double |0.3942 |The payable fee for this billing item. |
|Currency |String |CNY |Currency type. The default value is `CNY`. |
|DescribeDBProxyPriceDetailStr |Object |Please refer to the response example. |Price information returned as a string. |
|Currency |String | |Currency, default to RMB |
|CouponAmount |String | |@sdk_hide_next_line代金券抵扣金额 |
|PayablePrice |String | |应付总价 |
|DiscountPrice |String | |折扣总价 |
|OriginalPrice |String | |原始总价 |
|ChargeItemPrices |Object[] | |第一个配置项的费用明细，兼容单次询价 |
|ChargeItemKey |String |rds.mysql.d1.1c2g_cn\-guangzhou |The key of the billing item. |
|ChargeItemType |String |Proxy |Billing item names, with values:<br><br><br>* `Primary`: Primary node.<br><br>* `Secondary`: Secondary node.<br><br>* `ReadOnly`: Read\-only node.<br><br>* `Storage`: Physical storage space.<br><br>* `Proxy`: Database proxy. |
|ChargeItemValue |Long |6 |If the value of ChargeItemType is `Primary`, `Secondary` or `ReadOnly`, then this field is the number of nodes.<br><br> <br><br>If the value of ChargeItemType is `Proxy`, then this field is the number of cores of the data proxy service.<br><br> <br><br>If the value of ChargeItemType is `Storage`, this parameter returns the storage space size of a single node. |
|DiscountPrice |String |0.3942 |The discount amount of this billing item. |
|OriginalPrice |String |0.876 |The original price of this billing item. |
|PayablePrice |String |0.3942 |The payable fee for this billing item. |
|DiscountPrice |Double |0.3942 |Discount amount. |
|OriginalPrice |Double |0.876 |Original price. |
|PayablePrice |Double |0.3942 |Payable amount. |
|HidePriceInfo |Boolean |true |Whether the price information is hidden. If set, the specific price will be replaced with `***`. Values:<br><br><br>* `true`: Yes.<br><br>* `false`: No. |

## Sample request

```json
POST /?Action=DescribeDBProxyPriceDetail&Version=2022-01-01 HTTP/1.1
Content-Type: application/json
Host: open.ap-southeast-1.byteplusapi.com
X-Date: 20211202T101010Z
Authorization: HMAC-SHA256 Credential=AKLTN2I0MmFiNzMxNWE5NDgzMzk4MmVjMTVkODlkZTZ****/20211202/ap-southeast-1/rds_mysql/request,SignedHeaders=x-date, Signature=71d31fc7bcf990142851c9833c5656391486cda0ae2e0b8ada733b7c6458****
{
    "instanceid": "mysql-25651c34****",
    "ProxyNodeCustom": {
        "CpuNum": 6
    }
}
```

## Sample response

```json
{
    "ResponseMetadata": {
        "RequestId": "202506052002028A774423EE75A8635B4F-871992",
        "Action": "DescribeDBProxyPriceDetail",
        "Version": "2022-01-01",
        "Service": "rds_mysql",
        "Region": "ap-southeast-12"
    },
    "Result": {
        "ChargeItemPrices": [
            {
                "ChargeItemKey": "rds.mysql.d1.proxy.rcu_ap-southeast-1",
                "ChargeItemType": "Proxy",
                "ChargeItemValue": 6,
                "DiscountPrice": 0.3942,
                "OriginalPrice": 0.876,
                "PayablePrice": 0.3942,
                "UnitPrice": 0
            }
        ],
        "CouponAmount": 0,
        "Currency": "人民币",
        "DescribeDBProxyPriceDetailStr": {
            "ChargeItemPrices": [
                {
                    "ChargeItemKey": "rds.mysql.d1.proxy.rcu_ap-southeast-12",
                    "ChargeItemType": "Proxy",
                    "ChargeItemValue": 6,
                    "DiscountPrice": "0.3942",
                    "OriginalPrice": "0.876",
                    "PayablePrice": "0.3942"
                }
            ],
            "Currency": "人民币",
            "DiscountPrice": "0.3942",
            "OriginalPrice": "0.876",
            "PayablePrice": "0.3942"
        },
        "DiscountPrice": 0.3942,
        "OriginalPrice": 0.876,
        "PayablePrice": 0.3942
    }
}
```

## Error codes

For more details, refer to [Error codes](https://docs.byteplus.com/en/docs/RDS_for_MySQL/error_code).
