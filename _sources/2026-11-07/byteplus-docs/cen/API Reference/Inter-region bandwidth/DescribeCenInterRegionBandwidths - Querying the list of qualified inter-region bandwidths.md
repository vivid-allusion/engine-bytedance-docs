---
title: "DescribeCenInterRegionBandwidths - Querying the list of qualified inter-region bandwidths for CEN instances"
product: "Cloud Enterprise Network"
product_code: "cen"
source: "https://docs.byteplus.com/en/docs/cen/DescribeCenInterRegionBandwidths"
---

Call the DescribeCenInterRegionBandwidths API to query inter\-region bandwidth that meets the conditions.

## Debug

[去调试](https://api.volcengine.com/tools/api-explorer/?action=DescribeCenInterRegionBandwidths&groupName=%E5%9F%9F%E9%97%B4%E5%B8%A6%E5%AE%BD&serviceCode=cen&version=2020-04-01)

## Request parameters

The table below lists only the request parameters unique to this interface and some common parameters. For more information, see [Common parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).

**Action ** string必选 `Example: DescribeCenInterRegionBandwidths`

Action to execute. Set the value to DescribeCenInterRegionBandwidths.

**Version ** string必选 `Example: 2020-04-01`

Current API version is 2020\-04\-01.

**PageNumber ** integer`optional` `Example: 1`

Page number of the list. Default: 1.

**PageSize ** integer`optional` `Example: 20`

The number of rows per page for paginated queries. Value range: 1–100. Default: 20.

**CenId ** string`optional` `Example: cen-7qthudw0ll6jmc****`

The CEN instance ID.

**InterRegionBandwidthIds.N ** string[]`optional` `Example: cirb-3tex2x1cwd4c6c0v****`

ID of the CEN inter\-region bandwidth.

* Parameter \- N: Represents the serial number of the CEN inter\-region bandwidth ID, value range: 1 to 100.

* Separate multiple inter\-region bandwidth IDs with ampersands (&).

## Response parameters

Only the response parameters specific to this API are listed below. For more information, see [Response structure](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response).

**InterRegionBandwidths ** object[]`Example: --`

Details of CEN inter\-region bandwidth.

**InterRegionBandwidthId ** string`Example: cirb-3tex2x1cwd4c6c0v****`

ID of the CEN inter\-region bandwidth.

**CreationTime ** string`Example: 2021-04-09T08:36:47+08:00`

Creation time of the CEN inter\-region bandwidth.

**UpdateTime ** string`Example: 2021-04-10T09:18:28+08:00`

Update time of CEN inter\-region bandwidth.

**CenId ** string`Example: cen-2fehhikz9v9xc59gp684g****`

ID of the CEN instance.

**LocalRegionId ** string`Example: cn-beijing`

The ID of the local region for the CEN inter\-region bandwidth.

**PeerRegionId ** string`Example: cn-nantong`

The ID of the peer region for the CEN inter\-region bandwidth.

**Bandwidth ** integer`Example: 1000`

Peak bandwidth of CEN inter\-region bandwidth.

**Status ** string`Example: Available`

The status of the CEN inter\-region bandwidth.

* Creating

* Deleting

* Pending: Configuration in progress.

* Available

**CenBandwidthPackageId ** string`Example: cbp-4c2zaavbvh5fx****`

Bandwidth package ID.

**BandwidthType ** string`Example: BandwidthPackage`

Bandwidth usage method.

* BandwidthPackage: Subscription bandwidth package.

* CloudDataTransfer: Pay\-by\-traffic billing, i.e., billing for traffic between regions. It is already integrated with Cloud Data Transfer (CDT). For more information, see [Cloud Data Transfer](https://docs.byteplus.com/en/docs/Cloud_Data_Transfer/What_is_Cloud_Data_Transfer).

**LineOperator ** string`Example: ChinaUnicom`

* Line operator.

   ChinaUnicom: China Unicom.

   ChinaTelecom: China Telecom.

**PageSize ** integer`Example: 20`

The number of rows on the current page.

**PageNumber ** integer`Example: 1`

Current page number.

**TotalCount** integer `Example: 10`

Total number of CEN inter\-region bandwidths that meet the specified conditions.

## Request example

```text
GET /?Action=DescribeCenInterRegionBandwidths&Version=2020-04-01 HTTP/1.1
Host: cen.byteplusapi.com
X-Date: 20260109T083223Z
Authorization: HMAC-SHA256 Credential=Adfks******wekfwe/20260109/cn-beijing/cen/request, SignedHeaders=host;x-date, Signature=47a7d934ff7b37c03938******cd7b8278a40a1057690c401e92246a0e41085f


```

## Response example

```json
{
  "ResponseMetadata": {
    "RequestId": "20250815172134047147186243D6F3F9",
    "Action": "DescribeCenInterRegionBandwidths",
    "Version": "2020-04-01",
    "Service": "cen",
    "Region": "cn-beijing"
  },
  "Result": {
    "InterRegionBandwidths": [
      {
        "InterRegionBandwidthId": "cirb-3tex2x1cwd4c6c0v****",
        "CreationTime": "2021-04-09T08:36:47+08:00",
        "UpdateTime": "2021-04-10T09:18:28+08:00",
        "CenId": "cen-2fehhikz9v9xc59gp684g****",
        "LocalRegionId": "cn-beijing",
        "PeerRegionId": "cn-nantong",
        "Bandwidth": 1000,
        "CenBandwidthPackageId": "cbp-4c2zaavbvh5fx****",
        "Status": "Available"
      }
    ],
    "PageSize": 20,
    "PageNumber": 1,
    "TotalCount": 10
  }
}
```

## Error codes

The following table lists the error codes related to the business logic for this API. For details, see [Common error codes](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-error-codes).

|Status code |Error codes |Error message |Description |
|---|---|---|---|
|400 |InvalidPage.Malformed |The specified page is malformed. |The specified pagination parameter is invalid. |
|400 |InvalidParameter |A parameter specified in the request is not valid, is unsupported or cannot be used. |This request contains an invalid or unsupported parameter. |
|400 |LimitExceeded.ResourceIds |You've reached the limit of 100 resource IDs that can be specified in this request. |The maximum number of instances that can be queried in a single request has been reached. |
|400 |MissingParameter |The request is missing a required parameter. Ensure that you have supplied all the required parameters for the request. |This request is missing a required parameter. Ensure all required parameters are provided when initiating the request. |
|500 |InternalError |Request failed with internal server error. |Internal system error. |
