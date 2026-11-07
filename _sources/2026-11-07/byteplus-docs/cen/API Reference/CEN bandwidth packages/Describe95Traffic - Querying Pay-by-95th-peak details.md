---
title: "Describe95Traffic - Querying Pay-by-95th-peak details"
product: "Cloud Enterprise Network"
product_code: "cen"
source: "https://docs.byteplus.com/en/docs/cen/Describe95Traffic"
---

Call the Describe95Traffic API to query Pay\-by\-95th\-peak details.

## Request parameters

The following only details request parameters specific to this API and key common parameters. More information can be found in [Common parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).

**Action ** string必选`Example: Describe95Traffic`

Action to execute. Set the value to Describe95Traffic.

**Version ** string必选 `Example: 2020-04-01`

The API version. Value: 2020\-04\-01.

**ResourceType ** string必选 `Example: CenBandwidthPackage`

The resource type. Valid values:

* CenBandwidthPackage: CEN Bandwidth Package

**InstanceId ** string必选 `Example: cbp-4c2zaavbvh5fx****`

ID of the CEN Bandwidth Package instance.

**Day ** string必选 `Example: 2026-01-01`

Query date.

## Response parameters

Only the response parameters specific to this API are listed below. More information, see [Response structure](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response).

**TrafficData ** object`Example: --`

Billing traffic information.

**InstanceId ** string`Example: cbp-4c2zaavbvh5fx****`

ID of the CEN Bandwidth Package instance.

**Bandwidth ** long`Example: 100`

Daily bandwidth cap of the CEN Bandwidth Package instance, unit: Mbps.

**GuaranteedRatio ** integer`Example: 20`

Minimum guaranteed ratio for the current day, unit: %.

**TrafficDetailDatas ** object[]`Example: --`

Detailed bandwidth usage data at sampling points.

**StartTime ** string`Example: 2026-01-01T00:00:00+08:00`

Sampling start time.

**EndTime ** string`Example: 2026-01-01T00:00:00+08:00`

Sampling end time.

**BillBandwidth ** string`Example: 100`

Billing bandwidth in Mbps.

## Request example

```text
GET /?Action=Describe95Traffic&Version=2020-04-01&ResourceType=CenBandwidthPackage&InstanceId=cbp-4c2zaavbvh5fx****&Day=2026-01-01 HTTP/1.1
Host: cen.byteplusapi.com
X-Date: 20260703T040012Z
Authorization: HMAC-SHA256 Credential=Adfks******wekfwe/20260703/cn-beijing/cen/request, SignedHeaders=host;x-date, Signature=47a7d934ff7b37c03938******cd7b8278a40a1057690c401e92246a0e41085f


```

## Response examples

```json
{
  "ResponseMetadata": {
    "RequestId": "20260703120017031195004154DF6C88",
    "Action": "Describe95Traffic",
    "Version": "2020-04-01",
    "Service": "cen",
    "Region": "cn-beijing"
  },
  "Result": {
    "TrafficData": {
      "InstanceId": "cbp-4c2zaavbvh5fx****",
      "Bandwidth": 100,
      "GuaranteedRatio": 20,
      "TrafficDetailDatas": [
        {
          "StartTime": "2026-01-01T00:00:00+08:00",
          "EndTime": "2026-01-01T00:00:00+08:00",
          "BillBandwidth": "100"
        }
      ]
    }
  }
}
```

## Error codes

The following table lists the error codes related to the business logic for this API. For details, see [Common error codes](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-error-codes).

|Status code |Error codes |Error message |Notes |
|---|---|---|---|
|400 |InvalidParameter |A parameter specified in the request is not valid, is unsupported or cannot be used. |This request contains an invalid or unsupported parameter. |
|400 |MissingParameter |The request is missing a required parameter. Ensure that you have supplied all the required parameters for the request. |This request is missing a required parameter. Ensure all required parameters are provided when initiating the request. |
|400 |InvalidParameter.ResourceTypeNotSupported |The specified ResourceType is not supported. |The specified ResourceType does not support this query operation. |
|400 |InvalidParameter.Day |The specified Day is malformed. Ensure that the format is YYYY\-MM\-DD. |The specified date format is invalid. The required format is YYYY\-MM\-DD. |
|400 |InvalidParameter.InstanceId |The specified InstanceId is invalid or does not match the ResourceType. |The specified InstanceId format is invalid or does not match the ResourceType. |
|400 |InvalidParameter.DayOutOfRange |The specified InstanceId is invalid or does not match the ResourceType. |The specified date is beyond the queryable range. Currently, only tracking data from the last 3 months can be queried. |
|500 |InternalError |Request failed with internal server error. |Internal system error. |
