---
title: "ListProbeTaskIds"
product: "BytePlus DNS Suite"
product_code: "byteplus-dns-suite"
source: "https://docs.byteplus.com/en/docs/byteplus-dns-suite/ListProbeTaskIds"
---

Lists health check tasks by ID.

## Request

* Method: POST

* URL: https://gtm.byteplusapi.com/?Action=ListProbeTaskIds&Version=2023\-01\-01

## Request parameters

In addition to the following parameters, you need to [authenticate the request](https://docs.byteplus.com/docs/byteplus-dns-suite/FvV-sD).

### Query

|**Name** |**Type** |**Required** |Example |**Description** |
|---|---|---|---|---|
|Action |String |Yes |`ListProbeTaskIds` |The name of the API. The value of this parameter is `ListProbeTaskIds`. |
|Version |String |Yes |`2023-01-01` |The version of the API. The value of this parameter is `2023-01-01`. |
|GtmId |String |Yes |`2a8f91c4-aa07-4ae4-9ebc-68750d611822` |The UUID of the GTM instance. You can obtain the GtmId through the [ListGtms API](https://docs.byteplus.com/docs/byteplus-dns-suite/CrGpNh). |
|Address |String |No |`203.0.113.0` |Address of the health check tasks. By default, this API returns all health check tasks of a maximum of 100 randomly selected addresses. |

## Response parameters

### ResponseMetadata object

|Name |Type |Description |
|---|---|---|
|RequestId |String |The ID that identifies this request. |
|Action |String |The value of the Action query parameter. |
|Version |String |The API version. |
|Service |String |The service type. |
|Region |String |The region where the service is located. |

### Result object

|Name |Type |Description |
|---|---|---|
|Data |JSON Object |Health check tasks. |
|ProbeTasks |Array of Objects |A group of health check tasks with the same target address. |
|Line |String |Line of the health check task. |
|ProbeTaskId |Integer |ID the health check task. |
|RuleName |String |Name of the rule associated with the health check task. If the rule is a system\-generated rule, RuleName is `-`. |
|Target |String |Target address of the health check tasks. |

## Example

### Request example

```HTTP
POST https://gtm.byteplusapi.com/?Action=ListProbeTaskIds&Version=2023-01-01&GtmId=31cb7495-72ae-4854-92f3-b8e80eb99171

```

### Response example

```json
{
  "ResponseMetadata": {
    "RequestId": "20240722065033A59118D3AD7C1B0B6628",
    "Action": "ListProbeTaskIds",
    "Version": "2023-01-01",
    "Service": "gtm",
    "Region": "ap-southeast-1"
  },
  "Result": {
    "Data": [
      {
        "ProbeTasks": [
          {
            "Line": "cn_telecom_qinghai",
            "ProbeTaskId": 24277816,
            "RuleName": "-"
          },
          {
            "Line": "cn_telecom_hubei",
            "ProbeTaskId": 24277807,
            "RuleName": "-"
          },
          {
            "Line": "cn_unicom_heilongjiang",
            "ProbeTaskId": 24277803,
            "RuleName": "-"
          },
          {
            "Line": "cn_unicom_jilin",
            "ProbeTaskId": 24277799,
            "RuleName": "-"
          },
          {
            "Line": "cn_telecom_liaoning",
            "ProbeTaskId": 24277795,
            "RuleName": "-"
          },
          {
            "Line": "cn_mobile_hubei",
            "ProbeTaskId": 24277793,
            "RuleName": "-"
          },
          {
            "Line": "cn_telecom_chongqing",
            "ProbeTaskId": 24277786,
            "RuleName": "-"
          },
          {
            "Line": "cn_telecom_shanghai",
            "ProbeTaskId": 24277783,
            "RuleName": "-"
          },
          {
            "Line": "cn_unicom_liaoning",
            "ProbeTaskId": 24277779,
            "RuleName": "-"
          },
          {
            "Line": "cn_mobile_beijing",
            "ProbeTaskId": 24277775,
            "RuleName": "-"
          },
          {
            "Line": "cn_mobile_chongqing",
            "ProbeTaskId": 24277730,
            "RuleName": "-"
          },
          {
            "Line": "cn_mobile_heilongjiang",
            "ProbeTaskId": 24277726,
            "RuleName": "-"
          },
          {
            "Line": "volc",
            "ProbeTaskId": 24277722,
            "RuleName": "-"
          },
          {
            "Line": "volc",
            "ProbeTaskId": 24277722,
            "RuleName": "-"
          },
          {
            "Line": "cn_telecom_guangdong",
            "ProbeTaskId": 24277719,
            "RuleName": "-"
          },
          {
            "Line": "cn_telecom_beijing",
            "ProbeTaskId": 24277716,
            "RuleName": "-"
          },
          {
            "Line": "cn_unicom_beijing",
            "ProbeTaskId": 24277710,
            "RuleName": "-"
          },
          {
            "Line": "cn_mobile_shanghai",
            "ProbeTaskId": 24277706,
            "RuleName": "-"
          }
        ],
        "Target": "203.0.113.0"
      },
      {
        "ProbeTasks": [
          {
            "Line": "cn_telecom_qinghai",
            "ProbeTaskId": 24277814,
            "RuleName": "-"
          },
          {
            "Line": "cn_telecom_hubei",
            "ProbeTaskId": 24277806,
            "RuleName": "-"
          },
          {
            "Line": "cn_unicom_heilongjiang",
            "ProbeTaskId": 24277802,
            "RuleName": "-"
          },
          {
            "Line": "cn_unicom_jilin",
            "ProbeTaskId": 24277798,
            "RuleName": "-"
          },
          {
            "Line": "cn_telecom_liaoning",
            "ProbeTaskId": 24277794,
            "RuleName": "-"
          },
          {
            "Line": "cn_mobile_hubei",
            "ProbeTaskId": 24277792,
            "RuleName": "-"
          },
          {
            "Line": "cn_telecom_chongqing",
            "ProbeTaskId": 24277789,
            "RuleName": "-"
          },
          {
            "Line": "cn_telecom_shanghai",
            "ProbeTaskId": 24277782,
            "RuleName": "-"
          },
          {
            "Line": "cn_unicom_liaoning",
            "ProbeTaskId": 24277778,
            "RuleName": "-"
          },
          {
            "Line": "cn_mobile_beijing",
            "ProbeTaskId": 24277774,
            "RuleName": "-"
          },
          {
            "Line": "cn_mobile_guangdong",
            "ProbeTaskId": 24277770,
            "RuleName": "-"
          },
          {
            "Line": "cn_mobile_shanghai",
            "ProbeTaskId": 24277705,
            "RuleName": "-"
          }
        ],
        "Target": "203.0.113.1"
      },
      {
        "ProbeTasks": [
          {
            "Line": "default",
            "ProbeTaskId": 24277749,
            "RuleName": "-"
          }
        ],
        "Target": "203.0.113.2"
      }
    ]
  }
}
```

## Common error codes

Refer to [Common Error Codes](https://docs.byteplus.com/docs/byteplus-dns-suite/PujiSz).
