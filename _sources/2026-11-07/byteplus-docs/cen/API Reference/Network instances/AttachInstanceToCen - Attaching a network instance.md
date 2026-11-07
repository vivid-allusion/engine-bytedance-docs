---
title: "AttachInstanceToCen - Attaching a network instance"
product: "Cloud Enterprise Network"
product_code: "cen"
source: "https://docs.byteplus.com/en/docs/cen/AttachInstanceToCen"
---

Call the AttachInstanceToCen API to attach a network instance to a Cloud Enterprise Network (CEN) instance.

## Instructions

A single CEN instance can support attaching up to 10 network instances per region.

## Debug

[去调试](https://api.byteplus.com/api-explorer/?action=AttachInstanceToCen&groupName=%E7%BD%91%E7%BB%9C%E5%AE%9E%E4%BE%8B&serviceCode=cen&version=2020-04-01)

## Request parameters

The following only details request parameters specific to this API and key common parameters. More information can be found in [Common parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).

**Action ** string必选 `Example: AttachInstanceToCen`

Action to execute. Set the value to AttachInstanceToCen.

**Version ** string必选 `Example: 2020-04-01`

The API version. Value: 2020\-04\-01.

**InstanceType ** string必选 `Example: VPC`

Type of the network instance. Valid values:

* VPC: Virtual Private Cloud

* DCGW: Direct Connect Gateway

**InstanceRegionId ** string必选 `Example: cn-beijing`

The region where the network instance resides.

**InstanceOwnerId ** string`optional` `Example: 210000****`

The ID of the account to which the network instance belongs.

> **tip**

> This parameter needs to be configured when attaching a network instance from a different account. If this parameter is not specified, it defaults to the ID of the current account, i.e., the account ID to which the CEN instance belongs.

**InstanceId ** string必选 `Example: vpc-2fexiqjlgjif45oxruvso****`

The network instance ID.

**CenId ** string必选 `Example: cen-7qthudw0ll6jmc****`

The ID of the CEN.

## Response parameters

This API does not have specific response parameters. For more information, see [Response structure](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response).

## Request examples

```text
GET /?Action=AttachInstanceToCen&Version=2020-04-01&InstanceType=VPC&InstanceRegionId=cn-beijing&InstanceId=vpc-2fexiqjlgjif45oxruvso****&CenId=cen-7qthudw0ll6jmc**** HTTP/1.1
Host: cen.byteplusapi.com
X-Date: 20260109T084301Z
Authorization: HMAC-SHA256 Credential=Adfks******wekfwe/20260109/cn-beijing/cen/request, SignedHeaders=host;x-date, Signature=47a7d934ff7b37c03938******cd7b8278a40a1057690c401e92246a0e41085f


```

## Response examples

```json
{
  "ResponseMetadata": {
    "RequestId": "20250815165242151204065068D097F8",
    "Action": "AttachInstanceToCen",
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
|400 |InvalidCenAttachedInstance.Malformed |The specified instance type is malformed. |The specified network instance type is not supported. |
|400 |InvalidCenAttachedInstance.DcgwMismatch |The specified DCGW cannot be attached to CEN due to the lack of a virtual interface. |The specified Direct Connect Gateway lacks a virtual interface and cannot be associated with the CEN instance. |
|400 |QuotaExceeded.CenAttachedInstance |You've reached the number of instances can be attached to CEN in one region. |The maximum number of network instances that can be attached to the CEN instance in this region has been reached. |
|400 |InvalidCenRouteEntry.AsNumberMalformed |The specified AS is malformed. Ensure the maximum value of AS is 4294960000. |The specified AS number is invalid. The AS number cannot exceed 4294960000. |
|400 |InvalidCenAttachedInstance.InvalidStatus |The specified instance is not in the correct status for the request. |The specified network instance is in a status that cannot respond to the request. |
|400 |InvalidCenRouteEntry.AsPathMalformed |The specified AsPath is malformed. |The specified AsPath attribute is invalid. |
|400 |InvalidCenAttachedInstance.DcgwInvalidStatus |Specified direct connect gateway has been frozen. |The specified Direct Connect Gateway is frozen. |
|400 |InvalidCenAttachedInstance.CannotUpdate |Failed to update the specified attached instance, please try again later. |Failed to update the specified network instance. Please try again later. |
|400 |InvalidCenAttachedInstance.RegionTypeConflictsWithAttachedInstance |The region type of specified instance conflicts with attached instances. |The region type of the specified instance conflicts with the regions of already attached network instances. |
|400 |InvalidCenAttachedInstance.RegionTypeMissMatchInterRegionBandwidth |The region type of specified instance does not match with inter\-region bandwidths. |The region type of the specified instance does not match the regions for inter\-region bandwidth allocation. |
|400 |InvalidInstance.Isolated |The specified instance is abnormal and has been isolated. |The specified resource has been isolated due to an exception. Please try again later. |
|400 |InvalidInstanceOwnerId.OperationFailed |The specified operation has failed. Please submit a ticket or contact your account manager. |The specified operation failed. Please submit a ticket or contact your account manager. |
|404 |InvalidDcgwId.NotFound |The specified DCGW ID does not exist in this region. |The specified DC Gateway does not exist in the specified region. |
|404 |InvalidVpcId.NotFound |The specified VPC ID does not exist in this region. |The specified VPC does not exist in the specified region. |
|404 |InvalidCenRegion.NotFound |The specified region does not exist. |The specified region does not exist. |
|404 |InvalidCrossAccountInstance.NotFound |The specified instance has not been granted. |The specified network instance has not been authorized. |
|404 |InvalidCen.NotFound |The specified CEN does not exist. |The specified CEN instance does not exist. |
|409 |InvalidCen.InvalidStatus |The specified CEN instance is not in the correct status for the request. |The specified CEN instance is in a state that cannot process the request. Please try again later. |
|409 |InvalidCenAttachedInstance.Conflict |The specified instance has already been attached to CEN. |The specified network instance has been attached to the CEN instance. |
|409 |InvalidCenAttachedInstance.Conflict |The specified instance has already been attached to Transit Router. |The specified network instance has already been attached to a transit router. |
|500 |InternalError |Request failed with internal server error. |Internal system error. |
