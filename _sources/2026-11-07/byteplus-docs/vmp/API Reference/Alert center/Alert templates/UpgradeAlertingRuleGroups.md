---
title: "UpgradeAlertingRuleGroups"
product: "Vital Managed Service for Prometheus"
product_code: "vmp"
source: "https://docs.byteplus.com/en/docs/vmp/UpgradeAlertingRuleGroups"
---

Upgrades alert rule groups.

## Request description

* Request method: POST

* Request URL: https://vmp.cn\-beijing.byteplusapi.com.cn?Action=UpgradeAlertingRuleGroups&Version=2021\-03\-03

## Debugging

[去调试](https://api.byteplus.com/api-explorer/debug?action=UpgradeAlertingRuleGroups&serviceCode=vmp&version=2021-03-03&groupName=)

## Request parameters

|**Parameters** |**Type** |**Required** |**Sample value** |**Description** |
|---|---|---|---|---|
|Action |String |Yes |UpgradeAlertingRuleGroups |The name of the API action. The API name is `UpgradeAlertingRuleGroups`. |
|Version |String |Yes |2021\-03\-03 |The API version. The API version is `2021-03-03`. |
|Filter |Object of [UpgradeAlertingRuleGroupFilter](https://docs.byteplus.com/en/docs/88/123599#upgradealertingrulegroupfilter) |No |\- |The filter criteria for rule groups. |

### UpgradeAlertingRuleGroupFilter

|**Parameters** |**Type** |**Required** |**Sample value** |**Description** |
|---|---|---|---|---|
|Ids |Array of String |No |["e28a\-\*\*\*\*\-1e0e\*\*\*\*"] |Exact query by the IDs of alerting rule groups. |

## Sample request

```JSON
POST https://vmp.cn-beijing.byteplusapi.com.cn?Action=UpgradeAlertingRuleGroups&Version=2021-03-03
Content-Type: application/json
{
    "Filter": {
        "Ids": [
            "e28a-****-1e0e****"
        ]
    }
}
```

## Response parameters

|**Parameters** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|SuccessfulItems |Array of String |["e28a\-\*\*\*\*\-1e0e\*\*\*\*"] |The list of IDs on which operations succeeded. |
|UnsuccessfulItems |Array of [UnsuccessfulItem](https://docs.byteplus.com/en/docs/88/123599#unsuccessfulitem) |e28\-\*\*\*\*\-abf4\*\*\* |The list of failed operations. |

### UnsuccessfulItem

|**Parameters** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|Id |String |e28\-\*\*\*\*\-abf4\*\*\* |The ID of the object on which the operation failed. |
|Error |Object of [UnsuccessfulItemError](https://docs.byteplus.com/en/docs/88/123599#unsuccessfulitemerror) |\- |Reason for failed actions. |

### UnsuccessfulItemError

|**Parameters** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|Code |String |NotFound.Ids |Error code. For details, see **Error codes** or [Common error codes](https://docs.byteplus.com/en/docs/vmp/Common-error-codes). |
|Message |String |The specified Contact abc was not found. |Error message. For details, see **Error codes** or [Common error codes](https://docs.byteplus.com/en/docs/vmp/Common-error-codes). |
|Data |JSON Map |\- |Error metadata. |

## Sample response

```JSON
HTTP/1.1: 200 OK
Content-Type: application/json
{
    "ResponseMetadata": {
        "RequestId": "20230604110420****100232280022D31",
        "Action": "UpgradeAlertingRuleGroups",
        "Version": "2021-03-03",
        "Service": "vmp",
        "Region": "cn-beijing"
    },
    "Result": {
        "SuccessfulItems": [
            "e28a-****-1e0e****"
        ],
        "UnsuccessfulItems": [
            {
                "Id": "e28-****-abf4***",
                "Error": {
                    "Code": "NotFound.Ids",
                    "Message": "The specified Contact abc is not found."
                }
            }
        ]
    }
}
```

## Error codes

The error codes for this API are listed in the table below. For a list of error codes for other APIs, see [Public error codes](https://docs.byteplus.com/en/docs/vmp/Common-error-codes).

|**HTTP status codes** |**Error codes** |**Error messages** |**Description** |
|---|---|---|---|
|403 |ProductUnsubscribed |You are not subscribed to VMP. Please go to the VMP console web page to subscribe to the service |The current account is not subscribed to the VMP service. |
|400 |InvalidParameter.{{parameter}} |The specified parameter {{parameter}} is invalid. |The input is invalid. For example, the workspace name does not meet the requirements. |
