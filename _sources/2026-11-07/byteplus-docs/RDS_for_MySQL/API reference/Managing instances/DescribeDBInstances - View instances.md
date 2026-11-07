---
title: "DescribeDBInstances - View instances"
product: "RDS for MySQL"
product_code: "RDS_for_MySQL"
source: "https://docs.byteplus.com/en/docs/RDS_for_MySQL/describedbinstances"
---

Call the DescribeDBInstances API to view the instance list.

<span id=".6K-35rGC57G75Z6L"></span>
## Request type

Synchronous request.

<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters


|Parameter |Type |Is it required? |Sample value |Description |
|---|---|---|---|---|
|InstanceId |String |No |mysql\-1d797b6f\*\*\*\* |Instance ID. |
|InstanceName |String |No |TestDB |Instance name. |
|InstanceStatus |String |No |Running |Instance state, values:<br><br><br>* `Creating`: creating.<br><br>* `Running`: running.<br><br>* `Deleting`: deleting.<br><br>* `Restarting`: restarting.<br><br>* `Updating`: modifying.<br><br>* `Restoring`: recovering.<br><br>* `Error`: error.<br><br>* `Upgrading`: upgrading.<br><br>* `Released`: recycling.<br><br>* `Recycled`: recycled.<br><br>* `MasterChanging`: primary node switching.<br><br>* `TDEUpdating`: TDE modifying.<br><br>* `Closed`: shut down.<br><br>* `Maintaining`: maintaining.<br><br>* `CreateFailed`: failed to create.<br><br>* `Closing`: Shutting down.<br><br>* `SSLUpdating`: SSL modifying.<br><br>* `AllowListMaintaining`: Allowlist modifying.<br><br>* `Unknown`: Unknown.<br><br>* `ProxyCreating`: Proxy is enabling.<br><br>* `ProxyDeleting`: proxy is disabling.<br><br>* `ChargeTypeChanging`: billing method changing.<br><br>* `NetWorkChanging`: Network changing. |
|DBEngineVersion |String |No |MySQL_8_0 |Compatible version. Values:<br><br><br>* `MySQL_5_7`: MySQL 5.7.<br><br>* `MySQL_8_0`: MySQL 8.0.<br><br>* `MySQL 8.4`: MySQL 8.4. |
|CreateTimeStart |String |No |2022\-01\-01T10:10:10Z |Query the creation time range of the instance. |
|CreateTimeEnd |String |No |2022\-01\-01T10:10:10Z |Query the creation time range of the instance. |
|ZoneId |String |No |cn\-beijing\-a |Instance's availability zone. |
|ChargeType |String |No |PostPaid |Billing method. Values:<br><br><br>* `PostPaid`: pay\-as\-you\-go (post\-paid).<br><br>* `PrePaid`: subscription (pre\-paid). |
|InstanceType |String |No |DoubleNode |Instance type. The value is `DoubleNode`. |
|NodeSpec |String |No |rds.mysql.1c2g |Primary node specifications. For details on node specification, refer to [Product specification](https://docs.byteplus.com/en/docs/RDS_for_MySQL/product_specifications). |
|TagFilters |Array of [TagFilterObject](https://docs.byteplus.com/en/docs/40/15523#tagfilterobject) |No |[<br><br>{<br><br>"Key":"key1",<br><br>"Value":"value1"<br><br>}<br><br>] |An array of tag key\-value pairs for querying and filtering.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">It supports querying and filtering up to 10 tag key\-value pairs simultaneously per request.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">Both the key and value fields must be set.</div><br> |
|ProjectName |String |No |testProject |Project name. |
|PageNumber |Integer |No |1 |Current page number. The minimum value is 1. Default value: 1. |
|PageSize |Integer |No |10 |Number of records per page. The minimum value is 1, and the maximum value cannot exceed 1,000. The default value is 10. |
|PrivateNetworkIpAddress |String |No |192. ** *.* ** .19 |The IP address of the instance's default endpoint, used to query the instance by IP address first. |
|KernelVersion |Array of String |No |["MySQL 5.7.32_20240415","MySQL 8.0.32_20240815"] |Kernel minor version. Filters instances with the specified kernel minor version. You can pass in multiple kernel minor version numbers. For detailed information on the kernel minor version of MySQL, refer to [Kernel version release note](https://docs.byteplus.com/en/docs/RDS_for_MySQL/kernal_version_release_notes). |
|PrivateNetworkVpcId |String |No |vpc\-3rebt5uf5fr405zsk2if9\*\*\*\* |Virtual private cloud ID. This field can be used to filter instances using a specified virtual private cloud. |
|StorageType |String |No |LocalSSD |The storage type of the instance. Range:<br><br><br>* `LocalSSD`: local SSD.<br><br>* `CloudESSD_FlexPL`: Cloud ESSD FlexPL.<br><br>* `CloudESSD_PL0`: Cloud ESSD PL0.<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">The StorageType parameter is required if you set the StorageSpace parameter.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">When the InstanceType is set to <code>SingleNode</code>, the StorageType can only be <code>CloudESSD_FlexPL</code> or <code>CloudESSD_PL0</code>.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">This parameter has different value ranges for different APIs. The rules are as follows:</div><br><br><br>   * <div data-tips="true" data-tips-type="tip">When used as a request parameter in the following APIs, StorageType can only be <code>LocalSSD</code>.</div><br><br><br>      * <div data-tips="true" data-tips-type="tip">RestoreToCrossRegionInstance</div><br><br><br>      * <div data-tips="true" data-tips-type="tip">RestoreToNewInstanceFromUserTos</div><br><br><br>* <div data-tips="true" data-tips-type="tip">When used as a request parameter for some API operations, the value range of this parameter is related to the storage type of the original instance. The specific rules are as follows:</div><br><br><br>   * <div data-tips="true" data-tips-type="tip">If the original instance storage type is <code>LocalSSD</code> or <code>CloudESSD_FlexPL</code>, changing the storage type is not supported.</div><br><br><br>   * <div data-tips="true" data-tips-type="tip">If the original instance storage type is <code>CloudESSD_PL0</code>, the value can be <code>CloudESSD_PL0</code> or <code>CloudESSD_FlexPL</code>.</div><br><br><br>      <div data-tips="true" data-tips-type="tip">The related APIs are:      </div><br>      <br><br>      * <div data-tips="true" data-tips-type="tip">RebuildDBInstance</div><br><br><br>      * <div data-tips="true" data-tips-type="tip">RestoreToNewInstance</div><br><br><br>      * <div data-tips="true" data-tips-type="tip">ModifyDBNodeSpec</div><br> |
|EngineType |String |No |RocksDB |Database engine type. Values:<br><br><br>* `InnoDB`: InnoDB engine.<br><br>* `RocksDB`: RocksDB engine.<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">When used as a request parameter, the default value is <code>InnoDB</code>.</div><br> |


<span id="tagfilterobject"></span>
### TagFilterObject


|Parameter |Type |Is it required? |Sample value |Description |
|---|---|---|---|---|
|Key |String |Yes |ExampleKey |The tag key for querying and filtering. |
|Value |String |No |ExampleValue |The tag value for query filtering.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">If a tag value is set when associating a tag, this parameter is required for filtering.</div><br> |
|Values |Array of String |No |["ExampleValue1","ExampleValue2"] |The tag value for querying and filtering.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">If Value and Values both exist, Values takes precedence.</div><br> |


<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters


|Parameter |Type |Sample value |Description |
|---|---|---|---|
|Total |Integer |1 |Total number of instances. |
|Instances |Array of [InstanceInfoObject](https://docs.byteplus.com/en/docs/40/15523#instanceinfoobject) |Refer to the sample response. |\> Instances. |


<span id="instanceinfoobject"></span>
### InstanceInfoObject


|Parameter |Type |Sample value |Description |
|---|---|---|---|
|AddressObject |Array of [AddressObject](https://docs.byteplus.com/en/docs/40/15523#addressobject) |[<br><br>{<br><br>"Domain":"mysql77c004ac\*\*\*\*.rds.ivolces.com",<br><br>"EipId":"",<br><br>"IPAddress":"",<br><br>"NetworkType":"Private",<br><br>"Port":"3306",<br><br>"SubnetId":""<br><br>}<br><br>] |Connection information of the default endpoint. |
|AllowListVersion |String |v2 |The IP allowlist version. The value can be `0`, `v1`, or `v2`. |
|ChargeDetail |Object of [ChargeDetailObject](https://docs.byteplus.com/en/docs/40/15523#chargedetailobject) |None. |Payment method. |
|CreateTime |String |2022\-01\-01T10:10:10Z |Instance creation time (UTC time). |
|CurrentKernelVersion |String |MySQL 5.7.32_20241015 |Kernel minor version of the instance. |
|DBEngineVersion |String |MySQL_8_0 |Compatible version. Values:<br><br><br>* `MySQL_5_7`: MySQL 5.7.<br><br>* `MySQL_8_0`: MySQL 8.0.<br><br>* `MySQL 8.4`: MySQL 8.4. |
|DeletionProtection |String |Enabled |Indicates whether to enable deletion protection for the instance. Values:<br><br><br>* `Enabled`: yes.<br><br>* `Disabled`: no. Default value. |
|EngineType |String |RocksDB |Database engine type. Values:<br><br><br>* `InnoDB`: InnoDB engine.<br><br>* `RocksDB`: RocksDB engine.<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">When used as a request parameter, the default value is <code>InnoDB</code>.</div><br> |
|InstanceId |String |mysql\-h441603c\*\*\*\* |Instance ID. |
|InstanceName |String |Instance name |Instance name. |
|InstanceStatus |String |Running |Instance state, values:<br><br><br>* `Creating`: creating.<br><br>* `Running`: running.<br><br>* `Deleting`: deleting.<br><br>* `Restarting`: restarting.<br><br>* `Updating`: modifying.<br><br>* `Restoring`: recovering.<br><br>* `Error`: error.<br><br>* `Upgrading`: upgrading.<br><br>* `Released`: recycling.<br><br>* `Recycled`: recycled.<br><br>* `MasterChanging`: primary node switching.<br><br>* `TDEUpdating`: TDE modifying.<br><br>* `Closed`: shut down.<br><br>* `Maintaining`: maintaining.<br><br>* `CreateFailed`: failed to create.<br><br>* `Closing`: Shutting down.<br><br>* `SSLUpdating`: SSL modifying.<br><br>* `AllowListMaintaining`: Allowlist modifying.<br><br>* `Unknown`: Unknown.<br><br>* `ProxyCreating`: Proxy is enabling.<br><br>* `ProxyDeleting`: Proxy is disabling.<br><br>* `ChargeTypeChanging`: billing method changing.<br><br>* `NetWorkChanging`: Network changing. |
|InstanceType |String |DoubleNode |Instance type. Values:<br><br><br>* `DoubleNode`, Double node type.<br><br>* `MultiNode`, multiple node type.<br><br>* `SingleNode`, Single node type.<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">If the blue instance is a single\-node type, you can select a single\-node or double\-node type for the green instance.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">If the blue instance is a double\-node type, you can select a double\-node or multiple\-node type for the green instance.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">If the blue instance is a multiple\-node type, you can only select the multiple\-node type for the green instance.</div><br> |
|LowerCaseTableNames |String |1 |Specifies whether the table name is case sensitive. The default value is `1`. Range:<br><br><br>* `0`: table names are stored in their original case and are case\-sensitive.<br><br>* `1`: table names are stored in lowercase and are case\-insensitive. |
|MaintenanceWindow |Object of [MaintenanceWindowObject](https://docs.byteplus.com/en/docs/40/15523#maintenancewindowobject) |{<br><br>"DayKind": "Week",<br><br>"DayOfMonth": [],<br><br>"DayOfWeek": [<br><br>"Monday",<br><br>"Tuesday",<br><br>"Wednesday",<br><br>"Thursday",<br><br>"Friday",<br><br>"Saturday",<br><br>"Sunday"<br><br>],<br><br>"MaintenanceTime": "18:00Z\-21:59Z"<br><br>} |Maintenance window. |
|NodeCPUUsedPercentage |Double |0.3 |The average CPU usage rate of the instance's primary node in the recent minute. |
|NodeMemoryUsedPercentage |Double |8.67 |The average memory usage rate of the instance primary node in the last minute. |
|NodeNumber |Integer |2 |Number of nodes. |
|NodeSpaceUsedPercentage |Double |21.49 |The average disk usage rate of the instance's primary node in the last minute. |
|NodeSpec |String |rds.mysql.1c2g |Node specification. For details on node specification, refer to [Product specification](https://docs.byteplus.com/en/docs/RDS_for_MySQL/product_specifications). |
|ProjectName |String |Default |Affiliated project. |
|RegionId |String |cn\-beijing |Region ID, use [DescribeRegions](https://docs.byteplus.com/en/docs/RDS_for_MySQL/describeregions) to query the available region list. Use this parameter to specify the region for creating the instance. |
|StorageSpace |Integer |200 |The storage space for the instance. The unit is GiB. |
|StorageType |String |LocalSSD |The storage type of the instance. Range:<br><br><br>* `LocalSSD`: local SSD.<br><br>* `CloudESSD_FlexPL`: Cloud ESSD FlexPL.<br><br>* `CloudESSD_PL0`: Cloud ESSD PL0.<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">The StorageType parameter is required if you set the StorageSpace parameter.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">When the InstanceType is set to <code>SingleNode</code>, the StorageType can only be <code>CloudESSD_FlexPL</code> or <code>CloudESSD_PL0</code>.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">This parameter has different value ranges for different APIs. The rules are as follows:</div><br><br><br>   * <div data-tips="true" data-tips-type="tip">When used as a request parameter in the following APIs, StorageType can only be <code>LocalSSD</code>.</div><br><br><br>      * <div data-tips="true" data-tips-type="tip">RestoreToCrossRegionInstance</div><br><br><br>      * <div data-tips="true" data-tips-type="tip">RestoreToNewInstanceFromUserTos</div><br><br><br>* <div data-tips="true" data-tips-type="tip">When used as a request parameter for some API operations, the value range of this parameter is related to the storage type of the original instance. The specific rules are as follows:</div><br><br><br>   * <div data-tips="true" data-tips-type="tip">If the original instance storage type is <code>LocalSSD</code> or <code>CloudESSD_FlexPL</code>, changing the storage type is not supported.</div><br><br><br>   * <div data-tips="true" data-tips-type="tip">If the original instance storage type is <code>CloudESSD_PL0</code>, the value can be <code>CloudESSD_PL0</code> or <code>CloudESSD_FlexPL</code>.</div><br><br><br>      <div data-tips="true" data-tips-type="tip">The related APIs are:      </div><br>      <br><br>      * <div data-tips="true" data-tips-type="tip">RebuildDBInstance</div><br><br><br>      * <div data-tips="true" data-tips-type="tip">RestoreToNewInstance</div><br><br><br>      * <div data-tips="true" data-tips-type="tip">ModifyDBNodeSpec</div><br> |
|SubnetId |String |subnet\-rrzzs6dzof0gv0x58b\*\*\*\* |Subnet ID. |
|Tags |Array of [TagObject](https://docs.byteplus.com/en/docs/40/15523#tagobject) |[ { "Key": "key1", "Value": "value1" } ] |An array object of tag keys and tag values to be bound. |
|TimeZone |String |UTC + 08: 00 |Time zone. |
|VpcId |String |vpc\-13g2qkkzntfy83n6nu4z1\*\*\*\* |Proprietary network (VPC) ID. |
|ZoneId |String |cn\-beijing\-a |The availability zone where the primary instance node resides. |
|ZoneIds |Array of String |[<br><br>"cn\-beijing\-a",<br><br>"cn\-beijing\-b"<br><br>] |A list of availability zones where the instance nodes are located. |
|DrDtsTaskId |String |df5a93434880466cb8422b2db93d\*\*\*\* |The ID of the DTS data synchronization task for the synchronization link between the primary and disaster recovery instances. |


<span id="addressobject"></span>
### AddressObject


|Parameter |Type |Sample value |Description |
|---|---|---|---|
|DNSVisibility |Boolean |false |* `false`: BytePlus private network resolution (default).<br><br>* `true`: BytePlus private and public network resolution. |
|Domain |String |mysql1d797b6f\*\*\*\*.rds.ivolces.com |Connection domain name. |
|EipId |String |eip\-13g6t81tglmgw3n6nu4vt\*\*\*\* |ID of EIP, valid only for public address. |
|IPAddress |String |10. ** *.* ** .3 |IP address. |
|InternetProtocol |String |IPv4 |IP protocol version. Value is `IPv4`. |
|NetworkType |String |Private |Network address type, values are:<br><br><br>* `Private`: private network connection address.<br><br>* `Public`: public network connection address. |
|Port |String |3306 |Port. |
|SubnetId |String |subnet\-2bzr8zdx5o8ao2dx0efq4\*\*\*\* |Subnet ID, valid for private addresses only. |
|EipLocked |Boolean |false |Whether the EIP for the connection endpoint is shut down due to arrears. Values:<br><br><br>* `true`: yes.<br><br>* `false`: no. |


<span id="chargedetailobject"></span>
### ChargeDetailObject


|Parameter |Type |Sample value |Description |
|---|---|---|---|
|AutoRenew |Boolean |true |Is automatic renewal enabled for the prepaid scenario?<br><br><br>* `true`: automatic renewal.<br><br>* `false`: no automatic renewal. |
|ChargeEndTime |String |2025\-08\-22T15:59:59.000Z |Billing end time for the subscription instance (UTC time). Format: `yyyy-MM-ddTHH:mm:ss.sssZ`.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">This field is empty for pay\-as\-you\-go instances.</div><br> |
|ChargeStartTime |String |2025\-07\-22T13:10:15.000Z |The billing start time of the instance (UTC time). Format: `yyyy-MM-ddTHH:mm:ss.sssZ`. |
|ChargeStatus |String |Normal |Billing state of the instance. Values:<br><br><br>* `Normal`: normal.<br><br>* `Overdue`: overdue.<br><br>* `Overdue`: waiting for payment. |
|ChargeType |String |PostPaid |Payment type. Values:<br><br><br>* `PostPaid`: pay\-as\-you\-go (post\-paid).<br><br>* `PrePaid`: subscription (pre\-paid). |
|OverdueReclaimTime |String |2025\-08\-29T15:59:59.000Z |The estimated UTC release time after the instance is shut down due to overdue payments (pay\-as\-you\-go) or expiration (subscription). Format: `yyyy-MM-ddTHH:mm:ss.sssZ`. |
|OverdueTime |String |2025\-08\-23T04:00:00.000Z |The time in UTC when the instance is shut down due to overdue payments (pay\-as\-you\-go) or expiration (subscription). Format: `yyyy-MM-ddTHH:mm:ss.sssZ`. |
|Period |Integer |1 |Subscription duration in a prepaid scenario.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">When this parameter is used as a request parameter, the default value is <code>1</code>.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">When PeriodUnit is<code> Year</code>, Period ranges from 1 to 3.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">When PeriodUnit is <code>Month</code>, Period ranges from 1 to 9.</div><br> |
|PeriodUnit |String |Month |Purchase period for prepaid scenarios.<br><br><br>* `Month`: the purchase cycle is by month.<br><br>* `Year`: the purchase cycle is by year.<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">When this parameter is used as a request parameter, the default value is <code>Month</code>.</div><br> |
|TempModifyStartTime |String |2022\-01\-01T10:10:10.000Z |Start time of the temporary upgrade (UTC time). Format: `yyyy-MM-ddTHH:mm:ss.sssZ`.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">This field is not returned for an instance that is not in a temporary upgrade period.</div><br> |
|TempModifyEndTime |String |2022\-01\-01T10:10:09.000Z |Restoration time of temporary upgrade (UTC time). Format: `yyyy-MM-ddTHH:mm:ss.sssZ`.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">This field is not returned for an instance that is not in a temporary upgrade period.</div><br> |


<span id="maintenancewindowobject"></span>
### MaintenanceWindowObject


|Parameter |Type |Sample value |Description |
|---|---|---|---|
|DayKind |String |Week |The granularity of the maintenance cycle, with values of `Week`. |
|DayOfWeek |Array of String |["Monday","Tuesday"] |Specifies the day(s) of the week for the maintenance window. Valid values are `Monday`, `Tuesday`, `Wednesday`, `Thursday`, `Friday`, `Saturday`, and `Sunday`. You can select more than one day. If this value is not specified or is empty, it defaults to all seven days of the week. |
|MaintenanceTime |String |22:00Z\-02:00Z |The maintenance window for the instance. Format: `HH:mmZ-HH:mmZ` (UTC time). |


<span id="tagobject"></span>
### TagObject


|Parameter |Type |Sample value |Description |
|---|---|---|---|
|Key |String |tagkey |The key of the instance tag. The rules for the tag key are as follows:<br><br><br>* Supports letters or characters of any language, digits, and spaces.<br><br>* Supports special characters: `_.:/=+-@`.<br><br>* `volc:` is a system\-reserved tag key. When adding tags, the tag key cannot start with any case form of `volc:`.<br><br>* The tag key must be 1 to 128 characters in length. |
|Value |String |tagvalue |The value of the instance tag. The rules for setting the tag value are as follows:<br><br><br>* Supports letters or characters of any language, digits, and spaces.<br><br>* Supports special characters: `_.:/=+-@`.<br><br>* The tag value must be 0 to 256 characters in length, which means the tag value can be empty. |


<span id=".56S65L6L"></span>
## Sample

<span id=".6K-35rGC56S65L6L"></span>
### Sample request

```json
POST /?Action=DescribeDBInstances&Version=2022-01-01 HTTP/1.1
Content-Type: application/json
Host: rds-mysql.cn-beijing.byteplusapi.com.cn
X-Date: 20211202T101010Z
Authorization: HMAC-SHA256 Credential=AKLTN2I0MmFiNzMxNWE5NDgzMzk4MmVjMTVkODlkZTZ****/20211202/cn-beijing/rds_mysql/request,SignedHeaders=x-date, Signature=71d31fc7bcf990142851c9833c5656391486cda0ae2e0b8ada733b7c6458****
{
    "InstanceStatus": "Running"
}
```


<span id=".6L-U5Zue56S65L6L"></span>
### Sample response

```json
{
    "ResponseMetadata": {
        "RequestId": "20230110194301C23B8A99043A27D617A2",
        "Action": "DescribeDBInstances",
        "Version": "2022-01-01",
        "Service": "rds_mysql",
        "Region": "cn-beijing"
    },
    "Result": {
        "Instances": [
            {
                "AddressObject": [
                    {
                        "DNSVisibility": false,
                        "Domain": "mysql-1d797b6f****-public.rds.volces.com",
                        "EipId": "eip-13flx63066io03n6nu51u****",
                        "EipLocked": false,
                        "IPAddress": "180.***.***.***",
                        "InternetProtocol": "IPv4",
                        "NetworkType": "Public",
                        "SubnetId": "subnet-rs4brkc5pnuov0x576g****"
                    },
                    {
                        "DNSVisibility": false,
                        "Domain": "mysql-1d797b6f****.rds.ivolces.com",
                        "EipId": "",
                        "EipLocked": false,
                        "IPAddress": "192.***.***.***",
                        "InternetProtocol": "IPv4",
                        "NetworkType": "Private",
                        "SubnetId": "subnet-rs4brkc5pnuov0x576g****"
                    }
                ],
                "AllowListVersion": "v2",
                "ChargeDetail": {
                    "AutoRenew": false,
                    "ChargeEndTime": "",
                    "ChargeStartTime": "2023-01-10T11:13:34.000Z",
                    "ChargeStatus": "Normal",
                    "ChargeType": "PostPaid",
                    "Number": 0,
                    "OverdueReclaimTime": "2200-01-15T16:00:00.000Z",
                    "OverdueTime": "",
                    "Period": 0,
                    "PeriodUnit": "Month"
                },
                "CreateTime": "2023-01-10T11:13:30.000Z",
                "CurrentKernelVersion": "MySQL 5.7.32_20241015",
                "DBEngineVersion": "MySQL_5_7",
                "InstanceId": "mysql-1d797b6f****",
                "InstanceName": "测试实例 1",
                "InstanceStatus": "Running",
                "InstanceType": "DoubleNode",
                "LowerCaseTableNames": "1",
                "MaintenanceWindow": {
                    "DayKind": "Week",
                    "DayOfMonth": [],
                    "DayOfWeek": [
                        "Monday",
                        "Tuesday",
                        "Wednesday",
                        "Thursday",
                        "Friday",
                        "Saturday",
                        "Sunday"
                    ],
                    "MaintenanceTime": "19:00Z-22:59Z"
                },
                "NodeCPUUsedPercentage": 1.59,
                "NodeMemoryUsedPercentage": 16.46,
                "NodeNumber": 3,
                "NodeSpaceUsedPercentage": 4.23,
                "NodeSpec": "rds.mysql.1c2g",
                "ProjectName": "",
                "RegionId": "cn-beijing",
                "StorageSpace": 20,
                "StorageType": "LocalSSD",
                "SubnetId": "subnet-2bzr8zdx5o8ao2dx0efq4****",
                "TimeZone": "UTC +08:00",
                "VpcId": "vpc-3rebt5uf5fr405zsk2if9****",
                "ZoneId": "cn-beijing-c",
                "ZoneIds": [
                    "cn-beijing-a",
                    "cn-beijing-c"
                ]
            }
        ],
        "Total": 1
    }
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error code

For more details, refer to [Error codes](https://docs.byteplus.com/en/docs/RDS_for_MySQL/error_code).
