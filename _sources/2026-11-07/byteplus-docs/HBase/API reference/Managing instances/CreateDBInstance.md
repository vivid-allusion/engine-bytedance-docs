---
title: "CreateDBInstance"
product: "Table Storage for HBase"
product_code: "HBase"
source: "https://docs.byteplus.com/en/docs/HBase/CreateDBInstance"
---

Call the CreateDBInstance API to create an HBase instance.

<span id=".6K-35rGC57G75Z6L"></span>
## Request type

Asynchronous request.

<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters


|Name |Type |Required |Example value |Description |
|---|---|---|---|---|
|InstanceName |String |No |test_api |Instance name. The naming convention is as follows:<br><br><br>* Cannot start with digits or hyphen (\-).<br><br>* It can contain only Chinese characters, letters, digits, underscores (_), and hyphens (\-).<br><br>* It must be 1 to 128 characters in length.<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">If this parameter is left blank, the instance ID will be used as the instance name by default.</div><br> |
|InstanceType |String |No |Standard |Instance type. Only the standard type is supported. The default value is `Standard`. |
|EngineVersion |String |Yes |HBase_2.0 |The version of the HBase database engine. Only HBase 2.0 is currently supported. The value defaults to `HBase_2.0`. |
|ZoneId |String |Yes |cn\-beijing\-a |Availability zone ID.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">You can call the <a href="https://docs.byteplus.com/en/docs/HBase/DescribeZones">DescribeZones</a> API to query the resource information for all availability zones of an HBase instance in a specified region, including the availability zone ID.</div><br> |
|RegionId |String |Yes |cn\-beijing |Region ID.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">You can call the <a href="https://docs.byteplus.com/en/docs/HBase/DescribeRegions">DescribeRegions</a> API to query resource information in all available regions for the instance, including the Region ID.</div><br> |
|MasterSpec |String |Yes |hbase.x1.4xlarge |The specification code of the Master node.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">For information about specifications supported by the Master node, see <a href="https://docs.byteplus.com/en/docs/HBase/Product_specifications">Product specifications</a>.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">The number of Master nodes is fixed and cannot be increased or decreased.</div><br> |
|RSCount |Integer |Yes |4 |The number of RegionServer nodes. An integer from 2 to 100. |
|RSSpec |String |Yes |hbase.x1.4xlarge |The specification code for the RegionServer node.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">For information about specifications supported by the RegionServer node, see <a href="https://docs.byteplus.com/en/docs/HBase/Product_specifications">Product specifications</a>.</div><br> |
|StorageType |String |Yes |HdfsHdd |The storage type of the instance. Valid values include:<br><br><br>* `HdfsHdd`: HDD file storage (default).<br><br>* `HdfsSsd`: SSD file storage. |
|StorageCapacity |Integer |Yes |1000 |The storage space size, in increments of 10 GiB. The value range is from 100 GiB to 20,000 GiB. |
|EnableCloudStorage |Bool |No |true |Specifies whether to enable Capacity storage. Valid values:<br><br><br>* `true`: Enables Capacity storage.<br><br>* `false`: Capacity storage is not enabled.<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">For a detailed introduction to capacity storage, see <a href="https://docs.byteplus.com/en/docs/HBase/About_hot_and_cold_data_separation">About hot and cold data separation</a>.</div><br> |
|ColdStorage |Integer |No |800 |The size of the capacity storage space. The value ranges from 800 GiB to 1,000,000 GiB in 10 GiB increments.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">This parameter is required when <code>EnableCloudStorage</code> is set to <code>true</code>.</div><br> |
|VpcId |String |Yes |vpc\-2d66uvmd9i8lc58ozz\*\*\*\* |The VPC ID.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">You can call the <a href="https://docs.byteplus.com/en/docs/vpc/DescribeVpcs">DescribeVpcs</a> API to query VPC information, including the VPC ID, for creating HBase instances.</div><br> |
|SubnetId |String |Yes |subnet\-2d6pl8bcpl2io58ozfd43\*\*\*\* |Subnet ID. The subnet must belong to the selected availability zone.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">A subnet is an IP address block within a VPC. All cloud resources in the VPC must be deployed within a subnet. The subnet allocates private IP addresses to cloud resources. You can call the <a href="https://docs.byteplus.com/en/docs/vpc/CreateSubnet">CreateSubnet</a> API to create a subnet.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">You can call the <a href="https://docs.byteplus.com/en/docs/vpc/DescribeSubnets">DescribeSubnets</a> API to query information about all subnets in a specified availability zone, including their subnet IDs.</div><br> |
|ProjectName |String |No |default |Select the project for the instance. If this parameter is left empty, the new instance is added to the `default` project.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">A project is a virtual concept that includes a set of resources, users, and roles. A project allows you to view and manage a group of resources in a unified manner and control the permissions of users and roles to these resources.</div><br> |
|ChargeType |String |Yes |PostPaid |The billing method of the instance. Value:<br><br><br>* `PostPaid`: Pay\-as\-you\-go.<br><br>* `PrePaid`: Yearly or monthly subscription. |
|PurchaseMonths |Integer |No |1 |The purchase duration, in months. The valid values are as follows:<br><br>`1`，`2`，`3`，`4`，`5`，`6`，`7`，`8`，`9`，`12`，`24`，`36`。<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">This parameter is required when <code>ChargeType</code> is <code>PrePaid</code>.</div><br> |
|AutoRenew |Bool |No |false |Whether to enable the automatic renewal function. The valid values are as follows:<br><br><br>* `true`: Enabled.<br><br>* `false`: Not enabled (default).<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">This parameter is valid only when <code>ChargeType</code> is set to <code>PrePaid</code>.</div><br> |
|DeletionProtection |String |No |enabled |The status of instance deletion protection. The valid values are as follows:<br><br><br>* `enabled`: The feature is enabled.<br><br>* `disabled`: The feature is disabled (default).<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">For more information about removal protection, see <a href="https://docs.byteplus.com/en/docs/HBase/Instance_deletion_protection">Instance deletion protection</a>.</div><br> |
|Tags |Array of [Tag](https://docs.byteplus.com/en/docs/219/60842#tag) |No |See the request example. |An array object of tag keys and tag values to be bound.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">It supports passing in multiple sets of tag key\-value objects at once, separated by commas (,). A single request supports up to 20 tag key\-value pairs, and a single instance can be bound with a maximum of 50 tags.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">The tag key value must meet certain setting rules. For details, please refer to the <a href="https://docs.byteplus.com/en/docs/HBase/Tag_overview">Tag setting rules</a>.</div><br> |
|MaintenanceWindow |Object of MaintenanceWindow |No |See the request example. |The maintenance window for the instance. If this parameter is not specified, the default maintenance window is 02:00\-05:59 (UTC+08:00) daily. |
|ClientToken |String |No |WbiAlPqJM6tMoSOYhT\*\*\*\* |Ensures the idempotence of the request and prevents repeated submissions. The client generates this parameter value, which must be unique across requests. The value is case\-sensitive and must not exceed 127 ASCII characters. |


<span id="973d01f8"></span>
### MaintenanceWindow


|Name |Type |Required |Example value |Description |
|---|---|---|---|---|
|Period |Long |Yes |4 |The duration of the maintenance window. |
|DayKind |String |Yes |Week |The granularity of the maintenance period. The default value is `Week`. |
|StartTime |String |Yes |18:00Z |The start time of the maintenance window (UTC). |
|DayOfWeeks |Array of String |Yes |["Monday","Tuesday","Wednesday","Thursday","Friday","Saturday","Sunday"] |Specifies the days of the week for the maintenance window. You can select multiple values: `Monday`, `Tuesday`, `Wednesday`, `Thursday`, `Friday`, `Saturday`, `Sunday`. If this value is not specified or is empty, it defaults to all seven days of the week. |


<span id="tag"></span>
### Tag


|Name |Type |Required |Example value |Description |
|---|---|---|---|---|
|Key |String |Yes |chargetype |The key of the tag to associate. |
|Value |String |Yes |postpaid |The value of the tag to be associated. |


<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameter


|Name |Type |Example value |Description |
|---|---|---|---|
|InstanceId |String |hb\-cn01762cf4d6\*\*\*\* |Instance ID. |
|OrderNo |String |Order730602621667020\*\*\*\* |Order ID. |


<span id=".56S65L6L"></span>
## Example

<span id=".6K-35rGC56S65L6LIDE="></span>
### Request example

```json
POST /?Action=CreateDBInstance&Version=2018-01-01 HTTP/1.1
Host: hbase.cn-beijing.byteplusapi.com.cn
Content-Type: application/json; charset=utf-8
X-Date: 20201103T104027Z
Authorization: HMAC-SHA256 Credential=AK****/20201103/cn-beijing/hbase/request,SignedHeaders=content-type;host;x-date,  Signature=****
{
    "RegionId": "cn-beijing",
    "ZoneId": "cn-beijing-a",
    "InstanceName": "test_api",
    "MasterSpec": "hbase.x1.4xlarge",
    "RSCount": 3,
    "RSSpec": "hbase.x1.4xlarge",
    "StorageCapacity": 600,
    "ChargeType": "PostPaid",
    "EngineVersion": "HBase_2.0",
    "VpcId": "vpc-3redy6326y7ls5zsk2iko****",
    "SubnetId": "subnet-3redy6qqkavb45zsk2i1m****",
    "StorageType": "HdfsSsd",
    "Tags": [
        {
            "Key": "chargetype",
            "Value": "postpaid"
        }
    ]
}
```


<span id=".6L-U5Zue56S65L6LIDE="></span>
### Response example

```json
{
    "ResponseMetadata": {
        "RequestId": "202303141924047CADEE887F9E5297****",
        "Action": "CreateDBInstance",
        "Version": "2018-01-01",
        "Service": "hbase",
        "Region": "cn-beijing"
    },
    "Result": {
        "InstanceId": "hb-cn01762cf4d6****",
        "OrderNo": "Order721036083523859****"
    }
}
```
