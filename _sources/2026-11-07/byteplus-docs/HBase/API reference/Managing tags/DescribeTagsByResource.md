---
title: "DescribeTagsByResource"
product: "Table Storage for HBase"
product_code: "HBase"
source: "https://docs.byteplus.com/en/docs/HBase/DescribeTagsByResource"
---

Call the DescribeTagsByResource interface to query the tag information associated with the instance.

<span id=".6K-35rGC57G75Z6L"></span>
## Request type

Synchronous request.

<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters


|**Name** |**Type** |**Required** |**Example value** |**Description** |
|---|---|---|---|---|
|InstanceIds |Array of String |Yes |[ "hb\-cncqbedcce3c\*\*\*\*", "hb\-cncqbedcce3c\*\*\*\*" ] |The ID of the instance whose associated tags you want to query.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="default">You can specify multiple instance IDs, separated by commas (,). You can specify a maximum of 50 instance IDs.</div><br><br><br>* <div data-tips="true" data-tips-type="default">You can call the <a href="https://docs.byteplus.com/en/docs/HBase/DescribeDBInstances">DescribeDBInstances</a> interface to query the basic information of all HBase instances in the target region, including the instance ID.</div><br> |
|TagFilters |Array of [TagFilterObject](https://docs.byteplus.com/en/docs/219/60856#tagfilterobject) |No |See the request example. |An array of tag key\-value pairs for querying and filtering.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="default">When you use tags to filter query results, the tag key (Key) is required, but the tag value (Value) is optional. If you do not specify a tag value, the system searches for all instances associated with the specified tag key.</div><br><br><br>* <div data-tips="true" data-tips-type="default">Up to 10 tag key\-value pairs can be passed in at a time for querying and filtering.</div><br> |
|PageSize |Integer |Yes |10 |The number of records per page. The value must be between 1 and 1000. |
|PageNumber |Integer |Yes |1 |The page number of the instance tag list. The value cannot exceed the maximum value of the Integer data type. The starting value is 1. |


<span id="tagfilterobject"></span>
### TagFilterObject


|**Name** |**Type** |**Required** |**Example value** |**Description** |
|---|---|---|---|---|
|Key |String |Yes |instancetype |Tag key for query filtering.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="default">This parameter is required to query and filter instances using tags.</div><br><br><br>* <div data-tips="true" data-tips-type="default">Duplicate tag keys are allowed.</div><br><br><br>* <div data-tips="true" data-tips-type="default">Up to 10 tags can be passed in at a time for query filtering.</div><br> |
|Value |String |No |cluster |The tag value that corresponds to the tag key for filtering queries.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="default">If this parameter is left empty, the tag value is not restricted, and all instances associated with the specified tag key are filtered.</div><br><br><br>* <div data-tips="true" data-tips-type="default">If you pass an empty string, the system filters for instances where the tag value is empty for the corresponding tag key.</div><br> |


<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameter


|**Name** |**Type** |**Example value** |**Description** |
|---|---|---|---|
|Total |Integer |3 |The total number of results that match the query criteria. |
|TagResources |Array of [TagResource](https://docs.byteplus.com/en/docs/219/60856#tagresource) |Refer to the Sample response. |The tag information associated with the instance. |


<span id="tagresource"></span>
### TagResource


|**Name** |**Type** |**Example value** |**Description** |
|---|---|---|---|
|Key |String |instancetype |The tag key associated with the instance. |
|Value |String |cluster |The value of the tag key associated with the instance. |
|InstanceId |String |hb\-cn019f341d51\*\*\*\* |Instance ID. |


<span id=".56S65L6L"></span>
## Example

<span id=".6K-35rGC56S65L6L"></span>
### Request example

```JSON
POST /?Action=DescribeTagsByResource&Version=2018-01-01 HTTP/1.1
Host: hbase.cn-beijing.byteplusapi.com.cn
Content-Type: application/json; charset=utf-8
X-Date: 20201103T104027Z
Authorization: HMAC-SHA256 Credential=AK****/20201103/cn-beijing/hbase/request,SignedHeaders=content-type;host;x-date,  Signature=****
{
    "InstanceIds": [
        "hb-cncqbedcce3c****",
        "hb-cncqbedcce3c****"
    ],
    "TagFilters": [
        {
            "Key": "instancetype",
            "Value": "cluster"
        },
        {
            "Key": "chargetype",
            "Value": "postpaid"
        }
    ],
    "PageNumber": 1,
    "PageSize": 10
}
```


<span id=".6L-U5Zue56S65L6L"></span>
### Response example

```JSON
{
    "ResponseMetadata": {
        "RequestId": "2023082814520678680D04B5DBAC619DF5",
        "Action": "DescribeTagsByResource",
        "Version": "2018-01-01",
        "Service": "hbase",
        "Region": "cn-beijing"
    },
    "Result": {
        "TagResources": [
            {
                "InstanceId": "hb-cncq335e3f13****",
                "Key": "chargetype",
                "Value": "prepaid"
            },
            {
                "InstanceId": "hb-cncq335e3f13****",
                "Key": "instancetype",
                "Value": "cluster"
            }
        ],
        "Total": 2
    }
}
```
