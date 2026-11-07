---
title: "DescribeTags - Queries tagged resources (earlier version)"
product: "Elastic Compute Service"
product_code: "ecs"
source: "https://docs.byteplus.com/en/docs/ecs/DescribeTags"
---

Call the DescribeTags operation to query resources associated with tags.

<span id=".5L2_55So6K-05piO"></span>
## Usage notes

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">This page describes the tag\-targeted operation of the earlier version, which may no longer be maintained in the future. The new version of tag\-targeted interfaces supports more scenarios. We recommend new users use the following new versions of the interfaces.</div>



* <div data-tips="true" data-tips-type="warning"><a href="https://docs.byteplus.com/en/docs/ecs/TagResources">TagResources \- Creates tags (new version)</a></div>


* <div data-tips="true" data-tips-type="warning"><a href="https://docs.byteplus.com/en/docs/ecs/UntagResources">UntagResources \- Deletes tags (new version)</a></div>


* <div data-tips="true" data-tips-type="warning"><a href="https://docs.byteplus.com/en/docs/ecs/ListTagsForResources">ListTagsForResources \- Queries tagged resources (new version)</a></div>



<span id=".5rOo5oSP5LqL6aG5"></span>
## Usage notes


* This operation supports a maximum of 10 tags per query.

* You can query up to three tag values for the same tag key.


<span id=".6LCD6K-V"></span>
## Debugging

[去调试](https://api.byteplus.com/api-explorer/?action=DescribeTags&groupName=%E6%A0%87%E7%AD%BE&serviceCode=ecs&version=2020-04-01)


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters

Only the request parameters specific to this operation and some common parameters are listed below. For more information, refer to [Common parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).



**Action** <span data-label="purple">string</span> <span data-api-tag="require|PNinID">必选</span> `Sample value: DescribeTags`

The action that you want to perform. Value: DescribeTags.



**Version** <span data-label="purple">string</span> <span data-api-tag="require|vgkzCW">必选</span> `Sample value: 2020-04-01`

The version of the API. Valid value: 2020\-04\-01.



**MaxResults** <span data-label="purple">integer</span> `Optional` `Sample value: 10`

The number of entries returned on each page in a pagination query.


* Maximum value: 100

* Default value: 10



**NextToken** <span data-label="purple">string</span> `Optional` `Sample value: bHpwdXJja2RxemU1eG5sb3NzdGcW1-RCEq******`

Pagination token marking the query position. Omit this parameter for initial API requests. In the next query, set the NextToken parameter to the value returned by the previous API call.



**ResourceIds.N** <span data-label="purple">string[]</span> `Optional` `Sample value: ResourceIds.1=i-l8u0p77yseabkpak****&ResourceIds.2=i-l8u0p7xyseabkbak****`

The resource ID.


* Argument \- N: indicates the serial number of the resource. Valid range: 1\-50.

* Separate resources with &.



**ResourceType** <span data-label="purple">string</span> <span data-api-tag="require|SMCtzQ">必选</span> `Sample value: instance`

The resource type. Valid values:


* instance: instance

* image: image

* reservedinstance: Reserved Instances (RI)

* scheduledinstance: Elastic Scheduled Instances (ESI)

* keypair: key pair



**TagFilters.N.Key** <span data-label="purple">string[]</span> `Optional` `Sample value: TagFilters.1.Key=k1`

The specified tag key when querying resources based on tags.


* Argument \- N: specifies the serial number of the tag key. Valid range: 1–10.

* Separate multiple tag keys with "&". Duplicate tag keys are not allowed.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">If you do not pass in the parameter, all tags are queried.</div>


* <div data-tips="true" data-tips-type="tip">When an empty string is passed in, the error code InvalidTagFilterKey.Malformed is returned.</div>




**TagFilters.N.Values.N** <span data-label="purple">string[]</span> `Optional` `Sample value: TagFilters.1.Values.1=v1&TagFilters.1.Values.2=v2`

The specified tag value when querying resources based on tags.


* The first N: specifies the serial number of the tag key. Value range: 1–10.

* The second N: specifies the serial number of a tag value. Value range: 1–3.

* Separate multi values with ampersands (&).


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">To pass in this parameter, pass in <code>TagFilters.N.Key</code> first.</div>


* <div data-tips="true" data-tips-type="tip">If you do not pass in the TagFilters.N.Key parameter, all tag values corresponding to the same tag key are queried.</div>


* <div data-tips="true" data-tips-type="tip">If you specify an empty string, you query tags with an empty tag value.</div>




&nbsp;

<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters

Only the response parameters specific to this operation are listed below. For more information, refer to the [response structure](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response).



**NextToken** <span data-label="purple">string</span> `Sample value: bHpwdXJja2RxemU1eG5sb3NzdGcW1-RCEq******`

The query credentials value returned by this call. If null is returned, this page is the last page.



**TagResources** <span data-label="purple">object[]</span> `Sample value: --`

This parameter contains resource information and associated tags.


**ResourceId** <span data-label="purple">string</span> `Sample value: i-l8u0p77yseabkpak****`

The resource ID.



**ResourceType** <span data-label="purple">string</span> `Sample value: instance`

Resource type.



**TagKey** <span data-label="purple">string</span> `Sample value: k1`

The key of the tag associated with the resource.



**TagValue** <span data-label="purple">string</span> `Sample value: v1`

The value of the tag associated with the resource.


&nbsp;


**ResourceId** <span data-label="purple">string</span> `Sample value: i-l8u0p77yseabkpak****`

The resource ID.



**ResourceType** <span data-label="purple">string</span> `Sample value: instance`

Resource type.



**TagKey** <span data-label="purple">string</span> `Sample value: k1`

The key of the tag associated with the resource.



**TagValue** <span data-label="purple">string</span> `Sample value: v1`

The value of the tag associated with the resource.




&nbsp;

<span id=".6K-35rGC56S65L6L"></span>
## Sample request

```text
GET /?Action=DescribeTags&Version=2020-04-01&ResourceType=instance&ResourceIds.1=i-l8u0p77yseabkpak****&ResourceIds.2=i-l8u0p7xyseabkbak****&TagFilters.1.Key=k1&TagFilters.1.Values.1=v1&TagFilters.1.Values.2=v2 HTTP/1.1
Host: ecs.cn-beijing.byteplusapi.com.cn
Region: cn-beijing
ServiceName: ecs
```


<span id=".6L-U5Zue56S65L6L"></span>
## Sample response

```json
{
    "ResponseMetadata": {
        "RequestId": "2021062415303301022514515207C4****",
        "Action": "DescribeTags",
        "Version": "2020-04-01",
        "Service": "ecs",
        "Region": "cn-beijing"
    },
    "Result": {
        "NextToken": "bHpwdXJja2RxemU1eG5sb3NzdGcW1-RCEq******"
        "TagResources": [
            {
                "ResourceType": "instance",
                "ResourceId": "i-l8u0p77yseabkpak****",
                "TagKey": "k1",
                "TagValue": "v1"
            },
            {
                "ResourceType": "instance",
                "ResourceId": "i-l8u0p7xyseabkbak****",
                "TagKey": "k1",
                "TagValue": "v2"
            }
        ]
    }
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error codes

The table below lists the business\-related error codes of the operation. For more information, refer to [Common error codes](https://docs.byteplus.com/en/docs/ecs/Public-error-codes).


|Status code |Error code |Error message |Description |
|---|---|---|---|
|400 |InvalidArgument |The specified argument is invalid. |The specified parameter is invalid. |
|400 |InvalidTagFilterKey.Malformed |The specified TagFilterKey is malformed. |The format of the specified tag key for query is invalid. |
|400 |InvalidTagFilterValue.Malformed |The specified TagFilterValue is malformed. |The format of the specified tag value for query is invalid. |
|400 |LimitExceeded.MaximumResourceIds |You've reached the limit on the number of ResourceIds that you can set. |The specified number of resource IDs exceeds the limit. |
|400 |LimitExceeded.MaximumTagFilterKeys |You've reached the limit on the number of TagFilterKeys that you can set. |The specified query tag key is out of range. |
|400 |LimitExceeded.MaximumTagFilterValues |You've reached the limit on the number of TagFilterValues that you can set. |The specified query tag value exceeds the valid range. |
|404 |InvalidResourceType.NotFound |The specified ResourceType does not exist. |The specified resource type does not exist. |
|409 |InvalidTagFilterKey.Conflict |The specified TagFilterKey already exists. |The specified tag filter key already exists. |
