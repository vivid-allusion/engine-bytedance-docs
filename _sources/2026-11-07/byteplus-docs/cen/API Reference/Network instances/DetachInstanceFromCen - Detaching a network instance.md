---
title: "DetachInstanceFromCen - Detaching a network instance"
product: "Cloud Enterprise Network"
product_code: "cen"
source: "https://docs.byteplus.com/en/docs/cen/DetachInstanceFromCen"
---

Call the DetachInstanceFromCen API to detach the network instance from a Cloud Enterprise Network (CEN) instance.

## Debug

[去调试](https://api.byteplus.com/api-explorer/?action=DetachInstanceFromCen&groupName=%E7%BD%91%E7%BB%9C%E5%AE%9E%E4%BE%8B&serviceCode=cen&version=2020-04-01)

## Request parameters

The following only details request parameters specific to this API and key common parameters. More information can be found in [Common parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).

**Action ** string必选 `Example: DetachInstanceFromCen`

Action to execute. Set the value to DetachInstanceFromCen.

**Version ** string必选 `Example: 2020-04-01`

The API version. Value: 2020\-04\-01.

**InstanceType ** string必选 `Example: VPC`

Type of the network instance. Valid values:

* VPC: Virtual Private Cloud

* DCGW: Direct Connect Gateway

**InstanceRegionId ** string必选 `Example: cn-beijing`

The region where the network instance resides.

**InstanceId ** string必选 `Example: vpc-2fexiqjlgjif45oxruvso****`

The network instance ID.

* You can call the [DescribeVpcs](https://docs.byteplus.com/en/docs/vpc/DescribeVpcs) API query the ID of a network instance of the "VPC" type.

* You can call the [DescribeDirectConnectGateways](https://docs.byteplus.com/en/docs/directconnect/DescribeDirectConnectGateways) API to query the ID of a network instance of the "DCGW" type.

**CenId ** string必选 `Example: cen-7qthudw0ll6jmc****`

The CEN instance ID.

You can call the [DescribeCens](https://docs.byteplus.com/en/docs/cen/DescribeCens) API to query the CEN instance ID.

## Response parameters

This API does not have specific response parameters. For more information, see [Response structure](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response).

## Request examples

```text
GET /?Action=DetachInstanceFromCen&Version=2020-04-01&InstanceType=VPC&InstanceRegionId=cn-beijing&InstanceId=vpc-2fexiqjlgjif45oxruvso****&CenId=cen-7qthudw0ll6jmc**** HTTP/1.1
Host: cen.byteplusapi.com
X-Date: 20260109T084333Z
Authorization: HMAC-SHA256 Credential=Adfks******wekfwe/20260109/cn-beijing/cen/request, SignedHeaders=host;x-date, Signature=47a7d934ff7b37c03938******cd7b8278a40a1057690c401e92246a0e41085f


```

## Response examples

```json
{
  "ResponseMetadata": {
    "RequestId": "20250815165121108141133252C32212",
    "Action": "DetachInstanceFromCen",
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
|400 |InvalidCenAttachedInstance.CannotUpdate |Failed to update the specified attached instance, please try again later. |Failed to update the specified network instance. Please try again later. |
|400 |InvalidCenAttachedInstance.Malformed |The specified instance type is malformed. |The specified network instance type is not supported. |
|400 |InvalidCenAttachedInstance.DcgwInvalidStatus |Specified direct connect gateway has been frozen. |The specified Direct Connect Gateway is frozen. |
|400 |InvalidCenAttachedInstance.InvalidStatus |The specified instance is not in the correct status for the request. |The specified network instance is in a status that cannot respond to the request. |
|400 |InvalidCenAttachedInstance.DcgwMismatch |The specified DCGW cannot be attached to CEN due to the lack of a virtual interface. |The specified Direct Connect Gateway lacks a virtual interface and cannot be associated with the CEN instance. |
|400 |InvalidCenAttachedInstance.InUse |The specified CEN attached instance is in use. |The specified network instance is currently in use. |
|400 |InvalidCenAttachedInstance.HasVpcCustomRouteEntry |The specified CEN attached instance has published VPC custom route entry and cannot be detached. |The specified network instance cannot be detached because it has published custom routes from the VPC. |
|400 |InvalidCenAttachedInstance.HasServiceRouteEntry |The specified CEN attached instance has configured service route entry and cannot be detached. |The specified network instance cannot be detached because it has configured cloud service routes. |
|400 |InvalidInstance.Isolated |The specified instance is abnormal and has been isolated. |The specified resource has been isolated due to an exception. Please try again later. |
|404 |InvalidVpcId.NotFound |The specified VPC ID does not exist in this region. |The specified VPC does not exist in the specified region. |
|404 |InvalidDcgwId.NotFound |The specified DCGW ID does not exist in this region. |The specified DC Gateway does not exist in the specified region. |
|404 |InvalidCenAttachedInstance.NotFound |The specified CEN attached instance does not exist. |The specified network instance does not exist. |
|404 |InvalidCenAttachedInstance.NotMatch |The specified instance has not attached to the given CEN. |The specified network instance is not attached to this CEN instance. |
|409 |InvalidCen.InvalidStatus |The specified CEN instance is not in the correct status for the request. |The specified CEN instance is in a state that cannot process the request. Please try again later. |
|500 |InternalError |Request failed with internal server error. |Internal system error. |
