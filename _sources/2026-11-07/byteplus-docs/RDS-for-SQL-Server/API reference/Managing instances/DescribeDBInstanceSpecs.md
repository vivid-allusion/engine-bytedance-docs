---
title: "DescribeDBInstanceSpecs"
product: "RDS for SQL Server"
product_code: "RDS-for-SQL-Server"
source: "https://docs.byteplus.com/en/docs/RDS-for-SQL-Server/describedbInstancespecs"
---

Invoke DescribeDBInstanceSpecs interface query instance specification code.

<span id="request-type"></span>
## request type

Synchronization request.

<span id="request-parameters"></span>
## request parameters


|**name** |**type** |**Is it required** |**sample value** |**describe** |
|---|---|---|---|---|
|ZoneId |String |No |cn\-beijing\-a |Instance Availability Zone ID.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">You can call the <a href="https://docs.byteplus.com/en/docs/RDS-for-SQL-Server/describeavailabilityzones">DescribeAvailabilityZones </a>interface to query the instance Availability Zone ID.</div><br> |
|DBEngineVersion |String |No |SQLServer_2019_Std |Compatible version. The values are as follows:<br><br><br>* `SQLServer_2019_Std`: Represents SQL Server 2019 Standard Edition.<br><br>* `SQLServer_2019_Web`: Represents SQL Server 2019 Web Edition.<br><br>* `SQLServer_2019_Ent`: Represents SQL Server 2019 Enterprise Edition. |
|InstanceType |String |No |Basic |Instance type. The values are as follows:<br><br><br>* `HA`: Represents a highly available type.<br><br>* `Basic`: Represents the basic version type.<br><br>* `Cluster`: Represents the cluster version type.<br><br>* `ReadOnly`: Represents read\-only instances.<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">If this parameter is not passed, the specifications of all instance types are returned.</div><br> |


<span id="return-parameters"></span>
## return parameters


|name |type |sample value |describe |
|---|---|---|---|
|InstanceSpecInfo |Array of [InstanceSpecObject](https://docs.byteplus.com/en/docs/RDS-for-SQL-Server/data-structure#instancespecobject) |```json```<br>```[```<br>```    {```<br>```        "DBEngineVersion": "SQLServer_2019_Ent",```<br>```        "Generation": "Generation1",```<br>```        "InstanceType": "Basic",```<br>```        "Memory": 4,```<br>```        "SpecCode": "rds.mssql.ee.std.d2.2c4g",```<br>```        "SpecFamily": "General",```<br>```        "SpecSaleType": "SPLA",```<br>```        "SpecStatus": "Normal",```<br>```        "VCPU": 2,```<br>```        "ZoneId": "cn-beijing-b"```<br>```    }```<br>``` ]```<br> |List of specifications. |


<span id="request-example"></span>
## Request example

```plain
POST /?Action=DescribeDBInstanceSpecs&Version=2022-01-01 HTTP/1.1 
Content-Type: application/json 
Host: rds-mssql.cn-beijing.byteplusapi.com.cn 
X-Date: 20230131T101010Z 
Authorization: HMAC-SHA256 Credential=AKLTN2I0MmFiNzMxNWE5NDgzMzk4MmVjMTVkODlkZTZ****/20211202/cn-beijing/rds_mssql/request,SignedHeaders=x-date, Signature=71d31fc7bcf990142851c9833c5656391486cda0ae2e0b8ada733b7c6458****
```


<span id="back-to-example"></span>
## Back to example

```json
{ 
    "ResponseMetadata": { 
        "RequestId": "202409121945533F5BF46BC9700311825D-35381b", 
        "Action": "DescribeDBInstanceSpecs", 
        "Version": "2022-01-01", 
        "Service": "rds_mssql", 
        "Region": "cn-beijing" 
    }, 
    "Result": { 
        "InstanceSpecsInfo": [ 
            { 
                "DBEngineVersion": "SQLServer_2019_Ent", 
                "Generation": "Generation1", 
                "InstanceType": "Basic", 
                "Memory": 4, 
                "SpecCode": "rds.mssql.ee.std.d2.2c4g", 
                "SpecFamily": "General", 
                "SpecSaleType": "SPLA", 
                "SpecStatus": "Normal", 
                "VCPU": 2, 
                "ZoneId": "cn-beijing-b" 
            }, 
            { 
                "DBEngineVersion": "SQLServer_2019_Web", 
                "Generation": "Generation2", 
                "InstanceType": "Basic", 
                "Memory": 64, 
                "SpecCode": "rds.mssql.3il.s4.2xlarge.w1", 
                "SpecFamily": "General", 
                "SpecSaleType": "SPLA", 
                "SpecStatus": "Normal", 
                "VCPU": 16, 
                "ZoneId": "cn-beijing-c" 
            } 
        ] 
    } 
}
```


<span id="error-code"></span>
## error code

For more details, see [Error Code ](https://docs.byteplus.com/en/docs/RDS-for-SQL-Server/error-codes).
