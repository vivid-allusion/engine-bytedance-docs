---
title: "CreateLoadBalancer - Creating a CLB"
product: "Cloud Load Balancer"
product_code: "clb"
source: "https://docs.byteplus.com/en/docs/clb/CreateLoadBalancer"
---

Call the CreateLoadBalancer API to create a CLB instance.

## Instructions

By default, you can create up to 60 CLB instances per account per region. If the default quota cannot meet your needs, go to [Quota Center](https://console.byteplus.com/quota/productList/coParameterList?ProviderCode=VPC) to increase the corresponding quota.

## Debug

[去调试](https://api.byteplus.com/api-explorer/debug?action=CreateLoadBalancer&serviceCode=clb&version=2020-04-01&groupName=)

## Request parameters

**Action ** String必选 `Example: CreateLoadBalancer`

Action to execute. Set the value to **CreateLoadBalancer**.

**Version ** String必选 `Example: 2020-04-01`

API version. The current version is **2020\-04\-01**.

**ExclusiveClusterId ** String`optional` `Example: ec-bp1o94dp5i6ea****`

The ID of the exclusive cluster to which the CLB instance belongs.

* You can call the [DescribeExclusiveClusters](https://docs.byteplus.com/en/docs/6406/112134) API to query the exclusive cluster ID.

* This parameter is passed only when creating a CLB instance of the exclusive cluster type.

> **tip**

> The exclusive cluster feature is currently in beta stage and only supports trial applications from accounts that have completed enterprise certification. If you need a trial, please contact the account manager.

**RegionId ** String必选 `Example: cn-shanghai`

Request region.

**ZoneType ** String`optional` `Example: active-standby`

Availability zone type of the CLB instance.

* single: Single availability zone.

* active\-standby: Primary and secondary availability zone.

* If not specified: when the specified region is deployed in a single availability zone, the default is "single"; when the specified region is deployed in multiple availability zones, the default is "active\-standby".

> **tip**

> The feature supporting single\-AZ deployment for CLB is currently in beta stage. To request a trial, please contact your account manager.

**MasterZoneId ** String`optional` `Example: cn-shanghai-a`

Primary Availability Zone ID of the CLB instance. For information on the availability zones currently supported in each region, see [Regions and availability zones](https://docs.byteplus.com/en/docs/clb/Product-Overview-08).

* The value cannot be the same as that of the `SlaveZoneId` parameter.

* If left empty, the availability zone of the subnet is assigned as the primary availability zone by default.

**SlaveZoneId** String `optional` `Example: cn-beijing-b`

Secondary Zone ID of the CLB Instance.

* If this parameter is passed, the `MasterZoneId` parameter must also be passed, and its value cannot be the same as that of the `MasterZoneId` parameter.

* If left empty, the behavior is as follows:

   * If the specified region is deployed in a single availability zone, this parameter is empty, and a single\-AZ CLB instance is created.

   * If the specified region is deployed in multiple availability zones and `ZoneType` is set to "single", this parameter is empty, and a single\-AZ CLB instance is created.

   * If the specified region is deployed in multiple availability zones and `ZoneType` is set to "active\-standby", the standby availability zone is randomly assigned from the availability zones supported by the specified region.

**LoadBalancerName ** String`optional` `Example: clb-test`

Name of the CLB instance.

* Must start with a letter, number, or Chinese character. May include letters, numbers, Chinese characters, and the following symbols: periods (.), underscores (_), and hyphens (\-).

* Length limit is 1 to 128 characters.

* If left blank, it defaults to the instance ID.

**Description ** String`optional` `Example: This is a LB.`

Description of the CLB instance.

* Must start with a letter, number, or Chinese character. May include letters, numbers, Chinese characters, and the following symbols: commas (,), periods (.), underscores (_), spaces ( ), equal signs (=), hyphens (\-), full\-width commas ( ， ), and full\-width periods ( 。 ).

* The length limit is 0 to 255 characters.

* If left blank, it defaults to an empty string.

**LoadBalancerBillingType ** Integer`optional` `Example: 2`

Billing methods of the CLB instance. Values:

* 1: Subscription

* 2 (default): Pay\-by\-Specification

* 3: Pay\-by\-CU

> **tip**

> Pay\-by\-CU is in the beta stage. To request a trial, please contact your account manager.

**PeriodUnit ** String`optional` `Example: Month`

The unit of duration for purchasing a subscription CLB instance.

This parameter is valid only when `LoadBalancerBillingType` is set to 1. Values:

* Month (default)

* Year

**Period ** Integer`optional` `Example: 1`

The duration for purchasing a subscription CLB instance. Default: 1.

* When `PeriodUnit` is set to Month, the value range is 1\-9, 12, 24, and 36.

* When `PeriodUnit` is set to Year, valid values range from 1 to 3.

**LoadBalancerSpec** String `optional` `Example: small_1`

CLB instances come in different specifications, each offering different forwarding performance. For more information, see [Product type and specification](https://docs.byteplus.com/en/docs/clb/Product-Overview-02).

* small_1: Small I

* small_2: Small II

* medium_1: Medium I

* medium_2: Medium II

* large_1: Large I

* large_2: Large II

> **tip**

> When `LoadBalancerBillingType` is set to 3, this parameter does not need to be passed; it defaults to clb_lcu (which means a single instance provides up to 1 million concurrent connections, 100,000 new connections, 10 Gbps inbound/outbound bandwidth, and 100,000 QPS by default).

**Type ** String必选 `Example: private`

Type of the CLB instance. Values:

* public: Internet type. When creating a public network type CLB instance, the system assigns an EIP address for forwarding public network requests.

* private: VPC type. When creating a private network type CLB instance, you need to bind an EIP address to it before it can forward public network requests.

**AddressIpVersion ** String`optional` `Example: ipv4`

IP address type of the CLB instance. Values:

* ipv4 (default): CLB is of IPv4 type and only supports forwarding IPv4 requests.

* DualStack: Indicates that the CLB is a dual\-stack type, supporting forwarding of both IPv4 and IPv6 requests. DualStack can be passed only when the parameter `Type` is set to private.

**VpcId ** String`optional` `Example: vpc-bp1aevy8sofi8mh1****`

The VPC ID to which the CLB instance belongs.

* You can call the [DescribeVpcs](https://docs.byteplus.com/en/docs/vpc/DescribeVpcs) API to query the VPC ID.

* If not specified, the default is the VPC ID to which the subnet belongs.

**SubnetId ** String必选 `Example: subnet-bp12mw1f8k3jgy****`

The subnet ID within the VPC to which the CLB instance belongs.

* The private IP address of the CLB instance will be allocated from the CIDR block of this subnet.

* You can call the [DescribeSubnets](https://docs.byteplus.com/en/docs/vpc/DescribeSubnets) API to query subnet IDs.

**EniAddress ** String`optional` `Example: 192.XX.XX.06`

Private IPv4 address of the CLB instance.

* Specify an available IPv4 address from the subnet.

* If not specified, an inactive IPv4 address will be automatically allocated from the subnet.

**EniAddressNum ** Integer`optional` `Example: 2`

The number of private IPv4 addresses of the CLB instance. Automatically allocate the specified number of inactive IPv4 addresses from the subnet.

* This parameter takes effect only when `Type` is set to private and `EniAddress` is not passed.

* Value range: 1\-5. Default: 1.

* This parameter is currently in beta stage, available exclusively for completing [Enterprise certification](https://docs.byteplus.com/en/docs/6261/64937) accounts for trial use. If you need a trial, please contact the account manager.

**EniIpv6Address ** String`optional` `Example: 2408:4005:XX:XX:200`

Private IPv6 address of the CLB instance.

* This parameter is valid when the parameter `AddressIpVersion` is set to DualStack.

* Specify an available private IPv6 address from the subnet.

* If left blank, an available private IPv6 address will be automatically allocated from the subnet.

**EipBillingConfig.ISP ** String`optional` `Example: BGP`

ISP of the EIP address.

This parameter is valid only when the parameter `Type` is set to public. Values:

* BGP (default): BGP multi\-ISP

* ChinaMobile: China Mobile static single ISP

* ChinaTelecom: China Telecom static single ISP

* ChinaUnicom: China Unicom static single ISP

* SingleLine_BGP: BGP single ISP

* Static_BGP: Static BGP

> **tip**

> Except for BGP (Multi\-ISP), other ISPs are currently in beta stage. To request a trial, please contact your account manager.

**EipBillingConfig.EipBillingType ** Integer`optional` `Example: 2`

The metering method of the EIP.

This parameter is valid only when the parameter `Type` is set to public.

* When the parameter `LoadBalancerBillingType` is set to 1, this parameter is required and must be 1, indicating subscription.

* When the parameter `LoadBalancerBillingType` is set to 2 or 3:

   * 2: Pay\-by\-bandwidth.

   * 3: Pay\-by\-data\-transfer.

   * If left blank, it defaults to 2.

**EipBillingConfig.Bandwidth ** Integer`optional` `Example: 10`

The bandwidth cap of the EIP, with a default value of 1, in Mbps.

* When the parameter `EipBillingConfig.EipBillingType` is set to 2, the bandwidth value range is 1 to 500.

* When `EipBillingConfig.EipBillingType` is set to 3, bandwidth ranges from 1 to 200.

**EipBillingConfig.BandwidthPackageId ** String`optional` `Example: bwp-2zeo05qre24nhrqpy****`

The ID of the bandwidth package to which the EIP will be added.

* This parameter is valid only when the parameter `EipBillingConfig.EipBillingType` is set to 2 or 3.

* You can call the [DescribeBandwidthPackages](https://docs.byteplus.com/en/docs/bandwidthpackage/DescribeBandwidthPackages) API to query the Bandwidth Package ID.

**EipBillingConfig.SecurityProtectionTypes.N ** String`optional` `Example: AntiDDoS_Enhanced`

The protection type of the EIP.

This parameter is valid only when the parameter `EipBillingConfig.EipBillingType` is set to 2 or 3. Values:

* AntiDDoS_Enhanced: Enhanced protection type. An EIP of this type can be added to an Anti\-DDoS Origin (Enterprise Edition) instance.

* If not specified, the EIP is of the Anti\-DDoS Basic type.

Parameter \-N: Indicates the serial number of security protection types. Currently, only the value 1 is supported.

> **tip**

> The enhanced protection feature for EIP is in beta stage. If you need a trial, please contact your account manager.

**EipBillingConfig.SecurityProtectionInstanceId ** Integer`optional` `Example: 20`

ID of the Anti\-DDoS Origin (Enterprise Edition) instance.

* When the parameter `EipBillingConfig.SecurityProtectionTypes.N` is set to AntiDDoS_Enhanced, this parameter is valid and required.

* You can call the [DescInstanceList](https://docs.byteplus.com/en/docs/6352/1263659) API to query the IDs of Anti\-DDoS Origin (Enterprise Edition) instances.

**ModificationProtectionStatus ** String`optional` `Example: ConsoleProtection`

Enable console modification protection for the CLB instance. After enabling, modifying or deleting the instance via the console is prohibited. Values:

* NonProtection: Disabled.

* ConsoleProtection: Enable.

* If not specified, the default is empty, meaning it is not enabled.

**ModificationProtectionReason ** String`optional` `Example: managed instance`

The reason for setting console modification protection.

This parameter is valid only when the parameter `ModificationProtectionStatus` is set to ConsoleProtection.

* Must start with a letter, number, or Chinese character. May include letters, numbers, Chinese characters, and the following symbols: half\-width periods (.), underscores (_), and hyphens (\-).

* Length limit: 1 to 80 characters.

**ProjectName ** String`optional` `Example: default`

The name of the project to which the CLB instance belongs. If left blank, it defaults to the default project.

**Tags.N.Key ** String`optional` `Example: key1`

The tag key of the custom tag.

* N represents the sequence number of a tag key. Valid range: 1 to 20.

* Separate multiple tag keys with &.

* Must not start with `volc:` or `sys:` in any case form.

* Must be 1 to 128 characters. May include characters (any language), numbers, spaces ( ), underscores (_), periods (.), half\-width colons (:), slashes (/), equal signs (=), plus signs (+), hyphens (\-), and at signs (@).

* If a tag key contains leading or trailing spaces, the system will automatically delete them.

> **tip**

> Duplicate tag keys are not allowed for the same resource.

**Tags.N.Value ** String`optional` `Example: value1`

The tag value of the custom tag.

* N represents the sequence number of a tag value. Valid range: 1–20.

* Separate multiple tag values with ampersands (&).

* Must be 0 to 256 characters. If left blank, this parameter defaults to an empty string.

* The following characters are allowed: characters from all languages, numbers, spaces ( ), underscores (_), periods (.), colons (:), forward slashes (/), equal signs (=), plus signs (+), hyphens (\-), and the at symbol (@).

* Case\-sensitive.

* If a tag value starts or ends with a space, the system will automatically delete it.

> **tip**

> To pass in this parameter, pass in `Tags.N.Key` first.

**BypassSecurityGroupEnabled ** String`optional` `Example: off`

CLB instance enables the "Allow Backend Security Group Traffic" feature.

* on: Enable. After enabling, the security group of the ECSs in the backend server group (server type only) no longer checks CLB traffic; it is allowed by default.

* off (default): Disable.

**TimestampRemoveEnabled ** String`optional` `Example: off`

Whether to enable the function of stripping TCP/HTTP/HTTPS packet timestamps

* on: Enable.

* off (default): Disable.

> **tip**

> This feature is currently in Beta stage. For trial requests, please contact your account manager.

**ClientToken ** String`optional` `Example: 123e4567-e89b-12d3-a456-42665544****`

The Client Token that is used to ensure the request idempotency.

* This parameter value is auto\-generated by the client. Ensure uniqueness across requests, preventing duplicate actions caused by multiple client retries during API timeouts or server internal errors.

* Must not exceed 64 ASCII characters.

* If you do not set this parameter, idempotency check is not performed.

## Response parameters

**LoadBalancerId ** String`Example: clb-bp1o94dp5i6ea****`

CLB Instance ID.

**RequestId ** String`Example: 20210811152539010225146063030****`

Request ID.

**OrderId ** String`Example: Order705261343570982****`

The order ID.

> **tip**

> This parameter is returned only when `LoadBalancerBillingType` is set to 1.

## Request examples

```json
GET /?Action=CreateLoadBalancer&Version=2020-04-01&Type=private&LoadBalancerName=clb-test&VpcId=vpc-bp1aevy8sofi8mh1****&SubnetId=subnet-bp12mw1f8k3jgy****&LoadBalancerSpec=small_1&LoadBalancerBillingType=2 HTTP/1.1
Host: clb.cn-beijing.byteplusapi.com.cn
X-Date: 20251121T094038Z
Authorization: HMAC-SHA256 Credential=Adfks******wekfwe/20251121/cn-beijing/clb/request, SignedHeaders=host;x-date, Signature=47a7d934ff7b37c03938******cd7b8278a40a1057690c401e92246a0e41085f
```

## Response examples

```json
{
    "ResponseMetadata": {
        "RequestId": "20230604110420****100232280022D31",
        "Action": "CreateLoadBalancer",
        "Version": "2020-04-01",
        "Service": "clb",
        "Region": "cn-beijing"
    },
    "Result": {
        "LoadBalancerId": "clb-bp1o94dp5i6ea****",
        "OrderId": "Order705261343570982****",
        "RequestId": "20210811152539010225146063030****"
    }
}
```

## Error codes

This section displays only the error codes of the current API. For more error codes, see [Common error codes](https://docs.byteplus.com/en/docs/clb/Public-error-codes).

|Status code |Error codes |Error message |Notes |
|---|---|---|---|
|400 |IdempotentParameterMismatch |Arguments on this idempotent request are inconsistent with arguments used in previous request(s). |The parameters of this idempotent request are inconsistent with those used in the previous request. |
|400 |InvalidAddressIpVersion.Malformed |The specified AddressIpVersion is malformed. |The specified AddressIpVersion parameter format is invalid. |
|400 |InvalidAllowedPorts.Conflict |The specified AllowedPorts has conflict. |The specified allowed port ranges overlap. |
|400 |InvalidAllowedPorts.Malformed |The specified AllowedPorts is malformed. |The specified AllowedPorts parameter format is invalid. |
|400 |InvalidBandwidth.Malformed |The specified Bandwidth is malformed. |The format specified for Bandwidth is invalid. |
|400 |InvalidBypassSecurityGroupEnabled.Malformed |The specified BypassSecurityGroupEnabled is malformed. |The specified BypassSecurityGroupEnabled parameter format is invalid. |
|400 |InvalidBypassSecurityGroupEnabled.NotSupport |The specified LoadBalancer does not support BypassSecurityGroupEnabled. |The specified CLB does not support the Bypass security group feature. |
|400 |InvalidClientToken.Malformed |The specified ClientToken is malformed. |The specified ClientToken format is invalid. |
|400 |InvalidCount.Malformed |The specified Count is malformed. |The specified Count parameter format is invalid. |
|400 |InvalidEip.InvalidStatus |The specified Eip is not in the correct status for the request. |The specified EIP cannot respond to this request due to its status. |
|400 |InvalidEipBillingConfig.Bandwidth.Malformed |The specified EipBillingConfig.Bandwidth is malformed. |The specified EipBillingConfig.Bandwidth parameter format is invalid. |
|400 |InvalidEipBillingConfig.EipBillingType.Malformed |The specified EipBillingConfig.EipBillingType is malformed. |The specified EipBillingConfig.EipBillingType format is invalid. |
|400 |InvalidEipBillingConfig.SecurityProtectionInstanceId.Malformed |The specified EipBillingConfig.SecurityProtectionInstanceId is malformed. |The specified EipBillingConfig.SecurityProtectionInstanceId parameter format is invalid. |
|400 |InvalidEipBillingType.Malformed |The specified EipBillingType is malformed. |The specified EipBillingType parameter format is invalid. |
|400 |InvalidEipId.Malformed |The specified EipId is malformed. |The specified EipId parameter format is invalid. |
|400 |InvalidEniAddress.Malformed |The specified EniAddress is malformed. |The specified EniAddress parameter format is invalid. |
|400 |InvalidEniAddressNum.Malformed |The specified EniAddressNum is malformed. |The specified EniAddressNum parameter format is invalid. |
|400 |InvalidEniIpv6Address.Malformed |The specified EniIpv6Address is malformed. |The specified EniIpv6Address parameter format is invalid. |
|400 |InvalidExclusiveCluster.UnSupportAction |The specified ResourceType does not support this action. |The specified exclusive cluster does not support the current operation. |
|400 |InvalidISP.Malformed |The specified ISP is malformed. |The specified ISP parameter format is invalid. |
|400 |InvalidIncorrectOrder.Malformed |The specified index order is malformed. |The specified index order parameter format is invalid. |
|400 |InvalidLoadBalancer.InvalidStatus |The specified LoadBalancer is not in the correct status for the request. |The specified load balancer cannot respond to this request due to its status. |
|400 |InvalidLoadBalancerBillingType.Malformed |The specified LoadBalancerBillingType is malformed. |The specified LoadBalancerBillingType parameter format is invalid. |
|400 |InvalidLoadBalancerDescription.Malformed |The specified LoadBalancerDescription is malformed. |The specified LoadBalancerDescription parameter format is invalid. |
|400 |InvalidLoadBalancerName.Malformed |The specified LoadBalancerName is malformed. |The specified LoadBalancerName format is invalid. |
|400 |InvalidLoadBalancerSpec.Malformed |The specified LoadBalancerSpec is malformed. |The specified LoadBalancerSpec parameter format is invalid. |
|400 |InvalidMasterZoneId.Malformed |The specified MasterZoneId is malformed. |The specified MasterZoneId parameter format is invalid. |
|400 |InvalidModificationProtectionReason.Malformed |The specified ModificationProtectionReason is malformed. |The specified ModificationProtectionReason parameter format is invalid. |
|400 |InvalidModificationProtectionStatus.Malformed |The specified ModificationProtectionStatus is malformed. |The specified ModificationProtectionStatus format is invalid. |
|400 |InvalidParameter.AddressIpVersionConflictsEniAddressNum |The specified AddressIpVersion and EniAddressNum conflict. |The specified AddressIpVersion and EniAddressNum parameters conflict. |
|400 |InvalidParameter.EniAddressConflictsEniAddressNum |The specified EniAddress and EniAddressNum conflict. |The specified EniAddress and EniAddressNum parameters conflict. |
|400 |InvalidParameter.EniAddressNumConflictsType |The specified EniAddressNum and Type conflict. |The specified EniAddressNum and Type parameters conflict. |
|400 |InvalidPeriod.Malformed |The specified Period is malformed. |The specified Period format is invalid. |
|400 |InvalidPeriodUnit.Malformed |The specified PeriodUnit is malformed. |The specified PeriodUnit parameter format is invalid. |
|400 |InvalidProject.Malformed |The specified Project is malformed. |The format of the specified Project is invalid. |
|400 |InvalidQuotaCode.Malformed |The specified QuotaCode is malformed. |The specified QuotaCode parameter format is invalid. |
|400 |InvalidRegionId.Malformed |The specified RegionId is malformed. |The specified RegionId format is invalid. |
|400 |InvalidSlaveZoneId.Malformed |The specified SlaveZoneId is malformed. |The specified SlaveZoneId parameter format is invalid. |
|400 |InvalidSubnetIPv4Cidr.NotSupport |The specified subnet does not support ipv4 cidr. |The specified subnet does not support IPv4 CIDR blocks. |
|400 |InvalidSubnetIPv6Cidr.NotSupport |The specified subnet does not support ipv6 cidr. |The specified subnet does not support IPv6 CIDR blocks. |
|400 |InvalidSuffixIndex.Malformed |The specified SuffixIndex is malformed. |The specified SuffixIndex parameter format is invalid. |
|400 |InvalidTagKey.Malformed |The specified TagKey is malformed. |The specified TagKey parameter format is invalid. |
|400 |InvalidTagValue.Malformed |The specified TagValue is malformed. |The specified TagValue parameter format is invalid. |
|400 |InvalidTimestampRemoveEnabled.Malformed |The specified TimestampRemoveEnabled is malformed. |The specified TimestampRemoveEnabled parameter format is invalid. |
|400 |InvalidType.Malformed |The specified Type is malformed. |The specified Type parameter format is invalid. |
|400 |InvalidZoneType.Malformed |The specified ZoneType is malformed. |The specified ZoneType parameter format is invalid. |
|400 |LimitExceeded.LoadBalancerName |You've reached the limit on the length of LoadBalancerName, please shorten your LoadBalancerName or close UniqueSuffix. |CLB instance name length has been exceeded. Please shorten your instance name or disable the ordered suffix feature. |
|400 |LimitExceeded.ServiceManagedTag |You've reached the limit on the number of service managed tags that you can create. |You have reached the limit for the number of managed resource tag key\-value pairs that can be created in a single request. |
|400 |LimitExceeded.SuffixIndex |You've reached the limit on the number of SuffixIndex. |The maximum value of the ordered suffix serial number has been exceeded. |
|400 |LimitExceeded.TagOperation |You've reached the limit on the number of tags that you can operate at a time. |You have reached the maximum number of tag entries that can be operated on in a single request. |
|400 |MissingParameter |The request is missing a required parameter. Ensure that you have supplied all the required parameters for the request; for example, the 'RegionId'. |This request does not contain required parameters. Please ensure the request includes all required parameters, such as RegionId. |
|400 |MissingParameter |The request is missing a required parameter. Ensure that you have supplied all the required parameters for the request; for example, the 'SubnetId'. |This request does not contain required parameters. Confirm that this request contains all required parameters (such as SubnetId). |
|400 |MissingParameter |The request is missing a required parameter. Ensure that you have supplied all the required parameters for the request; for example, the 'Type'. |This request is missing a required parameter. Please ensure that all required parameters, such as Type, are provided in the request. |
|400 |MissingParameter |The request is missing a required parameter. Ensure that you have supplied all the required parameters for the request; for example, the 'MasterZoneId'. |This request is missing a required parameter. Please ensure the request includes all required parameters, such as MasterZoneId. |
|400 |MissingParameter |The request is missing a required parameter. Ensure that you have supplied all the required parameters for the request; for example, the ''. |This request is missing a required parameter. Ensure the request includes all required parameters, such as . |
|400 |OrderError.OrderPay |Failed to create order and pay. |The order payment failed. |
|400 |OrderError.PreOrder |Failed to create a preorder. |Order placement failed. |
|400 |QuotaExceed.AllowedPortNumberEachInstance |You've reached the limit on the number of AllowedPort that you can operate. |The maximum number of configurable allowed port ranges has been reached. |
|400 |QuotaExceed.Eip |You've reached the limit on the number of EIP that you can create. |The quota limit for the number of EIP instances that can be created has been reached. |
|400 |QuotaExceed.ExclusiveClusterInstanceNumber |You've reached the limit on the number of exclusive cluster instance that you can create. |The quota limit for the number of load balancer instances that can be created in an exclusive cluster has been reached. |
|400 |QuotaExceed.InstanceNumber |You've reached the limit on the number of instance that you can create. |You have reached the quota limit for the number of load balancer instances that can be created. |
|400 |QuotaExceed.XLargeOneInstanceNumber |You've reached the limit on the number of xlarge_1 instance that you can create. |The quota limit for the number of ultra\-large I CLB instances that can be created has been reached. |
|400 |QuotaExceed.XLargeTwoInstanceNumber |You've reached the limit on the number of xlarge_2 instance that you can create. |The quota limit for the number of ultra\-large II CLB instances that can be created has been reached. |
|400 |UnsupportedOperation |The request on the specified instance is denied due to the account balance and available vouchers are less than 100 yuan in total. |The action request on this instance is denied due to the sum of both account balance and available coupons being less than USD 100. |
|400 |UnsupportedOperation |The request on the specified instance is denied due to the account in arrears status. |The action request on this instance is denied because the account is in arrears. |
|400 |UnsupportedOperation.AccountArrears |The request on the specified instance is denied due to the account balance and available vouchers are less than 100 yuan in total. |The action request on this instance is denied due to the sum of both account balance and available coupons being less than USD 100. |
|400 |UnsupportedOperation.AccountArrears |The request on the specified instance is denied due to the account in arrears status. |The action request on this instance is denied because the account is in arrears. |
|400 |UnsupportedOperation.MainAccountNotSupportPaypal |You are requested to contact the main account to provide an alternative payment method other than Paypal before enabling the pay\-as\-you\-go products in BytePlus. |本次下单的后付费商品不支持 Paypal 支付，请联系主账号补充其他支付方式。 |
|400 |UnsupportedOperation.NotSupportPaypal |You are requested to provide an alternative payment method other than Paypal before enabling the pay\-as\-you\-go products in BytePlus. |本次下单的后付费商品不支持 Paypal 支付，请补充其他支付方式。 |
|403 |Forbidden |You are not authorized to perform operations on the specified service; for example, the 'AllowedPorts'. |No permission to operate on the specified service, such as AllowedPorts. |
|403 |Forbidden |You are not authorized to perform operations on the service managed tag. |No permission to tag the specified resource with managed tags. |
|403 |Forbidden |You are not authorized to perform operations on the specified service; for example, the 'MasterZone'. |No permission to operate on the specified service, such as MasterZone. |
|403 |Forbidden |You are not authorized to perform operations on the specified service; for example, the 'SlaveZone'. |No permission to operate on the specified service, such as SlaveZone. |
|403 |Forbidden |You are not authorized to perform operations on the specified service; for example, the 'TimestampRemoveEnabled'. |No permission to operate on the specified service, such as TimestampRemoveEnabled. |
|403 |Forbidden |You are not authorized to perform operations on the specified service. |You do not have permission to perform operations on the specified service. |
|403 |Forbidden |You are not authorized to perform operations on the specified service; for example, the 'EniAddressNum'. |No permission to operate on the specified service, such as EniAddressNum. |
|403 |Forbidden |You are not authorized to perform operations on the specified service; for example, the 'Region'. |No permission to operate on the specified service, such as Region. |
|403 |Forbidden |The operation of public type is forbidden. |Internet\-related operations are prohibited. |
|403 |Forbidden |You are not authorized to perform operations on the system tag. |No permission to tag the specified resource with a system tag. |
|404 |InvalidCluster.NotFound |The specified Cluster does not exist. |The specified cluster does not exist. |
|404 |InvalidDispatchUnit.NotFound |The specified DispatchUnit does not exist. |The specified scheduling unit does not exist. |
|404 |InvalidEip.NotFound |The specified Eip does not exist. |The specified EIP does not exist. |
|404 |InvalidEipBillingType.NotFound |The specified EipBillingType does not exist. |The specified EIP billing method does not exist. |
|404 |InvalidExclusiveCluster.NotFound |The specified ExclusiveCluster does not exist. |The specified Exclusive Cluster does not exist. |
|404 |InvalidLoadBalancer.NotFound |The specified LoadBalancer does not exist. |The specified load balancer does not exist. |
|404 |InvalidProject.NotFound |The specified Project does not exist. |The specified project does not exist. |
|404 |InvalidSubnet.NotFound |The specified Subnet does not exist. |The specified subnet does not exist. |
|404 |InvalidVPC.NotFound |The specified VPC does not exist. |The specified VPC does not exist. |
|404 |InvalidZone.NotFound |The specified Zone mapping does not exist. |The specified primary\-secondary availability zone relationship does not exist. |
|409 |InvalidAllowedPort.Conflict |The specified AllowedPort already exists. |The specified allowed port range already exists. |
|412 |IdempotentProcessing |The request uses the same client token as a previous one that is still in process. |The idempotent request is in progress. |
|412 |InvalidExclusiveCluster.Expired |The specified ExclusiveCluster has expired. |The specified Exclusive Cluster has expired. |
|412 |InvalidExclusiveCluster.UnPurchased |The specified ExclusiveCluster is not purchased. |The specified Exclusive Cluster is not purchased. |
|500 |InternalError |An internal error has occurred. |An internal error occurred. |
