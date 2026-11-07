---
title: "DeleteSandboxImage"
product: "Function Service"
product_code: "faas"
source: "https://docs.byteplus.com/en/docs/faas/DeleteSandboxImage"
---

Delete the preheated image.

<span id=".6K-35rGC6K-05piO"></span>
## Request description


* Request method: POST

* Request URL: http://vefaas.ap\-southeast\-1.byteplusapi.com/?Action=DeleteSandboxImage&Version=2024\-06\-06


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters


|**ParameterParameter** |**TypeType** |**RequiredRequired** |**Sample valueSample value** |**DescriptionDescription** |
|---|---|---|---|---|
|Action |String |Yes |DeleteSandboxImage |Interface name. The name of the current API is `DeleteSandboxImage`. |
|Version |String |Yes |2024\-06\-06 |Interface version. The current version of the API is `2024-06-06 `. |
|ImageIdImageId |StringString |YesYes |9px3\*\*\*\*\*\*9px3\*\*\*\*\*\* |Sandbox image ID.Sandbox image ID. |


<span id=".6K-35rGC56S65L6L"></span>
## Sample requests

```JSON
POST http://vefaas.ap-southeast-1.byteplusapi.com/?Action=DeleteSandboxImage&Version=2024-06-06 HTTP/1.1
Content-Type: application/json
{
    "ImageId": "9px3******"
}
```


<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters


|**Parameter** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|Status |String |success |Result of delete action:<br><br><br>* **success**: deleted successfully<br><br>* **failed**: failed to delete |
|RelatedSandboxApplications |Array of String |["wxd2\*\*\*\*"] |A list of associated sandbox application IDs. |


<span id=".6L-U5Zue56S65L6L"></span>
## Sample responses

```JSON
HTTP/1.1 200 OK
Content-Type: application/json
{
    "ResponseMetadata": {
        "RequestId": "20230604110420****100232280022D31",
        "Action": "DeleteSandboxImage",
        "Version": "2024-06-06",
        "Service": "vefaas",
        "Region": "ap-southeast-1"
    },
    "Result": {
        "Status": "success",
        "RelatedSandboxApplications": [
            "wxd2****"
        ]
    }
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error codes

There is no error code dedicated to this interface currently. If you encounter an exception when calling the interface, you can refer to [Public error codes](https://docs.byteplus.com/en/docs/faas/Public_error_code) for troubleshooting.
