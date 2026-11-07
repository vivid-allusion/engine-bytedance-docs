---
title: "AddTagsToResource"
product: "Table Storage for HBase"
product_code: "HBase"
source: "https://docs.byteplus.com/en/docs/HBase/AddTagsToResource"
---

Call the AddTagsToResource to associate tags to one or more instances.

<span id=".6K-35rGC57G75Z6L"></span>
## Request type

Asynchronous request.

<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters


|**Name** |**Type** |**Required** |**Example value** |**Description** |
|---|---|---|---|---|
|InstanceIds |Array of String |Yes |[ "hb\-cncqbedcce3c\*\*\*\*", "hb\-cncqbedcce3c\*\*\*\*" ] |The ID of the instance to add a tag to.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="default">You can call the <a href="https://docs.byteplus.com/en/docs/HBase/DescribeDBInstances">DescribeDBInstances</a> interface to query the basic information of all HBase instances in the target region, including the instance ID.</div><br><br><br>* <div data-tips="true" data-tips-type="default">You can specify multiple instance IDs, separated by commas (,). Each time, you can pass up to 20 instance IDs simultaneously, and each instance can bind up to 50 tags.</div><br> |
|Tags |Array of [TagObject](https://docs.byteplus.com/en/docs/219/60854#tagobject) |Yes |See the request example. |An array object of tag keys and tag values to be bound.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="default">It supports passing in multiple sets of tag key\-value objects at once, separated by commas (,). A single request supports up to 20 tag key\-value pairs, and a single instance can be bound with a maximum of 50 tags.</div><br><br><br>* <div data-tips="true" data-tips-type="default">The tag key value must meet certain setting rules. For details, please refer to the <a href="https://docs.byteplus.com/en/docs/HBase/Tag_overview">Tag setting rules</a>.</div><br> |


<span id="tagobject"></span>
### TagObject


|**Name** |**Type** |**Required** |**Example value** |**Description** |
|---|---|---|---|---|
|Key |String |Yes |department |The key of the tag to associate. |
|Value |String |No |game |The value of the tag to be associated. |


<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameter

None.

<span id=".56S65L6L"></span>
## Example

<span id=".6K-35rGC56S65L6L"></span>
### Request example

```JSON
POST /?Action=AddTagsToResource&Version=2018-01-01 HTTP/1.1
Host: hbase.cn-beijing.byteplusapi.com.cn
Content-Type: application/json; charset=utf-8
X-Date: 20201103T104027Z
Authorization: HMAC-SHA256 Credential=AK****/20201103/cn-beijing/hbase/request,SignedHeaders=content-type;host;x-date,  Signature=****
{
    "InstanceIds": [
        "hb-cncqbedcce3c****"
    ],
    "Tags": [
        {
            "Key": "department",
            "Value": "game"
        }
    ]
}
```


<span id=".6L-U5Zue56S65L6L"></span>
### Response example

```JSON
{
    "ResponseMetadata": {
        "RequestId": "202308281132166620963CF728A936C17B",
        "Action": "AddTagsToResource",
        "Version": "2018-01-01",
        "Service": "hbase",
        "Region": "cn-beijing"
    },
    "Result": null
}
```
