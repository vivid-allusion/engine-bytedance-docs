---
title: "AssociateEipAddress - Associating an EIP"
product: "Elastic IP Address"
product_code: "eip"
source: "https://docs.byteplus.com/en/docs/eip/AssociateEipAddress"
---

Call the AssociateEipAddress API to associate an elastic IP address (EIP) with a cloud resource.

<span id=".5L2_55So6K-05piO"></span>
## Instructions

The daily call quota for this API is three times the quota of EIPs that you can apply for, per account per region.

<span id=".6LCD6K-V"></span>
## Debug

[去调试](https://api.byteplus.com/api-explorer/debug?action=AssociateEipAddress&serviceCode=vpc&version=2020-04-01&groupName=)


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters

The following only details request parameters specific to this API and key common parameters. For more information, see [Common parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).



**Action ** <span data-label="purple"> String  </span><span data-api-tag="require|7CrWw_">必选</span> `Example: AssociateEipAddress`

The action that you want to perform. Value: **AssociateEipAddress**.



**Version ** <span data-label="purple"> string </span><span data-api-tag="require|I3K3Qn">必选</span> `Example: 2020-04-01`

API version. The current version is **2020\-04\-01**.



**AllocationId ** <span data-label="purple"> String </span><span data-api-tag="require|9wIDSu">必选</span> `Example: eip-2zeewb7ujxscd****`

The ID of the EIP.

You can call [DescribeEipAddresses](https://docs.byteplus.com/en/docs/eip/DescribeEipAddressAttributes) to query the EIP ID.



**DirectMode ** <span data-label="purple"> Boolean  </span>`optional` `Example: false`

Specify whether to enable Direct when associating an EIP. Type the enumerated values strictly in the case form as follows. Do not set other values.


* false (default): Do not enable Direct mode.

* true: Enable Direct mode.


<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">The EIP Direct feature is in the beta stage. If you need a trial, contact your account manager.</div>




**InstanceType ** <span data-label="purple"> String  </span><span data-api-tag="require|ycxNfY">必选</span>`Example: EcsInstance`

The type of instance to be associated with an EIP.


* Nat: NAT gateway.

* NetworkInterface: Secondary network interface.

* ClbInstance: Classic Load Balancer.

* EcsInstance: Elastic Compute Service.

* HaVip: High\-Availability Virtual IP Address.



**InstanceId ** <span data-label="purple"> String </span><span data-api-tag="require|L1Icw_">必选</span> `Example: i-2zebbhyczzaweeval****`

ID of the cloud resource to be associated. Provide the ID of the cloud resource whose type corresponds to the value of `InstanceType`.



**PrivateIpAddress** <span data-label="purple">String</span> `optional` `Example: 192.XX.XX.4`

Private IP address of the instance to be associated with an EIP.


* You can only specify the private IP address of the ECS primary network interface and the IP address of the secondary network interface.

* If left blank: The primary private IP address of ECS primary network interface is associated when `InstanceType` is set to EcsInstance. And the primary private IP address of the secondary network interface is associated when `InstanceType` is set to NetworkInterface.


<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">When an EIP is associated with a HAVIP, NAT gateway or CLB, <code>PrivateIpAddress</code> is not supported.</div>




**VpcId** <span data-label="purple">String</span> `optional` Example: vpc\-257gqcdfvx6n\*\*\*\*

The ID of the VPC associated with the EIP.

This parameter is required when **InstanceType** is set to `IpAddress`. You can only type the ID of the VPC that has the IPv4 gateway enabled and is in the same region as the EIP.



**ClientToken ** <span data-label="purple"> String </span>`optional` `Example: 123e4567-e89b-12d3-a456-42665544****`

Ensure the request idempotency. You can use the client to automatically generate a token, but must confirm that the tokens for different requests are unique. This prevents repeated actions due to multiple client retries when the call of the API action times out or an internal server error occurs. Values:


* Must not exceed 64 ASCII characters.



<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters

The following only details response parameters specific to this API. For more information, see [Response structure](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response).



**RequestId ** <span data-label="purple"> String </span>`Example: 2021062415303301022514515207C4****`

Request ID.



<span id=".6K-35rGC56S65L6L"></span>
## Request examples

```JSON
GET /?Action=AssociateEipAddress&Version=2020-04-01&AllocationId=eip-2zeewb7ujxscd****&InstanceType=EcsInstance&InstanceId=i-2zebbhyczzaweeval**** HTTP/1.1
Host: vpc.cn-beijing.byteplusapi.com.cn
Service: vpc
Region: cn-beijing
```


<span id=".6L-U5Zue56S65L6L"></span>
## Response examples

```JSON
{
    "ResponseMetadata": {
        "RequestId": "2021062415303301022514515207C4****",
        "Action": "AssociateEipAddress",
        "Version": "2020-04-01",
        "Service": "vpc",
        "Region": "cn-beijing"
    },
    "Result":{
        "RequestId": "2021062415303301022514515207C4****"
    }
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error codes

For more information, see [Common error codes](https://docs.byteplus.com/en/docs/eip/Public-error-codes).


|**Status code** |**Error codes** |**Error message** |**Explain** |
|---|---|---|---|
|400 |IdempotentParameterMismatch |Arguments on this idempotent request are inconsistent with arguments used in previous request(s). |The parameters of this idempotent request are inconsistent with those used in the previous request. |
|400 |InvalidClb.InUse |The specified CLB instance has already been associated with an anycast elastic ip address. |The specified CLB instance is already associated with an Anycast EIP. |
|400 |InvalidClb.InUse |The specified CLB has already been associated with an elastic ip address. |The specified CLB is associated with an EIP. |
|400 |InvalidClb.InvalidStatus |The specified CLB is not in the correct status for the request. Current CLB has been frozen. |The specified CLB cannot respond to this request due to its status. The current CLB is frozen. |
|400 |InvalidDirectModeEip.IPv4GatewayEnabled |EIP not allowed to open direct mode when VPC has been attached to IPv4 gateway. |The VPC is attached to an IPv4 gateway. Therefore, the EIP cannot enable Direct mode. |
|400 |InvalidEcs.InUse |The specified ECS instance has already been associated with an anycast elastic ip address. |The specified ECS instance is already associated with an Anycast EIP. |
|400 |InvalidEip.InstanceMismatch |The specified instance private ip does not support eip association. |The private IP address of the specified instance does not support associating an EIP. |
|400 |InvalidEip.InvalidStatus |The specified elastic ip address is not in the correct status for the request. |The specified EIP is in a status that cannot respond to this request. |
|400 |InvalidEip.InvalidStatus |The specified elastic ip is not in the correct status for the request. The specified elastic ip is in freeze. |The specified EIP or VPC cannot respond to this request due to its status. The current EIP is frozen. |
|400 |InvalidEni.InUse |The specified elastic network interface has already been associated with an elastic ip address. |The specified network interface is associated with an EIP. |
|400 |InvalidEip.PrivateAddressConflict |The specified private address conflicts with another associated with EIP. |The specified private IP address is already associated with an EIP. |
|400 |InvalidEni.InvalidType |The type of specified elastic network interface is illegal for the request. |The specified ENI type cannot respond to this request. |
|400 |InvalidHaVip.InUse |The specified HaVip has already been associated with an elastic ip address. |The specified high\-availability virtual IP address (HAVIP) is already associated with an EIP. |
|400 |InvalidInstance.InUse |The specified ECS has already been associated with an elastic ip address. |The specified ECS instance is already associated with an EIP. |
|400 |InvalidInstance.InvalidStatus |The specified ECS is not in the correct status for the request. Current ECS has been frozen. |The specified ECS instance cannot respond to this request due to its status. The current ECS instance is frozen. |
|400 |InvalidIpAddress.InUse |The specified IP address of elastic network interface has already been associated with an anycast elastic ip address. |The IP address of the specified elastic network interface (ENI) is already associated with an Anycast EIP. |
|400 |InvalidModeEip.DirectMode |EIP not allowed to open direct mode. |Direct mode cannot be enabled for the EIP. |
|400 |InvalidNatGateway.InvalidStatus |The operation is not supported by the current nat gateway |The specified NAT gateway is in a status that cannot respond to this request. |
|400 |InvalidNatGateway.UnSupportAction |The specified NAT gateway does not support this action. |The specified NAT gateway does not support the current action. |
|400 |InvalidParameter.ClientTokenMalformed |The specified parameter ClientToken is malformed. |The format of specified CientToken is invalid. It must not exceed 64 ASCII characters. |
|400 |InvalidPrivateIp.IPFormatError |The specified private IP format error. |The specified secondary IP format is incorrect. |
|400 |InvalidPrivateIp.InstanceMismatch |The specified private ip and the instance mismatch. |The specified secondary IP does not match the instance. Note For more information, see the description of PrivateIpAddress in [Request parameters](https://docs.byteplus.com/en/docs/eip/AssociateEipAddress#.6K-35rGC5Y-C5pWw). |
|400 |InvalidPrivateIp.Malformed |The specified private ip is malformed. The specified private ip is not the primary ip of ECS. |The specified private IP address is invalid. The specified private IP address is not the primary private IP address of the ECS instance. |
|400 |InvalidVpc.IPv4GatewayDisabled |IPv4 gateway attached to the specified VPC is disabled. |The specified VPC does not enable IPv4 gateway. |
|400 |InvalidVpc.InvalidStatus |The specified VPC is not in the correct status for the request. |The specified VPC is in a state that cannot respond to this request. |
|400 |QuotaExceeded.Eip |The number of EIPs bound to the NAT gateway exceeded quota. |You have reached the maximum of EIPs that you can associate with a single NAT gateway. |
|400 |QuotaExceeded.ExceedLimit |Interface call exceeds limit. |The number of API calls exceeds the quota. |
|403 |Forbidden |You are not authorized to perform operations on the specified elastic ip and ALB. |No permission to operate this EIP and the Application Load Balancer (ALB). |
|403 |Forbidden |You are not authorized to associate EIP by IP address. |No permission to attach the IP Address to the EIP. |
|403 |Forbidden |You are not authorized to perform operations on the specified elastic network interface. The specified elastic network interface is a service\-managed elastic network interface. |No permission to perform actions on the specified elastic network interface. The specified elastic network interface is managed by a cloud product. |
|403 |Forbidden |You are not authorized to perform operations on the specified elastic ip and public CLB. |No permission to manage this EIP and the public Classic Load Balancer (CLB). |
|400 |InvalidDirectModeEip.InstanceMismatch |The specified instance type does not support direct mode EIP. |The specified instance type does not support EIP Direct mode. |
|400 |InvalidDirectModeEip.InvalidBindInstanceType |Only elastic network interface bound to ECS support associating direct mode EIP. |Only ENIs associated with ECSs support associating direct EIPs. |
|400 |InvalidInstance.IPv4Disabled |IPv4 has been disabled for the specified instance. |The specified instance has disabled IPv4. |
|403 |Forbidden |You are not authorized to perform operations on ESI related resources. |No permission to manage resources associated with the Elastic Scheduled Instance (ESI). |
|403 |Forbidden |You are not authorized to associate direct mode EIP with ECS. |No permission to associate a direct EIP with an Elastic Compute Service (ECS). |
|403 |Forbidden |You are not authorized to associate binded EIP on elastic network interface. |No permission to associate the direct EIP with the ENI. |
|404 |InvalidEip.NotFound |The specified EIP does not exist. |The specified EIP does not exist. |
|404 |InvalidEniId.NotFound |The specified elastic network interface does not exist. |The specified ENI does not exist. |
|404 |InvalidInstance.NotFound |The specified instance does not exist. |The specified instance does not exist. |
|404 |InvalidInstanceType.NotFound |The specified instance type does not exist. |The specified instance type does not exist. |
|404 |InvalidNatGateway.NotFound |The specified NAT gateway does not exist. |The specified NAT gateway does not exist. |
|404 |InvalidVpc.NotFound |The specified VPC does not exist. |The specified Virtual Private Cloud (VPC) does not exist. |
|412 |IdempotentProcessing |The request uses the same client token as a previous one that is still in process. |The idempotent request is in progress. |
|412 |InvalidNatGateway.Expired |The specified NAT gateway has expired. |The specified NAT gateway is expired. |
