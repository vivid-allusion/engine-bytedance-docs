---
title: "DescribeLoadBalancers - Querying a CLB list"
product: "Cloud Load Balancer"
product_code: "clb"
source: "https://docs.byteplus.com/en/docs/clb/DescribeLoadBalancers"
---

Call the DescribeLoadBalancers API to query CLB instances that meet the specified conditions.

<span id=".5L2_55So6K-05piO"></span>
## Instructions


* Pass in multiple request parameters, query based on the passed parameters, and return CLB instances that meet all the conditions. If no CLB instance meets the conditions, return an empty value.

* If none of the non\-required request parameters are passed, query based on the currently logged\-in account and return all CLB instances under the current account.


<span id=".6LCD6K-V"></span>
## Debug

[去调试](https://api.byteplus.com/api-explorer/debug?action=DescribeLoadBalancers&serviceCode=clb&version=2020-04-01&groupName=)


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters



**Action ** <span data-label="purple">String </span><span data-api-tag="require|HgZTsd">必选</span> `Example: DescribeLoadBalancers`

Action to execute. Set the value to **DescribeLoadBalancers**.



**Version ** <span data-label="purple">String </span><span data-api-tag="require|XwYtgL">必选</span> `Example: 2020-04-01`

API version. The current version is **2020\-04\-01**.



**LoadBalancerName ** <span data-label="purple">String </span>`optional` `Example: clb-test`

Name of the CLB instance.



**LoadBalancerIds.N ** <span data-label="purple">String </span>`optional` `Example: clb-bp1b6c719dfa08ex****`

CLB instance ID.


* Parameter \- N: Represents the serial number of the CLB instance ID, ranging from 1 to 20.

* Separate multiple CLB instance IDs with ampersands (&).



**InstanceIds.N ** <span data-label="purple">String </span>`optional` `Example: eni-2feo5qd3orri85oxruvxv***`

Backend server ID of the CLB.


* Parameter \- N: Specifies the serial number of the backend server ID, ranging from 1 to 20.

* Separate multiple backend server IDs with ampersands (&).



**InstanceIps.N ** <span data-label="purple">String </span>`optional` `Example: 192.168.1.66`

IP address of the CLB backend server.


* Parameter \- N: Specifies the serial number of the backend server IP, ranging from 1 to 20.

* Separate multiple backend server IPs with ampersands (&).



**MasterZoneId ** <span data-label="purple">String </span>`optional` `Example: cn-shanghai-a`

Primary Availability Zone ID of the CLB instance.

You can call the [DescribeZones](https://docs.byteplus.com/en/docs/clb/DescribeZones) API to query the primary availability zone ID.



**AddressIpVersion ** <span data-label="purple">String </span>`optional` `Example: ipv4`

IP address type of the CLB instance. Valid values:


* ipv4: IPv4 only.

* DualStack: dual stack, supporting both IPv4 and IPv6.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Dual\-stack CLB feature is currently in beta stage. If you need a trial, please contact your account manager.</div>




**Type ** <span data-label="purple">String </span>`optional` `Example: private`

Network type of the CLB instance.


* Public: Internet.

* private: VPC.



**VpcId ** <span data-label="purple">String </span>`optional` `Example: vpc-13fd2oy7dsiyo3n6nu4ye****`

The VPC ID to which the CLB instance belongs.

You can call the [DescribeVpcs](https://docs.byteplus.com/en/docs/vpc/DescribeVpcs) API to query the VPC ID.



**EniAddress ** <span data-label="purple">String </span>`optional` `Example: 192.XX.XX.06`

Private IPv4 address of the CLB instance.

You can call the [DescribeLoadBalancerAttributes](https://docs.byteplus.com/en/docs/clb/DescribeLoadBalancerAttributes) API to query the private IPv4 address of the CLB instance.



**EipAddress ** <span data-label="purple">String </span>`optional` `Example: 10.XX.XX.4`

EIP address bound to the CLB instance.

You can call the [DescribeEipAddresses](https://docs.byteplus.com/en/docs/eip/DescribeEipAddressAttributes) API to query the EIP addresses of CLB instances.



**Status ** <span data-label="purple">String </span>`optional` `Example: Active`

CLB instance status. Valid values:


* Inactive: Disabled.

* Active: Running.

* Creating

* Provisioning: Creating.

* Configuring: Pending.

* Deleting

* CreateFailed: Creation failed.



**ProjectName ** <span data-label="purple">String </span>`optional` `Example: default`

The name of the project to which the CLB instance belongs.



**TagFilters.N.Key ** <span data-label="purple">String </span>`optional` `Example: k1`

The tag key.


* N represents the sequence number of a tag key. Values: 1\-10.

* Separate multiple tag keys with &. Multiple tag keys have a logical AND relationship. The query returns CLBs tagged with all the specified keys.

* Duplicate values are not allowed.



**TagFilters.N.Values.N ** <span data-label="purple">String </span>`optional` `Example: v1`

The tag value.


* The first N specifies the serial number of a tag key. Valid values: 1–10.

* The second N represents the serial number of the tag value. Valid values: 1–3. Multiple tag values under the same tag key are combined using a logical OR operation, meaning the query returns CLBs that have any of the specified tag values for that key.

* Separate multiple tag values with ampersands (&).


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">If this parameter is passed in, <code>TagFilters.N.Key</code> must be passed in first.</div>


* <div data-tips="true" data-tips-type="tip">When an empty string is passed, it indicates querying CLB instances with empty tag values.</div>




**PageNumber ** <span data-label="purple">Integer </span>`optional` `Example: 1`

The page number of the list. Default: 1.



**PageSize ** <span data-label="purple">Integer </span>`optional` `Example: 10`

The number of rows per page when paginating queries. Value range: 1 to 100. Default: 10.



&nbsp;

<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters



**RequestId ** <span data-label="purple">String </span>`Example: 202108161106382514606306AF947C****`

Request ID.



**TotalCount ** <span data-label="purple">Integer </span>`Example: 50`

Total number of instances that meet the conditions.



**PageNumber ** <span data-label="purple">Integer </span>`Example: 1`

Current page number.



**PageSize ** <span data-label="purple">Integer </span>`Example: 10`

The number of rows on the current page.



**LoadBalancers ** <span data-label="purple">Object[] </span>`Example: --`

Details of CLB instances that meet the conditions.


**AccountId ** <span data-label="purple">String </span>`Example: 210012****`

Account ID of the CLB instance.



**LoadBalancerId ** <span data-label="purple">String </span>`Example: clb-bp1o94dp5i6ea****`

CLB Instance ID.



**LoadBalancerName ** <span data-label="purple">String </span>`Example: clb-test`

Name of the CLB instance.



**Description ** <span data-label="purple">String </span>`Example: test instance`

Description of the CLB instance.



**Type ** <span data-label="purple">String </span>`Example: private`

Type of the CLB instance.



**AddressIpVersion ** <span data-label="purple">String </span>`Example: ipv4`

IP address type of the CLB instance.



**LoadBalancerBillingType ** <span data-label="purple">Integer </span>`Example: 2`

Metering methods of the CLB instance.


* 1: Subscription

* 2: Pay\-by\-Specification

* 3: Pay\-by\-CU


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Pay\-by\-CU is in the beta stage. To request a trial, please contact your account manager.</div>




**LoadBalancerSpec ** <span data-label="purple">String </span>`Example: small_1`

The specification of the CLB instance.

When the parameter LoadBalancerBillingType returns 3, this parameter returns empty.



**MasterZoneId ** <span data-label="purple">String </span>`Example: cn-shanghai-a`

Primary Availability Zone ID of the CLB instance.



**SlaveZoneId ** <span data-label="purple">String </span>`Example: cn-shanghai-b`

Secondary Zone ID of the CLB Instance.

Returns empty if the CLB instance is a single\-zone instance.



**VpcId ** <span data-label="purple">String </span>`Example: vpc-bp1aevy8sofi8mh1****`

The VPC ID to which the CLB instance belongs.



**SubnetId ** <span data-label="purple">String </span>`Example: subnet-bp12mw1f8k3jgy****`

The subnet ID to which the CLB instance belongs.



**EniID ** <span data-label="purple">String </span>`Example: eni-2fe6rabqt8gxruv8u8c9f****`

Occupied Network interface ID of the CLB Instance.



**EniAddress ** <span data-label="purple">String </span>`Example: 172.XX.XX.33`

Private IPv4 address of the CLB instance.



**EniAddressNum ** <span data-label="purple">Integer </span>`Example: 2`

The number of private IPv4 addresses of the CLB instance.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">This parameter is currently in Beta stage. For trial requests, please contact your account manager.</div>




**EniAddresses ** <span data-label="purple">Object[] </span>`Example:--`

Private IPv4 address information of the CLB instance.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">This parameter is currently in Beta stage. For trial requests, please contact your account manager.</div>



**EniAddress ** <span data-label="purple">String </span>`Example: 172.XX.XX.33`

Private IPv4 address of the CLB instance.



**EipId ** <span data-label="purple">String </span>`Example: eip-3ciyamhu46c6rrswwusg****`

The ID of the EIP bound to the private IPv4 address.



**EipAddress ** <span data-label="purple">String </span>`Example: 10.XX.XX.27`

The Elastic IP (EIP) address associated with the private IPv4 address.




**EipID ** <span data-label="purple">String </span>`Example: eip-3ciyamhu46c6rrswwusg****`

EIP ID associated with the CLB instance.



**EipAddress ** <span data-label="purple">String </span>`Example: 10.XX.XX.27`

EIP Address of the CLB instance.



**EniIpv6Address ** <span data-label="purple">String </span>`Example: 2408:4005:XX:XX:200`

Private IPv6 address of the CLB instance.



**Ipv6EipId ** <span data-label="purple">String </span>`Example: eip-2zaiwb7ujxscd****`

ID of the IPv6 Internet bandwidth.



**ModificationProtectionStatus ** <span data-label="purple">String </span>`Example: ConsoleProtection`

Enable console modification protection for the CLB instance.

After enabling, modifying or deleting the instance via the console is prohibited.


* NonProtection or Empty: Disabled

* ConsoleProtection: Enable.



**ModificationProtectionReason ** <span data-label="purple">String </span>`Example: Managed instance`

Reason for setting modification protection status.

This parameter is valid only when the parameter `ModificationProtectionStatus` is set to ConsoleProtection.



**ServiceManaged ** <span data-label="purple">Boolean </span>`Example: true`

Whether the CLB instance is a managed resource.


* true: Managed resource. Indicates that the CLB resource was automatically created by the system when other cloud resources (besides the CLB) were created.

* false: Not a managed resource. Indicates that the CLB resource was created manually on the CLB platform.



**Status ** <span data-label="purple">String </span>`Example: Active`

CLB instance status.



**BusinessStatus** <span data-label="purple">String</span> `Example: FinancialLocked`

CLB Instance is locked


* Normal

* FinancialLocked: Being locked.

* Returns empty if the instance is not locked.



**LockReason ** <span data-label="purple">String </span>`Example: Financial`

The reason why the CLB instance is locked.


* Financial: Being locked due to arrears.

* When the parameter `BusinessStatus` is "Normal" or empty, this parameter returns empty.



**ProjectName ** <span data-label="purple">String </span>`Example: default`

The name of the project to which the CLB instance belongs.



**Tags ** <span data-label="purple">Object[] </span>`Example: --`

Tag information of the CLB instance.


**Key ** <span data-label="purple">String </span>`Example: k1`

The tag key.



**Value ** <span data-label="purple">String </span>`Example: v1`

The tag value.




**BypassSecurityGroupEnabled ** <span data-label="purple">String </span>`Example: off`

Whether the "Allow Backend Security Group Access" feature is enabled for the CLB instance.


* on: Enable.

* off: Disable.



**TimestampRemoveEnabled ** <span data-label="purple">String </span>`Example: off`

Whether to enable the function of stripping TCP/HTTP/HTTPS packet timestamps


* on: Enable.

* off: Disable.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">This feature is currently in Beta stage. For trial requests, please contact your account manager.</div>




**CreateTime ** <span data-label="purple">String </span>`Example: 2021-08-11T16:37:37Z`

Creation time of the CLB instance.



**UpdateTime ** <span data-label="purple">String </span>`Example: 2021-08-11T16:37:37Z`

Last modified time of the CLB instance.



**OverdueTime ** <span data-label="purple">String </span>`Example: 2021-08-11T16:37:37Z`

The time when the CLB instance was frozen.

When the parameter `BusinessStatus` is "Normal" or empty, this parameter returns empty.



**DeletedTime ** <span data-label="purple">String </span>`Example: 2021-08-11T16:37:37Z`

Scheduled Reclaim Time of the CLB Instance.



**ExpiredTime ** <span data-label="purple">String </span>`Example: 2021-08-11T23:59:59Z`

Expiration Time of the CLB Instance.

This parameter is returned only when the parameter `LoadBalancerBillingType` is set to 1.




&nbsp;

<span id=".6K-35rGC56S65L6L"></span>
## Request examples

```json
GET /?Action=DescribeLoadBalancers&Version=2020-04-01&ExclusiveClusterId=ec-bp1o94dp5i6ea****&LoadBalancerName=clb-test&LoadBalancerIds.1=clb-bp1b6c719dfa08ex****&InstanceIds.1=eni-2feo5qd3orri85oxruvxv***&InstanceIps.1=192.168.1.66&MasterZoneId=cn-shanghai-a&AddressIpVersion=ipv4&Type=private&VpcId=vpc-13fd2oy7dsiyo3n6nu4ye****&EniAddress=192.XX.XX.06&EipAddress=10.XX.XX.4&Status=Active&ProjectName=default&TagFilters.1.Key=k1&TagFilters.1.Values.1=v1&PageNumber=1&PageSize=10
Host: clb.cn-beijing.byteplusapi.com.cn
X-Date: 20251121T094038Z
Authorization: HMAC-SHA256 Credential=Adfks******wekfwe/20251121/cn-beijing/clb/request, SignedHeaders=host;x-date, Signature=47a7d934ff7b37c03938******cd7b8278a40a1057690c401e92246a0e41085f
```


<span id=".6L-U5Zue56S65L6L"></span>
## Response examples

```json
{
    "ResponseMetadata": {
        "RequestId": "20230604110420****100232280022D31",
        "Action": "DescribeLoadBalancers",
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
                "Type": "private",
                "EipID": "eip-3ciyamhu46c6rrswwusg****",
                "EniID": "eni-2fe6rabqt8gxruv8u8c9f****",
                "VpcId": "vpc-bp1aevy8sofi8mh1****",
                "Status": "Active",
                "SubnetId": "subnet-bp12mw1f8k3jgy****",
                "AccountId": "210012****",
                "Ipv6EipId": "eip-2zaiwb7ujxscd****",
                "CreateTime": "2021-08-11T16:37:37Z",
                "EipAddress": "10.XX.XX.27",
                "EniAddress": "172.XX.XX.33",
                "LockReason": "Financial",
                "UpdateTime": "2021-08-11T16:37:37Z",
                "DeletedTime": "2021-08-11T16:37:37Z",
                "Description": "测试实例",
                "ExpiredTime": "2021-08-11T23:59:59Z",
                "OverdueTime": "2021-08-11T16:37:37Z",
                "ProjectName": "default",
                "SlaveZoneId": "cn-shanghai-b",
                "EniAddresses": [
                    {
                        "EipId": "eip-3ciyamhu46c6rrswwusg****",
                        "EipAddress": "10.XX.XX.27",
                        "EniAddress": "172.XX.XX.33"
                    }
                ],
                "MasterZoneId": "cn-shanghai-a",
                "EniAddressNum": 2,
                "BusinessStatus": "FinancialLocked",
                "EniIpv6Address": "2408:4005:XX:XX:200",
                "LoadBalancerId": "clb-bp1o94dp5i6ea****",
                "ServiceManaged": true,
                "AddressIpVersion": "ipv4",
                "LoadBalancerName": "clb-test",
                "LoadBalancerSpec": "small_1",
                "ExclusiveClusterId": "ec-bp1o94dp5i6ea****",
                "TimestampRemoveEnabled": "off",
                "LoadBalancerBillingType": 2,
                "BypassSecurityGroupEnabled": "off",
                "ModificationProtectionReason": "托管实例",
                "ModificationProtectionStatus": "ConsoleProtection"
            }
        ],
        "PageNumber": 1,
        "PageSize": 10,
        "RequestId": "202108161106382514606306AF947C****",
        "TotalCount": 50
    }
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error codes

This section displays only the error codes of the current API. For more error codes, see [Common error codes](https://docs.byteplus.com/en/docs/clb/Public-error-codes).


|Status code |Error codes |Error message |Notes |
|---|---|---|---|
|400 |InvalidEipAddress.Malformed |The specified EipAddress is malformed. |The specified EipAddress parameter format is invalid. |
|400 |InvalidEniAddress.Malformed |The specified EniAddress is malformed. |The specified EniAddress parameter format is invalid. |
|400 |InvalidIncorrectOrder.Malformed |The specified index order is malformed. |The specified index order parameter format is invalid. |
|400 |InvalidInstanceIp.Malformed |The specified InstanceIp is malformed. |The specified InstanceIp parameter format is invalid. |
|400 |InvalidName.Malformed |The specified Name is malformed. |The format specified for Name is invalid. |
|400 |InvalidPageNumber.Malformed |The specified PageNumber is malformed. |The specified PageNumber parameter format is invalid. |
|400 |InvalidPageSize.Malformed |The specified PageSize is malformed. |The specified PageSize parameter format is invalid. |
|400 |InvalidPaging.Malformed |The specified PageNumber or PageSize is malformed. |The format specified for pagination parameter is invalid. |
|400 |InvalidTagKey.Malformed |The specified TagKey is malformed. |The specified TagKey parameter format is invalid. |
|400 |InvalidTagValue.Malformed |The specified TagValue is malformed. |The specified TagValue parameter format is invalid. |
|400 |LimitExceeded.LoadBalancerIdNumber |You've reached the limit on the number of description LoadBalancer that you can operate. |The maximum number of Load Balancers allowed for a single query has been reached. |
|400 |LimitExceeded.ServerInstanceIdNumber |You've reached the limit on the number of description ServerInstanceId that you can operate. |The maximum number of server IDs that can be queried in a single request has been reached. |
|400 |LimitExceeded.ServerInstanceIpNumber |You've reached the limit on the number of description ServerInstanceIp that you can operate. |The maximum number of server IPs that can be queried in a single request has been reached. |
|400 |LimitExceeded.TagFilterKey |You've reached the limit on the number of tag keys that you can filter. |You have reached the maximum number of filter tag keys that can be specified in a single request. |
|400 |LimitExceeded.TagFilterValues |You've reached the limit on the number of tag values that you can filter. |The maximum tag key\-value pairs for filtering in a single request has been reached. |
|400 |MissingParameter |The request is missing a required parameter. Ensure that you have supplied all the required parameters for the request; for example, the ''. |This request is missing a required parameter. Ensure the request includes all required parameters, such as . |
|500 |InternalError |An internal error has occurred. |An internal error occurred. |
