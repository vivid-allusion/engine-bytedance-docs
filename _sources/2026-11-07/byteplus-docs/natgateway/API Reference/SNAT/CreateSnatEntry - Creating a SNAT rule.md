---
title: "CreateSnatEntry - Creating a SNAT rule"
product: "NAT Gateway"
product_code: "natgateway"
source: "https://docs.byteplus.com/en/docs/natgateway/CreateSnatEntry"
---

Call the CreateSnatEntry API to create a Source Network Address Translation (SNAT) rule.

<span id=".5L2_55So6K-05piO"></span>
## Instructions


* You can create a maximum of 40 SNAT rules for a single NAT gateway.

* You can associate a maximum of 20 elastic IP addresses (EIPs) with a single SNAT rule.

* If the default SNAT quota is insufficient, go to BytePlus Quota Center to increase the corresponding quota.


<span id=".5rOo5oSP5LqL6aG5"></span>
## Precautions


* The EIP used by the SNAT rule must be an EIP associated with the NAT gateway where the rule is configured. You can call [DescribeNatGateways](https://docs.byteplus.com/en/docs/natgateway/DescribeNatGateways) to query the EIP associated with the NAT gateway.

* If the NAT gateway of the SNAT rule does not have an EIP associated, you can call [AssociateEipAddress](https://docs.byteplus.com/en/docs/eip/AssociateEipAddress) to associate an EIP with the NAT gateway.

* If an Elastic Compute Service (ECS) instance having associated EIPs is configured with SNAT rules, the EIP will be preferred when accessing the internet.

* When multiple SNAT rules have overlapping scopes, the SNAT rule with the longer subnet mask has a higher priority.


<span id=".6LCD6K-V"></span>
## Debug

[去调试](https://api.byteplus.com/api-explorer/?action=CreateSnatEntry&groupName=SNAT%E8%A7%84%E5%88%99&serviceCode=natgateway&version=2020-04-01)


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters

The following only details request parameters specific to this API and key common parameters. For more information, see [Common parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).



**Action ** <span data-label="purple">string </span><span data-api-tag="require|NAUKpj">必选</span> `Example: CreateSnatEntry`

The action that you want to perform. Value: CreateSnatEntry.



**Version ** <span data-label="purple">string </span><span data-api-tag="require|43Akzq">必选</span> `Example: 2020-04-01`

The API version. Value: 2020\-04\-01.



**EipId ** <span data-label="purple">string </span>`optional` `Example: eip-2feaac9wtccn459gp67****`

The ID of the EIP associated with the Internet NAT gateway. Separate multiple EIP IDs with commas (,).

You can call [DescribeEipAddresses](https://docs.byteplus.com/en/docs/eip/DescribeEipAddressAttributes) to query the EIP ID.


* If a single EIP is specified, the SNAT rule will be associated with that IP. All business connections will then access the Internet through this specific IP address.

* If multiple EIPs are specified, the SNAT rule will be associated with all of them. Business connections are distributed across these IPs based on a hash of their five\-tuple​.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">This parameter is required when NatGatewayId is set to an Internet NAT gateway ID.</div>



* When a SNAT rule is associated with multiple EIPs, we recommend adding the EIPs to a Bandwidth Package to prevent any traffic packet loss caused by any one EIP reaching its bandwidth limit.​​



**SubnetId ** <span data-label="purple">string </span>`optional` `Example: subnet-2fe1vklp295a859gp6766****`

ID of the subnet associated with the SNAT rule.

You can call the [DescribeSubnets](https://docs.byteplus.com/en/docs/vpc/DescribeSubnets) API to query the subnet ID.

At least one of the two parameters (SubnetId and SourceCidr) must be provided.



**SnatEntryName ** <span data-label="purple">string </span>`optional` `Example: snat-01`

Name of the SNAT rule.


* Must start with a letter, Chinese character, or number. May include periods (.), underscores (_), and hyphens (\-).

* Must be 1 to 128 characters. If left blank, this parameter defaults to the SNAT rule ID.



**SourceCidr ** <span data-label="purple">string </span>`optional` `Example: 192.XX.XX.0/20`

Specify the CIDR block for the SNAT rule. Different granularities correspond to different CIDR blocks, as detailed below:


* VPC granularity: The CIDR block of the VPC where the NAT gateway resides. All ECS instances without an associated EIP in this VPC can access the internet via the SNAT rule.

* Subnet granularity: The CIDR block of a specified subnet (e.g., 192.XX.XX.0/24). All ECS instances without an associated EIP in the specified subnet can access the internet via the SNAT rule.

* ECS granularity: The IP address of the specified ECS instance (e.g., 192.XX.XX.20/32). The specified ECS instance without an associated EIP can access the internet via the SNAT rule.

* Custom CIDR granularity: Specify a custom CIDR block (e.g., 192.XX.XX.0/26). All ECS instances without an associated EIP within the specified custom CIDR block can access the internet via the SNAT rule.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">At least one of the two parameters (SubnetId and SourceCidr) must be provided. If SubnetId is provided, SourceCidr cannot be specified. While if SourceCidr is provided, SubnetId cannot be specified. The specified CIDR block cannot overlap with an existing SNAT rule's CIDR block.​</div>




**NatIpId ** <span data-label="purple">string </span>`optional` `Example: vpcnatip-gw8y7q3cpk3fggs8****`

The ID of the NAT IP address used by the VPC NAT gateway.

You can call the [DescribeNatIps](https://docs.byteplus.com/en/docs/natgateway/DescribeNatIps) API to query the NAT IP ID.

If left blank, this parameter defaults to the ID of the NAT IP.



**NatGatewayId ** <span data-label="purple">string </span><span data-api-tag="require|TR9wQF">必选</span> `Example: ngw-2fedgzyvtzaio59gp675****`

The ID of the NAT gateway to which the SNAT rule belongs.

You can call the [DescribeNatGateways](https://docs.byteplus.com/en/docs/natgateway/DescribeNatGateways) API to query the ID of a NAT gateway.



&nbsp;

<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters

The following only details response parameters specific to this API. For more information, see [Response structure](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response).



**RequestId ** <span data-label="purple">string </span>`Example: 2021062415303301022514515207C4****`

Request ID.



**SnatEntryId ** <span data-label="purple">string </span>`Example: snat-2fedhzdlyknb459gp676o****`

ID of the SNAT rule.



&nbsp;

<span id=".6K-35rGC56S65L6L"></span>
## Request examples

```text
GET /?Action=CreateSnatEntry&Version=2020-04-01&NatGatewayId=ngw-2fedgzyvtzaio59gp675****&SubnetId=subnet-2fe1vklp295a859gp6766****&EipId=eip-2feaac9wtccn459gp67****&SnatEntryName=snat-01 HTTP/1.1
Host: natgateway.cn-beijing.byteplusapi.com.cn
Service: natgateway
Region: cn-beijing
```


<span id=".6L-U5Zue56S65L6L"></span>
## Response examples

```json
{
    "ResponseMetadata": {
        "RequestId": "2021062415303301022514515207C4****",
        "Action": "CreateSnatEntry",
        "Version": "2020-04-01",
        "Service": "natgateway",
        "Region": "cn-beijing"
    },
    "Result":{
        "RequestId": "2021062415303301022514515207C4****",
        "SnatEntryId": "snat-2fedhzdlyknb459gp676o****"
    }
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error codes

The table below describes the error codes for this API that are associated with business logic. For details, see [Common error codes](https://docs.byteplus.com/en/docs/natgateway/Public-error-codes).


|Status code |Error codes |Error message |Description |
|---|---|---|---|
|400 |MissingParameter |The request is missing a required parameter. |This request does not contain required parameters. |
|400 |InvalidEip.InvalidStatus |The specified elastic ip is not in the correct status for the request. The specified elastic ip is in freeze. |The specified EIP or VPC cannot respond to this request due to its status. The current EIP is frozen. |
|400 |InvalidParameter.SourceCidrConflict |The specified source cidr and subnet conflict. |The specified CIDR block conflicts with the subnet parameter. |
|400 |QuotaExceeded.SnatEntry |SNAT entries number of the NAT gateway exceeded quota. |You have reached the maximum number of SNAT rules that you can create in a single NAT gateway. |
|400 |LimitExceeded.EipsPerSnatEntry |You've reached the limit on the number of EIPs per snat entry. |You have reached the maximum number of EIPs that can be associated per SNAT rule. |
|400 |InvalidSourceCidr.Malformed |The specified source cidr is malformed. |The format of the specified CIDR block is invalid. |
|400 |InvalidSnatEntry.VpcMismatch |The specified subnet is not in the NAT gateway's VPC. |The specified subnet is not within the NAT gateway's VPC. |
|400 |InvalidSnatEntry.Conflict |The specified source cidr or subnet conflicts with that of a SNAT entry in your NAT gateway. |The specified CIDR block or subnet CIDR conflicts with an associated SNAT rule. |
|400 |InvalidNatGateway.InvalidStatus |The specified NAT gateway is not in the correct status for the request. |The specified NAT gateway cannot respond to this request due to its status. |
|400 |InvalidEip.InstanceMismatch |The specified elastic ip and instance mismatch. |The specified EIP does not match the instance. |
|400 |InvalidSnatEntry.EipNotSupported |Can not create or modify SNAT entry with eip on the specified NAT gateway. |You cannot create or modify a SNAT rule that uses an EIP in the specified NAT gateway. |
|400 |InvalidSnatEntry.NatIpConflict |The specified nat ip and eip conflict. |The specified NAT IP conflicts with the EIP parameter. |
|400 |InvalidSnatEntry.NatIpNotSupported |Can not create or modify SNAT entry with nat ip on the specified NAT gateway. |You cannot create or modify a SNAT rule that uses a NAT IP in the specified NAT gateway. |
|400 |InvalidEip.InUse |The specified eip has been used by dnat entry of ip mapping. |The specified EIP is already used by a DNAT rule for IP mapping. |
|400 |InvalidName.Malformed |The specified name is malformed. |The format of the specified name is invalid. Correct the name format and retry. |
|400 |InvalidName.Malformed |The specified name is malformed.Ensure the maximum length of name is 128. |The format of specified name is invalid. A name must not exceed 128 characters in length. |
|404 |InvalidProject.NotFound |The specified Project does not exist. |The specified project does not exist. |
|404 |InvalidSubnet.NotFound |The specified subnet does not exist. |The specified subnet does not exist. |
|404 |InvalidNatGateway.NotFound |The specified NAT gateway does not exist. |The specified NAT gateway does not exist. |
|404 |InvalidEip.NotFound |The specified EIP does not exist. |The specified EIP does not exist. |
|404 |InvalidNatIp.NotFound |The specified nat ip does not exist. |The specified NAT IP does not exist. |
|409 |InvalidSnatEntry.EipConflict |The specified EIP conflicts with that of another EIP in the snat entry. |The EIP in the SNAT rule conflicted. |
|412 |InvalidNatGateway.Expired |The specified NAT gateway has expired. |The specified NAT gateway is expired. |
|500 |InternalError |An internal error has occurred. |An internal error occurred. |
