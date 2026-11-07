---
title: "UpgradeDBInstanceThriftServer"
product: "Table Storage for HBase"
product_code: "HBase"
source: "https://docs.byteplus.com/en/docs/HBase/UpgradeDBInstanceThriftServer"
---

Call the UpgradeDBInstanceThriftServer API to upgrade a legacy Thrift2 connection address to high\-availability Thrift mode.

<span id=".6K-35rGC57G75Z6L"></span>
## Request type

Asynchronous request.

<span id=".5rOo5oSP5LqL6aG5"></span>
## Precautions

The instance has a legacy Thrift2 connection address.

<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters


|**Name** |**Type** |**Required** |**Example value** |**Description** |
|---|---|---|---|---|
|InstanceId |String |Yes |hb\-cn01762cf4d6\*\*\*\* |Instance ID. |
|ThriftServerSpec |Object of [ThriftServerResourceSpec](https://docs.byteplus.com/en/docs/219/120641#thriftserverresourcespec) |Yes |See the request example |Thrift Server specification configuration. |
|ClientToken |String |No |WbiAlPqJM6tMoSOYhT\*\*\*\* |Ensures the idempotence of the request and prevents repeated submissions. The client generates this parameter value, which must be unique across requests. The value is case\-sensitive and must not exceed 127 ASCII characters. |


<span id="thriftserverresourcespec"></span>
### ThriftServerResourceSpec


|**Name** |**Type** |**Required** |**Example value** |**Description** |
|---|---|---|---|---|
|NodeSpec |String |No |hbase.x1.2xlarge |The specification code of the Thrift Server node. |
|NodeCount |Integer |No |2 |The number of Thrift Server nodes. The value must be an integer from 2 to 100. |


<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameter


|**Name** |**Type** |**Example value** |**Description** |
|---|---|---|---|
|InstanceId |String |hb\-cn01762cf4d6\*\*\*\* |Instance ID. |
|OrderNo |String |Order730602621667020\*\*\*\* |Order ID. |


<span id=".56S65L6L"></span>
## Example

<span id=".6K-35rGC56S65L6L"></span>
### Request example

```JSON
POST /?Action=UpgradeDBInstanceThriftServer&Version=2018-01-01 HTTP/1.1
Host: hbase.cn-beijing.byteplusapi.com.cn
Content-Type: application/json; charset=utf-8
X-Date: 20201103T104027Z
Authorization: HMAC-SHA256 Credential=AK****/20201103/cn-beijing/hbase/request,SignedHeaders=content-type;host;x-date,  Signature=****
{
    "InstanceId": "hb-cn01762cf4d6****",
    "ThriftServerSpec": {
        "NodeSpec": "hbase.x1.2xlarge",
        "NodeSpec": 2
    }
}
```


<span id=".6L-U5Zue56S65L6L"></span>
### Response example

```JSON
{
    "ResponseMetadata": {
        "Action": "UpgradeDBInstanceThriftServer",
        "Region": "cn-beijing",
        "Service": "hbase",
        "Version": "2018-01-01",
        "RequestId": "20230604110420****100232280022D31"
    },
    "Result": {
        "InstanceId": "hb-cn01762cf4d6****",
        "OrderNo": "Order730602621667020****"
    }
}
```
