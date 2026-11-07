---
title: "RestoreToNewInstance"
product: "NDB for mysql"
product_code: "NDB_for_MySQL"
source: "https://docs.byteplus.com/en/docs/NDB_for_MySQL/RestoreToNewInstance"
---

Call the RestoreToNewInstance to restore the backup data of an existing instance to a new instance.

<span id=".6K-35rGC57G75Z6L"></span>
## Request type

Asynchronous request.

<span id=".6LCD6K-V"></span>
## Debug

[去调试](https://api.byteplus.com/api-explorer/debug?action=RestoreToNewInstance&serviceCode=vedbm&version=2022-01-01&groupName=)


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters


|**Name** |**Type** |**Required** |**Example** |**Description** |
|---|---|---|---|---|
|SrcInstanceId |String |Yes |vedbm\-h441603c68aaa\*\*\*\* |The ID of the original instance to which the backup file belongs.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">You can call the <a href="https://docs.byteplus.com/en/docs/NDB_for_MySQL/DescribeDBInstances">DescribeDBInstances</a> API to query the Instance ID.</div><br> |
|BackupId |String |No |snap\-64b7\*\*\*\*\-5935 |The ID of the backup file from the original instance. A new instance is created using the data stored in this backup file.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="default">Either this parameter or the RestoreTime parameter is required.</div><br><br><br>* <div data-tips="true" data-tips-type="default">You can call <a href="https://docs.byteplus.com/en/docs/NDB_for_MySQL/DescribeBackups">DescribeBackups</a> to query the list of backup files for a specified instance.</div><br> |
|RestoreTime |String |No |2023\-07\-14T15:47:10Z |Any point in time within the log backup retention period of the original instance, in yyyy\-MM\-ddTHH:mm:ssZ format (UTC time).<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="default">You must specify either this parameter or the BackupId parameter.</div><br><br><br>* <div data-tips="true" data-tips-type="default">You can call <a href="https://docs.byteplus.com/en/docs/NDB_for_MySQL/DescribeRecoverableTime">DescribeRecoverableTime</a> to query the recoverable time range for the specified instance.</div><br> |
|InstanceName |String |No |Name123 |Instance name. Naming rules:<br><br><br>* It cannot start with a number or hyphen (\-).<br><br>* It can only contain Chinese characters, letters, digits, underscores (_), and hyphens (\-).<br><br>* The length must be between 1 and 128 characters. |
|DBMinorVersion |String |No |3.0 |* When the compatible version of the source instance is `MySQL_5_7`, this parameter value defaults to `2.0`.<br><br>* When the compatible version of the source instance is `MySQL_8_0`, the parameter value defaults to `3.0`.<br><br><br> |
|NodeSpec |String |Yes |vedb.mysql.x4.large |The specification code of the instance. For more information, refer to [Product specifications](https://docs.byteplus.com/en/docs/NDB_for_MySQL/Product_specifications). |
|NodeNumber |Integer |Yes |2 |Number of nodes. The value range is 2 to 16. |
|ZoneIds |String |Yes |cn\-beijing\-a |Availability zone ID.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">You can call the <a href="https://docs.byteplus.com/en/docs/NDB_for_MySQL/DescribeAvailabilityZones">DescribeAvailabilityZones</a> API to query the availability zones supported by the instance.</div><br> |
|VpcId |String |Yes |vpc\-3ajzohyfaru9s340jz1rp\*\*\*\* |Virtual private cloud (VPC) ID.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">You can call the <a href="https://docs.byteplus.com/en/docs/vpc/DescribeVpcs">DescribeVpcs</a> API to query the VPC ID needed to create an instance.</div><br> |
|SubnetId |String |Yes |subnet\-1g15j13jtzgu88ibuxwqp\*\*\*\* |Subnet ID. The subnet must belong to the selected availability zone.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="default">A subnet is an IP address block within a VPC. All cloud resources in the VPC must be deployed within a subnet. The subnet allocates private IP addresses to cloud resources.</div><br><br><br>* <div data-tips="true" data-tips-type="default">You can call <a href="https://docs.byteplus.com/en/docs/vpc/CreateSubnet">CreateSubnet</a> to create a subnet, and call <a href="https://docs.byteplus.com/en/docs/vpc/DescribeSubnets">DescribeSubnets</a> to query the list of all subnets and their IDs in a specified availability zone.</div><br> |
|Port |Integer |No |3306 |Specifies the private port number for the connection endpoint that the instance creates by default. The default value is 3306, and the range is 1000 to 65534.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="default">This configuration item is only valid for <strong>Primary node endpoint</strong>, and <strong>Default endpoint</strong>. That is, after the instance is successfully created, the newly created custom endpoint, the port number still defaults to 3306.</div><br><br><br>* <div data-tips="true" data-tips-type="default">After the instance is successfully created, you can also modify the port number at any time. For activity details, see <a href="https://docs.byteplus.com/en/docs/NDB_for_MySQL/Modifying_address_prefix_and_port">Modifying address prefix and port</a>.</div><br> |
|ProjectName |String |No |default |The name of the project to which the instance belongs. If this parameter is left empty, the new instance is added to the `default` project. |
|SrcProjectName |String |No |default |The name of the Project to which the original instance backup file belongs. |
|Tags |Array of [TagObject](https://docs.byteplus.com/en/docs/265/57391#tagobject) |No |See the request example. |An array object of tag keys and tag values to be bound.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="default">It supports passing in multiple sets of tag key\-value objects at once, separated by commas (,). A single request supports up to 20 tag key\-value pairs, and a single instance can be bound with a maximum of 50 tags.</div><br><br><br>* <div data-tips="true" data-tips-type="default">The tag key value must meet certain setting rules. For details, please refer to the <a href="https://docs.byteplus.com/en/docs/NDB_for_MySQL/Tag_overview#.5qCH562-6K6-572u6KeE5YiZ">Tag setting rules</a>.</div><br> |
|DeletionProtection |String |No |disabled |Enable or disable the instance deletion protection function. Valid values:<br><br><br>* `enabled`: Enable.<br><br>* `disabled`: Disable (default).<br><br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">Once turned on, the instance cannot be deleted. To delete an instance, you need to call the ModifyDBInstanceDeletionProtectionPolicy interface to disable the function first. For more information about removal protection, see <a href="https://docs.byteplus.com/en/docs/NDB_for_MySQL/Instance_deletion_protection">Instance deletion protection</a>.</div><br> |
|StorageType |String |String |IOOptimizedStorage |Storage type. Value range:<br><br><br>* `IOOptimizedStorage`: IO performance type (default).<br><br>* `SmartCompressedStorage`: Intelligent compression type.<br><br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="default">For details about the two storage types and their price differences, refer to <a href="https://docs.byteplus.com/en/docs/NDB_for_MySQL/Storage#hGEe8xbZ">Storage type comparison</a>.</div><br><br><br>* <div data-tips="true" data-tips-type="default">Supports upgrading the storage type from smart compression storage to IO performance storage. For more information, refer to <a href="https://docs.byteplus.com/en/docs/NDB_for_MySQL/ModifyDBInstanceStorageType">ModifyDBInstanceStorageType</a>.</div><br><br><br><br> |
|ChargeType |String |Yes |PostPaid |Calculate billing type, which is the same as that of the original instance by default. The values are as follows:<br><br><br>* `PostPaid`: Pay\-as\-you\-go.<br><br>* `PrePaid`: Yearly or monthly subscription. |
|StorageChargeType |String |No |PostPaid |The storage billing type is the same as the original instance by default. If this parameter is not specified, the storage billing type is the same as the calculate billing type by default. The valid values are as follows:<br><br><br>* `PostPaid`: Pay\-as\-you\-go.<br><br>* `PrePaid`: Yearly or monthly subscription.<br><br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="default">When the calculate billing type is <code>PostPaid</code>, the storage billing type can only be <code>PostPaid</code>.</div><br><br><br>* <div data-tips="true" data-tips-type="default">When the calculate billing type is <code>PrePaid</code>, the storage billing type can be <code>PrePaid</code> or <code>PostPaid</code>.</div><br> |
|AutoRenew |Boolean |No |false |Specifies whether to enable Due Automatic renewal for prepaid instances. Value:<br><br><br>* `true`: enables auto\-renewal.<br><br>* `false`: no automatic renewal.<br><br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">This parameter is required when <code>ChargeType</code> (Billing method) is set to <code>PrePaid</code> (Subscription).</div><br> |
|PeriodUnit |String |No |Month |The prepaid purchase duration.<br><br><br>* `Month`: Monthly subscription.<br><br>* `Year`: Yearly subscription.<br><br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">This parameter is required when <code>ChargeType</code> (Billing method) is set to <code>PrePaid</code> (Subscription).</div><br> |
|Period |Integer |No |1 |The purchase duration for a subscription.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">This parameter is required when <code>ChargeType</code> (Billing method) is set to <code>PrePaid</code> (Subscription).</div><br> |
|PrePaidStorageInGB |Integer |No |50 |The storage space size in a subscription scenario.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">This parameter is required when <code>ChargeType</code> (Billing method) is set to <code>PrePaid</code> (Subscription).</div><br> |


<span id="tagobject"></span>
### TagObject


|**Name** |**Type** |**Required** |**Example** |**Description** |
|---|---|---|---|---|
|Key |String |Yes |department |Tag key bound to the instance. |
|Value |String |No |game |Tag value bound to the instance. |


<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameter


|**Name** |**Type** |**Example** |**Description** |
|---|---|---|---|
|InstanceId |String |vedbm\-h441603c68aaa\*\*\*\* |Instance ID. |
|OrderId |String |Order707643373078888\*\*\*\* |Order ID. |


<span id=".56S65L6L"></span>
## Example

<span id=".6K-35rGC56S65L6L"></span>
### Request example

```JSON
POST /?Action=RestoreToNewInstance&Version=2022-01-01 HTTP/1.1
Content-Type: application/json
Host:vedbm.cn-beijing.byteplusapi.com.cn
X-Date: 20220101T101010Z
Authorization: HMAC-SHA256 Credential=AKLTN2I0MmFiNzMxNWE5NDgzMzk4MmVjMTVkODlkZTZ****/20220101/cn-beijing/vedbm/request,SignedHeaders=x-date, Signature=71d31fc7bcf990142851c9833c5656391486cda0ae2e0b8ada733b7c645****
{
    "ZoneIds": "cn-beijing-b",
    "NodeSpec": "vedb.mysql.x4.large",
    "NodeNumber": 2,
    "SrcInstanceId": "vedbm-gzwdsf9b****",
    "VpcId": "vpc-13fz0iip9nlds3n6nu4fi****",
    "SubnetId": "subnet-13fz1bsbrsw743n6nu47c****",
    "ProjectName": "default",
    "ChargeType": "PostPaid",
    "BackupId": "snap-64b7****-5935",
    "Tags": [
        {
            "Key": "chargetype",
            "Value": "prepaid"
        }
    ],
    "InstanceName": "Name123"
}
```


<span id=".6L-U5Zue56S65L6L"></span>
### Response example

```JSON
{
    "ResponseMetadata": {
        "RequestId": "202307192136280102090801470751B90C",
        "Action": "RestoreToNewInstance",
        "Version": "2022-01-01",
        "Service": "vedbm",
        "Region": "cn-beijing"
    },
    "Result": {
        "InstanceId": "vedbm-d4mx2akm****",
        "OrderId": "Order707643373078888****"
    }
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error code

For details, refer to [Error codes](https://docs.byteplus.com/en/docs/NDB_for_MySQL/Error_codes).
