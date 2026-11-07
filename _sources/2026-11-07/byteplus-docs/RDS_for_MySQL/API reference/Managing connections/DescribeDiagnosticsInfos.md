---
title: "DescribeDiagnosticsInfos"
product: "RDS for MySQL"
product_code: "RDS_for_MySQL"
source: "https://docs.byteplus.com/en/docs/RDS_for_MySQL/describediagnosticsinfos"
---

Call the DescribeDiagnosticsInfos API to query the connection diagnostic results of an instance.

## Request type

Synchronous request.

## Request parameters

|Name |Type |Required |Example |Description |
|---|---|---|---|---|
|InstanceId |String |Yes |mysql\-db6d920e\*\*\*\* |Instance ID. |
|DiagnosticsType |String |No |PrivateLink |The connection type of the diagnosis. Values:<br><br><br>* `PrivateLink`: Private network connection.<br><br>* `PublicLink`: Public network connection.<br><br><br>tip<br><br>When this field is used as a request parameter, the default value is `PrivateLink`. |
|DiagnosticsResult |String |No |Abnormal |The overall result of the diagnostic item. Values:<br><br><br>* `Normal`: normal.<br><br>* `Abnormal`: abnormal.<br><br>* `NotDiagnose`: not diagnosed.<br><br>* `Diagnosing`: in the process of diagnosis.<br><br>* `DiagnoseFailed`: diagnosis failed. |
|PageSize |Integer |No |10 |Number of records per page. Minimum value is 1, maximum value does not exceed 100. Default value is 10. |
|PageNumber |Integer |No |1 |Current page number. The minimum value is 1. Default value is 1. |

## Response parameters

|Name |Type |Example |Description |
|---|---|---|---|
|DiagnosticsInfos |Object[] |Please refer to the response example. |Specific diagnostic information. |
|DiagnosticsItems |Object[] |Please refer to the return example. |Diagnostic information of connection diagnosis. |
|DiagnosticsItem |String |MySQLWhiteListPolicy |Diagnostic items for connection diagnosis. Values:<br><br><br>* `MySQLInstanceStatus`: MySQL instance status.<br><br>* `ECSInstanceStatus`: ECS instance status.<br><br>* `SameVpc`: The same VPC.<br><br>* `SameNetworkType`: Network type.<br><br>* `EcsSecurityGroupPolicy`: Security group policy.<br><br>* `MySQLWhiteListPolicy`: MySQL whitelist policy.<br><br>* `Other`: Others. Internal system error. |
|DiagnosticsResult |String |Abnormal |The overall result of the diagnostic item. Values:<br><br><br>* `Normal`: normal.<br><br>* `Abnormal`: abnormal.<br><br>* `NotDiagnose`: not diagnosed.<br><br>* `Diagnosing`: in the process of diagnosis.<br><br>* `DiagnoseFailed`: diagnosis failed. |
|PossibleEffect |String |The cloud server (ECS) cannot access the MySQL instance. |Possible impact of the diagnosis result. Returned when the diagnosis fails. |
|Suggestion |String |It is detected that the whitelist bound to your MySQL instance does not allow access to the IP of the cloud server (ECS). |Suggestions for improvement of the diagnosis result. Returned when the diagnosis fails. |
|DiagnosticsRecordId |String |6a2c3f29a96c45b3b400476eb6c2\*\*\*\* |Connection diagnostic record ID. |
|DiagnosticsResult |String |Normal |The overall result of connection diagnosis. Values:<br><br><br>* `Normal`: Normal.<br><br>* `Abnormal`: Abnormal.<br><br>* `NotDiagnose`: Not diagnosed.<br><br>* `Diagnosing`: In diagnosis.<br><br>* `DiagnoseFailed`: Diagnosis failed. |
|EcsInfo |Object |Please refer to the return example. |The information of the cloud server in the connection diagnosis. |
|EcsInstanceId |String |i\-yd7nac9mv44uvzod\*\*\*\* |Cloud server instance ID. |
|EcsInstanceName |String |Test Instance ECS |The name of the cloud server instance. |
|EcsPrivateIpv4Address |String |192. ** *.* ** .5 |The private IPv4 address of the cloud server instance. |
|EcsPrivateIpv6Address |String[] |2408: **:** : **:** : **:** :71c2 |The private IPv6 address of the cloud server instance. |
|EcsVpcId |String |vpc\-3jh82ag7t5g5c3pncmemv\*\*\*\* |The ID of the private network to which the cloud server instance belongs. |
|EcsVpcName |String |Test the private network. |The name of the private network to which the cloud server instance belongs. |
|EndpointInfo |Object |Please refer to the return example. |The information of the connection terminal in the connection diagnosis. |
|EndpointId |String |mysql\-db6d920e\*\*\*\*\-cluster |Connect to the terminal ID. |
|EndpointName |String |Default terminal |Connection terminal name. |
|PriaveDomain |String |mysqldb6d920e\*\*\*\*.rds.ivolces.com |The private network domain name of the connection terminal. |
|PrivateIpv4Address |String |192. ** *.* ** .19:3306 |Connect to the private network IPv4 address and port of the terminal. |
|PrivateIpv6Address |String |1200: **:** : **:** : **:** :3352:3306 |Connect to the private IPv6 address and port of the terminal. |
|PublicDomain |String |mysql\-db6d920e\*\*\*\*\-public.rds.volces.com |The public network domain name for connecting the terminal. |
|PublicIpAddress |String |10. ** *.* ** .114:3306 |Connect to the public network address and port of the terminal. |
|VpcId |String |vpc\-3jh82ag7t5g5c3pncmemv\*\*\*\* |The ID of the private network to which the terminal belongs. |
|VpcName |String |Test the private network. |The name of the private network to which the connected terminal belongs. |
|InstanceId |String |mysql\-db6d920e\*\*\*\* |Instance ID. |
|PublicAddressInfo |Object |Please refer to the return example. |The information of the public network server in the connection diagnosis. |
|EipId |String |eip\-3jh0q9ouwi9kw3pncmfw5\*\*\*\* |Public network ID. |
|EipName |String |Test public network |Public network name. |
|PublicIpAddress |String |192. ** *.* ** .5 |The public IP address. |
|DiagnosticsTaskStatus |String |Success |The execution status of the diagnostic task. Possible values are as follows:<br><br><br>* `NotStart`: The diagnosis has not started.<br><br>* `Running`: The diagnosis is in progress.<br><br>* `Failed`: The diagnosis failed.<br><br>* `Success`: The diagnosis is completed. |
|LastDiagnosticsTime |String |2024\-10\-31T02:57:20.000Z |The time when the last connection diagnosis was performed. The time format is `yyyy-MM-ddTHH:mm:ss.sssZ`(UTC time). |
|Total |Integer |3 |Total number of diagnostic results matching the query conditions. |

## Sample request

```json
POST /?Action=DescribeDiagnosticsInfos&Version=2022-01-01 HTTP/1.1
Content-Type: application/json
Host: open.ap-southeast-1.byteplusapi.com
X-Date: 20211202T101010Z
Authorization: HMAC-SHA256 Credential=AKLTN2I0MmFiNzMxNWE5NDgzMzk4MmVjMTVkODlkZTZ****/20211202/ap-southeast-1/rds_mysql/request,SignedHeaders=x-date, Signature=71d31fc7bcf990142851c9833c5656391486cda0ae2e0b8ada733b7c6458****
{
    "InstanceId": "mysql-db6d920e****"
}
```

## Sample response

```json
{
    "ResponseMetadata": {
        "RequestId": "2024103112060529E360524F9BD51239CB-3b3e28",
        "Action": "DescribeDiagnosticsInfos",
        "Version": "2022-01-01",
        "Service": "rds_mysql",
        "Region": "ap-southeast-1"
    },
    "Result": {
        "DiagnosticsInfos": [
            {
                "DiagnosticsItems": [
                    {
                        "DiagnosticsItem": "MySQLInstanceStatus",
                        "DiagnosticsResult": "Normal",
                        "PossibleEffect": "",
                        "Suggestion": ""
                    },
                    {
                        "DiagnosticsItem": "ECSInstanceStatus",
                        "DiagnosticsResult": "Normal",
                        "PossibleEffect": "",
                        "Suggestion": ""
                    },
                    {
                        "DiagnosticsItem": "SameVpc",
                        "DiagnosticsResult": "Normal",
                        "PossibleEffect": "",
                        "Suggestion": ""
                    },
                    {
                        "DiagnosticsItem": "SameNetworkType",
                        "DiagnosticsResult": "Normal",
                        "PossibleEffect": "",
                        "Suggestion": ""
                    },
                    {
                        "DiagnosticsItem": "EcsSecurityGroupPolicy",
                        "DiagnosticsResult": "Normal",
                        "PossibleEffect": "",
                        "Suggestion": ""
                    },
                    {
                        "DiagnosticsItem": "MySQLWhiteListPolicy",
                        "DiagnosticsResult": "Abnormal",
                        "PossibleEffect": "云服务器(ECS)无法访问MySQL实例",
                        "Suggestion": "检测到您MySQL实例所绑定白名单未放通对云服务器(ECS) IP的访问"
                    }
                ],
                "DiagnosticsRecordId": "6a5af3e3b36145cd95f11a5b90fd4da9",
                "DiagnosticsResult": "Abnormal",
                "EcsInfo": {
                    "EcsInstanceId": "i-yd7nac9mv44uvzod****",
                    "EcsInstanceName": "测试实例ECS",
                    "EcsPrivateIpv4Address": "192.***.***.5",
                    "EcsPrivateIpv6Address": null,
                    "EcsVpcId": "vpc-3jh82ag7t5g5c3pncmemv****",
                    "EcsVpcName": "测试私有网络"
                },
                "EndpointInfo": {
                    "EndpointId": "mysql-db6d920e****-cluster",
                    "EndpointName": "默认终端",
                    "PriaveDomain": "mysqldb6d920e****.rds-boe.ivolces.com",
                    "PrivateIpv4Address": "192.***.***.19:3306",
                    "PrivateIpv6Address": "",
                    "PublicDomain": "mysql-db6d920e****-public.rds-boe.volces.com",
                    "PublicIpAddress": "192.***.***.19:3306",
                    "VpcId": "vpc-3jh82ag7t5g5c3pncmemv****",
                    "VpcName": "测试私有网络"
                },
                "InstanceId": "mysql-db6d920e****"
            },
            {
                "DiagnosticsItems": [
                    {
                        "DiagnosticsItem": "MySQLInstanceStatus",
                        "DiagnosticsResult": "Normal",
                        "PossibleEffect": "",
                        "Suggestion": ""
                    },
                    {
                        "DiagnosticsItem": "MySQLWhiteListPolicy",
                        "DiagnosticsResult": "Abnormal",
                        "PossibleEffect": "无法访问MySQL实例",
                        "Suggestion": "检测到您MySQL实例所绑定白名单未放通对指定公网IP的访问"
                    }
                ],
                "DiagnosticsRecordId": "013bebfa2c7349039da3646213cc7ffa",
                "DiagnosticsResult": "Abnormal",
                "EndpointInfo": {
                    "EndpointId": "mysql-db6d920e****-cluster",
                    "EndpointName": "默认终端",
                    "PriaveDomain": "mysqldb6d920e****.rds-boe.ivolces.com",
                    "PrivateIpv4Address": "192.***.***.19:3306",
                    "PrivateIpv6Address": "",
                    "PublicDomain": "mysql-db6d920e****-public.rds-boe.volces.com",
                    "PublicIpAddress": "192.***.***.19:3306",
                    "VpcId": "vpc-3jh82ag7t5g5c3pncmemv****",
                    "VpcName": "测试私有网络"
                },
                "InstanceId": "mysql-db6d920e****",
                "PublicAddressInfo": {
                    "EipId": "eip-3jh0q9ouwi9kw3pncmfw5****",
                    "EipName": "测试公网",
                    "PublicIpAddress": "192.***.***.5"
                }
            }
        ],
        "DiagnosticsTaskStatus": "Success",
        "LastDiagnosticsTime": "2024-10-31T04:06:01.000Z",
        "Total": 2
    }
}
```

## Error codes

For more details, refer to [Error codes](https://docs.byteplus.com/en/docs/RDS_for_MySQL/error_code).
