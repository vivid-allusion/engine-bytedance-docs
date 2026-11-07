---
title: "DescribeCenAttachedInstances - Querying the network instance list"
product: "Cloud Enterprise Network"
product_code: "cen"
source: "https://docs.byteplus.com/en/docs/cen/DescribeCenAttachedInstances"
---

Call the DescribeCenAttachedInstances API to query network instances that meet the specified conditions.

## Debug

[去调试](https://api.byteplus.com/api-explorer/?action=DescribeCenAttachedInstances&groupName=%E7%BD%91%E7%BB%9C%E5%AE%9E%E4%BE%8B&serviceCode=cen&version=2020-04-01)

## Request parameters

The following only details request parameters specific to this API and key common parameters. More information can be found in [Common parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).

**Action ** string必选 `Example: DescribeCenAttachedInstances`

Action to execute. Set the value to DescribeCenAttachedInstances.

**Version ** string必选 `Example: 2020-04-01`

The API version. Value: 2020\-04\-01.

**InstanceType ** string`optional` `Example: VPC`

Type of the network instance. Valid values:

* VPC: Virtual Private Cloud

* DCGW: Direct Connect Gateway

**InstanceRegionId ** string`optional` `Example: cn-beijing`

Region to which the network instance belongs.

**PageNumber ** integer`optional` `Example: 1`

Page number of the list. Default: 1.

**PageSize ** integer`optional` `Example: 20`

The number of entries per page in a pagination query. Value range: 1–100. Default: 20.

**InstanceId ** string`optional` `Example: vpc-2fexiqjlgjif45oxruvso****`

The network instance ID.

* You can call the [DescribeVpcs](https://docs.byteplus.com/en/docs/vpc/DescribeVpcs) API to query the ID of a network instance of the "VPC" type.

* You can call the [DescribeDirectConnectGateways](https://docs.byteplus.com/en/docs/directconnect/DescribeDirectConnectGateways) to query the ID of a network instance of the "DCGW" type.

**CenId ** string`optional` `Example: cen-7qthudw0ll6jmc****`

The ID of the CEN.

## Response parameters

The following only details response parameters specific to this API. For more information, see [Response structure](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response).

**TotalCount ** integer`Example: 10`

The total number of network instances that meet the specified conditions.

**PageNumber ** integer`Example: 1`

The current page number.

**PageSize ** integer`Example: 20`

Number of entries per page in the current pagination.

**AttachedInstances ** object[]`Example: -`

Details of the network instance.

**InstanceType ** string`Example: VPC`

The network instance type.

**InstanceRegionId ** string`Example: cn-beijing`

The region where the network instance resides.

**Status ** string`Example: Available`

Loading status of the network instance.

* Attaching

* Available

**CreationTime ** string`Example: 2021-01-28T14:55:11+08:00`

Creation time of the network instance.

**CenId ** string`Example: cen-7qthudw0ll6jmc****`

The CEN instance ID.

**InstanceId ** string`Example: vpc-2fexiqjlgjif45oxruvso****`

The network instance ID.

**InstanceOwnerId ** string`Example: 210000****`

The ID of the account to which the network instance belongs.

**TotalCount ** integer`Example: 10`

The total number of network instances that meet the specified conditions.

**PageNumber ** integer`Example: 1`

The current page number.

**PageSize ** integer`Example: 20`

Number of entries per page in the current pagination.

**AttachedInstances ** object[]`Example: -`

Details of the network instance.

**InstanceType ** string`Example: VPC`

The network instance type.

**InstanceRegionId ** string`Example: cn-beijing`

The region where the network instance resides.

**Status ** string`Example: Available`

Loading status of the network instance.

* Attaching

* Available

**CreationTime ** string`Example: 2021-01-28T14:55:11+08:00`

Creation time of the network instance.

**CenId ** string`Example: cen-7qthudw0ll6jmc****`

The CEN instance ID.

**InstanceId ** string`Example: vpc-2fexiqjlgjif45oxruvso****`

The network instance ID.

**InstanceOwnerId ** string`Example: 210000****`

The ID of the account to which the network instance belongs.

## Request examples

```text
GET /?Action=DescribeCenAttachedInstances&Version=2020-04-01 HTTP/1.1
Host: cen.byteplusapi.com
X-Date: 20260109T084147Z
Authorization: HMAC-SHA256 Credential=Adfks******wekfwe/20260109/cn-beijing/cen/request, SignedHeaders=host;x-date, Signature=47a7d934ff7b37c03938******cd7b8278a40a1057690c401e92246a0e41085f


```

## Response examples

```json
{
  "ResponseMetadata": {
    "RequestId": "20250815165535000237144252168618",
    "Action": "DescribeCenAttachedInstances",
    "Version": "2020-04-01",
    "Service": "cen",
    "Region": "cn-beijing"
  },
  "Result": {
    "TotalCount": 10,
    "PageNumber": 1,
    "PageSize": 20,
    "AttachedInstances": [
      {
        "InstanceType": "VPC",
        "InstanceRegionId": "cn-beijing",
        "Status": "Available",
        "CreationTime": "2021-01-28T14:55:11+08:00",
        "CenId": "cen-7qthudw0ll6jmc****",
        "InstanceId": "vpc-2fexiqjlgjif45oxruvso****",
        "InstanceOwnerId": "210000****"
      }
    ]
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
|500 |InternalError |Request failed with internal server error. |Internal system error. |
