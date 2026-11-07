---
title: "GetSandboxImagePrecacheTicket"
product: "Function Service"
product_code: "faas"
source: "https://docs.byteplus.com/en/docs/faas/GetSandboxImagePrecacheTicket"
---

Obtain the details of image preheating tickets.

<span id=".6K-35rGC6K-05piO"></span>
## Request description


* Request method: POST

* Request URL: http://vefaas.ap\-southeast\-1.byteplusapi.com/?Action=GetSandboxImagePrecacheTicket&Version=2024\-06\-06


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters


|**parameter** |**Type** |**Required** |**sample value** |**Description** |
|---|---|---|---|---|
|Action |String |Yes |GetSandboxImagePrecacheTicket |Interface name. The name of the current API is `GetSandboxImagePrecacheTicket`. |
|Version |String |Yes |2024\-06\-06 |Interface version. The current version of the API is `2024-06-06 `. |
|TicketId |String |No |948410ee80954\*\*\*\*\*\* |Preheating ticket ID.<br><br><br>* If you keep the preheating ticket IDs when performing image preheating in batch, you use a specific ID to obtain detailed information.<br><br>* If no ID is specified, all preheating ticket information under the current account will be returned. |


<span id=".6K-35rGC56S65L6L"></span>
## Sample requests

```JSON
POST http://vefaas.ap-southeast-1.byteplusapi.com/?Action=GetSandboxImagePrecacheTicket&Version=2024-06-06 HTTP/1.1
Content-Type: application/json
{
    "TicketId": "948410ee80954******"
}
```


<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters


|**parameter** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|TicketId |String |948410ee80954\*\*\*\*\*\* |Preheating ticket ID. |
|Status |String |success |The status of preheating tickets:<br><br><br>* **pending**: awaiting processing<br><br>* **running**: preheating in progress<br><br>* **success**: Preheated<br><br>* **failed**: Preheating failed |
|Progress |JSON Map |{"9px3\*\*\*\*\*\*": "success"} |The progress of preheating tickets. Presented with the format`{"key": "value"}`, where the `key` is the sandbox image ID and the `value` is the preheating status. |
|Duration |Long |100 |Preheating ticket handling time measured in seconds. |


<span id=".6L-U5Zue56S65L6L"></span>
## Sample responses

```JSON
HTTP/1.1 200 OK
Content-Type: application/json
{
    "ResponseMetadata": {
        "RequestId": "20230604110420****100232280022D31",
        "Action": "GetSandboxImagePrecacheTicket",
        "Version": "2024-06-06",
        "Service": "vefaas",
        "Region": "ap-southeast-1"
    },
    "Result": {
        "TicketId": "948410ee80954******",
        "Status": "success",
        "Progress": {
            "9px3******": "success"
        },
        "Duration": 100
    }
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error codes

There is no error code dedicated to this interface currently. If you encounter an exception when calling the interface, you can refer to [Public error codes](https://docs.byteplus.com/en/docs/faas/Public_error_code) for troubleshooting.
