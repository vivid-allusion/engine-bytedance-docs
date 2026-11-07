---
title: "UpdateImageCacheRetentionDays"
product: " Vital Kubernetes Engine"
product_code: "vke"
source: "https://docs.byteplus.com/en/docs/vke/UpdateImageCacheRetentionDays"
---

Update the expiration time of multiple image caches at the same time.

<span id=".6K-35rGC6K-05piO"></span>
## Request description

VKE has deployed services in multiple regions globally to provide a stable and low\-latency access experience. You can refer to the [Service addresses](https://docs.byteplus.com/en/docs/vke/Service_addresses) topic and select the most suitable access point for your business region.


* Request method: POST

* Request URL: https://vke.cn\-beijing.byteplusapi.com.cn?Action=UpdateImageCacheRetentionDays&Version=2022\-05\-12


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters

The following table contains the request parameters for the API. You also need to provide public parameters when calling this API. See [Public parameters](https://docs.byteplus.com/en/docs/vke/Common-parameters) for details.


|Parameter |Type |Required |Sample value |Description |
|---|---|---|---|---|
|Action |String |Yes |UpdateImageCacheRetentionDays |The API name. The name of the current API is `UpdateImageCacheRetentionDays`. |
|Version |String |Yes |2022\-05\-12 |The API version. The current version of the API is `2022-05-12`. |
|Retentiondays |Integer |Yes |15 |Update the retention duration of filtered image caches to the specified number of days.<br><br><br>* Valid values: 1 to 365. The value must be a positive integer.<br><br>* Unit: days. |
|Filter |Object of [Filter](https://docs.byteplus.com/en/docs/vke/UpdateImageCacheRetentionDays#filter) |Yes |\- |The criteria for filtering image caches to be updated. |


<span id="filter"></span>
### Filter


|Parameters |Type |Required |Sample value |Description |
|---|---|---|---|---|
|Images |Array of String |no |["cr\-cn\-beijing.volces.com/vke\*\*\*\*/nginx:latest"] |The list of container images that correspond to the image caches. |
|ImageCacheIds |Array of String |no |["imc\-3uqroqkx0i3j\*\*\*\*\*\*\*\*"] |The list of image cache IDs. You can enter up to 100 IDs at a time. |
|ImageCacheNames |Array of String |no |["image\-cache\-test"] |The list of image cache names. You can enter up to 100 names at a time. |


<span id=".6K-35rGC56S65L6L"></span>
## Sample requests

```json
POST /?Action=UpdateImageCacheRetentionDays&Version=2022-05-12 HTTP/1.1
Content-Type: application/json
{
    "Retentiondays": 15,
    "Filter": {
        "ImageCacheIds": [
            "imc-3uqroqkx0i3j********"
        ],
        "Images": [
            "cr-cn-beijing.volces.com/vke****/nginx:latest"
        ],
        "ImageCacheNames": [
            "image-cache-test"
        ]
    }
}
```


<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters

The following table contains the response parameters of this API. See [Response results](https://docs.byteplus.com/en/docs/vke/Response) for details about public response parameters.


|Parameters |Type |Sample value |Description |
|---|---|---|---|
|TotalAmount |Integer |50 |The total number of image caches involved in the batch update (including those updated and those that failed to be updated). |
|UpdatedImageCacheIds |Array of String |["imc\-3uqroqkx0i3j\*\*\*\*\*\*\*\*"] |The IDs of image caches for which the expiration time was updated. |
|FailedItems |Array of [FailedItems](https://docs.byteplus.com/en/docs/vke/UpdateImageCacheRetentionDays#faileditems) | |The list of image caches for which the expiration time failed to be updated, and the failure causes. |


<span id="faileditems"></span>
### FailedItems


|Parameter |Type |Sample value |Description |
|---|---|---|---|
|ImageCacheId |String |imc\-3uqroqkx\*\*\*\*\*\*\*\* |The IDs of image caches for which the expiration time failed to be updated. |
|FailedReason |String |ImageCache status {Phase} is not allowed for updating retentiondays. |The reason for the failure to update the expiration time of the image cache. |


<span id=".6L-U5Zue56S65L6L"></span>
## Sample responses

```json
{
    "ResponseMetadata": {
        "RequestId": "20230604110420********",
        "Action": "UpdateImageCacheRetentionDays",
        "Version": "2022-05-12",
        "Service": "vke",
        "Region": "cn-beijing"
    },
    "Result": {
        "TotalAmount": 50,
        "UpdatedImageCacheIds": [
            "imc-3uqroqkx0i3j********"
        ],
        "FailedItems": [
            {
                "ImageCacheId": "imc-3uqroqkx********",
                "FailedReason": "ImageCache status {Phase} is not allowed for updating retentiondays."
            }
        ]
    }
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error code

There are no error codes proprietary to this API. See [Public error codes](https://docs.byteplus.com/en/docs/vke/Common-error-codes) for details.

&nbsp;
