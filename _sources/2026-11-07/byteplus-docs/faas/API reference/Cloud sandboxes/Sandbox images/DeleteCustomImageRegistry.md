---
title: "DeleteCustomImageRegistry"
product: "Function Service"
product_code: "faas"
source: "https://docs.byteplus.com/en/docs/faas/DeleteCustomImageRegistry"
---

Delete custom CR.

## Request description

* Request method: POST

* Request URL: http://vefaas.ap\-southeast\-1.byteplusapi.com/?Action=DeleteCustomImageRegistry&Version=2024\-06\-06

## Request parameters

|**Parameter** |**Type** |**Require** |**Sample value** |**Description** |
|---|---|---|---|---|
|Action |String |Yes |DeleteCustomImageRegistry |Interface name. The current API name is `DeleteCustomImageRegistry`. |
|Version |String |Yes |2024\-06\-06 |Interface version. The current version of the API is `2024-06-06 `. |
|RegistryId |String |Yes |regcfg\-2fvj\*\*\*\* |ID of the custom CR. |

## Sample requests

```JSON
POST http://vefaas.ap-southeast-1.byteplusapi.com/?Action=DeleteCustomImageRegistry&Version=2024-06-06 HTTP/1.1
Content-Type: application/json
{
    "RegistryId": "regcfg-2fvj****"
}
```

## Response parameters

|**Parameter** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|Status |String |success |The status of the delete operation. Available values are as follows.<br><br><br>* success: deleted successfully<br><br>* failed: failed to delete |
|Message |String |Deletion successful |Detailed description of the operation result or error. |

## Sample responses

```JSON
HTTP/1.1 200 OK
Content-Type: application/json
{
    "ResponseMetadata": {
        "RequestId": "20230604110420****100232280022D31",
        "Action": "DeleteCustomImageRegistry",
        "Version": "2024-06-06",
        "Service": "vefaas",
        "Region": "ap-southeast-1"
    },
    "Result": {
        "Status": "success",
        "Message": "Deletion successful"
    }
}
```

## Error codes

The current interface temporarily has no independent error code. If the interface calls back abnormally, you can refer to the [Public error code](https://docs.byteplus.com/en/docs/faas/Public_error_code) to troubleshoot.
