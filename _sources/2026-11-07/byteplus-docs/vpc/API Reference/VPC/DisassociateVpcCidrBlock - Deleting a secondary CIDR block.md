---
title: "DisassociateVpcCidrBlock - Deleting a secondary CIDR block"
product: "Virtual Private Cloud"
product_code: "vpc"
source: "https://docs.byteplus.com/en/docs/vpc/DisassociateVpcCidrBlock"
---

Call the DisassociateVpcCidrBlock API to delete the specified secondary CIDR block from the specified VPC.

## Instructions

* No subnets created using the secondary CIDR. You can call the [DescribeSubnets](https://docs.byteplus.com/en/docs/vpc/DescribeSubnets) API check for existing subnets. If so, you can delete them by calling the [DeleteSubnet](https://docs.byteplus.com/en/docs/vpc/DeleteSubnet) API.

* DisassociateVpcCidrBlock is an asynchronous API. When a request ID is returned, the system is still configuring in the background. You can call [DescribeVpcAttributes](https://docs.byteplus.com/en/docs/vpc/DescribeVpcAttributes) API to check the VPC status. `Pending` means configuring, and `Available` means configuration is completed.

## Debug

[去调试](https://api.byteplus.com/api-explorer/debug?action=DisassociateVpcCidrBlock&serviceCode=vpc&version=2020-04-01&groupName=)

## Request parameters

The following only details request parameters specific to this API and key common parameters. More information can be found in [Common parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).

**Action ** String必选 `Example: DisassociateVpcCidrBlock`

The interface name. The current API name is `DisassociateVpcCidrBlock`.

**Version ** String必选 `Example: 2020-04-01`

The interface version. the current API version is `2020-04-01`.

**VpcId ** String必选 `Example: vpc-257gqcdfvx6n****`

VPC ID.

You can call the [DescribeVpcs](https://docs.byteplus.com/en/docs/vpc/DescribeVpcs) API to query the VPC ID.

**SecondaryCidrBlock ** String`optional` `Example: 172.16.XX.0/24`

The secondary IPv4 CIDR block of the VPC to be deleted.

**Ipv6CidrBlock ** String`optional` `Example: 2408:XXXX:0:a600::/56`

The secondary IPv6 CIDR block of the VPC to be deleted.

> **tip**

> IPv6 is currently in Beta stage and temporarily only supports accounts that have completed [Enterprise certification](https://docs.byteplus.com/en/docs/6261/64937) to apply for trial. If you need a trial, please contact your account manager.

## Response parameters

Only the response parameters specific to this API are listed below. More information, see [Response structure](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response).

**RequestId ** String`Example: 2021062415303301022514515207C4****`

Request ID.

## Request examples

```json
GET /?Action=DisassociateVpcCidrBlock&Version=2020-04-01&VpcId=vpc-257gqcdfvx6n****&SecondaryCidrBlock=172.16.XX.0/24 HTTP/1.1
Host: vpc.cn-beijing.byteplusapi.com.cn
X-Date: 20251121T094038Z
Authorization: HMAC-SHA256 Credential=Adfks******wekfwe/20251121/cn-beijing/vpc/request, SignedHeaders=host;x-date, Signature=47a7d934ff7b37c03938******cd7b8278a40a1057690c401e92246a0e41085f
```

## Response examples

```json
{
    "ResponseMetadata": {
        "RequestId": "20230604110420****100232280022D31",
        "Action": "DisassociateVpcCidrBlock",
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

|Status code |Error codes |Error message |Notes |
|---|---|---|---|
|400 |DryRunOperation |Exception raised to indicate a successfully authorized action when the DryRun flag is set to true. |This request is set to DryRun. The action is authorized but not executed. |
|400 |InvalidCidr.Malformed |The specified cidr block is malformed. |The format of the specified CIDR block is invalid. |
|400 |InvalidIPv6CidrBlock.InUse |The specified IPv6 CIDR block is in use. |The specified IPv6 CIDR block is currently in use. |
|400 |InvalidIPv6CidrBlock.NotFound |The specified IPv6 CIDR block is not found in your VPC. |The specified IPv6 CIDR block does not exist in the specified VPC. |
|400 |InvalidParameter.SecondaryCidrAndIpv6Cidr |The param of request are mutually exclusive. |The request contains mutually exclusive parameters. |
|400 |InvalidSecondaryCidrBlock.InUse |The specified secondary CIDR block is in use. |The specified secondary CIDR block is currently in use. |
|400 |InvalidSecondaryCidrBlock.NotFound |The specified secondary CIDR block is not found. |The specified secondary CIDR block does not exist in the specified VPC. |
|400 |InvalidVpc.InvalidStatus |The specified VPC is not in the correct status for the request. |The specified VPC is in a state that cannot respond to this request. |
|400 |QuotaExceeded.VpcIpv6Cidr |You've reached the limit on the number of IPv6 CIDR blocks per VPC that you can create. |The maximum number of IPv6 CIDR blocks allowed for the specified VPC has been reached. |
|400 |QuotaExceeded.VpcSecondaryCidr |You've reached the limit on the number of secondary cidr blocks per VPC. |The maximum number of secondary CIDR blocks allowed for the VPC has been reached. |
|404 |InvalidVpc.NotFound |The specified VPC does not exist. |The specified Virtual Private Cloud (VPC) does not exist. |
