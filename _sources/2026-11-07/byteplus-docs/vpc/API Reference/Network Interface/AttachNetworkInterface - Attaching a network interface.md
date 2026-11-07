---
title: "AttachNetworkInterface - Attaching a network interface"
product: "Virtual Private Cloud"
product_code: "vpc"
source: "https://docs.byteplus.com/en/docs/vpc/AttachNetworkInterface"
---

Call the AttachNetworkInterface API to attach a secondary network interface (ENI) to an Elastic Compute Service (ECS) instance.

## Instructions

Prerequisites for calling this API:

* The ECS instance and the secondary ENI must reside in the same VPC and the same Availability Zone.

* The ECS instance status is **Running** or **Stopped**.

* The number of assigned private IPv4 addresses and private IPv6 addresses on the secondary network interface must be within the per\-network interface IP quota supported by the instance type.

* The target ECS instance has not reached its maximum number of attachable ENIs (which includes 1 primary ENI). The maximum number of ENIs that can be attached varies by ECS instance type. For details, see [instance type list](https://docs.byteplus.com/en/docs/ecs/General-purpose).

* AttachNetworkInterface is an asynchronous API. When a request ID is returned, the system is still configuring in the background. You can call [DescribeNetworkInterfaceAttributes](https://docs.byteplus.com/en/docs/vpc/DescribeRouteEntryList) to check the status of the ENI. `Attaching` means attaching, and `InUse` means attached.

## Debug

[去调试](https://api.byteplus.com/api-explorer/debug?action=AttachNetworkInterface&serviceCode=vpc&version=2020-04-01&groupName=)

## Request parameters

The table below lists only the request parameters unique to this interface and some common parameters. For more information, see [Common parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).

**Action ** String必选 `Example: AttachNetworkInterface`

The API name. The current API name is `AttachNetworkInterface`.

**Version ** String必选 `Example: 2020-04-01`

The API version. The current API version is `2020-04-01`.

**NetworkInterfaceId ** String必选 `Example: eni-bp1fg655nh68xyz9****`

Secondary ENI ID.

You can call the [DescribeNetworkInterfaces](https://docs.byteplus.com/en/docs/vpc/DescribeNetworkInterfaces) API to query the ENI ID.

**InstanceId ** String必选 `Example: i-wijfn35c****`

ID of the ECS instance.

You can call the [DescribeInstances](https://docs.byteplus.com/en/docs/ecs/DescribeInstances) API to query the IDs of ECS instances.

**DeleteOnTermination ** Boolean`optional` `Example: false`

Enable delete with ECS instance.

* true: Enable.

* false: Disable.

## Response parameters

Only the response parameters specific to this API are listed below. For more information, see [Response structure](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response).

**RequestId ** String`Example: 2021062415303301022514515207C4****`

Request ID.

## Request example

```json
GET /?Action=AttachNetworkInterface&Version=2020-04-01&NetworkInterfaceId=eni-bp1fg655nh68xyz9****&InstanceId=i-wijfn35c**** HTTP/1.1
Host: vpc.cn-beijing.byteplusapi.com.cn
X-Date: 20251121T094038Z
Authorization: HMAC-SHA256 Credential=Adfks******wekfwe/20251121/cn-beijing/vpc/request, SignedHeaders=host;x-date, Signature=47a7d934ff7b37c03938******cd7b8278a40a1057690c401e92246a0e41085f
```

## Response example

```json
{
    "ResponseMetadata": {
        "RequestId": "20230604110420****100232280022D31",
        "Action": "AttachNetworkInterface",
        "Version": "2020-04-01",
        "Service": "vpc",
        "Region": "cn-beijing"
    },
    "Result": {
        "RequestId": "2021062415303301022514515207C4****"
    }
}
```

## Error codes

|Status code |Error codes |Error message |Description |
|---|---|---|---|
|400 |Forbidden.TrafficMode |You are not authorized to perform operations on the specified network interface. |You do not have permission to perform operations on the specified ENI. |
|400 |InvalidENI.DeviceType |The specified Eni deviceType is invalid. |The ENI device type is invalid. |
|400 |InvalidEip.InUse |The specified EIP is being operated by another request. |The specified EIP is being operated by another request. Try again later. |
|400 |InvalidEni.AccountMismatch |The specified elastic network interface and instance are in different account. |The specified ENI and the target instance must belong to the same account. |
|400 |InvalidEni.InvalidStatus |The specified elastic network interface is not in the correct status for the request. |The specified ENI is not in a status that can respond to this request. |
|400 |InvalidEni.InvalidType |The type of specified elastic network interface is illegal for the request. |The specified type of ENI cannot process this request. |
|400 |InvalidEni.ZoneMismatch |The specified elastic network interface and instance are in different Available Zones. |The specified ENI and the instance are not in the same availability zone. |
|400 |InvalidInstance.InvalidStatus |The specified instance is not in the correct status for the request. |The specified ECS instance is in a state that cannot process this request. |
|400 |InvalidInstance.InvalidType |The specified instance type is invalid for the request. |The specified ECS instance type cannot respond to the request. |
|400 |InvalidInstance.Malformed |The specified instance does not support vRDMA currently. |The specified ECS instance does not currently support vRDMA. |
|400 |InvalidIp.Malformed |The specified ip is malformed. |The specified IP is invalid. |
|400 |InvalidTrafficMirrorSession.InvalidStatus |The specified traffic mirror session is not in the correct status for the request. |The specified traffic mirror session is in a state that cannot respond to this request. |
|400 |InvalidVpcEip.InUse |The specified vpc eip is being operated by another request. |The specified EIP is being operated by another request. Try again later. |
|400 |InvalidVrdmaEnable.JumboFrameMismatch |The specified instance is not supported to enable vRDMA without jumbo frame enabled. |The specified instance does not support enabling vRDMA when JumboFrame is not enabled. |
|400 |LimitExceeded.BranchEnisPerInstance |You've reached the limit on the number of branch enis that can be attached to a single instance. |The maximum number of branch ENIs allowed for this ECS instance has been reached. |
|400 |LimitExceeded.EnisPerInstance |You've reached the limit on the number of elastic network interfaces that can be attached to a single instance. |The maximum number of ENIs that can be bound to the ECS instance has been reached. |
|400 |LimitExceeded.HighPerformanceEnisPerInstance |You've reached the limit on the number of high performance elastic network interfaces that can be attached to the specified instance. |The maximum number of high\-performance ENIs that can be bound to the ECS instance has been reached. |
|400 |LimitExceeded.Ipv6AddressesPerEni |The number of IPv6 addresses for a specified network interface exceeds the limit for the type of instance you are attaching. |The ENI has reached the maximum number of assignable IPv6 addresses for the specified instance type. |
|400 |LimitExceeded.PrivateIpsPerEni |You've reached the limit on the number of private IPs per elastic network interface that you can create. |The maximum number of assignable secondary IP addresses for the ENI has been reached. |
|403 |Forbidden |You are not authorized to perform operations on ESI related resources. |No permission to manage resources associated with the Elastic Scheduled Instance (ESI). |
|403 |Forbidden |You are not authorized to perform operations on the specified elastic network interface. |No sufficient permissions to perform this operation on the specified ENI. |
|403 |Forbidden |You are not authorized to perform operations on the specified elastic network interface. The specified elastic network interface is a service\-managed elastic network interface. |No permission to perform actions on the specified ENI. The specified ENI is managed by a cloud product. |
|404 |InvalidEniId.NotFound |The specified elastic network interface does not exist. |The specified ENI does not exist. |
|404 |InvalidInstance.NotFound |The specified instance does not exist. |The specified ECS instance does not exist. |
|409 |InvalidEniVtepIp.Conflict |The specified elastic network interface vtep ip is conflict. |The specified ENI has a conflicting VTEP IP. |
|500 |VportLimit.Exceed |The number of Vports on the specified host has exceeded the limit. |The number of Vports on the specified Host has exceeded the limit. |
