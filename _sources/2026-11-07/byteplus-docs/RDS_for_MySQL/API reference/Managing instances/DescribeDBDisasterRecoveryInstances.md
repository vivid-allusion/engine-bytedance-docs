---
title: "DescribeDBDisasterRecoveryInstances"
product: "RDS for MySQL"
product_code: "RDS_for_MySQL"
source: "https://docs.byteplus.com/en/docs/RDS_for_MySQL/DescribeDBDisasterRecoveryInstances"
---

Call the DescribeDBDisasterRecoveryInstances API to query the disaster recovery instance information of the instance.

## Request type

Synchronous request.

## Request parameters

|Name |Type |Required |Example |Description |
|---|---|---|---|---|
|InstanceId |String |Yes |mysql\-f83edc2e\*\*\*\* |Instance ID. |

## Response parameters

The range of returned parameters varies depending on the role of the incoming instance:

* If the incoming InstanceId is the disaster recovery instance ID, then DrDtsTaskId, TestTask, DrDtsTaskStatus, DrSecondsBehindMaster, MasterInstanceId, MasterInstanceName and MasterRegion are returned.

* If the incoming InstanceId is the primary instance ID, only DisasterRecoveryInstances are returned.

* When the disaster recovery link between the primary instance and the disaster recovery instance has not been created, regardless of whether the incoming InstanceId is the disaster recovery instance ID or the primary instance ID, DrDtsTaskId, TestTask and DrDtsTaskStatus are not returned.

* If the instance corresponding to the incoming InstanceId is neither the primary instance nor the disaster recovery instance, then an empty return is made.

|Name |Type |Example |Description |
|---|---|---|---|
|DisasterRecoveryInstances |Object[] |Please refer to the return example. |The information of the disaster recovery instance of the instance. |
|Region |String |cn\-shanghai |The region where the disaster recovery instance is located. |
|DtsTaskId |String |9c0c17a0b82f460b87b338d1db8d\*\*\*\* |The ID of the synchronization task between the primary instance and the disaster recovery instance. |
|InstanceId |String |mysql\-6c7c35fb\*\*\*\* |The ID of the disaster recovery instance. |
|DtsTaskName |String |TestTask |The name of the synchronization task between the primary instance and the disaster recovery instance. |
|InstanceName |String |DrInstance\-test |The name of the disaster recovery instance. |
|DtsTaskStatus |String |Running |The status of the synchronization task between the primary instance and the disaster recovery instance. |
|SecondsBehindMaster |Integer |0 |The latency between the disaster recovery instance and the primary instance. |
|MasterInstanceId |String |mysql\-f83edc2e\*\*\*\* |The ID of the main instance. |
|MasterInstanceName |String |Test Instance |The name of the main instance. |
|MasterRegion |String |cn\-guangzhou |The region where the main instance is located. |
|DrDtsTaskId |String |9c0c17a0b82f460b87b338d1db8d\*\*\*\* |The ID of the synchronization task between the primary instance and the disaster recovery instance. |
|DrDtsTaskName |String |TestTask |The name of the synchronization task between the primary instance and the disaster recovery instance. |
|DrSecondsBehindMaster |Integer |1 |The latency between the disaster recovery instance and the primary instance. |
|DrDtsTaskStatus |String |Running |The status of the synchronization task between the primary instance and the disaster recovery instance. |

## Sample request

```json
POST /?Action=DescribeDBDisasterRecoveryInstances&Version=2022-01-01
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
        "RequestId": "202507241529338A603E6C7E84B0047221-45a378",
        "Action": "DescribeDBDisasterRecoveryInstances",
        "Version": "2022-01-01",
        "Service": "rds_mysql",
        "Region": "cn-guangzhou"
    },
    "Result": {
        "DisasterRecoveryInstances": [
            {
                "DtsTaskId": "9c0c17a0b82f460b87b338d1db8d8189",
                "DtsTaskName": "TestTask",
                "DtsTaskStatus": "Running",
                "InstanceId": "mysql-6c7c35fb6aed",
                "InstanceName": "测试实例",
                "Region": "cn- hanghai",
                "SecondsBehindMaster": 1
            }
        ]
    }
}
```

## Error codes

For more details, refer to [Error codes](https://docs.byteplus.com/en/docs/RDS_for_MySQL/error_code).
