---
title: "ListSandboxImages"
product: "Function Service"
product_code: "faas"
source: "https://docs.byteplus.com/en/docs/faas/ListSandboxImages"
---

Obtain information of preheated images in batch.

<span id=".6K-35rGC6K-05piO"></span>
## Request description


* Request method: POST

* Request URL: http://vefaas.ap\-southeast\-1.byteplusapi.com/?Action=ListSandboxImages&Version=2024\-06\-06


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters


|**Parameter** |**Type** |**Required** |**Sample value** |**Description** |
|---|---|---|---|---|
|Action |String |Yes |ListSandboxImages |Interface name. The name of the current API is `ListSandboxImages`. |
|Version |String |Yes |2024\-06\-06 |Interface version. The current version of the API is `2024-06-06 `. |
|ImageType |String |Yes |private |Image types:<br><br><br>* **private**: custom images<br><br>* **public**: public images |
|Filters |Array of [SandboxImageFilter](https://docs.byteplus.com/en/docs/192/69677#sandboximagefilter) |No |\- |Filter condition used to query preheated images. |
|PageNumber |Integer |No |1 |The starting page number for paginated queries. The default value is 1. |
|PageSize |Integer |No |10 |Number of results displayed per page for paginated queries:<br><br><br>* Minimum value: 1<br><br>* Default value: 10 |


<span id="sandboximagefilter"></span>
### SandboxImageFilter


|**Parameter** |**Type** |**Required** |**Sample value** |**Description** |
|---|---|---|---|---|
|Key |String |No |id |The key of a filter condition:<br><br><br>* **id**: Sandbox image ID.<br><br>* **source_image_url**: Sandbox image address.<br><br>* **precache_status**: The preheating status of sandbox images.<br><br>* **image_group**: Sandbox image category. |
|Values |Array of String |No |["9px3\*\*\*\*\*\*"] |The value of a filter condition. It includes sandbox image ID, image address, preheating status, and image type. You can obtain the information by calling the [GetSandboxImagePrecacheTicket](https://docs.byteplus.com/en/docs/6662/1824713) API. |


<span id=".6K-35rGC56S65L6L"></span>
## Sample requests

```JSON
POST http://vefaas.ap-southeast-1.byteplusapi.com/?Action=ListSandboxImages&Version=2024-06-06 HTTP/1.1
Content-Type: application/json
{
    "ImageType": "private",
    "Filters": [
        {
            "Key": "id",
            "Values": [
                "9px3******"
            ]
        }
    ],
    "PageNumber": 1,
    "PageSize": 10
}
```


<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters


|**Parameter** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|Images |Array of [SandboxImage](https://docs.byteplus.com/en/docs/192/69677#sandboximage) |\- |Image list. |
|TotalCount |Integer |100 |Total number of images. |


<span id="sandboximage"></span>
### SandboxImage


|**Parameter** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|ImageId |String |9px3r68nu9 |Sandbox image ID. |
|ImageUrl |String |vefaas\-\*\*\*\*.cr.volces.com/vefaas\-cr/\*\*\*\*:latest |The sandbox image address. |
|ImageGroup |String |Code |Categories of sandbox images:<br><br><br>* **Code**: Code runtime environment image.<br><br>* **Browser**: Browser runtime environment image.<br><br>* **All\-in\-one**: A highly integrated, multifunctional image for cloud\-based development and execution environments.<br><br>* **SWE**: [[beta · apply for trial](https://docs.byteplus.com/en/docs/faas/How_do_I_apply_for_beta_features)] SWE\-bench image series. |
|UpdateTime |String |2025\-04\-25 11:11:29.376 +0000 UTC |The latest update time of sandbox images. |
|PrecacheStatus |String |success |Preheating status of sandbox images:<br><br><br>* **success**: preheated<br><br>* **failed**: failed to preheat<br><br>* **caching**: preheating in progress |
|PrecacheStatusReason |String |\- |The reason for the sandbox image preheating failure. |
|RelatedSandboxApplications |Array of String |["wxd2\*\*\*\*"] |The list of sandbox application IDs associated with the sandbox image. |


<span id=".6L-U5Zue56S65L6L"></span>
## Sample responses

```JSON
HTTP/1.1 200 OK
Content-Type: application/json
{
    "ResponseMetadata": {
        "RequestId": "20230604110420****100232280022D31",
        "Action": "ListSandboxImages",
        "Version": "2024-06-06",
        "Service": "vefaas",
        "Region": "ap-southeast-1"
    },
    "Result": {
        "Images": [
            {
                "ImageId": "9px3r68nu9",
                "ImageUrl": "vefaas-****.cr.volces.com/vefaas-cr/****:latest",
                "ImageGroup": "Code",
                "UpdateTime": "2025-04-25 11:11:29.376 +0000 UTC",
                "PrecacheStatus": "success",
                "PrecacheStatusReason": "",
                "RelatedSandboxApplications": [
                    "wxd2****"
                ]
            }
        ],
        "TotalCount": 100
    }
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error codes

There is no error code dedicated to this interface currently. If you encounter an exception when calling the interface, you can refer to [Public error codes](https://docs.byteplus.com/en/docs/faas/Public_error_code) for troubleshooting.
