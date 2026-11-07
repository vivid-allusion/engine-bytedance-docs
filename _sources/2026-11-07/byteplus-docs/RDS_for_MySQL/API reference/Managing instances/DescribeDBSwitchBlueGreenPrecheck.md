---
title: "DescribeDBSwitchBlueGreenPrecheck"
product: "RDS for MySQL"
product_code: "RDS_for_MySQL"
source: "https://docs.byteplus.com/en/docs/RDS_for_MySQL/DescribeDBSwitchBlueGreenPrecheck"
---

Call the DescribeDBSwitchBlueGreenPrecheck interface to query the pre\-check result of the blue\-green deployment switch.

## Request type

Synchronous request.

## Request parameters

|Name |Type |Required |Example |Description |
|---|---|---|---|---|
|InstanceId |String |Yes |mysql\-f83edc2e\*\*\*\* |The ID of the blue instance in blue\-green deployment. |
|BeginTime |String |No |2025\-07\-24T09:20:52.477Z |Specify the starting time (UTC time) when querying the pre\-check results according to the time range. The format is `yyyy-MM-ddTHH:mm:ss.sssZ`.<br><br>tip<br><br>There is no default value. If not set, the query results will be returned according to the query conditions set by other fields. |
|EventId |String |No |20250724171204259F91326A6ACD0B791D\-5176f4 |The ID of the pre\-check event for blue\-green deployment switching.<br><br>tip<br><br>There is no default value. If not set, it will return according to the query conditions set in other fields. |

## Response parameters

|Name |Type |Example |Description |
|---|---|---|---|
|PrecheckResults |Object[] |Please refer to the return example. |The pre\-check results of the blue\-green deployment switch. |
|Result |String |Pass |Pre\-check result. Value:<br><br><br>* `Pass`: Passed.<br><br>* `Failed`: Failed. |
|TaskId |String |2025072417253957250BB01665529D2515\-961d25 |Task ID. |
|Progress |Long |100 |The progress of the pre\-check. The unit is percentage. |
|CheckTime |String |2025\-07\-24T09:25:52.477Z |The initiation time of the pre\-check (UTC time). The format is `yyyy-MM-ddTHH:mm:ss.sssZ`. |
|EffectiveTime |String |2025\-07\-25T09:25:52.477Z |The end point of the pre\-check result validity period (UTC time). The format is `yyyy-MM-ddTHH:mm:ss.sssZ`. |
|PrecheckItems |Object[] |Please refer to the return example. |Pre\-check items for blue\-green deployment switching. |
|CheckDetail |Object |{<br><br>"Impact": "The sorting of the results returned after SQL execution may differ from that before the upgrade.",<br><br>"Issue": "After the upgrade, the default character collation is changed to utf8mb4_0900_ai_ci."<br><br>} |Detailed information on the inspection items that failed to pass. |
|Issue |String |The sorting of the results returned after SQL execution may differ from that before the upgrade. |Problems that cause the inspection items to fail. |
|Impact |String |After the upgrade, the default character order is changed to utf8mb4_0900_ai_ci. |The impact brought by the issues that caused the failure of the inspection items after the upgrade. |
|Description |String |initConnectCheck |Description information of the inspection item. |
|ItemName |String |initConnectCheck |The name of the inspection item. |
|RiskLevel |String |Warning |The risk level of the items that failed the check. Values:<br><br><br>* `Notice`: Prompt.<br><br>* `Warning`: Warning.<br><br>* `Error`: Error. |
|GreenInstanceId |String |mysql\-06c7db72\*\*\*\* |The ID of the green instance in the blue\-green deployment. |

## Sample request

```json
POST /?Action=DescribeDBSwitchBlueGreenPrecheck&Version=2022-01-01
Host: open.ap-southeast-1.byteplusapi.com
Content-Type: application/json
X-Date: 20180614T114308Z
Authorization: HMAC-SHA256 Credential=AKIAIAGMBG4SXSQQ****/20180614/ap-southeast-1/rds_mysql/request, SignedHeaders=accept;content-type;host;x-date, Signature=6a593bf5f59e7c1109fb205c739d1cff4c672fe2d251963f4d48c8701d16****
{
    "InstanceId": "mysql-f83edc2e****"
}
```

## Sample response

```json
{
    "ResponseMetadata": {
        "RequestId": "202507241749444958F4F8739B10011CCC-32eedc",
        "Action": "DescribeDBSwitchBlueGreenPrecheck",
        "Version": "2022-01-01",
        "Service": "rds_mysql",
        "Region": "cn-guangzhou"
    },
    "Result": {
        "PrecheckResults": [
            {
                "CheckTime": "2025-07-24T09:25:52.477Z",
                "EffectiveTime": "2025-07-25T09:25:52.477Z",
                "GreenInstanceId": "mysql-06c7db72****",
                "PrecheckItems": [
                    {
                        "Description": "蓝色、绿色实例切换后，监控告警配置可能不一致。",
                        "ItemName": "check_monitor",
                        "RiskLevel": "Notice"
                    },
                    {
                        "Description": "切换蓝色、绿色实例不会迁移实例备份。",
                        "ItemName": "check_backup",
                        "RiskLevel": "Notice"
                    },
                    {
                        "Description": "蓝色、绿色实例切换过程中，不会切换 IP，仅切换您指定的终端的域名。",
                        "ItemName": "check_domain",
                        "RiskLevel": "Notice"
                    },
                    {
                        "Description": "检查蓝色实例和绿色实例的增量数据一致性。",
                        "ItemName": "check_dts_incr_data_validation",
                        "RiskLevel": "Warning"
                    }
                ],
                "Progress": 100,
                "Result": "Pass",
                "TaskId": "2025072417253957250BB01665529D2515-961d25"
            },
            {
                "CheckTime": "2025-07-24T09:12:17.139Z",
                "EffectiveTime": "2025-07-25T09:12:17.139Z",
                "GreenInstanceId": "mysql-06c7db72****",
                "PrecheckItems": [
                    {
                        "Description": "蓝色、绿色实例切换后，监控告警配置可能不一致。",
                        "ItemName": "check_monitor",
                        "RiskLevel": "Notice"
                    },
                    {
                        "Description": "切换蓝色、绿色实例不会迁移实例备份。",
                        "ItemName": "check_backup",
                        "RiskLevel": "Notice"
                    },
                    {
                        "Description": "蓝色、绿色实例切换过程中，不会切换 IP，仅切换您指定的终端的域名。",
                        "ItemName": "check_domain",
                        "RiskLevel": "Notice"
                    },
                    {
                        "Description": "检查蓝色实例和绿色实例的增量数据一致性。",
                        "ItemName": "check_dts_incr_data_validation",
                        "RiskLevel": "Warning"
                    }
                ],
                "Progress": 100,
                "Result": "Pass",
                "TaskId": "20250724171204259F91326A6ACD0B791D-5176f4"
            }
        ]
    }
}
```

## Error codes

For more details, refer to [Error codes](https://docs.byteplus.com/en/docs/RDS_for_MySQL/error_code).
