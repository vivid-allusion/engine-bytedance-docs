---
title: "DeleteDBInstance"
product: "Table Storage for HBase"
product_code: "HBase"
source: "https://docs.byteplus.com/en/docs/HBase/DeleteDBInstance"
---

Call the DeleteDBInstance interface to delete a pay\-as\-you\-go instance.

<span id=".6K-35rGC57G75Z6L"></span>
## Request type

Asynchronous request.

<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites

The deletion protection function has been disabled. You can call the [ModifyInstanceDeletionProtectionPolicy](https://docs.byteplus.com/en/docs/HBase/ModifyInstanceDeletionProtectionPolicy) interface to disable instance deletion protection. For more information about removal protection, see [Instance deletion protection](https://docs.byteplus.com/en/docs/HBase/Instance_deletion_protection).

<span id=".5rOo5oSP5LqL6aG5"></span>
## Precautions

Only pay\-as\-you\-go HBase instances can be deleted by calling the DeleteDBInstance interface. You can only unsubscribe from yearly/monthly subscription instances through the console. For detailed steps, refer to [Unsubscribe from yearly/monthly subscription instance](https://docs.byteplus.com/en/docs/HBase/Deleting_or_unsubscribing_an_instance#.6YCA6K6i5YyF5bm05YyF5pyI5a6e5L6L).

<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters


|Name |Type |Required |Example value |Description |
|---|---|---|---|---|
|InstanceId |String |Yes |hb\-cn01bbb73ea0\*\*\*\* |Instance ID.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">You can call the <a href="https://docs.byteplus.com/en/docs/HBase/DescribeDBInstances">DescribeDBInstances</a> interface to query the basic information of all HBase instances in the target region, including the instance ID.</div><br> |
|ClientToken |String |No |WbiAlPqJM6tMoSOYhT\*\*\*\* |Ensures the idempotence of the request and prevents repeated submissions. The client generates this parameter value, which must be unique across requests. The value is case\-sensitive and must not exceed 127 ASCII characters. |


<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameter

None.

<span id=".56S65L6L"></span>
## Example

<span id=".6K-35rGC56S65L6L"></span>
### Request example

```json
POST /?Action=DeleteDBInstance&Version=2018-01-01 HTTP/1.1
Host: hbase.cn-beijing.byteplusapi.com.cn
Content-Type: application/json; charset=utf-8
X-Date: 20201103T104027Z
Authorization: HMAC-SHA256 Credential=AK****/20201103/cn-beijing/hbase/request,SignedHeaders=content-type;host;x-date,  Signature=****
{
    "InstanceId": "hb-cn01bbb73ea0****"
}
```


<span id=".6L-U5Zue56S65L6L"></span>
### Response example

```json
{
    "ResponseMetadata": {
        "RequestId": "202211092027580101742491480098****",
        "Action": "DeleteDBInstance",
        "Version": "2018-01-01",
        "Service": "hbase",
        "Region": "cn-beijing"
    },
    "Result": null
}
```
