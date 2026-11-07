---
title: "CreateDBEndpoint"
product: "Table Storage for HBase"
product_code: "HBase"
source: "https://docs.byteplus.com/en/docs/HBase/CreateDBEndpoint"
---

Call the CreateDBEndpoint API to enable public access for the specified connection address.

<span id=".6K-35rGC57G75Z6L"></span>
## Request type

Asynchronous request.

<span id=".5rOo5oSP5LqL6aG5"></span>
## Precautions


* When you apply for a public IP address, it will be bound to your Elastic IP Address (EIP), and fees are charged by EIP. For more details, see [Billing overview](https://docs.byteplus.com/en/docs/eip/Billing-overview). You can call the [AllocateEipAddress](https://docs.byteplus.com/en/docs/eip/AllocateEipAddress) API to apply for a public IP.

* To enable the Thrift2 public connection address, you must first apply for a Thrift2 private connection address. You can call the [StartThrift2](https://docs.byteplus.com/en/docs/HBase/StartThrift2) API to apply for a Thrift2 private connection address for the specified instance.

* Enabling public network access for both ZK and Thrift2 connection addresses simultaneously is not supported.


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters


|**Name** |**Type** |**Required** |**Example value** |**Description** |
|---|---|---|---|---|
|InstanceId |String |Yes |hb\-cn016dc3297a\*\*\*\* |Instance ID.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">You can call the <a href="https://docs.byteplus.com/en/docs/HBase/DescribeDBInstances">DescribeDBInstances</a> interface to query the basic information of all HBase instances in the target region, including the instance ID.</div><br> |
|AddressType |String |Yes |Zk |The connection address type for which to enable public access. Value range:<br><br><br>* Zk: ZK connection address.<br><br>* Thrift: Thrift2 connection address. |
|EipList |Array of String |Yes |["eip\-30uwfh8l9a5ts7r2qr29o\*\*\*\* ", "eip\-3jhhte3gs0ruo3pncmfzm\*\*\*\* "] |The list of EIP IDs to associate with the public connection address.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="default">To enable public network access for a ZK connection address, you need to provide 2 EIP IDs. One EIP is required for the ZK node, and the other EIP is shared by other components in the instance (such as RS and Master nodes).</div><br><br><br>* <div data-tips="true" data-tips-type="default">To enable public network access for a Thrift2 connection address, you only need to provide 1 EIP ID.</div><br><br><br>* <div data-tips="true" data-tips-type="default">You can call the <a href="https://docs.byteplus.com/en/docs/eip/DescribeEipAddressAttributes">DescribeEipAddresses</a> interface to view all public IP information for the current account, including the EIP ID (the value of the <code>AllocationId</code> parameter in the returned data).</div><br> |
|ClientToken |String |No |WbiAlPqJM6tMoSOYhT\*\*\*\* |Ensures the idempotence of the request and prevents repeated submissions. The client generates this parameter value, which must be unique across requests. The value is case\-sensitive and must not exceed 127 ASCII characters. |


<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameter

None.

<span id=".56S65L6L"></span>
## Example

<span id=".6K-35rGC56S65L6LIDE="></span>
### Request example 1

Create a public ZK connection address

```JSON
POST /?Action=CreateDBEndpoint&Version=2018-01-01 HTTP/1.1
Host: hbase.cn-beijing.byteplusapi.com.cn
Content-Type: application/json; charset=utf-8
X-Date: 20201103T104027Z
Authorization: HMAC-SHA256 Credential=AK****/20201103/cn-beijing/hbase/request,SignedHeaders=content-type;host;x-date,  Signature=****
{
    "InstanceId": "hb-cn016dc3297a****",
    "EipList": [
        "eip-30uwfh8l9a5ts7r2qr29o****",
        "eip-3jhhte3gs0ruo3pncmfzm****"
    ],
    "AddressType": "Zk"
}
```


<span id=".6L-U5Zue56S65L6LIDE="></span>
### Response example 1

```JSON
{
    "ResponseMetadata": {
        "RequestId": "20230109205853EB443C38324455CA****",
        "Action": "CreateDBEndpoint",
        "Version": "2018-01-01",
        "Service": "hbase",
        "Region": "cn-beijing"
    },
    "Result": null
}
```


<span id=".6K-35rGC56S65L6LIDI="></span>
### Request example 2

Create a public Thrift2 connection address

```JSON
POST /?Action=CreateDBEndpoint&Version=2018-01-01 HTTP/1.1
Host: hbase.cn-beijing.byteplusapi.com.cn
Content-Type: application/json; charset=utf-8
X-Date: 20201103T104027Z
Authorization: HMAC-SHA256 Credential=AK****/20201103/cn-beijing/hbase/request,SignedHeaders=content-type;host;x-date,  Signature=****
{
    "InstanceId": "hb-cn016dc3297a****",
    "EipList": [
        "eip-30uwfh8l9a5ts7r2qr29o****"
    ],
    "AddressType": "Thrift"
}
```


<span id=".6L-U5Zue56S65L6LIDI="></span>
### Response example 2

```JSON
{
    "ResponseMetadata": {
        "RequestId": "20230109205853EB443C38324455CA****",
        "Action": "CreateDBEndpoint",
        "Version": "2018-01-01",
        "Service": "hbase",
        "Region": "cn-beijing"
    },
    "Result": null
}
```
