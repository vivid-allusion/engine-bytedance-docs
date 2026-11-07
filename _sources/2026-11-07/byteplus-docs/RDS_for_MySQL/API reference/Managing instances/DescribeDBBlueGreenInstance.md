---
title: "DescribeDBBlueGreenInstance"
product: "RDS for MySQL"
product_code: "RDS_for_MySQL"
source: "https://docs.byteplus.com/en/docs/RDS_for_MySQL/DescribeDBBlueGreenInstance"
---

Call the DescribeDBBlueGreenInstance interface to query the blue\-green deployment information of the instance.

## Request type

Synchronous request.

## Request parameters

|Name |Type |Required |Example |Description |
|---|---|---|---|---|
|InstanceId |String |Yes |mysql\-f83edc2e\*\*\*\* |Instance ID. |

## Response parameters

|Name |Type |Example |Description |
|---|---|---|---|
|GreenInstance |Object |Please refer to the return example. |The information of the green instance in the blue\-green deployment. |
|DtsTaskId |String |9879df1b169e4271abeafc5b393\*\*\*\* |The ID of the synchronization task in blue\-green deployment.<br><br>tip<br><br>If the synchronization task for blue\-green deployment has not been created yet, this field will return empty. |
|InstanceId |String |mysql\-d4a1171e\*\*\*\* |Instance ID. |
|DtsTaskName |String |BlueGreenTest |The name of the blue\-green deployment synchronization task.<br><br>tip<br><br>If the synchronization task for blue\-green deployment has not been created, this field will not be returned. |
|InstanceName |String |Test instance |Instance name. |
|DtsTaskStatus |String |Canceled |The status of the blue\-green deployment synchronization task. |
|SecondsBehindMaster |Integer |17 |The latency between blue\-green instances. |
|BlueInstance |Object |Please refer to the return example. |The information of the blue instance in the blue\-green deployment. |
|DtsTaskId |String |9879df1b169e4271abeafc5b393\*\*\*\* |The ID of the synchronization task in blue\-green deployment.<br><br>tip<br><br>If the synchronization task for blue\-green deployment has not been created yet, this field will return empty. |
|InstanceId |String |mysql\-d4a1171e\*\*\*\* |Instance ID. |
|DtsTaskName |String |BlueGreenTest |The name of the blue\-green deployment synchronization task.<br><br>tip<br><br>If the synchronization task for blue\-green deployment has not been created, this field will not be returned. |
|InstanceName |String |Test instance |Instance name. |
|DtsTaskStatus |String |Canceled |The status of the blue\-green deployment synchronization task. |
|SecondsBehindMaster |Integer |17 |The latency between blue\-green instances. |

## Sample request

```json
POST /?Action=DescribeDBBlueGreenInstance&Version=2022-01-01
Host: open.ap-southeast-1.byteplusapi.com
Content-Type: application/json
X-Date: 20180614T114308Z
Authorization: HMAC-SHA256 Credential=AKIAIAGMBG4SXSQQ****/20180614/ap-southeast-1/rds_mysql/request, SignedHeaders=accept;content-type;host;x-date, Signature=6a593bf5f59e7c1109fb205c739d1cff4c672fe2d251963f4d48c8701d16****
{
    "InstanceId": "mysql-d4a1171e****"
}
```

## Sample response

```json
{
    "ResponseMetadata": {
        "RequestId": "202508122025128CD75BD341C74881E68C-402322",
        "Action": "DescribeDBBlueGreenInstance",
        "Version": "2022-01-01",
        "Service": "rds_mysql",
        "Region": "cn-chongqing-sdv"
    },
    "Result": {
        "BlueInstance": {
            "DtsTaskId": "9879df1b169e4271abeafc5b3939****",
            "InstanceId": "mysql-d4a1171e****",
            "InstanceName": "蓝绿部署-蓝色实例"
        },
        "GreenInstance": {
            "DtsTaskId": "879df1b169e4271abeafc5b3939****",
            "DtsTaskName": "test",
            "InstanceId": "mysql-23987082****",
            "InstanceName": "蓝绿部署-绿色实例",
            "SecondsBehindMaster": 17
        }
    }
}
```

## Error codes

For more details, refer to [Error codes](https://docs.byteplus.com/en/docs/RDS_for_MySQL/error_code).
