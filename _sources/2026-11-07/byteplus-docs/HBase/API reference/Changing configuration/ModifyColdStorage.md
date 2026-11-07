---
title: "ModifyColdStorage"
product: "Table Storage for HBase"
product_code: "HBase"
source: "https://docs.byteplus.com/en/docs/HBase/ModifyColdStorage"
---

Call the ModifyColdStorage API to enable capacity storage for an instance or modify the capacity storage space size.

<span id=".6K-35rGC57G75Z6L"></span>
## Request type

Synchronous request.

<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters


|**Name** |**Type** |**Required** |**Example value** |**Description** |
|---|---|---|---|---|
|InstanceId |String |Yes |hb\-cn01762cf4d6\*\*\*\* |Instance ID.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">You can call the <a href="https://docs.byteplus.com/en/docs/HBase/DescribeDBInstances">DescribeDBInstances</a> interface to query the basic information of all HBase instances in the target region, including the instance ID.</div><br> |
|ColdStorageStatus |Boolean |Yes |true |The status of Capacity storage. This value must be `true` when enabling or modifying Capacity storage. |
|ColdStorage |Long |Yes |600 |The size of the capacity storage space. The value ranges from 800 GiB to 1,000,000 GiB in 10 GiB increments.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">When scaling down, the target capacity storage space cannot be less than 120% of the currently used space. Please make a reasonable choice based on your actual business situation. You can call the <a href="https://docs.byteplus.com/en/docs/HBase/DescribeDBInstanceDetail">DescribeDBInstanceDetail</a> API to query the amount of used Capacity storage space for the instance.</div><br> |
|ClientToken |String |No |WbiAlPqJM6tMoSOYhT\*\*\*\* |Ensures the idempotence of the request and prevents repeated submissions. The client generates this parameter value, which must be unique across requests. The value is case\-sensitive and must not exceed 127 ASCII characters. |


<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameter


|**Name** |**Type** |**Example value** |**Description** |
|---|---|---|---|
|InstanceId |String |hb\-cn01762cf4d6\*\*\*\* |Instance ID. |
|OrderNo |String |Order716536966356027\*\*\*\* |Order ID. |


<span id=".56S65L6L"></span>
## Example

<span id=".6K-35rGC56S65L6L"></span>
### Request example

```JSON
POST /?Action=ModifyColdStorage&Version=2018-01-01 HTTP/1.1
Host: hbase.cn-beijing.byteplusapi.com.cn
Content-Type: application/json; charset=utf-8
X-Date: 20201103T104027Z
Authorization: HMAC-SHA256 Credential=AK****/20201103/cn-beijing/hbase/request,SignedHeaders=content-type;host;x-date,  Signature=****
{
    "InstanceId": "hb-cn01762cf4d6****",
    "ColdStorage": 820,
    "ColdStorageStatus": true
}
```


<span id=".6L-U5Zue56S65L6L"></span>
### Response example

```JSON
{
    "ResponseMetadata": {
        "RequestId": "202312131519401D22F7D1872A8BD99FA3",
        "Action": "ModifyColdStorage",
        "Version": "2018-01-01",
        "Service": "hbase",
        "Region": "cn-beijing"
    },
    "Result": {
        "InstanceId": "hb-cn01762cf4d6****",
        "OrderNo": "Order731197541786239****"
    }
}
```
