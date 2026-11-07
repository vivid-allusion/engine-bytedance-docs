---
title: "ListImageCaches"
product: " Vital Kubernetes Engine"
product_code: "vke"
source: "https://docs.byteplus.com/en/docs/vke/ListImageCaches"
---

Query the list of image caches that meet the specified criteria.

<span id=".6K-35rGC6K-05piO"></span>
## Request description

VKE has deployed services in multiple regions globally to provide a stable and low\-latency access experience. You can refer to the [Service addresses](https://docs.byteplus.com/en/docs/vke/Service_addresses) topic and select the most suitable access point for your business region.


* Request method: POST

* Request URL: https://vke.cn\-beijing.byteplusapi.com.cn?Action=ListImageCaches&Version=2022\-05\-12


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters

The following table contains the API request parameters. You also need to provide public parameters when calling this API. See [Public parameters](https://docs.byteplus.com/en/docs/vke/Common-parameters) for details.


|Parameters |Type |Required |Sample value |Description |
|---|---|---|---|---|
|Action |String |Yes |ListImageCaches |The API name. The name of the current API is `ListImageCaches`. |
|Version |String |Yes |2022\-05\-12 |The API version. The current version of the API is `2022-05-12`. |
|Filter |Object of [Filter](https://docs.byteplus.com/en/docs/vke/ListImageCaches#filter) |no |\- |The criteria for querying image caches. |
|PageNumber |Integer |no |1 |The starting page number when querying. The default number is 1. |
|PageSize |Integer |no |10 |The number of results per page:<br><br><br>* Minimum value: 1<br><br>* Maximum value: 100<br><br>* Default value: 10 |


&nbsp;


|Parameters |Type |Required |Sample value |Description |
|---|---|---|---|---|
|Action |String |Yes |ListImageCaches |The API name. The name of the current API is `ListImageCaches`. |
|Version |String |Yes |2022\-05\-12 |The API version. The current version of the API is `2022-05-12`. |
|Filter |Object of [Filter](https://docs.byteplus.com/en/docs/vke/ListImageCaches#filter) |no |\- |The criteria for querying image caches. |
|PageNumber |Integer |no |1 |The starting page number when querying. The default number is 1. |
|PageSize |Integer |no |10 |The number of results per page:<br><br><br>* Minimum value: 1<br><br>* Maximum value: 100<br><br>* Default value: 10 |


<span id="filter"></span>
### Filter


|Parameters |Type |Required |Sample value |Description |
|---|---|---|---|---|
|Images |Array of String |no |["cr\-cn\-beijing.volces.com/vke\*\*\*\*/nginx:latest"] |The list of image addresses. |
|ImageCacheIds |Array of String |no |["imc\-3uqroqkx0i3j\*\*\*\*\*\*\*\*"] |The list of the image cache IDs. You can enter up to 100 IDs at a time. |
|ImageCacheNames |Array of String |no |["image\-cache\-test"] |The list of image cache names. You can enter up to 100 names at a time. |


<span id=".6K-35rGC56S65L6L"></span>
## Sample requests

```json
POST /?Action=ListImageCaches&Version=2022-05-12 HTTP/1.1
Content-Type:application/json
{
    "PageNumber": 1,
    "PageSize": 10,
    "Filter": {
        "ImageCacheNames": ["image-cache-test"],
        "ImageCacheIds": ["imc-3uqroqkx0i3j********"],
        "Images": ["cr-cn-beijing.volces.com/vke****/nginx:latest"]
    }
}
```


<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters

The following table contains the response parameters of this API. See [Response results](https://docs.byteplus.com/en/docs/vke/Response) for details about public response parameters.


|Parameters |Type |Sample value |Description |
|---|---|---|---|
|Items |Array of [Items](https://docs.byteplus.com/en/docs/vke/ListImageCaches#items) |\- |The details of the image cache. |


<span id="items"></span>
### Items


|Parameters |Type |Sample value |Description |
|---|---|---|---|
|ImageCacheId |String |imc\-3v7jly9r\*\*\*\*\*\*\*\* |The ID of the image cache. |
|ImageCacheName |String |auto\-imc\-for\-vci\-3v7j\*\*\*\*\*\* |The image cache name. |
|Images |Array of String |["cr\-cn\-beijing.volces.com/vke\*\*\*\*/nginx:latest"] |The list of container images included in the image cache. |
|ImageCacheSize |Integer |40 |The image cache capacity. Unit: GiB. |
|CreationTime |String |2023\-10\-17T13:14:18Z |The time when the image cache was created.<br><br>UTC+0 time in standard [RFC3339](https://tools.ietf.org/html/rfc3339) format. |
|ExpireDateTime |String |2023\-11\-01T13:14:18Z |The time when the image cache expires.<br><br>UTC+0 time in standard [RFC3339](https://tools.ietf.org/html/rfc3339) format.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">If you do not specify the <strong>RetentionDays </strong>parameter that controls the image cache retention duration (The image cache never expires) when creating an image cache, this parameter will not be returned.</div><br> |
|LastMatchedTime |String |2023\-02\-20T05:26:34Z |The time when the image cache was last matched.<br><br>UTC+0 time in standard [RFC3339](https://tools.ietf.org/html/rfc3339) format. |
|Status |Object of [Status](https://docs.byteplus.com/en/docs/vke/ListImageCaches#status) |\- |The status information of the image cache. |
|Events |Array of [Events](https://docs.byteplus.com/en/docs/vke/ListImageCaches#events) |\- |The event information of the image cache. |
|AutoPrewarmInfos |Array of [AutoPrewarmInfos](https://docs.byteplus.com/en/docs/vke/ListImageCaches#autoprewarminfos) |\- |The warm\-up configurations of the EBS snapshots that correspond to the image cache. |
|UpdateTime |String |2023\-02\-20T05:26:34Z |The time when the image cache was updated.<br><br>UTC+0 time in standard [RFC3339](https://tools.ietf.org/html/rfc3339) format. |


<span id="status"></span>
### Status


|Parameters |Type |Sample value |Description |
|---|---|---|---|
|Phase |String |Ready |The status of the image cache. Valid values:<br><br><br>* **Creating**: The image cache is being created.<br><br>* **Updating**: The image cache is being updated.<br><br>* **Ready**: The image cache has been created.<br><br>* **Failed**: The image cache creation failed.<br><br>* **Deleting**: The image cache is being deleted.<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">When the image cache is in the <strong>Ready</strong> state, you can use it.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">For valid combinations of <strong>Phase</strong> and <strong>Conditions.Type</strong>, see <a href="https://docs.byteplus.com/en/docs/vke/Resource-status-description">Resources status description</a>.</div><br> |
|Conditions |Array of [Conditions](https://docs.byteplus.com/en/docs/vke/ListImageCaches#conditions) |\- |The conditions under which the add\-on enters the primary status.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">For valid combinations of <strong>Phase</strong> and <strong>Conditions.Type</strong>, see <a href="https://docs.byteplus.com/en/docs/vke/Resource-status-description">Resources status description</a>.</div><br> |


<span id="conditions"></span>
### Conditions


|Parameter |Type |Sample value |Description |
|---|---|---|---|
|Type |String |Ok |The conditions under which the image cache enters the primary status. Available status<br><br><br>* **Ok**: The image cache is in a normal status.<br><br>* **Progressing**: The image cache creation is in progress.<br><br>* **CreationFailed**: The image cache creation has failed.<br><br>* **UpdateFailed**: The image cache update has failed.<br><br>* **Balance**: The account is in arrears.<br><br>* **Unknown**: An unknown issue occurred. |


<span id="events"></span>
### Events


|Parameters |Type |Sample value |Description |
|---|---|---|---|
|Type |String |Normal |The event type. Valid values:<br><br><br>* **Normal**: normal event<br><br>* **Warning**: alert event |
|Reason |String |DiskCreated |The event cause. |
|Message |String |The image cache disk has been created successfully |The event details. |
|FirstTimestamp |String |2023\-10\-17T13:14:20Z |The event start time. |
|Name |String |auto\-imc\-for\-vci\-3v7jly7kx95g1ho3mixi.3v7\*\*\*\*\*\* |The event name. |


<span id="autoprewarminfos"></span>
### AutoPrewarmInfos


|Parameters |Type |Sample value |Description |
|---|---|---|---|
|ZoneId |String |cn\-beijing\-b |The ID of the warm\-up availability zone for the EBS snapshot that corresponds to the image cache. |
|PrewarmCreationTime |String |2023\-10\-17T13:14:18Z |The warm\-up start time for the EBS snapshot that corresponds to the image cache.<br><br>UTC+0 time in standard [RFC3339](https://tools.ietf.org/html/rfc3339) format. |
|PrewarmExpireTime |String |2024\-01\-15T14:08:46Z |The warm\-up expiration time for the EBS snapshot that corresponds to the image cache.<br><br>UTC+0 time in standard [RFC3339](https://tools.ietf.org/html/rfc3339) format. |
|PrewarmUpdateTime |String |2023\-10\-10T10:33:30Z |The warm\-up update time for the EBS snapshot that corresponds to the image cache.<br><br>UTC+0 time in standard [RFC3339](https://tools.ietf.org/html/rfc3339) format. |


<span id=".6L-U5Zue56S65L6L"></span>
## Sample responses

```json
{
    "ResponseMetadata": {
        "RequestId": "20231019152631F27********",
        "Action": "ListImageCaches",
        "Version": "2022-05-12",
        "Service": "vke",
        "Region": "cn-guangzhou"
    },
    "Result": {
        "Items": [
            {
                "ImageCacheId": "imc-3v7jly9r********",
                "ImageCacheName": "auto-imc-for-vci-3v7j******",
                "ImageCacheSize": 40,
                "Images": [
                    "vci-demo-gz-cn-guangzhou.cr.volces.com/vci_demo/big-image: 24G"
                ],
                "Status": {
                    "Phase": "Ready",
                    "Conditions": [
                        {
                            "Type": "Ok"
                        }
                    ]
                },
                "Events": [
                    {
                        "Type": "Normal",
                        "Name": "auto-imc-for-vci-3v7jly7kx95g1ho3mixi.3v7******",
                        "Reason": "DiskCreated",
                        "Message": "The image cache disk has been created successfully",
                        "FirstTimestamp": "2023-10-17T13:14:20Z"
                    },
                    {
                        "Type": "Normal",
                        "Name": "auto-imc-for-vci-3v7jly7kx95g1ho3mixi.3v7j******",
                        "Reason": "Pulling",
                        "Message": "Pulling images [vci-demo-gz-cn-guangzhou.cr.volces.com/vci_demo/big-image:24G]",
                        "FirstTimestamp": "2023-10-17T13:14:20Z"
                    },
                    {
                        "Type": "Normal",
                        "Name": "auto-imc-for-vci-3v7jly7kx95g1ho3mixi.3v7j******",
                        "Reason": "Pulled",
                        "Message": "Successfully pulled image [vci-demo-gz-cn-guangzhou.cr.volces.com/vci_demo/big-image:24G]",
                        "FirstTimestamp": "2023-10-17T14:03:56Z"
                    },
                    {
                        "Type": "Normal",
                        "Name": "auto-imc-for-vci-3v7jly7kx95g1ho3mixi.3v7j******",
                        "Reason": "ImageCacheCreated",
                        "Message": "The image cache has been created successfully,total capacity is 40 GiB",
                        "FirstTimestamp": "2023-10-17T14:11:10Z"
                    },
                    {
                        "Type": "Normal",
                        "Name": "auto-imc-for-vci-3v7jly7kx95g1ho3mixi.3v7j******",
                        "Reason": "ImageCacheReady",
                        "Message": "The image cache [vci-demo-gz-cn-guangzhou.cr.volces.com/vci_demo/big-image:24G] has been made successfully",
                        "FirstTimestamp": "2023-10-17T14:11:10Z"
                    }
                ],
                "AutoPrewarmInfos": [
                    {
                        "ZoneId": "cn-guangzhou-a",
                        "PrewarmCreationTime": "2023-10-17T13:14:18Z",
                        "PrewarmExpireTime": "2024-01-15T14:08:46Z"
                    }
                ],
                "CreationTime": "2023-10-17T13:14:18Z",
                "ExpireDateTime": "2023-11-01T13:14:18Z"
            }
        ],
        "PageNumber": 1,
        "PageSize": 100,
        "TotalCount": 1
    }
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error code

There are no proprietary error codes for this API. See [Public error codes](https://docs.byteplus.com/en/docs/vke/Common-error-codes) for details.

&nbsp;
