---
title: "ModifyLoadBalancerType - Changing the ALB instance network type"
product: "Cloud Load Balancer"
product_code: "clb"
source: "https://docs.byteplus.com/en/docs/clb/ModifyLoadBalancerType"
---

Call the ModifyLoadBalancerType API to change the ALB instance network type.

## Instructions

* Submit up to 5 API requests per second.

* IPv4&IPv6 dual\-stack ALB instances do not support changing the network type.

* The following table describes the network type change for IPv4 ALB instances:

   |**Change actions** |**Effective scope** |
   |---|---|
   |Change from private network to public network instance |The ALB instance domain name resolves to the EIP address.<br><br>> **tip**<br><br><br>> The EIP address will incur charges. For billing details, see [EIP billing](https://docs.byteplus.com/docs/eip/Pay-as-you-go).<br><br><br><br>* > When selecting **Anycast EIP** for the first time, you need to grant the ServiceRoleForAlb service role permissions for the Anycast EIP service. Please note: Do not delete this role, otherwise cross\-service authorization will become invalid.<br><br><br>* > If the ALB instance is the first origin site bound to the Anycast EIP, it becomes the default origin site. In this case, the system automatically associates all access points with this origin site. If you need to adjust the default origin site of the Anycast EIP, please go to the [Anycast EIP console](https://console.byteplus.com/eip/region:eip+cn-beijing/anycasts).<br> |
   |Change public network instance to private network instance |* All EIP addresses associated with the instance will be unbound automatically.<br><br>   * If an EIP address was created synchronously with the instance, it will be deleted.<br><br>   * If an EIP address was created manually by you, it will not be deleted. If it is no longer needed, you can manually delete it to avoid charges.<br><br>* The instance domain name resolves to the private IP address.<br><br>* The instance cannot be accessed from the internet. |

## Debug

[去调试](https://api.byteplus.com/api-explorer/?action=ModifyLoadBalancerType&groupName=%E5%AE%9E%E4%BE%8B&serviceCode=alb&version=2020-04-01)

## Request parameters

The following only details request parameters specific to this API and key common parameters. More information can be found in [Common parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).

**Action ** string必选 `Example: ModifyLoadBalancerType`

Action to execute. Set the value to ModifyLoadBalancerType.

**Version ** string必选 `Example: 2020-04-01`

The API version. Value: 2020\-04\-01.

**Type ** string必选 `Example: private`

Type of ALB instance. Valid values:

* public: Change to public ALB instance.

* private: Change to private ALB instance.

**ZoneMappings.N.AllocationId ** string[]`optional` `Example: ZoneMappings.1.AllocationId=eip-****&ZoneMappings.2.AllocationId=eip-***`

The EIP ID.

**ZoneMappings.N.ZoneId ** string[]`optional` `Example: ZoneMappings.1.ZoneId=cn-beijing-a&ZoneMappings.2.ZoneId=cn-beijing-b`

Availability zone ID of the ALB instance.

* ALB allows you to call the [DescribeZones](https://docs.byteplus.com/en/docs/clb/ALB-DescribeZones) API to obtain information about the availability zone corresponding to an availability zone ID.

**ZoneMappings.N.EipType ** string[]`optional` `Example: ZoneMappings.1.EipType=anycast&ZoneMappings.2.EipType=anycast`

EIP type.

* empty: EIP.

* anycast: Anycast EIP. The current Anycast EIP type requires allowlist activation in both the Anycast EIP and ALB products before it can be used.

**ZoneMappings.N.PopLocations ** string[]`optional` `Example: ZoneMappings.1.PopLocations=cn-beijing-pop,cn-shanghai-pop&ZoneMappings.1.PopLocations=cn-beijing-pop,cn-shanghai-pop`

When binding an Anycast EIP type, you can specify an access point.

* Separate multiple access points with commas (,).

* You can call the Anycast API DescribeAnycastPopLocations (visible to allowlisted accounts) to query valid access point information.

**LoadBalancerId ** string必选 `Example: alb-*******`

ALB instance ID.

## Response parameters

Only the response parameters specific to this API are listed below. More information, see [Response structure](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response).

**RequestId ** string`Example: 20210811152539010225146063030****`

Request ID.

## Request example

```text
GET /?Action=ModifyLoadBalancerType&Version=2020-04-01&Type=public&ZoneMappings.1.AllocationId=eip-2fe6iauhyn3ls5oxruuyf****&ZoneMappings.1.ZoneId=cn-beijing-a
Host: alb.cn-beijing.byteplusapi.com.cn
X-Date: 20251121T094038Z
Authorization: HMAC-SHA256 Credential=Adfks******wekfwe/20251121/cn-beijing/alb/request, SignedHeaders=host;x-date, Signature=47a7d934ff7b37c03938******cd7b8278a40a1057690c401e92246a0e41085f
```

## Response examples

```text
{
    "ResponseMetadata": {
        "RequestId": "20210816110638****2514606306AF947C",
        "Action": "ModifyLoadBalancerType",
        "Version": "2020-04-01",
        "Service": "alb",
        "Region": "cn-beijing"
    },
    "Result": {
        "RequestId": "20210811152539010225146063030****"
    }
}
```

## Error codes

The following table lists the error codes related to the business logic for this API. For details, see [Common error codes](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-error-codes).

|Status code |Error codes |Error message |Notes |
|---|---|---|---|
|400 |Invalid%s.Malformed |MismatchThe specified %s is malformed. |The specified %s parameter format is invalid. |
|400 |MissingParameter |The request is missing a required parameter. Ensure that you have supplied all the required parameters for the request; for example, '%s'. |This request does not contain the required parameter. Please ensure the request includes all required parameters, such as: %s. |
|400 |InvalidParameter |Data unmarshal failed. |Failed to parse the request. |
|400 |InvalidType.Malformed |The specified Type is malformed. |The specified Type parameter format is invalid. |
|400 |OperationFailed.EipUsedByBandwidthPackage |The request on the specified LoadBalancer failed due to eip being used by bandwidth package. |Because the EIP instance is still being used by a bandwidth package, the operation request for this ALB instance fails. Please remove the EIP instance from the bandwidth package before performing the operation. |
|400 |OperationFailed.OperateGtmFailed |The request on the specified resource failed due to operating gtm failed. |The request to operate on this resource failed because the operation on the GTM instance failed. |
|400 |InvalidLoadBalancer.InvalidStatus |The specified LoadBalancer is not in the correct status for the request. |The specified ALB is in a state that cannot respond to this request. |
|400 |InvalidEipBandwidthPackage.InUse |The specified EIP is being used by bandwidth package. |The specified EIP is being used by a bandwidth package. |
|400 |InvalidZoneMappings.EipType.Malformed |The specified ZoneMappings.EipType is malformed. |The specified ZoneMappings.EipType parameter format is invalid. |
|400 |OperationDenied.EipBindExist |The request on the specified LoadBalancer is denied due to the specified Anycast EIP has already bound instance in this region. |Because the specified Anycast EIP is already bound to an instance in this region, the operation request for this ALB instance is rejected. |
|400 |InvalidAnycastEip.InvalidStatus |The specified Anycast EIP is not in the correct status for the request. |The specified Anycast EIP is in a status that cannot respond to this request. |
|400 |OperationFailed.QueryVpc |The request on the specified resource failed due to the query on VPC failed. |The request to operate on this resource failed because the VPC request failed. |
|400 |OperationFailed.QueryIAM |The request on the specified resource failed due to the query on IAM failed. |The request to operate on this resource failed because the IAM request failed. |
|400 |InvalidZoneMappings.AllocationId.Duplicated |The specified ZoneMappings.AllocationId is duplicated. |The specified ZoneMappings.AllocationId is duplicated. |
|400 |OperationDenied.UnsupportedEipBillingType |The request on the specified LoadBalancer is denied due to unsupported EIP billing type. |Because the EIP bound to the private ALB instance does not support this billing method, the operation request for this ALB instance is rejected. |
|400 |InvalidEip.InvalidStatus |The specified EIP is not in the correct status for the request. |The specified EIP is in a state that cannot respond to this request. |
|400 |InvalidEipType.ExpectedEipTypeMismatch |The specified EIP type and expected EIP type do not match. |The specified EIP type does not match the expected EIP type. |
|400 |MissingParameter |The request is missing a required parameter. Ensure that you have supplied all the required parameters for the request; for example, 'ZoneMappings.AllocationId'. |This request does not contain required parameters. Please ensure the request includes all required parameters, such as: ZoneMappings.AllocationId. |
|400 |InvalidZoneMappings.ZoneId.Duplicated |The specified ZoneMappings.ZoneId is duplicated. |The specified ZoneMappings.ZoneId is duplicated. |
|400 |InvalidNumberForZone.AllocationIdMismatch |The specified number of Zone and AllocationId do not match. |The number of specified availability zones and EIPs does not match. |
|400 |OperationDenied.TypeNotChange |The request on the specified LoadBalancer is denied due to the type not changing. The type to be modified should not be the same as the original one. |Because the specified Type is the same as the original Type, the operation request for this ALB instance is rejected. The expected instance type to change to cannot be the same as the original type. |
|400 |OperationDenied.DualStackUnsupported |The request on the specified LoadBalancer is denied due to dual stack loadbalancer does not support to modify type. |Because dual\-stack ALB instances do not currently support changing the network type, the operation request for this ALB instance is rejected. |
|400 |OperationDenied.ModifyLoadBalancerType |The request on the specified LoadBalancer is denied due to the LoadBalancer is used by ArkClaw. |Because the ALB instance has ArkClaw enabled, modifying the instance type is not supported, and operation requests for this ALB instance are rejected. |
|403 |Forbidden |You are not authorized to associate Anycast EIP with the specified LoadBalancer. |You do not have permission to bind an Anycast EIP to this ALB instance. |
|404 |InvalidLoadBalancer.NotFound |The specified LoadBalancer does not exist. |The specified ALB instance does not exist. |
|404 |InvalidZone.NotFound |The specified Zone does not exist. The LoadBalancer has not been deployed in the specified zone yet. |The specified availability zone does not exist. The ALB instance has not been deployed in this availability zone. |
|404 |InvalidEip.NotFound |The specified EIP does not exist. |The specified EIP does not exist. |
|404 |InvalidAnycastEip.NotFound |The specified Anycast EIP does not exist. |The specified Anycast EIP does not exist. |
|404 |InvalidPopLocation.NotFound |The specified PopLocation does not exist. |The specified access point does not exist. |
|500 |InternalError |An internal error has occurred. |An internal error occurred. Please try again later or contact an engineer for further consultation. |
