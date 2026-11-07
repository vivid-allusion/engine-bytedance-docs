---
title: "DescribeDBInstanceSpecs"
product: "NDB for mysql"
product_code: "NDB_for_MySQL"
source: "https://docs.byteplus.com/en/docs/NDB_for_MySQL/DescribeDBInstanceSpecs"
---

Call DescribeDBInstanceSpecs to query the node specification code supported by the availability zone.

<span id=".6K-35rGC57G75Z6L"></span>
## Request type

Synchronous request.

<span id=".6LCD6K-V"></span>
## Debug

[去调试](https://api.byteplus.com/api-explorer/debug?action=DescribeDBInstanceSpecs&serviceCode=vedbm&version=2022-01-01&groupName=)


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters


|**Name** |**Type** |**Required** |**Example** |**Description** |
|---|---|---|---|---|
|ZoneIds |String |No |cn\-beijing\-a |Availability zone ID.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="default">Call the <a href="https://docs.byteplus.com/en/docs/NDB_for_MySQL/DescribeAvailabilityZones">DescribeAvailabilityZones</a> API to query the resource information of availability zones in a specified region.</div><br><br><br>* <div data-tips="true" data-tips-type="default">If this parameter is empty, it returns the specification codes for all availability zones in the instance region.</div><br> |


<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameter


|**Name** |**Type** |**Example** |**Description** |
|---|---|---|---|
|Total |Integer |1 |Total number of specifications. |
|NodeSpecs |Array of [NodeSpecObject](https://docs.byteplus.com/en/docs/265/57341#nodespecobject) |Refer to the Sample response. |Specifications list. |


<span id="nodespecobject"></span>
### NodeSpecObject


|**Name** |**Type** |**Example** |**Description** |
|---|---|---|---|
|Connection |Integer |400 |Max connections. |
|Memory |Integer |8 |Memory size, in GiB. |
|NodeSpec |String |vedb.mysql.x4.xlarge |Specification code. |
|PrePaidMinStorage |Integer |50 |Minimum storage space in GiB. |
|PrePaidMaxStorage |Integer |2000000 |The upper limit of the storage space in GiB. |
|SpecFamily |String |General |Instance specification type. The valid values are:<br><br><br>* `General`: General type.<br><br>* `Exclusive`: Exclusive type. |
|vCPU |Integer |8 |CPU size. For example, 1 indicates 1 vCPU. |
|MaxIops |Integer |66000 |Maximum IOPS. |


<span id=".56S65L6L"></span>
## Example

<span id=".6K-35rGC56S65L6L"></span>
### Request example

```JSON
POST /?Action=DescribeDBInstanceSpecs&Version=2022-01-01 HTTP/1.1
Content-Type: application/json
Host:vedbm.cn-beijing.byteplusapi.com.cn
X-Date: 20220101T101010Z
Authorization: HMAC-SHA256 Credential=AKLTN2I0MmFiNzMxNWE5NDgzMzk4MmVjMTVkODlkZTZ****/20220101/cn-beijing/vedbm/request,SignedHeaders=x-date, Signature=71d31fc7bcf990142851c9833c5656391486cda0ae2e0b8ada733b7c645****
{
    "ZoneIds": "cn-beijing-b"
}
```


<span id=".6L-U5Zue56S65L6L"></span>
### Response example

```JSON
{
    "ResponseMetadata": {
        "RequestId": "20250428104107FBDF962634C2BD40D736-d2262f",
        "Action": "DescribeDBInstanceSpecs",
        "Version": "2022-01-01",
        "Service": "vedbm",
        "Region": "cn-beijing"
    },
    "Result": {
        "NodeSpecs": [
            {
                "Connection": 1800,
                "MaxIops": 12000,
                "Memory": 4,
                "NodeSpec": "vedb.mysql.g2.medium",
                "PrePaidMaxStorage": 100000,
                "PrePaidMinStorage": 50,
                "SpecFamily": "General",
                "vCPU": 2
            },
            {
                "Connection": 2000,
                "MaxIops": 24000,
                "Memory": 8,
                "NodeSpec": "vedb.mysql.g4.medium",
                "PrePaidMaxStorage": 100000,
                "PrePaidMinStorage": 50,
                "SpecFamily": "General",
                "vCPU": 2
            },
            {
                "Connection": 6000,
                "MaxIops": 24000,
                "Memory": 8,
                "NodeSpec": "vedb.mysql.x4.medium",
                "PrePaidMaxStorage": 100000,
                "PrePaidMinStorage": 50,
                "SpecFamily": "Exclusive",
                "vCPU": 2
            },
            {
                "Connection": 8000,
                "MaxIops": 44000,
                "Memory": 16,
                "NodeSpec": "vedb.mysql.g4.large",
                "PrePaidMaxStorage": 100000,
                "PrePaidMinStorage": 50,
                "SpecFamily": "General",
                "vCPU": 4
            },
            {
                "Connection": 8000,
                "MaxIops": 66000,
                "Memory": 16,
                "NodeSpec": "vedb.mysql.x4.large",
                "PrePaidMaxStorage": 100000,
                "PrePaidMinStorage": 50,
                "SpecFamily": "Exclusive",
                "vCPU": 4
            },
            {
                "Connection": 8000,
                "MaxIops": 80000,
                "Memory": 32,
                "NodeSpec": "vedb.mysql.x8.large",
                "PrePaidMaxStorage": 100000,
                "PrePaidMinStorage": 50,
                "SpecFamily": "Exclusive",
                "vCPU": 4
            },
            {
                "Connection": 16000,
                "MaxIops": 98000,
                "Memory": 32,
                "NodeSpec": "vedb.mysql.x4.xlarge",
                "PrePaidMaxStorage": 100000,
                "PrePaidMinStorage": 50,
                "SpecFamily": "Exclusive",
                "vCPU": 8
            },
            {
                "Connection": 16000,
                "MaxIops": 56000,
                "Memory": 32,
                "NodeSpec": "vedb.mysql.g4.xlarge",
                "PrePaidMaxStorage": 100000,
                "PrePaidMinStorage": 50,
                "SpecFamily": "General",
                "vCPU": 8
            },
            {
                "Connection": 16000,
                "MaxIops": 110000,
                "Memory": 64,
                "NodeSpec": "vedb.mysql.x8.xlarge",
                "PrePaidMaxStorage": 100000,
                "PrePaidMinStorage": 50,
                "SpecFamily": "Exclusive",
                "vCPU": 8
            },
            {
                "Connection": 32000,
                "MaxIops": 65000,
                "Memory": 64,
                "NodeSpec": "vedb.mysql.g4.2xlarge",
                "PrePaidMaxStorage": 100000,
                "PrePaidMinStorage": 50,
                "SpecFamily": "General",
                "vCPU": 16
            },
            {
                "Connection": 32000,
                "MaxIops": 194000,
                "Memory": 64,
                "NodeSpec": "vedb.mysql.x4.2xlarge",
                "PrePaidMaxStorage": 100000,
                "PrePaidMinStorage": 50,
                "SpecFamily": "Exclusive",
                "vCPU": 16
            },
            {
                "Connection": 32000,
                "MaxIops": 194000,
                "Memory": 128,
                "NodeSpec": "vedb.mysql.x8.2xlarge",
                "PrePaidMaxStorage": 100000,
                "PrePaidMinStorage": 50,
                "SpecFamily": "Exclusive",
                "vCPU": 16
            },
            {
                "Connection": 32000,
                "MaxIops": 65000,
                "Memory": 128,
                "NodeSpec": "vedb.mysql.g8.2xlarge",
                "PrePaidMaxStorage": 100000,
                "PrePaidMinStorage": 50,
                "SpecFamily": "General",
                "vCPU": 16
            },
            {
                "Connection": 64000,
                "MaxIops": 290000,
                "Memory": 128,
                "NodeSpec": "vedb.mysql.x4.4xlarge",
                "PrePaidMaxStorage": 500000,
                "PrePaidMinStorage": 50,
                "SpecFamily": "Exclusive",
                "vCPU": 32
            },
            {
                "Connection": 64000,
                "MaxIops": 86000,
                "Memory": 128,
                "NodeSpec": "vedb.mysql.g4.4xlarge",
                "PrePaidMaxStorage": 500000,
                "PrePaidMinStorage": 50,
                "SpecFamily": "General",
                "vCPU": 32
            },
            {
                "Connection": 64000,
                "MaxIops": 290000,
                "Memory": 256,
                "NodeSpec": "vedb.mysql.x8.4xlarge",
                "PrePaidMaxStorage": 500000,
                "PrePaidMinStorage": 50,
                "SpecFamily": "Exclusive",
                "vCPU": 32
            },
            {
                "Connection": 64000,
                "MaxIops": 300000,
                "Memory": 384,
                "NodeSpec": "vedb.mysql.x8.6xlarge",
                "PrePaidMaxStorage": 500000,
                "PrePaidMinStorage": 50,
                "SpecFamily": "Exclusive",
                "vCPU": 48
            },
            {
                "Connection": 64000,
                "MaxIops": 300000,
                "Memory": 256,
                "NodeSpec": "vedb.mysql.x4.8xlarge",
                "PrePaidMaxStorage": 500000,
                "PrePaidMinStorage": 50,
                "SpecFamily": "Exclusive",
                "vCPU": 64
            },
            {
                "Connection": 64000,
                "MaxIops": 300000,
                "Memory": 512,
                "NodeSpec": "vedb.mysql.x8.8xlarge",
                "PrePaidMaxStorage": 500000,
                "PrePaidMinStorage": 50,
                "SpecFamily": "Exclusive",
                "vCPU": 64
            }
        ],
        "Total": 19
    }
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error code

For details, refer to [Error codes](https://docs.byteplus.com/en/docs/NDB_for_MySQL/Error_codes).
