---
title: "DescribeLoadBalancerAttributes - Querying the CLB details"
product: "Cloud Load Balancer"
product_code: "clb"
source: "https://docs.byteplus.com/en/docs/clb/DescribeLoadBalancerAttributes"
---

Call the DescribeLoadBalancerAttributes API to view details of the specified CLB instance.

## Debug

[去调试](https://api.byteplus.com/api-explorer/debug?action=DescribeLoadBalancerAttributes&serviceCode=clb&version=2020-04-01&groupName=)

## Request parameters

**Action ** String必选 `Example: DescribeLoadBalancerAttributes`

Action to execute. Set the value to **DescribeLoadBalancerAttributes**.

**Version ** String必选 `Example: 2020-04-01`

API version. The current version is **2020\-04\-01**.

**LoadBalancerId ** String必选 `Example: clb-bp1b6c719dfa08ex****`

CLB Instance ID.

You can call the [DescribeLoadBalancers](https://docs.byteplus.com/en/docs/clb/DescribeLoadBalancers) API to query the CLB Instance ID.

## Response parameters

**RequestId ** String`Example: 202108161106382514606306AF947C****`

Request ID.

**AccountId ** String`Example: 210012****`

Account ID of the CLB instance.

**ExclusiveClusterId ** String`Example: ec-bp1o94dp5i6ea****`

ID of the exclusive cluster.

> This parameter returns empty for CLB instances of non\-exclusive cluster types. The exclusive cluster is currently in beta stage and only supports trial applications from accounts that have completed enterprise certification. If you need a trial, please contact the account manager.

**LoadBalancerId ** String`Example: clb-bp1b6c719dfa08ex****`

CLB Instance ID.

**LoadBalancerName ** String`Example: clb-test1`

Name of the CLB instance.

**Description ** String`Example: CLB-Description`

Description of the CLB instance.

**Type ** String`Example: private`

Type of the CLB instance.

* Public: Internet.

* private: VPC.

**AddressIpVersion ** String`Example: ipv4`

IP address type of the CLB instance.

* ipv4: IPv4 only.

* DualStack: dual stack, supporting both IPv4 and IPv6.

**LoadBalancerBillingType ** Integer`Example: 2`

Select a billing method for the CLB instance.

* 1: Subscription

* 2: Pay\-by\-Specification

* 3: Pay\-by\-CU

> **tip**

> Pay\-by\-CU is in the beta stage. To request a trial, please contact your account manager.

**LoadBalancerSpec ** String`Example: small_1`

The specification of the CLB instance.

* small_1: Small I

* small_2: Small II

* medium_1: Medium I

* medium_2: Medium II

* large_1: Large I

* large_2: Large II

**MasterZoneId ** String`Example: cn-shanghai-a`

Primary Availability Zone ID of the CLB instance.

**SlaveZoneId ** String`Example: cn-shanghai-b`

Secondary Zone ID of the CLB Instance.

Returns empty if the CLB instance is a single\-zone instance. The CLB single availability zone is in beta stage. For trial requests, please contact your account manager.

**VpcId ** String`Example: vpc-bp1aevy8sofi8mh1****`

The VPC ID to which the CLB instance belongs.

**SubnetId ** String`Example: subnet-bp12mw1f8k3jgy****`

The subnet ID to which the CLB instance belongs.

**EniID ** String`Example: eni-2fe6rabqt8gxruv8u8c9f****`

Occupied Network interface ID of the CLB Instance.

**EipID ** String`Example: eip-2fe698wsnjoxruvtryndp****`

The ID of the elastic IP address (EIP).

**EipAddress ** String`Example: 10.XX.XX.27`

EIP Address of the CLB instance.

**EniAddress ** String`Example: 172.XX.XX.33`

Private IPv4 address of the CLB instance.

**EniAddressNum ** Integer`Example: 2`

The number of private IPv4 addresses of the CLB instance.

**EniAddresses ** Object[]`Example: 172.XX.XX.2`

Private IPv4 address information of the CLB instance.

**EniAddress ** String`Example: 172.XX.XX.33`

Private IPv4 address of the CLB instance.

**EipId ** String`Example: eip-3ciyamhu46c6rrswwusg****`

The ID of the EIP bound to the private IPv4 address.

**EipAddress ** String`Example: 10.XX.XX.27`

The Elastic IP (EIP) associated with the private IPv4 address.

**Eip ** Object`Example: -`

Information about the EIP address of the CLB instance.

**ISP ** String`Example: BGP`

ISPs for CLB Instance EIPs.

* BGP: BGP (multi\-line).

* ChinaMobile: Static single\-ISP provided by China Mobile.

* ChinaTelecom: Static single\-ISP provided by China Telecom.

* ChinaUnicom: Static single\-ISP provided by China Unicom.

* SingleLine_BGP: BGP single\-ISP.

* Static_BGP: Static BGP.

> **tip**

> Except for BGP (multi\-line), all other line types are currently in beta stage and temporarily only supports accounts that have completed [Enterprise certification](https://docs.byteplus.com/en/docs/6261/64937) to apply for trial. If you need a trial, please contact your account manager.

**EipBillingType ** Integer`Example: 2`

The metering method of the EIP.

* 1: Subscription

* 2: Pay\-by\-bandwidth

* 3: Pay\-by\-data\-transfer

**Bandwidth ** Integer`Example: 10`

The peak bandwidth of the EIP. Unit: Mbps

**EipAddress ** String`Example: 10.XX.XX.27`

EIP Address of the CLB instance.

**BandwidthPackageId ** String`Example: bwp-2zeo05qre24nhrqpy****`

ID of the bandwidth package to which the EIP is added.

**SecurityProtectionTypes ** String[]`Example: ["AntiDDoS_Enhanced"]`

The protection type of the EIP.

* AntiDDoS_Enhanced: Indicates that the EIP is of the enhanced protection type and can be added to a DDoS Origin Advanced (Enterprise Edition) instance.

* Empty value: the EIP is of the Anti\-DDoS Basic type.

> **tip**

> The enhanced protection EIP feature is currently in beta stage. If the feature has not been activated, this parameter will not be returned.

**EniIpv6Address ** String`Example: 2408:4005:XX:XX:200`

Private IPv6 address of the CLB instance.

**Ipv6EipId ** String`Example: eip-2zaiwb7ujxscd****`

ID of the IPv6 Internet bandwidth.

**Ipv6AddressBandwidth ** Object`Example: -`

IPv6 Internet bandwidth information of the CLB instance.

**Bandwidth ** Integer`Example: 10`

The peak bandwidth of the IPv6 internet. Unit: Mbps

**NetworkType** String `Example: public`

The network type of the CLB instance's IPv6 address.

* public: Indicates that the IPv6 address has Internet bandwidth enabled and can forward IPv6 internet traffic.

**BillingType ** Integer`Example: 2`

Metering methods for IPv6 Internet bandwidth.

* 2: Pay\-by\-bandwidth.

* 3: Pay\-by\-data\-transfer

**ISP ** String`Example: BGP`

IPv6 Internet bandwidth ISP.

* BGP (Multi\-ISP).

**BandwidthPackageId ** String`Example: bwp-2zeo05qre24nhrqpy****`

ID of the bandwidth package to which the IPv6 internet bandwidth is added.

**ModificationProtectionStatus ** String`Example: ConsoleProtection`

Enable console modification protection.

* NonProtection or Empty: Disabled Once configured, the existing `ModificationProtectionReason` will be cleared.

* ConsoleProtection: Enable. When enabled, modifications or deletion of the instance via the console are prohibited, but changes or deletion via API are still allowed

**ModificationProtectionReason ** String`Example: managed instance`

Reason for setting modification protection status.

> **tip**

> This parameter takes effect only when `ModificationProtectionStatus` is set to **ConsoleProtection**.

**ServiceManaged ** Boolean`Example: false`

Whether the CLB instance is a managed resource.

* true: Managed resource. Indicates that the CLB resource was automatically created by the system when other cloud resources (besides the CLB) were created.

* false: Not a managed resource. Indicates that the CLB resource was created manually on the CLB platform.

**Status ** String`Example: Active`

CLB instance status.

* Inactive: Disabled.

* Active: Running.

* Creating

* Provisioning: Creating.

* Configuring: Pending.

* Deleting

* CreateFailed: Creation failed.

**BusinessStatus** String `Example: FinancialLocked`

CLB Instance is locked

* Normal

* FinancialLocked: Being locked.

> **tip**

> Returns empty if the instance is not locked.

**LockReason ** String`Example: Financial`

Reasons for CLB instance freezing. This parameter returns a value only when the instance is in the **FinancialLocked** status.

* Financial: Being locked due to arrears.

> **tip**

> When the value of the `BusinessStatus` parameter is "Normal" or empty, this parameter returns empty.

**Listeners ** Object[]`Example: -`

Information about the listeners in the CLB instance.

**ListenerId ** String`Example: lsn-2fea4ayvu2g3k5oxruuze****`

Listener ID.

**ListenerName ** String`Example: listener-1`

Listener name.

**ServerGroups ** Object[]`Example: -`

Information about the backend server group in the CLB instance.

**ServerGroupId ** String`Example: rsp-1g0ogy36a8t8g8ibuxwy5****`

ID of the backend server group.

**ServerGroupName ** String`Example: servergroup-1`

Name of the backend server group.

**LogTopicId ** String`Example: 74936ae4-bbd6-41de-a0d2-ed156203****`

The ID of the log topic.

**AccessLog ** Object`Example: -`

Information about the access logs in the CLB instance.

**Enabled ** Boolean`Example: true`

Whether the access log (Layer 7) delivery to TOS is enabled.

* true: Enabled

* false: Disabled.

**BucketName ** String`Example: clb-tos`

The name of the TOS storing Layer\-7 access logs.

**TlsEnabled ** Boolean`Example: true`

Enable access log (Layer\-7) delivery to TLS

* true: Enabled

* false: Disabled.

**TlsProjectId ** String`Example: fc6953c1-fe50-***`

Log project.

**TlsTopicId ** String`Example: 74936ae4-bbd6-***`

Log Topic.

**Enabled ** Boolean`Example: true`

Enabled status of the CLB instance.

* true: Enabled.

* false: Disabled.

> **tip**

> When the CLB instance is in arrears suspension or expired suspension status, the value of this parameter is "false"; in all other cases, it is "true".

**ProjectName ** String`Example: default`

The name of the project to which the CLB instance belongs.

**Tags ** Object[]`Example: -`

Tag information of the CLB instance.

**Key ** String`Example: k1`

The tag key.

**Value ** String`Example: v1`

The tag value.

**BypassSecurityGroupEnabled ** String`Example: off`

Whether the "Allow Backend Security Group Access" feature is enabled for the CLB instance.

* on: Enable.

* off: Disable.

**TimestampRemoveEnabled ** String`Example: off`

Whether to enable the function of stripping TCP/HTTP/HTTPS packet timestamps

* on: Enable.

* off: Disable.

> **tip**

> This feature is currently in Beta stage. For trial requests, please contact your account manager.

**CreateTime ** String`Example: 2021-08-11T16:37:37Z`

Creation time of the CLB instance.

**UpdateTime ** String`Example: 2021-08-11T16:37:37Z`

Last modified time of the CLB instance.

**OverdueTime ** String`Example: 2021-08-11T16:37:37Z`

The freeze time of the CLB instance.

> **tip**

> When the value of the `BusinessStatus` parameter is "Normal" or empty, this parameter returns empty.

**DeletedTime ** String`Example: 2021-08-11T16:37:37Z`

Scheduled Reclaim Time of the CLB Instance. This parameter returns a value only when the instance is in the **FinancialLocked** status.

**ExpiredTime ** String`Example: 2021-08-11T23:59:59Z`

Expiration Time of the CLB Instance.

> **tip**

> This parameter is returned only when `LoadBalancerBillingType` is set to 1.

## Request examples

```json
GET /?Action=DescribeLoadBalancerAttributes&LoadBalancerId=clb-bp1b6c719dfa08ex****&Version=2020-04-01 HTTP/1.1
Host: clb.cn-beijing.byteplusapi.com.cn
X-Date: 20251121T094038Z
Authorization: HMAC-SHA256 Credential=Adfks******wekfwe/20251121/cn-beijing/clb/request, SignedHeaders=host;x-date, Signature=47a7d934ff7b37c03938******cd7b8278a40a1057690c401e92246a0e41085f
```

## Response examples

```json
{
    "ResponseMetadata": {
        "RequestId": "20230604110420****100232280022D31",
        "Action": "DescribeLoadBalancerAttributes",
        "Version": "2020-04-01",
        "Service": "clb",
        "Region": "cn-beijing"
    },
    "Result": {
        "AccessLog": {
            "Enabled": true,
            "BucketName": "clb-tos",
            "TlsEnabled": true,
            "TlsTopicId": "74936ae4-bbd6-***",
            "TlsProjectId": "fc6953c1-fe50-***"
        },
        "AccountId": "210012****",
        "AddressIpVersion": "ipv4",
        "BusinessStatus": "FinancialLocked",
        "BypassSecurityGroupEnabled": "off",
        "CreateTime": "2021-08-11T16:37:37Z",
        "DeletedTime": "2021-08-11T16:37:37Z",
        "Description": "CLB-Description",
        "Eip": {
            "ISP": "BGP",
            "Bandwidth": 10,
            "EipAddress": "10.XX.XX.27",
            "EipBillingType": 2,
            "BandwidthPackageId": "bwp-2zeo05qre24nhrqpy****",
            "SecurityProtectionTypes": [
                "AntiDDoS_Enhanced"
            ]
        },
        "EipAddress": "10.XX.XX.27",
        "EipID": "eip-2fe698wsnjoxruvtryndp****",
        "Enabled": true,
        "EniAddress": "172.XX.XX.33",
        "EniAddressNum": 2,
        "EniAddresses": [
            {
                "EipId": "eip-3ciyamhu46c6rrswwusg****",
                "EipAddress": "10.XX.XX.27",
                "EniAddress": "172.XX.XX.33"
            }
        ],
        "EniID": "eni-2fe6rabqt8gxruv8u8c9f****",
        "EniIpv6Address": "2408:4005:XX:XX:200",
        "ExclusiveClusterId": "ec-bp1o94dp5i6ea****",
        "ExpiredTime": "2021-08-11T23:59:59Z",
        "Ipv6AddressBandwidth": {
            "ISP": "BGP",
            "Bandwidth": 10,
            "BillingType": 2,
            "NetworkType": "public",
            "BandwidthPackageId": "bwp-2zeo05qre24nhrqpy****"
        },
        "Ipv6EipId": "eip-2zaiwb7ujxscd****",
        "Listeners": [
            {
                "ListenerId": "lsn-2fea4ayvu2g3k5oxruuze****",
                "ListenerName": "listener-1"
            }
        ],
        "LoadBalancerBillingType": 2,
        "LoadBalancerId": "clb-bp1b6c719dfa08ex****",
        "LoadBalancerName": "clb-test1",
        "LoadBalancerSpec": "small_1",
        "LockReason": "Financial",
        "LogTopicId": "74936ae4-bbd6-41de-a0d2-ed156203****",
        "MasterZoneId": "cn-shanghai-a",
        "ModificationProtectionReason": "托管实例",
        "ModificationProtectionStatus": "ConsoleProtection",
        "OverdueTime": "2021-08-11T16:37:37Z",
        "ProjectName": "default",
        "RequestId": "202108161106382514606306AF947C****",
        "ServerGroups": [
            {
                "ServerGroupId": "rsp-1g0ogy36a8t8g8ibuxwy5****",
                "ServerGroupName": "servergroup-1"
            }
        ],
        "ServiceManaged": true,
        "SlaveZoneId": "cn-shanghai-b",
        "Status": "Active",
        "SubnetId": "subnet-bp12mw1f8k3jgy****",
        "Tags": [
            {
                "Key": "k1",
                "Value": "v1"
            }
        ],
        "TimestampRemoveEnabled": "off",
        "Type": "private",
        "UpdateTime": "2021-08-11T16:37:37Z",
        "VpcId": "vpc-bp1aevy8sofi8mh1****"
    }
}
```

## Error codes

This section displays only the error codes of the current API. For more error codes, see [Common error codes](https://docs.byteplus.com/en/docs/clb/Public-error-codes).

|Status code |Error codes |Error message |Notes |
|---|---|---|---|
|400 |MissingParameter |The request is missing a required parameter. Ensure that you have supplied all the required parameters for the request; for example, the 'LoadBalancerId'. |This request is missing a required parameter. Please ensure the request includes all required parameters, such as LoadBalancerId. |
|400 |MissingParameter |The request is missing a required parameter. Ensure that you have supplied all the required parameters for the request; for example, the ''. |This request is missing a required parameter. Ensure the request includes all required parameters, such as . |
|403 |Forbidden |You are not authorized to perform operations on the specified service. |You do not have permission to perform operations on the specified service. |
|404 |InvalidLoadBalancer.NotFound |The specified LoadBalancer does not exist. |The specified load balancer does not exist. |
|500 |InternalError |An internal error has occurred. |An internal error occurred. |
