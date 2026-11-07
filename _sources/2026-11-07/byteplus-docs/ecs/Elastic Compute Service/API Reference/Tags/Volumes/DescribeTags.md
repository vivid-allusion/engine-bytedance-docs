---
title: "DescribeTags"
product: "Elastic Compute Service"
product_code: "ecs"
source: "https://docs.byteplus.com/en/docs/ecs/DescribeTags-01"
---

Call DescribeTags to query resources that have associated tags.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">You are allowed to call this API action to query up to 10 tags at a time.</div>


* <div data-tips="true" data-tips-type="tip">Up to three tag values can be queried by using a tag key.</div>



<span id="request-parameters"></span>
## Request parameters


|Name |Type |Required |Example |Description |
|---|---|---|---|---|
|Action |String |Yes |DescribeTags |The action that you want to perform. Value: DescribeTags. |
|ResourceType |String |Yes |volume |The resource type. Valid values:<br><br><br>* volume |
|ResourceIds.N |String |Yes |ResourceIds.1=vol\-76pwr6rilv8lzwxv\*\*\*\*&ResourceIds.2=vol\-76pwr6rilv8lzwxv\*\*\*\* |The resource ID.<br><br><br>* Parameter \- N specifies the serial number of the resource. Valid values: 1–50.<br><br>* Separate resources with ampersands ( & ). |
|TagFilters.N.Key |String |No |TagFilters.1.Key=k1 |The tag key you specified when querying resources using tags.<br><br><br>* Parameter \- N specifies the serial number of the tag key. Valid values: 1–10.<br><br>* Separate tag keys with ampersands ( & ). Each tag key must be unique.<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">All tags are queried if you do not specify a value for this parameter.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">If you specify an empty string, the <code>InvalidTagFilterKey.Malformed</code> error code will be returned.</div><br> |
|TagFilters.N.Values.N |String |No |TagFilters.1.Values.1=v1&TagFilters.1.Values.2=v2 |The tag value you specified when querying resources using tags.<br><br><br>* The first N specifies the serial number of the tag key. Valid values: 1–10.<br><br>* The second N specifies the serial number of the tag value. Valid values: 1–3.<br><br>* Separate tag values with ampersands ( & ).<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">Before specifying a value for this parameter, you must specify a value for <code>TagFilters.N.Key</code> first.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">If you do not specify a value for this parameter, all tag values corresponding to the tag key are queried.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">If you specify an empty string, tags with empty values are queried.</div><br> |
|SysTagVisible |Boolean |No |false |Whether to display system tags.Valid values:<br><br><br>* true:Display system tags.<br><br>* false:Do not display system tags.The default value is false. |
|PageNumber |Integer |No |1 |The page number. |
|PageSize |Integer |No |15 |The number of entries on each page. |


<span id="response-parameters"></span>
## Response parameters


|Name |Type |Example |Description |
|---|---|---|---|
|PageNumber |Integer |1 |The page number. |
|PageSize |Integer |15 |The number of entries on each page. |
|TagResources |Array of TagResources |\- |A collection consisting of resources and tags.For more information, refer to **TagResources structure.**  |
|TotalCount |Integer |1 |Total count of resources that meet the criteria. |


**TagResources structure**


|Name |Type |Example |Description |
|---|---|---|---|
|ResourceType |String |volume |Resource type.Valid values:<br><br><br>* volume |
|ResourceId |String |vol\-jfrnoryrnpgn6u5w\*\*\*\* |Resource ID. |
|TagKey |String |tag |Tag keys for the attached tags of the resource. |
|TagValue |String |test |Tag values for the attached tags of the resource. |


<span id="sample-request"></span>
## Sample request

```Plain Text
GET /?Action=DescribeTags&Version=2020-04-01&ResourceType=volume&ResourceIds.1=vol-76pwr6rilv8lzwxv*****&ResourceIds.2=vol-76pwr6rilv8lzwxv**** HTTP/1.1
Host: open.ap-southeast-1.byteplusapi.com
Region: ap-southeast-1
ServiceName: storage_ebs
```


<span id="sample-response"></span>
## Sample response

```Plain Text
{
    "ResponseMetadata": {
        "RequestId": "20230303143154E698024A111791BD1EA2",
        "Action": "DescribeTags",
        "Version": "2020-04-01",
        "Service": "storage_ebs",
        "Region": "ap-southeast-1"
    },
    "Result": {
        "PageNumber": 1,
        "PageSize": 15,
        "TagResources": [
            {
                "ResourceId": "vol-jfrnoryrnpgn6u5w****",
                "ResourceType": "volume",
                "TagKey": "tag",
                "TagValue": "test"
            }
        ],
        "TotalCount": 1
    }
}
```


<span id="error-codes"></span>
## Error codes


|**HttpCode** |**Error Code** |**Error Message** |
|---|---|---|
|400 |ErrTagServiceUnavailable |tag service unavailable |
|400 |ErrTagNotFound |tag not found in request |
|400 |InvalidTagKeyConflict |tag key conflict |
|400 |ErrInvalidTagKey |tag key invalid |
|400 |ErrInvalidTagValue |tag value invalid |
|400 |ErrTagKeyNotFound |tag key not found |
|400 |ErrMaximumResourceIds |too many resource ids |
|400 |ErrResourceTypeNotFound |resource type not found |
|400 |ErrResourceTypeUnknown |resource type unknown |
|400 |ErrInvalidAccountId |account id invalid |
|400 |ErrMaximumTagFilterKeys |too many tag filter keys |
|400 |ErrInvalidTagFilterKey |tag filter key invalid |
|400 |ErrMaximumTagFilterValues |too many tag filter value |
|400 |ErrInvalidTagFilterValue |tag filter value invalid |
