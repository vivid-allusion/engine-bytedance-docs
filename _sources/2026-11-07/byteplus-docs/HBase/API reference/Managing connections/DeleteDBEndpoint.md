---
title: "DeleteDBEndpoint"
product: "Table Storage for HBase"
product_code: "HBase"
source: "https://docs.byteplus.com/en/docs/HBase/DeleteDBEndpoint"
---

Call the DeleteDBEndpoint interface to close public network access to the specified connection address.

<span id=".6K-35rGC57G75Z6L"></span>
## Request type

Asynchronous request.

<span id=".5rOo5oSP5LqL6aG5"></span>
## Precautions


* After disabling public network access, the corresponding public network access address will be deleted, and the client will not be able to access the HBase instance through the original public network address. Please confirm that your business does not use public network addresses to avoid losses.

* After public network access is disabled, the associated EIP is automatically unbound. The unbound EIP will be retained and continue to incur charges. If no longer needed, release the relevant resources manually. To learn how to release an EIP, see [Releasing an EIP](https://docs.byteplus.com/en/docs/eip/Releasing-an-EIP).

* To ensure database security, we recommend promptly deleting the IP addresses of related client devices from the IP allowlist after you disable public network access. You can call the [ModifyAllowList](https://docs.byteplus.com/en/docs/HBase/ModifyAllowList) API to modify a specified IP allowlist, such as its name and IP addresses. For more information about allowlists, see [Configuring an allowlist](https://docs.byteplus.com/en/docs/HBase/Configuring_an_Allowlist).


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters


|**Name** |**Type** |**Required** |**Example value** |**Description** |
|---|---|---|---|---|
|InstanceId |String |Yes |hb\-cn016dc3297a\*\*\*\* |Instance ID.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">You can call the <a href="https://docs.byteplus.com/en/docs/HBase/DescribeDBInstances">DescribeDBInstances</a> interface to query the basic information of all HBase instances in the target region, including the instance ID.</div><br> |
|ClientToken |String |No |WbiAlPqJM6tMoSOYhT\*\*\*\* |Ensures the idempotence of the request and prevents repeated submissions. The client generates this parameter value, which must be unique across requests. The value is case\-sensitive and must not exceed 127 ASCII characters. |


<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameter

None.

<span id=".56S65L6L"></span>
## Example

<span id=".6K-35rGC56S65L6L"></span>
### Request example

```JSON
POST /?Action=DeleteDBEndpoint&Version=2018-01-01 HTTP/1.1
Host: hbase.cn-beijing.byteplusapi.com.cn
Content-Type: application/json; charset=utf-8
X-Date: 20201103T104027Z
Authorization: HMAC-SHA256 Credential=AK****/20201103/cn-beijing/hbase/request,SignedHeaders=content-type;host;x-date,  Signature=****
{
    "InstanceId": "hb-cn016dc3297a****"
}
```


<span id=".6L-U5Zue56S65L6L"></span>
### Response example

```JSON
{
    "ResponseMetadata": {
        "RequestId": "2023010920524296FEEE3647BD0EE8****",
        "Action": "DeleteDBEndpoint",
        "Version": "2018-01-01",
        "Service": "hbase",
        "Region": "cn-beijing"
    },
    "Result": null
}
```
