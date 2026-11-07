---
title: "RemoveTagsFromResource"
product: "Table Storage for HBase"
product_code: "HBase"
source: "https://docs.byteplus.com/en/docs/HBase/RemoveTagsFromResource"
---

Call the RemoveTagsFromResource to disassociate tags from one or more instances.

<span id=".6K-35rGC57G75Z6L"></span>
## Request type

Asynchronous request.

<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters


|**Name** |**Type** |**Required** |**Example value** |**Description** |
|---|---|---|---|---|
|InstanceIds |Array of String |Yes |[ "hb\-cncqbedcce3c\*\*\*\*", "hb\-cncqbedcce3c\*\*\*\*" ] |The instance ID for which the tag needs to be removed.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="default">You can call the <a href="https://docs.byteplus.com/en/docs/HBase/DescribeDBInstances">DescribeDBInstances</a> API to query the basic information of all instances in the target region, including their instance IDs.</div><br><br><br>* <div data-tips="true" data-tips-type="default">You can specify multiple instance IDs, separated by commas (,). You can specify a maximum of 20 instance IDs.</div><br> |
|TagKeys |Array of String |No |["instancetype", "chargetype"] |The tag keys to remove.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="default">You can enter multiple tag keys, separated by commas (,). You can pass a maximum of 20 tag keys at once.</div><br><br><br>* <div data-tips="true" data-tips-type="default">When <code>InstanceIds</code> contains multiple instance IDs, tags with the provided tag keys will be removed from all of them. Proceed with caution.</div><br> |
|All |Boolean |No |false |Whether to remove all tags on the specified instance. Value range:<br><br><br>* `true`: remove all tags from the specified instance.<br><br>* `false`: do not remove all tags from the specified instance (default).<br><br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">The <code>All</code> parameter takes effect only when <code>TagKeys</code> is empty.</div><br> |


<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameter

None.

<span id=".56S65L6L"></span>
## Example

<span id=".6K-35rGC56S65L6L"></span>
### Request example

```JSON
POST /?Action=RemoveTagsFromResource&Version=2018-01-01 HTTP/1.1
Host: hbase.cn-beijing.byteplusapi.com.cn
Content-Type: application/json; charset=utf-8
X-Date: 20201103T104027Z
Authorization: HMAC-SHA256 Credential=AK****/20201103/cn-beijing/hbase/request,SignedHeaders=content-type;host;x-date,  Signature=****
{
    "InstanceIds": [
        "hb-cncqbedcce3c****"
    ],
    "TagKeys": [
        "instancetype",
        "chargetype"
    ],
    "All": false
}
```


<span id=".6L-U5Zue56S65L6L"></span>
### Response example

```JSON
{
    "ResponseMetadata": {
        "RequestId": "20230828113857341E2CA8E14426319DA1",
        "Action": "RemoveTagsFromResource",
        "Version": "2018-01-01",
        "Service": "hbase",
        "Region": "cn-beijing"
    },
    "Result": null
}
```
