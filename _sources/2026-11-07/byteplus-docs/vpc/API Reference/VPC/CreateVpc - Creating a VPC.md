---
title: "CreateVpc - Creating a VPC"
product: "Virtual Private Cloud"
product_code: "vpc"
source: "https://docs.byteplus.com/en/docs/vpc/CreateVpc"
---

Call the CreateVpc API to create a VPC.

> **tip**

> IPv6 is currently in the invite\-only Beta stage and temporarily only supports accounts that have completed [Enterprise certification](https://docs.byteplus.com/en/docs/6261/64937) to apply for trial. If you need a trial, please contact your account manager.

## Instructions

* A single account can create up to 10 VPCs per region by default. If the default quota cannot meet your needs, go to the [Quota Center](https://console.byteplus.com/quota/productList/coParameterList?ProviderCode=VPC) to increase the corresponding quota.

* CreateVpc is an asynchronous API. When a request ID is returned, the system is still creating the VPC in the background. You can call [DescribeVpcAttributes](https://docs.byteplus.com/en/docs/vpc/DescribeVpcAttributes) to check the VPC status. `Creating` means being created, and `Available` means creation is complete.

## Debug

[去调试](https://api.byteplus.com/api-explorer/debug?action=CreateVpc&serviceCode=vpc&version=2020-04-01&groupName=)

## Request parameters

The table below lists only the request parameters unique to this API and some common parameters. For more information, see [Common parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).

**Action ** String必选 `Example: CreateVpc`

The API name. The current API name is `CreateVpc`.

**Version ** String必选 `Example: 2020-04-01`

API version. The current API version is `2020-04-01`.

**VpcName ** String`optional` `Example: vpc-1`

Name of the VPC.

* Must be 1 to 128 characters.

* Must start with a letter, Chinese character, or number. May include periods (.), underscores (_), and hyphens (\-).

* If left blank, it defaults to the VPC instance ID.

* Cannot start with `http://` or `https://`.

**Description ** String`optional` `Example: This is my first Vpc`

Description of the VPC.

* Length limit: 0 to 255 characters.

* If left blank, it defaults to an empty string.

* Must start with a letter, Chinese character, or number. It may include half\-width commas (,), periods (.), underscores (_), spaces ( ), equal signs (=), hyphens (\-), full\-width commas (，), and full\-width periods (。).

* Cannot start with `http://` or `https://`.

**CidrBlock ** String必选 `Example: 172.XX.XX.0/12`

IPv4 CIDR block of the VPC. You may use the following CIDR blocks (or their subsets) as the IPv4 CIDR block for your VPC:

* 192.168.0.0/16 ~ 28

* 10.0.0.0/8 ~ 28

* 172.16.0.0/12 ~ 28

**EnableIpv6 ** Boolean`optional` `Example: true`

Enable the IPv6 CIDR block.

Please input the enumerated values strictly in case as follows, and do not pass in other values.

* **false** (default): Disable.

* **true**: Enable.

**Ipv6Isp ** String`optional` `Example: ChinaMobile`

ISP. Valid values:

* BGP (default): BGP (Multi\-ISP).

* ChinaMobile: China Mobile static single\-ISP.

* ChinaTelecom: China Telecom static single\-ISP.

* ChinaUnicom: China Unicom static single\-ISP.

* ChinaMobile_Value: The static preferential single\-ISP provided by China Mobile.

* ChinaUnicom_Value: The static preferential single\-ISP provided by China Unicom.

* ChinaTelecom_Value: The static preferential single\-ISP provided by China Telecom.

> **tip**

> Except for BGP (Multi\-ISP), all other line types are only supported in the China (Shanghai) region.

**Ipv6MaskLen** Integer `optional` `Example: 62`

Mask length of the IPv6 CIDR block.

* When Ipv6Isp is set to BGP, only a prefix length of /56 is supported. Otherwise, this parameter supports /62 to /64.

* After the parameter Ipv6CidrBlock is provided, this parameter does not take effect.

* If Ipv6Isp is set to a value other than BGP, then one of the parameters Ipv6MaskLen or Ipv6CidrBlock must be provided.

**Ipv6CidrBlock ** String`optional` `Example: 2408:XXXX:0:a600::/56`

IPv6 CIDR block of the VPC.

* When this parameter is provided, the Ipv6MaskLen parameter does not take effect.

* If Ipv6Isp is set to a value other than BGP, then one of the parameters Ipv6MaskLen or Ipv6CidrBlock must be provided.

* If the Ipv6Isp parameter is not provided or is set to BGP, and this parameter is not provided, the system will automatically assign an IPv6 CIDR block.

**DnsServers.N ** String`optional` `Example: 12.XX.XX.5`

DNS server address of the VPC.

* N represents the serial number of a DNS server address. A maximum of 5 addresses can be specified per single API call. Each DnsServer must be provided as a valid IP address.

* Separate multiple IP addresses with ampersands (&).

* If left blank, it will be configured to use the default DNS server addresses.

**ProjectName ** String`optional` `Example: default`

Name of the project to which the VPC belongs. If left blank, it defaults to the default project.

**Tags.N.Key ** String`optional` `Example: key1`

The tag key of the custom tag.

* N represents the serial number of the tag key. Valid values: 1–50.

* Separate multiple tag keys with ampersands ( & ).

* It cannot start with `volc:` or `sys:` in any case form.

* Must be 1 to 128 characters. May include characters in different languages, numbers, spaces ( ), underscores (_), periods (.), half\-width colons (:), slashes (/), equal signs (=), plus signs (+), hyphens (\-), and at signs (@).

* If a tag key contains leading or trailing spaces, the system will automatically delete them.

> **tip**

> Duplicate tag keys are not allowed for the same resource.

**Tags.N.Value** String `optional` `Example: value1`

The tag value of the custom tag.

* N specifies the serial number of the tag value. Valid range: 1–50.

* Separate multiple tag values with ampersands (&).

* The value can be 0 to 256 characters in length. If left blank, the parameter defaults to an empty value.

* May include characters from various languages, digits, spaces ( ), underscores (_), periods (.), colons (:), slashes (/), equal signs (=), plus signs (+), hyphens (\-), and at signs (@).

* Case\-sensitive.

* If a tag value starts or ends with a space, the system will automatically delete them.

> **tip**

> If this parameter is passed in, `Tags.N.Key` must be passed in first.

**ClientToken ** String`optional` `Example: 123e4567-e89b-12d3-a456-42665544****`

Client token: Used to ensure request idempotency.

* You can use the client to automatically generate a token, but you must make sure that the token is unique among different requests. This prevents repeated actions due to multiple client retries when the call of the API action times out or an internal server error occurs.

* Must not exceed 64 ASCII characters.

* If no ClientToken passed in, the API call does not verify idempotency.

**DryRun ** Boolean`optional` `Example: false`

Whether to only precheck the request. Values:

* **true**: Sends a check request without creating the VPC. Checks include: Whether required parameters are entered, request format, and service limits. If the check fails, the corresponding error is returned. If the check passes, the error code DryRunOperation is returned.

* **false** (default): Sends a normal request. After passing the check, an HTTP 2xx status code is returned and the VPC is created directly.

## Response parameters

Only the response parameters specific to this API are listed below. For more information, see [Response structure](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response).

**VpcId ** String`Example: vpc-bp15zkdt37pq72zv****`

ID of the newly created VPC.

**RouteTableId ** String`Example: vtb-bp145q7glnuzdv****`

The ID of the route table automatically created by the system after VPC creation (i.e., the system route table ID).

**RequestId ** String`Example: 2021062415303301022514515207C4****`

Request ID.

## Request example

```json
GET /?Action=CreateVpc&Version=2020-04-01&CidrBlock=172.XX.XX.0/12&VpcName=vpc-1 HTTP/1.1
Host: vpc.cn-beijing.byteplusapi.com.cn
X-Date: 20251121T094038Z
Authorization: HMAC-SHA256 Credential=Adfks******wekfwe/20251121/cn-beijing/vpc/request, SignedHeaders=host;x-date, Signature=47a7d934ff7b37c03938******cd7b8278a40a1057690c401e92246a0e41085f
```

## Response example

```json
{
    "ResponseMetadata": {
        "RequestId": "20230604110420****100232280022D31",
        "Action": "CreateVpc",
        "Version": "2020-04-01",
        "Service": "vpc",
        "Region": "cn-beijing"
    },
    "Result": {
        "RequestId": "2021062415303301022514515207C4****",
        "RouteTableId": "vtb-bp145q7glnuzdv****",
        "VpcId": "vpc-bp15zkdt37pq72zv****"
    }
}
```

## Error codes

|Status code |Error codes |Error message |Description |
|---|---|---|---|
|400 |DryRunOperation |Exception raised to indicate a successfully authorized action when the DryRun flag is set to true. |This request is set to DryRun action. The action has been authorized but has not been executed. |
|400 |IdempotentParameterMismatch |Arguments on this idempotent request are inconsistent with arguments used in previous request(s). |The parameters of this idempotent request are inconsistent with those used in the previous request. |
|400 |InsufficientIpv6Blocks |The specified pool does not contain enough free IPv6 blocks to fulfill your request. |The IPv6 pool has insufficient IPv6 address range resources. |
|400 |InvalidCidr.Malformed |The specified cidr block is malformed. |The format of the specified CIDR block is invalid. |
|400 |InvalidDescription.Malformed |The specified description is malformed. |The specified description format is invalid. Correct the description format and retry. |
|400 |InvalidDescription.Malformed |The specified description is malformed. Ensure the maximum length of description is 255. |The specified description format is invalid. The description cannot exceed 255 characters. |
|400 |InvalidIpamPoolCidrAllocation.Malformed |The specified CIDR in the IPAM pool is unavailable. |The specified IPAM pool cannot allocate CIDR blocks. |
|400 |InvalidIpv6CidrBlock.NotReserved |The specified IPv6 CIDR block is not reserved. |The specified IPv6 address range is not reserved. |
|400 |InvalidName.Malformed |The specified name is malformed. |The specified name format is invalid. Correct the name format and retry. |
|400 |InvalidName.Malformed |The specified name is malformed. Ensure the maximum length of name is 128. |The specified name format is invalid. A name must not exceed 128 characters. |
|400 |InvalidParameter.ClientTokenMalformed |The specified parameter ClientToken is malformed. |The specified ClientToken format is invalid. It cannot exceed 64 ASCII characters. |
|400 |InvalidParameter.EnableIpv6 |The EnableIpv6 parameter is currently not supported. |The EnableIpv6 request parameter is not currently supported. |
|400 |InvalidParameter.MaskLength |The IPv6 mask length in this request is invalid. |The IPv6 mask length in this request is invalid. |
|400 |InvalidTag.Disorder |The specified index order of tag is malformed. |The index order format of the specified tag is invalid. |
|400 |InvalidTagKey.Malformed |The specified parameter tag key is invalid. |The specified tag key is invalid. |
|400 |InvalidTagValue.Malformed |The specified parameter tag value is invalid. |The specified tag value is invalid. |
|400 |InvalidVpcDnsServerIpAddress.Malformed |The specified DNS server IP address is malformed. |The specified DNS server IP address format is invalid. |
|400 |LimitExceeded.Tags |You've reached the limit on the number of tags that you can operate at one time. |The maximum tags that you can operate in a single request have been reached. |
|400 |LimitExceeded.VpcDnsServerNumber |You've reached the limit on the number of DNS servers that you can add. |Reached the maximum DNS servers that you can add. |
|400 |QuotaExceeded.RouteTable |Route table number exceeded quota. |Reached the maximum route tables that you can create. |
|400 |QuotaExceeded.SecurityGroup |Security group number exceeded quota. |The maximum number of security groups that can be created has been reached. |
|400 |QuotaExceeded.Vpc |VPC number exceeded quota. |Reached the maximum VPCs that you can create. |
|403 |Forbidden.IpamPoolAllocationResourceDiscovery |The IPAM pool owner cannot discover resources from the specified account. |The IPAM pool owner cannot discover resources of the specified account. |
|403 |Forbidden.Ipv6IspType |You are not authorized to create this type IPv6 CIDR. |You do not have permission to create an IPv6 CIDR block for the specified ISP. |
|404 |InvalidProject.NotFound |The specified Project does not exist. |The specified project does not exist. |
|412 |IdempotentProcessing |The request uses the same client token as a previous one that is still in process. |The idempotent request is in process. |
