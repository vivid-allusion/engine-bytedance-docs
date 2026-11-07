---
title: "DescribeLoadBalancerAttributes - Querying the details of ALB instances"
product: "Cloud Load Balancer"
product_code: "clb"
source: "https://docs.byteplus.com/en/docs/clb/ALB-DescribeLoadBalancerAttributes"
---

Call the DescribeLoadBalancerAttributes API to view the ALB instance details.

## Instructions

Submit up to 200 API requests per second.

## Debug

[去调试](https://api.byteplus.com/api-explorer/?action=DescribeLoadBalancerAttributes&groupName=%E5%AE%9E%E4%BE%8B&serviceCode=alb&version=2020-04-01)

## Request parameters

The following only details request parameters specific to this API and key common parameters. More information can be found in [Common parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).

**Action ** string必选 `Example: DescribeLoadBalancerAttributes`

Action to execute. Set the value to DescribeLoadBalancerAttributes.

**Version ** string必选 `Example: 2020-04-01`

The API version. Value: 2020\-04\-01.

**LoadBalancerId ** string必选 `Example: alb-bp1b608ex****`

ALB instance ID.

## Response parameters

Only the response parameters specific to this API are listed below. More information, see [Response structure](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response).

**RequestId ** string`Example: 202125146063030****`

Request ID.

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

**Description ** string`Example: Test`

Description of the ALB instance.

**CreateTime ** string`Example: 2021-08-11T16:37:37Z`

Creation time of the ALB instance.

**UpdateTime ** string`Example: 2021-08-11T16:37:37Z`

Last modified time of the ALB instance.

**Type ** string`Example: private`

Type of ALB instance.

* public: public ALB.

* private: private ALB.

**VpcId ** string`Example: vpc-bp1aevy8sofi8mh1****`

VPC ID to which the ALB instance belongs.

**SubnetId ** string`Example: subnet-bp11f8k3jgy****`

The subnet ID to which the ALB instance belongs.

> **tip**

> This parameter is deprecated. Please use the ZoneMappings field.

**EipId ** string`Example: eip-2fe698wsddsnj****`

The ID of the EIP.

> **tip**

> This parameter is deprecated. Please use the ZoneMappings field.

**EniAddress ** string`Example: 172.XX.XX.33`

Private IP address of the ALB instance.

> **tip**

> This parameter is deprecated. Please use the ZoneMappings field.

**EniId ** string`Example: eni-2fe6rabddqt8g****`

Occupied Network interface ID of the ALB Instance.

> **tip**

> This parameter is deprecated. Please use the ZoneMappings field.

**EipAddress ** string`Example: 10.XX.XX.27`

EIP address of the ALB instance.

> **tip**

> This parameter is deprecated. Please use the ZoneMappings field.

**BusinessStatus ** string`Example: FinancialLocked`

The ALB instance is locked. When this value is empty, the instance status is normal.

* Normal

* FinancialLocked: Being locked.

**LockReason ** string`Example: Financial`

Reason for the ALB instance freezing. This parameter returns a value only when the instance is in the FinancialLocked status.

* Financial: Being locked due to arrears.

* Security: Being locked due to security.

**OverdueTime ** string`Example: 2021-08-11T16:37:37Z`

Freeze time of the ALB instance. This parameter returns a value only when the instance is in the FinancialLocked status.

**DeletedTime ** string`Example: 2021-08-11T16:37:37Z`

Expected reclaim time of the ALB instance. This parameter returns a value only when the instance is in the FinancialLocked status.

**LoadBalancerBillingType ** integer`Example: 1`

Billing methods of the ALB instance.

1: LCU capacity unit

**Eip ** object`Example: -`

Information about the EIP address of the ALB instance.

**ISP ** string`Example: BGP`

ISP for ALB Instance EIP.

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

The EIP type of the ALB instance.

* Empty: EIP.

* anycast: Anycast EIP.

**PopLocations ** object[]`Example: -`

The access point information associated when ALB acts as the origin of an Anycast EIP.

**PopId ** string`Example: cn-beijing-pop`

Access point ID of the Anycast EIP.

**PopName ** string`Example: beijing-pop`

The access point name of the Anycast EIP.

**AssociationMode ** string`Example: Default`

The origin type when ALB acts as an Anycast EIP source. Only valid when bound to an Anycast EIP.

* Default: Default mode.

* Normal: Normal mode.

**Listeners ** object[]`Example: -`

Information about the listeners in the ALB instance.

**ListenerId ** string`Example: lsn-2fea4ayvu2g3k5oxruuze****`

ID of the listener in the ALB instance.

**ListenerName ** string`Example: listener-1`

Name of the listener in the ALB instance.

**AccessLog ** object`Example: -`

Information about the access logs in the ALB instance.

**BucketName ** string`Example: alb-tos`

The name of the TOS storing Layer\-7 access logs.

**Enabled ** boolean`Example: true`

Enable access log.

* true: Enabled

* false: Disabled.

**TLSAccessLog ** object`Example: -`

Information about the access logs in the ALB instance.

**Enabled ** boolean`Example: true`

Enable access log delivery to TLS.

* true: Enabled

* false: Disabled.

**ProjectId ** string`Example: project-xxxx`

TLS project ID bound to the access log.

**TopicId ** string`Example: topic-xxxxx`

TLS topic ID bound to the access log.

**HealthLog ** object`Example: -`

Health check log information in the ALB instance.

**Enabled ** boolean`Example: true`

Enable access log.

* true: Enabled

* false: Disabled.

**ProjectId ** string`Example: project-xxxx`

TLS project ID bound to the health check log.

**TopicId ** string`Example: topic-xxxxx`

TLS topic ID bound to the health check log.

**DNSName** string `Example: alb-qwe1344.cn-beijing.volcenginealb.com`

DNS domain name.

**ZoneMappings ** object[]`Example: -`

Configuration information of the ALB instance across different availability zones.

**ZoneId ** string`Example: cn-beijing-a`

The availability zone where the ALB instance resides

**SubnetId ** string`Example: subnet-bp12mw1f8k3jgy****`

Subnet ID of the ALB instance in this availability zone.

**LoadBalancerAddresses ** object[]`Example: -`

The IP address of the ALB instance in this availability zone.

**Ipv4LocalAddresses ** string[]`Example: ["172.XX.XX.34","172.XX.XX.35"]`

IPv4 local address list. The address list used by the ALB to communicate with backend services.

**Ipv6LocalAddresses ** string[]`Example: ["2408:4005:XX:XX:201","2408:4005:XX:XX:202"]`

IPv6 local address list. The address list used by the ALB to communicate with backend services.

**EniAddress ** string`Example: 172.XX.XX.33`

The private IP address of the ALB instance in this availability zone.

**EniId ** string`Example: eni-2fe6rabqt8g****xruv8u8c9f`

The ID of the network interface occupied by the ALB instance in this availability zone.

**EipAddress ** string`Example: 10.XX.XX.27`

EIP address of the ALB instance in this availability zone.

**EipId ** string`Example: eip-2fe698wsnj****oxruvtryndp`

The EIP ID of the ALB instance in this availability zone.

**Eip ** object`Example: -`

EIP information of the ALB instance in that availability zone.

**ISP ** string`Example: BGP`

ISP for ALB Instance EIP.

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

The EIP type of the ALB instance.

* Empty: EIP.

* anycast: Anycast EIP.

**PopLocations ** object[]`Example: -`

The access point information associated when ALB acts as the origin of an Anycast EIP. Only valid when bound to Anycast EIP.

**PopId ** string`Example: cn-beijing-pop`

Access point ID of the Anycast EIP.

**PopName ** string`Example: beijing-pop`

The access point name of the Anycast EIP.

**AssociationMode ** string`Example: Default`

The origin type when ALB acts as an Anycast EIP source. Only valid when bound to an Anycast EIP.

* Default: Default mode.

* Normal: Normal mode.

**EniIpv6Address ** string`Example: 2408:4005:XX:XX:200`

For an ALB instance of IPv4&IPv6 dual\-stack type, the IPv6 address in that availability zone.

**Ipv6EipId ** string`Example: eip-2fe698wsnj****oxruvtryndp`

The IPv6 internet bandwidth ID of the ALB public instance of IPv4&IPv6 dual\-stack type in this availability zone.

**Ipv6Eip ** object`Example: -`

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

**LocalAddresses ** string[]`Example: ["100.64.1.0/20", "xxx"]`

The origin address of the ALB instance.

**ProjectName ** string`Example: default`

Name of the project to which the instance belongs.

**Tags ** object[]`Example: -`

The tags associated with the instance.

**Key ** string`Example: key`

The tag key of the custom tag.

**Value ** string`Example: value`

The tag value of the custom tag.

**SniAutoMatch ** string`Example: off`

Instance supports automatic selection of extended certificates.

* off: Not supported.

* on: Supported.

**WafProtectionEnabled ** string`Example: off`

WAF protection switch.

* off: Disable.

* on: Enable.

**WafInstanceId ** string`Example: waf-14ca6f67c33c0****`

The ID of the WAF security protection instance bound to the ALB instance.

**GlobalAccelerators ** object[]`Example: -`

Global accelerator bound to the ALB instance.

**AcceleratorId ** string`Example: accinstance-VYjG****`

Global Accelerator ID.

**AcceleratorName ** string`Example: global-test`

The global accelerator name.

**ModificationProtectionStatus** string `Example: NonProtection`

Enable instance modification protection feature.

* NonProtection: Disabled.

* ConsoleProtection: Enabled.

**ModificationProtectionReason** string `Example: This is modification protection`

Reason for enabling instance modification protection.

**LoadBalancerEdition ** string`Example: Standard`

ALB instance edition:

* Basic: Basic edition.

* Standard: Standard edition.

**Enabled ** boolean`Example: true`

Enabled status of the instance.

* true: Enabled.

* false: Disabled.

   The instance enabled status is false only when the instance is shut down due to arrears or expiration.

**SecurityGroupIds ** string[]`Example: ["sg-bp67acfmxazb4p****"]`

Security group ID associated with the ALB instance.

**ArkClawEnabled ** string`Example: off`

Enable ArkClaw feature.

* on: Enable.

* off: Disable.

> **tip**

> This parameter is currently in Beta stage. For trial requests, please contact your account manager.

**SpaceNetworkId ** string`Example: csn-bpkdt37pq72zv\*\*\*\*`

ID of the SpaceNetwork where the ArkClaw instance resides.

> **tip**

> This parameter is currently in Beta stage. For trial requests, please contact your account manager.

## Request example

```text
GET /?Action=DescribeLoadBalancerAttributes&LoadBalancerId=alb-1g1f1c6ae****A7&Version=2020-04-01 HTTP/1.1
Host: alb.cn-beijing.byteplusapi.com.cn
X-Date: 20251121T094038Z
Authorization: HMAC-SHA256 Credential=Adfks******wekfwe/20251121/cn-beijing/alb/request, SignedHeaders=host;x-date, Signature=47a7d934ff7b37c03938******cd7b8278a40a1057690c401e92246a0e41085f
```

## Response examples

```text
{
    "ResponseMetadata": {
        "RequestId": "20210816110638****2514606306AF947C",
        "Action": "DescribeLoadBalancerAttributes",
        "Version": "2020-04-01",
        "Service": "alb",
        "Region": "cn-beijing"
    },    
    "Result": {
            "RequestId": "20210811183410010****4214202005AE9",
            "LoadBalancerId": "alb-1g1f1c6aevm****buxws5k0k3",
            "LoadBalancerName": "test",
            "Status": "Active",
            "Description": "test",
            "CreateTime": "2021-08-11T18:01:42Z",
            "UpdateTime": "2021-08-11T18:18:13Z",
            "Type": "public",
            "VpcId": "vpc-3tj9fo0uqy3****28rma",
            "SubnetId": "subnet-3tj9f****m3vj0x28rn5",
            "EipID": "eip-2fe698wsnj8c****ruvtryndp",
            "EipAddress": "10.XX.XX.17",
            "EniID": "eni-2fe6sjrih****5oxruw1c3d8b",
            "EniAddress": "172.XX.XX.172",
            "BusinessStatus": "",
            "LockReason": "",
            "OverdueTime": "",
            "DeletedTime": "",
            "LoadBalancerBillingType": 1,
            "AccessLog": {
                "Enabled": "true",
                "BucketName": "alb-tos",
            },
            "Eip": {
                "ISP": "BGP",
                "Bandwidth": 1,
                "EipBillingType": 2,
                "EipAddress": "10.XX.XX.17"
            },
            "Listeners": [
                {
                    "ListenerId": "lsn-2ff0ixt8****g5oxruw4bbqjt",
                    "ListenerName": "test"
                }
            ],
            "DNSName": "alb-t5aepy8j****7mrjdjavoc2c.cn-beijing.volcalb.com",
            "ZoneMappings": [
                {
                    "ZoneId": "cn-beijing-a",
                    "SubnetId": "subnet-274tv****duyo7fap8sc658ze",
                    "LoadBalancerAddresses": [
                        {
                            "EniAddress": "192.168.0.25",
                            "EniId": "eni-274js3****xhc7fap8ssed7qg",
                            "EipAddress": "",
                            "EipId": "",
                            "Eip": {
                                "ISP": "BGP",
                                "Bandwidth": 1,
                                "EipBillingType": 2,
                                "EipAddress": "10.XX.XX.17"，
                                "SecurityProtectionTypes": ["AntiDDoS_Enhanced"]
                            },
                        }
                    ]
                },
                {
                    "ZoneId": "cn-beijing-b",
                    "SubnetId": "subnet-274u****nb8xs7fap8t1odh1n",
                    "LoadBalancerAddresses": [
                        {
                            "EniAddress": "192.168.1.254",
                            "EniId": "eni-274j****c6zgg7fap8t05movj",
                            "EipAddress": "",
                            "EipId": "",
                            "Eip": {
                                "ISP": "BGP",
                                "Bandwidth": 1,
                                "EipBillingType": 2,
                                "EipAddress": "10.XX.XX.17"，
                                "SecurityProtectionTypes": ["AntiDDoS_Enhanced"]
                            },
                        }
                    ]
                }
            ]
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
|404 |InvalidLoadBalancer.NotFound |The specified LoadBalancer does not exist. |The specified ALB instance does not exist. |
|500 |InternalError |An internal error has occurred. |An internal error occurred. Please try again later or contact an engineer for further consultation. |
