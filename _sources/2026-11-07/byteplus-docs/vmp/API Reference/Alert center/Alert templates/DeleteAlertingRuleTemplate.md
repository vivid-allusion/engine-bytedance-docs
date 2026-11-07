---
title: "DeleteAlertingRuleTemplate"
product: "Vital Managed Service for Prometheus"
product_code: "vmp"
source: "https://docs.byteplus.com/en/docs/vmp/DeleteAlertingRuleTemplate"
---

Deletes an alert template.

## Request description

* Request method: POST

* Request URL: https://vmp.cn\-beijing.byteplusapi.com.cn?Action=DeleteAlertingRuleTemplate&Version=2021\-03\-03

## Debugging

[去调试](https://api.byteplus.com/api-explorer/debug?action=DeleteAlertingRuleTemplate&serviceCode=vmp&version=2021-03-03&groupName=)

## Request parameters

|**Parameters** |**Type** |**Required** |**Sample value** |**Description** |
|---|---|---|---|---|
|Action |String |Yes |DeleteAlertingRuleTemplate |The API name. The API name is `DeleteAlertingRuleTemplate`. |
|Version |String |Yes |2021\-03\-03 |The API version. The API version is `2021-03-03`. |
|Id |String |Yes |e28a\-\*\*\*\*\-8808\*\*\*\* |Alert template ID. |

## Sample request

```JSON
POST https://vmp.cn-beijing.byteplusapi.com.cn?Action=DeleteAlertingRuleTemplate&Version=2021-03-03
Content-Type: application/json
{
    "Id": "e28a-****-8808****"
}
```

## Response parameters

|**Parameters** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|Id |String |e28a\-\*\*\*\*\-8808\*\*\*\* |Alert template ID. |

## Sample response

```JSON
HTTP/1.1: 200 OK
Content-Type: application/json
{
    "ResponseMetadata": {
        "RequestId": "20230604110420****100232280022D31",
        "Action": "DeleteAlertingRuleTemplate",
        "Version": "2021-03-03",
        "Service": "vmp",
        "Region": "cn-beijing"
    },
    "Result": {
        "Id": "e28a-****-8808****"
    }
}
```

## Error codes

The error codes for this API are listed in the table below. For a list of error codes for other APIs, see [Public error codes](https://docs.byteplus.com/en/docs/vmp/Common-error-codes).

|**HTTP status codes** |**Error codes** |**Error messages** |**Description** |
|---|---|---|---|
|403 |ProductUnsubscribed |You are not subscribed to VMP. Please go to the VMP console web page to subscribe to the service |The current account is not subscribed to the VMP service. |
|400 |MissingParameter.{{parameter}} |The required parameter {{parameter}} is missing. |A required parameter is missing. |
