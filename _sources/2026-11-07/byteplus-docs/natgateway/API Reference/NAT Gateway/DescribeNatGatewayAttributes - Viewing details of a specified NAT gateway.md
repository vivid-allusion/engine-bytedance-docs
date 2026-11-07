---
title: "DescribeNatGatewayAttributes - Viewing details of a specified NAT gateway"
product: "NAT Gateway"
product_code: "natgateway"
source: "https://docs.byteplus.com/en/docs/natgateway/DescribeNatGatewayAttributes"
---

Call the DescribeNatGatewayAttributes API to view the details of a NAT gateway.

<span id=".6LCD6K-V"></span>
## Debug

[去调试](https://api.byteplus.com/api-explorer/?action=DescribeNatGatewayAttributes&groupName=NAT%E7%BD%91%E5%85%B3&serviceCode=natgateway&version=2020-04-01)


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters

The following only details request parameters specific to this API and key common parameters. For more information, see [Common parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).



**Action ** <span data-label="purple">string </span><span data-api-tag="require|Kqnx5e">必选</span> `Example: DescribeNatGatewayAttributes`

The action that you want to perform. Value: DescribeNatGatewayAttributes.



**Version ** <span data-label="purple">string </span><span data-api-tag="require|OyQjKf">必选</span> `Example: 2020-04-01`

The API version. Value: 2020\-04\-01.



**NatGatewayId ** <span data-label="purple">string </span><span data-api-tag="require|7LhwwE">必选</span> `Example: ngw-0x57a0gevp****`

ID of the NAT gateway.



&nbsp;

<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters

The following only details response parameters specific to this API. For more information, see [Response structure](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response).



**SmartScheduleEnabled ** <span data-label="purple">boolean </span>`Example: false`

Describe whether smart scheduling is enabled.


* true: Yes.

* false: No.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">This feature is currently available for trial only to accounts with enterprise authentication. If you need a trial, please contact your account manager.</div>




**SmartScheduleRule ** <span data-label="purple">string </span>`Example: BGP`

The smart scheduling policy rule.


* ChinaMobile: China Mobile.

* ChinaUnicom: China Unicom.

* ChinaTelecom: China Telecom.

* BGP: BGP multi\-ISP.



**NatIpAddresses ** <span data-label="purple">object[] </span>`Example: -`

The NAT IP list of VPC NAT gateways.


**NatIpId ** <span data-label="purple">string </span>`Example: vpcnatip-gw8y7q3cpk3fggs87****`

The ID of the NAT IP address.



**NatIpAddress ** <span data-label="purple">string </span>`Example: 192.168.XX.34`

The address of the NAT IP.




**DirectMode ** <span data-label="purple">boolean </span>`Example: true`

Describe whether the NAT gateway is in direct mode.


* true: Yes.

* false: No.



**NatGatewayId ** <span data-label="purple">string </span>`Example: ngw-3tex2x1cwd4c6c0v****`

ID of the NAT gateway



**NatGatewayName ** <span data-label="purple">string </span>`Example: nat-01`

Name of the NAT gateway.



**Description ** <span data-label="purple">string </span>`Example: This is a nat`

Description of the NAT gateway.



**RequestId ** <span data-label="purple">string </span>`Example: 2021062415303301022514515207C4****`

Request ID.



**Spec ** <span data-label="purple">string </span>`Example: Medium`

The specification of the NAT gateway.


* Small (default)

* Medium

* Large



**EipAddresses ** <span data-label="purple">object[] </span>`Example: -`

The information about the EIP associated with the NAT gateway.


**AllocationId ** <span data-label="purple">string </span>`Example: eip-rs59q8hqtaf****`

The ID of the elastic IP address (EIP).



**EipAddress ** <span data-label="purple">string </span>`Example: 121.XX.XX.52`

Address of the EIP.



**UsingStatus ** <span data-label="purple">string </span>`Example: Idle`

The usage status of the EIP.


* Idle: Not in use.

* UsedBySnat: Used by the SNAT rule.

* UsedByDnat: Used by the DNAT rule.

* UsedByNat: Used by both SNAT and DNAT rules.




**VpcId ** <span data-label="purple">string </span>`Example: vpc-7dk2hs5smt0bu****`

ID of the Virtual Private Cloud (VPC) to which the NAT gateway belongs.



**SubnetId ** <span data-label="purple">string </span>`Example: subnet-mj6v3t43k05s****`

ID of the subnet to which the NAT gateway belongs.



**ProjectName ** <span data-label="purple">string </span>`Example: Project_1`

The name of the project to which the NAT gateway belongs.



**ZoneId ** <span data-label="purple">string </span>`Example: cn-beijing-a`

ID of the primary availability zone to which the NAT gateway belongs.



**NetworkInterfaceId ** <span data-label="purple">string </span>`Example: eni-2dffi32452fcv2****`

ID of the network interface occupied by the NAT gateway.



**Tags ** <span data-label="purple">object[] </span>`Example: -`

Tag information of the NAT gateway.


**Key ** <span data-label="purple">string </span>`Example: k1`

The tag key.



**Value ** <span data-label="purple">string </span>`Example: v1`

The tag value.




**BillingType ** <span data-label="purple">integer </span>`Example: 2`

The metering method of the NAT Gateway.


* 1: Subscription.

* 2: Pay\-by\-Specification

* 3: Pay\-by\-CU.



**DeletedTime ** <span data-label="purple">string </span>`Example: 2021-12-21 18:26:27`

The time when the resource is scheduled to be forcibly reclaimed.


* This parameter returns a value for Subscription NAT gateways.

* For Pay\-as\-you\-go NAT gateways, this parameter returns a value only if arrears\-related freezing occurs.



**OverdueTime ** <span data-label="purple">string </span>`Example: 2021-12-06 18:26:27`

The time when the resource is frozen. This parameter returns a value only if the resource is frozen due to overdue payments.



**ExpiredTime ** <span data-label="purple">string </span>`Example: 2021-05-07 23:59:59`

The time when the Subscription NAT gateway expires. This parameter returns a value only for Subscription NAT gateways.



**UpdatedAt ** <span data-label="purple">string </span>`Example: 2021-12-06T18:26:27+08:00`

The time when the NAT gateway is last operated.



**CreationTime ** <span data-label="purple">string </span>`Example: 2021-11-30T16:59:27+08:00`

The time when the NAT gateway is created.



**LockReason ** <span data-label="purple">string </span>`Example: financial`

The reason why the NAT gateway instance is locked.


* financial: Being locked due to arrears.

* security: Being locked due to security.



**BusinessStatus ** <span data-label="purple">string </span>`Example: Normal`

Describe whether the NAT gateway is locked.


* Null: Normal and not locked.

* Normal: Normal and not locked.

* FinancialLocked: Being locked due to arrears.



**Status ** <span data-label="purple">string </span>`Example: Available`

Status of the NAT gateway.


* Available

* Creating

* Pending: Action in progress​.

* Deleting



**NetworkType ** <span data-label="purple">string </span>`Example: internet`

The type of the NAT gateway.


* internet: Internet NAT Gateway.

* intranet: VPC NAT Gateway.



**SnatEntryIds ** <span data-label="purple">string[] </span>`Example: snat-3fvhk47kf56****`

List of SNAT rule IDs.



**DnatEntryIds ** <span data-label="purple">string[] </span>`Example: dnat-342abc3bc3****`

List of DNAT rule IDs.



&nbsp;

<span id=".6K-35rGC56S65L6L"></span>
## Request examples

```text
GET /?Action=DescribeNatGatewayAttributes&Version=2020-04-01&NatGatewayId=ngw-2fesmko5zhdz459gp67sc**** HTTP/1.1
Host: natgateway.cn-beijing.byteplusapi.com.cn
ServiceName: natgateway
Region: cn-beijing
```


<span id=".6L-U5Zue56S65L6L"></span>
## Response examples

```json
{
  "ResponseMetadata": {
    "RequestId": "20251223184826030017116094AB30B8",
    "Action": "DescribeNatGatewayAttributes",
    "Version": "2020-04-01",
    "Service": "natgateway",
    "Region": "cn-beijing"
  },
  "Result": {
    "SmartScheduleEnabled": true,
    "SmartScheduleRule": "BGP",
    "NatIpAddresses": [],
    "DirectMode": true,
    "NatGatewayId": "ngw-3tex2x1cwd4c6c0v****",
    "NatGatewayName": "nat-01",
    "Description": "This is a nat",
    "RequestId": "2021062415303301022514515207C4****",
    "Spec": "Medium",
    "EipAddresses": [],
    "VpcId": "vpc-7dk2hs5smt0bu****",
    "SubnetId": "subnet-mj6v3t43k05s****",
    "ProjectName": "Project_1",
    "ZoneId": "cn-beijing-a",
    "NetworkInterfaceId": "eni-2dffi32452fcv2****",
    "Tags": [],
    "BillingType": 2,
    "DeletedTime": "2021-12-21 18:26:27",
    "OverdueTime": "2021-12-06 18:26:27",
    "ExpiredTime": "2021-05-07 23:59:59",
    "UpdatedAt": "2021-12-06T18:26:27+08:00",
    "CreationTime": "2021-11-30T16:59:27+08:00",
    "LockReason": "financial",
    "BusinessStatus": "Normal",
    "Status": "Available",
    "NetworkType": "internet",
    "SnatEntryIds": [
      "snat-3fvhk47kf56****"
    ],
    "DnatEntryIds": [
      "dnat-342abc3bc3****"
    ]
  }
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error codes

The table below describes the error codes for this API that are associated with business logic. For details, see [Common error codes](https://docs.byteplus.com/en/docs/natgateway/Public-error-codes).


|Status code |Error codes |Error message |Description |
|---|---|---|---|
|400 |MissingParameter |The request is missing a required parameter. |This request does not contain required parameters. |
|404 |InvalidNatGateway.NotFound |The specified NAT gateway does not exist. |The specified NAT gateway does not exist. |
|500 |InternalError |An internal error has occurred. |An internal error occurred. |
