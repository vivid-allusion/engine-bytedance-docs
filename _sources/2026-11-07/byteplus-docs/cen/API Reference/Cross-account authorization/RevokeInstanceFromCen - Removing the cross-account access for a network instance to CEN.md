---
title: "RevokeInstanceFromCen - Removing the cross-account access for a network instance to CEN"
product: "Cloud Enterprise Network"
product_code: "cen"
source: "https://docs.byteplus.com/en/docs/cen/RevokeInstanceFromCen"
---

Call the RevokeInstanceFromCen API to remove the authorization relationship between a network instance under the current account and a CEN instance under a specified account.

## Debug

[去调试](https://api.byteplus.com/api-explorer/?action=RevokeInstanceFromCen&groupName=%E8%B7%A8%E8%B4%A6%E5%8F%B7%E6%8E%88%E6%9D%83&serviceCode=cen&version=2020-04-01)

## Request parameters

The following only details request parameters specific to this API and key common parameters. More information can be found in [Common parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).

**Action ** string必选 `Example: RevokeInstanceFromCen`

Action to execute. Set the value to RevokeInstanceFromCen.

**Version ** string必选 `Example: 2020-04-01`

The API version. Value: 2020\-04\-01.

**CenId ** string必选 `Example: cen-7qthudw0ll6jmc****`

The ID of the CEN instance of the other account.

You can call the [DescribeCens](https://docs.byteplus.com/en/docs/cen/DescribeCens) API to query the CEN instance ID.

**CenOwnerId ** string必选 `Example: 210000****`

Peer account.

You can call the [DescribeCens](https://docs.byteplus.com/en/docs/cen/DescribeCens) API to query the account ID.

**InstanceId ** string必选 `Example: vpc-uf6o8d1dj8sjwxi6o****`

The ID of the network instance for which authorization is to be removed.

**InstanceType ** string必选 `Example: VPC`

The network instance type. Valid values:

* VPC: Virtual Private Cloud.

* DCGW: Direct Connect Gateway.

**InstanceRegionId ** string必选 `Example: cn-beijing`

The region where the network instance resides.

## Response parameters

This API does not have specific response parameters. For more information, see [Response structure](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response).

## Request examples

```text
GET /?Action=RevokeInstanceFromCen&Version=2020-04-01&CenId=cen-7qthudw0ll6jmc****&CenOwnerId=210000****&InstanceId=vpc-uf6o8d1dj8sjwxi6o****&InstanceType=VPC&InstanceRegionId=cn-beijing HTTP/1.1
Host: cen.byteplusapi.com
X-Date: 20260109T083818Z
Authorization: HMAC-SHA256 Credential=Adfks******wekfwe/20260109/cn-beijing/cen/request, SignedHeaders=host;x-date, Signature=47a7d934ff7b37c03938******cd7b8278a40a1057690c401e92246a0e41085f


```

## Response examples

```json
{
  "ResponseMetadata": {
    "RequestId": "202508151732202270370310693FF0F9",
    "Action": "RevokeInstanceFromCen",
    "Version": "2020-04-01",
    "Service": "cen",
    "Region": "cn-beijing"
  },
  "Result": {}
}
```

## Error codes

The table below describes the error codes for this API that are associated with business logic. For details, see [Common error codes](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-error-codes).

|Status code |Error codes |Error message |Notes |
|---|---|---|---|
|400 |MissingParameter |The request is missing a required parameter. Ensure that you have supplied all the required parameters for the request. |This request does not contain required parameters. Ensure all required parameters are provided when initiating the request. |
|400 |InvalidParameter |A parameter specified in the request is not valid, is unsupported or cannot be used. |The request contains invalid or unsupported parameters. |
|404 |InvalidCen.NotFound |The specified CEN does not exist. |The specified CEN instance does not exist. |
|404 |InvalidGrantInstance.NotFound |The specified instance has not been granted. |The specified network instance has not been authorized. |
|409 |InvalidCen.InvalidStatus |The specified CEN instance is not in the correct status for the request. |The specified CEN instance is in a state that cannot process the request. Please try again later. |
|409 |InvalidCenAttachedInstance.Conflict |The specified instance has already been attached to CEN. |The specified network instance has been attached to the CEN instance. |
|500 |InternalError |Request failed with internal server error. |Internal system error. |
