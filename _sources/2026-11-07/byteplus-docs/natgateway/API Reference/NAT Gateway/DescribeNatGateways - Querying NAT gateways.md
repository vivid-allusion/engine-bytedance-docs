---
title: "DescribeNatGateways - Querying NAT gateways"
product: "NAT Gateway"
product_code: "natgateway"
source: "https://docs.byteplus.com/en/docs/natgateway/DescribeNatGateways"
---

Call the DescribeNatGateways API to query NAT gateway instances that meet the specified conditions.

## Instructions

* If multiple request parameters are provided, the system will query based on these parameters and return all NAT gateways that meet all the specified conditions. An empty list is returned if no qualified NAT gateways exist.

* If no optional parameters are provided, the system will query based on the currently logged\-in account, and return all NAT gateways under that account.

* When using a tag to filter NAT gateway instances, you can query up to 1,000 instances associated with the specified tag. If the number of NAT gateway instances associated with a specified tag exceeds 1,000, use the [ListTagsForResources](https://docs.byteplus.com/en/docs/natgateway/ListTagsForResources) API to query.

## Debug

[去调试](https://api.byteplus.com/api-explorer/?action=DescribeNatGateways&groupName=NAT%E7%BD%91%E5%85%B3&serviceCode=natgateway&version=2020-04-01)

## Request parameters

The following only details request parameters specific to this API and key common parameters. For more information, see [Common parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).

**Action ** string必选 `Example: DescribeNatGateways`

The action that you want to perform. Value: DescribeNatGateways.

**Version ** string必选 `Example: 2020-04-01`

The API version. Value: 2020\-04\-01.

**Description ** string`optional` `Example: This is a NAT`

Description of the NAT gateway.

**TagFilters.N.Values.N ** string[]`optional` `Example: v1`

The tag value of the NAT gateway.

* The first N represents the serial number of the tag key. Valid values: 1–10.

* The second N represents the serial number of the tag value. Valid values: 1–3. The relationship between multiple tag values for the same tag key is a logical "OR". That is, the query returns NAT gateways tagged with any one of the specified values.

* Separate multiple tag values with ampersands (&).

> **tip**

* > To provide this parameter, provide TagFilters.N.Key first.

* > If an empty string is provided, the query returns NAT gateways that have the specified tag key with an empty value.

**TagFilters.N.Key ** string[]`optional` `Example: k1`

The tag key of the NAT gateway.

* N represents the serial number of the tag key. Valid values: 1\-10.

* Separate multiple tag keys with &. The relationship between multiple tag keys is a logical "AND". That is, the query returns only those NAT gateways that have all of the specified keys.

* The tag key must be unique.

**SubnetId ** string`optional` `Example: subnet-1t1apofp97****`

ID of the subnet where the NAT Gateway is located.

You can call the [DescribeSubnets](https://docs.byteplus.com/en/docs/vpc/DescribeSubnets) API to query the subnet ID.

**VpcId ** string`optional` `Example: vpc-p1b1p30ve5yze****`

The ID of the Virtual Private Cloud (VPC) where the NAT gateway resides.

You can call the [DescribeVpcs](https://docs.byteplus.com/en/docs/vpc/DescribeVpcs) API to query the VPC ID.

**NatGatewayName ** string`optional` `Example: nat-01`

The name of the NAT gateway.

**PageSize ** integer`optional` `Example: 20`

The number of entries per page in a pagination query. Value range: 1–100. Default: 20.

**PageNumber ** integer`optional` `Example: 1`

The page number of the list. Default: 1.

**Spec ** string`optional` `Example: Medium`

Specification of the NAT gateway.

* Small (default)

* Medium.

* Large.

**NetworkType ** string`optional` `Example: internet`

The type of the NAT gateway. Values:

* internet (default): Internet NAT Gateway.

* intranet: VPC NAT Gateway.

**ProjectName ** string`optional` `Example: Project_1`

The name of the project to which the NAT gateway belongs.

**NatGatewayIds.N ** string[]`optional` `Example: ngw-3tex2x1cwd4c6c0v****`

ID of the NAT gateway.

* N represents the serial number of the NAT gateway. You can call a maximum of 20 IDs in a single request.

* Separate multiple IDs with ampersands (&).

## Response parameters

The following only details response parameters specific to this API. For more information, see [Response structure](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response).

**PageNumber ** integer`Example: 1`

The current page number.

**NatGateways ** object[]`Example: -`

Details of the NAT gateway.

**NatGatewayName ** string`Example: nat-01`

Name of the NAT gateway.

**Description ** string`Example: This is a nat`

Description of the NAT gateway.

**EipAddresses ** object[]

The information about the EIP associated with the NAT gateway.

**AllocationId ** string`Example: eip-4v0x57pna7x****`

The ID of the elastic IP address (EIP).

**EipAddress ** string`Example: 121.XX.XX.52`

Address of the EIP.

**UsingStatus ** string`Example: Idle`

The usage status of the EIP.

* Idle: Not in use.

* UsedBySnat: Used by the SNAT rule.

* UsedByDnat: Used by the DNAT rule.

* UsedByNat: Used by both SNAT and DNAT rules.

**VpcId ** string`Example: vpc-yxa83n6nu****`

ID of the VPC to which the NAT gateway belongs.

**Spec ** string`Example: Medium`

The specification of the NAT gateway.

* Small (default)

* Medium

* Large

**BillingType ** integer`Example: 2`

The metering method of the NAT Gateway.

* 1: Subscription.

* 2: Pay\-by\-Specification

* 3: Pay\-by\-CU.

**NatGatewayId ** string`Example: ngw-3tex2x1cwd4c6c0v****`

ID of the NAT gateway

**ExpiredTime ** string`Example: 2021-05-07 23:59:59`

The time when the Subscription NAT gateway expires. This parameter returns a value only for Subscription NAT gateways.

**DeletedTime ** string`Example: 2021-12-21 18:26:27`

The time when the resource is scheduled to be forcibly reclaimed.

* This parameter returns a value for Subscription NAT gateways.

* For Pay\-as\-you\-go NAT gateways, this parameter returns a value only if arrears\-related freezing occurs.

**OverdueTime ** string`Example: 2021-12-06 18:26:27`

The time when the resource is frozen. This parameter returns a value only if the resource is frozen due to overdue payments.

**UpdatedAt ** string`Example: 2021-12-06T18:26:27+08:00`

The time when the NAT gateway is last operated.

**CreationTime ** string`Example: 2021-11-30T16:59:27+08:00`

The time when the NAT gateway is created.

**BusinessStatus ** string`Example: Normal`

Describe whether the NAT gateway is locked.

* Null: Normal and not locked.

* Normal: Normal and not locked.

* FinancialLocked: Being locked due to arrears.

**Status ** string`Example: Available`

Status of the NAT gateway.

* Available

* Creating

* Pending: Action in progress​.

* Deleting

**Tags ** object[]

Tag information of the NAT gateway.

**Key ** string`Example: k1`

The tag key.

**Value ** string`Example: v1`

The tag value.

**ProjectName ** string`Example: Project_1`

The name of the project to which the NAT gateway belongs.

**NetworkInterfaceId ** string`Example: eni-13fvhq3a7opv****`

ID of the network interface occupied by the NAT gateway.

**ZoneId ** string`Example: cn-beijing-a`

ID of the primary availability zone to which the NAT gateway belongs.

**SubnetId ** string`Example: subnet-kty2akgv0x5****`

ID of the subnet to which the NAT gateway belongs.

**LockReason ** string`Example: financial`

The cause that the NAT gateway is locked.

* financial: Being locked due to arrears.

* security: Being locked due to security.

**SnatEntryIds ** string[]`Example: ["snat-3fvhk47kf56****", "snat-3fvhk47kf78****"]`

List of SNAT rule IDs.

**NetworkType ** string`Example: internet`

The type of the NAT gateway.

* internet: Internet NAT Gateway.

* intranet: VPC NAT Gateway.

**DnatEntryIds ** string[]`Example: ["dnat-342abc3bc3****", "dnat-342abc3bd4****"]`

List of DNAT rule IDs.

**SmartScheduleEnabled ** boolean`Example: false`

Describe whether to enable smart scheduling

**SmartScheduleRule ** string`Example: ChinaMobile,ChinaTelecom,ChinaUnicom,BGP`

Smart scheduling policy

**DirectMode ** boolean

Direct or Non\-direct

**PageSize ** integer`Example: 20`

Number of entries per page in the current pagination.

**RequestId ** string`Example: 2021062415303301022514515207C4****`

Request ID.

**TotalCount ** integer`Example: 33`

Total number of NAT gateways that meet the conditions.

## Request examples

```text
GET /?Action=DescribeNatGateways&Version=2020-04-01&NatGatewayIds.1=ngw-2fesmko5zhdz459gp67sc****&PageNumber=1&PageSize=5 HTTP/1.1
Host: natgateway.cn-beijing.byteplusapi.com.cn
Service: natgateway
Region: cn-beijing
```

## Response examples

```json
{
    "ResponseMetadata": {
        "RequestId": "2021062415303301022514515207C4****",
        "Action": "DescribeNatGateways",
        "Version": "2020-04-01",
        "Service": "natgateway",
        "Region": "cn-beijing"
    },
    "Result": {
        "RequestId": "2021062415303301022514515207C4****",
        "TotalCount": 1,
        "PageNumber": 1,
        "PageSize": 5,
        "NatGateways": [
            {
                  "NetworkType": "internet",
                  "NatGatewayId": "ngw-2feq5xhimd88w59gp686****",
                  "NatGatewayName": "nat-01",
                  "Description": "This is a nat",            
                  "Spec": "Small",          
                  "BillingType": 2,
                  "EipAddresses": [
                      {
                          "AllocationId": "eip-2fejrf9qxlla859gp6850****",
                          "EipAddress": "180.XX.XX.79",
                          "UsingStatus": "UsedBySnat"
                       }
                   ],
                  "DirectMode":false,
                  "BandwidthLimit":10,            
                  "VpcId": "vpc-2feacqu7h3klc59gp67u3****",
                  "SubnetId": "subnet-2feacrhvug8ao59gp671b****",
                  "ZoneId": "cn-beijing-a",
                  "NetworkInterfaceId": "eni-2fesmkw23xlvk59gp67g9****",
                  "SnatEntryIds"[
                      "snat-3fvhk47kf56****",
                      "snat-3fvhk47kf78****"
                  ],  
                  "DnatEntryIds"[
                      "dnat-342abc3bc3****",
                      "dnat-342abc3bd4****"
                  ],           
                  "ProjectName": "Project_1",
                  "Tags":[
                      {
                            "Key":"k1",
                            "Value":"v1"
                      },
                      {
                            "Key":"k2",
                            "Value":""
                      }
                  ]
                  "Status": "Available",
                  "BusinessStatus": "FinancialLocked",
                  "LockReason": "financial",              
                  "CreationTime": "2021-11-30T16:59:27+08:00",
                  "UpdatedAt": "2021-12-06T18:26:27+08:00",
                  "ExpiredTime": "",
                  "OverdueTime": "2021-12-06 18:26:27",
                  "DeletedTime": "2021-12-21 18:26:27"
            }
        ]
    }
}
```

## Error codes

The table below describes the error codes for this API that are associated with business logic. For details, see [Common error codes](https://docs.byteplus.com/en/docs/natgateway/Public-error-codes).

|Status code |Error codes |Error message |Description |
|---|---|---|---|
|400 |InvalidTagFilterValue.Malformed |The specified parameter tag filter value is invalid. |The tag filter value is invalid. |
|400 |InvalidTagFilterKey.Malformed |The specified parameter tag filter key is invalid. |The tag filter key is invalid. |
|400 |LimitExceeded.TagFilterValue |You've reached the limit on the number of tag values that you can filter. |You have reached the maximum number of tag values that you can specify for filtering in a single request. |
|400 |LimitExceeded.TagFilterKey |You've reached the limit on the number of tag keys that you can filter. |You have reached the maximum number of tag keys that you can specify for filtering in a single request. |
|400 |LimitExceeded.NatGatewayId |You've reached the limit on the number of NAT gateway IDs that you can describe. |You have reached the maximum number of NAT gateway IDs that can be queried. |
|400 |InvalidPage.Malformed |The specified page is malformed. |The specified pagination parameter is invalid. |
|400 |InvalidTagFilter.Disorder |The specified index order of tag filter is malformed. |The index order format of the specified tag filter is invalid. |
|500 |InternalError |An internal error has occurred. |An internal error occurred. |
