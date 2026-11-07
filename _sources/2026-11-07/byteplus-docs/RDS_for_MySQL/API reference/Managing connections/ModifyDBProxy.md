---
title: "ModifyDBProxy"
product: "RDS for MySQL"
product_code: "RDS_for_MySQL"
source: "https://docs.byteplus.com/en/docs/RDS_for_MySQL/modifydbproxy"
---

## Request type

Asynchronous request.

## Precautions

* This API is used only to enable or disable the database proxy feature and to specify the number of CPU cores for the proxy node when the feature is enabled. It cannot be used to change the proxy node's configuration after the database proxy is enabled. To modify the configuration of the proxy node, use the [ModifyDBProxySpec](https://docs.byteplus.com/en/docs/RDS_for_MySQL/modifydbproxyspec) API.

* The database proxy feature for multiple node instances cannot be disabled.

* Overdue or recovering instances do not support modification of the database proxy feature.

## Request parameters

|**Parameter** |**Type** |**Is it required?**  |**Sample value** |**Description** |
|---|---|---|---|---|
|InstanceId |String |Yes |mysql\-cf4f3ddc\*\*\*\* |Instance ID. |
|EnableDBProxy |Boolean |Yes |false |The state of the database proxy for the instance. value range:<br><br><br>* `true`: enable.<br><br>* `false`: disable.<br><br><br>> **tip**<br><br><br>> When enabling or disabling the database proxy, you may encounter an "Operation not supported" or other errors. Call the [DescribeDBProxyConfig](https://docs.byteplus.com/en/docs/RDS_for_MySQL/describedbproxyconfig) API to query the specific reason.<br> |
|ProxyNodeCustom |Object of [ProxyNodeCustomObject](https://docs.byteplus.com/en/docs/40/54510#proxynodecustomobject) |No |See the request example. |The number of cores for the database proxy service of the instance.<br><br>> **tip**<br><br><br>> This parameter is required when EnableDBProxy is set to `true`.<br> |
|ConvertDefaultEndpoint |Boolean |No |true |Specifies whether to convert the default endpoint to a proxy endpoint when enabling the database proxy. Values:<br><br><br>* `yes`: yes. Default value.<br><br>* `false`: no. |

### ProxyNodeCustomObject

|**Parameter** |**Type** |**Is it required?**  |**Sample value** |**Description** |
|---|---|---|---|---|
|CpuNum |Integer |No |4 |The number of CPU cores for the database proxy service of the instance. Values are as follows:<br><br><br>* Value range: Upper limit 1024.<br><br>* For multiple node instances:<br><br>   * The recommended number of proxy cores is the `total number of CPUs of all serviceable nodes of the instance * 0.25` (round up the result).<br><br>   * The minimum number of proxy cores is the greater of 2 and `the number of CPU cores of the primary node * 0.125`.<br><br>* For double node instances:<br><br>   * The recommended number of proxy cores is `the total number of CPUs of all serviceable nodes of the instance * 0.5` (round up the result).<br><br>   * The minimum number of proxy cores is the greater of 2 and `the number of CPU cores of the primary node * 0.5`. |

## Response parameter

|**Parameter** |**Type** |**Example** |**Description** |
|---|---|---|---|
|OrderId |String |Order2002000002284548640 |Order ID. |

Call the ModifyDBProxy API to enable or disable the database proxy feature.

## Sample

### Sample request

```json
POST /?Action=ModifyDBProxy&Version=2022-01-01 HTTP/1.1
Content-Type: application/json
Host: rds-mysql.cn-beijing.byteplusapi.com.cn
X-Date: 20211202T101010Z
Authorization: HMAC-SHA256 Credential=AKLTN2I0MmFiNzMxNWE5NDgzMzk4MmVjMTVkODlkZTZ****/20211202/cn-beijing/rds_mysql/request,SignedHeaders=x-date, Signature=71d31fc7bcf990142851c9833c5656391486cda0ae2e0b8ada733b7c6458****
{
    "InstanceId": "mysql-cf4f3ddc****",
    "EnableDBProxy": true,
    "ProxyNodeCustom": {
        "CpuNum": 4
    },
    "ConvertDefaultEndpoint": true
}
```

### Sample response

```json
{
    "ResponseMetadata": {
        "RequestId": "202410121445576B08EFFCA6DD57334FDC-efdcec",
        "Action": "ModifyDBProxy",
        "Version": "2022-01-01",
        "Service": "rds_mysql",
        "Region": "cn-beijing"
    },
    "Result": {
        "OrderId": "Order2180000007639198690"
    }
}
```

## Error code

For more details, refer to [Error codes](https://docs.byteplus.com/en/docs/RDS_for_MySQL/error_code).
