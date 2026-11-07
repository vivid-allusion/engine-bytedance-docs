---
title: "DeleteRule"
product: "BytePlus DNS Suite"
product_code: "byteplus-dns-suite"
source: "https://docs.byteplus.com/en/docs/byteplus-dns-suite/DeleteRule"
---

Deletes a rule.

## Request

* Method: POST

* URL: https://gtm.byteplusapi.com/?Action=DeleteRule&Version=2023\-01\-01

## Request parameters

In addition to the following parameters, you need to [authenticate the request](https://docs.byteplus.com/docs/byteplus-dns-suite/FvV-sD).

### Query

|**Name** |**Type** |**Required** |Example |**Description** |
|---|---|---|---|---|
|Action |String |Yes |`DeleteRule` |Name of the API. The value of this parameter is `DeleteRule`. |
|Version |String |Yes |`2023-01-01` |Version of the API. The value of this parameter is `2023-01-01`. |

### Body

|Name |Type |Required |Example |Description |
|---|---|---|---|---|
|GtmId |String |Yes |`2a8f91c4-aa07-4ae4-9ebc-68750d611822` |The UUID of the GTM instance. You can obtain the GtmId through the [ListGtms API](https://docs.byteplus.com/docs/byteplus-dns-suite/CrGpNh) |
|PolicyType |String |Yes |`geo` |The policy type corresponding to the rule.<br><br><br>* geo: Basic routing.<br><br>* perf: Intelligent routing. |
|RuleId |String |Yes |`c3f65de3-7b01-4ad5-8225-d0e42ced2e05` |The ID of the rule. You can obtain the rule ID through the [ListRules API](https://docs.byteplus.com/docs/byteplus-dns-suite/ListRules). |

## Response parameters

### ResponseMetadata object

|Name |Type |Description |
|---|---|---|
|RequestId |String |The ID that identifies this request. |
|Action |String |The value of the Action query parameter. |
|Version |String |The API version. |
|Service |String |The service type. |
|Region |String |The region where the service is located. |

## Example

### Request example

```JSON
POST https://gtm.byteplusapi.com/?Action=DeleteRule&Version=2023-01-01

{
    "GtmId": "2a8f91c4-aa07-4ae4-9ebc-68750d611822",
  "PolicyType": "geo",
    "RuleId": "c3f65de3-7b01-4ad5-8225-d0e42ced2e05"
}
```

### Response example

```json
{
    "ResponseMetadata": {
        "RequestId": "2022111713414601017424613601224A27",
        "Action": "DeleteRule",
        "Version": "2023-01-01",
        "Service": "gtm",
        "Region": "ap-southeast-1"
    }
}
```

## Common error codes

Refer to [Common Error Codes](https://docs.byteplus.com/docs/byteplus-dns-suite/PujiSz).
