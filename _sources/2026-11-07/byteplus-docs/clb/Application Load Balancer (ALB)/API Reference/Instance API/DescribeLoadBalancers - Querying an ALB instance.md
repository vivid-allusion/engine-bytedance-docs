---
title: "DescribeLoadBalancers - Querying an ALB instance"
product: "Cloud Load Balancer"
product_code: "clb"
source: "https://docs.byteplus.com/en/docs/clb/ALB-DescribeLoadBalancers"
---

Call the DescribeLoadBalancers API to query the ALB instances.

## Instructions

* Submit up to 200 API requests per second.

* Pass in multiple request parameters, query based on the passed parameters, and return ALB instances that meet all the conditions. If no ALB instance meets the conditions, return an empty value.

* If none of the non\-required request parameters are passed, query based on the currently logged\-in account and return all ALB instances under the current account.

## Debug

[去调试](https://api.byteplus.com/api-explorer/?action=DescribeLoadBalancers&groupName=%E5%AE%9E%E4%BE%8B&serviceCode=alb&version=2020-04-01)

## Request parameters

The following only details request parameters specific to this API and key common parameters. More information can be found in [Common parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).

**Action ** string必选 `Example: DescribeLoadBalancers`

Action to execute. Set the value to DescribeLoadBalancers.

**Version ** string必选 `Example: 2020-04-01`

The API version. Value: 2020\-04\-01.

**EniAddress ** string`optional` `Example: 192.168.XX.XX`

Private IP address of the ALB instance.

**LoadBalancerIds.N ** string[]`optional` `Example: LoadBalancerIds.1=alb-bp1b6c719dfa08ex****&LoadBalancerIds.2=alb-2fea2u2m4qhog5oxruuoo****`

ALB instance ID.

* Parameter \-N: Indicates the serial number of the ALB instance ID, ranging from 1 to 20, meaning up to 20 instance IDs can be queried when specified.

* Separate multiple ALB instance IDs with ampersands (&).

**LoadBalancerName ** string`optional` `Example: ls-test`

Name of the ALB instance.

**PageNumber ** integer`optional` `Example: 1`

The page number of the list. Default: 1.

**PageSize ** integer`optional` `Example: 10`

The number of rows per page when paginating queries. Value range: 1 to 100. Default: 10.

**TagFilters.N.Key ** string[]`optional` `Example: TagFilters.1.Key=k1&TagFilters.2.Key=k2`

The tag key.

* N represents the sequence number of a tag key. Values: 1\-10.

* Separate multiple tag keys with &. Multiple tag keys have a logical AND relationship. The query returns ALBs tagged with all the specified keys.

* Duplicate values are not allowed.

**VpcId ** string`optional` `Example: vpc-13fd2oy7du4ye****`

VPC ID to which the ALB instance belongs.

**TagFilters.N.Values.N ** string[]`optional` `Example: TagFilters.1.Values.1=v1&TagFilters.1.Values.2=v2& TagFilters.2.Values.1=v3`

The tag value of tag 2.

* The first N represents the serial number of the tag key. Valid values: 1–10.

* The second N represents the serial number of the tag value. Valid values: 1–3. Multiple tag values under the same tag key are combined using a logical OR operation, meaning the query returns ALBs that have any of the specified tag values for that key.

* Separate multiple tag values with an ampersand (&).

> **tip**

* > If this parameter is passed in, TagFilters.N.Key must be passed in first.

* > When an empty string is passed, it indicates querying ALB instances with empty tag values.

**EipAddress ** string`optional` `Example: 180.112.XX.XX`

EIP address of the ALB instance.

**Type ** string`optional` `Example: public`

Type of ALB instance. Valid values:

* public: public ALB.

* private: private ALB.

**SpaceNetworkId ** string`optional` `Example: csn-bpkdt37pq72zv****`

ID of the SpaceNetwork where the ArkClaw instance resides.

> **tip**

> This parameter is currently in Beta stage. For trial requests, please contact your account manager.

**ProjectName ** string`optional` `Example: default`

Name of the project to which the instance belongs.

## Response parameters

Only the response parameters specific to this API are listed below. More information, see [Response structure](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response).

**RequestId ** string`Example: 202108111103030****`

Request ID.

**PageSize ** integer`Example: 10`

The number of rows on the current page.

**PageNumber ** integer`Example: 1`

Current page number.

**TotalCount ** integer`Example: 50`

Total number of ALB instances that meet the criteria.

**LoadBalancers ** object[]`Example: --`

Details of ALB instances that meet the conditions.

**SecurityGroupIds ** string[]`Example: ["sg-bp67acfmxazb4p****"]`

Security group ID associated with the ALB instance.

**SpaceNetworkId ** string`Example: csn-bpkdt37pq72zv****`

ID of the SpaceNetwork where the ArkClaw instance resides.

**ArkClawEnabled ** string`Example: off`

Enable ArkClaw feature.

off: Disable.

on: Enable.

**LoadBalancerId ** string`Example: alb-bp1o94dp5i6ea****`

ALB instance ID.

**LoadBalancerName ** string`Example: alb-test1`

Name of the ALB instance.

**AddressIpVersion** string `Example: DualStack`

IP type of the ALB instance.

* IPv4: IPv4 type.

* DualStack: IPv4 & IPv6 dual\-stack type.

**Status ** string`Example: Active`

ALB instance status.

* Active: Running.

* Provisioning: Creating.

* Configuring: Pending.

* Deleting

* CreateFailed: Creation failed.

* Inactive: Disabled.

**Description ** string`Example: test`

Description of the ALB instance.

**CreateTime ** string`Example: 2021-08-11T16:37:37Z`

Creation time of the ALB instance.

**UpdateTime ** string`Example: 2021-08-11T16:37:37Z`

Last modified time of the ALB instance.

**Type ** string`Example: private`

Type of ALB instance.

**VpcId ** string`Example: vpc-bp1aevy8sh1****`

VPC ID to which the ALB instance belongs.

**SubnetId ** string`Example: subnet-bp12m3jgy****`

The subnet ID to which the ALB instance belongs.

> **tip**

> This parameter is deprecated. Please use the ZoneMappings field.

**EipId ** string`Example: eip-3ciyamrswwusg****`

EIP ID associated with the ALB instance.

> **tip**

> This parameter is deprecated. Please use the ZoneMappings field.

**EniAddress ** string`Example: 172.XX.XX.33`

Private IP address of the ALB instance.

> **tip**

> This parameter is deprecated. Please use the ZoneMappings field.

**EniId ** string`Example: eni-2fe6rabqt8c9f****`

Occupied Network interface ID of the ALB Instance.

> **tip**

> This parameter is deprecated. Please use the ZoneMappings field.

**EipAddress ** string`Example: 10.XX.XX.27`

EIP address of the ALB instance.

> **tip**

> This parameter is deprecated. Please use the ZoneMappings field.

**BusinessStatus ** string`Example: FinancialLocked`

The ALB instance is locked.

* Normal

* FinancialLocked: Being locked.

**LockReason ** string`Example: Financial`

The reason why the ALB instance is locked. This parameter returns a value only when the instance is in the FinancialLocked status.

* Financial: Being locked due to arrears.

* Security: Being locked due to security.

**OverdueTime ** string`Example: 2021-08-11T16:37:37Z`

The time when the ALB instance was frozen. This parameter returns a value only when the instance is in the FinancialLocked status.

**DeletedTime ** string`Example: 2021-08-11T16:37:37Z`

Expected reclaim time of the ALB instance. This parameter returns a value only when the instance is in the FinancialLocked status.

**LoadBalancerBillingType ** integer`Example: 1`

Billing method of the ALB instance.

1: Pay\-by\-LCU.

**DNSName** string `Example: alb-qwe1344.cn-beijing.volcenginealb.com`

DNS domain name.

**ZoneMappings ** object[]`Example: --`

Configuration information of the ALB instance across different availability zones.

**ZoneId ** string`Example: cn-beijing-a`

The availability zone where the ALB instance resides

**SubnetId ** string`Example: subnet-bp12m3jgy****`

Subnet ID of the ALB instance in this availability zone.

**LoadBalancerAddresses ** object[]`Example: --`

The IP address of the ALB instance in this availability zone.

**Ipv4LocalAddresses ** string[]`Example: ["172.XX.XX.34","172.XX.XX.35"]`

IPv4 local address list. The address list used by the ALB to communicate with backend services.

**Ipv6LocalAddresses ** string[]`Example: ["2408:4005:XX:XX:201","2408:4005:XX:XX:202"]`

IPv6 local address list. The address list used by the ALB to communicate with backend services.

**EniAddress ** string`Example: 172.XX.XX.33`

The private IP address of the ALB instance in this availability zone.

**EniId ** string`Example: eni-2fe6rabqt8g****`

The ID of the network interface occupied by the ALB instance in this availability zone.

**EipAddress ** string`Example: 10.XX.XX.27`

EIP address of the ALB instance in this availability zone.

**EipId ** string`Example: eip-2fe698wsnj****`

EIP ID of the ALB instance in this availability zone.

**Eip ** object`Example: --`

EIP information of the ALB instance in that availability zone.

**ISP ** string`Example: BGP`

ISPs for ALB Instance EIPs:

* BGP: BGP multi\-ISP.

**EipBillingType ** integer`Example: 2`

The metering method of the EIP.

* 2: Pay\-by\-bandwidth.

* 3: Pay\-by\-data\-transfer.

**Bandwidth ** integer`Example: 10`

The peak bandwidth of the EIP. Unit: Mbps

**EipAddress ** string`Example: 10.XX.XX.27`

EIP address of the CLB instance.

**SecurityProtectionTypes ** string[]`Example: -`

The protection type of the EIP.

* AntiDDoS_Enhanced: EIP with enhanced protection type, which can be added to a DDoS native protection instance.

* Empty value: EIP with basic protection type.

**EipType ** string`Example: anycast`

EIP type on the ALB instance. Supported values:

* empty: EIP.

* anycast: Anycast EIP.

**PopLocations ** object[]`Example: -`

The access point information associated when ALB acts as the origin of an Anycast EIP. Only valid when bound to Anycast EIP.

**PopId ** string`Example: cn-beijing-pop`

Access point ID of the Anycast EIP.

**PopName ** string`Example: Beijing-access point`

The access point name of the Anycast EIP.

**AssociationMode ** string`Example: Default`

The origin type when ALB acts as an Anycast EIP source. Only valid when bound to an Anycast EIP.

* Default: Default mode.

* Normal: Normal mode.

**EniIpv6Address ** string`Example: 2408:4005:XX:XX:200`

For an ALB instance of IPv4&IPv6 dual\-stack type, the IPv6 address in that availability zone.

**Ipv6EipId ** string`Example: eip-2fe698wsnj****`

The IPv6 internet bandwidth ID of the ALB public instance of IPv4&IPv6 dual\-stack type in this availability zone.

**Ipv6Eip ** object`Example: --`

For a public ALB instance of IPv4&IPv6 dual\-stack type, the IPv6 internet bandwidth information in that availability zone.

**Bandwidth ** integer`Example: 200`

The bandwidth upper limit of the IPv6 internet bandwidth for the public ALB instance, in Mbps.

**BillingType ** integer`Example: 2`

Billing method for IPv6 Internet Bandwidth of the ALB instance.

* 2: Pay\-by\-bandwidth\-cap.

* 3: Pay\-by\-data\-transfer.

**ISP ** string`Example: BGP`

ISP of the IPv6 internet bandwidth for the public ALB instance.

* BGP: BGP multi\-ISP.

**DeleteProtection ** string`Example: off`

The delete protection feature of the ALB instance is enabled or disabled.

* off: Disable.

* on: Enable.

**ProjectName ** string`Example: default`

Name of the project to which the instance belongs.

**Tags ** object[]`Example: -`

The tags associated with the instance.

**Key ** string`Example: key`

The tag key of the custom tag.

**Value ** string`Example: value`

The tag value of the custom tag.

**WafProtectionEnabled ** string`Example: off`

WAF protection switch.

* off: Disable.

* on: Enable.

**WafInstanceId ** string`Example: waf-14ca6f67c09****`

The ID of the WAF security protection instance bound to the ALB instance.

**ModificationProtectionStatus** string `Example: NonProtection`

Enable instance modification protection feature.

* NonProtection: Disabled.

* ConsoleProtection: Enabled.

**ModificationProtectionReason** string `Example: This is modification protection`

Reason for enabling instance modification protection.

**LoadBalancerEdition ** string`Example: Standard`

ALB instance edition.

* Basic: Basic edition.

* Standard: Standard edition.

**SniAutoMatch ** string `on`

Listeners under the instance support automatic selection of extended certificates.

**LocalAddresses ** string[]`Example: ["100.64.1.0/20", "xxx"]`

The origin address of the ALB instance.

**ProxyProtocolEnabled ** string`Example: off`

ALB supports the Proxy Protocol and can record the client's real IP address.

## Request example

```text
GET /?Action=DescribeLoadBalancers&Version=2020-04-01 HTTP/1.1
Host: alb.cn-beijing.byteplusapi.com.cn
X-Date: 20261027T113919Z
Authorization: HMAC-SHA256 Credential=Adfks******wekfwe/20261027/cn-beijing/alb/request, SignedHeaders=host;x-date, Signature=47a7d934ff7b37c03938******cd7b8278a40a1057690c401e92246a0e41085f
```

## Response examples

```json
{
    "ResponseMetadata": {
        "RequestId": "20210816110638****2514606306AF947C",
        "Action": "DescribeLoadBalancers",
        "Version": "2020-04-01",
        "Service": "alb",
        "Region": "cn-beijing"
    },   
    "Result": {
        "RequestId": "2021081117061401****2431470319AF3B",
        "PageNumber": 1,
        "PageSize": 2,
        "TotalCount": 21,
        "LoadBalancers": [
            {
                "LoadBalancerId": "alb-1g1f19vdq5****ibuxyek20wz",
                "LoadBalancerName": "test",
                "Status": "Active",
                "Description": "test ",
                "CreateTime": "2021-08-11T16:37:37Z",
                "UpdateTime": "2021-08-11T16:37:41Z",
                "Type": "public",
                "VpcId": "vpc-2fe624a318b****xruuoxjjug",
                "SubnetId": "subnet-2fe6iau****ls5oxruuyfo0dd",
                "EipID": "eip-1g1f19xc****c8ibuxy91k9rc",
                "EipAddress": "10.XX.XX.217",
                "EniID": "eni-2fe6rx****xc5oxruvejddd5",
                "EniAddress": "192.XX.XX.44",
                "BusinessStatus": "",
                "LockReason": "",
                "OverdueTime": "",
                "DeletedTime": "",
                "LoadBalancerBillingType": 1,
                "DNSName": "alb-t5aepy8j5****jdjavoc2c.cn-beijing.volcalb.com",
                "ZoneMappings": [
                    {
                        "ZoneId": "cn-beijing-a",
                        "SubnetId": "subnet-274tv****duyo7fap8sc658ze",
                        "LoadBalancerAddresses": [
                            {
                                "EniAddress": "192.168.0.25",
                                "EniId": "eni-274js****2xhc7fap8ssed7qg",
                                "EipAddress": "",
                                "EipId": "",
                                "Eip": null
                            }
                        ]
                    },
                    {
                        "ZoneId": "cn-beijing-b",
                        "SubnetId": "subnet-274up****b8xs7fap8t1odh1n",
                        "LoadBalancerAddresses": [
                            {
                                "EniAddress": "192.168.1.254",
                                "EniId": "eni-274js****6zgg7fap8t05movj",
                                "EipAddress": "",
                                "EipId": "",
                                "Eip": null
                            }
                        ]
                    }
                ]
            }
      }
}
```

## Error codes

The following table lists the error codes related to the business logic for this API. For details, see [Common error codes](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-error-codes).

|Status code |Error codes |Error message |Notes |
|---|---|---|---|
|400 |Invalid%s.Malformed |MismatchThe specified %s is malformed. |The specified %s parameter format is invalid. |
|400 |MissingParameter |The request is missing a required parameter. Ensure that you have supplied all the required parameters for the request; for example, '%s'. |This request does not contain required parameters. Ensure that your request includes all required parameters, such as: %s. |
|400 |InvalidParameter |Data unmarshal failed. |Failed to parse the request. |
|400 |InvalidPaging.Malformed |The specified PageNumber or PageSize is malformed. |The format specified for pagination parameter is invalid. |
|400 |InvalidLoadBalancerName.Malformed |The specified LoadBalancerName is malformed. |The specified LoadBalancerName format is invalid. |
|400 |InvalidEniAddress.Malformed |The specified EniAddress is malformed. |The specified EniAddress parameter format is invalid. |
|400 |LimitExceed.LoadBalancer |You've reached the limit on the number of loadbalancers that you can operate at a time. |The maximum number of ALB instances that can be operated on in a single request has been reached. |
|400 |LimitExceed.TagFilters.Values |You've reached the limit on the number of tag filter values that you can operate at a time. |You have reached the maximum number of tag values that can be operated on in a single request. |
|400 |LimitExceed.TagFilters |You've reached the limit on the number of tag filters that you can operate at a time. |The maximum number of tag filters that can be operated on at one time has been reached. |
|400 |InvalidTagFilters.Key.Malformed |The specified TagFilters.Key is malformed. |The specified TagFilters.Key parameter format is invalid. |
|400 |InvalidTags.Value.Malformed |The specified Tags.Value is malformed. |The specified Tags.Value parameter format is invalid. |
|400 |InvalidTags.Key.Duplicated |The specified Tags.Key is duplicated. |The specified Tags.Key is duplicated. |
|400 |InvalidEipAddress.Malformed |The specified EipAddress is malformed. |The specified EipAddress parameter format is invalid. |
|400 |OperationDenied.QueryConditionConflict |The request on the specified LoadBalancer is denied due to VpcId and SpaceNetworkId cannot be specified at the same time. |The operation request for this ALB instance is rejected because VpcId and SpaceNetworkId cannot be specified at the same time. |
|500 |InternalError |An internal error has occurred. |An internal error occurred. Please try again later or contact an engineer for further consultation. |
