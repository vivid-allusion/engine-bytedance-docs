---
title: "UntagResources"
product: " Vital Kubernetes Engine"
product_code: "vke"
source: "https://docs.byteplus.com/en/docs/vke/UntagResources"
---

Remove a label from a resource.

<span id=".6K-35rGC6K-05piO"></span>
## Request description

VKE has deployed services in multiple regions globally to provide a stable and low\-latency access experience. You can refer to the [Service addresses](https://docs.byteplus.com/en/docs/vke/Service_addresses) topic and select the most suitable access point for your business region.


* Request method: POST

* Request URL: https://vke.cn\-beijing.byteplusapi.com.cn?Action=UntagResources&Version=2022\-05\-12


<span id=".6LCD6K-V"></span>
## Debugging

[去调试](https://api.byteplus.com/api-explorer/debug?action=UntagResources&serviceCode=vke&version=2022-05-12&groupName=)


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters

The following table lists the API request parameters. When calling this API, you also need to provide public parameters. See [public parameters](https://docs.byteplus.com/en/docs/vke/Common-parameters) for details.


|Parameters |Type |Required |Sample value |Description |
|---|---|---|---|---|
|Action |String |Yes |UntagResources |The API name. The name of the current API is `UntagResources`. |
|Version |String |Yes |2022\-05\-12 |The API version. The current version of the API is `2022-05-12`. |
|ResourceType |String |Yes |Cluster |The type of resources for which labels are to be disassociated. VKE supports the following two types of resource labels:<br><br><br>* **Cluster**<br><br>* **NodePool** |
|ResourceIds |Array of String |Yes |["cc9q8pbfqtofn8jxxxx"] |The list of resource IDs, which is a cluster ID list or a node pool ID list.<br><br>You can call the [ListClusters API](https://docs.byteplus.com/en/docs/vke/ListClusters) to obtain cluster IDs, and call the [ListNodePools](https://docs.byteplus.com/en/docs/vke/ListNodePools) API to obtain node pool IDs.<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">Warning</div><br><br><br><br>* <div data-tips="true" data-tips-type="warning">When you enter multiple resource IDs, the IDs cannot be repeated.</div><br><br><br>* <div data-tips="true" data-tips-type="warning">You can enter up to 50 resource IDs.</div><br> |
|TagKeys |Array of String |Yes |["key"] |The list of label keys to be disassociated. |


&nbsp;


|Parameters |Type |Required |Sample value |Description |
|---|---|---|---|---|
|Action |String |Yes |UntagResources |The API name. The name of the current API is `UntagResources`. |
|Version |String |Yes |2022\-05\-12 |The API version. The current version of the API is `2022-05-12`. |
|ResourceType |String |Yes |Cluster |The type of resources for which labels are to be disassociated. VKE supports the following two types of resource labels:<br><br><br>* **Cluster**<br><br>* **NodePool** |
|ResourceIds |Array of String |Yes |["cc9q8pbfqtofn8jxxxx"] |The list of resource IDs, which is a cluster ID list or a node pool ID list.<br><br>You can call the [ListClusters API](https://docs.byteplus.com/en/docs/vke/ListClusters) to obtain cluster IDs, and call the [ListNodePools](https://docs.byteplus.com/en/docs/vke/ListNodePools) API to obtain node pool IDs.<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">Warning</div><br><br><br><br>* <div data-tips="true" data-tips-type="warning">When you enter multiple resource IDs, the IDs cannot be repeated.</div><br><br><br>* <div data-tips="true" data-tips-type="warning">You can enter up to 50 resource IDs.</div><br> |
|TagKeys |Array of String |Yes |["key"] |The list of label keys to be disassociated. |


<span id=".6K-35rGC56S65L6L"></span>
## Sample requests

```json
POST /?Action=UntagResources&Version=2022-05-12 HTTP/1.1
Content-Type:application/json
{
    "ResourceType": "Cluster",
    "ResourceIds": [
        "cc5silumrsfeq****"
    ],
    "TagKeys": [
        "key1",
        "key2"
    ]
}
```


<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters

There are no API\-specific response parameters. See [Response results](https://docs.byteplus.com/en/docs/vke/Response) for details about public response parameters.

<span id=".6L-U5Zue56S65L6L"></span>
## Sample responses

```json
HTTP/1.1 200 OK
Content-Type:application/json
{
    "ResponseMetadata": {
        "RequestId": "0216353****",
        "Action": "UntagResources",
        "Version": "2022-05-12",
        "Service": "vke",
        "Region": "cn-beijing"
    },
    "Result": {}
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error code

There are no error codes proprietary to this API. See [Public error codes](https://docs.byteplus.com/en/docs/vke/Common-error-codes) for details.

&nbsp;
