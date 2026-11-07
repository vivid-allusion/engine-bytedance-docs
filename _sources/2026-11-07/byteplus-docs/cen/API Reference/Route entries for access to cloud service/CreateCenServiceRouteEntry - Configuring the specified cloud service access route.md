---
title: "CreateCenServiceRouteEntry - Configuring the specified cloud service access route"
product: "Cloud Enterprise Network"
product_code: "cen"
source: "https://docs.byteplus.com/en/docs/cen/CreateCenServiceRouteEntry"
---

Call the CreateCenServiceRouteEntry API to configure the specified cloud service access route.

## Instructions

The custom cloud service access route publish scope feature is in Beta stage. For trial requests, please contact your account manager.

## Debug

[去调试](https://api.byteplus.com/api-explorer/?action=CreateCenServiceRouteEntry&groupName=%E4%BA%91%E6%9C%8D%E5%8A%A1%E8%AE%BF%E9%97%AE&serviceCode=cen&version=2020-04-01)

## Request parameters

The following only details request parameters specific to this API and key common parameters. More information can be found in [Common parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).

**Action ** string必选 `Example:  CreateCenServiceRouteEntry`

Action to execute. Set the value to CreateCenServiceRouteEntry.

**Version ** string必选 `Example: 2020-04-01`

The API version. Value: 2020\-04\-01.

**CenId ** string必选 `Example: cen-2nim00ybaylts7trquyzt****`

The CEN instance ID.

You can call the [DescribeCens](https://docs.byteplus.com/en/docs/cen/DescribeCens) API to query the CEN instance ID.

**DestinationCidrBlock ** string必选`Example: 100.XX.XX.0/24`

The address where the cloud service is deployed. It must belong to the `100.64.0.0/10` or `fd00:64::/32` CIDR block.

**ServiceRegionId ** string必选 `Example: cn-beijing`

The region of cloud service.

**ServiceVpcId ** string必选 `Example: vpc-3rlkeggyn6tc010exd32q****`

VPC instance ID used to access the cloud service.

You can call the [DescribeVpcs](https://docs.byteplus.com/en/docs/vpc/DescribeVpcs) API to obtain the VPC instance ID.

**Description ** string`optional` `Example: test-service-route`

The description of cloud service access.

* Must start with a letter, number, or Chinese character. May include letters, numbers, Chinese characters, and the following symbols: commas (,), periods (.), underscores (_), spaces ( ), equal signs (=), hyphens (\-), full\-width commas ( ， ), and full\-width periods ( 。 ).

* Must be 0 to 255 characters.

* If left blank, it defaults to an empty string.

**PublishMode ** string`optional` `Example: LocalDCGW`

Publish scope of cloud service route entry.

* LocalDCGW (default): Indicates that the cloud service route entry is automatically published to all Direct Connect Gateways in the region where the cloud service is deployed that are attached to the CEN instance.

* Custom: Indicates that you manually specify the network instances to which the cloud service route entry needs to be published.

**PublishToInstances.N.InstanceRegionId ** string[]`optional` `Example: cn-guangzhou`

Region to which the cloud service route entry is published.

* This parameter is valid and required only when the `PublishMode` parameter is set to Custom.

* For supported regions of the CEN, see [Areas and Regions](https://docs.byteplus.com/en/docs/cen/Product-Overview-05).

**PublishToInstances.N.InstanceType ** string[]`optional` `Example: VPC`

The type of network instance to which the cloud service route entry needs to be published.

This parameter is valid and required only when the `PublishMode` parameter is set to Custom. Valid values:

* VPC: Virtual Private Cloud.

* DCGW: Direct Connect Gateway.

**PublishToInstances.N.InstanceId ** string[]`optional` `Example: vpc-7qthudw0ll6jmc****`

The ID of the network instance to which the cloud service route entry needs to be published.

* This parameter is valid and required only when the `PublishMode` parameter is set to Custom.

* You can call the [DescribeVpcs](https://docs.byteplus.com/en/docs/vpc/DescribeVpcs) API to query the ID of a network instance of the "VPC" type.

* You can call the [DescribeDirectConnectGateways](https://docs.byteplus.com/en/docs/directconnect/DescribeDirectConnectGateways) API to query the ID of a network instance of the "DCGW" type.

## Response parameters

This API does not have specific response parameters. For more information, see [Response structure](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response).

## Request examples

```text
GET /?Action=CreateCenServiceRouteEntry&Version=2020-04-01&CenId=cen-2nim00ybaylts7trquyzt****&DestinationCidrBlock=100.XX.XX.0%2F24&ServiceRegionId=cn-beijing&ServiceVpcId=vpc-3rlkeggyn6tc010exd32q**** HTTP/1.1
Host: cen.byteplusapi.com
X-Date: 20260109T082627Z
Authorization: HMAC-SHA256 Credential=Adfks******wekfwe/20260109/cn-beijing/cen/request, SignedHeaders=host;x-date, Signature=47a7d934ff7b37c03938******cd7b8278a40a1057690c401e92246a0e41085f


```

## Response examples

```json
{
  "ResponseMetadata": {
    "RequestId": "20250815163416072183002255BDFC28",
    "Action": "CreateCenServiceRouteEntry",
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
|400 |InvalidCidr.Malformed |The specified cidr block is malformed. |The format of the specified CIDR block is invalid. |
|400 |InvalidServiceRoute.Malformed |The specified destination cidr block is malformed. |The destination CIDR block of the specified cloud service route entry is not within 100.64.0.0/10 or fd00:64::/32. |
|400 |InvalidServiceRoute.Existed |The specified service route already exists. |The specified cloud service route entry already exists. |
|400 |QuotaExceeded.CenRouteEntry |You've reached the number of route entries can be published to CEN. |The quota limit for the number of CEN route entries has been reached. |
|400 |InvalidServiceRoute.PublishInstanceDuplicated |The specified publish instance is specified more than once in the request. |The specified publish instance is duplicated. |
|400 |InvalidDescription.Malformed |The specified description is malformed. |The specified description format is invalid. Correct the description format and retry. |
|400 |InvalidDescription.Malformed |The specified description is malformed. Ensure the maximum length of description is 255. |The specified description format is invalid. A description must not exceed 255 characters. |
|403 |Forbidden.PublishIPv6CenRouteEntry |You are not authorized to publish IPv6 route entry to CEN. |No permission to publish the specified IPv6 route. |
|403 |Forbidden.PublishToSameRegionVpcInstance |You are not authorized to publish the service route to same region vpc instance. |You are not authorized to publish the cloud service route to a VPC instance in the same region. Please apply for the relevant allowlist. |
|404 |InvalidServiceRoute.PublishInstanceNotFound |The specified publish instance does not exist. |The specified publish instance does not exist. |
|404 |InvalidCen.NotFound |The specified CEN does not exist. |The specified CEN instance does not exist. |
|404 |InvalidCenAttachedInstance.NotFound |The specified CEN attached instance does not exist. |The specified network instance does not exist. |
|409 |InvalidCen.InvalidStatus |The specified CEN instance is not in the correct status for the request. |The specified CEN instance is in a state that cannot process the request. Please try again later. |
|409 |InvalidServiceRoute.Conflict |There is conflict between the specified service route and existed routes. |The specified cloud service route conflicts with an existing route in the CEN route table. |
|500 |InternalError |Request failed with internal server error. |Internal system error. |
