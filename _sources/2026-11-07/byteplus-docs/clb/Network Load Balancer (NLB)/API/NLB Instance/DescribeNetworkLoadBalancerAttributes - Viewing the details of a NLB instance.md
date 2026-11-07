---
title: "DescribeNetworkLoadBalancerAttributes - Viewing the details of a NLB instance"
product: "Cloud Load Balancer"
product_code: "clb"
source: "https://docs.byteplus.com/en/docs/clb/DescribeNetworkLoadBalancerAttributes"
---

Call the DescribeNetworkLoadBalancerAttributes API to view the details of a Network Load Balancer (NLB) instance.

<span id=".6LCD6K-V"></span>
## Debug

[去调试](https://api.byteplus.com/api-explorer/debug?action=DescribeNetworkLoadBalancerAttributes&serviceCode=clb&version=2020-04-01&groupName=)


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters



**Action ** <span data-label="purple">String </span><span data-api-tag="require|aaM5W5">必选</span>`Example: DescribeNetworkLoadBalancerAttributes`

Action to execute. Set the value to DescribeNetworkLoadBalancerAttributes.



**Version ** <span data-label="purple">String </span><span data-api-tag="require|FQ9nKV">必选</span> `Example: 2020-04-01`

Current API version is 2020\-04\-01.



**LoadBalancerId ** <span data-label="purple">String </span><span data-api-tag="require|JISZv7">必选</span> `Example: nlb-bp1b6c719dfa08ex****`

NLB instance ID.

You can call the [DescribeNetworkLoadBalancers](https://docs.byteplus.com/en/docs/clb/DescribeNetworkLoadBalancers) API to get the NLB instance ID.



&nbsp;

<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters



**RequestId ** <span data-label="purple">String </span>`Example: 202409291106382514606306AF947C****`

Request ID.



**CreateTime ** <span data-label="purple">String </span>`Example: 2024-08-11T16:37:37Z`

Creation time of the NLB instance.



**UpdateTime ** <span data-label="purple">String </span>`Example: 2024-08-11T16:37:37Z`

Last modified time of the NLB instance.



**LoadBalancerId ** <span data-label="purple">String </span>`Example: nlb-bp1b6c719dfa08ex****`

NLB instance ID.



**AccountId ** <span data-label="purple">String </span>`Example: 210012****`

The account ID to which the NLB instance belongs.



**ProjectName ** <span data-label="purple">String </span>`Example: default`

Name of the project to which the NLB instance belongs.



**LoadBalancerName ** <span data-label="purple">String </span>`Example: nlb-test1`

Name of the NLB instance.



**Status ** <span data-label="purple">String </span>`Example: Active`

The status of the NLB instance.


* Inactive: Stopped.

* Active: Running.

* Creating.

* Provisioning: Creating. This status only exists when creating an NLB instance by calling the API.

* Configuring: Pending configuration.

* Deleting

* CreateFailed: Creation failed.



**Description ** <span data-label="purple">String </span>`Example: test`

Description of the NLB instance.



**Ipv4NetworkType ** <span data-label="purple">String </span>`Example: intranet`

The IPv4 network type of the NLB instance.


* internet: Public network.

* intranet: Private network.



**Ipv6NetworkType ** <span data-label="purple">String </span>`Example: intranet`

IPv6 network type of the NLB instance.


* internet: Public network.

* intranet: Private network.



**IpAddressVersion ** <span data-label="purple">String </span>`Example: ipv4`

The IP address type of the NLB instance.


* ipv4: IPv4 version.

* dualstack: Dual stack, which supports both IPv4 and IPv6 versions.



**CrossZoneEnabled ** <span data-label="purple">Boolean </span>`Example: true`

NLB instance enables cross\-az forwarding.



**DNSName ** <span data-label="purple">String </span>`Example: nlb-bp1aevy8sofi8mh1****.cn-ningbo-sdv.volces.com`

DNS address of the NLB instance.



**BillingType ** <span data-label="purple">Integer </span>`Example: 3`

Billing method of the NLB instance.


* 3: Pay\-by\-CU



**BillingStatus ** <span data-label="purple">String </span>`Example: FinancialLocked`

The billing status of the NLB instance.


* Normal

* FinancialLocked: Being locked.



**ExpectedOverdueTime ** <span data-label="purple">String </span>`Example: 2023-07-17T01:37:38Z`

The suspension time of the NLB instance due to overdue payment.



**OverdueTime ** <span data-label="purple">String </span>`Example: 2023-07-17T01:37:38Z`

Locked time of the NLB instance.

When the parameter `BillingStatus` is set to `Normal`, this parameter returns an empty string.



**ReclaimedTime ** <span data-label="purple">String </span>`Example: 2024-07-17T01:37:38Z`

Expected reclaim time of the NLB instance.

When the parameter `BillingStatus` is set to `Normal`, this parameter returns an empty string.



**Ipv4BandwidthPackageId ** <span data-label="purple">String </span>`Example: bwp-2zeo05qre24nhrqpy****`

ID of the IPv4 Bandwidth Package.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">When the instance is not added to the IPv4 Bandwidth Package, this field returns an empty string.</div>




**Ipv6BandwidthPackageId ** <span data-label="purple">String </span>`Example: bwp-b2weev3esweer8mt****`

ID of the IPv6 Bandwidth Package.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">When the instance is IPv4 type or the instance is not added to the IPv6 Bandwidth Package, this field returns an empty string.</div>




**VpcId ** <span data-label="purple">String </span>`Example: vpc-bp1aevy8sofi8mh1****`

The VPC ID to which the NLB instance belongs.



**ManagedSecurityGroupId ** <span data-label="purple">String </span>`Example: sg-bp1aevy8sofi8mh1****`

The managed security group ID automatically associated by the system with the NLB instance.



**SecurityGroupIds ** <span data-label="purple">String[] </span>`Example: ["sg-bpo05q8so05qmh1****", "sg-5eorfq84r05rfmhw****"]`

ID of the non\-managed security group attached to the NLB instance.



**ModificationProtectionStatus ** <span data-label="purple">String </span>`Example: ConsoleProtection`

Enable console modification protection for the NLB instance.


* NonProtection or empty: Disable, allowing modification or deletion of the instance via the console.

* ConsoleProtection: Enable, prohibiting modification or deletion of the instance via the console.



**AccessLog ** <span data-label="purple">Object </span>`Example: --`

Access log information of the NLB instance.


**AccessLogEnabled ** <span data-label="purple">Boolean </span>`Example: true`

Enable access log.


* true: Yes

* false: No



**ProjectId ** <span data-label="purple">String </span>`Example: fc6953c1-fe50-43aa-9d26-c1e0a207****`

ID of the log project.



**TopicId ** <span data-label="purple">String </span>`Example: 74936ae4-bbd6-41de-a0d2-ed156203****`

ID of the log topic.




**Tags ** <span data-label="purple">Object[] </span>`Example: --`

Tag information of the NLB instance.


**Key ** <span data-label="purple">String </span>`Example: k1`

The tag key.



**Value ** <span data-label="purple">String </span>`Example: v1`

The tag value.




**ZoneMappings ** <span data-label="purple">Object[] </span>`Example: --`

Availability zone information of the NLB instance.


**ZoneId ** <span data-label="purple">String </span>`Example: cn-beijing-a`

Availability zone ID.



**SubnetId ** <span data-label="purple">String </span>`Example: subnet-5eorfq84r05rfmhw****`

Subnet ID.



**EniId ** <span data-label="purple">String </span>`Example: eni-bp1aevy8sofi8mh1****`

Network Interface ID.



**Ipv4Address ** <span data-label="purple">String </span>`Example: 192.XX.XX.10`

The private IPv4 VIP address of the NLB instance.



**Ipv4EipAddress ** <span data-label="purple">String </span>`Example: 22.XX.XX.22`

The address of the EIP.



**Ipv6Address ** <span data-label="purple">String </span>`Example: 2000:1000:2c7f:fe40:ca2f:dd0a:XX.XX`

The private IPv6 VIP address of the NLB instance.



**Ipv4EipId ** <span data-label="purple">String </span>`Example: eip-2beasvyfs2fiwmws****`

ID of the Elastic IP Address (EIP) associated with the NLB instance.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">When the IPv4 network type of the NLB instance is "Intranet", this parameter returns an empty string.</div>




**Ipv6EipId ** <span data-label="purple">String </span>`Example: eip-2zaiwb7ujxscd****`

ID of the IPv6 Internet bandwidth associated with the NLB instance.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">When the IPv6 network type of the NLB instance is "Intranet" or the IP version of the NLB instance is "ipv4", this parameter returns an empty string.</div>




**Ipv4HcStatus ** <span data-label="purple">String </span>`Example: Healthy`

Health status of the private IPv4 address of the NLB instance.


* Healthy: Normal.

* Unhealthy: Abnormal.



**Ipv6HcStatus ** <span data-label="purple">String </span>`Example: Healthy`

Health status of the private IPv6 address of the NLB instance.


* Healthy: Normal.

* Unhealthy: Abnormal.



**Ipv4LocalAddresses ** <span data-label="purple">String[] </span>`Example: 192.XX.XX.12`

The private IPv4 LIP address of the NLB instance.



**Ipv6LocalAddresses ** <span data-label="purple">String[] </span>`Example: 2000:1000:2c7f:fe40:ca2f:dd0a:XX.XX`

The private IPv6 LIP address of the NLB instance.




**DNSAffinity ** <span data-label="purple">Boolean </span>`Example: false`

Whether to enable DNS Availability Zone (AZ) affinity.


* true: Private network clients preferentially resolve to the IPs of NLB nodes in the same AZ, so traffic does not cross AZs. If a node in the same AZ fails, the IPs of all non\-faulty AZs are automatically returned.

* false: DNS returns the IPs of nodes in all AZs of the instance, and clients select randomly or by round\-robin, which may result in cross\-AZ access.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">This applies only to private network resolution; public DNS is not affected.</div>




&nbsp;

<span id=".6K-35rGC56S65L6L"></span>
## Request example

```json
GET /?Action=DescribeNetworkLoadBalancerAttributes&Version=2020-04-01&LoadBalancerId=nlb-bp1b6c719dfa08ex**** HTTP/1.1
Host: clb.cn-beijing.byteplusapi.com.cn
Date: 20260310T094038Z
Authorization: HMAC-SHA256 Credential=Adfks******wekfwe/20251121/cn-beijing/clb/request, SignedHeaders=host;x-date, Signature=47a7d934ff7b37c03938******cd7b8278a40a1057690c401e92246a0e41085f
```


<span id=".6L-U5Zue56S65L6L"></span>
## Response example

```json
{
    "ResponseMetadata": {
        "RequestId": "20230604110420****100232280022D31",
        "Action": "DescribeNetworkLoadBalancerAttributes",
        "Version": "2020-04-01",
        "Service": "clb",
        "Region": "cn-beijing"
    },
    "Result": {
        "AccessLog": {
            "TopicId": "74936ae4-bbd6-41de-a0d2-ed156203****",
            "ProjectId": "fc6953c1-fe50-43aa-9d26-c1e0a207****",
            "AccessLogEnabled": true
        },
        "AccountId": "210012****",
        "BillingStatus": "FinancialLocked",
        "BillingType": 3,
        "CreateTime": "2024-08-11T16:37:37Z",
        "CrossZoneEnabled": true,
        "DNSName": "nlb-bp1aevy8sofi8mh1****.cn-ningbo-sdv.volces.com",
        "Description": "test",
        "ExpectedOverdueTime": "2023-07-17T01:37:38Z",
        "IpAddressVersion": "ipv4",
        "Ipv4BandwidthPackageId": "bwp-2zeo05qre24nhrqpy****",
        "Ipv4NetworkType": "intranet",
        "Ipv6BandwidthPackageId": "bwp-b2weev3esweer8mt****",
        "Ipv6NetworkType": "intranet",
        "LoadBalancerId": "nlb-bp1b6c719dfa08ex****",
        "LoadBalancerName": "nlb-test1",
        "ManagedSecurityGroupId": "sg-bp1aevy8sofi8mh1****",
        "ModificationProtectionStatus": "ConsoleProtection",
        "OverdueTime": "2023-07-17T01:37:38Z",
        "ProjectName": "default",
        "ReclaimedTime": "2024-07-17T01:37:38Z",
        "RequestId": "202409291106382514606306AF947C****",
        "SecurityGroupIds": [
            "sg-bpo05q8so05qmh1****",
            "sg-5eorfq84r05rfmhw****"
        ],
        "Status": "Active",
        "Tags": [
            {
                "Key": "k1",
                "Value": "v1"
            }
        ],
        "UpdateTime": "2024-08-11T16:37:37Z",
        "VpcId": "vpc-bp1aevy8sofi8mh1****",
        "ZoneMappings": [
            {
                "EniId": "eni-bp1aevy8sofi8mh1****",
                "ZoneId": "cn-beijing-a",
                "SubnetId": "subnet-5eorfq84r05rfmhw****",
                "Ipv4EipId": "eip-2beasvyfs2fiwmws****",
                "Ipv6EipId": "eip-2zaiwb7ujxscd****",
                "Ipv4Address": "192.XX.XX.10",
                "Ipv6Address": "2000:1000:2c7f:fe40:ca2f:dd0a:XX.XX",
                "Ipv4HcStatus": "Healthy",
                "Ipv6HcStatus": "Healthy",
                "Ipv4EipAddress": "22.XX.XX.22",
                "Ipv4LocalAddresses": [
                    ""
                ],
                "Ipv6LocalAddresses": [
                    ""
                ]
            }
        ]
    }
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error codes

This section displays only the error codes of the current API. For more error codes, see [Common error codes](https://docs.byteplus.com/en/docs/clb/NLB-Common-Error-Codes).


|Status code |Error codes |Error message |Description |
|---|---|---|---|
|400 |DryRunOperation |Exception raised to indicate a successfully authorized action when the DryRun flag is set to true. |This request is set to DryRun action. The action has been authorized but has not been executed. |
|400 |IdempotentParameterMismatch |Arguments on this idempotent request are inconsistent with arguments used in previous request(s). |The parameters of this idempotent request are inconsistent with those used in the previous request. |
|400 |InvalidClientToken.Malformed |The specified ClientToken is malformed. |The specified ClientToken parameter format is invalid. |
|404 |InvalidLoadBalancer.NotFound |The specified LoadBalancer does not exist. |The specified CLB does not exist. |
|409 |InvalidOperation.Conflict |The specified resource operation conflicts. |The specified action on the resource conflicts. |
|412 |IdempotentProcessing |The request uses the same client token as a previous one that is still in process. |The idempotent request is in process. |
