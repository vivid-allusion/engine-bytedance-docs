---
title: "PrecacheSandboxImages"
product: "Function Service"
product_code: "faas"
source: "https://docs.byteplus.com/en/docs/faas/PrecacheSandboxImages"
---

Preheat custom images in batch.

## Request description

* Request method: POST

* Request URL: http://vefaas.ap\-southeast\-1.byteplusapi.com/?Action=PrecacheSandboxImages&Version=2024\-06\-06

## Request parameters

|**Parameter** |**Type** |**Require** |**Sample value** |**Description** |
|---|---|---|---|---|
|Action |String |Yes |PrecacheSandboxImages |Interface name. The name of the current API is `PrecacheSandboxImages`. |
|Version |String |Yes |2024\-06\-06 |Interface version. The current version of the API is `2024-06-06 `. |
|ImageUrls |Array of String |Yes |["vefaas\-\*\*\*\*\*\*.cr.volces.com/vefaas\-cr/\*\*\*\*\*\*:latest"] |A list of Sandbox custom image addresses to be preheated.<br><br><br>* BytePlus Container Registry (CR): After uploading an image to the CR, obtain the image address from the image details on the **OCI artifact repository** page of [CR console](https://console.byteplus.com/cr).<br><br>* Third\-party registry: The complete address of the image to be warmed up. It is composed of the domain name, namespace, image name, and version of the target image registry. The format is `{registry domain}/{namespace}/{image name}:{version}`. |
|RegistryId |String |No |regcfg\-2fvj\*\*\*\* |ID of the custom CR. Fill this in only when warming up images from a third\-party custom registry. You can obtain the ID of the custom registry via [ListCustomImageRegistries](https://docs.byteplus.com/en/docs/6662/2600008?lang=en).<br><br>If left empty, warm\-up is supported only when ImageUrls are BytePlus CR addresses. |

## Sample requests

```JSON
POST http://vefaas.ap-southeast-1.byteplusapi.com/?Action=PrecacheSandboxImages&Version=2024-06-06 HTTP/1.1
Content-Type: application/json
{
    "ImageUrls": [
        "vefaas-******.cr.volces.com/vefaas-cr/******:latest"
    ]
}
```

## Response parameters

|**Parameter** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|TicketId |String |948410ee80954\*\*\*\*\*\* |Preheating ticket ID.<br><br>You can keep the preheating ticket ID locally and use it later to query the details of that ticket. |

## Sample responses

```JSON
HTTP/1.1 200 OK
Content-Type: application/json
{
    "ResponseMetadata": {
        "RequestId": "20230604110420****100232280022D31",
        "Action": "PrecacheSandboxImages",
        "Version": "2024-06-06",
        "Service": "vefaas",
        "Region": "ap-southeast-1"
    },
    "Result": {
        "TicketId": "948410ee80954******"
    }
}
```

## Error codes

The current interface temporarily has no independent error code. If the interface calls back abnormally, you can refer to the [Public error code](https://docs.byteplus.com/en/docs/faas/Public_error_code) to troubleshoot.
