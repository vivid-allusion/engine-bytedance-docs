---
title: "DescribeNodeSpecs"
product: "Document Database for MongoDB"
product_code: "mongodb"
source: "https://docs.byteplus.com/en/docs/mongodb/describenodespecs"
---

Call the DescribeNodeSpecs API query the list of node specifications supported by MongoDB.

<span id=".6K-35rGC57G75Z6L"></span>
## Request type

Synchronous request.

<span id=".6LCD6K-V"></span>
## Debugging

[去调试](https://api.byteplus.com/api-explorer/debug?action=DescribeNodeSpecs&serviceCode=mongodb&version=2022-01-01&groupName=实例管理)


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters



**RegionId ** <span data-label="purple"> String  </span>`Optional` `Sample value: cn-beijing`

Region ID.

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="default">If this parameter is left blank, it will return the node information for all regions where MongoDB instances can be created under the current account.</div>


* <div data-tips="true" data-tips-type="default">You can call the <a href="https://docs.byteplus.com/en/docs/mongodb/describeregions">DescribeRegions</a> API to query all region information supported by MongoDB instances, including Region ID.</div>




<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters



**MongosNodeSpecs ** <span data-label="purple"> Object[]  </span>`Sample value: `

Mongos node specification list.


**CpuNum ** <span data-label="purple"> Double  </span>`Sample value: 2`

Number of CPU cores.



**MaxConn ** <span data-label="purple"> Long </span>`Sample value: 2000`

Max connections.



**MemInGb ** <span data-label="purple"> Double  </span>`Sample value: 4`

Memory. Unit: GiB.



**SpecName ** <span data-label="purple"> String  </span>`Sample value: mongo.mongos.2c4g`

Specification code.




**NodeSpecs ** <span data-label="purple"> Object[] </span>`Sample value:`

Specification list of replica set nodes.


**CpuNum ** <span data-label="purple"> Double  </span>`Sample value: 2`

Cores.



**MaxConn ** <span data-label="purple"> Long </span>`Sample value: 2000`

Max connections.



**MaxStorage ** <span data-label="purple"> Long  </span>`Sample value: 2000`

Maximum storage space for local disks. Unit: GiB.



**MinStorage ** <span data-label="purple"> Long </span>`Sample value: 20`

Minimum optional storage space for local disks. Unit: GiB.



**MemInGb ** <span data-label="purple"> Double  </span>`Sample value: 4`

Memory. Unit: GiB.



**SpecName ** <span data-label="purple"> String  </span>`Sample value: mongo.2c4g`

Specification code.




**ShardNodeSpecs ** <span data-label="purple"> Object[]  </span>`Sample value:`

List of Shard node specifications.


**CpuNum ** <span data-label="purple"> Double </span>`Sample value: 2`

Cores.



**MaxConn ** <span data-label="purple"> Long </span>`Sample value: 2000`

Max connections.



**MaxStorage ** <span data-label="purple"> Long  </span>`Sample value: 2000`

Maximum storage space for local disks. Unit: GiB.



**MinStorage ** <span data-label="purple"> Long </span>`Sample value: 20`

Minimum optional storage space for local disks. Unit: GiB.



**MemInGb ** <span data-label="purple"> Double  </span>`Sample value: 4`

Memory. Unit: GiB.



**SpecName ** <span data-label="purple"> String </span>`Sample value: mongo.shard.2c4g`

Specification code.




**ConfigServerNodeSpecs ** <span data-label="purple"> Object[]  </span>`Sample value:`

List of ConfigServer node specifications.


**CpuNum ** <span data-label="purple"> Double  </span>`Sample value: 2`

Cores.



**MaxConn ** <span data-label="purple"> Long </span>`Sample value: 2000`

Max connections.



**MaxStorage ** <span data-label="purple"> Long  </span>`Sample value: 2000`

Maximum storage space for local disks. Unit: GiB.



**MinStorage ** <span data-label="purple"> Long </span>`Sample value: 20`

Minimum optional storage space for local disks. Unit: GiB.



**MemInGb ** <span data-label="purple"> Double  </span>`Sample value: 4`

Memory. Unit: GiB.



**SpecName ** <span data-label="purple"> String  </span>`Sample value: mongo.config.2c4g`

Specification code.




**MongotNodeSpecs ** <span data-label="purple"> Object[]  </span>`Sample value: `

Mongot node specification list


**CpuNum ** <span data-label="purple"> Double  </span>`Sample value: 2`

Cores.



**MaxConn ** <span data-label="purple"> Long </span>`Sample value: 2000`

Max connections.



**MaxStorage ** <span data-label="purple"> Long  </span>`Sample value: 2000`

Maximum storage space for local disks. Unit: GiB.



**MinStorage ** <span data-label="purple"> Long </span>`Sample value: 20`

Minimum optional storage space for local disks. Unit: GiB.



**MemInGb ** <span data-label="purple"> Double  </span>`Sample value: 4`

Memory. Unit: GiB.



**SpecName ** <span data-label="purple"> String  </span>`Sample value: mongo.2c4g`

Specification code.




<span id=".56S65L6L"></span>
## Example

<span id=".6K-35rGC56S65L6L"></span>
### Request example

```JSON
POST https://mongodb.cn-beijing.byteplusapi.com.cn/?Action=DescribeNodeSpecs&Version=2022-01-01 HTTP/1.1
Host: mongodb.cn-beijing.byteplusapi.com.cn
Content-Type: application/json; charset=utf-8
X-Date: 20201103T104027Z
Authorization: HMAC-SHA256 Credential=AK****/20201103/cn-beijing/mongodb/request,SignedHeaders=content-type;host;x-date,Signature=****
{
    "RegionId":"cn-beijing"
}
```


<span id=".6L-U5Zue56S65L6L"></span>
### Response example

This example displays partial node specification information. The actual returned data depends on the API call's result.

```JSON
{
    "ResponseMetadata": {
        "RequestId": "2026072217393456044489A8E13D97832F-174ad1",
        "Action": "DescribeNodeSpecs",
        "Version": "2022-01-01",
        "Service": "mongodb",
        "Region": "cn-nanjing-bbit"
    },
    "Result": {
        "ConfigServerNodeSpecs": [
            {
                "CpuNum": 1,
                "DefaultStorage": 20,
                "MaxCloudStorage": 0,
                "MaxConn": 1000,
                "MaxStorage": 2000,
                "MemInGb": 2,
                "MinCloudStorage": 0,
                "MinStorage": 20,
                "SpecName": "mongo.config.1c2g"
            },
            {
                "CpuNum": 2,
                "DefaultStorage": 20,
                "MaxCloudStorage": 0,
                "MaxConn": 2000,
                "MaxStorage": 2000,
                "MemInGb": 4,
                "MinCloudStorage": 0,
                "MinStorage": 20,
                "SpecName": "mongo.config.2c4g"
            },
            {
                "CpuNum": 4,
                "DefaultStorage": 20,
                "MaxCloudStorage": 0,
                "MaxConn": 4000,
                "MaxStorage": 2000,
                "MemInGb": 8,
                "MinCloudStorage": 0,
                "MinStorage": 20,
                "SpecName": "mongo.config.4c8g"
            },
            {
                "CpuNum": 4,
                "DefaultStorage": 20,
                "MaxCloudStorage": 0,
                "MaxConn": 6000,
                "MaxStorage": 2000,
                "MemInGb": 16,
                "MinCloudStorage": 0,
                "MinStorage": 20,
                "SpecName": "mongo.config.4c16g"
            },
            {
                "CpuNum": 4,
                "DefaultStorage": 20,
                "MaxCloudStorage": 0,
                "MaxConn": 8000,
                "MaxStorage": 2000,
                "MemInGb": 32,
                "MinCloudStorage": 0,
                "MinStorage": 20,
                "SpecName": "mongo.config.4c32g"
            },
            {
                "CpuNum": 8,
                "DefaultStorage": 20,
                "MaxCloudStorage": 0,
                "MaxConn": 16000,
                "MaxStorage": 2000,
                "MemInGb": 16,
                "MinCloudStorage": 0,
                "MinStorage": 20,
                "SpecName": "mongo.config.8c16g"
            },
            {
                "CpuNum": 8,
                "DefaultStorage": 20,
                "MaxCloudStorage": 0,
                "MaxConn": 16000,
                "MaxStorage": 2000,
                "MemInGb": 32,
                "MinCloudStorage": 0,
                "MinStorage": 20,
                "SpecName": "mongo.config.8c32g"
            },
            {
                "CpuNum": 8,
                "DefaultStorage": 20,
                "MaxCloudStorage": 0,
                "MaxConn": 16000,
                "MaxStorage": 2000,
                "MemInGb": 64,
                "MinCloudStorage": 0,
                "MinStorage": 20,
                "SpecName": "mongo.config.8c64g"
            },
            {
                "CpuNum": 16,
                "DefaultStorage": 20,
                "MaxCloudStorage": 0,
                "MaxConn": 24000,
                "MaxStorage": 2000,
                "MemInGb": 32,
                "MinCloudStorage": 0,
                "MinStorage": 20,
                "SpecName": "mongo.config.16c32g"
            },
            {
                "CpuNum": 16,
                "DefaultStorage": 20,
                "MaxCloudStorage": 0,
                "MaxConn": 24000,
                "MaxStorage": 2000,
                "MemInGb": 64,
                "MinCloudStorage": 0,
                "MinStorage": 20,
                "SpecName": "mongo.config.16c64g"
            },
            {
                "CpuNum": 32,
                "DefaultStorage": 20,
                "MaxCloudStorage": 0,
                "MaxConn": 24000,
                "MaxStorage": 2000,
                "MemInGb": 64,
                "MinCloudStorage": 0,
                "MinStorage": 20,
                "SpecName": "mongo.config.32c64g"
            }
        ],
        "MongosNodeSpecs": [
            {
                "CpuNum": 1,
                "MaxConn": 1000,
                "MemInGb": 2,
                "SpecName": "mongo.mongos.1c2g"
            },
            {
                "CpuNum": 2,
                "MaxConn": 2000,
                "MemInGb": 4,
                "SpecName": "mongo.mongos.2c4g"
            },
            {
                "CpuNum": 4,
                "MaxConn": 4000,
                "MemInGb": 8,
                "SpecName": "mongo.mongos.4c8g"
            },
            {
                "CpuNum": 4,
                "MaxConn": 6000,
                "MemInGb": 16,
                "SpecName": "mongo.mongos.4c16g"
            },
            {
                "CpuNum": 4,
                "MaxConn": 8000,
                "MemInGb": 32,
                "SpecName": "mongo.mongos.4c32g"
            },
            {
                "CpuNum": 8,
                "MaxConn": 16000,
                "MemInGb": 16,
                "SpecName": "mongo.mongos.8c16g"
            },
            {
                "CpuNum": 8,
                "MaxConn": 16000,
                "MemInGb": 32,
                "SpecName": "mongo.mongos.8c32g"
            },
            {
                "CpuNum": 8,
                "MaxConn": 16000,
                "MemInGb": 64,
                "SpecName": "mongo.mongos.8c64g"
            },
            {
                "CpuNum": 16,
                "MaxConn": 24000,
                "MemInGb": 32,
                "SpecName": "mongo.mongos.16c32g"
            },
            {
                "CpuNum": 16,
                "MaxConn": 24000,
                "MemInGb": 64,
                "SpecName": "mongo.mongos.16c64g"
            },
            {
                "CpuNum": 16,
                "MaxConn": 24000,
                "MemInGb": 128,
                "SpecName": "mongo.mongos.16c128g"
            },
            {
                "CpuNum": 32,
                "MaxConn": 24000,
                "MemInGb": 64,
                "SpecName": "mongo.mongos.32c64g"
            },
            {
                "CpuNum": 32,
                "MaxConn": 42000,
                "MemInGb": 128,
                "SpecName": "mongo.mongos.32c128g"
            },
            {
                "CpuNum": 32,
                "MaxConn": 42000,
                "MemInGb": 256,
                "SpecName": "mongo.mongos.32c256g"
            },
            {
                "CpuNum": 60,
                "MaxConn": 64000,
                "MemInGb": 120,
                "SpecName": "mongo.mongos.60c120g"
            }
        ],
        "MongotNodeSpecs": [
            {
                "CpuNum": 2,
                "DefaultStorage": 200,
                "MaxCloudStorage": 0,
                "MaxConn": 2000,
                "MaxStorage": 2000,
                "MemInGb": 4,
                "MinCloudStorage": 0,
                "MinStorage": 100,
                "SpecName": "mongo.mongot.2c4g"
            },
            {
                "CpuNum": 4,
                "DefaultStorage": 300,
                "MaxCloudStorage": 0,
                "MaxConn": 4000,
                "MaxStorage": 2000,
                "MemInGb": 8,
                "MinCloudStorage": 0,
                "MinStorage": 100,
                "SpecName": "mongo.mongot.4c8g"
            },
            {
                "CpuNum": 4,
                "DefaultStorage": 300,
                "MaxCloudStorage": 0,
                "MaxConn": 6000,
                "MaxStorage": 2000,
                "MemInGb": 16,
                "MinCloudStorage": 0,
                "MinStorage": 100,
                "SpecName": "mongo.mongot.4c16g"
            },
            {
                "CpuNum": 4,
                "DefaultStorage": 300,
                "MaxCloudStorage": 0,
                "MaxConn": 8000,
                "MaxStorage": 2000,
                "MemInGb": 32,
                "MinCloudStorage": 0,
                "MinStorage": 100,
                "SpecName": "mongo.mongot.4c32g"
            },
            {
                "CpuNum": 8,
                "DefaultStorage": 400,
                "MaxCloudStorage": 0,
                "MaxConn": 16000,
                "MaxStorage": 3000,
                "MemInGb": 16,
                "MinCloudStorage": 0,
                "MinStorage": 200,
                "SpecName": "mongo.mongot.8c16g"
            },
            {
                "CpuNum": 8,
                "DefaultStorage": 400,
                "MaxCloudStorage": 0,
                "MaxConn": 16000,
                "MaxStorage": 3000,
                "MemInGb": 32,
                "MinCloudStorage": 0,
                "MinStorage": 200,
                "SpecName": "mongo.mongot.8c32g"
            },
            {
                "CpuNum": 8,
                "DefaultStorage": 400,
                "MaxCloudStorage": 0,
                "MaxConn": 16000,
                "MaxStorage": 3000,
                "MemInGb": 64,
                "MinCloudStorage": 0,
                "MinStorage": 200,
                "SpecName": "mongo.mongot.8c64g"
            },
            {
                "CpuNum": 16,
                "DefaultStorage": 500,
                "MaxCloudStorage": 0,
                "MaxConn": 24000,
                "MaxStorage": 3000,
                "MemInGb": 32,
                "MinCloudStorage": 0,
                "MinStorage": 200,
                "SpecName": "mongo.mongot.16c32g"
            },
            {
                "CpuNum": 16,
                "DefaultStorage": 500,
                "MaxCloudStorage": 0,
                "MaxConn": 24000,
                "MaxStorage": 3000,
                "MemInGb": 64,
                "MinCloudStorage": 0,
                "MinStorage": 200,
                "SpecName": "mongo.mongot.16c64g"
            },
            {
                "CpuNum": 16,
                "DefaultStorage": 500,
                "MaxCloudStorage": 0,
                "MaxConn": 24000,
                "MaxStorage": 3000,
                "MemInGb": 128,
                "MinCloudStorage": 0,
                "MinStorage": 200,
                "SpecName": "mongo.mongot.16c128g"
            },
            {
                "CpuNum": 32,
                "DefaultStorage": 1000,
                "MaxCloudStorage": 0,
                "MaxConn": 24000,
                "MaxStorage": 3000,
                "MemInGb": 64,
                "MinCloudStorage": 0,
                "MinStorage": 200,
                "SpecName": "mongo.mongot.32c64g"
            },
            {
                "CpuNum": 32,
                "DefaultStorage": 1000,
                "MaxCloudStorage": 0,
                "MaxConn": 42000,
                "MaxStorage": 3000,
                "MemInGb": 128,
                "MinCloudStorage": 0,
                "MinStorage": 200,
                "SpecName": "mongo.mongot.32c128g"
            },
            {
                "CpuNum": 32,
                "DefaultStorage": 1000,
                "MaxCloudStorage": 0,
                "MaxConn": 42000,
                "MaxStorage": 3000,
                "MemInGb": 256,
                "MinCloudStorage": 0,
                "MinStorage": 200,
                "SpecName": "mongo.mongot.32c256g"
            },
            {
                "CpuNum": 60,
                "DefaultStorage": 3000,
                "MaxCloudStorage": 0,
                "MaxConn": 64000,
                "MaxStorage": 3000,
                "MemInGb": 120,
                "MinCloudStorage": 0,
                "MinStorage": 200,
                "SpecName": "mongo.mongot.60c120g"
            },
            {
                "CpuNum": 60,
                "DefaultStorage": 3000,
                "MaxCloudStorage": 0,
                "MaxConn": 64000,
                "MaxStorage": 3000,
                "MemInGb": 240,
                "MinCloudStorage": 0,
                "MinStorage": 200,
                "SpecName": "mongo.mongot.60c240g"
            },
            {
                "CpuNum": 90,
                "DefaultStorage": 3000,
                "MaxCloudStorage": 0,
                "MaxConn": 64000,
                "MaxStorage": 3000,
                "MemInGb": 360,
                "MinCloudStorage": 0,
                "MinStorage": 200,
                "SpecName": "mongo.mongot.90c360g"
            },
            {
                "CpuNum": 120,
                "DefaultStorage": 3000,
                "MaxCloudStorage": 0,
                "MaxConn": 64000,
                "MaxStorage": 3000,
                "MemInGb": 480,
                "MinCloudStorage": 0,
                "MinStorage": 200,
                "SpecName": "mongo.mongot.120c480g"
            }
        ],
        "NodeSpecs": [
            {
                "CpuNum": 1,
                "DefaultStorage": 100,
                "MaxCloudStorage": 0,
                "MaxConn": 1000,
                "MaxStorage": 200,
                "MemInGb": 2,
                "MinCloudStorage": 0,
                "MinStorage": 20,
                "SpecName": "mongo.1c2g"
            },
            {
                "CpuNum": 2,
                "DefaultStorage": 200,
                "MaxCloudStorage": 0,
                "MaxConn": 2000,
                "MaxStorage": 2000,
                "MemInGb": 4,
                "MinCloudStorage": 0,
                "MinStorage": 100,
                "SpecName": "mongo.2c4g"
            },
            {
                "CpuNum": 4,
                "DefaultStorage": 300,
                "MaxCloudStorage": 0,
                "MaxConn": 4000,
                "MaxStorage": 2000,
                "MemInGb": 8,
                "MinCloudStorage": 0,
                "MinStorage": 100,
                "SpecName": "mongo.4c8g"
            },
            {
                "CpuNum": 4,
                "DefaultStorage": 300,
                "MaxCloudStorage": 0,
                "MaxConn": 6000,
                "MaxStorage": 2000,
                "MemInGb": 16,
                "MinCloudStorage": 0,
                "MinStorage": 100,
                "SpecName": "mongo.4c16g"
            },
            {
                "CpuNum": 4,
                "DefaultStorage": 300,
                "MaxCloudStorage": 0,
                "MaxConn": 8000,
                "MaxStorage": 2000,
                "MemInGb": 32,
                "MinCloudStorage": 0,
                "MinStorage": 100,
                "SpecName": "mongo.4c32g"
            },
            {
                "CpuNum": 8,
                "DefaultStorage": 400,
                "MaxCloudStorage": 0,
                "MaxConn": 16000,
                "MaxStorage": 3000,
                "MemInGb": 16,
                "MinCloudStorage": 0,
                "MinStorage": 200,
                "SpecName": "mongo.8c16g"
            },
            {
                "CpuNum": 8,
                "DefaultStorage": 400,
                "MaxCloudStorage": 0,
                "MaxConn": 16000,
                "MaxStorage": 3000,
                "MemInGb": 32,
                "MinCloudStorage": 0,
                "MinStorage": 200,
                "SpecName": "mongo.8c32g"
            },
            {
                "CpuNum": 8,
                "DefaultStorage": 400,
                "MaxCloudStorage": 0,
                "MaxConn": 16000,
                "MaxStorage": 3000,
                "MemInGb": 64,
                "MinCloudStorage": 0,
                "MinStorage": 200,
                "SpecName": "mongo.8c64g"
            },
            {
                "CpuNum": 16,
                "DefaultStorage": 500,
                "MaxCloudStorage": 0,
                "MaxConn": 24000,
                "MaxStorage": 3000,
                "MemInGb": 32,
                "MinCloudStorage": 0,
                "MinStorage": 200,
                "SpecName": "mongo.16c32g"
            },
            {
                "CpuNum": 16,
                "DefaultStorage": 500,
                "MaxCloudStorage": 0,
                "MaxConn": 24000,
                "MaxStorage": 3000,
                "MemInGb": 64,
                "MinCloudStorage": 0,
                "MinStorage": 200,
                "SpecName": "mongo.16c64g"
            },
            {
                "CpuNum": 16,
                "DefaultStorage": 500,
                "MaxCloudStorage": 0,
                "MaxConn": 24000,
                "MaxStorage": 3000,
                "MemInGb": 128,
                "MinCloudStorage": 0,
                "MinStorage": 200,
                "SpecName": "mongo.16c128g"
            },
            {
                "CpuNum": 32,
                "DefaultStorage": 1000,
                "MaxCloudStorage": 0,
                "MaxConn": 24000,
                "MaxStorage": 3000,
                "MemInGb": 64,
                "MinCloudStorage": 0,
                "MinStorage": 200,
                "SpecName": "mongo.32c64g"
            },
            {
                "CpuNum": 32,
                "DefaultStorage": 1000,
                "MaxCloudStorage": 0,
                "MaxConn": 42000,
                "MaxStorage": 3000,
                "MemInGb": 128,
                "MinCloudStorage": 0,
                "MinStorage": 200,
                "SpecName": "mongo.32c128g"
            },
            {
                "CpuNum": 32,
                "DefaultStorage": 1000,
                "MaxCloudStorage": 0,
                "MaxConn": 42000,
                "MaxStorage": 3000,
                "MemInGb": 256,
                "MinCloudStorage": 0,
                "MinStorage": 200,
                "SpecName": "mongo.32c256g"
            },
            {
                "CpuNum": 60,
                "DefaultStorage": 3000,
                "MaxCloudStorage": 0,
                "MaxConn": 64000,
                "MaxStorage": 3000,
                "MemInGb": 120,
                "MinCloudStorage": 0,
                "MinStorage": 200,
                "SpecName": "mongo.60c120g"
            },
            {
                "CpuNum": 60,
                "DefaultStorage": 3000,
                "MaxCloudStorage": 0,
                "MaxConn": 64000,
                "MaxStorage": 3000,
                "MemInGb": 240,
                "MinCloudStorage": 0,
                "MinStorage": 200,
                "SpecName": "mongo.60c240g"
            },
            {
                "CpuNum": 60,
                "DefaultStorage": 3000,
                "MaxCloudStorage": 0,
                "MaxConn": 64000,
                "MaxStorage": 3000,
                "MemInGb": 480,
                "MinCloudStorage": 0,
                "MinStorage": 200,
                "SpecName": "mongo.60c480g"
            },
            {
                "CpuNum": 90,
                "DefaultStorage": 3000,
                "MaxCloudStorage": 0,
                "MaxConn": 64000,
                "MaxStorage": 3000,
                "MemInGb": 360,
                "MinCloudStorage": 0,
                "MinStorage": 200,
                "SpecName": "mongo.90c360g"
            },
            {
                "CpuNum": 120,
                "DefaultStorage": 3000,
                "MaxCloudStorage": 0,
                "MaxConn": 64000,
                "MaxStorage": 3000,
                "MemInGb": 480,
                "MinCloudStorage": 0,
                "MinStorage": 200,
                "SpecName": "mongo.120c480g"
            }
        ],
        "ShardNodeSpecs": [
            {
                "CpuNum": 1,
                "DefaultStorage": 100,
                "MaxCloudStorage": 0,
                "MaxConn": 1000,
                "MaxStorage": 200,
                "MemInGb": 2,
                "MinCloudStorage": 0,
                "MinStorage": 20,
                "SpecName": "mongo.shard.1c2g"
            },
            {
                "CpuNum": 2,
                "DefaultStorage": 200,
                "MaxCloudStorage": 0,
                "MaxConn": 2000,
                "MaxStorage": 2000,
                "MemInGb": 4,
                "MinCloudStorage": 0,
                "MinStorage": 100,
                "SpecName": "mongo.shard.2c4g"
            },
            {
                "CpuNum": 4,
                "DefaultStorage": 300,
                "MaxCloudStorage": 0,
                "MaxConn": 4000,
                "MaxStorage": 2000,
                "MemInGb": 8,
                "MinCloudStorage": 0,
                "MinStorage": 100,
                "SpecName": "mongo.shard.4c8g"
            },
            {
                "CpuNum": 4,
                "DefaultStorage": 300,
                "MaxCloudStorage": 0,
                "MaxConn": 6000,
                "MaxStorage": 2000,
                "MemInGb": 16,
                "MinCloudStorage": 0,
                "MinStorage": 100,
                "SpecName": "mongo.shard.4c16g"
            },
            {
                "CpuNum": 4,
                "DefaultStorage": 300,
                "MaxCloudStorage": 0,
                "MaxConn": 8000,
                "MaxStorage": 2000,
                "MemInGb": 32,
                "MinCloudStorage": 0,
                "MinStorage": 100,
                "SpecName": "mongo.shard.4c32g"
            },
            {
                "CpuNum": 8,
                "DefaultStorage": 400,
                "MaxCloudStorage": 0,
                "MaxConn": 16000,
                "MaxStorage": 3000,
                "MemInGb": 16,
                "MinCloudStorage": 0,
                "MinStorage": 200,
                "SpecName": "mongo.shard.8c16g"
            },
            {
                "CpuNum": 8,
                "DefaultStorage": 400,
                "MaxCloudStorage": 0,
                "MaxConn": 16000,
                "MaxStorage": 3000,
                "MemInGb": 32,
                "MinCloudStorage": 0,
                "MinStorage": 200,
                "SpecName": "mongo.shard.8c32g"
            },
            {
                "CpuNum": 8,
                "DefaultStorage": 400,
                "MaxCloudStorage": 0,
                "MaxConn": 16000,
                "MaxStorage": 3000,
                "MemInGb": 64,
                "MinCloudStorage": 0,
                "MinStorage": 200,
                "SpecName": "mongo.shard.8c64g"
            },
            {
                "CpuNum": 16,
                "DefaultStorage": 500,
                "MaxCloudStorage": 0,
                "MaxConn": 24000,
                "MaxStorage": 3000,
                "MemInGb": 32,
                "MinCloudStorage": 0,
                "MinStorage": 200,
                "SpecName": "mongo.shard.16c32g"
            },
            {
                "CpuNum": 16,
                "DefaultStorage": 500,
                "MaxCloudStorage": 0,
                "MaxConn": 24000,
                "MaxStorage": 3000,
                "MemInGb": 64,
                "MinCloudStorage": 0,
                "MinStorage": 200,
                "SpecName": "mongo.shard.16c64g"
            },
            {
                "CpuNum": 16,
                "DefaultStorage": 500,
                "MaxCloudStorage": 0,
                "MaxConn": 24000,
                "MaxStorage": 3000,
                "MemInGb": 128,
                "MinCloudStorage": 0,
                "MinStorage": 200,
                "SpecName": "mongo.shard.16c128g"
            },
            {
                "CpuNum": 32,
                "DefaultStorage": 1000,
                "MaxCloudStorage": 0,
                "MaxConn": 24000,
                "MaxStorage": 3000,
                "MemInGb": 64,
                "MinCloudStorage": 0,
                "MinStorage": 200,
                "SpecName": "mongo.shard.32c64g"
            },
            {
                "CpuNum": 32,
                "DefaultStorage": 1000,
                "MaxCloudStorage": 0,
                "MaxConn": 42000,
                "MaxStorage": 3000,
                "MemInGb": 128,
                "MinCloudStorage": 0,
                "MinStorage": 200,
                "SpecName": "mongo.shard.32c128g"
            },
            {
                "CpuNum": 32,
                "DefaultStorage": 1000,
                "MaxCloudStorage": 0,
                "MaxConn": 42000,
                "MaxStorage": 3000,
                "MemInGb": 256,
                "MinCloudStorage": 0,
                "MinStorage": 200,
                "SpecName": "mongo.shard.32c256g"
            },
            {
                "CpuNum": 60,
                "DefaultStorage": 3000,
                "MaxCloudStorage": 0,
                "MaxConn": 64000,
                "MaxStorage": 3000,
                "MemInGb": 120,
                "MinCloudStorage": 0,
                "MinStorage": 200,
                "SpecName": "mongo.shard.60c120g"
            },
            {
                "CpuNum": 60,
                "DefaultStorage": 3000,
                "MaxCloudStorage": 0,
                "MaxConn": 64000,
                "MaxStorage": 3000,
                "MemInGb": 240,
                "MinCloudStorage": 0,
                "MinStorage": 200,
                "SpecName": "mongo.shard.60c240g"
            },
            {
                "CpuNum": 60,
                "DefaultStorage": 3000,
                "MaxCloudStorage": 0,
                "MaxConn": 64000,
                "MaxStorage": 3000,
                "MemInGb": 480,
                "MinCloudStorage": 0,
                "MinStorage": 200,
                "SpecName": "mongo.shard.60c480g"
            },
            {
                "CpuNum": 90,
                "DefaultStorage": 3000,
                "MaxCloudStorage": 0,
                "MaxConn": 64000,
                "MaxStorage": 3000,
                "MemInGb": 360,
                "MinCloudStorage": 0,
                "MinStorage": 200,
                "SpecName": "mongo.shard.90c360g"
            },
            {
                "CpuNum": 120,
                "DefaultStorage": 3000,
                "MaxCloudStorage": 0,
                "MaxConn": 64000,
                "MaxStorage": 3000,
                "MemInGb": 480,
                "MinCloudStorage": 0,
                "MinStorage": 200,
                "SpecName": "mongo.shard.120c480g"
            }
        ]
    }
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error code

For more details, see [Error code](https://docs.byteplus.com/en/docs/mongodb/error-code).
