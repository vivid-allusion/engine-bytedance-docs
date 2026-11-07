---
title: "DeleteImageCache"
product: " Vital Kubernetes Engine"
product_code: "vke"
source: "https://docs.byteplus.com/en/docs/vke/DeleteImageCache"
---

Delete a specified image cache.

<span id=".6K-35rGC6K-05piO"></span>
## Request description

VKE has deployed services in multiple regions globally to provide a stable and low\-latency access experience. You can refer to the [Service addresses](https://docs.byteplus.com/en/docs/vke/Service_addresses) topic and select the most suitable access point for your business region.


* Request method: POST

* Request URL: https://vke.cn\-beijing.byteplusapi.com.cn?Action=DeleteImageCache&Version=2022\-05\-12


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters

The following table lists the API request parameters. You must also provide public parameters when calling this API. For details, see [Public parameters](https://docs.byteplus.com/en/docs/vke/Common-parameters).


|Parameters |Type |Required |Sample value |Description |
|---|---|---|---|---|
|Action |String |Yes |DeleteImageCache |The API name. The name of the current API is `DeleteImageCache`. |
|Version |String |Yes |2022\-05\-12 |The API version. The current version of the API is `2022-05-12`. |
|ImageCacheId |String |Yes |imc\-3uqroqkx\*\*\*\*\*\*\*\* |The ID of the image cache to be deleted.<br><br>You can call the [ListImageCaches](https://docs.byteplus.com/en/docs/vke/ListImageCaches) API to obtain the ID of the image cache.<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">Warning</div><br><br><br><div data-tips="true" data-tips-type="warning">The image cache must be in the <strong>Ready</strong> or <strong>Failed</strong> state. You can call the <a href="https://docs.byteplus.com/en/docs/vke/ListImageCaches">ListImageCaches</a> API to obtain the current status of the image cache.</div><br> |


&nbsp;


|Parameters |Type |Required |Sample value |Description |
|---|---|---|---|---|
|Action |String |Yes |DeleteImageCache |The API name. The name of the current API is `DeleteImageCache`. |
|Version |String |Yes |2022\-05\-12 |The API version. The current version of the API is `2022-05-12`. |
|ImageCacheId |String |Yes |imc\-3uqroqkx\*\*\*\*\*\*\*\* |The ID of the image cache to be deleted.<br><br>You can call the [ListImageCaches](https://docs.byteplus.com/en/docs/vke/ListImageCaches) API to obtain the ID of the image cache.<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">Warning</div><br><br><br><div data-tips="true" data-tips-type="warning">The image cache must be in the <strong>Ready</strong> or <strong>Failed</strong> state. You can call the <a href="https://docs.byteplus.com/en/docs/vke/ListImageCaches">ListImageCaches</a> API to obtain the current status of the image cache.</div><br> |


<span id=".6K-35rGC56S65L6L"></span>
## Sample requests

```json
POST /?Action=DeleteImageCache&Version=2022-05-12 HTTP/1.1
Content-Type:application/json
{
    "ImageCacheId": "imc-3uqroqkx********"
}
```


<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters

There are no proprietary response parameters for this API. See [Response results](https://docs.byteplus.com/en/docs/vke/Response) for details about public response parameters.

<span id=".6L-U5Zue56S65L6L"></span>
## Sample responses

```json
{
    "ResponseMetadata": {
        "RequestId": "2023022020005173B********",
        "Action": "DeleteImageCache",
        "Version": "2022-05-12",
        "Service": "vke",
        "Region": "cr-cn-beijing"
    },
    "Result": {}

}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error code

The error codes for this API are listed in the table below. Refer to the [Public error codes](https://docs.byteplus.com/en/docs/vke/Common-error-codes) topic.


|HTTP status code |Error code |Error message |Description |
|---|---|---|---|
|400 |OperationDenied.Stauts |The action has been forbidden due to wrong status %Status.State and [%Status.StateConditions,...]. |The current status of the specified image cache does not support this operation. Please confirm the required image cache status for this API and try again later. |


&nbsp;
