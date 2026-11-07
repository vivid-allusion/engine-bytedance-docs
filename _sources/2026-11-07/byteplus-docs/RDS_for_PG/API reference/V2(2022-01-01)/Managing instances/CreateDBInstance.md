---
title: "CreateDBInstance"
product: "RDS for PostgreSQL"
product_code: "RDS_for_PG"
source: "https://docs.byteplus.com/en/docs/RDS_for_PG/CreateDBInstance"
---

## Request type

Asynchronous request.

## Request parameters

|**Parameter** |**Type** |**Required?**  |**Example** |**Description** |
|---|---|---|---|---|
|DBEngineVersion |String |Yes |PostgreSQL_12 |Compatible version. Values:<br><br><br>* `PostgreSQL_11`: PostgreSQL 11.<br><br>* `PostgreSQL_12`: PostgreSQL 12.<br><br>* `PostgreSQL_13`: PostgreSQL 13.<br><br>* `PostgreSQL_14`: PostgreSQL 14.<br><br>* `PostgreSQL_15`: PostgreSQL 15.<br><br>* `PostgreSQL_16`: PostgreSQL 16.<br><br>* `PostgreSQL_17`: PostgreSQL 17.<br><br>* `PostgreSQL_18`：PostgreSQL 18.<br><br><br>> **tip**<br><br><br>> If you need to enable TDE encryption, only **PostgreSQL 17** is supported.<br> |
|NodeInfo |Array of [NodeInfoObject](https://docs.byteplus.com/en/docs/61/15763#nodeinfoobject) |Yes |Refer to the request example. |Instance specification configuration. There is exactly one primary node and one secondary node, with 0 to 10 optional read\-only nodes. |
|StorageType |String |Yes |LocalSSD |Instance storage type. Fixed value `LocalSSD` (local SSD disk). |
|StorageSpace |Integer |No |100 |Instance storage space<br><br>> **tip**<br><br><br>> Different specifications have different storage space value ranges. For detailed information on storage space value ranges, refer to [Product specifications](https://docs.byteplus.com/en/docs/RDS_for_PG/product_specifications?lang=en). Unit in GB, step size of 10 GB.<br> |
|VpcId |String |Yes |vpc\-2gdgzrrl5icjk50ztyz6b\*\*\*\* |Use this parameter to specify the virtual private cloud used by the instance.<br><br>> **tip**<br><br><br><br>* > If you use ECS to connect to the PostgreSQL instance, the virtual private cloud must be the same as that of the ECS instance. Otherwise, the ECS instance cannot connect to the PostgreSQL instance through the private network.<br><br><br>* > You can call the [DescribeVpcs](https://docs.byteplus.com/en/docs/vpc/DescribeVpcs) API to query available virtual private clouds.<br><br><br>* > You can call the [CreateVpc](https://docs.byteplus.com/en/docs/vpc/CreateVpc) API to create a new virtual private cloud.<br> |
|SubnetId |String |Yes |subnet\-30uhx4w39n75s7r2qr0lq\*\*\*\* |Subnet ID.<br><br>> **tip**<br><br><br><br>* > Only subnets in the availability zone where the instance is located can be selected.<br><br><br>* > You can call the [DescribeSubnets](https://docs.byteplus.com/en/docs/vpc/DescribeSubnets) API to query all subnet information within the specified virtual private cloud and availability zone.<br><br><br>* > You can call the [CreateSubnet](https://docs.byteplus.com/en/docs/vpc/CreateSubnet) API to create a new subnet.<br> |
|AllowListIds |Array of String |No |[<br><br>"acl\-fdd6293f300143f2a4932bb483c8\*\*\*\*",<br><br>"acl\-ded4c0b707e44efd8f0dbc4e88f5\*\*\*\*"<br><br>] |Allowlist ID. To associate multiple allowlists, separate the allowlist IDs with a comma (,). An instance can associate up to 100 allowlists. |
|InstanceName |String |No |Name123 |Instance name rules:<br><br><br>* It cannot start with a digit or hyphen.<br><br>* It can only contain Chinese characters, letters, digits, underscores (_) and hyphens (\-).<br><br>* Length must be between 1 and 128. |
|MaintenanceWindow |Object of [MaintenanceWindowObject](https://docs.byteplus.com/en/docs/61/15763#maintenancewindowobject) |No |Refer to the request example. |The maintenance window for the instance. |
|ProjectName |String |No |Test |Affiliated project. The default value is the default project. |
|Tags |Array of [TagObject](https://docs.byteplus.com/en/docs/61/15763#tagobject) |No |[{<br><br>"Key": "test",<br><br>"Value": "123"<br><br>}] |Array of tag objects.<br><br>> **tip**<br><br><br>> Supports passing multiple sets of tag key\-value objects at once, separated by commas (,). Each time, you can pass up to 20 sets of tag key\-value pairs simultaneously, and each instance can bind up to 50 tags.<br> |
|ChargeInfo |Object of [ChargeInfoObject](https://docs.byteplus.com/en/docs/61/15763#chargeinfoobject) |Yes |{<br><br>"ChargeType": "PostPaid"<br><br>} |Payment method. |
|TDEEnable |Boolean |No |true |Enable TDE encryption? Values:<br><br><br>* `true`: enable TDE encryption.<br><br>* `false`: disable TDE encryption (default).<br><br><br>> **tip**<br><br><br><br>* > TDE encryption is currently in invitation\-only testing. To use it, [submit a ticket](https://console.byteplus.com/workorder/create).<br><br><br>* > TDE encryption cannot be disabled once enabled.<br> |
|KMSTrn |String |No |trn:kms:cn\-beijing:210xxxx:keyrings/testxxxx/keys/testxxxx |KMS key ring TRN. Format: `trn:kms:<region>:<account_id>:keyrings/<ring_name>/keys/<key_name>`.<br><br>> **tip**<br><br><br>> When `EnableTDE` is `true`, this parameter is required.<br> |

### NodeInfoObject

|**Parameter** |**Type** |**Required?**  |**Example** |**Description** |
|---|---|---|---|---|
|NodeId |String |No |postgres\-ca7b7019\*\*\*\* |Node ID. You can call the [DescribeDBInstanceDetail](https://docs.byteplus.com/en/docs/RDS_for_PG/describedbinstancedetail) API to query.<br><br>> **tip**<br><br><br>> Required when modifying node specification and deleting nodes (ModifyDBInstancesSpec).<br> |
|ZoneId |String |Yes |cn\-beijing\-a |The availability zone where the node is located. You can call the [DescribeAvailabilityZones](https://docs.byteplus.com/en/docs/RDS_for_PG/describeavailabilityzones) API to query it.<br><br>> **tip**<br><br><br><br>* > Required when creating an instance (CreateDBInstance), restoring to a new instance (RestoreToNewInstance), and adding or modifying nodes (ModifyDBInstancesSpec).<br><br><br>* > Primary, secondary, and read\-only nodes can be deployed in different availability zones within the same region.<br> |
|NodeType |String |Yes |Primary |Node type, with values:<br><br><br>* `Primary`: Primary node.<br><br>* `Secondary`: indicates the secondary node.<br><br>* `ReadOnly`: Read\-only node. |
|NodeSpec |String |Yes |rds.postgres.1c2g |Node specification. Query specifications available for sale via [DescribeDBInstanceSpecs](https://docs.byteplus.com/en/docs/RDS_for_PG/describedbinstancespecs) API. |
|NodeOperateType |String |No |Create |Operation type. Range:<br><br><br>* `Create`: add.<br><br>* `Delete`: delete.<br><br>* `Modify`: modify.<br><br><br>> **tip**<br><br><br><br>* > In the CreateDBInstance and RestoreToNewInstance APIs, this field can only be set to `Create`.<br><br><br>* > When modifying instance configuration, the specified NodeOperateType must be passed in for the involved nodes.<br> |

### MaintenanceWindowObject

|**Parameter** |**Type** |**Required?**  |**Example** |**Description** |
|---|---|---|---|---|
|DayKind |String |Yes |Week |The granularity of the maintenance cycle, with values of `Week`. |
|DayOfWeekMaintenanceTime |Array of [DayOfWeekObject](https://docs.byteplus.com/en/docs/61/15763#dayofweekobject) |No |Refer to the sample. |Details of the instance maintenance window. |

### DayOfWeekObject

|**Parameter** |**Type** |**Required?**  |**Example** |**Description** |
|---|---|---|---|---|
|DayOfWeek |String |Yes |Monday,Tuesday |Specify the maintainable day for the instance each week. Multiple selections allowed.<br><br><br>* `Monday`: Monday.<br><br>* `Tuesday`: Tuesday.<br><br>* `Wednesday`: Wednesday.<br><br>* `Thursday`: Thursday.<br><br>* `Friday`: Friday.<br><br>* `Saturday`: Saturday.<br><br>* `Sunday`: Sunday.<br><br><br>> **tip**<br><br><br>> If this value is not specified or empty, it defaults to all seven days of the week.<br> |
|MaintenanceWindowStartTime |String |Yes |22:00Z |The instance's start time within the maintenance window on the maintainable day. Format: HH:mmZ (UTC time).<br><br>> **tip**<br><br><br>> Currently, only start times between 16:00Z and 20:00Z are supported for the maintenance window.<br> |
|Period |Integer |Yes |6 |Duration of the instance's maintenance window on a maintainable day.<br><br>> **tip**<br><br><br>> The duration is at least 2 hours and at most 6 hours.<br> |

### TagObject

|**Parameter** |**Type** |**Required?**  |**Example** |**Description** |
|---|---|---|---|---|
|Key |String |Yes |abc |Tag key. Naming rules are as follows:<br><br><br>* It cannot start with any case\-insensitive variation of the prefix `volc:`. `volc:` is a system\-reserved tag key and is forbidden to use.<br><br>* It can only contain language characters, numbers, spaces, and English symbols (`_`, `.`, `:`, `/`, `=`, `+`, `-`, and `@`).<br><br>* The length must be between 1 and 128 characters.<br><br><br>> **tip**<br><br><br><br>* > The number of tags created at one time cannot exceed 20.<br><br><br>* > Tag keys cannot be duplicated under a single instance.<br> |
|Value |String |No |3 |Tag value. The naming rules are as follows:<br><br><br>* It can only contain language characters, numbers, spaces, and English symbols (`_`, `.`, `:`, `/`, `=`, `+`, `-`, and `@`).<br><br>* Nullable. Length must be between 0 and 256 characters. |

### ChargeInfoObject

|**Parameter** |**Type** |**Required?**  |**Example** |**Description** |
|---|---|---|---|---|
|ChargeType |String |Yes |PostPaid |Payment type. Values:<br><br><br>* `PostPaid`: pay\-as\-you\-go.<br><br>* `PrePaid`: subscription (default). |
|AutoRenew |Boolean |No |true |Is automatic renewal enabled for the prepaid scenario?<br><br><br>* `yes`: automatic renewal.<br><br>* `false`: no automatic renewal (default). |
|PeriodUnit |String |No |Month |Purchase period for prepaid scenarios.<br><br><br>* `Month`: monthly (default).<br><br>* `Year`: subscription. |
|Period |Integer |No |1 |Subscription duration in a prepaid scenario. default value: 1. |
|Number |Integer |No |1 |Instance purchase quantity. Acceptable integer values range from 1 to 20, with a default of 1.<br><br>> **tip**<br><br><br>> When ChargeInfoObject is referenced by the RestoreToNewInstance API, Number can only be set to 1.<br> |

## Response parameters

|**Parameter** |**Type** |**Example** |**Description** |
|---|---|---|---|
|InstanceId |String |postgres\-21a3333b\*\*\*\* |Instance ID. |
|OrderId |String |Order634971667632428\*\*\*\* |Order ID. |

## Example

### Sample request

```json
POST /?Action=CreateDBInstance&Version=2022-01-01 HTTP/1.1
Content-Type: application/json
Host: rds-postgresql.cn-beijing.byteplusapi.com.cn
X-Date: 20231002T101010Z
Authorization: HMAC-SHA256 Credential=AKLTN2I0MmFiNzMxNWE5NDgzMzk4MmVjMTVkODlkZTZ****/20211202/cn-beijing/rds_postgresql/request,SignedHeaders=x-date, Signature=71d31fc7bcf990142851c9833c5656391486cda0ae2e0b8ada733b7c6458****
{
    "DBEngineVersion": "PostgreSQL_12",
    "StorageType": "LocalSSD",
    "StorageSpace": 20,
    "VpcId": "vpc-2gdgzrrl5icjk50ztyz6b****",
    "InstanceName": "Name123",
    "ChargeInfo": {
        "ChargeType": "PostPaid",
        "Number": 1
    },
    "ProjectName": "default",
    "SubnetId": "subnet-30uhx4w39n75s7r2qr0lq****",
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
    "Tags": [
        {
            "Key": "test",
            "Value": "123"
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

### Sample response

```json
{
    "ResponseMetadata": {
        "RequestId": "20230801104043BEB227FB89B5F73A1436",
        "Action": "CreateDBInstance",
        "Version": "2022-01-01",
        "Service": "rds_postgresql",
        "Region": "cn-beijing"
    },
    "Result": {
        "InstanceId": "postgres-21a3333b****",
        "OrderId": "Order634971667632428****"
    }
}
```
