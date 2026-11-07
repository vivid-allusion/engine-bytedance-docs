---
title: "DescribeCenBandwidthPackagesBilling - Querying the billing information of qualified bandwidth package instances"
product: "Cloud Enterprise Network"
product_code: "cen"
source: "https://docs.byteplus.com/en/docs/cen/DescribeCenBandwidthPackagesBilling"
---

Call the DescribeCenBandwidthPackagesBilling API to view the billing information of bandwidth packages.

## Debug

[去调试](https://api.byteplus.com/api-explorer/?action=DescribeCenBandwidthPackagesBilling&groupName=%E5%B8%A6%E5%AE%BD%E5%8C%85&serviceCode=cen&version=2020-04-01)

## Request parameters

The following only details request parameters specific to this API and key common parameters. More information can be found in [Common parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).

**Action ** string必选 `Example: DescribeCenBandwidthPackagesBilling`

Action to execute. Set the value to DescribeCenBandwidthPackagesBilling.

**Version ** string必选 `Example: 2020-04-01`

The API version. Value: 2020\-04\-01.

**PageSize ** integer`optional` `Example: 20`

Number of rows displayed per page in paginated queries. Value range: 1–100. Default: 20.

**PageNumber ** integer`optional` `Example: 1`

The page number of the list. Default: 1.

**CenBandwidthPackageIds.N ** string[]`optional` `Example: cbp-4c2zaavbvh5x****`

Bandwidth package ID.

You can call the [DescribeCenBandwidthPackages](https://docs.byteplus.com/en/docs/cen/DescribeCenBandwidthPackages) API to get the Bandwidth Package ID.

* Parameter \- N: Indicates the serial number of the bandwidth package ID, ranging from 1 to 100.

* Separate multiple Bandwidth Package IDs with ampersands (&).

## Response parameters

The following only details response parameters specific to this API. More information, see [Response structure](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response).

**PageSize ** integer`Example: 20`

Number of entries per page in the current pagination.

**PageNumber ** integer`Example: 1`

The current page number.

**TotalCount ** integer`Example: 1`

Total number of eligible bandwidth package instances.

**CenBandwidthPackages ** object[]`Example: --`

Detailed information of the bandwidth package instance.

**BillingStatus ** integer`Example: 1`

Billing status of the bandwidth package instance.

* 0: Creating

* 1: Running

* 3: Unsubscribed

* 4: Expired and suspended

* 5: Expired and reclaimed

* 6: Suspended due to overdue payments

* 7: Reclaimed due to overdue payments

* 8: Suspended due to unsubscription

**BillingType ** integer`Example: 1`

Billing method of the bandwidth package instance.

* 1: Subscription.

* 4: Pay\-as\-you\-go \- Pay\-by\-95\-peak.

**ExpiredTime ** string`Example: 2021-05-07 23:59:59`

Expiration time of the bandwidth package instance.

**ReclaimTime ** string`Example: 2021-05-07 23:23:23`

Reclaim time after expiration for a bandwidth package instance.

**RemainRenewTimes ** integer`Example: 1`

The number of automatic renewals.

Values include \-1 and 1 to 100. The default is \-1, meaning unlimited automatic renewals.

**RenewType ** string`Example: Auto`

Renewal type of the bandwidth package instance.

* Manual: Manual renewal.

* Auto: Automatic renewal

* NoRenew: Non\-renewal.

**CenBandwidthPackageId ** string`Example: cbp-4c2zaavbvh5x****`

The instance ID of the bandwidth package.

## Request examples

```text
GET /?Action=DescribeCenBandwidthPackagesBilling&Version=2020-04-01 HTTP/1.1
Host: cen.byteplusapi.com
X-Date: 20260109T085237Z
Authorization: HMAC-SHA256 Credential=Adfks******wekfwe/20260109/cn-beijing/cen/request, SignedHeaders=host;x-date, Signature=47a7d934ff7b37c03938******cd7b8278a40a1057690c401e92246a0e41085f


```

## Response examples

```json
{
  "ResponseMetadata": {
    "RequestId": "20250815170517145088034118C01048",
    "Action": "DescribeCenBandwidthPackagesBilling",
    "Version": "2020-04-01",
    "Service": "cen",
    "Region": "cn-beijing"
  },
  "Result": {
    "PageSize": 20,
    "PageNumber": 1,
    "TotalCount": 2,
    "CenBandwidthPackages": {
      "BillingStatus": 1,
      "BillingType": 1,
      "ExpiredTime": "2021-05-07 23:59:59",
      "ReclaimTime": "2021-05-07 23:23:23",
      "RemainRenewTimes": 1,
      "RenewType": "Auto",
      "CenBandwidthPackageId": "cbp-4c2zaavbvh5x****"
    }
  }
}
```

## Error codes

The table below describes the error codes for this API that are associated with business logic. For details, see [Common error codes](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-error-codes).

|Status code |Error codes |Error message |Notes |
|---|---|---|---|
|400 |MissingParameter |The request is missing a required parameter. Ensure that you have supplied all the required parameters for the request. |This request does not contain required parameters. Ensure all required parameters are provided when initiating the request. |
|400 |InvalidParameter |A parameter specified in the request is not valid, is unsupported or cannot be used. |The request contains invalid or unsupported parameters. |
|400 |LimitExceeded.ResourceIds |You've reached the limit of 100 resource IDs that can be specified in this request. |You have reached the maximum number of instances that you can query in a single request. |
|400 |InvalidPage.Malformed |The specified page is malformed. |The specified pagination parameter is invalid. |
|500 |InternalError |Request failed with internal server error. |Internal system error. |
