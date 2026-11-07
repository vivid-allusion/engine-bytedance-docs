---
title: "DescribeDBProxy"
product: "RDS for MySQL"
product_code: "RDS_for_MySQL"
source: "https://docs.byteplus.com/en/docs/RDS_for_MySQL/DescribeDBProxy"
---

Call the DescribeDBProxy API to query the proxy configuration of the instance.

## Request type

Synchronous request.

## Request parameters

|Name |Type |Required |Example |Description |
|---|---|---|---|---|
|InstanceId |String |Yes |mysql\-54fc7408\*\*\*\* |Instance ID. |

## Response parameters

|Name |Type |Example |Description |
|---|---|---|---|
|ProxyDetail |Object |Please refer to the return example. |Proxy information |
|DBProxyStatus |String |Shutdown |The status of the database proxy function of the instance. Values:<br><br><br>* `Creating`: The proxy is being started.<br><br>* `Running`: The proxy is running.<br><br>* `Shutdown`: The proxy has been shut down.<br><br>* `Deleting`: The proxy is being shut down. |
|ProxyResourceInfo |Object |Please refer to the return example. |The resource information of the database proxy service of the instance. |
|MaxProxyCpuNum |Integer |1024 |The maximum number of cores that the user can configure for the database proxy service. |
|MinProxyCpuNum |Integer |2 |The minimum number of cores that a user can configure for the database proxy service. |
|CurrentProxyCpuNum |Integer |2 |The number of cores of the current instance database proxy service. |

## Sample request

```json
POST /?Action=DescribeDBProxy&Version=2022-01-01
Host: open.ap-southeast-1.byteplusapi.com
Content-Type: application/json
X-Date: 20180614T114308Z
Authorization: HMAC-SHA256 Credential=AKIAIAGMBG4SXSQQ****/20180614/ap-southeast-1/rds_mysql/request, SignedHeaders=accept;content-type;host;x-date, Signature=6a593bf5f59e7c1109fb205c739d1cff4c672fe2d251963f4d48c8701d16****
{
    "InstanceId": "mysql-54fc7408****"
}
```

## Sample response

```json
{
    "ResponseMetadata": {
        "RequestId": "20250724200740F86AA2C013975813C517-16fc92",
        "Action": "DescribeDBProxy",
        "Version": "2022-01-01",
        "Service": "rds_mysql",
        "Region": "cn-guangzhou"
    },
    "Result": {
        "ProxyDetail": {
            "DBProxyStatus": "Running",
            "ProxyResourceInfo": {
                "CurrentProxyCpuNum": 2,
                "MaxProxyCpuNum": 1024,
                "MinProxyCpuNum": 2
            }
        }
    }
}
```

## Error codes

For more details, refer to [Error codes](https://docs.byteplus.com/en/docs/RDS_for_MySQL/error_code).
