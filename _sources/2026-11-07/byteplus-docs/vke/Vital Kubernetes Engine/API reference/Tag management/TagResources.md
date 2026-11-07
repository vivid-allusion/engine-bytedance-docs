---
title: "TagResources"
product: " Vital Kubernetes Engine"
product_code: "vke"
source: "https://docs.byteplus.com/en/docs/vke/TagResources"
---

Add a label to a specified resource.

<span id=".5L2_55So6K-05piO"></span>
## Usage instructions


* When you add a label to a resource, if the label key does not exist, a new label will be created. If a label with the same key already exists, the corresponding label value will be updated.

* Labels are categorized into user\-defined labels and system labels. Only user\-defined labels can be added to resources.

* You can add up to 50 user\-defined labels to each resource.


<span id=".6K-35rGC6K-05piO"></span>
## Request description

VKE has deployed services in multiple regions globally to provide a stable and low\-latency access experience. You can refer to the [Service addresses](https://docs.byteplus.com/en/docs/vke/Service_addresses) topic and select the most suitable access point for your business region.


* Request method: POST

* Request URL: https://vke.cn\-beijing.byteplusapi.com.cn?Action=TagResources&Version=2022\-05\-12


<span id=".6LCD6K-V"></span>
## Debugging

[去调试](https://api.byteplus.com/api-explorer/debug?action=TagResources&serviceCode=vke&version=2022-05-12&groupName=)


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters

The following table contains the request parameters for the API. You also need to provide public parameters when calling this API. See [Public parameters](https://docs.byteplus.com/en/docs/vke/Common-parameters) for details.


|Parameter |Type |Required |Sample value |Description |
|---|---|---|---|---|
|Action |String |Yes |TagResources |The API name. The name of the current API is `TagResources`. |
|Version |String |Yes |2022\-05\-12 |The API version. The current version of the API is `2022-05-12`. |
|ResourceType |String |Yes |Cluster |The type of resources for which labels are to be added. You can add resource labels only to clusters and node pools.<br><br><br>* **Cluster**<br><br>* **NodePool** |
|ResourceIds |Array of String |Yes |["cc5silumrsfeq\*\*\*\*"] |The list of resource IDs, which is a cluster ID list or a node pool ID list.<br><br>You can call the [ListClusters](https://docs.byteplus.com/en/docs/vke/ListClusters) API to obtain cluster IDs, and call the [ListNodePools](https://docs.byteplus.com/en/docs/vke/ListNodePools) API to obtain node pool IDs.<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">Warning</div><br><br><br><br>* <div data-tips="true" data-tips-type="warning">When you enter multiple resource IDs, the IDs cannot be repeated.</div><br><br><br>* <div data-tips="true" data-tips-type="warning">You can enter up to 50 resource IDs.</div><br> |
|Tags |Array of [Tag](https://docs.byteplus.com/en/docs/vke/TagResources#tag) |Yes |\- |The information about resource\-associated labels.<br><br><br>* Each **Key** of **Tags** must be unique.<br><br>* If the resource already has the same **Tags.Key**, an error will not occur if you bind the same **Tags.Key** again. Instead, the latest **Tags.Value** will be used.<br><br>* You can add up to 50 **labels** for each resource.<br><br>* The **Key** and **Value** in **Tags** cannot start or end with a space. |


<span id="tag"></span>
### Tag


|Parameters |Type |Required |Sample value |Description |
|---|---|---|---|---|
|Key |String |Yes |key |The label key.<br><br><br>* It must not start with `volc:` regardless of case.<br><br>* It can only contain characters, digits, spaces, and special characters `_.:/=+-@`.<br><br>* The length is limited to 1 to 128 characters. |
|Value |String |no |value |The label value, which can be left empty.<br><br><br>* It can only contain characters, digits, spaces, and special characters `_.:/=+-@`.<br><br>* Its length does not exceed 256 characters. |


<span id=".6K-35rGC56S65L6L"></span>
## Sample requests

```json
POST /?Action=TagResources&Version=2022-05-12 HTTP/1.1
Content-Type:application/json
{
    "ResourceType": "Cluster",
    "ResourceIds": [
        "cc5silumrsfeq****"
    ],
    "Tags": [
        {
            "Key": "key",
            "Value": "value"
        }
    ]
}
```


<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters

There are no response parameters proprietary to this API. See [Response results](https://docs.byteplus.com/en/docs/vke/Response) for details about public response parameters.

<span id=".6L-U5Zue56S65L6L"></span>
## Sample responses

```json
HTTP/1.1 200 OK
Content-Type:application/json
{
    "ResponseMetadata": {
        "RequestId": "0216353****",
        "Action": "TagResources",
        "Version": "2022-05-12",
        "Service": "vke",
        "Region": "cn-beijing"
    },
    "Result": {}
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error code

The error codes for this API are listed in the table below. Refer to the [Public error codes](https://docs.byteplus.com/en/docs/vke/Common-error-codes) topic.


|HTTP status code |Error code |Error message |Description |
|---|---|---|---|
|400 |QuotaExceeded.{{ResourceType}} |The quota of {{ResourceType}} has reached the limit. |The label resource quota has been reached. |


&nbsp;
