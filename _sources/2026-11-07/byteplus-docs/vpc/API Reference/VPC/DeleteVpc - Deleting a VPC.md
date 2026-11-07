---
title: "DeleteVpc - Deleting a VPC"
product: "Virtual Private Cloud"
product_code: "vpc"
source: "https://docs.byteplus.com/en/docs/vpc/DeleteVpc"
---

Call the DeleteVpc API to delete the specified Virtual Private Cloud (VPC).

## Instructions

|Prerequisites |Description |
|---|---|
|No subnets exist within the VPC |You can call the [DescribeVpcs](https://docs.byteplus.com/en/docs/vpc/DescribeVpcs) API to check for any subnets. If any exist, you can delete them by calling the [DeleteSubnet](https://docs.byteplus.com/en/docs/vpc/DeleteSubnet) API. |
|No network ACL exists within the VPC |You can call the [DescribeVpcs](https://docs.byteplus.com/en/docs/vpc/DescribeVpcs) API to check for any network ACLs. If any exist, you can delete ACLs by calling the [DeleteNetworkAcl](https://docs.byteplus.com/en/docs/vpc/DeleteNetworkAcl) API. |
|No custom route tables exist within the VPC |You can call the [DescribeVpcs](https://docs.byteplus.com/en/docs/vpc/DescribeVpcs) API to check for any custom route tables. If any exist, you can delete them by calling the [DeleteRouteTable](https://docs.byteplus.com/en/docs/vpc/DeleteRouteTable) API. |
|No custom security groups exist within the VPC |You can call the [DescribeVpcs](https://docs.byteplus.com/en/docs/vpc/DescribeVpcs) API to check for any custom security groups. If any exist, you can delete them by calling the [DeleteSecurityGroup](https://docs.byteplus.com/en/docs/vpc/DeleteSecurityGroup) API. |
|No IPv6 gateway is associated with the VPC |You can call the [DescribeIpv6Gateways](https://docs.byteplus.com/en/docs/IPv6/DescribeIpv6Gateways) API to check if an IPv6 gateway is associated. If present, you can call the [DeleteIpv6Gateway](https://docs.byteplus.com/en/docs/IPv6/DeleteIpv6Gateway) API to delete the IPv6 gateway. |
|VPC is not authorized to other accounts |You can call the [DescribeGrantRulesToCen](https://docs.byteplus.com/en/docs/cen/DescribeGrantRulesToCen) API to check if it is authorized to other accounts. If any exist, you can revoke the authorization by calling the [RevokeInstanceFromCen](https://docs.byteplus.com/en/docs/cen/RevokeInstanceFromCen) API. |

DeleteVpc is an asynchronous API. When a request ID is returned, the system is still deleting the VPC in the background. You can call [DescribeVpcAttributes](https://docs.byteplus.com/en/docs/vpc/DescribeVpcAttributes) to check the status of a VPC. `Pending` indicates it is being deleted, and a failed query indicates deletion is complete.

## Debug

[去调试](https://api.byteplus.com/api-explorer/debug?action=DeleteVpc&serviceCode=vpc&version=2020-04-01&groupName=)

## Request parameters

The table below lists only the request parameters unique to this interface and some common parameters. For more information, see [Common parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).

**Action ** String必选 `Example: DeleteVpc`

Interface name. The current API name is `DeleteVpc`.

**Version ** String必选 `Example: 2020-04-01`

The interface version. The current API version is `2020-04-01`.

**VpcId ** String必选 `Example: 2ff3ruwe8fbb6****`

The ID of the VPC to be deleted.

You can call the [DescribeVpcs](https://docs.byteplus.com/en/docs/vpc/DescribeVpcs) API to query the VPC ID.

## Response parameters

Only the response parameters specific to this API are listed below. For more information, see [Response structure](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response).

**RequestId ** String`Example: 2021062415303301022514515207C4****`

Request ID.

## Request example

```json
GET /?Action=DeleteVpc&Version=2020-04-01&VpcId=vpc-2ff3ruwe8fbb6**** HTTP/1.1
Host: vpc.cn-beijing.byteplusapi.com.cn
X-Date: 20251121T094038Z
Authorization: HMAC-SHA256 Credential=Adfks******wekfwe/20251121/cn-beijing/vpc/request, SignedHeaders=host;x-date, Signature=47a7d934ff7b37c03938******cd7b8278a40a1057690c401e92246a0e41085f
```

## Response example

```json
{
    "ResponseMetadata": {
        "RequestId": "2021062415303301022514515207C4****",
        "Action": "DeleteVpc",
        "Version": "2020-04-01",
        "Service": "vpc",
        "Region": "cn-beijing"
    },
    "Result": {
        "RequestId": "2021062415303301022514515207C4****"
    }
}
```

## Error codes

|Status code |Error codes |Error message |Description |
|---|---|---|---|
|400 |DependencyViolation.CenAttached |Specified VPC is attached to a CEN instance |This VPC is included in a CEN. Please disassociate it from the CEN before attempting deletion. |
|400 |DryRunOperation |Exception raised to indicate a successfully authorized action when the DryRun flag is set to true. |This request is set to DryRun. The action is authorized but not executed. |
|400 |InvalidClassicVpc.InUse |The specified classic VPC cannot be deleted. |The specified classic VPC cannot be deleted. |
|400 |InvalidFlowLog.InvalidStatus |The specified flow log is not in the correct status for the request. |The specified flow log is in a state that cannot respond to this request. |
|400 |InvalidRouteTable.InUse |The specified route table has dependent resource of a route entry. |The specified route table contains route entries and cannot be deleted. |
|400 |InvalidSecurityGroup.InvalidStatus |The specified security group is not in the correct status for the request. |The specified security group is in a state that cannot respond to this request. |
|400 |InvalidVpc.HasInstanceGroup |The specified VPC has dependent resource of an instance group. |The specified VPC contains server groups and cannot be deleted. |
|400 |InvalidVpc.HasIpv4Gateway |The specified VPC has dependent resource of an ipv4 gateway. |The specified VPC contains an IPv4 gateway and cannot be deleted. |
|400 |InvalidVpc.InUse |The specified VPC contains Network ACL not been deleted. |Network ACLs exist within the specified VPC, and it cannot be deleted. |
|400 |InvalidVpc.InUse |The specified VPC has dependent resource of a Cloud Enterprise Network. |The specified VPC has been added to a Cloud Enterprise Network (CEN) and cannot be deleted. |
|400 |InvalidVpc.InUse |The specified VPC has dependent resource of a Core Network. |The specified VPC contains a NAT gateway and cannot be deleted. |
|400 |InvalidVpc.InUse |The specified VPC has dependent resource of a NAT gateway. |The specified VPC has been added to a transit router and cannot be deleted. |
|400 |InvalidVpc.InUse |The specified VPC has dependent resource of a Transit Router. |The specified VPC contains a VPN gateway and cannot be deleted. |
|400 |InvalidVpc.InUse |The specified VPC has dependent resource of a VPN gateway. |The specified VPC contains route tables and cannot be deleted. |
|400 |InvalidVpc.InUse |The specified VPC has dependent resource of a direct connect gateway. |The specified VPC contains security groups and cannot be deleted. |
|400 |InvalidVpc.InUse |The specified VPC has dependent resource of a peering connection. |The specified VPC contains subnets and cannot be deleted. |
|400 |InvalidVpc.InUse |The specified VPC has dependent resource of a route table. |The specified VPC contains an IPv6 gateway and cannot be deleted. |
|400 |InvalidVpc.InUse |The specified VPC has dependent resource of a security group. |The specified VPC contains security groups and cannot be deleted. |
|400 |InvalidVpc.InUse |The specified VPC has dependent resource of a subnet. |The specified VPC contains subnets and cannot be deleted. |
|400 |InvalidVpc.InUse |The specified VPC has dependent resource of an Ipv6Gateway. |The specified VPC contains an IPv6 gateway and cannot be deleted. |
|400 |InvalidVpc.InvalidStatus |The specified VPC is not in the correct status for the request. |The specified VPC is in a state that cannot respond to this request. |
|404 |InvalidFlowLog.NotFound |The specified flow log does not exist. |The specified flow log does not exist. |
|404 |InvalidVpc.NotFound |The specified VPC does not exist. |The specified VPC does not exist. |
