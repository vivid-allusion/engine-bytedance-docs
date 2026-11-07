---
title: "CreateDBInstance"
product: "NDB for mysql"
product_code: "NDB_for_MySQL"
source: "https://docs.byteplus.com/en/docs/NDB_for_MySQL/CreateDBInstance"
---

Call the CreateDBInstance to create a new instance.

<span id=".6K-35rGC57G75Z6L"></span>
## Request type

Asynchronous request.

<span id=".6LCD6K-V"></span>
## Debug

[去调试](https://api.byteplus.com/api-explorer/debug?action=CreateDBInstance&serviceCode=vedbm&version=2022-01-01&groupName=)


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters


|**Name** |**Type** |**Required** |**Example** |**Description** |
|---|---|---|---|---|
|InstanceName |String |No |test |Instance name. Naming rules:<br><br><br>* It cannot start with a number or hyphen (\-).<br><br>* It can only contain Chinese characters, letters, digits, underscores (_), and hyphens (\-).<br><br>* The length must be between 1 and 128 characters.<br><br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="default">If left blank, the instance ID will be used as the instance name by default.</div><br><br><br>* <div data-tips="true" data-tips-type="default">If an instance name is provided when creating instances in a batch, a serial number is automatically appended to the name.</div><br> |
|DBEngineVersion |String |Yes |MySQL_8_0 |The compatible version of the instance. Value range:<br><br><br>* `MySQL_8_0`: Compatible with MySQL version 8.0.<br><br>* `MySQL_5_7`: Compatible with MySQL version 5.7.<br><br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="default">See the <a href="https://docs.byteplus.com/en/docs/NDB_for_MySQL/Features_overview">Feature overview</a> for differences in functionality supported by different version instances.</div><br><br><br>* <div data-tips="true" data-tips-type="default">MySQL 5.7 is currently invite\-only features. If you need to use it, please <a href="https://console.byteplus.com/workorder/create">submit a ticket</a> to contact technical support.</div><br> |
|DBMinorVersion |String |No |3.0 |* When `DBEngineVersion` is set to `MySQL_5_7`, this parameter defaults to `2.0`.<br><br>* When `DBEngineVersion` is set to `MySQL_8_0`, this parameter defaults to `3.0`. |
|NodeSpec |String |Yes |vedb.mysql.x4.xlarge |The node specification code for the instance.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">For detailed information on instance node specifications, refer to <a href="https://docs.byteplus.com/en/docs/NDB_for_MySQL/Product_specifications">Product specifications</a>.</div><br> |
|ZoneIds |String |Yes |cn\-beijing\-b |Availability zone ID.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">Call the <a href="https://docs.byteplus.com/en/docs/NDB_for_MySQL/DescribeAvailabilityZones">DescribeAvailabilityZones</a> API to query the availability zone resources supported by the instance.</div><br> |
|NodeNumber |Integer |Yes |2 |Number of instance nodes. The value range is 2 to 16. |
|VpcId |String |Yes |vpc\-3ajzohyfaru9s340jz1rp\*\*\*\* |Virtual private cloud (VPC) ID.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">You can call the <a href="https://docs.byteplus.com/en/docs/vpc/DescribeVpcs">DescribeVpcs</a> API to query the VPC ID needed to create an instance.</div><br> |
|SubnetId |String |Yes |subnet\-1g15j13jtzgu88ibuxwqp\*\*\*\* |Subnet ID. The subnet must belong to the selected availability zone.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="default">A subnet is an IP address block within a VPC. All cloud resources in the VPC must be deployed within a subnet. The subnet allocates private IP addresses to cloud resources.</div><br><br><br>* <div data-tips="true" data-tips-type="default">You can call <a href="https://docs.byteplus.com/en/docs/vpc/CreateSubnet">CreateSubnet</a> to create a subnet, and call <a href="https://docs.byteplus.com/en/docs/vpc/DescribeSubnets">DescribeSubnets</a> to query the list of all subnets and their IDs in a specified availability zone.</div><br> |
|Port |Integer |No |3306 |Specifies the private port number for the connection endpoint that the instance creates by default. The default value is 3306, and the range is 1000 to 65534.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="default">This configuration item is only valid for <strong>Primary node endpoint</strong>, and <strong>Default endpoint</strong>. That is, after the instance is successfully created, the newly created custom endpoint, the port number still defaults to 3306.</div><br><br><br>* <div data-tips="true" data-tips-type="default">After the instance is successfully created, you can also modify the port number at any time. For activity details, see <a href="https://docs.byteplus.com/en/docs/NDB_for_MySQL/Modifying_address_prefix_and_port">Modifying address prefix and port</a>.</div><br> |
|SuperAccountName |String |No |vedbuser |Account name for the super user. The account name must meet the following requirements:<br><br><br>* The name must be unique and 2 to 32 characters in length.<br><br>* It must consist of letters, numbers, underscores (_) and hyphens (\-).<br><br>* The name must start with a letter and ends with a letter or a digit.<br><br>* The name cannot contain any forbidden keywords. For more details, refer to [List of forbidden keywords](https://docs.byteplus.com/en/docs/NDB_for_MySQL/List_of_forbidden_keywords).<br><br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">You can call the <a href="https://docs.byteplus.com/en/docs/NDB_for_MySQL/CreateDBAccount">CreateDBAccount</a> interface to create a super account or a normal account for an instance after it is created successfully.</div><br> |
|SuperAccountPassword |String |No |kira\*\*\*\* |Password for the super account. The account password must meet the following requirements:<br><br><br>* Can only contain uppercase and lowercase letters, digits, and special characters (such as `~!@#$%^&*_-+=`\|\(){}[]:;'<>,.?/`).<br><br>* The length must be between 8 and 32 characters.<br><br>* Must contain at least three of the following character types: uppercase letters, lowercase letters, digits, and specific special characters. |
|DBTimeZone |String |No |UTC +08:00 |The time zone of the instance. The default time zone for all regions in China is UTC + 08:00. |
|LowerCaseTableNames |String |No |1 |Specifies whether the table name is case sensitive. The default value is 1.<br><br>Value range:<br><br><br>* `0`: table names are stored as is and are case\-sensitive.<br><br>* `1`: (default) table names are stored in lowercase and are case\-insensitive.<br><br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">After creating an instance, it is not supported to modify this rule. Please set it reasonably according to business requirements.</div><br> |
|ProjectName |String |No |default |The name of the project to which the instance belongs. If this parameter is left empty, the new instance is added to the `default` project.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">A project is a virtual concept that includes a set of resources, users, and roles. A project allows you to view and manage a group of resources in a unified manner and control the permissions of users and roles to these resources. </div><br> |
|Tags |Array of [TagObject](https://docs.byteplus.com/en/docs/265/57342#tagobject) |No |See the request example. |An array object of tag keys and tag values to be bound.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="default">A single request supports up to 20 tag key\-value pairs, and a single instance can be bound with a maximum of 50 tags.</div><br><br><br>* <div data-tips="true" data-tips-type="default">The tag key value must meet certain setting rules. For details, please refer to the <a href="https://docs.byteplus.com/en/docs/NDB_for_MySQL/Tag_overview#.5qCH562-6K6-572u6KeE5YiZ">Tag setting rules</a>.</div><br> |
|DeletionProtection |String |No |disabled |Enable or disable the instance deletion protection function. Valid values:<br><br><br>* `enabled`: Enable.<br><br>* `disabled`: Disable (default).<br><br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">Once turned on, the instance cannot be deleted. To delete an instance, you need to call the ModifyDBInstanceDeletionProtectionPolicy interface to disable the function first. For more information about removal protection, see <a href="https://docs.byteplus.com/en/docs/NDB_for_MySQL/Instance_deletion_protection">Instance deletion protection</a>.</div><br> |
|StorageType |String |String |IOOptimizedStorage |Storage type. Value range:<br><br><br>* `IOOptimizedStorage`: IO performance type (default).<br><br>* `SmartCompressedStorage`: Intelligent compression type.<br><br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="default">For details about the two storage types and their price differences, refer to <a href="https://docs.byteplus.com/en/docs/NDB_for_MySQL/Storage#hGEe8xbZ">Storage type comparison</a>.</div><br><br><br>* <div data-tips="true" data-tips-type="default">Supports upgrading the storage type from smart compression storage to IO performance storage. For more information, refer to <a href="https://docs.byteplus.com/en/docs/NDB_for_MySQL/ModifyDBInstanceStorageType">ModifyDBInstanceStorageType</a>.</div><br><br><br><br> |
|ChargeType |String |Yes |PostPaid |Calculate billing type. The following values are available for Calculate billing type when you create an instance:<br><br><br>* `PostPaid`: Pay\-as\-you\-go.<br><br>* `PrePaid`: Yearly or monthly subscription. |
|StorageChargeType |String |No |PostPaid |Storage billing type. If this parameter is not specified, the storage billing type is the same as the calculate billing type by default. The valid values are as follows:<br><br><br>* `PostPaid`: Pay\-as\-you\-go.<br><br>* `PrePaid`: Yearly or monthly subscription.<br><br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="default">When the calculate billing type is <code>PostPaid</code>, the storage billing type can only be <code>PostPaid</code>.</div><br><br><br>* <div data-tips="true" data-tips-type="default">When the calculate billing type is <code>PrePaid</code>, the storage billing type can be <code>PrePaid</code> or <code>PostPaid</code>.</div><br> |
|AutoRenew |Boolean |No |false |Specifies whether to enable Due Automatic renewal for prepaid instances. Value:<br><br><br>* `true`: enables auto\-renewal.<br><br>* `false`: no automatic renewal.<br><br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">This parameter is required when <code>ChargeType</code> (Billing method) is set to <code>PrePaid</code> (Subscription).</div><br> |
|PeriodUnit |String |No |Month |The prepaid purchase duration.<br><br><br>* `Month`: Monthly subscription.<br><br>* `Year`: Yearly subscription.<br><br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">This parameter is required when <code>ChargeType</code> (Calculate billing type) is set to <code>PrePaid</code> (Subscription).</div><br> |
|Period |Integer |No |1 |The purchase duration for a subscription.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">This parameter is required when <code>ChargeType</code> (Calculate billing type) is set to <code>PrePaid</code> (Subscription).</div><br> |
|PrePaidStorageInGB |Integer |No |50 |The storage space size in a subscription scenario.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">This parameter is required when <code>StorageChargeType</code> (Storage billing type) is set to <code>PrePaid</code> (Subscription).</div><br> |
|Number |Integer |No |1 |The number of instances to create, ranging from 1 to 50. The default value is `1`. |


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
|InstanceId |String |vedbm\-d4mx2akm\*\*\*\* |Instance ID. |
|OrderId |String |Order707643373078888\*\*\*\* |Order ID. |


<span id=".56S65L6L"></span>
## Sample

<span id=".6K-35rGC56S65L6L"></span>
### Request example 1

Pay\-as\-you\-go instance.

```JSON
POST /?Action=CreateDBInstance&Version=2022-01-01 HTTP/1.1
Content-Type: application/json
Host:vedbm.cn-beijing.byteplusapi.com.cn
X-Date: 20220101T101010Z
Authorization: HMAC-SHA256 Credential=AKLTN2I0MmFiNzMxNWE5NDgzMzk4MmVjMTVkODlkZTZ****/20220101/cn-beijing/vedbm/request,SignedHeaders=x-date, Signature=71d31fc7bcf990142851c9833c5656391486cda0ae2e0b8ada733b7c645****
{
    "DBEngineVersion":"MySQL_8_0",
    "ZoneIds":"cn-beijing-b",
    "NodeSpec":"vedb.mysql.x4.xlarge",
    "NodeNumber":2,
    "VpcId":"vpc-3ajzohyfaru9s340jz1rp****",
    "SubnetId":"subnet-1g15j13jtzgu88ibuxwqp****",
    "InstanceName":"test",
    "SuperAccountName":"vedbuser",
    "SuperAccountPassword":"Kira****",
    "DBTimeZone":"UTC +08:00",
    "Tags":[
        {
            "Key":"chargetype",
            "Value":"postpaid"
        }
    ],
    "ChargeType":"PostPaid"
}
```


<span id=".6L-U5Zue56S65L6L"></span>
### Response example 1

```JSON
{
    "ResponseMetadata": {
        "RequestId": "202204102136280102090801470751****",
        "Action": "CreateDBInstance",
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


<span id=".6K-35rGC56S65L6LLTI="></span>
### Request example 2

A yearly/monthly subscription instance.

```JSON
POST /?Action=CreateDBInstance&Version=2022-01-01 HTTP/1.1
Content-Type: application/json
Host: vedbm.cn-beijing.byteplusapi.com.cn
X-Date: 20220101T101010Z
Authorization: HMAC-SHA256 Credential=AKLTN2I0MmFiNzMxNWE5NDgzMzk4MmVjMTVkODlkZTZ****/20220101/cn-beijing/vedbm/request,SignedHeaders=x-date, Signature=71d31fc7bcf990142851c9833c5656391486cda0ae2e0b8ada733b7c645****
{
    "DBEngineVersion":"MySQL_8_0",
    "ZoneIds":"cn-beijing-b",
    "NodeSpec":"vedb.mysql.x4.large",
    "NodeNumber":2,
    "SuperAccountName":"test",
    "SuperAccountPassword":"Root****",
    "VpcId":"vpc-3jhizogw3t3b43pncmfsy****",
    "SubnetId":"subnet-2gdmggo776m8050ztyz6b****",
    "ProjectName":"default",
    "ChargeType":"PrePaid",
    "InstanceName":"test",
    "Period":2,
    "PeriodUnit":"Month",
    "AutoRenew":true,
    "PrePaidStorageInGB":50
}
```


<span id=".6L-U5Zue56S65L6LLTI="></span>
### Response example 2

```JSON
{
    "ResponseMetadata": {
        "RequestId": "202204102136280102090801470751****",
        "Action": "CreateDBInstance",
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
