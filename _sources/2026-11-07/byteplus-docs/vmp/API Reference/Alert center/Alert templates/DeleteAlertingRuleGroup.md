---
title: "DeleteAlertingRuleGroup"
product: "Vital Managed Service for Prometheus"
product_code: "vmp"
source: "https://docs.byteplus.com/en/docs/vmp/DeleteAlertingRuleGroup"
---

Delete an alerting rule group.

## Request description

Vital Managed Service for Prometheus has been deployed in multiple regions worldwide to provide you with a more stable, lower\-latency experience. You can choose an optimal access point for your service region by referring to the [Service addresses](https://docs.byteplus.com/en/docs/vmp/Service_address) topic.

* Request method: POST

* Request URL: https://vmp.cn\-beijing.byteplusapi.com.cn?Action=DeleteAlertingRuleGroup&Version=2021\-03\-03

## Debugging

[去调试](https://api.byteplus.com/api-explorer/debug?action=DeleteAlertingRuleGroup&serviceCode=vmp&version=2021-03-03&groupName=)

## Request parameters

|**Parameters** |**Type** |**Required** |**Sample value** |**Description** |
|---|---|---|---|---|
|Action |String |Yes |DeleteAlertingRuleGroup |The API name. The API name is `DeleteAlertingRuleGroup`. |
|Version |String |Yes |2021\-03\-03 |The API version. The API version is `2021-03-03`. |
|Id |String |Yes |e28a\-\*\*\*\*\-abf4\*\*\*\* |ID of alerting rule group. |

## Sample request

```JSON
POST https://vmp.cn-beijing.byteplusapi.com.cn?Action=DeleteAlertingRuleGroup&Version=2021-03-03
Content-Type: application/json
{
    "Id": "e28a-****-abf4****"
}
```

## Response parameters

|**Parameters** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|Id |String |e28a\-\*\*\*\*\-abf4\*\*\*\* |ID of alerting rule group. |

## Sample response

```JSON
HTTP/1.1: 200 OK
Content-Type: application/json
{
    "ResponseMetadata": {
        "RequestId": "20230604110420****100232280022D31",
        "Action": "DeleteAlertingRuleGroup",
        "Version": "2021-03-03",
        "Service": "vmp",
        "Region": "cn-beijing"
    },
    "Result": {
        "Id": "e28a-****-abf4****"
    }
}
```

## Error codes

The error codes for this API are listed in the table below. For a list of error codes for other APIs, see [Public error codes](https://docs.byteplus.com/en/docs/vmp/Common-error-codes).

|**HTTP status codes** |**Error codes** |**Error messages** |**Description** |
|---|---|---|---|
|403 |ProductUnsubscribed |You are not subscribed to VMP. Please go to the VMP console web page to subscribe to the service |The current account is not subscribed to the VMP service. |
|400 |InvalidParameter.{{parameter}} |The specified parameter {{parameter}} is invalid. |The input is invalid. For example, the workspace name does not meet the requirements. |
|400 |MissingParameter.{{parameter}} |The required parameter {{parameter}} is missing. |A required parameter is missing. |
