---
title: "ListTagsForResources"
product: "Parallel File Storage"
product_code: "pfs"
source: "https://docs.byteplus.com/en/docs/pfs/ListTagsForResources"
---

Call ListTagsForResources interface to filter PFS resources by label.

<span id="request-parameters"></span>
## Request parameters


|Name |Type |Required |Example |Description |
|---|---|---|---|---|
|ResourceType |String |No |filesystem |The type of resource to be filtered, the value selection description is as follows:<br><br>Filesystem: Represents a PFS instance. |
|ResourceIds |Array of String |No |[<br><br>"vepfs\-apse1dfff3e96\*\*\*\*",<br><br>"vepfs\-apse17cf88bf7\*\*\*\*"<br><br>] |The list of resource IDs that need to be filtered supports up to 50 resource IDs at a time, separated by a comma (,) between each ID.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">Tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">You can call the <a href="https://docs.byteplus.com/en/docs/pfs/DescribeFileSystems">DescribeFileSystems</a> interface to query the basic information of all file systems in the target region, including the file system ID.</div><br><br><br>* <div data-tips="true" data-tips-type="tip"><code>ResourceIds</code> and <code>TagFilters</code> cannot be empty at the same time and cannot be passed in at the same time.</div><br> |
|TagFilters |Array of [TagFilter](https://docs.byteplus.com/en/docs/pfs/ListTagsForResources?lang=en#tagfilter) |No |[<br><br>{<br><br>"Key": "key",<br><br>"Value": "value"<br><br>}<br><br>] |List of label filters, as follows:<br><br>You can pass in up to 10 label key\-value pairs at a time.<br><br>When multiple label key\-value pairs are passed in, multiple Keys are AND relationships, and different Values under the same Key are OR relationships.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">Tip</div><br><br><br><div data-tips="true" data-tips-type="tip"><code>ResourceIds</code> and <code>TagFilters</code> cannot be empty at the same time and cannot be passed in at the same time.</div><br> |
|PageSize |Integer |No |10 |Number of records per page, the default is 10. |
|PageNumber |Integer |No |1 |The page number of the list, up to the maximum value of the Integer data type, starting at 1. |


<span id="tagfilter"></span>
### TagFilter


|Name |Type |Required |Example |Description |
|---|---|---|---|---|
|Key |String |Yes |key |The label key to filter. |
|Value |String |No |value |The tag value to filter. |


<span id="response-parameters"></span>
## Response parameters


|Name |Type |Example |Description |
|---|---|---|---|
|ResourceTags |Array of [ResourceTag](https://docs.byteplus.com/en/docs/pfs/ListTagsForResources?lang=en#resourcetag) |See the return example for details |List of eligible resources. |
|PageSize |Integer |10 |The number of tags per page. |
|PageNumber |Integer |1 |The paginated page number of the tag list. |
|TotalCount |Integer |10 |The total number of eligible labels. |


<span id="resourcetag"></span>
### ResourceTag


|Name |Type |Example |Description |
|---|---|---|---|
|TagKey |String |key |Label key. |
|TagValue |String |value |Label value. |
|ResourceId |String |vepfs\-apse1dfff3e96\*\*\*\* |The resource ID that binds the tag. |
|ResourceType |String |instance |The resource type to bind the tag to. |


<span id="sample-request"></span>
## Sample request

```json
POST /?Action=ListTagsForResources&Version=2022-01-01 HTTP/1.1
Host: open.ap-southeast-1.byteplusapi.com
Authorization: HMAC-SHA256 Credential=AKLTOGJhY2E1NTdkZGFmNDg0Yjk0ZDFiNjE5Y2NjZjI****/20230907/ap-southeast-1/vepfs/request, SignedHeaders=host;x-date;x-content-sha256;content-type, Signature=7f1119a75111535b1d6e7929700f22e1474af0fb4fe26c59f5ac5cdba0cc****
Content-Type: application/json; charset=utf-8
X-Content-Sha256: 567112abe45bd6a09504fd244237f14c0ba120491da0d35097afd54d87bd****
X-Date: 20230907T124910Z
{
    "ResourceType": "filesystem",
    "ResourceIds": [
        "vepfs-apse1dfff3e96****",
        "vepfs-apse17cf88bf7****"
    ],
    "TagFilters": [
        {
            "Key": "key",
            "Value": "value"
        }
    ],
    "PageSize": 10,
    "PageNumber": 1
}
```


<span id="sample-response"></span>
## Sample response

```json
{
    "ResponseMetadata": {
        "Action": "ListTagsForResources",
        "Region": "ap-southeast-1",
        "Service": "vepfs",
        "Version": "2022-01-01",
        "RequestId": "20230604110420****100232280022D31"
    },
    "Result": {
        "ResourceTags": [
            {
                "TagKey": "key",
                "TagValue": "value",
                "ResourceId": "vepfs-apse1dfff3e96****",
                "ResourceType": "instance"
            }
        ],
        "PageSize": 10,
        "PageNumber": 1,
        "TotalCount": 10
    }
}
```
