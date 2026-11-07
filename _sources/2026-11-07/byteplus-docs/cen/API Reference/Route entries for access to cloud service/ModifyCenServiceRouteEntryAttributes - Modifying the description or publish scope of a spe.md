---
title: "ModifyCenServiceRouteEntryAttributes - Modifying the description or publish scope of a specified service access route"
product: "Cloud Enterprise Network"
product_code: "cen"
source: "https://docs.byteplus.com/en/docs/cen/ModifyCenServiceRouteEntryAttributes"
---

Call the ModifyCenServiceRouteEntryAttributes API to modify the description or publish scope of a specified cloud service route entry.

## Instructions

In the table below, for the "PublishToInstances.N.a" type parameter, "N" represents the serial number of the cloud service route entry publish information. It must be filled in sequential numeric order starting from 1, with a maximum of 100 per API call. Separate multiple pieces of publish information for cloud service route entries with an ampersand (&).

## Debug

[去调试](https://api.byteplus.com/api-explorer/?action=ModifyCenServiceRouteEntryAttributes&groupName=%E4%BA%91%E6%9C%8D%E5%8A%A1%E8%AE%BF%E9%97%AE&serviceCode=cen&version=2020-04-01)

## Request parameters

The following only details request parameters specific to this API and key common parameters. More information can be found in [Common parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).

**Action ** string必选 `Example: ModifyCenServiceRouteEntryAttributes`

Action to execute. Set the value to ModifyCenServiceRouteEntryAttributes.

**Version ** string必选 `Example: 2020-04-01`

The API version. Value: 2020\-04\-01.

**CenId ** string必选 `Example: cen-2nim00ybaylts7trquyzt****`

The CEN instance ID.

You can call the [DescribeCens](https://docs.byteplus.com/en/docs/cen/DescribeCens) API to get the CEN instance ID.

**DestinationCidrBlock ** string必选 `Example: 100.XX.XX.0/24`

The address where the cloud service is deployed. It must belong to the `100.64.0.0/10` or `fd00:64::/32` CIDR block.

**ServiceRegionId ** string必选 `Example: cn-beijing`

The Region of cloud service.

**Description ** string`optional` `Example: test-service-route`

The description of cloud service access.

* Must start with a letter, number, or Chinese character. May include letters, numbers, Chinese characters, and the following symbols: commas (,), periods (.), underscores (_), spaces ( ), equal signs (=), hyphens (\-), full\-width commas ( ， ), and full\-width periods ( 。 ).

* Must be 0 to 255 characters.

* If you do not provide this parameter or leave it unset, it defaults to an empty string.

**PublishMode ** string`optional` `Example: LocalDCGW`

Publish scope of the cloud service route.

* LocalDCGW: Indicates that the cloud service route entry is automatically published to all Direct Connect Gateways in the region where the cloud service is deployed that are attached to the CEN instance.

* Custom: Indicates that you manually specify the network instances to which the cloud service route entry needs to be published.

**PublishToInstances.N.InstanceRegionId ** string[]`optional` `Example: cn-guangzhou`

The region to which the cloud service route needs to be published.

For supported regions of the CEN service, see Areas and Regions.

**PublishToInstances.N.InstanceType ** string[]`optional` `Example: VPC`

The type of network instance to which the cloud service route entry needs to be published. Values:

* VPC: Virtual Private Cloud.

* DCGW: Direct Connect Gateway.

**PublishToInstances.N.InstanceId ** string[]`optional` `Example: vpc-7qthudw0ll6jmc****`

The ID of the network instance to which the cloud service route entry needs to be published.

* You can call the [DescribeVpcs](https://docs.byteplus.com/en/docs/vpc/DescribeVpcs) API to obtain the ID of a network instance of the "VPC" type.

* You can call the [DescribeDirectConnectGateways](https://docs.byteplus.com/en/docs/directconnect/DescribeDirectConnectGateways) API to obtain the ID of a network instance of the "DCGW" type.

## Response parameters

This API does not have specific response parameters. For more information, see [Response structure](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response).

## Request examples

```text
GET /?Action=ModifyCenServiceRouteEntryAttributes&Version=2020-04-01&CenId=cen-2nim00ybaylts7trquyzt****&DestinationCidrBlock=100.XX.XX.0%2F24&ServiceRegionId=cn-beijing HTTP/1.1
Host: cen.byteplusapi.com
X-Date: 20260109T082526Z
Authorization: HMAC-SHA256 Credential=Adfks******wekfwe/20260109/cn-beijing/cen/request, SignedHeaders=host;x-date, Signature=47a7d934ff7b37c03938******cd7b8278a40a1057690c401e92246a0e41085f


```

## Response examples

```json
{
  "ResponseMetadata": {
    "RequestId": "20250815163500024047166055C7DCB8",
    "Action": "ModifyCenServiceRouteEntryAttributes",
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
|400 |InvalidServiceRoute.PublishInstanceDuplicated |The specified publish instance is specified more than once in the request. |The specified publish instance is duplicated. |
|400 |InvalidDescription.Malformed |The specified description is malformed. |The specified description format is invalid. Correct the description format and retry. |
|400 |InvalidDescription.Malformed |The specified description is malformed. Ensure the maximum length of description is 255. |The specified description format is invalid. A description must not exceed 255 characters. |
|400 |InvalidServiceRoute.Existed |The specified service route already exists. |The specified cloud service route entry already exists. |
|403 |Forbidden.CreateServiceRoute |You are not authorized to perform operations on the service route. |You are not authorized to operate on the specified resource. Please apply for the allowlist for cloud service access. |
|403 |Forbidden.PublishToSameRegionVpcInstance |You are not authorized to publish the service route to same region vpc instance. |You are not authorized to publish the cloud service route to a VPC instance in the same region. Please apply for the relevant allowlist. |
|404 |InvalidServiceRouteEntry.NotFound |The specified service route entry does not exist. |The specified cloud service route entry does not exist. |
|404 |InvalidServiceRoute.PublishInstanceNotFound |The specified publish instance does not exist. |The specified publish instance does not exist. |
|409 |InvalidCen.InvalidStatus |The specified CEN instance is not in the correct status for the request. |The specified CEN instance is in a state that cannot process the request. Please try again later. |
|409 |InvalidServiceRouteEntry.InvalidStatus |The specified CEN service route is not in the correct status for the request. |The specified Cloud Service Route is in a state that cannot respond to this request. Please try again later. |
|409 |InvalidServiceRoute.Conflict |There is conflict between the specified service route and existed routes. |The specified cloud service route conflicts with an existing route in the CEN route table. |
|500 |InternalError |Request failed with internal server error. |Internal system error. |
