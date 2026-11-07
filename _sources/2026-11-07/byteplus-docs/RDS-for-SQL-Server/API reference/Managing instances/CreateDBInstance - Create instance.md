---
title: "CreateDBInstance - Create instance"
product: "RDS for SQL Server"
product_code: "RDS-for-SQL-Server"
source: "https://docs.byteplus.com/en/docs/RDS-for-SQL-Server/createdbInstance"
---

Call the CreateDBInstance API to create an instance.

<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters

This section describes only the request parameters specific to this API and some common parameters. For more information, refer to [Common parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).



**Action** <span data-label="purple">string</span> <span data-api-tag="require|JpA5Jw">必选</span> `Example value: CreateDBInstance`

The action to perform. Value: `CreateDBInstance`.



**Version ** <span data-label="purple">string </span><span data-api-tag="require|GV9Tai">必选</span> `Example value: 2022-01-01`

The API version is `2022-01-01`.



**MaintenanceTime** <span data-label="purple">string</span> `Optional` `Example: 22:00Z-02:59Z`

The maintenance window for the instance. Format: HH:mmZ\-HH:mmZ (UTC time). The default is 18:00–21:59 UTC (2:00–5:59 Beijing time).

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">The system performs periodic maintenance on instances to ensure the stability of cloud databases. Set the maintenance window during off\-peak hours to avoid affecting your business.</div>


* <div data-tips="true" data-tips-type="tip">During the maintenance window, your instance may experience 1 to 2 transient disconnections. Ensure your application has an automatic reconnection mechanism.</div>


* <div data-tips="true" data-tips-type="tip">The maintenance window duration ranges from 1 to 24 hours. The selected time range can not span across two days.</div>




**DBEngineVersion ** <span data-label="purple">string </span><span data-api-tag="require|53MyIt">必选</span> `Example value: SQLServer_2019_Std`

Compatible versions. The values are as follows:


* `SQLServer_2019_Std`: SQL Server 2019 Standard Edition.

* `SQLServer_2019_Ent`: SQL Server 2019 Enterprise Edition.

* `SQLServer_2019_Web`: SQL Server 2019 Web Edition.

* `SQLServer_2022_Std`: Indicates SQL Server 2022 Standard Edition.

* `SQLServer_2022_Ent`: Indicates SQL Server 2022 Enterprise Edition.

* `SQLServer_2022_Web`: Indicates SQL Server 2022 Web Edition.



**InstanceType ** <span data-label="purple">string </span><span data-api-tag="require|133mRX">必选</span> `Example value: HA`

Instance type. The values are as follows:


* `HA`: Indicates the High Availability type.

* `Basic`: Indicates the single\-node edition type.

* `Cluster`: Indicates the Cluster edition type.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">When <code>DBEngineVersion</code> is set to <code>SQLServer_2019_Std</code> or <code>SQLServer_2022_Std</code>, <code>InstanceType</code> can be set to <code>HA</code> or <code>Basic</code>.</div>


* <div data-tips="true" data-tips-type="tip">When <code>DBEngineVersion</code> is set to <code>SQLServer_2019_Ent</code> or <code>SQLServer_2022_Ent</code>, <code>InstanceType</code> can be set to <code>Cluster</code> or <code>Basic</code>.</div>


* <div data-tips="true" data-tips-type="tip">When <code>DBEngineVersion</code> is set to <code>SQLServer_2019_Web</code> or <code>SQLServer_2022_Web</code>, <code>InstanceType</code> can be set to <code>Basic</code>.</div>




**ZoneId ** <span data-label="purple">string </span><span data-api-tag="require|GMJEZQ">必选</span> `Example value: cn-beijing-a`

The availability zone where the node resides. When the primary and secondary nodes are in different availability zones, separate the zones with a semicolon (;). The first availability zone is for the primary node, and the second is for the secondary node.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Call the <a href="https://docs.byteplus.com/en/docs/RDS-for-SQL-Server/describeavailabilityzones">DescribeAvailabilityZones</a> API to query availability zones.</div>




**NodeSpec ** <span data-label="purple">string </span><span data-api-tag="require|FNkFIo">必选</span> `Example value: rds.mssql.se.ha.d4.4c16g`

Instance specification code. For more information about instance specification codes, see [Product specifications](https://docs.byteplus.com/en/docs/RDS-for-SQL-Server/master-instance-specification).



**StorageSpace ** <span data-label="purple">integer </span><span data-api-tag="require|qaI6dH">必选</span> `Example value: 100`

The storage space size in GiB. The value ranges from 20 GiB to 4000 GiB, in increments of 10 GiB.



**VpcId ** <span data-label="purple">string </span><span data-api-tag="require|Dq2ZHD">必选</span> `Example: VPC123456`

Virtual private cloud (VPC) ID.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Call the <a href="https://docs.byteplus.com/en/docs/vpc/DescribeVpcs">DescribeVpcs</a> operation to query virtual private clouds that meet specified conditions.</div>




**SubnetId ** <span data-label="purple">string </span><span data-api-tag="require|rUC8xC">必选</span> `Example value: Subnet123456`

The subnet ID. If the primary and secondary nodes are in different availability zones, their subnets must be set within the virtual private cloud of their respective availability zones. Use a semicolon (;) to separate multiple availability zones.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">You can call the <a href="https://docs.byteplus.com/en/docs/vpc/DescribeSubnets">DescribeSubnets</a> API to query the subnet ID.</div>




**SuperAccountPassword ** <span data-label="purple">string </span><span data-api-tag="require|JaXhgh">必选</span> `Example value: Test@123456`

The password for the super account. The password must meet the following requirements:


* It must be 8 to 32 characters long.

* It must contain at least three of the following character types: uppercase letters, lowercase letters, numbers, and special characters.

* Special characters are `!@#$%^&*()_+-=`.



**DBTimeZone ** <span data-label="purple">string </span><span data-api-tag="require|e1KejI">必选</span> `Example value: China Standard Time`

Time zone. Only `China Standard Time` is supported.



**ChargeInfo ** <span data-label="purple">object </span><span data-api-tag="require|wzPKSp">必选</span> `Example value: { "ChargeType": "PostPaid", "Number": 1 }`

The billing method. For more information about `ChargeInfo`, see [Data structure](https://docs.byteplus.com/en/docs/RDS-for-SQL-Server/data-structure#chargeinfoobject).


**ChargeType ** <span data-label="purple">string </span><span data-api-tag="require|g7LUff">必选</span> `Example: PostPaid`

Payment type. Possible values:


* `PostPaid`: Pay\-as\-you\-go.

* `PrePaid`: Subscription.



**AutoRenew** <span data-label="purple">boolean</span> `Optional` `Example value: true`

Specifies whether to enable automatic renewal in a prepaid scenario. This parameter can be set when `ChargeType` is `Prepaid`.


* `true`: Enables automatic renewal (default value).

* `false`: Disables automatic renewal.



**PeriodUnit** <span data-label="purple">string</span> `Optional` `Example value: Month`

The purchase period for prepaid plans. This parameter can be set when `ChargeType` is `Prepaid`.


* `Month`: A monthly subscription (default).

* `Year`: A yearly subscription.



**Period** <span data-label="purple">integer</span> `Optional` `Example value: 1`

The subscription duration for prepaid instances. This parameter is required when `ChargeType` is set to `Prepaid`.



**Number** <span data-label="purple">integer</span> `Optional` `Example value: 1`

The number of instances to purchase. Default value: `1` The value range is `[1,10]`.




**InstanceName** <span data-label="purple">string</span> `Optional` `Example value: Name123`

Instance name. The naming rules for the instance name are as follows:


* It cannot start with a number or a hyphen.

* It can only contain Chinese characters, letters, numbers, underscores, and hyphens.

* The length must be between 1 and 128 characters.



**Tags** <span data-label="purple">object[]</span> `Optional` `Example: {\"Key\":\"key\", \"Value\":\"value\"}`

Instance tags. For more information, see [Data structure](https://docs.byteplus.com/en/docs/RDS-for-SQL-Server/data-structure#tagsobject).


**Key ** <span data-label="purple">string </span><span data-api-tag="require|EFzaOZ">必选</span> `Example value: aa`

The tag key for the instance.



**Value ** <span data-label="purple">string </span><span data-api-tag="require|Dxahzc">必选</span>Required</a\> `Example value: bb`

The value of the instance tag.




**ServerCollation** <span data-label="purple">string</span> `Optional` `Example: Chinese_PRC_CI_AS`

The default instance character set collation is `Chinese_PRC_CI_AS`. Most native character sets are supported. The values are as follows:


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



**ProjectName** <span data-label="purple">string</span> `Optional` `Example value: default`

The project to which it belongs. The default value is empty.



**AllowListIds** <span data-label="purple">string[]</span> `Optional` `Example: [ "acl-a29be2559dc4406883d358892b90****", "acl-ded4c0b707e44efd8f0dbc4e88f5****" ]`

The allowlist IDs. To bind multiple allowlists, separate the Allowlist IDs with commas (,).

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">An instance can bind a maximum of 100 allowlists.</div>




<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters

This section describes only the response parameters specific to this API. For more information, refer to [Return structure](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response).



**InstanceId ** <span data-label="purple">string </span>`Example value: mssql-44171da8****`

Instance ID.



**OrderId ** <span data-label="purple">string </span>`Example value: Order719479011897090****`

The order ID.



<span id=".6K-35rGC56S65L6L"></span>
## Request example

```JSON
POST /?Action=CreateDBInstance&Version=2022-01-01 HTTP/1.1
Content-Type: application/json
Host: rds-mssql.cn-beijing.byteplusapi.com.cn
X-Date: 20230131T101010Z
Authorization: HMAC-SHA256 Credential=AKLTN2I0MmFiNzMxNWE5NDgzMzk4MmVjMTVkODlkZTZ****/20211202/cn-beijing/rds_mssql/request,SignedHeaders=x-date, Signature=71d31fc7bcf990142851c9833c5656391486cda0ae2e0b8ada733b7c6458****
{
    "DBEngineVersion":"SQLServer_2019_Std",
    "InstanceType":"HA",
    "ZoneId":"cn-beijing-a",
    "NodeSpec":"rds.mssql.se.ha.d4.4c16g",
    "StorageSpace":20,
    "VpcId":"vpc-2d5xeur6hiscg58ozfcuq****",
    "SubnetId":"subnet-2bzup883l93402dx0efe1****",
    "InstanceName":"实例样例",
    "SuperAccountPassword":"Admin@123",
    "ServerCollation":"Chinese_PRC_CI_AS",
    "Tags":[
        {
            "Key":"key1",
            "Value":"value1"
        },
        {
            "Key":"key2",
            "Value":"value2"
        }
    ],
    "DBTimeZone":"China Standard Time",
    "ProjectName":"default",
    "ChargeInfo":{
        "ChargeType":"PostPaid",
        "Number":1
    }
}

```


<span id=".6L-U5Zue56S65L6L"></span>
## Response example

```JSON
{
    "ResponseMetadata": {
        "RequestId": "202301312022404400C80FE28234E9F81D",
        "Action": "CreateDBInstance",
        "Version": "2022-01-01",
        "Service": "rds_mssql",
        "Region": "cn-beijing"
    },
    "Result": {
        "InstanceId": "mssql-44171da8****",
        "OrderId": "Order719479011897090****"
    }
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error code

The following table lists the business logic\-related error codes for this API. For public error codes, see the [Public Error Codes](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-error-codes) document.


|Status code |Error code |Error message |Description |
|---|---|---|---|
|400 |OperationDenied_ImportJobExists |The operation is not permitted due to existing running import jobs. |This action can not be performed because the current instance is running a data import task. |
|400 |UserBackupAmountOverTheLimit |The operation is not permitted due to the user backup amount over the limit. |The number of manual backups exceeds the limit. |
|400 |OperationDenied_BackupJobExists |The operation is not permitted due to running backup jobs. |This operation cannot be performed because the instance is currently running a backup task. |
|400 |OperationUnsupported |The operation is unsupported for the specified instance. |Operation not supported. |
|400 |InstanceIsNotRunning |The specified instance is not running. |The current instance is not in the Running state. |
|400 |OperationDenied_IncrBackupUnsupportRecovery |The operation is not permitted due to incr backup unsupport recovery. |This operation can not be performed on an incremental backup. |
|400 |MissingParameter |The input parameter %s that is mandatory for processing this request is not supplied. |Missing the {parameter1} parameter. |
|400 |InvalidDBName_Duplicate |The specified DBName already exists. |The database already exists. |
|400 |TosRestoreTaskDbVerifyFailed |db verify failed, reason:%s. |DB verification failed: {parameter1}. |
|400 |InvalidParameter |The specified parameter %s is not valid. |The value of Parameter {parameter1} is invalid. |
|400 |InvalidParameterFormat |The input parameter is not valid. |Invalid parameter. |
|400 |QuotaExceeded |The Instance Number has exceeded quota %d. |The number of instances exceeds the quota of {parameter1}. |
|403 |QuotaExceeded_RestoreDB |The quota of restore db exceeds. |The quota for database restores has been exceeded. |
|403 |OperationDenied_ResourceSoldOut |The requested resource is sold out in the specified zone; try other types of resources or other regions and zones. |The current availability zone has insufficient resources. |
|404 |BackupNotFound |The specified instance does not have available backup records. |No available backup records found. |
|404 |InstanceNotFound |The specified instance does not exist. |Instance not found. |
|500 |InternalError |The request failed with internal server error. |Internal error. |
|500 |TosRestoreTaskNumExceedLimit |Too many tasks are being executed. Please submit them later. |Too many tasks are currently running. Try submitting again later. |
