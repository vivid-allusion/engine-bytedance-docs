---
title: "DescribeCenSummaryRouteEntries - Querying the qualified CEN summary route entries"
product: "Cloud Enterprise Network"
product_code: "cen"
source: "https://docs.byteplus.com/en/docs/cen/DescribeCenSummaryRouteEntries"
---

Call the DescribeCenSummaryRouteEntries API to query the summary route entries that meet specified conditions.

## Instructions

The summary route entry is currently in beta stage. If you need a trial, please contact your account manager.

## Debug

[去调试](https://api.byteplus.com/api-explorer/?action=DescribeCenSummaryRouteEntries&groupName=%E6%B1%87%E6%80%BB%E8%B7%AF%E7%94%B1&serviceCode=cen&version=2020-04-01)

## Request parameters

The following only details request parameters specific to this API and key common parameters. More information can be found in [Common parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).

**Action ** string必选 `Example: DescribeCenSummaryRouteEntries`

Action to execute. Set the value to DescribeCenSummaryRouteEntries.

**Version ** string必选 `Example: 2020-04-01`

The API version. Value: 2020\-04\-01.

**CenId ** string必选 `Example: cen-7qthudw0ll6jmc****`

CEN instance ID.

You can call the [DescribeCens](https://docs.byteplus.com/en/docs/cen/DescribeCens) API to query the CEN instance ID.

**DestinationCidrBlock ** string`optional` `Example: 172.XX.XX.0/24`

The destination CIDR of the CEN summary route.

**PageNumber ** integer`optional` `Example: 1`

Page number of the list. Default: 1.

**PageSize ** integer`optional` `Example: 20`

The number of entries per page in a pagination query. Value range: 1–100. Default: 20.

## Response parameters

The following only details response parameters specific to this API. For more information, see [Response structure](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response).

**PageSize ** integer`Example: 1`

Number of entries per page in the current pagination.

**TotalCount ** integer`Example: 1`

Total number of eligible summary routes.

**CenSummaryRouteEntries ** object[]`Example: --`

Details of the CEN summary route entries.

**DestinationCidrBlock ** string`Example: 172.XX.XX.0/24`

Destination CIDR of the summary route entry.

**Status ** string`Example: Available`

Effective status of the summary route.

* Available

* Pending: ​​Configuration in progress.

* Conflicted

**CreationTime ** string`Example: 2021-04-09T08:36:47+08:00`

Creation time of the summary route.

**UpdateTime ** string`Example: 2021-04-10T09:18:28+08:00`

Update time of summary route.

**Description ** string`Example: This is an example description.`

Description of the CEN summary route.

**CenId ** string`Example: cen-7qthudw0ll6jmc****`

The CEN instance ID.

**PageNumber ** integer`Example: 1`

The current page number.

**PageSize ** integer`Example: 1`

Number of entries per page in the current pagination.

**TotalCount ** integer`Example: 1`

Total number of eligible summary routes.

**CenSummaryRouteEntries ** object[]`Example: --`

Details of the CEN summary route entries.

**DestinationCidrBlock ** string`Example: 172.XX.XX.0/24`

Destination CIDR of the summary route entry.

**Status ** string`Example: Available`

Effective status of the summary route.

* Available

* Pending: ​​Configuration in progress.

* Conflicted

**CreationTime ** string`Example: 2021-04-09T08:36:47+08:00`

Creation time of the summary route.

**UpdateTime ** string`Example: 2021-04-10T09:18:28+08:00`

Update time of summary route.

**Description ** string`Example: This is an example description.`

Description of the CEN summary route.

**CenId ** string`Example: cen-7qthudw0ll6jmc****`

The CEN instance ID.

**PageNumber ** integer`Example: 1`

The current page number.

## Request examples

```text
GET /?Action=DescribeCenSummaryRouteEntries&Version=2020-04-01&CenId=cen-7qthudw0ll6jmc**** HTTP/1.1
Host: cen.byteplusapi.com
X-Date: 20260109T074209Z
Authorization: HMAC-SHA256 Credential=Adfks******wekfwe/20260109/cn-beijing/cen/request, SignedHeaders=host;x-date, Signature=47a7d934ff7b37c03938******cd7b8278a40a1057690c401e92246a0e41085f


```

## Response examples

```json
{
  "ResponseMetadata": {
    "RequestId": "20250815154640242088015211674609",
    "Action": "DescribeCenSummaryRouteEntries",
    "Version": "2020-04-01",
    "Service": "cen",
    "Region": "cn-beijing"
  },
  "Result": {
    "PageSize": 1,
    "TotalCount": 1,
    "CenSummaryRouteEntries": [
      {
        "DestinationCidrBlock": "172.XX.XX.0/24",
        "Status": "Available",
        "CreationTime": "2021-04-09T08:36:47+08:00",
        "UpdateTime": "2021-04-10T09:18:28+08:00",
        "Description": "This is an example description.",
        "CenId": "cen-7qthudw0ll6jmc****"
      }
    ],
    "PageNumber": 1
  }
}
```

## Error codes

The table below describes the error codes for this API that are associated with business logic. For details, see [Common error codes](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-error-codes).

|Status code |Error codes |Error message |Notes |
|---|---|---|---|
|400 |MissingParameter |The request is missing a required parameter. Ensure that you have supplied all the required parameters for the request. |This request does not contain required parameters. Ensure all required parameters are provided when initiating the request. |
|400 |InvalidParameter |A parameter specified in the request is not valid, is unsupported or cannot be used. |The request contains invalid or unsupported parameters. |
|400 |InvalidCidr.Malformed |The specified cidr block is malformed. |The format of the specified CIDR block is invalid. |
|400 |InvalidDescription.Malformed |The specified description is malformed. |The specified description format is invalid. Correct the description format and retry. |
|400 |LimitExceeded.CenSummaryRouteEntry |You've reached the limit on the number of summary route entries that you can create on a CEN. |The maximum number of summary routes that can be created on a single CEN instance has been reached. |
|400 |InvalidPage.Malformed |The specified page is malformed. |The specified pagination parameter is invalid. |
|403 |Forbidden.CreateCenSummaryRouteEntry |You are not authorized to create CEN summary route entry. |No permission to create a CEN summary route. |
|404 |InvalidCen.NotFound |The specified CEN does not exist. |The specified CEN instance does not exist. |
|409 |InvalidCen.InvalidStatus |The specified CEN instance is not in the correct status for the request. |The specified CEN instance is in a state that cannot process the request. Please try again later. |
|409 |InvalidCenSummaryRoute.Conflict |The specified summary route has already existed on the CEN. |The specified summary route entry already exists. |
|500 |InternalError |Request failed with internal server error. |Internal system error. |
