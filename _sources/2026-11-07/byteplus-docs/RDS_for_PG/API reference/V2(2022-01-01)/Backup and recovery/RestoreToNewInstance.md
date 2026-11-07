---
title: "RestoreToNewInstance"
product: "RDS for PostgreSQL"
product_code: "RDS_for_PG"
source: "https://docs.byteplus.com/en/docs/RDS_for_PG/restoretonewinstance"
---

Call the RestoreToNewInstance API to restore data to a new instance.

<span id=".6K-35rGC57G75Z6L"></span>
## Request type

Asynchronous request.

<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters


|**Parameter** |**Type** |**Required?**  |**Example** |**Description** |
|---|---|---|---|---|
|SrcInstanceId |String |Yes |postgres\-21a3333b\*\*\*\* |ID of the source instance to which the backup file belongs. |
|BackupId |String |No |20230801\-170\*\*\*\* |Backup file ID of the source instance. Use the data saved in this backup file to create a new instance. You can query the backup file list information of the specified instance by calling [DescribeBackups](https://docs.byteplus.com/en/docs/RDS_for_PG/describebackups).<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">At least one of BackupId or RestoreTime should be provided. If both BackupId and RestoreTime are provided, BackupId takes precedence.</div><br> |
|RestoreTime |String |No |2022\-01\-01T10:10:10Z |Any point in time within the retention period of the source instance log backup, formatted as` yyyy-MM-ddTHH:mm:ssZ` (UTC time). Call the [DescribeRecoverableTime](https://docs.byteplus.com/en/docs/RDS_for_PG/describerecoverabletime) API to query the time range for data recovery from an instance backup.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">One of the two parameters, this parameter or BackupId, must be selected.</div><br> |
|NodeInfo |Array of [NodeInfoObject](https://docs.byteplus.com/en/docs/61/15718#nodeinfoobject) |Yes |Refer to the request example. |Instance specification configuration. There is exactly one primary node and one secondary node, with 0 to 10 optional read\-only nodes. |
|StorageType |String |Yes |LocalSSD |Instance storage type. Fixed value `LocalSSD` (local SSD disk). |
|StorageSpace |Integer |No |100 |Instance storage space Unit is GB, with a step size of 10 GB.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">Different specifications have different storage space value ranges. For detailed information on storage space value ranges, refer to <a href="https://docs.byteplus.com/en/docs/RDS_for_PG/product_specifications?lang=zh">Product specifications</a>.</div><br> |
|VpcId |String |Yes |vpc\-2gdgzrrl5icjk50ztyz6b\*\*\*\* |Use this parameter to specify the virtual private cloud used by the instance.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="default">If you use ECS to connect to the PostgreSQL instance, the virtual private cloud must be the same as that of the ECS instance. Otherwise, the ECS instance cannot connect to the PostgreSQL instance through the private network.</div><br><br><br>* <div data-tips="true" data-tips-type="default">You can call the <a href="https://docs.byteplus.com/en/docs/vpc/DescribeVpcs">DescribeVpcs</a> API to query available virtual private clouds.</div><br><br><br>* <div data-tips="true" data-tips-type="default">You can call the <a href="https://docs.byteplus.com/en/docs/vpc/CreateVpc">CreateVpc</a> API to create a new virtual private cloud.</div><br> |
|SubnetId |String |Yes |subnet\-30uhx4w39n75s7r2qr0lq\*\*\*\* |Subnet ID.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="default">Only subnets in the availability zone where the instance is located can be selected.</div><br><br><br>* <div data-tips="true" data-tips-type="default">You can call the <a href="https://docs.byteplus.com/en/docs/vpc/DescribeSubnets">DescribeSubnets</a> API to query all subnet information within the specified virtual private cloud and availability zone.</div><br><br><br>* <div data-tips="true" data-tips-type="default">You can call the <a href="https://docs.byteplus.com/en/docs/vpc/CreateSubnet">CreateSubnet</a> API to create a new subnet.</div><br> |
|InstanceName |String |No |Name123 |Storage type. Rules:<br><br><br>* It cannot start with a digit or hyphen.<br><br>* It can only contain Chinese characters, letters, digits, underscores, and hyphens.<br><br>* The length must be between 1 and 128 characters. |
|ProjectName |String |No |Test |Affiliated project. If this parameter is left empty, the new instance will be added to the default project by default. |
|Tags |Array of [TagObject](https://docs.byteplus.com/en/docs/61/15718#tagobject) |No |Refer to the request example. |Array of tag objects.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">Supports input of multiple sets of tag key\-value objects at once. Up to 20 sets of tag key\-value pairs can be input simultaneously per submission, and up to 50 tags can be bound to a single instance.</div><br> |
|ChargeInfo |Object of [ChargeInfoObject](https://docs.byteplus.com/en/docs/61/15718#chargeinfoobject) |Yes |{<br><br>"ChargeType": "PostPaid"<br><br>} |Payment method. |
|AllowListIds |Array of String |No |[<br><br>"acl\-fdd6293f300143f2a4932bb483c8\*\*\*\*",<br><br>"acl\-ded4c0b707e44efd8f0dbc4e88f5\*\*\*\*"<br><br>] |Allowlist ID. To associate multiple allowlists, separate the allowlist IDs with a comma (,). An instance can associate up to 100 allowlists. |
|MaintenanceWindow |Object of [MaintenanceWindowObject](https://docs.byteplus.com/en/docs/61/15718#maintenancewindowobject) |No |Refer to the request example. |Details of the instance maintenance window. |


<span id="nodeinfoobject"></span>
### NodeInfoObject


|**Parameter** |**Type** |**Required?**  |**Example** |**Description** |
|---|---|---|---|---|
|NodeId |String |No |postgres\-ca7b7019\*\*\*\* |Node ID. You can call the [DescribeDBInstanceDetail](https://docs.byteplus.com/en/docs/RDS_for_PG/describedbinstancedetail) API to query.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">Required when modifying node specification and deleting nodes (ModifyDBInstancesSpec).</div><br> |
|ZoneId |String |Yes |cn\-beijing\-a |The availability zone where the node is located. You can call the [DescribeAvailabilityZones](https://docs.byteplus.com/en/docs/RDS_for_PG/describeavailabilityzones) API to query it.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="default">Required when creating an instance (CreateDBInstance), restoring to a new instance (RestoreToNewInstance), and adding or modifying nodes (ModifyDBInstancesSpec).</div><br><br><br>* <div data-tips="true" data-tips-type="default">Primary, secondary, and read\-only nodes can be deployed in different availability zones within the same region.</div><br> |
|NodeType |String |Yes |Primary |Node type, with values:<br><br><br>* `Primary`: Primary node.<br><br>* `Secondary`: indicates the secondary node.<br><br>* `ReadOnly`: Read\-only node. |
|NodeSpec |String |Yes |rds.postgres.1c2g |Node specification. Query specifications available for sale via [DescribeDBInstanceSpecs](https://docs.byteplus.com/en/docs/RDS_for_PG/describedbinstancespecs) API. |
|NodeOperateType |String |No |Create |Operation type. Range:<br><br><br>* `Create`: add.<br><br>* `Delete`: delete.<br><br>* `Modify`: modify.<br><br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="default">In the CreateDBInstance and RestoreToNewInstance APIs, this field can only be set to <code>Create</code>.</div><br><br><br>* <div data-tips="true" data-tips-type="default">When modifying instance configuration, the specified NodeOperateType must be passed in for the involved nodes.</div><br> |


<span id="tagobject"></span>
### TagObject


|**Parameter** |**Type** |**Required?**  |**Example** |**Description** |
|---|---|---|---|---|
|Key |String |Yes |abc |Tag key. Naming rules are as follows:<br><br><br>* It cannot start with any case\-insensitive variation of the prefix `volc:`. `volc:` is a system\-reserved tag key and is forbidden to use.<br><br>* It can only contain language characters, numbers, spaces, and English symbols (`_`, `.`, `:`, `/`, `=`, `+`, `-`, and `@`).<br><br>* The length must be between 1 and 128 characters.<br><br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="default">The number of tags created at one time cannot exceed 20.</div><br><br><br>* <div data-tips="true" data-tips-type="default">Tag keys cannot be duplicated under a single instance.</div><br> |
|Value |String |No |3 |Tag value. The naming rules are as follows:<br><br><br>* It can only contain language characters, numbers, spaces, and English symbols (`_`, `.`, `:`, `/`, `=`, `+`, `-`, and `@`).<br><br>* Nullable. Length must be between 0 and 256 characters. |


<span id="chargeinfoobject"></span>
### ChargeInfoObject


|**Parameter** |**Type** |**Required?**  |**Example** |**Description** |
|---|---|---|---|---|
|ChargeType |String |Yes |PostPaid |Payment type. Values:<br><br><br>* `PostPaid`: pay\-as\-you\-go.<br><br>* `PrePaid`: subscription (default). |
|AutoRenew |Boolean |No |true |Is automatic renewal enabled for the prepaid scenario?<br><br><br>* `yes`: automatic renewal.<br><br>* `false`: no automatic renewal (default). |
|PeriodUnit |String |No |Month |Purchase period for prepaid scenarios.<br><br><br>* `Month`: monthly (default).<br><br>* `Year`: subscription. |
|Period |Integer |No |1 |Subscription duration in a prepaid scenario. default value: 1. |
|Number |Integer |No |1 |Instance purchase quantity. Acceptable integer values range from 1 to 20, with a default of 1.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">When ChargeInfoObject is referenced by the RestoreToNewInstance API, Number can only be set to 1.</div><br> |


<span id="maintenancewindowobject"></span>
### MaintenanceWindowObject


|**Parameter** |**Type** |**Required?**  |**Example** |**Description** |
|---|---|---|---|---|
|DayKind |String |Yes |Week |The granularity of the maintenance cycle, with values of `Week`. |
|DayOfWeekMaintenanceTime |Array of [DayOfWeekObject](https://docs.byteplus.com/en/docs/61/15718#dayofweekobject) |No |Refer to the sample. |Details of the instance maintenance window. |


<span id="dayofweekobject"></span>
### DayOfWeekObject


|**Parameter** |**Type** |**Required?**  |**Example** |**Description** |
|---|---|---|---|---|
|DayOfWeek |String |Yes |Monday,Tuesday |Specify the maintainable day for the instance each week. Multiple selections allowed.<br><br><br>* `Monday`: Monday.<br><br>* `Tuesday`: Tuesday.<br><br>* `Wednesday`: Wednesday.<br><br>* `Thursday`: Thursday.<br><br>* `Friday`: Friday.<br><br>* `Saturday`: Saturday.<br><br>* `Sunday`: Sunday.<br><br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">If this value is not specified or empty, it defaults to all seven days of the week.</div><br> |
|MaintenanceWindowStartTime |String |Yes |22:00Z |The instance's start time within the maintenance window on the maintainable day. Format: HH:mmZ (UTC time).<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">Currently, only start times between 16:00Z and 20:00Z are supported for the maintenance window.</div><br> |
|Period |Integer |Yes |6 |Duration of the instance's maintenance window on a maintainable day.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">The duration is at least 2 hours and at most 6 hours.</div><br> |


<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters


|**Parameter** |**Type** |**Example** |**Description** |
|---|---|---|---|
|InstanceId |String |postgres\-21a3333b\*\*\*\* |Instance ID. |
|OrderId |String |Order71220115095297\*\*\*\* |Order ID. |


<span id=".56S65L6L"></span>
## Sample

<span id=".6K-35rGC56S65L6L"></span>
### Sample request

```json
POST /?Action=RestoreToNewInstance&Version=2022-01-01 HTTP/1.1
Content-Type: application/json
Host: rds-postgresql.cn-beijing.byteplusapi.com.cn
X-Date: 20231002T101010Z
Authorization: HMAC-SHA256 Credential=AKLTN2I0MmFiNzMxNWE5NDgzMzk4MmVjMTVkODlkZTZ****/20211202/cn-beijing/rds_postgresql/request,SignedHeaders=x-date, Signature=71d31fc7bcf990142851c9833c5656391486cda0ae2e0b8ada733b7c6458****
{
    "SrcInstanceId": "postgres-ca7b7019****",
    "NodeInfo": [
        {
            "ZoneId": "cn-beijing-a",
            "NodeSpec": "rds.postgres.1c2g",
            "NodeType": "Primary",
            "NodeOperateType": "Create"
        },
        {
            "ZoneId": "cn-beijing-a",
            "NodeSpec": "rds.postgres.1c2g",
            "NodeType": "Secondary",
            "NodeOperateType": "Create"
        }
    ],
    "BackupId": "20230801-170****",
    "StorageType": "LocalSSD",
    "StorageSpace": 20,
    "VpcId": "vpc-2gdgzrrl5icjk50ztyz6b****",
    "SubnetId": "subnet-30uhx4w39n75s7r2qr0lq****",
    "InstanceName": "测试实例",
    "ChargeInfo": {
        "ChargeType": "PostPaid",
        "Number": 1
    },
    "ProjectName": "default",
    "Tags": [
        {
            "Key": "Key",
            "Value": "Value"
        }
    ],
    "MaintenanceWindow": {
        "DayKind": "Week",
        "DayOfWeekMaintenanceTime": [
            {
                "Period": 6,
                "DayOfWeek": "Monday,Tuesday",
                "MaintenanceWindowStartTime": "16:00Z"
            }
        ]
    }
}
```


<span id=".6L-U5Zue56S65L6L"></span>
### Sample response

```json
{
    "ResponseMetadata": {
        "RequestId": "20230801173634010212035227001977AC",
        "Action": "RestoreToNewInstance",
        "Version": "2022-01-01",
        "Service": "rds_postgresql",
        "Region": "cn-beijing"
    },
    "Result": {
        "InstanceId": "postgres-21a3333b****",
        "OrderId": "Order71220115095297****"
    }
}
```
