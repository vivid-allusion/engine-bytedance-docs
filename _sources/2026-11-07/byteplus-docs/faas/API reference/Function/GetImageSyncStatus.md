---
title: "GetImageSyncStatus"
product: "Function Service"
product_code: "faas"
source: "https://docs.byteplus.com/en/docs/faas/GetImageSyncStatus"
---

View function image status, including image synchronization status and image cache creation status.

<span id=".6K-35rGC6K-05piO"></span>
## Request description


* Request method: POST

* Request address: http://vefaas.ap\-southeast\-1.byteplusapi.com/?Action=GetImageSyncStatus&Version=2024\-06\-06


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters


|**Parameter** |**Type** |**Require** |**Sample value** |**Description** |
|---|---|---|---|---|
|Action |String |Yes |GetImageSyncStatus |Interface name. The name of the current API is `GetImageSyncStatus`. |
|Version |String |Yes |2024\-06\-06 |Interface version. The current version of the API is `2024-06-06 `. |
|FunctionId |String |Yes |hl7s\*\*\*\* |Function ID. |
|Source |String |Yes |cr\-vefaas\-ap\-southeast\-1.cr.volces.com/\*\*\*\*/test/tz109:latest |Image address of the function to be queried. |


<span id=".6K-35rGC56S65L6L"></span>
## Sample requests

```JSON
POST http://vefaas.ap-southeast-1.byteplusapi.com/?Action=GetImageSyncStatus&Version=2024-06-06 HTTP/1.1
Content-Type: application/json
{
    "FunctionId": "hl7s****",
    "Source": "cr-vefaas-ap-southeast-1.cr.volces.com/****/test/tz109:latest"
}
```


<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters


|**Parameter** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|Status |String |Succeeded |The execution status of the image synchronization task can take the following values.<br><br><br>* `Pending`: Waiting.<br><br>* `Running`: Synchronizing.<br><br>* `Succeeded`: Synchronization successful.<br><br>* `Canceled`: Canceled.<br><br>* `Failed`: Synchronization failed. |
|Description |String |Succeeded |Description of the image synchronization task |
|StartTime |String |2024\-09\-11T14:02:12+08:00 |Image synchronization task start time. |
|EndTime |String |2024\-09\-11T14:02:19+08:00 |Image synchronization task end time. |
|ImageCacheEnabled |Boolean |true |Is the image cache switch enabled? |
|ImageCacheStatus |String |Ready |Possible values for the image cache status are as follows.<br><br><br>* `Creating`: Cache creation in progress.<br><br>* `Ready`: Cache has been created.<br><br>* `Failed`: Failed to create cache. |
|ImageCacheDescription |String |ImageCache imc\-3vvkvvvl2j520drd\*\*\*\* Ready |Image cache status descriptions. |
|ImageCacheExpireDateTime |String |2024\-09\-29T12:37:32+08:00 |Image cache expiration time. |
|ImagePreloadEnabled |Boolean |true |Whether the function Duma instance image preloading switch is enabled. |
|ImagePreloadStatus |String |Ready |The possible values for the function Duma instance image preload status are as follows.<br><br><br>* `Creating`: Preloading in progress.<br><br>* `Ready`: Preloading completed.<br><br>* `Failed`: Preloading failed. |


<span id=".6L-U5Zue56S65L6L"></span>
## Sample responses

```JSON
HTTP/1.1 200 OK
Content-Type: application/json
{
    "ResponseMetadata": {
        "RequestId": "20230604110420****100232280022D31",
        "Action": "GetImageSyncStatus",
        "Version": "2024-06-06",
        "Service": "vefaas",
        "Region": "ap-southeast-1"
    },
    "Result": {
        "Status": "Succeeded",
        "Description": "Succeeded",
        "StartTime": "2024-09-11T14:02:12+08:00",
        "EndTime": "2024-09-11T14:02:19+08:00",
        "ImageCacheEnabled": true,
        "ImageCacheStatus": "Ready",
        "ImageCacheDescription": "ImageCache imc-3vvkvvvl2j520drd**** Ready",
        "ImageCacheExpireDateTime": "2024-09-29T12:37:32+08:00",
        "ImagePreloadEnabled": true,
        "ImagePreloadStatus": "Ready"
    }
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error codes

There is no error code dedicated to this interface currently. If you encounter an exception when calling the interface, you can refer to [Public error codes](https://docs.byteplus.com/en/docs/faas/Public_error_code) for troubleshooting.
