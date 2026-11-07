---
title: "CloneLoadBalancer - Cloning an ALB instance"
product: "Cloud Load Balancer"
product_code: "clb"
source: "https://docs.byteplus.com/en/docs/clb/CloneLoadBalancer"
---

Call the CloneLoadBalancer API to clone an existing ALB instance.

<span id=".6LCD6K-V"></span>
## Debug

[去调试](https://api.byteplus.com/api-explorer/?action=CloneLoadBalancer&groupName=%E5%AE%9E%E4%BE%8B&serviceCode=alb&version=2020-04-01)


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters

The following only details request parameters specific to this API and key common parameters. More information can be found in [Common parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).



**Action ** <span data-label="purple">string </span><span data-api-tag="require|qKUyym">必选</span> `Example: CloneLoadBalancer`

Action to execute. Set the value to CloneLoadBalancer.



**Version ** <span data-label="purple">string </span><span data-api-tag="require|QvYBJu">必选</span> `Example: 2020-04-01`

The API version. Value: 2020\-04\-01.



**Ipv6BandwidthPackageId ** <span data-label="purple">string </span>`optional` `Example: bwp-2d6dcpvaeq9s058****`

When cloning a public ALB instance, specify the ID of the shared bandwidth package to which the IPv6 EIP address should be added.



**RegionId ** <span data-label="purple">string </span><span data-api-tag="require|BJtRT1">必选</span> `Example: cn-beijing`

Request region.



**LoadBalancerId ** <span data-label="purple">string </span><span data-api-tag="require|o8Okn7">必选</span> `Example: alb-bp1b6c719dfa08ex****`

The ALB instance ID to be cloned.



**LoadBalancerName** <span data-label="purple">string</span> `optional` `Example: alb-bp1o94dp5i6ea****`

Name of the ALB instance.


* Must start with a letter or Chinese character. May include numbers, periods (.), underscores (_), and hyphens (\-).

* Length limit is 1 to 128 characters.

* If left blank, it defaults to the instance ID.



**Description ** <span data-label="purple">string </span>`optional` `Example: This is an ALB instance.`

Description of the ALB instance.


* If left blank, this parameter defaults to an empty string.

* Must start with a letter or Chinese character and may include numbers, half\-width commas (,), periods (.), underscores (_), spaces ( ), equal signs (=), hyphens (\-), full\-width commas (，), and full\-width periods (。)

* Must be 1 to 255 characters.



**EipBillingConfig.ISP ** <span data-label="purple">string </span>`optional` `Example: BGP`

The IPv4 EIP ISP of the public ALB instance. Valid values:


* BGP (default): BGP (Multi\-ISP).



**EipBillingConfig.EipBillingType ** <span data-label="purple">integer </span>`optional` `Example: 2`

Billing method for the IPv4 EIP of the public ALB instance. Valid values:


* 2 (default): Pay\-as\-you\-go (pay\-by\-bandwidth).

* 3: Pay\-by\-data\-transfer.



**EipBillingConfig.Bandwidth ** <span data-label="purple">integer </span>`optional` `Example: 10`

The peak bandwidth of the IPv4 EIP of a public ALB instance. The default value is 1, in Mbps.



**Ipv6EipBillingConfig.ISP ** <span data-label="purple">string </span>`optional` `Example: BGP`

ISP of the IPv6 internet bandwidth for the public ALB instance. Valid values:


* BGP (default): BGP (Multi\-ISP).



**Ipv6EipBillingConfig.BillingType ** <span data-label="purple">integer </span>`optional` `Example: 2`

The billing method of the IPv6 internet bandwidth for the public ALB instance. Valid values:


* 2: Pay\-by\-bandwidth.

* 3 (default): Pay\-as\-you\-go (pay\-by\-data\-transfer).



**Ipv6EipBillingConfig.Bandwidth ** <span data-label="purple">integer </span>`optional` `Example: 200`

The bandwidth upper limit of the IPv6 internet bandwidth for the public ALB instance, in Mbps.


* This parameter is required when creating an IPv4&IPv6 dual\-stack public ALB instance.

* Bandwidth range:

   * When the Ipv6Address.BillingType parameter value is 2, default value range: 1 to 500.

   * When the Ipv6Address.BillingType parameter value is 3, default value range: 1 to 200.

   * If you need to increase the maximum bandwidth, please contact your account manager for the IPv6 gateway.



**EipBillingConfig.SecurityProtectionTypes ** <span data-label="purple">string </span>`optional` `Example: AntiDDoS_Enhanced`

When cloning a public ALB instance, ALB allows you to purchase multiple EIP protection resources. The specific rules for EIP protection resources are as follows:


* Separate multiple protection resources with commas (,).

* Values for protection resources:

   * AntiDDoS_Enhanced: You are applying for an EIP address of the enhanced protection type; you can add this IP to a Cloud DDoS Protection instance.

   * Not filled: You are applying for an EIP address of the basic protection type.

* Currently, the purchase of EIP protection resources is only available to allowlisted users. If you have business requirements, please contact your account manager.



**DeleteProtection ** <span data-label="purple">string </span>`optional` `Example: off`

Enable the delete protection feature for the ALB instance. Valid values:


* off (default): Disable.

* on: Enable.



**EipBillingConfig.SecurityProtectionInstanceId ** <span data-label="purple">long </span>`optional` `Example: 123132`

When cloning a public ALB instance, if IP protection resources are used, you need to specify the ID of an Anti\-DDoS Origin instance.



**ZoneMappings.N.SubnetId ** <span data-label="purple">string[] </span>`optional` `Example: subnet-bp12mw1f8k3jgy****`

Subnet ID. The private IP address of the ALB instance in this availability zone will be allocated from the subnet CIDR block of this subnet.



**ZoneMappings.N.ZoneId ** <span data-label="purple">string[] </span>`optional` `Example: cn-beijing-a`

Availability zone ID of the ALB instance. ALB allows you to call the DescribeZones API to obtain information about the availability zone corresponding to an availability zone ID. SubnetId and ZoneId must match.



**BandwidthPackageId ** <span data-label="purple">string </span>`optional` `Example: bwp-6248cim0mayon3gd5tv****`

When cloning a public ALB instance, specify the ID of the bandwidth package to which the EIP should be added.



**ProjectName ** <span data-label="purple">string </span>`optional` `Example: default`

Name of the project to which the ALB instance belongs.



**DryRun ** <span data-label="purple">string </span>`optional` `Example: off`

Whether to only precheck the request Values:


* on: Send a dry\-run request to perform request parameter validation without performing the actual clone operation.

* off (default): Send a normal request; after request parameter validation passes, perform the clone operation.



&nbsp;

<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters

Only the response parameters specific to this API are listed below. More information, see [Response structure](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response).



**LoadBalancerId ** <span data-label="purple">string </span>`Example: alb-bp1o94dp5i6ea****`

ALB instance ID.



**RequestId ** <span data-label="purple">string </span>`Example: 20210811152539010225146063030****`

Request ID.



&nbsp;

<span id=".6K-35rGC56S65L6L"></span>
## Request examples

```text
GET /?Action=CloneLoadBalancer&Version=2020-04-01&LoadBalancerId=alb-bp1b6c719dfa08ex****
Host: alb.cn-beijing.byteplusapi.com.cn
X-Date: 20251121T094038Z
Authorization: HMAC-SHA256 Credential=Adfks******wekfwe/20251121/cn-beijing/alb/request, SignedHeaders=host;x-date, Signature=47a7d934ff7b37c03938******cd7b8278a40a1057690c401e92246a0e41085f
```


<span id=".6L-U5Zue56S65L6L"></span>
## Response examples

```json
{
    "ResponseMetadata": {
        "RequestId": "20210816110638****2514606306AF947C",
        "Action": "CloneLoadBalancer",
        "Version": "2020-04-01",
        "Service": "alb",
        "Region": "cn-beijing"
    },
    "Result": {
        "RequestId": "20210816110638****2514606306AF947C",
        "LoadBalancerId": "alb-bp1o94dp5i6ea****"
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
|400 |InvalidDescription.Malformed |The specified Description is malformed. |The format specified for Description is invalid. |
|400 |InvalidLoadBalancerName.Malformed |The specified LoadBalancerName is malformed. |The specified LoadBalancerName format is invalid. |
|400 |QuotaExceed.Eip |You've reached the limit on the number of EIP that you can create. |The maximum number of EIPs that can be created has been reached. |
|400 |OperationFailed.QueryVpc |The request on the specified resource failed due to the query on VPC failed. |The request to operate on this resource failed because the VPC request failed. |
|400 |InvalidSubnet.ZoneMismatch |The specified subnet and zone do not match. |The specified subnet does not match the availability zone. |
|400 |OperationFailed.QueryProject |The request on the specified resource failed due to the query on project failed. |The request to operate on this resource failed because the project query failed. |
|400 |InvalidZoneMappings.ZoneId.Duplicated |The specified ZoneMappings.ZoneId is duplicated. |The specified ZoneMappings.ZoneId is duplicated. |
|400 |OperationDenied.ZoneUnsupported |The request on the specified LoadBalancer is denied due to the specified zone is unsupported. DescribeZones will tell you which zones ALB supports. |The operation request for this ALB instance was rejected because the specified availability zone does not support the creation of ALB instances. You can obtain information about availability zones where ALB instances can be deployed by calling the DescribeZones API. |
|400 |InvalidIndexOrder.Malformed |The specified index order is malformed. |The specified index order parameter format is invalid. |
|400 |InvalidDeleteProtection.Malformed |The specified DeleteProtection is malformed. |The specified DeleteProtection parameter format is invalid. |
|400 |OperationFailed.AccountBalanceNotEnough |The request on the specified Resource failed due to the account balance and available vouchers are less than 100 yuan in total. |The operation request for this resource failed because the total of your account balance and available vouchers is less than 100 USD. Recharge and try again. |
|400 |OperationFailed.CreateOrderFailed |The request on the specified LoadBalancer failed due to creating an order failed. |Because the order payment failed, the operation request for this ALB instance fails. |
|400 |OperationFailed.CreatePrivateEniFailed |The request on the specified LoadBalancer failed due to creating private eni failed. |The operation request for this ALB instance failed because the secondary network interface failed to be created. |
|400 |OperationFailed.CreatePreOrderFailed |The request on the specified LoadBalancer failed due to creating a pre order failed. |Because the configuration order failed to be placed, the operation request for this ALB instance fails. |
|400 |QuotaExceed.EipInBandwidthPackage |You've reached the limit on the number of EIP per bandwidth package you can add in. |The maximum number of EIPs that can be added to the bandwidth package has been reached. |
|400 |QuotaExceed.InstancePerRegion |You've reached the limit on the number of loadbalancers the current region you can create in, usage xx/xx. |The maximum number of ALB instances that can be created in the current region has been reached. Used: xxx. Quota: xxx |
|400 |InvalidIpv6Gateway.InvalidStatus |The specified IPv6Gateway of VPC is not in the correct status for the request. |The IPv6 gateway corresponding to the specified VPC is in a state that cannot respond to this request. |
|400 |InvalidIpv6EipBillingConfig.Bandwidth.Malformed |The specified Ipv6EipBillingConfig.Bandwidth is malformed. |The specified Ipv6EipBillingConfig.Bandwidth parameter format is invalid. |
|400 |OperationFailed.QueryIpv6Gateway |The request on the specified resource failed due to the query on ipv6 gateway failed. |The request to operate on this resource failed because the IPv6 gateway request failed. |
|400 |OperationFailed.QueryIAM |The request on the specified resource failed due to the query on IAM failed. |The request to operate on this resource failed because the IAM request failed. |
|400 |InvalidIpv6EipBillingConfig.BillingType.Malformed |The specified Ipv6EipBillingConfig.BillingType is malformed. |The specified Ipv6EipBillingConfig.BillingType parameter format is invalid. |
|400 |InvalidIpv6EipBillingConfig.ISP.Malformed |The specified Ipv6EipBillingConfig.ISP is malformed. |The specified Ipv6EipBillingConfig.ISP parameter format is invalid. |
|400 |InvalidISPForEip.BandwidthPackageMismatch |The specified ISP for EIP and BandwidthPackage do not match. |The specified EIP does not match the ISP of bandwidth package. |
|400 |OperationDenied.Ipv6NotEnabled |The request on the specified LoadBalancer is denied due to the vpc does not have an IPv6 gateway. |The operation request for this ALB instance was rejected because the VPC where the ALB instance is to be created does not have an IPv6 gateway enabled. |
|400 |InvalidEipBillingConfig.EipBillingType.Malformed |The specified EipBillingConfig.EipBillingType is malformed. |The specified EipBillingConfig.EipBillingType format is invalid. |
|400 |QuotaExceed.Eni |You've reached the limit on the number of Eni that you can create. |The maximum number of ENIs that can be created has been reached. |
|400 |QuotaExceed.RulePerGroup |You've reached the limit on the number of rules per server group you can associate with, resource {*resource*}, usage {*usage*}/{*tag*}. |The maximum number of forwarding rules that can be associated with a single server group has been reached. The resource is {*resource*}, {*usage*} used, quota: {*tag*}. |
|400 |QuotaExceed.ListenerPerCustomizedCfg |You've reached the limit on the number of listeners per CustomizedCfg you can associate with, resource {*resource*}, usage {*usage*}/{*tag*}. |The maximum number of listeners that can be associated with a single custom configuration has been reached. The resource is {*resource*}, {*usage*} used, quota: {*tag*}. |
|400 |QuotaExceed.ListenerPerAcl |You've reached the limit on the number of listeners per ACL you can associate with, resource {*resource*}, usage {*usage*}/{*tag*}. |The maximum number of listeners that can be associated with a single ACL has been reached. The resource is {*resource*}, {*usage*} used, quota: {*tag*}. |
|400 |QuotaExceed.RulePerInstanceForClone |You've reached the limit on the number of rules per ALB you can create in for clone, resource {*resource*}, usage {*usage*}/{*tag*}. |The maximum number of forwarding rules that can be created per cloned instance has been reached. The resource is {*resource*}, {*usage*} used, quota: {*tag*}. |
|400 |QuotaExceed.ServerPerInstanceForClone |You've reached the limit on the number of backend servers per ALB you can associate with for clone, resource {*resource*}, usage {*usage*}/{*tag*}. |The maximum number of backend servers that can be associated with a single cloned instance has been reached. The resource is {*resource*}, {*usage*} used, quota: {*tag*}. |
|400 |QuotaExceed.ListenerPerInstanceForClone |You've reached the limit on the number of listeners per ALB you can add in for clone, resource {*resource*}, usage {*usage*}/{*tag*}. |The maximum number of listeners that can be created per cloned ALB instance has been reached. The resource is {*resource*}, {*usage*} used, quota: {*tag*}. |
|400 |OperationDenied.CloneLoadBalancer |The request on the specified LoadBalancer is denied due to the LoadBalancer is associated with different EIP attributes. |The operation request for this ALB instance was rejected because the EIPs bound to the ALB instance have inconsistent properties. |
|400 |InvalidLoadBalancer.InvalidStatus |The specified LoadBalancer is not in the correct status for the request. |The specified ALB is in a state that cannot respond to this request. |
|400 |OperationDenied.ZoneTypeConflict |The request on the specified LoadBalancer is denied due to standard zones and local zones cannot be specified at the same time. |The operation request for this ALB instance was rejected because standard availability zones and local availability zones cannot coexist. |
|400 |DryRunOperation |Exception raised to indicate a successfully authorized action when the DryRun flag is set to true. |This request is set to DryRun. The action is authorized but not executed. |
|400 |InsufficientIpInSubnet |The specified subnet does not contain enough free private IP addresses to fulfill your request. |The available IPs under the specified subnet are insufficient. |
|403 |Forbidden |You are not authorized to clone LoadBalancer. |You do not have permission to clone the ALB instance. |
|404 |InvalidBandwidthPackage.NotFound |The specified BandwidthPackage does not exist. |The specified Bandwidth Package does not exist. |
|404 |InvalidVpc.NotFound |The specified VPC does not exist. |The specified VPC does not exist. |
|404 |InvalidSubnet.NotFound |The specified Subnet does not exist. |The specified subnet does not exist. |
|404 |InvalidProject.NotFound |The specified Project does not exist. |The specified project does not exist. |
|404 |InvalidRegion.NotFound |The specified Region does not exist. |The specified Region does not exist. |
|404 |InvalidTopic.NotFound |The specified Topic does not exist. |The specified log topic does not exist. |
|404 |InvalidEip.NotFound |The specified EIP does not exist. |The specified EIP does not exist. |
|404 |InvalidLoadBalancer.NotFound |The specified LoadBalancer does not exist. |The specified ALB instance does not exist. |
|500 |InternalError |An internal error has occurred. |An internal error occurred. Please try again later or contact an engineer for further consultation. |
