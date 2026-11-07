---
title: "DescribeDBInstanceDetail - Query instance details"
product: "RDS for SQL Server"
product_code: "RDS-for-SQL-Server"
source: "https://docs.byteplus.com/en/docs/RDS-for-SQL-Server/describedbInstancedetail"
---

Call the DescribeDBInstanceDetail API to query instance details. 

<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters

This section describes only the request parameters specific to this API and some common parameters. For more information, refer to [Common parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).



**Action ** <span data-label="purple">string </span><span data-api-tag="require|ZPWIYa">必选</span> `Example value: DescribeDBInstanceDetail`

The action to perform. The value is DescribeDBInstanceDetail.



**Version ** <span data-label="purple">string </span><span data-api-tag="require|q1FyIJ">必选</span> `Example value: 2022-01-01`

The API version is 2022\-01\-01.



**InstanceId ** <span data-label="purple">string </span><span data-api-tag="require|eeBqCw">必选</span> `Example value: mssql-dab1be87****`

Instance ID

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">You can call the <a href="https://docs.byteplus.com/en/docs/RDS-for-SQL-Server/describedbInstances">DescribeDBInstances</a> operation to query the instance ID.</div>




<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters

This section describes only the response parameters specific to this API. For more information, refer to [Return structure](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response).



**BasicInfo ** <span data-label="purple">object </span>`Example value: BasicInfo`

Instance basic information.


**Tags ** <span data-label="purple">object[] </span>`Example value: { "Key":"key", "Value":"value" }`

Instance tags. For more information, see [Data structure](https://docs.byteplus.com/en/docs/RDS-for-SQL-Server/data-structure?lang=en#tagfilterobject).


**Key** <span data-label="purple">string</span> `Example value: aa`

The tag key of the instance.



**Value ** <span data-label="purple">string </span>`Example value: bb`

The value of the instance tag.




**ReadOnlyNumber ** <span data-label="purple">integer </span>`Example value: 1`

The number of read\-only instances.



**PrimaryInstanceId ** <span data-label="purple">string </span>`Example value: mssql-e75beddc****`

Primary instance ID.



**BackupUse ** <span data-label="purple">float </span>`Example value: 1.42`

The backup space used by the instance. Unit: GiB.



**CreateTime ** <span data-label="purple">string </span>`Example value: 2023-12-26T02:32:36.000Z`

The time when the instance was created.



**DBEngineVersion ** <span data-label="purple">string </span>`Example value: SQLServer_2019_Std`<

Compatible version.< The values are as follows:


* `SQLServer_2019_Std`: SQL Server 2019 Standard Edition.

* `SQLServer_2019_Web`: SQL Server 2019 Web Edition.

* `SQLServer_2019_Ent`: SQL Server 2019 Enterprise Edition.



**InstanceId ** <span data-label="purple">string </span>`Example value: mssql-dab1be87****`

Instance ID.



**InstanceName ** <span data-label="purple">string </span>`Example: Instance example`

The instance name.



**InstanceStatus ** <span data-label="purple">string </span>`Example value: Running`

The status of the instance. Valid values:


* `Running`: Running.

* `Creating`: creating.

* `Deleting`: deleting.

* `Restarting`: restarting.

* `Updating`: changing.

* `MasterChanging`: Primary node is switching.

* `Error`: Error.



**InstanceType ** <span data-label="purple">string </span>`Example value: HA`

Instance type. The values are as follows:


* `HA`: Indicates the High Availability type.

* `Basic`: Indicates the single\-node edition type.

* `Cluster` represents the Cluster edition type.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">When <code>DBEngineVersion</code> is set to <code>SQLServer_2019_Std</code>, <code>InstanceType</code> supports <code>HA</code> or <code>Basic</code>.</div>


* <div data-tips="true" data-tips-type="tip">When <code>DBEngineVersion</code> is set to <code>SQLServer_2019_Ent</code>, <code>InstanceType</code> supports <code>Cluster</code> or <code>Basic</code>.</div>


* <div data-tips="true" data-tips-type="tip">When <code>DBEngineVersion</code> is set to <code>SQLServer_2019_Web</code>, <code>InstanceType</code> supports <code>Basic</code>.</div>




**Memory ** <span data-label="purple">integer </span>`Example value: 16`

Memory size in GiB.



**NodeSpec ** <span data-label="purple">string </span>`Example value: rds.mssql.ee.ha.x8.4c32g`

Master node specifications.



**ProjectName ** <span data-label="purple">string </span>`Example value: Test`

Project.



**RegionId ** <span data-label="purple">string </span>`Example value: cn-beijing`

Region ID.



**SlowQueryEnable ** <span data-label="purple">boolean </span>`Example value: false`

Indicates whether the slow query log is enabled. The values are as follows:


* `true`: The slow query log is enabled.

* `false`: The slow query log is disabled.



**SlowQueryTime ** <span data-label="purple">string </span>`Example value: 1`

The threshold for the slow query log. The value ranges from 1 to 10. Unit: seconds (s).



**StorageSpace ** <span data-label="purple">integer </span>`Example value: 200`

Total instance storage space. Unit: GiB.



**StorageType ** <span data-label="purple">string </span>`Example value: ESSDPL1`

The storage type of the instance. A value of `ESSDPL1` indicates Extreme Speed SSD PL1.



**StorageUse ** <span data-label="purple">float </span>`Example value: 1.85`

The storage space used by the instance. Unit: GiB.



**SubnetId ** <span data-label="purple">string </span>`Example value: subnet-rroau2hdn1mov0x57f7****`

Subnet ID.



**TimeZone ** <span data-label="purple">string </span>`Example value: China Standard Time`

Time zone.



**UpdateTime ** <span data-label="purple">string </span>`Example value: 2024-01-03T07:15:08.000Z`

The time when the instance was updated.



**VCPU ** <span data-label="purple">integer </span>`Example value: 4`

CPU size. For example, 1 indicates 1 core.



**VpcId ** <span data-label="purple">string </span>`Example value: vpc-13g2qkkzntfy83n6nu4z1****`

Virtual private cloud (VPC) ID.



**ZoneId ** <span data-label="purple">string </span>`Example value: cn-beijing-a`

Availability zone ID.



**InnerVersion ** <span data-label="purple">string </span>`Example value: 15.0.4335.1`

The kernel version number.



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



**MaintenanceTime ** <span data-label="purple">string </span>`Example value: 22:00Z-02:59Z`

The maintenance window for the instance. Format: HH:mmZ\-HH:mmZ (UTC time).




**ChargeDetail ** <span data-label="purple">object </span>`Example value: ChargeDetail`

Billing method.


**AutoRenew ** <span data-label="purple">boolean </span>`Example value: false`

Specifies whether to enable auto\-renewal for prepaid instances.


* `true`: Auto\-renewal (Default).

* `false`: No auto\-renewal.



**ChargeStartTime ** <span data-label="purple">string </span>`Example value: 2023-02-03T06:16:03.000Z`

The billing start time in the yyyy\-MM\-ddTHH:mm:ssZ format (UTC).



**ChargeEndTime ** <span data-label="purple">string </span>`Example value: 2023-03-02T15:59:59.000Z`

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

The billing cycle for prepaid instances.


* `Month`: Indicates a monthly subscription (default).

* `Year`: A yearly subscription.




**ConnectionInfo ** <span data-label="purple">object[] </span>`Example value: ConnectionInfo`

The connection information for the instance.


**Description ** <span data-label="purple">string </span>`Example value: None`

The description.



**EndpointId ** <span data-label="purple">string </span>`Example value: mssql-dab1be87****-primary`

The endpoint ID.



**EndpointName ** <span data-label="purple">string </span>`Example value: Primary connection endpoint`

The name of the endpoint.



**Address ** <span data-label="purple">object[] </span>`Example value: None`

The address information.


**Domain ** <span data-label="purple">string </span>`Example: mssqldab1be87****.rds-mssql.ivolces.com`

Connection domain.



**EipId ** <span data-label="purple">string </span>`Example value: eip-5go6uulm687473inqk15****`

The ID of the EIP, which is only valid for public network addresses.



**IPAddress ** <span data-label="purple">string </span>`Example value: 10.1.2.3`

IP address.



**Port ** <span data-label="purple">string </span>`Example value: 1433`

Port.



**SubnetId ** <span data-label="purple">string </span>`Example value: subnet-2bzup883l93402dx0efe1****`

The subnet ID, which is valid only for private network addresses.



**DNSVisibility ** <span data-label="purple">boolean </span>`Example value: false`

Specifies whether to enable private\-to\-public network resolution. The valid values are as follows:


* `true`: Enables private\-to\-public network resolution.

* `false`: Disables private\-to\-public network resolution.



**NetworkType ** <span data-label="purple">string </span>`Example value: Private`

Network address type. Possible values:


* `Private`: Private network type.

* `Public`: Public network type.




**EndpointType ** <span data-label="purple">string </span>`Example value: Primary`

Endpoint type. The values are as follows:


* `Primary`: The primary node endpoint.

* `ROCluster`: The read\-only cluster endpoint.

* `RO`: Read\-only node endpoint.




**NodeDetailInfo ** <span data-label="purple">object[] </span>`Example value: NodeDetailInfo`

Instance node information.


**CreateTime ** <span data-label="purple">string </span>`Example value: 2024-01-02T11:17:33.000Z`

The creation time of the node.



**InstanceId ** <span data-label="purple">string </span>`Example value: mssql-93420fe2****`

Instance ID.



**Memory ** <span data-label="purple">integer </span>`Example value: 8`

Memory size, in GiB.



**NodeId** <span data-label="purple">string</span> `Example value: mssql-dab1be87****-0`

Node ID.



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




<span id=".6K-35rGC56S65L6L"></span>
## Request example

```JSON
POST /?Action=DescribeDBInstanceDetail&Version=2022-01-01 HTTP/1.1
Content-Type: application/json
Host: rds-mssql.cn-beijing.byteplusapi.com.cn
X-Date: 20230131T101010Z
Authorization: HMAC-SHA256 Credential=AKLTN2I0MmFiNzMxNWE5NDgzMzk4MmVjMTVkODlkZTZ****/20211202/cn-beijing/rds_mssql/request,SignedHeaders=x-date, Signature=71d31fc7bcf990142851c9833c5656391486cda0ae2e0b8ada733b7c6458****
{
    "InstanceId": "mssql-dab1be87****"
}
```


<span id=".6L-U5Zue56S65L6L"></span>
## Response example

```json
{
  "ResponseMetadata": {
    "RequestId": "202401081027172E3CCD0F346C0D1C9A2D",
    "Action": "DescribeDBInstanceDetail",
    "Version": "2022-01-01",
    "Service": "rds_mssql",
    "Region": "cn-beijing"
  },
  "Result": {
    "BasicInfo": {
      "BackupUse": 1662.47,
      "CreateTime": "2023-10-17T08:54:16.000Z",
      "DBEngineVersion": "SQLServer_2019_Std",
      "InnerVersion": "SQLServer_2019_Std",
      "InstanceId": "mssql-6fca82fa****",
      "InstanceName": "mssql-6fca82fa****",
      "InstanceStatus": "Running",
      "InstanceType": "HA",
      "Memory": 8,
      "NodeSpec": "rds.mssql.se.ha.d2.4c8g",
      "PrimaryInstanceId": "",
      "ProjectName": "default",
      "ReadOnlyNumber": 0,
      "RegionId": "cn-beijing",
      "ServerCollation": "Chinese_PRC_CI_AS",
      "SlowQueryEnable": false,
      "SlowQueryTime": "1",
      "StorageSpace": 1500,
      "StorageType": "ESSDPL1",
      "StorageUse": 634.66,
      "SubnetId": "subnet-13f4n08ww1d6o3n6nu5g0****",
      "Tags": [
        {
          "Key": "test",
          "Value": "test"
        }
      ],
      "TimeZone": "China Standard Time",
      "UpdateTime": "2023-12-04T06:26:49.000Z",
      "VCPU": 4,
      "VpcId": "vpc-13f4mzhagglj43n6nu500****",
      "ZoneId": "cn-beijing-a"
    },
    "ChargeDetail": {
      "AutoRenew": false,
      "ChargeEndTime": "",
      "ChargeStartTime": "2023-10-17T08:54:18.000Z",
      "ChargeStatus": "Normal",
      "ChargeType": "PostPaid",
      "OverdueReclaimTime": "2200-01-15T16:00:00.000Z",
      "OverdueTime": "",
      "Period": 0,
      "PeriodUnit": "Month"
    },
    "ConnectionInfo": [
      {
        "Address": [
          {
            "DNSVisibility": false,
            "Domain": "mssql6fca82fa****.rds-mssql.ivolces.com",
            "EipId": "",
            "IPAddress": "192.168.0.17",
            "NetworkType": "Private",
            "Port": "1433",
            "SubnetId": "subnet-13f4n08ww1d6o3n6nu5g0****"
          }
        ],
        "Description": "",
        "EndpointId": "mssql-6fca82fa****-primary",
        "EndpointName": "",
        "EndpointType": "Primary"
      }
    ],
    "NodeDetailInfo": [
      {
        "CreateTime": "2023-10-17T08:54:16.000Z",
        "InstanceId": "mssql-6fca82fa****",
        "Memory": 8,
        "NodeIP": "192.168.***.***",
        "NodeId": "mssql-6fca82fa****-0",
        "NodeSpec": "rds.mssql.se.ha.d2.4c8g",
        "NodeStatus": "Running",
        "NodeType": "Secondary",
        "RegionId": "cn-beijing",
        "UpdateTime": "2023-12-04T06:26:49.000Z",
        "VCPU": 4,
        "ZoneId": "cn-beijing-a"
      },
      {
        "CreateTime": "2023-10-17T08:54:16.000Z",
        "InstanceId": "mssql-6fca82fa****",
        "Memory": 8,
        "NodeIP": "192.168.***.***",
        "NodeId": "mssql-6fca82fa****-1",
        "NodeSpec": "rds.mssql.se.ha.d2.4c8g",
        "NodeStatus": "Running",
        "NodeType": "Primary",
        "RegionId": "cn-beijing",
        "UpdateTime": "2023-12-04T06:26:49.000Z",
        "VCPU": 4,
        "ZoneId": "cn-beijing-a"
      }
    ]
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
|400 |OperationDenied_BackupJobExists |The operation is not permitted due to running backup jobs. |This operation cannot be performed because the instance is currently running a backup task. |
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
|404 |BackupNotFound |The specified instance does not exist available backup records. |No available backup records found. |
|404 |InstanceNotFound |The specified instance does not exist. |Instance not found. |
|500 |InternalError |The request failed with internal server error. |Internal error. |
|500 |TosRestoreTaskNumExceedLimit |Too many tasks are being executed. Please submit them later. |Too many tasks are being executed. Try again later. |
