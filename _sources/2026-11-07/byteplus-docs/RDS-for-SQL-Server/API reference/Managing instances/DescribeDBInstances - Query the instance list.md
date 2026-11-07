---
title: "DescribeDBInstances - Query the instance list"
product: "RDS for SQL Server"
product_code: "RDS-for-SQL-Server"
source: "https://docs.byteplus.com/en/docs/RDS-for-SQL-Server/describedbInstances"
---

Call the DescribeDBInstances API to query the instance list.

<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters

This section describes only the request parameters specific to this API and some common parameters. For more information, refer to [Common parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).



**Action ** <span data-label="purple">string </span><span data-api-tag="require|FWyouA">必选</span> `example value: DescribeDBInstances`

The action to be performed is `DescribeDBInstances`.<



**Version ** <span data-label="purple">string </span><span data-api-tag="require|sxTIw0">必选</span> `Example value: 2022-01-01`

The API version is `2022-01-01`.



**PrimaryInstanceId** <span data-label="purple">string</span> `Optional` `Example value: mssql-h441603c****`

Primary instance ID.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">You can pass the primary instance ID to query information about all its read\-only instances.</div>




**InstanceCategory** <span data-label="purple">string</span> `Optional` `Example value: Primary`

Instance category. Used to classify and manage instances. If this parameter is not passed, all instances are returned. Possible values:


* `Primary`: The primary instance.

* `ReadOnly`: Read only instance.



**ProjectName** <span data-label="purple">string</span> `Optional` `Example value: default`

Project.



**ServerCollation** <span data-label="purple">string</span> `Optional` `Example: Chinese_PRC_CI_AS`

Instance character set collation.



**InstanceId** <span data-label="purple">string</span> `Optional` `Example value: mssql-dab1be87****`

Instance ID.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">You can call the <a href="https://docs.byteplus.com/en/docs/RDS-for-SQL-Server/describedbInstancedetail">DescribeDBInstanceDetail</a> API to view the instance ID.</div>




**InstanceName** <span data-label="purple">string</span> `Optional` `Example: Sample instance`

The instance name.



**InstanceStatus** <span data-label="purple">string</span> `Optional` `Example value: Running`

The status of the instance. Valid values:


* `Running`: Running.

* `Creating`: creating.

* `Deleting`: deleting.

* `Restarting`: restarting.

* `Updating`: changing.

* `MasterChanging`: Primary node is switching.

* `Error`: Error.



**DBEngineVersion** <span data-label="purple">string</span> `Optional` `Example value: SQLServer_2019_Std`

Compatible version. The values are as follows:


* `SQLServer_2019_Std`: SQL Server 2019 Standard Edition.

* `SQLServer_2019_Ent`: SQL Server 2019 Enterprise Edition.

* `SQLServer_2019_Web`: SQL Server 2019 Web Edition.

* `SQLServer_2022_Std`: SQL Server 2022 Standard Edition.

* `SQLServer_2022_Ent`: SQL Server 2022 Enterprise Edition.

* `SQLServer_2022_Web`: SQL Server 2022 Web Edition.



**InstanceType** <span data-label="purple">string</span> `Optional` `Example value: HA`

Instance type. The values are as follows:


* `HA`: Indicates the High Availability type.

* `Basic`: Indicates the single\-node edition type.

* `Cluster` Represents the Cluster edition type.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">When <code>DBEngineVersion</code> is set to <code>SQLServer_2019_Std</code> or <code>SQLServer_2022_Std</code>, you can set <code>InstanceType</code> to <code>HA</code> or <code>Basic</code>.</div>


* <div data-tips="true" data-tips-type="tip">When <code>DBEngineVersion</code> is set to <code>SQLServer_2019_Ent</code> or <code>SQLServer_2022_Ent</code>, you can set <code>InstanceType</code> to <code>Cluster</code> or <code>Basic</code>.</div>


* <div data-tips="true" data-tips-type="tip">When <code>DBEngineVersion</code> is set to <code>SQLServer_2019_Web</code> or <code>SQLServer_2022_Web</code>, you can set <code>InstanceType</code> to <code>Basic</code>.</div>




**CreateTimeStart** <span data-label="purple">string</span> `Optional` `Example value: 2023-09-10T09:19:39.000Z`

The start time for creating the instance, in UTC format.



**CreateTimeEnd** <span data-label="purple">string</span> `Optional` `Example value: 2023-09-19T09:19:39.000Z`

The end time for creating the instance, in UTC format.



**ZoneId** <span data-label="purple">string</span> `Optional` `Example value: cn-beijing-a`

The availability zone of the instance.



**ChargeType** <span data-label="purple">string</span> `Optional` `Example: PostPaid`

Payment type. Possible values:


* `PostPaid`: Pay\-as\-you\-go.

* `PrePaid`: Subscription.



**TagFilters** <span data-label="purple">object[]</span> `Optional` `Example value: TagFilter`

An array of tag filter objects.


**Key ** <span data-label="purple">string </span><span data-api-tag="require|LVaR3N">必选</span> `Example value: abc`

The key of the instance tag.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">A single query cannot contain more than 10 tags.</div>


* <div data-tips="true" data-tips-type="tip">Duplicate tag keys are allowed.</div>


* <div data-tips="true" data-tips-type="tip">Tag keys cannot be empty.</div>




**Value** <span data-label="purple">string</span> `Optional` `Example value: 3`

The value of the instance tag.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">If this parameter is specified, the key must be specified first.</div>


* <div data-tips="true" data-tips-type="tip">If this parameter is not specified, all tag values for the same tag key are queried.</div>


* <div data-tips="true" data-tips-type="tip">Passing an empty string queries for tags with an empty tag value.</div>




**Values** <span data-label="purple">string[]</span> `Optional` `Example: ["1", "2", "8"]`

When multiple tag values are passed in for an instance tag, they shall be separated by English commas (,) with the values in an OR logical relationship.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">If this parameter is specified, the key must be specified first.</div>


* <div data-tips="true" data-tips-type="tip">If this parameter is not specified, all tag values for the same tag key are queried.</div>


* <div data-tips="true" data-tips-type="tip">Passing an empty string queries for tags with an empty tag value.</div>





**PageNumber** <span data-label="purple">integer</span> `Optional`. `Example value: 1`

The number of the page to return. The minimum value is 1, the maximum is 2147483647, and the default value is 1.



**PageSize** <span data-label="purple">integer</span> `Optional` `Example value: 10`

Number of records per page. The minimum value is 1, the maximum is 1,000, and the default is 10.



<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters

This section describes only the response parameters specific to this API. For more information, refer to [Return structure](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response).



**Total ** <span data-label="purple">integer </span>`Example value: 1`

Total number of instances.



**InstancesInfo ** <span data-label="purple">object[] </span>`Example value: InstancesInfo`

Instance list.


**CreateTime ** <span data-label="purple">string </span>`Example value: 2023-04-04T07:04:21.000Z`

The time when the instance was created, in yyyy\-MM\-ddTHH:mm:ss.sZ format (UTC).



**ServerCollation ** <span data-label="purple">string </span>`Example value: Chinese_PRC_CI_AS`

The instance character set collation. The default value is `Chinese_PRC_CI_AS`. Most native character sets are supported. The values are as follows:


* `Chinese_PRC_90_CI_AI`

* `Chinese_PRC_CI_AI`

* `Chinese_PRC_CI_AS`

* `Chinese_PRC_CS_AS`

* `Chinese_PRC_BIN`

* `Chinese_PRC_BIN2`

* `Cyrillic_General_CI_AS`

* `Latin1_General_CI_AS`

* `Latin1_General_CS_AS`

* `SQL_Latin1_General_CP1_CI_AS`

* `SQL_Latin1_General_CP1_CS_AS`

* `Japanese_CI_AS`

* `Japanese_CS_AS`

* `Chinese_Taiwan_Stroke_CI_AS`

* `Chinese_Taiwan_Stroke_CS_AS`

* `Thai_CI_AS`



**ZoneId ** <span data-label="purple">string </span>`Example value: cn-beijing-a`

Availability zone ID.



**VpcId ** <span data-label="purple">string </span>`Example value: vpc-2d5xeur6hiscg58ozfcuq****`

The Virtual Private Cloud (VPC) ID.



**TimeZone ** <span data-label="purple">string </span>`Example value: China Standard Time`

Time zone.



**SubnetId ** <span data-label="purple">string </span>`Example value: subnet-2bzup883l93402dx0efe1****`

The subnet ID.



**StorageType ** <span data-label="purple">string </span>`Example value: ESSDPL1`

The storage type of the instance. The value is `ESSDPL1`.



**StorageSpace ** <span data-label="purple">integer </span>`Example value: 200`

Total instance storage space. Unit: GiB.



**RegionId ** <span data-label="purple">string </span>`Example: cn-beijing`

The region ID. You can call [DescribeRegions](https://docs.byteplus.com/en/docs/RDS-for-SQL-Server/describeRegions) to query for available regions. This parameter specifies the region where the instance is created.



**ProjectName ** <span data-label="purple">string </span>`Example value: Test`

Project.



**Port ** <span data-label="purple">string </span>`Example: 1433`

The instance's private network port.



**NodeSpec ** <span data-label="purple">string </span>`Example: rds.mssql.se.ha.d4.4c16g`

The primary node specification.



**NodeDetailInfo** <span data-label="purple">object[]</span> `Example value: None`

Instance node information.


**CreateTime ** <span data-label="purple">string </span>`Example value: 2024-01-02T11:17:33.000Z`

The creation time of the node.



**InstanceId ** <span data-label="purple">string </span>`Example value: mssql-93420fe2****`

Instance ID.



**Memory ** <span data-label="purple">integer </span>`Example value: 8`

Memory size, in GiB.



**NodeId** <span data-label="purple">string</span> `Example value: mssql-dab1be87****-0`

Node ID



**NodeSpec ** <span data-label="purple">string </span>`Example value: rds.mssql.se.ha.d4.4c16g`

Node specification.



**NodeStatus ** <span data-label="purple">string </span>`Example: Running`

The status of the node. Possible values are:


* `Running`: Running.

* `Creating`: creating.

* `Deleting`: deleting.

* `Restarting`: restarting.

* `Updating`: changing.

* `MasterChanging`: primary node switching.

* `Error`: Error.



**NodeType ** <span data-label="purple">string </span>`Example value: Primary`

Node type. Possible values:


* `Primary`: The primary node endpoint.

* `ReadOnly`: The read only node endpoint.

* `Secondary`: The secondary node endpoint.



**RegionId ** <span data-label="purple">string </span>`Example value: cn-beijing`

Region ID.



**UpdateTime ** <span data-label="purple">string </span>`Example value: 2024-01-03T09:34:55.000Z`

The update time of the node.



**VCPU ** <span data-label="purple">integer </span>`Example value: 4`

CPU size. For example, 1 indicates 1 core.



**ZoneId ** <span data-label="purple">string </span>`Example value: cn-beijing-a`

Availability zone ID.



**NodeIP ** <span data-label="purple">string </span>`Example value: 192.168.xx.xxx`

Node IP.



**HostName ** <span data-label="purple">string </span>`Example value: iv-xxx`

Node hostname.




**InstanceType ** <span data-label="purple">string </span>`Example value: HA`

Instance type. The values are as follows:


* `HA`: Indicates the High Availability type.

* `Basic`: Indicates the single\-node edition type.

* `Cluster` Represents the Cluster edition type.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">When <code>DBEngineVersion</code> is set to <code>SQLServer_2019_Std</code>, <code>InstanceType</code> supports <code>HA</code> or <code>Basic</code>.</div>


* <div data-tips="true" data-tips-type="tip">When <code>DBEngineVersion</code> is set to <code>SQLServer_2019_Ent</code>, <code>InstanceType</code> supports <code>Cluster</code> or <code>Basic</code>.</div>


* <div data-tips="true" data-tips-type="tip">When <code>DBEngineVersion</code> is set to <code>SQLServer_2019_Web</code>, <code>InstanceType</code> supports <code>Basic</code>.</div>




**InstanceStatus ** <span data-label="purple">string </span>`Example value: Running`

The status of the instance. Valid values:


* `Running`: Running.

* `Creating`: creating.

* `Deleting`: deleting.

* `Restarting`: restarting.

* `Updating`: changing.

* `PrimaryChanging`: Primary node is switching.

* `Error`: Error.



**InstanceName ** <span data-label="purple">string </span>`Example: Instance example`

The instance name.



**InstanceId ** <span data-label="purple">string </span>`Example value: mssql-dab1be87****`

Instance ID.



**DBEngineVersion ** <span data-label="purple">string </span>`Example value: SQLServer_2019_Std`

Compatible version. The values are as follows:


* `SQLServer_2019_Std`: SQL Server 2019 Standard Edition.

* `SQLServer_2019_Web`: SQL Server 2019 Web Edition.

* `SQLServer_2019_Ent`: SQL Server 2019 Enterprise Edition.



**ChargeDetail ** <span data-label="purple">object </span>`Example value: None`

The payment method.


**AutoRenew ** <span data-label="purple">boolean </span>`Example value: false`

Specifies whether to enable auto\-renewal for prepaid instances.


* `true`: Auto\-renewal (Default).

* `false`: No auto\-renewal.



**ChargeStartTime ** <span data-label="purple">string </span>`Example value: 2023-02-03T06:16:03.000Z`

The billing start time in the yyyy\-MM\-ddTHH:mm:ssZ format (UTC).



**ChargeEndTime ** <span data-label="purple">string </span>`Example: 2023-03-02T15:59:59.000Z`

The charge expiration time in yyyy\-MM\-ddTHH:mm:ssZ format (UTC time).



**ChargeStatus ** <span data-label="purple">string </span>`Example value: Normal`

Billing status. Possible values:


* `Normal`: the instance is normal.

* `Overdue`: The instance is overdue.

* `Unpaid`: The instance is awaiting payment.



**ChargeType ** <span data-label="purple">string </span>`Example value: PostPaid`

Billing method. Possible values:


* `PostPaid`: Pay\-as\-you\-go.

* `PrePaid`: Subscription.



**OverdueReclaimTime ** <span data-label="purple">string </span>`Example value: 2023-03-09T15:59:59.000Z`

The estimated release time when shut down due to an overdue payment. The format is yyyy\-MM\-ddTHH:mm:ssZ (UTC time).



**OverdueTime ** <span data-label="purple">string </span>`Example: 2023-03-03T04:00:00.000Z`

The time when the instance is shut down due to an overdue payment, in yyyy\-MM\-ddTHH:mm:ssZ format (UTC).



**Period ** <span data-label="purple">integer </span>`Example value: 1`

The subscription duration for prepaid instances. Default value: `1`.



**PeriodUnit ** <span data-label="purple">string </span>`Example value: Month`

The subscription period for prepaid plans. Possible values:


* `Month`: A monthly subscription. This is the default value.

* `Year`: A yearly subscription.




**ReadOnlyNumber ** <span data-label="purple">integer </span>`Example value: 1`

The number of read\-only instances.



**PrimaryInstanceId ** <span data-label="purple">string </span>`Example value: mssql-h441603c68****`

Primary instance ID. If this parameter is empty, it indicates a Primary instance.



**InstanceCategory ** <span data-label="purple">string </span>`Example value: Primary`

Instance category. Possible values:


* `Primary`: The primary instance.

* `ReadOnly`: Read only instance.



**Tags ** <span data-label="purple">object[]</span>

Instance tags.


**Key** <span data-label="purple">string</span> `Example value: aa`

The tag key of the instance.



**Value ** <span data-label="purple">string </span>`Example value: bb`

The value of the instance tag.




**MaintenanceTime ** <span data-label="purple">string </span>`Example value: 22:00Z-02:59Z`

The maintenance window for the instance. Format: HH:mmZ\-HH:mmZ (UTC time).




&nbsp;

<span id=".6K-35rGC56S65L6L"></span>
## Request example

```text
POST /?Action=DescribeDBInstances&Version=2022-01-01 HTTP/1.1
Content-Type: application/json
Host: rds-mssql.cn-beijing.byteplusapi.com.cn
X-Date: 20230131T101010Z
Authorization: HMAC-SHA256 Credential=AKLTN2I0MmFiNzMxNWE5NDgzMzk4MmVjMTVkODlkZTZ****/20211202/cn-beijing/rds_mssql/request,SignedHeaders=x-date, Signature=71d31fc7bcf990142851c9833c5656391486cda0ae2e0b8ada733b7c6458****
{
    "InstanceStatus": "Running",
    "ChargeType": "PostPaid",
    "PageNumber": 1,
    "PageSize": 300
}
```


<span id=".6L-U5Zue56S65L6L"></span>
## Response example

```text
{
    "ResponseMetadata": {
        "RequestId": "202301312037457ABC7E1F36D470F8790C",
        "Action": "DescribeDBInstances",
        "Version": "2022-01-01",
        "Service": "rds_mssql",
        "Region": "cn-beijing"
    },
    "Result": {
        "InstancesInfo": [
            {
                "ChargeDetail": {
                    "AutoRenew": false,
                    "ChargeEndTime": "",
                    "ChargeStartTime": "2023-08-22T09:24:08.000Z",
                    "ChargeStatus": "Normal",
                    "ChargeType": "PostPaid",
                    "OverdueReclaimTime": "2200-01-15T16:00:00.000Z",
                    "OverdueTime": "",
                    "Period": 0,
                    "PeriodUnit": "Month"
                },
                "CreateTime": "2023-08-22T09:24:06.000Z",
                "DBEngineVersion": "SQLServer_2019_Std",
                "InstanceId": "mssql-30529c3d****",
                "InstanceName": "mssql-30529c3d****",
                "InstanceStatus": "Running",
                "InstanceType": "HA",
                "NodeDetailInfo": null,
                "NodeSpec": "rds.mssql.se.ha.d2.4c8g",
                "Port": "1433",
                "ProjectName": "",
                "RegionId": "cn-beijing",
                "ServerCollation": "Chinese_PRC_CI_AS",
                "StorageSpace": 20,
                "StorageType": "ESSDPL1",
                "SubnetId": "subnet-mjm6qdbzuio05smt1bwf****",
                "TimeZone": "China Standard Time",
                "VpcId": "vpc-13fuw95qz5fk03n6nu45b****",
                "ZoneId": "cn-beijing-a"
            },
            {
                "ChargeDetail": {
                    "AutoRenew": false,
                    "ChargeEndTime": "",
                    "ChargeStartTime": "2023-08-17T08:00:32.000Z",
                    "ChargeStatus": "Normal",
                    "ChargeType": "PostPaid",
                    "OverdueReclaimTime": "2200-01-15T16:00:00.000Z",
                    "OverdueTime": "",
                    "Period": 0,
                    "PeriodUnit": "Month"
                },
                "CreateTime": "2023-08-17T08:00:30.000Z",
                "DBEngineVersion": "SQLServer_2019_Std",
                "InstanceId": "mssql-bbe31c86****",
                "InstanceName": "测试实例",
                "InstanceStatus": "Running",
                "InstanceType": "HA",
                "NodeDetailInfo": null,
                "NodeSpec": "rds.mssql.se.ha.d2.4c8g",
                "Port": "1433",
                "ProjectName": "",
                "RegionId": "cn-beijing",
                "ServerCollation": "Chinese_PRC_CI_AS",
                "StorageSpace": 20,
                "StorageType": "ESSDPL1",
                "SubnetId": "subnet-mjm6qdbzuio05smt1bwf****",
                "TimeZone": "China Standard Time",
                "VpcId": "vpc-13fuw95qz5fk03n6nu45b****",
                "ZoneId": "cn-beijing-a"
            }
        ],
        "Total": 2
    }
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error code

The following table lists the business logic\-related error codes for this API. For public error codes, see the [Public Error Codes](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-error-codes) document.


|Status code |Error code |Error message |Description |
|---|---|---|---|
|400 |OperationDenied_ImportJobExists |The operation is not permitted due to existing running import jobs. |This action can not be performed because the current instance is running a data import task. |
|400 |UserBackupAmountOverTheLimit |The operation is not permitted due to the user backup amount over the limit. |The maximum number of manual backups has been reached. |
|400 |OperationDenied_BackupJobExists |The operation is not permitted due to exist running backup job. |This operation cannot be performed because the instance is currently running a backup task. |
|400 |OperationUnsupported |The operation is unsupported for the specified instance. |The action is not supported. |
|400 |InstanceIsNotRunning |The specified instance is not running. |The current instance is not in the Running state. |
|400 |OperationDenied_IncrBackupUnsupportRecovery |The operation is not permitted due to incr backup unsupport recovery. |This operation can not be performed on an incremental backup. |
|400 |MissingParameter |The input parameter %s that is mandatory for processing this request is not supplied. |Missing the {parameter1} parameter. |
|400 |InvalidDBName_Duplicate |The specified DBName already exists. |The database already exists. |
|400 |TosRestoreTaskDbVerifyFailed |db verify failed, reason:%s. |DB verification failed: {parameter1}. |
|400 |InvalidParameter |The specified parameter %s is not valid. |The value of Parameter {parameter1} is invalid. |
|400 |InvalidParameterFormat |The input parameter is not valid. |Invalid parameter. |
|403 |QuotaExceeded_RestoreDB |The quota of restore db exceeds. |The quota for database restores has been exceeded. |
|403 |OperationDenied_ResourceSoldOut |The requested resource is sold out in the specified zone; try other types of resources or other regions and zones. |The current availability zone has insufficient resources. |
|404 |BackupNotFound |The specified instance does not have available backup records. |No available backup records found. |
|404 |InstanceNotFound |The specified instance does not exist. |Instance not found. |
|500 |InternalError |The request failed with internal server error. |Internal error. |
|500 |TosRestoreTaskNumExceedLimit |Too many tasks are being executed. Please submit them later. |Too many tasks are currently running. Try submitting again later. |
