---
title: "DeleteSubnet - Deleting a subnet"
product: "Virtual Private Cloud"
product_code: "vpc"
source: "https://docs.byteplus.com/en/docs/vpc/DeleteSubnet"
---

Call the DeleteSubnet API to delete the specified subnet.

## Instructions

|Prerequisites |Description |
|---|---|
|No ENI in the subnet |You can call the [DescribeNetworkInterfaces](https://docs.byteplus.com/en/docs/vpc/DescribeNetworkInterfaces) API to check if ENIs exist. If any exist, you can call the [DeleteNetworkInterface](https://docs.byteplus.com/en/docs/vpc/DeleteNetworkInterface) API to delete the ENIs. |
|The subnet is not associated with any SNAT entry |You can call the [DescribeSnatEntries](https://docs.byteplus.com/en/docs/natgateway/DescribeSnatEntries) API to check if the SNAT entry is associated. If associated, you can call the [DeleteSnatEntry](https://docs.byteplus.com/en/docs/natgateway/DeleteSnatEntry) API to delete the SNAT rule. |
|No HaVip in subnet |You can call the [DescribeHaVips](https://docs.byteplus.com/en/docs/vpc/DescribeHaVips) API to check if a High\-Availability Virtual IP Address (HaVip) exists. If any exist, you can call the [DeleteHaVip](https://docs.byteplus.com/en/docs/vpc/DeleteHaVip) API to delete the HaVip. |
|Subnet is not associated with a Network ACL |You can call the [DescribeSubnets](https://docs.byteplus.com/en/docs/vpc/DescribeSubnets) API to check if the Network ACL is associated. If any exist, you can call the [DisassociateNetworkAcl](https://docs.byteplus.com/en/docs/vpc/DisassociateNetworkAcl) API to disassociate it from the Network ACL. |

DeleteSubnet is an asynchronous API. When a request ID is returned, the system is still deleting in the background. You can call [DescribeSubnetAttributes](https://docs.byteplus.com/en/docs/vpc/DescribeSubnetAttributes) API to check the subnet status. Pending means deleting, and a failed query indicates deletion is complete.

## Debug

[去调试](https://api.byteplus.com/api-explorer/debug?action=DeleteSubnet&serviceCode=vpc&version=2020-04-01&groupName=)

## Request parameters

The table below lists only the request parameters unique to this interface and some common parameters. For more information, see [Common parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).

**Action ** String必选 `Example: DeleteSubnet`

Interface name. The current API name is `DeleteSubnet`.

**Version ** String必选 `Example: 2020-04-01`

Interface version. The current API version is `2020-04-01`.

**SubnetId ** String必选 `Example: subnet-bp15zckdt37pq72zv****`

ID of the subnet to be deleted.

You can call the [DescribeSubnets](https://docs.byteplus.com/en/docs/vpc/DescribeSubnets) API to query the subnet ID.

## Response parameters

Only the response parameters specific to this API are listed below. For more information, see [Response structure](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response).

**RequestId ** String`Example: 2021062415303301022514515207C4****`

The request ID.

## Request example

```json
GET /?Action=DeleteSubnet&Version=2020-04-01&SubnetId=subnet-bp15zdt37pq72zv**** HTTP/1.1
Host: vpc.cn-beijing.byteplusapi.com.cn
X-Date: 20251121T094038Z
Authorization: HMAC-SHA256 Credential=Adfks******wekfwe/20251121/cn-beijing/vpc/request, SignedHeaders=host;x-date, Signature=47a7d934ff7b37c03938******cd7b8278a40a1057690c401e92246a0e41085f
```

## Response example

```json
{
    "ResponseMetadata": {
        "RequestId": "20230604110420****100232280022D31",
        "Action": "DeleteSubnet",
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
|400 |DryRunOperation |Exception raised to indicate a successfully authorized action when the DryRun flag is set to true. |This request is set to DryRun action. The action has been authorized but has not been executed. |
|400 |IdempotentParameterMismatch |Arguments on this idempotent request are inconsistent with arguments used in previous request(s). |The parameters of this idempotent request are inconsistent with those used in the previous request. |
|400 |InvalidCen.InvalidStatus |The CEN that the specified VPC attached to is not in the correct status for the request. |The CEN instance associated with the VPC is in a state that cannot process the request. Please try again later. |
|400 |InvalidFlowLog.InvalidStatus |The specified flow log is not in the correct status for the request. |The specified flow log is in a status that cannot respond to this request. |
|400 |InvalidParameter.ClientTokenMalformed |The specified parameter ClientToken is malformed. |The format of specified ClientToken is invalid. It must not exceed 64 ASCII characters. |
|400 |InvalidSubnet.InUse |The specified subnet has dependent resource of an HaVip. |The specified subnet contains a HaVip and cannot be deleted. |
|400 |InvalidSubnet.InUse |The specified subnet has dependent resource of an SNAT entry. |The specified subnet contains SNAT rules and cannot be deleted. |
|400 |InvalidSubnet.InUse |The specified subnet has dependent resource of an elastic network interface. |The specified subnet contains Network Interfaces (ENIs) and cannot be deleted. |
|400 |InvalidSubnet.InUse |The specified subnet is associated with Network ACL. |The specified subnet is associated with a Network Access Control List and cannot be deleted. |
|400 |InvalidSubnet.InUse |The specified subnet is in use. The subnet in the resource sharing cannot be deleted. |The specified subnet is currently in use. Subnets involved in Resource Sharing cannot be deleted. |
|400 |InvalidSubnet.InvalidStatus |The specified subnet is not in the correct status for the request. |The specified subnet is in a state that cannot process this request. |
|400 |InvalidVpc.InvalidStatus |The specified VPC is not in the correct status for the request. |The specified VPC is in a state that cannot respond to this request. |
|400 |QuotaExceeded.SystemRouteEntry |You've reached the limit on the number of system route entries per route table. |The maximum number of system routes that you can create has been reached. |
|404 |InvalidFlowLog.NotFound |The specified flow log does not exist. |The specified flow log does not exist. |
|404 |InvalidSubnet.NotFound |The specified subnet does not exist. |The specified subnet does not exist. |
|404 |InvalidVpc.NotFound |The specified VPC does not exist. |The specified VPC does not exist. |
|409 |InvalidRouteCidr.Conflict |The specified CIDR block conflicts with that of another route in your route table. |The specified CIDR block conflicts with another rule's CIDR block in the same route table. |
|412 |IdempotentProcessing |The request uses the same client token as a previous one that is still in process. |The idempotent request is in process. |
