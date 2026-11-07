---
title: "DeleteCen - Deleting a CEN instance"
product: "Cloud Enterprise Network"
product_code: "cen"
source: "https://docs.byteplus.com/en/docs/cen/DeleteCen"
---

Call the DeleteCen API to delete the specified Cloud Enterprise Network (CEN) instance.

## Instructions

* The CEN instance has not attached a network instance.

   You can call the [DescribeCenAttachedInstances](https://docs.byteplus.com/en/docs/cen/DescribeCenAttachedInstanceAttributes) API to check if the CEN instance has attached network instances. If attached, call the [DetachInstanceFromCen](https://docs.byteplus.com/en/docs/cen/DetachInstanceFromCen) API to detach them.

* The CEN instance has not bound a bandwidth package.

   You can call the [DescribeCenBandwidthPackages](https://docs.byteplus.com/en/docs/cen/DescribeCenBandwidthPackages) API to check if the CEN instance has associated bandwidth packages. If associated, call the [DisassociateCenBandwidthPackage](https://docs.byteplus.com/en/docs/cen/DisassociateCenBandwidthPackage) API to detach.

## Debug

[去调试](https://api.byteplus.com/api-explorer/?action=DeleteCen&groupName=%E4%BA%91%E4%BC%81%E4%B8%9A%E7%BD%91%E5%AE%9E%E4%BE%8B&serviceCode=cen&version=2020-04-01)

## Request parameters

The following only details request parameters specific to this API and key common parameters. More information can be found in [Common parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).

**Action ** string必选 `Example: DeleteCen`

Action to execute. Set the value to DeleteCen.

**Version ** string必选 `Example: 2020-04-01`

The API version. Value: 2020\-04\-01.

**CenId ** string必选 `Example: cen-7qthudw0ll6jmc****`

ID of the CEN instance to be deleted.

You can call the [DescribeCens](https://docs.byteplus.com/en/docs/cen/DescribeCens) API to query the CEN instance ID.

## Response parameters

This API does not have specific response parameters. For more information, see [Response structure](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response).

## Request examples

```text
GET /?Action=DeleteCen&Version=2020-04-01&CenId=cen-7qthudw0ll6jmc**** HTTP/1.1
Host: cen.byteplusapi.com
X-Date: 20260109T085944Z
Authorization: HMAC-SHA256 Credential=Adfks******wekfwe/20260109/cn-beijing/cen/request, SignedHeaders=host;x-date, Signature=47a7d934ff7b37c03938******cd7b8278a40a1057690c401e92246a0e41085f


```

## Response examples

```json
{
  "ResponseMetadata": {
    "RequestId": "202508151644221640941710374624B8",
    "Action": "DeleteCen",
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
|400 |InvalidCen.InUse |The specified CEN has attached instances and cannot be deleted. |The specified CEN instance has attached network instances and cannot be deleted. |
|400 |InvalidCen.InUse |The specified CEN still has a bandwidth package and cannot be deleted. |The specified CEN instance has a bandwidth package bound and cannot be deleted. |
|400 |InvalidCen.InUse |The specified CEN has created summary route and cannot be deleted. |The specified CEN instance has created summary routes and cannot be deleted. |
|404 |InvalidCen.NotFound |The specified CEN does not exist. |The specified CEN instance does not exist. |
|409 |InvalidCen.InvalidStatus |The specified CEN instance is not in the correct status for the request. |The specified CEN instance is in a state that cannot process the request. Please try again later. |
|500 |InternalError |Request failed with internal server error. |Internal system error. |
