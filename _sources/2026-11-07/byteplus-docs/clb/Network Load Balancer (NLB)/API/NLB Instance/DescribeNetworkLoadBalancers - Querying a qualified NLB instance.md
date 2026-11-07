---
title: "DescribeNetworkLoadBalancers - Querying a qualified NLB instance"
product: "Cloud Load Balancer"
product_code: "clb"
source: "https://docs.byteplus.com/en/docs/clb/DescribeNetworkLoadBalancers"
---

Call the DescribeNetworkLoadBalancers API to query NLB instances that meet specified conditions.

<span id=".6LCD6K-V"></span>
## Debug

[去调试](https://api.byteplus.com/api-explorer/debug?action=DescribeNetworkLoadBalancers&serviceCode=clb&version=2020-04-01&groupName=)


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters

When none of the optional parameters in the table below are provided, all NLB instances under the current account are returned.



**Action ** <span data-label="purple">String </span><span data-api-tag="require|UtwAIh">必选</span> `Example: DescribeNetworkLoadBalancers`

Action to execute. Set the value to DescribeNetworkLoadBalancers.



**Version ** <span data-label="purple">String </span><span data-api-tag="require|DCHK5v">必选</span> `Example: 2020-04-01`

Current API version is 2020\-04\-01.



**MaxResults ** <span data-label="purple">Integer </span>`optional` `Example: 10`

The number of rows per page for paginated queries. Valid range: 1 to 20. Default value: 10.



**NextToken ** <span data-label="purple">String </span>`optional` `Example: caeba0bbb2be03f84eb48b699f0a****`

The pagination token that marks the position for paginated queries. Leave it empty for the initial call. For subsequent queries, set this value to the `NextToken` parameter returned by the previous API call.



**LoadBalancerIds.N ** <span data-label="purple">String </span>`optional` `Example: nlb-bp1b6c719dfa08ex****`

The ID of the NLB instance.


* N: Represents the serial number of the NLB instance, ranging from 1 to 20.

* Separate NLB instance IDs with ampersands (&).



**VpcId ** <span data-label="purple">String </span>`optional` `Example: vpc-13fd2oy7dsiyo3n6nu4ye****`

ID of the VPC to which the NLB instance belongs.



**LoadBalancerName ** <span data-label="purple">String </span>`optional` `Example: nlb-test`

Name of the NLB instance.



**Status ** <span data-label="purple">String </span>`optional` `Example: Active`

The status of the NLB instance. Valid values:


* Inactive: Disabled.

* Active: Running.

* Creating

* Provisioning: Creating. This status only exists when creating an NLB instance by calling the API.

* Configuring: Pending configuration.

* Deleting

* CreateFailed: Creation failed.



**IpAddressVersion ** <span data-label="purple">String </span>`optional` `Example: ipv4`

IP protocol version. Valid values:


* ipv4: IPv4 version.

* dualstack: Dual stack, which supports both IPv4 and IPv6 versions.



o**ZoneId ** <span data-label="purple">String </span>`optional` `Example: cn-beijing-a`

Availability Zone ID.

You can call the [DescribeNLBZones](https://docs.byteplus.com/en/docs/clb/DescribeNLBZones) API to view the availability zone IDs in the current region.



**ProjectName ** <span data-label="purple">String </span>`optional` `Example: default`

Name of the project to which the NLB instance belongs.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">If this parameter is not provided or is provided as empty, it means to query NLB instances of all projects.</div>




**TagFilters.N.Key ** <span data-label="purple">String </span>`optional` `Example: k1`

The tag key. If multiple tag keys are specified, this API returns NLB instances that contain all of the specified tag keys.


* N represents the serial number of the tag key, ranging from 1 to 10.

* Separate multiple tag keys with ampersands (&).



**TagFilters.N.Values.N ** <span data-label="purple">String </span>`optional` `Example: v1`

The tag value.


* The first N specifies the serial number of a tag key. Valid values: 1\-10.

* The second N specifies the serial number of a tag value. Valid values: 1\-3. The relationship between multiple tag values for the same tag key is a logical "OR". That is, the query returns resources tagged with any one of the specified values for that key.

* Separate multiple tags with ampersands (&).


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">To provide this parameter, you must first provide <code>TagFilters.N.Key</code>.</div>


* <div data-tips="true" data-tips-type="tip">When an empty value is set for this parameter, it means querying resources where the tag value is empty under the specified tag key.</div>




&nbsp;

<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters



**RequestId ** <span data-label="purple">String </span>`Example: 202409291106382514606306AF947C****`

Request ID.



**NextToken ** <span data-label="purple">String </span>`Example: caeba0bbb2be03f84eb48b699f0a****`

The query token returned by this API call. An empty value indicates that there is no next page.



**LoadBalancers ** <span data-label="purple">Object[] </span>`Example: --`

Details of the NLB instances that match the criteria.


**CreateTime ** <span data-label="purple">String </span>`Example: 2024-08-11T16:37:37Z`

Creation time of the NLB instance.



**UpdateTime ** <span data-label="purple">String </span>`Example: 2024-08-11T16:37:37Z`

Last modified time of the NLB instance.



**LoadBalancerId ** <span data-label="purple">String </span>`Example: nlb-bp1o94dp5i6ea****`

The ID of the NLB instance.



**AccountId ** <span data-label="purple">String </span>`Example: 210012****`

The account ID to which the NLB instance belongs.



**ProjectName ** <span data-label="purple">String </span>`Example: default`

Name of the project to which the NLB instance belongs.



**LoadBalancerName ** <span data-label="purple">String </span>`Example: nlb-test`

Name of the NLB instance.



**Status ** <span data-label="purple">String </span>`Example: Active`

NLB instance status.


* Inactive: Disabled.

* Active: Running.

* Creating

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



**CrossZoneEnabled ** <span data-label="purple">Boolean </span>`Example: true`

NLB instance enables cross\-az forwarding.



**DNSName ** <span data-label="purple">String </span>`Example: nlb-b2ea3vwwssefdmer****.cn-beijing.volces.com`

DNS address of the NLB instance.



**BillingType ** <span data-label="purple">Integer </span>`Example: 3`

The billing method of the NLB instance.


* 3: Pay\-by\-CU



**BillingStatus ** <span data-label="purple">String </span>`Example: FinancialLocked`

NLB instance is locked.


* Normal

* FinancialLocked: Being locked.



**OverdueTime ** <span data-label="purple">String </span>`Example: 2023-07-17T01:37:38Z`

Locked time of the NLB instance.

When the `BillingStatus` parameter is set to `Normal`, this parameter returns an empty string.



**ReclaimedTime ** <span data-label="purple">String </span>`Example: 2023-08-17T01:37:38Z`

Expected reclaim time of the NLB instance.



**ExpectedOverdueTime ** <span data-label="purple">String </span>`Example: 2023-07-17T01:37:38Z`

The suspension time of the NLB instance due to overdue payment.



**Ipv4BandwidthPackageId ** <span data-label="purple">String </span>`Example: bwp-2zeo05qre24nhrqpy****`

ID of the IPv4 Bandwidth Package.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">When the instance is not added to the IPv4 Bandwidth Package, this field returns an empty string.</div>




**Ipv6BandwidthPackageId ** <span data-label="purple">String </span>`Example: bwp-b2weev3esweer8mt****`

ID of the dual\-stack Bandwidth Package.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">When the instance is IPv4 type or the instance is not added to the IPv6 Bandwidth Package, this field returns an empty string.</div>




**VpcId ** <span data-label="purple">String </span>`Example: vpc-bp1aevy8sofi8mh1****`

The ID of the VPC to which the NLB instance belongs.



**ManagedSecurityGroupId ** <span data-label="purple">String </span>`Example: sg-bp1aevy8sofi8mh1****`

The managed security group ID automatically associated by the system with the NLB instance.



**SecurityGroupIds ** <span data-label="purple">String[] </span>`Example: ["sg-bpo05q8so05qmh1****", "sg-5eorfq84r05rfmhw****"]`

ID of the non\-managed security group attached to the NLB instance.



**ModificationProtectionStatus ** <span data-label="purple">String </span>`Example: ConsoleProtection`

Enable console modification protection for the NLB instance.


* NonProtection or empty: Disable, allowing modification or deletion of the instance via the console.

* ConsoleProtection: Enable, prohibiting modifications or deletion of the instance via the console.



**Tags ** <span data-label="purple">Object[] </span>`Example: --`

Tag information of the NLB instance.


**Key ** <span data-label="purple">String </span>`Example: k1`

The tag key.



**Value ** <span data-label="purple">String </span>`Example: v1`

The tag value.




**ZoneMappings ** <span data-label="purple">Object[] </span>`Example: --`

Availability zone information of the NLB instance.


**ZoneId ** <span data-label="purple">String </span>`Example: cn-beijing-a`

Availability Zone ID.



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

ID of the Elastic IP (EIP) associated with the NLB instance.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">When the IPv4 network type of the NLB instance is "Intranet", this parameter returns an empty string.</div>




**Ipv6EipId ** <span data-label="purple">String </span>`Example: eip-2zaiwb7ujxscd****`

ID of the IPv6 Internet bandwidth associated with the NLB instance.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">When the IPv6 network type of the NLB instance is "Intranet" or the IP version of the NLB instance is "ipv4", this parameter returns an empty string.</div>




**Ipv4HcStatus ** <span data-label="purple">String </span>`Example: Healthy`

Health status of the private IPv4 address of the NLB instance.


* Healthy: Normal.

* Unhealthy: Exception.



**Ipv6HcStatus ** <span data-label="purple">String </span>`Example: Healthy`

Health status of the private IPv6 address of the NLB instance.


* Healthy: Normal.

* Unhealthy: Exception.





&nbsp;

<span id=".6K-35rGC56S65L6L"></span>
## Request examples

```json
GET /?Action=DescribeNetworkLoadBalancers&Version=2020-04-01&MaxResults=10&NextToken=caeba0bbb2be03f84eb48b699f0a****&LoadBalancerIds.1=nlb-bp1b6c719dfa08ex****&VpcId=vpc-13fd2oy7dsiyo3n6nu4ye****&LoadBalancerName=nlb-test&Status=Active&IpAddressVersion=ipv4&ZoneId=cn-beijing-a&ProjectName=default&TagFilters.1.Key=k1&TagFilters.1.Values.1=v1 HTTP/1.1
Host: clb.cn-beijing.byteplusapi.com.cn
Date: 20260310T094038Z
Authorization: HMAC-SHA256 Credential=Adfks******wekfwe/20251121/cn-beijing/clb/request, SignedHeaders=host;x-date, Signature=47a7d934ff7b37c03938******cd7b8278a40a1057690c401e92246a0e41085f
```


<span id=".6L-U5Zue56S65L6L"></span>
## Response examples

```json
{
    "ResponseMetadata": {
        "RequestId": "20230604110420****100232280022D31",
        "Action": "DescribeNetworkLoadBalancers",
        "Version": "2020-04-01",
        "Service": "clb",
        "Region": "cn-beijing"
    },
    "Result": {
        "LoadBalancers": [
            {
                "Tags": [
                    {
                        "Key": "k1",
                        "Value": "v1"
                    }
                ],
                "VpcId": "vpc-bp1aevy8sofi8mh1****",
                "Status": "Active",
                "DNSName": "nlb-b2ea3vwwssefdmer****.cn-beijing.volces.com",
                "AccountId": "210012****",
                "CreateTime": "2024-08-11T16:37:37Z",
                "UpdateTime": "2024-08-11T16:37:37Z",
                "BillingType": 3,
                "Description": "test",
                "OverdueTime": "2023-07-17T01:37:38Z",
                "ProjectName": "default",
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
                        "Ipv4EipAddress": "22.XX.XX.22"
                    }
                ],
                "BillingStatus": "FinancialLocked",
                "ReclaimedTime": "2023-08-17T01:37:38Z",
                "LoadBalancerId": "nlb-bp1o94dp5i6ea****",
                "Ipv4NetworkType": "intranet",
                "Ipv6NetworkType": "intranet",
                "CrossZoneEnabled": true,
                "IpAddressVersion": "ipv4",
                "LoadBalancerName": "nlb-test",
                "SecurityGroupIds": [
                    "sg-bpo05q8so05qmh1****",
                    "sg-5eorfq84r05rfmhw****"
                ],
                "ExpectedOverdueTime": "2023-07-17T01:37:38Z",
                "Ipv4BandwidthPackageId": "bwp-2zeo05qre24nhrqpy****",
                "Ipv6BandwidthPackageId": "bwp-b2weev3esweer8mt****",
                "ManagedSecurityGroupId": "sg-bp1aevy8sofi8mh1****",
                "ModificationProtectionStatus": "ConsoleProtection"
            }
        ],
        "NextToken": "caeba0bbb2be03f84eb48b699f0a****",
        "RequestId": "202409291106382514606306AF947C****"
    }
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error codes

This section displays only the error codes of the current API. For more error codes, see [Common error codes](https://docs.byteplus.com/en/docs/clb/NLB-Common-Error-Codes).


|Status code |Error codes |Error message |Notes |
|---|---|---|---|
|400 |DryRunOperation |Exception raised to indicate a successfully authorized action when the DryRun flag is set to true. |This request is set to DryRun. The action is authorized but not executed. |
|400 |IdempotentParameterMismatch |Arguments on this idempotent request are inconsistent with arguments used in previous request(s). |The parameters of this idempotent request are inconsistent with those used in the previous request. |
|400 |InvalidClientToken.Malformed |The specified ClientToken is malformed. |The specified ClientToken format is invalid. |
|400 |InvalidIncorrectOrder.Malformed |The specified index order is malformed. |The specified index order parameter format is invalid. |
|400 |InvalidLoadBalancerName.Malformed |The specified LoadBalancerName is malformed. |The specified LoadBalancerName format is invalid. |
|400 |InvalidMaxResult.Malformed |The specified MaxResult is malformed. |The specified MaxResult parameter format is invalid. |
|400 |InvalidMaxResults.Malformed |The specified MaxResults is malformed. |The specified MaxResults parameter format is invalid. |
|400 |InvalidNextToken.Malformed |The specified NextToken is malformed. |The specified NextToken parameter format is invalid. |
|400 |InvalidPaging.Malformed |The specified PageNumber or PageSize is malformed. |The format specified for pagination parameter is invalid. |
|400 |InvalidTagKey.Malformed |The specified TagKey is malformed. |The specified TagKey parameter format is invalid. |
|400 |InvalidTagValue.Malformed |The specified TagValue is malformed. |The specified TagValue parameter format is invalid. |
|400 |LimitExceeded.TagFilterKey |You've reached the limit on the number of tag keys that you can filter. |You have reached the maximum number of filter tag keys that can be specified in a single request. |
|400 |LimitExceeded.TagFilterValues |You've reached the limit on the number of tag values that you can filter. |The maximum tag key\-value pairs for filtering in a single request has been reached. |
|409 |InvalidOperation.Conflict |The specified resource operation conflicts. |The specified resource action conflicted. |
|412 |IdempotentProcessing |The request uses the same client token as a previous one that is still in process. |The idempotent request is in progress. |
