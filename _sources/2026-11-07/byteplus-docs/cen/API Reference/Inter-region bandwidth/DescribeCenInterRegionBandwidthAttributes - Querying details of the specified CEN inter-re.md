---
title: "DescribeCenInterRegionBandwidthAttributes - Querying details of the specified CEN inter-region bandwidth instance"
product: "Cloud Enterprise Network"
product_code: "cen"
source: "https://docs.byteplus.com/en/docs/cen/DescribeCenInterRegionBandwidthAttributes"
---

Call the DescribeCenInterRegionBandwidthAttributes API to view the details of the specified inter\-region bandwidth.

## Debug

[去调试](https://api.volcengine.com/tools/api-explorer/?action=DescribeCenInterRegionBandwidthAttributes&groupName=%E5%9F%9F%E9%97%B4%E5%B8%A6%E5%AE%BD&serviceCode=cen&version=2020-04-01)

## Request parameters

The table below lists only the request parameters unique to this interface and some common parameters. For more information, see [Common parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).

**Action ** string必选 `Example: DescribeCenInterRegionBandwidthAttributes`

Action to execute. Set the value to DescribeCenInterRegionBandwidthAttributes.

**Version ** string必选`Example: 2020-04-01`

Current API version is 2020\-04\-01.

**InterRegionBandwidthId ** string必选 `Example: cirb-3tex2x1cwd4c6c0v****`

ID of the CEN inter\-region bandwidth.

You can call the [DescribeCenInterRegionBandwidths](https://docs.byteplus.com/en/docs/cen/DescribeCenInterRegionBandwidths) API to query the inter\-region bandwidth ID.

## Response parameters

Only the response parameters specific to this API are listed below. For more information, see [Response structure](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response).

**PeerRegionId ** string`Example: cn-nantong`

The ID of the peer region for the Cloud Enterprise Network(CEN) inter\-region bandwidth.

**LocalRegionId ** string`Example: cn-beijing`

The ID of the local region for the CEN inter\-region bandwidth.

**CenId ** string`Example: cen-2fehhikz9v9xc59gp684g****`

ID of the CEN instance.

**UpdateTime ** string`Example: 2021-04-10T09:18:28+08:00`

Update time of CEN inter\-region bandwidth.

**CreationTime ** string`Example: 2021-04-09T08:36:47+08:00`

Creation time of the CEN inter\-region bandwidth.

**InterRegionBandwidthId ** string`Example: cirb-3tex2x1cwd4c6c0v****`

ID of the CEN inter\-region bandwidth.

**Status ** string`Example: Available`

The status of the CEN inter\-region bandwidth.

* Creating

* Deleting

* Pending: Configuring

* Available

**Bandwidth ** integer`Example: 1000`

Peak bandwidth of CEN inter\-region bandwidth.

**CenBandwidthPackageId ** string`Example: cbp-4c2zaavbvh5fx****`

Bandwidth package ID.

**BandwidthType ** string`Example: BandwidthPackage`

Bandwidth usage method.

* BandwidthPackage: Subscription bandwidth package.

* CloudDataTransfer: Pay\-by\-traffic billing, i.e., billing for traffic between regions. It is already integrated with Cloud Data Transfer (CDT). For more information, see [Cloud Data Transfer](https://docs.byteplus.com/en/docs/Cloud_Data_Transfer/What_is_Cloud_Data_Transfer).

**LineOperator ** string`Example: ChinaUnicom`

Line Operator for cross\-border bandwidth.

* ChinaUnicom: China Unicom.

* ChinaTelecom: China Telecom.

## Request example

```text
GET /?Action=DescribeCenInterRegionBandwidthAttributes&Version=2020-04-01&InterRegionBandwidthId=cirb-3tex2x1cwd4c6c0v**** HTTP/1.1
Host: cen.byteplusapi.com
X-Date: 20260109T083158Z
Authorization: HMAC-SHA256 Credential=Adfks******wekfwe/20260109/cn-beijing/cen/request, SignedHeaders=host;x-date, Signature=47a7d934ff7b37c03938******cd7b8278a40a1057690c401e92246a0e41085f


```

## Response example

```json
{
  "ResponseMetadata": {
    "RequestId": "20250815172006243139111038E62978",
    "Action": "DescribeCenInterRegionBandwidthAttributes",
    "Version": "2020-04-01",
    "Service": "cen",
    "Region": "cn-beijing"
  },
  "Result": {
    "PeerRegionId": "cn-nantong",
    "LocalRegionId": "cn-beijing",
    "CenId": "cen-2fehhikz9v9xc59gp684g****",
    "UpdateTime": "2021-04-10T09:18:28+08:00",
    "CreationTime": "2021-04-09T08:36:47+08:00",
    "InterRegionBandwidthId": "cirb-3tex2x1cwd4c6c0v****",
    "Status": "Available",
    "Bandwidth": 1000,
    "CenBandwidthPackageId": "cbp-4c2zaavbvh5fx****"
  }
}
```

## Error codes

The following table lists the error codes related to the business logic for this API. For common error codes, see [Common error codes](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-error-codes).

|Status code |Error codes |Error message |Notes |
|---|---|---|---|
|400 |InvalidParameter |A parameter specified in the request is not valid, is unsupported or cannot be used. |This request contains an invalid or unsupported parameter. |
|400 |MissingParameter |The request is missing a required parameter. Ensure that you have supplied all the required parameters for the request. |This request does not contain the required parameter. Ensure all required parameters are provided when initiating the request. |
|404 |InvalidInterRegionBandwidth.NotFound |The specified inter\-region bandwidth does not exist. |The specified inter\-region bandwidth does not exist. |
|500 |InternalError |Request failed with internal server error. |Internal system error. |
