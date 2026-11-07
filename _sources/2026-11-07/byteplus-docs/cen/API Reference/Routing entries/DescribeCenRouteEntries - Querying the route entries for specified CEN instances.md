---
title: "DescribeCenRouteEntries - Querying the route entries for specified CEN instances"
product: "Cloud Enterprise Network"
product_code: "cen"
source: "https://docs.byteplus.com/en/docs/cen/DescribeCenRouteEntries"
---

Call the DescribeCenRouteEntries API to query details of CEN route entries.

## Debug

[去调试](https://api.byteplus.com/api-explorer/?action=DescribeCenRouteEntries&groupName=%E8%B7%AF%E7%94%B1%E4%BF%A1%E6%81%AF&serviceCode=cen&version=2020-04-01)

## Request parameters

The following only details request parameters specific to this API and key common parameters. More information can be found in [Common parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).

**Action ** string必选 `Example: DescribeCenRouteEntries`

Action to execute. Set the value to DescribeCenRouteEntries.

**Version ** string必选 `Example: 2020-04-01`

Current API version is 2020\-04\-01.

**PageNumber ** integer`optional` `Example: 1`

Page number of the list. Default: 1.

**PageSize ** integer`optional` `Example: 20`

The number of entries per page in a pagination query. Value range: 1–100. Default: 20.

**InstanceType ** string`optional` `Example: VPC`

Next hop type of the route entry. Values:

* VPC: Virtual Private Cloud

* DCGW: Direct Connect Gateway

**InstanceRegionId ** string`optional` `Example: cn-beijing`

Next hop region ID of the route entry.

**DestinationCidrBlock ** string`optional` `Example: 172.XX.XX.0/24`

The destination CIDR block of the route.

**InstanceId ** string`optional` `Example: vpc-2fexiqjlgjif45oxruvso****`

Next hop network instance ID of the route entry.

**CenId ** string`optional` `Example: cen-7qthudw0ll6jmc****`

The ID of the CEN.

## Response parameters

The following only details response parameters specific to this API. For more information, see Response structure.

**PageSize ** integer`Example: 20`

Page size.

**PageNumber ** integer`Example: 1`

Pagination page number.

**TotalCount ** integer`Example: 33`

Total number of route entries that meet the specified conditions.

**CenRouteEntries ** object[]`Example: --`

Details of the route entry.

**DestinationCidrBlock ** string`Example: 172.XX.XX.0/24`

The destination CIDR block of the route.

**InstanceType ** string`Example: VPC`

The next hop type of the route.

**InstanceRegionId ** string`Example: cn-beijing`

Next hop region ID of the route entry.

**Status ** string`Example: Available`

Effective status of the route entry.

* Available

* Pending: ​​Configuration in progress.

* Conflicted: Conflict detected.

**PublishStatus ** string`Example: Published`

Publish status of the route entry.

* Published

* Unpublished

**AsPath ** string[]`Example: 20314`

The AS path of the route.

**Type ** string`Example: System`

Type of CEN route.

* Custom: Indicates a route for accessing cloud services.

* System: Indicates a route learned from a network instance.

**CenId ** string`Example: cen-7qthudw0ll6jmc****`

The ID of the CEN.

**InstanceId ** string`Example: vpc-2fexiqjlgjif45oxruvso****`

Next hop network instance ID of the route entry.

**PageSize ** integer`Example: 20`

Page size.

**PageNumber ** integer`Example: 1`

Pagination page number.

**TotalCount ** integer`Example: 33`

Total number of route entries that meet the specified conditions.

**CenRouteEntries ** object[]`Example: --`

Details of the route entry.

**DestinationCidrBlock ** string`Example: 172.XX.XX.0/24`

The destination CIDR block of the route.

**InstanceType ** string`Example: VPC`

The next hop type of the route.

**InstanceRegionId ** string`Example: cn-beijing`

Next hop region ID of the route entry.

**Status ** string`Example: Available`

Effective status of the route entry.

* Available

* Pending: ​​Configuration in progress.

* Conflicted: Conflict detected.

**PublishStatus ** string`Example: Published`

Publish status of the route entry.

* Published

* Unpublished

**AsPath ** string[]`Example: 20314`

The AS path of the route.

**Type ** string`Example: System`

Type of CEN route.

* Custom: Indicates a route for accessing cloud services.

* System: Indicates a route learned from a network instance.

**CenId ** string`Example: cen-7qthudw0ll6jmc****`

The ID of the CEN.

**InstanceId ** string`Example: vpc-2fexiqjlgjif45oxruvso****`

Next hop network instance ID of the route entry.

## Request examples

```text
GET /?Action=DescribeCenRouteEntries&Version=2020-04-01 HTTP/1.1
Host: cen.byteplusapi.com
X-Date: 20260109T082811Z
Authorization: HMAC-SHA256 Credential=Adfks******wekfwe/20260109/cn-beijing/cen/request, SignedHeaders=host;x-date, Signature=47a7d934ff7b37c03938******cd7b8278a40a1057690c401e92246a0e41085f


```

## Response examples

```json
{
  "ResponseMetadata": {
    "RequestId": "20250818110346010046179141CE4638",
    "Action": "DescribeCenRouteEntries",
    "Version": "2020-04-01",
    "Service": "cen",
    "Region": "cn-beijing"
  },
  "Result": {
    "PageSize": 20,
    "PageNumber": 1,
    "TotalCount": 33,
    "CenRouteEntries": [
      {
        "DestinationCidrBlock": "172.XX.XX.0/24",
        "InstanceType": "VPC",
        "InstanceRegionId": "cn-beijing",
        "Status": "Available",
        "PublishStatus": "Published",
        "AsPath": [
          "20314"
        ],
        "Type": "System",
        "CenId": "cen-7qthudw0ll6jmc****",
        "InstanceId": "vpc-2fexiqjlgjif45oxruvso****"
      }
    ]
  }
}
```

## Error codes

The table below describes the error codes for this API that are associated with business logic. For details, see [Common error codes](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-error-codes).

|Status code |Error codes |Error message |Notes |
|---|---|---|---|
|400 |InvalidParameter |A parameter specified in the request is not valid, is unsupported or cannot be used. |The request contains invalid or unsupported parameters. |
|400 |MissingParameter |The request is missing a required parameter. Ensure that you have supplied all the required parameters for the request. |This request does not contain required parameters. Ensure all required parameters are provided when initiating the request. |
|400 |InvalidPage.Malformed |The specified page is malformed. |The specified pagination parameter is invalid. |
|400 |LimitExceeded.ResourceIds |You've reached the limit of 100 resource IDs that can be specified in this request. |You have reached the maximum number of instances that you can query in a single request. |
|500 |InternalError |Request failed with internal server error. |Internal system error. |
