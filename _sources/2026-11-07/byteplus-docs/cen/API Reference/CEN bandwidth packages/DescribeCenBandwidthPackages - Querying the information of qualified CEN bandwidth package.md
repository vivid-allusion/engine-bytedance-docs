---
title: "DescribeCenBandwidthPackages - Querying the information of qualified CEN bandwidth package instances"
product: "Cloud Enterprise Network"
product_code: "cen"
source: "https://docs.byteplus.com/en/docs/cen/DescribeCenBandwidthPackages"
---

Call the DescribeCenBandwidthPackages API to query CEN bandwidth packages that meet the specified conditions.

## Instructions

* Pass in multiple request parameters to query based on the specified parameters, returning bandwidth packages that meet all the conditions. If no bandwidth packages meet the conditions, an empty value is returned.

* If none of the optional request parameters are passed in, the query is performed based on the current logged\-in account, returning all bandwidth packages under that account.

* When using tags to query bandwidth packages, a maximum of 1000 bandwidth packages associated with the specified tags can be queried. If the number of bandwidth packages associated with the specified tags exceeds 1000, only the first 1000 are returned. At this point, use the [ListTagsForResources API](https://docs.byteplus.com/en/docs/cen/ListTagsForResources) to query.

## Debug

[去调试](https://api.byteplus.com/api-explorer/?action=DescribeCenBandwidthPackages&groupName=%E5%B8%A6%E5%AE%BD%E5%8C%85&serviceCode=cen&version=2020-04-01)

## Request parameters

The following only details request parameters specific to this API and key common parameters. More information can be found in [Common parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).

**Action ** string必选 `Example: DescribeCenBandwidthPackages`

Action to execute. Set the value to DescribeCenBandwidthPackages.

**Version ** string必选 `Example: 2020-04-01`

The API version. Value: 2020\-04\-01.

**PageSize ** integer`optional` `Example: 10`

Number of rows displayed per page in paginated queries. Value range: 1–50. Default: 10.

**PageNumber ** integer`optional` `Example: 1`

The page number of the list. Default: 1.

**LocalGeographicRegionSetId** string `optional` `Example: China`

The local geographic region ID for CEN interconnection.

**PeerGeographicRegionSetId ** string`optional` `Example: China`

The peer geographic region ID for CEN interconnection.

**CenBandwidthPackageName** string `optional` `Example: cbp-test`

Name of the bandwidth package.

**TagFilters.N.Key ** string[]`optional` `Example: k1`

The tag key.

* N specifies the serial number of the tag key. Valid values: 1\-10.

* Separate multiple tag keys with ampersands (&). The logical relationship between multiple tag keys is AND, meaning bandwidth packages that have all the specified tag keys are queried.

* The tag key must be unique.

**CenId ** string`optional` `Example: cen-7qthudw0ll6jmc****`

Bound CEN instance ID.

You can call the [DescribeCens](https://docs.byteplus.com/en/docs/cen/DescribeCens) API to query the CEN instance ID.

**TagFilters.N.Values.N ** string[]`optional` `Example: v1`

The tag value.

* The first N specifies the serial number of a tag key. Valid values: 1–10.

* The second N represents the serial number of the tag value. Valid values: 1–3. The logical relationship between multiple tag values under the same tag key is OR, meaning bandwidth packages that have any one of the specified tag values under the same tag key are queried.

* Separate multiple tag values with ampersands (&).

* To provide this parameter, provide `TagFilters.N.Key` first.

* When an empty string is passed in, it indicates a query for bandwidth packages with empty tag values.

**ProjectName ** string`optional` `Example: default`

Name of the project to which the bandwidth package belongs.

**CenBandwidthPackageIds.N ** string[]`optional Example: cbp-bp1o94dp5****`

Bandwidth package ID.

* Parameter \- N: Indicates the serial number of the bandwidth package ID, ranging from 1 to 100.

* Separate multiple Bandwidth Package IDs with ampersands (&).

## Response parameters

The following only details response parameters specific to this API. For more information, see [Response structure](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response).

**CenBandwidthPackages ** object[]`Example: --`

Details of the bandwidth package.

**UpdatedAt ** string`Example: 2018-04-18T15:02:37+08:00`

Update time of the bandwidth package.

**LocalGeographicRegionSetId ** string`Example: China`

The local geographic region ID for bandwidth package interconnection.

* China: Mainland China.

* Asia: Asia Pacific.

**BillingType ** integer`Example: 1`

Billing method of the bandwidth package.

* 1: Subscription.

* 4: Pay\-as\-you\-go \- Pay\-by\-95\-peak.

**Description ** string`Example: testdesc`

Description of the bandwidth package.

**PeerGeographicRegionSetId ** string`Example: China`

Peer geographic region ID for bandwidth package interconnection.

**Bandwidth ** integer`Example: 10`

Peak bandwidth of the bandwidth package, in Mbps.

**RemainingBandwidth ** integer`Example: 10`

Remaining unallocated bandwidth of the bandwidth package, in Mbps.

**Status ** string`Example: Available`

Status of the bandwidth package.

* Creating

* Deleting

* Pending: Action in progress​.

* Available: Unbound.

* InUse: Bound.

**Business ** string`Example: Normal`

The business status of the bandwidth package.

* Normal

* FinancialLocked: Locked.

**ProjectName ** string`Example: default`

Name of the project to which the bandwidth package belongs.

**CreationTime ** string`Example: 2018-04-18T15:02:37+08:00`

Creation time of the bandwidth package.

**ExpiredTime ** string`Example: 2021-05-07 23:59:59`

Expiration time of the bandwidth package.

**DeletedTime ** string`Example: 2021-05-22 00:00:00`

Deletion time of the bandwidth package.

**CenBandwidthPackageName ** string`Example: cbp-test`

Name of the bandwidth package.

**Tags ** object[]`Example: --`

Tag information of the bandwidth package.

**Value ** string`Example: v1`

The tag value.

**Key ** string`Example: k1`

The tag key.

**LineOperator ** string`Example: ChinaUnicom`

The provider of cross\-border bandwidth package.

* ChinaTelecom: China Telecom.

* ChinaUnicom: China Unicom.

**UpdateTime ** string`Example: 2018-04-18T15:02:37+08:00`

Update time of the bandwidth package.

**CenIds ** string[]`Example: cen-7qthudw0ll6jmc****`

ID of the CEN instance bound to the bandwidth package.

**CenBandwidthPackageId ** string`Example: cbp-4c2zaavbvh5x****`

Bandwidth package ID.

**AccountId ** string`Example: 210000****`

The ID of the account that owns the TR bandwidth package.

**TotalCount ** integer`Example: 1`

Total number of bandwidth packages that meet the condition.

**PageNumber ** integer`Example: 1`

The current page number.

**PageSize ** integer`Example: 10`

Number of entries per page in the current pagination.

**CenBandwidthPackages ** object[]`Example: --`

Details of the bandwidth package.

**UpdatedAt ** string`Example: 2018-04-18T15:02:37+08:00`

Update time of the bandwidth package.

**LocalGeographicRegionSetId ** string`Example: China`

The local geographic region ID for bandwidth package interconnection.

* China: Mainland China.

* Asia: Asia Pacific.

**BillingType ** integer`Example: 1`

Billing method of the bandwidth package.

* 1: Subscription.

* 4: Pay\-as\-you\-go \- Pay\-by\-95\-peak.

**Description ** string`Example: testdesc`

Description of the bandwidth package.

**PeerGeographicRegionSetId ** string`Example: China`

Peer geographic region ID for bandwidth package interconnection.

**Bandwidth ** integer`Example: 10`

Peak bandwidth of the bandwidth package, in Mbps.

**RemainingBandwidth ** integer`Example: 10`

Remaining unallocated bandwidth of the bandwidth package, in Mbps.

**Status ** string`Example: Available`

Status of the bandwidth package.

* Creating

* Deleting

* Pending: Action in progress​.

* Available: Unbound.

* InUse: Bound.

**Business ** string`Example: Normal`

The business status of the bandwidth package.

* Normal

* FinancialLocked: Locked.

**ProjectName ** string`Example: default`

Name of the project to which the bandwidth package belongs.

**CreationTime ** string`Example: 2018-04-18T15:02:37+08:00`

Creation time of the bandwidth package.

**ExpiredTime ** string`Example: 2021-05-07 23:59:59`

Expiration time of the bandwidth package.

**DeletedTime ** string`Example: 2021-05-22 00:00:00`

Deletion time of the bandwidth package.

**CenBandwidthPackageName ** string`Example: cbp-test`

Name of the bandwidth package.

**Tags ** object[]`Example: --`

Tag information of the bandwidth package.

**Value ** string`Example: v1`

The tag value.

**Key ** string`Example: k1`

The tag key.

**LineOperator ** string`Example: ChinaUnicom`

The provider of cross\-border bandwidth package.

* ChinaTelecom: China Telecom.

* ChinaUnicom: China Unicom.

**UpdateTime ** string`Example: 2018-04-18T15:02:37+08:00`

Update time of the bandwidth package.

**CenIds ** string[]`Example: cen-7qthudw0ll6jmc****`

ID of the CEN instance bound to the bandwidth package.

**CenBandwidthPackageId ** string`Example: cbp-4c2zaavbvh5x****`

Bandwidth package ID.

**AccountId ** string`Example: 210000****`

The ID of the account that owns the TR bandwidth package.

**TotalCount ** integer`Example: 1`

Total number of bandwidth packages that meet the condition.

**PageNumber ** integer`Example: 1`

The current page number.

**PageSize ** integer`Example: 10`

Number of entries per page in the current pagination.

## Request examples

```text
GET /?Action=DescribeCenBandwidthPackages&Version=2020-04-01 HTTP/1.1
Host: cen.byteplusapi.com
X-Date: 20260109T085116Z
Authorization: HMAC-SHA256 Credential=Adfks******wekfwe/20260109/cn-beijing/cen/request, SignedHeaders=host;x-date, Signature=47a7d934ff7b37c03938******cd7b8278a40a1057690c401e92246a0e41085f


```

## Response examples

```json
{
  "ResponseMetadata": {
    "RequestId": "20250818104641055129187147147908",
    "Action": "DescribeCenBandwidthPackages",
    "Version": "2020-04-01",
    "Service": "cen",
    "Region": "cn-beijing"
  },
  "Result": {
    "CenBandwidthPackages": [
      {
        "UpdatedAt": "2018-04-18T15:02:37+08:00",
        "LocalGeographicRegionSetId": "China",
        "BillingType": 1,
        "Description": "testdesc",
        "PeerGeographicRegionSetId": "China",
        "Bandwidth": 10,
        "RemainingBandwidth": 10,
        "Status": "Available",
        "Business": "Normal",
        "ProjectName": "default",
        "CreationTime": "2018-04-18T15:02:37+08:00",
        "ExpiredTime": "2021-05-07 23:59:59",
        "DeletedTime": "2021-05-22 00:00:00",
        "CenBandwidthPackageName": "cbp-test",
        "Tags": [
          {
            "Value": "v1",
            "Key": "k1"
          }
        ],
        "LineOperator": "ChinaUnicom",
        "UpdateTime": "2018-04-18T15:02:37+08:00",
        "CenIds": [
          "cen-7qthudw0ll6jmc****"
        ],
        "CenBandwidthPackageId": "cbp-4c2zaavbvh5x****",
        "AccountId": "210000****"
      }
    ],
    "TotalCount": 1,
    "PageNumber": 1,
    "PageSize": 10
  }
}
```

## Error codes

The table below describes the error codes for this API that are associated with business logic. For details, see [Common error codes](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-error-codes).

|Status code |Error codes |Error message |Notes |
|---|---|---|---|
|400 |MissingParameter |The request is missing a required parameter. Ensure that you have supplied all the required parameters for the request. |This request does not contain required parameters. Ensure all required parameters are provided when initiating the request. |
|400 |InvalidParameter |A parameter specified in the request is not valid, is unsupported or cannot be used. |The request contains invalid or unsupported parameters. |
|400 |InvalidPage.Malformed |The specified page is malformed. |The specified pagination parameter is invalid. |
|400 |LimitExceeded.ResourceIds |You've reached the limit of 100 resource IDs that can be specified in this request. |You have reached the maximum number of instances that you can query in a single request. |
|400 |InvalidTagFilterKey.Malformed |The specified parameter tag filter key is invalid. |The tag filter key is invalid. |
|400 |InvalidTagFilterValue.Malformed |The specified parameter tag filter value is invalid. |The tag filter value is invalid. |
|400 |LimitExceeded.TagFilterKey |You've reached the limit on the number of tag keys that you can filter. |You have reached the maximum number of tag keys that you can specify for filtering in a single request. |
|400 |LimitExceeded.TagFilterValue |You've reached the limit on the number of tag values that you can filter. |You have reached the maximum number of tag values that you can specify for filtering in a single request. |
|400 |InvalidTagFilter.Disorder |The specified index order of tag filter is malformed. |The index order format of the specified tag filter is invalid. |
|500 |InternalError |Request failed with internal server error. |Internal system error. |
