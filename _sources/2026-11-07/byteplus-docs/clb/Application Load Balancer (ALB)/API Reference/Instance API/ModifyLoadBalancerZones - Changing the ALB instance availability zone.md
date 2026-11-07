---
title: "ModifyLoadBalancerZones - Changing the ALB instance availability zone"
product: "Cloud Load Balancer"
product_code: "clb"
source: "https://docs.byteplus.com/en/docs/clb/ModifyLoadBalancerZones"
---

Call the ModifyLoadBalancerZones API to change the ALB instance availability zones.

<span id=".5L2_55So6K-05piO"></span>
## Instructions


* Submit up to 5 API requests per second.

* You must retain at least one availability zone currently in use by the ALB instance.


<span id=".6LCD6K-V"></span>
## Debug

[去调试](https://api.byteplus.com/api-explorer/?action=ModifyLoadBalancerZones&groupName=%E5%AE%9E%E4%BE%8B&serviceCode=alb&version=2020-04-01)


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters

The following only details request parameters specific to this API and key common parameters. More information can be found in [Common parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).



**Action ** <span data-label="purple">string </span><span data-api-tag="require|PE85Wa">必选</span> `Example: ModifyLoadBalancerZones`

Action to execute. Set the value to ModifyLoadBalancerZones.



**Version ** <span data-label="purple">string </span><span data-api-tag="require|YlREnh">必选</span> `Example: 2020-04-01`

The API version. Value: 2020\-04\-01.



**LoadBalancerId ** <span data-label="purple">string </span><span data-api-tag="require|awmqEB">必选</span> `Example: alb-*******`

ALB instance ID.



**ZoneMappings.N.ZoneId ** <span data-label="purple">string[] </span><span data-api-tag="require|Q3B27b">必选</span> `Example: ZoneMappings.1.ZoneId=cn-beijing-a&ZoneMappings.2.ZoneId=cn-beijing-b`

Availability zone ID of the ALB instance.


* You can call the [DescribeZones](https://docs.byteplus.com/docs/clb/ALB-DescribeZones) API to obtain the availability zone IDs where ALB instances can be deployed.

* `SubnetId` and `ZoneId` must match.



**ZoneMappings.N.AllocationId ** <span data-label="purple">string[] </span>`optional` `Example: ZoneMappings.1.AllocationId=eip-bp12mw1f8k3jgy****&ZoneMappings.2.AllocationId=eip-bp0ohf1f8k3jgy****`

The ID of the EIP.



**ZoneMappings.N.SubnetId ** <span data-label="purple">string[] </span><span data-api-tag="require|nakb8q">必选</span> `Example: ZoneMappings.1.SubnetId=subnet-bp12mw1f8k3jgy****&ZoneMappings.2.SubnetId=subnet-bp0ohf1f8k3jgy****`

Subnet ID. The private IP address of the ALB instance in this availability zone will be allocated from the subnet CIDR block of this subnet.



&nbsp;

<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters

Only the response parameters specific to this API are listed below. More information, see [Response structure](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response).



**RequestId ** <span data-label="purple">string </span>`Example: 202411152539010225146063030****`

Request ID.



&nbsp;

<span id=".6K-35rGC56S65L6L"></span>
## Request examples

```text
GET /?Action=ModifyLoadBalancerZones&Version=2020-04-01&LoadBalancerId=alb-habjsbfjbesjbchjbs&ZoneMappings.1.ZoneId=cn-beijing-a&ZoneMappings.1.AllocationId=eip-knkjsefksenckjscn&ZoneMappings.1.SubnetId=subnet-mndfkjsfkjcsck
Host: alb.cn-beijing.byteplusapi.com.cn
X-Date: 20251121T094038Z
Authorization: HMAC-SHA256 Credential=Adfks******wekfwe/20251121/cn-beijing/alb/request, SignedHeaders=host;x-date, Signature=47a7d934ff7b37c03938******cd7b8278a40a1057690c401e92246a0e41085f
```


<span id=".6L-U5Zue56S65L6L"></span>
## Response examples

```text
{
    "ResponseMetadata": {
        "RequestId": "20210816110638****2514606306AF947C",
        "Action": "ModifyLoadBalancerZones",
        "Version": "2020-04-01",
        "Service": "alb",
        "Region": "cn-beijing"
    },
    "Result": {
        "RequestId": "20210811152539010225146063030****"
    }
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error codes

The following table lists the error codes related to the business logic for this API. For details, see [Common error codes](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-error-codes).


|Status code |Error codes |Error message |Notes |
|---|---|---|---|
|400 |InvalidParameter |Data unmarshal failed. |Failed to parse the request. |
|400 |MissingParameter |The request is missing a required parameter. Ensure that you have supplied all the required parameters for the request; for example, '%s'. |This request is missing a required parameter. Please ensure the request includes all required parameters, such as: %s. |
|400 |Invalid%s.Malformed |MismatchThe specified %s is malformed. |The specified %s parameter format is invalid. |
|400 |OperationDenied.ModifyLoadBalancerZones |The request on the specified LoadBalancer is denied due to the count of listeners bound with the LoadBalancer is too much. |The operation request for this ALB instance was rejected because the ALB instance has too many listeners configured. |
|400 |OperationDenied.ZoneUnsupported |The request on the specified LoadBalancer is denied due to the specified zone is unsupported. DescribeZones will tell you which zones ALB supports. |The operation request for this ALB instance was rejected because the specified availability zone does not support the creation of ALB instances. You can obtain information about availability zones where ALB instances can be deployed by calling the DescribeZones API. |
|400 |OperationDenied.ZoneInfoChanged |The request on the specified LoadBalancer is denied due to the subnet id or eip id of the existing zone has changed. |The operation request for this ALB instance was rejected because the subnet or EIP information of an existing availability zone has changed. |
|400 |OperationDenied.MissingOldZone |The request on the specified LoadBalancer is denied due to missing old zones. Please specify an old zone at least. |The operation request for this ALB instance was rejected because no old availability zone was specified. Specify at least one old availability zone. |
|400 |OperationDenied.ZoneMappingsNotChanged |The request on the specified LoadBalancer is denied due to the zone info has not changed. |The operation request for this ALB instance was rejected because no change was made to the availability zone information. |
|400 |OperationDenied.Ipv6NotEnabled |The request on the specified LoadBalancer is denied due to subnet is not IPv6 enabled. |The operation request for this ALB instance was rejected because IPv6 is not enabled on the subnet. |
|400 |OperationDenied.IPv6OnlySubnetNotAllowed |The request on the specified LoadBalancer is denied due to IPv6\-only subnets can not be specified to add zones. |The operation request for this ALB instance was rejected because the subnet supports only IPv6 and cannot be used to deploy the ALB instance in a new availability zone. |
|400 |OperationDenied.LoadBalancerWithAnycastEipNotAllowed |The request on the specified LoadBalancer is denied due to the LoadBalancer associated with anycast eip does not support to modify zone. |The operation request for this ALB instance was rejected because an ALB instance bound to an Anycast EIP does not support changing availability zones. |
|400 |OperationDenied.UnsupportedEipBillingType |The request on the specified LoadBalancer is denied due to unsupported EIP billing type. |Because the EIP bound to the private ALB instance does not support this billing method, the operation request for this ALB instance is rejected. |
|400 |OperationDenied.MissIPv6Address |The request on the specified LoadBalancer is denied due to the subnet missing ipv6 address. |The operation request for this ALB instance was rejected because the subnet lacks IPv6 addresses. |
|400 |InvalidZoneMappings.ZoneId.Duplicated |The specified ZoneMappings.ZoneId is duplicated. |The specified ZoneMappings.ZoneId is duplicated. |
|400 |InvalidZoneMappings.AllocationId.Duplicated |The specified ZoneMappings.AllocationId is duplicated. |The specified ZoneMappings.AllocationId is duplicated. |
|400 |InvalidSubnet.ZoneMismatch |The specified subnet and zone do not match. |The specified subnet does not match the availability zone. |
|400 |LimitExceed.Zone |You've reached the limit on the number of zones that you can operate at a time. |You have reached the maximum number of availability zones that can be operated on in a single request. |
|400 |QuotaExceed.Eni |You've reached the limit on the number of Eni that you can create. |The maximum number of ENIs that can be created has been reached. |
|400 |InvalidEip.InvalidStatus |The specified EIP is not in the correct status for the request. |The specified EIP is in a state that cannot respond to this request. |
|400 |InvalidEni.InvalidStatus |The specified Eni is not in the correct status for the request. |The specified Elastic Network Interface is not in a status that can respond to this request. |
|400 |InvalidIPv6Eip.InvalidStatus |The specified IPv6 EIP is not in the correct status for the request. |The specified IPv6 EIP is in a state that cannot respond to this request. |
|400 |InvalidLoadBalancer.InvalidStatus |The specified LoadBalancer is not in the correct status for the request. |The specified ALB is in a state that cannot respond to this request. |
|400 |OperationFailed.QueryVpc |The request on the specified resource failed due to the query on VPC failed. |The request to operate on this resource failed because the VPC request failed. |
|400 |OperationFailed.CreatePrivateEniFailed |The request on the specified LoadBalancer failed due to creating private eni failed. |The operation request for this ALB instance failed because the secondary network interface failed to be created. |
|400 |OperationFailed.EipUsedByBandwidthPackage |The request on the specified LoadBalancer failed due to eip being used by bandwidth package. |Because the EIP instance is still being used by a bandwidth package, the operation request for this ALB instance fails. Please remove the EIP instance from the bandwidth package before performing the operation. |
|400 |OperationDenied.ZoneTypeConflict |The request on the specified LoadBalancer is denied due to standard zones and local zones cannot be specified at the same time. |The operation request for this ALB instance was rejected because standard availability zones and local availability zones cannot coexist. |
|400 |InsufficientIpInSubnet |The specified subnet does not contain enough free private IP addresses to fulfill your request. |The available IPs under the specified subnet are insufficient. |
|403 |Forbidden |You are not authorized to modify zones for the LoadBalancer. |You do not have permission to modify the availability zone of the ALB instance. |
|404 |InvalidLoadBalancer.NotFound |The specified LoadBalancer does not exist. |The specified ALB instance does not exist. |
|404 |InvalidSubnet.NotFound |The specified Subnet does not exist. |The specified subnet does not exist. |
|404 |InvalidEip.NotFound |The specified EIP does not exist. |The specified EIP does not exist. |
|500 |InternalError |An internal error has occurred. |An internal error occurred. Please try again later or contact an engineer for further consultation. |
