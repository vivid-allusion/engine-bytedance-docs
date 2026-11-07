---
title: "DescribeDBInstanceSpecs - Query supported specifications"
product: "RDS for MySQL"
product_code: "RDS_for_MySQL"
source: "https://docs.byteplus.com/en/docs/RDS_for_MySQL/describedbinstancespecs"
---

Call the DescribeDBInstanceSpecs API to query the supported specifications for MySQL.

<span id=".6K-35rGC57G75Z6L"></span>
## Request type

Synchronous request.

<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters


|Parameter |Type |Is it required? |Sample value |Description |
|---|---|---|---|---|
|DBEngineVersion |String |No |MySQL_8_0 |Compatible version. Values:<br><br><br>* `MySQL_5_7`: MySQL 5.7. Default value.<br><br>* `MySQL_8_0`: MySQL 8.0.<br><br>* `MySQL 8.4`: MySQL 8.4. |
|SpecCode |String |No |rds.mysql.1c2g |Instance specification code. |
|ZoneId |String |No |beijing\-a |Availability zone ID. |
|InstanceType |String |No |DoubleNode |Instance type. Values:<br><br><br>* `DoubleNode`, Double node type.<br><br>* `MultiNode`, multiple node type.<br><br>* `SingleNode`, Single node type.<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">If the blue instance is a single\-node type, you can select a single\-node or double\-node type for the green instance.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">If the blue instance is a double\-node type, you can select a double\-node or multiple\-node type for the green instance.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">If the blue instance is a multiple\-node type, you can only select the multiple\-node type for the green instance.</div><br> |
|SpecFamily |String |No |General |Instance specification type. Values:<br><br><br>* `General`, a general\-type specification.<br><br>* `Shared`: a shared\-type specification. |
|StorageType |String |No |LocalSSD |The storage type of the instance. Range:<br><br><br>* `LocalSSD`: local SSD.<br><br>* `CloudESSD_FlexPL`: Cloud ESSD FlexPL.<br><br>* `CloudESSD_PL0`: Cloud ESSD PL0.<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">The StorageType parameter is required if you set the StorageSpace parameter.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">When the InstanceType is set to <code>SingleNode</code>, the StorageType can only be <code>CloudESSD_FlexPL</code> or <code>CloudESSD_PL0</code>.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">This parameter has different value ranges for different APIs. The rules are as follows:</div><br><br><br>   * <div data-tips="true" data-tips-type="tip">When used as a request parameter in the following APIs, StorageType can only be <code>LocalSSD</code>.</div><br><br><br>      * <div data-tips="true" data-tips-type="tip">RestoreToCrossRegionInstance</div><br><br><br>      * <div data-tips="true" data-tips-type="tip">RestoreToNewInstanceFromUserTos</div><br><br><br>* <div data-tips="true" data-tips-type="tip">When used as a request parameter for some API operations, the value range of this parameter is related to the storage type of the original instance. The specific rules are as follows:</div><br><br><br>   * <div data-tips="true" data-tips-type="tip">If the original instance storage type is <code>LocalSSD</code> or <code>CloudESSD_FlexPL</code>, changing the storage type is not supported.</div><br><br><br>   * <div data-tips="true" data-tips-type="tip">If the original instance storage type is <code>CloudESSD_PL0</code>, the value can be <code>CloudESSD_PL0</code> or <code>CloudESSD_FlexPL</code>.</div><br><br><br>      <div data-tips="true" data-tips-type="tip">The related APIs are:      </div><br>      <br><br>      * <div data-tips="true" data-tips-type="tip">RebuildDBInstance</div><br><br><br>      * <div data-tips="true" data-tips-type="tip">RestoreToNewInstance</div><br><br><br>      * <div data-tips="true" data-tips-type="tip">ModifyDBNodeSpec</div><br> |


<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters


|Parameter |Type |Sample value |Description |
|---|---|---|---|
|InstanceSpecsInfo |Array of [InstanceSpecsInfoObject](https://docs.byteplus.com/en/docs/40/15518#instancespecsinfoobject) |Refer to the Sample response. |Specification list. |


<span id="instancespecsinfoobject"></span>
### InstanceSpecsInfoObject


|Parameter |Type |Sample value |Description |
|---|---|---|---|
|Connection |Integer |2000 |The default maximum number of connections. |
|DBEngineVersion |String |MySQL_8_0 |Compatible version. Values:<br><br><br>* `MySQL_5_7`: MySQL 5.7.<br><br>* `MySQL_8_0`: MySQL 8.0.<br><br>* `MySQL 8.4`: MySQL 8.4. |
|IOPS |Integer |1000 |Maximum IOPS. |
|InstanceType |String |DoubleNode |Instance type. The value is `DoubleNode`. |
|Memory |Integer |50 |Memory size. Unit is GiB. |
|QPS |Integer |0 |QPS. |
|SpecCode |String |rds.mysql.1c2g |Instance specification code. |
|RegionId |String |cn\-beijing |Supported region ID. |
|SpecFamily |String |General |Instance specification type. Values:<br><br><br>* `General`: dedicated type (formerly "general type").<br><br>* `Shared`: general type (formerly "shared type"). |
|SpecStatus |String |Normal |State of the specification in the availability zone, including the following:<br><br><br>* `Normal`: available for sale.<br><br>* `Soldout`: sold out. |
|StorageMax |Integer |3000 |Maximum disk size in GiB. |
|StorageMin |Integer |100 |The minimum disk specification in GiB. |
|StorageStep |Integer |100 |The disk step size in GiB. |
|VCPU |Integer |1 |CPU size. For example: 1 indicates 1U. |
|ZoneId |String |cn\-beijing\-a |Supported availability zone ID. |
|StorageType |String |LocalSSD |The storage type of the instance. Range:<br><br><br>* `LocalSSD`: local SSD.<br><br>* `CloudESSD_FlexPL`: Cloud ESSD FlexPL.<br><br>* `CloudESSD_PL0`: Cloud ESSD PL0.<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">The StorageType parameter is required if you set the StorageSpace parameter.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">When the InstanceType is set to <code>SingleNode</code>, the StorageType can only be <code>CloudESSD_FlexPL</code> or <code>CloudESSD_PL0</code>.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">This parameter has different value ranges for different APIs. The rules are as follows:</div><br><br><br>   * <div data-tips="true" data-tips-type="tip">When used as a request parameter in the following APIs, StorageType can only be <code>LocalSSD</code>.</div><br><br><br>      * <div data-tips="true" data-tips-type="tip">RestoreToCrossRegionInstance</div><br><br><br>      * <div data-tips="true" data-tips-type="tip">RestoreToNewInstanceFromUserTos</div><br><br><br>* <div data-tips="true" data-tips-type="tip">When used as a request parameter for some API operations, the value range of this parameter is related to the storage type of the original instance. The specific rules are as follows:</div><br><br><br>   * <div data-tips="true" data-tips-type="tip">If the original instance storage type is <code>LocalSSD</code> or <code>CloudESSD_FlexPL</code>, changing the storage type is not supported.</div><br><br><br>   * <div data-tips="true" data-tips-type="tip">If the original instance storage type is <code>CloudESSD_PL0</code>, the value can be <code>CloudESSD_PL0</code> or <code>CloudESSD_FlexPL</code>.</div><br><br><br>      <div data-tips="true" data-tips-type="tip">The related APIs are:      </div><br>      <br><br>      * <div data-tips="true" data-tips-type="tip">RebuildDBInstance</div><br><br><br>      * <div data-tips="true" data-tips-type="tip">RestoreToNewInstance</div><br><br><br>      * <div data-tips="true" data-tips-type="tip">ModifyDBNodeSpec</div><br> |


<span id=".56S65L6L"></span>
## Sample

<span id=".6K-35rGC56S65L6L"></span>
### Sample request

```json
POST /?Action=DescribeDBInstanceSpecs&Version=2022-01-01 HTTP/1.1
Accept: application/json
Content-Type: application/json
Host: rds-mysql.cn-beijing.byteplusapi.com.cn
X-Date: 20211202T101010Z
Authorization: HMAC-SHA256 Credential=AKLTN2I0MmFiNzMxNWE5NDgzMzk4MmVjMTVkODlkZTZ****/20211202/cn-beijing/rds_mysql/request,SignedHeaders=x-date, Signature=71d31fc7bcf990142851c9833c5656391486cda0ae2e0b8ada733b7c6458****
{
    "DBEngineVersion": "MySQL_8_0"
}
```


<span id=".6L-U5Zue56S65L6L"></span>
### Sample response

```json
{
    "ResponseMetadata": {
        "RequestId": "20230810141234966A39B950F7BE686AC1",
        "Action": "DescribeDBInstanceSpecs",
        "Version": "2022-01-01",
        "Service": "rds_mysql",
        "Region": "cn-beijing"
    },
    "Result": {
        "InstanceSpecsInfo": [
            {
                "Connection": 600,
                "DBEngineVersion": "MySQL_8_0",
                "IOPS": 1000,
                "InstanceType": "DoubleNode",
                "Memory": 2,
                "QPS": 0,
                "RegionId": "cn-beijing",
                "SpecCode": "rds.mysql.1c2g",
                "SpecFamily": "General",
                "SpecStatus": "Normal",
                "StorageMax": 6000,
                "StorageMin": 20,
                "StorageStep": 100,
                "VCPU": 1,
                "ZoneId": ""
            },
            {
                "Connection": 1200,
                "DBEngineVersion": "MySQL_8_0",
                "IOPS": 2000,
                "InstanceType": "DoubleNode",
                "Memory": 4,
                "QPS": 0,
                "RegionId": "cn-beijing",
                "SpecCode": "rds.mysql.2c4g",
                "SpecFamily": "General",
                "SpecStatus": "Normal",
                "StorageMax": 6000,
                "StorageMin": 20,
                "StorageStep": 100,
                "VCPU": 2,
                "ZoneId": ""
            },
            {
                "Connection": 2000,
                "DBEngineVersion": "MySQL_8_0",
                "IOPS": 4000,
                "InstanceType": "DoubleNode",
                "Memory": 8,
                "QPS": 0,
                "RegionId": "cn-beijing",
                "SpecCode": "rds.mysql.2c8g",
                "SpecFamily": "General",
                "SpecStatus": "Normal",
                "StorageMax": 6000,
                "StorageMin": 20,
                "StorageStep": 100,
                "VCPU": 2,
                "ZoneId": ""
            },
            {
                "Connection": 4000,
                "DBEngineVersion": "MySQL_8_0",
                "IOPS": 6000,
                "InstanceType": "DoubleNode",
                "Memory": 16,
                "QPS": 0,
                "RegionId": "cn-beijing",
                "SpecCode": "rds.mysql.2c16g",
                "SpecFamily": "General",
                "SpecStatus": "Normal",
                "StorageMax": 6000,
                "StorageMin": 20,
                "StorageStep": 100,
                "VCPU": 2,
                "ZoneId": ""
            },
            {
                "Connection": 2000,
                "DBEngineVersion": "MySQL_8_0",
                "IOPS": 5000,
                "InstanceType": "DoubleNode",
                "Memory": 8,
                "QPS": 0,
                "RegionId": "cn-beijing",
                "SpecCode": "rds.mysql.4c8g",
                "SpecFamily": "General",
                "SpecStatus": "Normal",
                "StorageMax": 6000,
                "StorageMin": 20,
                "StorageStep": 100,
                "VCPU": 4,
                "ZoneId": ""
            },
            {
                "Connection": 180000,
                "DBEngineVersion": "MySQL_8_0",
                "IOPS": 160000,
                "InstanceType": "DoubleNode",
                "Memory": 864,
                "QPS": 0,
                "RegionId": "cn-beijing",
                "SpecCode": "rds.mysql.108c864g",
                "SpecFamily": "General",
                "SpecStatus": "Normal",
                "StorageMax": 6000,
                "StorageMin": 900,
                "StorageStep": 100,
                "VCPU": 108,
                "ZoneId": ""
            }
        ]
    }
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error code

For more details, refer to [Error codes](https://docs.byteplus.com/en/docs/RDS_for_MySQL/error_code).
