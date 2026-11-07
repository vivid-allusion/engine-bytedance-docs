---
title: "ListTagsForResources"
product: " Vital Kubernetes Engine"
product_code: "vke"
source: "https://docs.byteplus.com/en/docs/vke/ListTagsForResources"
---

List all tags for resources that meet the specified conditions.

<span id=".6K-35rGC6K-05piO"></span>
## Request description

VKE has deployed services in multiple regions globally to provide a stable and low\-latency access experience. You can refer to the [Service addresses](https://docs.byteplus.com/en/docs/vke/Service_addresses) topic and select the most suitable access point for your business region.


* Request method: POST

* Request URL: https://vke.cn\-beijing.byteplusapi.com.cn?Action=ListTagsForResources&Version=2022\-05\-12


<span id=".6LCD6K-V"></span>
## Debugging

[去调试](https://api.byteplus.com/api-explorer/debug?action=ListTagsForResources&serviceCode=vke&version=2022-05-12&groupName=)


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters

The following table describes the API request parameters. You also need to provide public parameters when calling this API. See [Public parameters](https://docs.byteplus.com/en/docs/vke/Common-parameters) for details.


|Parameters |Type |Required |Sample value |Description |
|---|---|---|---|---|
|Action |String |Yes |ListTagsForResources |The API name. The name of the current API is `ListTagsForResources`. |
|Version |String |Yes |2022\-05\-12 |The API version. The current version of the API is `2022-05-12`. |
|ResourceType |String |Yes |Cluster |The resource type of the label. VKE supports the following two types of resource labels:<br><br><br>* **Cluster**<br><br>* **NodePool** |
|ResourceIds |Array of String |no |["cc5silumrsfeq\*\*\*\*"] |The list of resource IDs, which is a cluster ID list or a node pool ID list.<br><br>You can call the [ListClusters](https://docs.byteplus.com/en/docs/vke/ListClusters) API to obtain cluster IDs, and call the [ListNodePools](https://docs.byteplus.com/en/docs/vke/ListNodePools) API to obtain node pool IDs.<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">Warning</div><br><br><br><br>* <div data-tips="true" data-tips-type="warning">When you enter multiple resource IDs, the IDs cannot be repeated.</div><br><br><br>* <div data-tips="true" data-tips-type="warning">You can enter up to 50 resource IDs.</div><br> |
|TagFilters |Array of [TagFilter](https://docs.byteplus.com/en/docs/vke/ListTagsForResources#tagfilter) |no |\- |List of tags. Multiple keys are combined with AND, while different values under the same key are combined with OR.<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">Warning</div><br><br><br><br>* <div data-tips="true" data-tips-type="warning"><strong>TagFilter.Key</strong> cannot be repeated.</div><br><br><br>* <div data-tips="true" data-tips-type="warning">Up to 10 <strong>TagFilter</strong> are supported.</div><br> |
|Type |String |no |Custom |The label type. Valid values:<br><br><br>* **System**: System label<br><br>* **Custom**: user\-defined label |
|NextToken |String |no |Mzgw |The pagination token, which is used to indicate the start position from which to retrieve data on the next page.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">You do not specify this parameter when you call the API for the first time. When you query resource labels, the value is the value of the <strong>NextToken</strong> parameter returned by the previous call.</div><br> |
|MaxResults |Integer |no |10 |The number of results per page:<br><br><br>* Minimum value: 1<br><br>* Maximum value: 100<br><br>* Default value: 10 |


&nbsp;


|Parameters |Type |Required |Sample value |Description |
|---|---|---|---|---|
|Action |String |Yes |ListTagsForResources |The API name. The name of the current API is `ListTagsForResources`. |
|Version |String |Yes |2022\-05\-12 |The API version. The current version of the API is `2022-05-12`. |
|ResourceType |String |Yes |Cluster |The resource type of the label. VKE supports the following two types of resource labels:<br><br><br>* **Cluster**<br><br>* **NodePool** |
|ResourceIds |Array of String |no |["cc5silumrsfeq\*\*\*\*"] |The list of resource IDs, which is a cluster ID list or a node pool ID list.<br><br>You can call the [ListClusters](https://docs.byteplus.com/en/docs/vke/ListClusters) API to obtain cluster IDs, and call the [ListNodePools](https://docs.byteplus.com/en/docs/vke/ListNodePools) API to obtain node pool IDs.<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">Warning</div><br><br><br><br>* <div data-tips="true" data-tips-type="warning">When you enter multiple resource IDs, the IDs cannot be repeated.</div><br><br><br>* <div data-tips="true" data-tips-type="warning">You can enter up to 50 resource IDs.</div><br> |
|TagFilters |Array of [TagFilter](https://docs.byteplus.com/en/docs/vke/ListTagsForResources#tagfilter) |no |\- |List of tags. Multiple keys are combined with AND, while different values under the same key are combined with OR.<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">Warning</div><br><br><br><br>* <div data-tips="true" data-tips-type="warning"><strong>TagFilter.Key</strong> cannot be repeated.</div><br><br><br>* <div data-tips="true" data-tips-type="warning">Up to 10 <strong>TagFilter</strong> are supported.</div><br> |
|Type |String |no |Custom |The label type. Valid values:<br><br><br>* **System**: System label<br><br>* **Custom**: user\-defined label |
|NextToken |String |no |Mzgw |The pagination token, which is used to indicate the start position from which to retrieve data on the next page.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">You do not specify this parameter when you call the API for the first time. When you query resource labels, the value is the value of the <strong>NextToken</strong> parameter returned by the previous call.</div><br> |
|MaxResults |Integer |no |10 |The number of results per page:<br><br><br>* Minimum value: 1<br><br>* Maximum value: 100<br><br>* Default value: 10 |


<span id="tagfilter"></span>
### TagFilter


|Parameters |Type |Required |Sample value |Description |
|---|---|---|---|---|
|Key |String |Yes |key |The label key. |
|Values |Array of String |no |["value"] |The label value list. You can leave this parameter empty. |


<span id=".6K-35rGC56S65L6L"></span>
## Sample requests

```json
POST /?Action=ListTagsForResources&Version=2022-05-12 HTTP/1.1
Content-Type:application/json
{
    "ResourceType": "Cluster",
    "ResourceIds": [
        "cc5silumrsfeq****"
    ],
    "TagFilters": [
        {
            "Key": "key",
            "Values": [
                "value1",
                "value2"
            ]
        }
    ],
    "Type": "Custom",
    "NextToken": "MTIzNDU=",
    "MaxResults": 10
}
```


<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters

The following table contains the response parameters of this API. See [Response results](https://docs.byteplus.com/en/docs/vke/Response) for details about public response parameters.


|Parameters |Type |Sample value |Description |
|---|---|---|---|
|ResourceTags |Array of [ResourceTag](https://docs.byteplus.com/en/docs/vke/ListTagsForResources#resourcetag) | |The list of resource\-associated labels. |
|NextToken |String |Mzgw |The pagination token, which is used to indicate the start position from which to retrieve data on the next page.<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">After you call this API each time, you can save the value of this parameter to display the next page of resource label information in subsequent queries by page.</div><br> |


<span id="resourcetag"></span>
### ResourceTag


|Parameters |Type |Sample value |Description |
|---|---|---|---|
|ResourceType |String |Cluster |The resource type. Valid values:<br><br><br>* **Cluster**<br><br>* **NodePool** |
|ResourceId |String |cc9l74mvqt\*\*\*\* |The resource ID. |
|TagKey |String |Key |The label key. |
|TagValue |String |Value |The label value. |
|Type |String |Custom |The label type. Valid values:<br><br><br>* **System**: System label<br><br>* **Custom**: user\-defined label |


<span id=".6L-U5Zue56S65L6L"></span>
## Sample responses

```json
HTTP/1.1 200 OK
Content-Type:application/json
{
    "ResponseMetadata": {
        "RequestId": "0216353****",
        "Action": "ListTagsForResources",
        "Version": "2022-05-12",
        "Service": "vke",
        "Region": "cn-beijing"
    },
    "Result": {
        "NextToken": "MTIzNDU=",
        "ResourceTags": [
            {
                "ResourceType": "Cluster",
                "ResourceId": "cc5sil****",
                "TagKey": "key",
                "TagValue": "value",
                "Type": "Custom"
            }
        ]
    }
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error code

There are no error codes proprietary to this API. See [Public error codes](https://docs.byteplus.com/en/docs/vke/Common-error-codes) for details about public error codes.

&nbsp;
