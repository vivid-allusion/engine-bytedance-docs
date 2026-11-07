---
title: "CreateSubnet - Creating a subnet"
product: "Virtual Private Cloud"
product_code: "vpc"
source: "https://docs.byteplus.com/en/docs/vpc/CreateSubnet"
---

Call the CreateSubnet API to create a subnet.

## Instructions

* By default, a single VPC can have a maximum of 200 subnets. If the default quota cannot meet your needs, go to the [Quota Center](https://console.byteplus.com/quota/productList/coParameterList?ProviderCode=VPC) to increase the corresponding quota.

* Within the same VPC, subnet CIDR blocks cannot overlap.

* CreateSubnet is an asynchronous API. When a request ID is returned, the system is still creating in the background. You can call [DescribeSubnetAttributes](https://docs.byteplus.com/en/docs/vpc/DescribeSubnetAttributes) API to check the subnet status: `Pending` means creating, and `Available` means creation is complete.

## Debug

[去调试](https://api.byteplus.com/api-explorer/debug?action=CreateSubnet&serviceCode=vpc&version=2020-04-01&groupName=)

## Request parameters

The table below lists only the request parameters unique to this interface and some common parameters. For more information, see [Common parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).

**Action ** String必选 `Example: CreateSubnet`

The interface name. The current API name is `CreateSubnet`.

**Version ** String必选 `Example: 2020-04-01`

The interface version. Current API version is `2020-04-01`.

**VpcId ** String必选 `Example: vpc-257gqcdfvx6n****`

The ID of the VPC to which the subnet will belong.

You can call the [DescribeVpcs](https://docs.byteplus.com/en/docs/vpc/DescribeVpcs) API to query the VPC ID.

**ZoneId ** String必选 `Example: cn-beijing-a`

The Availability Zone ID where the subnet will be created. For more information about zones, see [Region and Availability Zone](https://docs.byteplus.com/en/docs/vpc/Regions-and-Availability-Zones).

**SubnetName ** String`optional` `Example: subnet-1`

Name of the subnet.

* Must be 1 to 128 characters.

* The name must start with a letter, Chinese character, or digit. It may contain periods (.), underscores (_), and hyphens (\-).

* Cannot start with `http://` or `https://`.

* If left blank, the subnet ID is used by default.

**Description ** String`optional` `Example: This is my subnet.`

Description of the subnet.

* Length limit: 0 to 255 characters.

* It must start with a letter, Chinese character, or number. May include commas (,), periods (.), underscores (_), spaces ( ), equal signs (=), hyphens (\-), full\-width commas (，), and full\-width periods (。).

* Cannot start with `http://` or `https://`.

* If left blank, the parameter defaults to an empty string.

**CidrBlock ** String必选 `Example: 172.XX.XX.0/24`

The CIDR block of the subnet.

* Ensure the subnet CIDR block falls within the CIDR range of its VPC.

* The subnet CIDR cannot be identical to the destination CIDR of a route in its VPC, but it can be a subset of that destination CIDR.

* The subnet mask length depends on the VPC's CIDR block, as follows:

   * For 10.XX.XX.XX networks, the mask range is 8 to 29

   * For 172.16.XX.XX networks, the mask range is 12 to 29

   * For 192.168.XX.XX networks, the mask range is 16 to 29.

**Ipv6CidrBlock ** Integer`optional` `Example: 12`

The last 8 bits of an IPv6 subnet CIDR (the subnet has a fixed mask of /64) must be in the range 0 to 255.

> **tip**

* > This parameter can be configured only if the VPC specified by `VpcId` has IPv6 enabled.

* > VPC's IPv6 is currently in invite\-only Beta and temporarily only supports accounts that have completed [enterprise certification](https://docs.byteplus.com/en/docs/6261/64937) to apply for trial. Contact your account manager.

**VpcIpv6CidrBlock ** String`optional` `Example: 2408:XXXX:0:a600::/64`

The IPv6 CIDR block for the subnet, with a fixed mask of /64.

If not provided, a /64 block will be automatically allocated from the VPC's first IPv6 CIDR.

> **tip**

> VPC's IPv6 is currently in invite\-only Beta and temporarily only supports accounts that have completed [Enterprise certification](https://docs.byteplus.com/en/docs/6261/64937) to apply for trial. Contact your account manager.

**Tags.N.Key ** String`optional` `Example: key1`

The tag key of the custom tag.

* N specifies the serial number of a tag key. Valid values: 1–50.

* Separate multiple tag keys with ampersands (&).

* Must not start with `volc:` or `sys:` in any case form.

* It can be 1 to 128 characters in length. It may contain characters in different languages, numbers, spaces ( ), underscores (_), periods (.), half\-width colons (:), slashes (/), equal signs (=), plus signs (+), hyphens (\-), and at signs (@).

* If a tag key contains leading or trailing spaces, the system will automatically delete them.

> **tip**

> Duplicate tag keys are not allowed for the same resource.

**Tags.N.Value ** String`optional` `Example: value1`

The tag value of the custom tag.

* N represents the serial number of the tag value. Valid range: 1–50.

* Separate multiple tag values with ampersands (&).

* The value can be 0 to 256 characters in length. If left blank, the parameter defaults to an empty value.

* The following characters are allowed: characters from all languages, numbers, spaces ( ), underscores (_), periods (.), colons (:), forward slashes (/), equal signs (=), plus signs (+), hyphens (\-), and the at symbol (@).

* Case\-sensitive.

* If a tag value starts or ends with a space, the system will automatically delete them.

> **tip**

> To provide this parameter, provide `Tags.N.Key` first.

**ClientToken ** String`optional` `Example: 123e4567-e89b-12d3-a456-42665544****`

Client token: Used to ensure request idempotency.

* You can use the client to automatically generate a token, but you must make sure that the token is unique among different requests. This prevents repeated actions due to multiple client retries when the call of the API action times out or an internal server error occurs.

* Must not exceed 64 ASCII characters.

* If no ClientToken passed in, the API call does not verify idempotency.

## Response parameters

Only the response parameters specific to this API are listed below. For more information, see [Response structure](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response).

**SubnetId ** String`Example: subnet-bpkdt37pq72zv****`

ID of the newly created subnet.

**RequestId ** String`Example: 2021062415303301022514515207C4****`

Request ID.

## Request example

```json
GET /?Action=CreateSubnet&Version=2020-04-01&VpcId=vpc-257gqcdfvx6n****&ZoneId=cn-beijing-a&CidrBlock=172.XX.XX.0/24&SubnetName=subnet-1 HTTP/1.1
Host: vpc.cn-beijing.byteplusapi.com.cn
X-Date: 20251121T094038Z
Authorization: HMAC-SHA256 Credential=Adfks******wekfwe/20251121/cn-beijing/vpc/request, SignedHeaders=host;x-date, Signature=47a7d934ff7b37c03938******cd7b8278a40a1057690c401e92246a0e41085f
```

## Response example

```json
{
    "ResponseMetadata": {
        "RequestId": "20230604110420****100232280022D31",
        "Action": "CreateSubnet",
        "Version": "2020-04-01",
        "Service": "vpc",
        "Region": "cn-beijing"
    },
    "Result": {
        "RequestId": "2021062415303301022514515207C4****",
        "SubnetId": "subnet-bpkdt37pq72zv****"
    }
}
```

## Error codes

|Status code |Error codes |Error message |Description |
|---|---|---|---|
|400 |DryRunOperation |Exception raised to indicate a successfully authorized action when the DryRun flag is set to true. |This request is set to DryRun. The action is authorized but not executed. |
|400 |IdempotentParameterMismatch |Arguments on this idempotent request are inconsistent with arguments used in previous request(s). |The parameters of this idempotent request are inconsistent with those used in the previous request. |
|400 |InvalidCen.InvalidStatus |The CEN that the specified VPC attached to is not in the correct status for the request. |The CEN instance associated with the VPC is in a state that cannot process the request. Please try again later. |
|400 |InvalidCidr.Malformed |The specified cidr block is malformed. |The format of the specified CIDR block is invalid. |
|400 |InvalidDescription.Malformed |The specified description is malformed. |The specified description format is invalid. Correct the description format and retry. |
|400 |InvalidDescription.Malformed |The specified description is malformed. Ensure the maximum length of description is 255. |The specified description format is invalid. The description cannot exceed 255 characters. |
|400 |InvalidName.Malformed |The specified name is malformed. |The specified name format is invalid. Correct the name format and retry. |
|400 |InvalidName.Malformed |The specified name is malformed. Ensure the maximum length of name is 128. |The specified name format is invalid. The name cannot exceed 128 characters. |
|400 |InvalidParameter.ClientTokenMalformed |The specified parameter ClientToken is malformed. |The format of specified ClientToken is invalid. It cannot exceed 64 ASCII characters. |
|400 |InvalidParameter.EnableIpv6 |Operation failed because IPv6 for the vpc of this subnet is not enabled. |The VPC to which the subnet belongs does not have IPv6 enabled. |
|400 |InvalidParameter.Ipv6CidrBlock |Specified subnet IPv6CidrBlock is invalid. |The subnet IPv6 CIDR is invalid. |
|400 |InvalidRouteCidr.Malformed |The specified CIDR is malformed. |The specified CIDR block is invalid. |
|400 |InvalidSpecificEgress.Mismatch |The specific egress of the IPv6 does not match with the zone if subnet. |The availability zone of the subnet does not match the specified egress for public IPv6. |
|400 |InvalidSubnet.IPv4GatewayAttached |The specified VPC has been attached to IPv4 gateway, local zone subnet cannot be created. |The specified VPC is already associated with an IPv4 gateway, so a LocalZone subnet cannot be created. |
|400 |InvalidSubnet.Ipv6OnlyHasIPv4Cidr |IPv6 only subnet must not have IPv4 CIDR. |An IPv6\-only subnet cannot have an IPv4 CIDR. |
|400 |InvalidSubnet.Ipv6OnlyInIpv4Vpc |You are not allowed to create IPv6 only subnet in IPv4 VPC. |You do not have permission to create IPv6\-only subnets in an IPv4 VPC. |
|400 |InvalidSubnet.Ipv6OnlyNoIPv6Cidr |IPv6 only subnet must have IPv6 CIDR. |An IPv6\-only subnet must have an IPv6 CIDR block. |
|400 |InvalidSubnetCidr.Malformed |The specified subnet cidr is malformed. If you are specifying a subnet cidr, ensure the CIDR of the subnet must fall into the range of the CIDR of the VPC to which the subnet belongs to. |The specified subnet CIDR block is invalid. Ensure the subnet CIDR block falls within the CIDR range of its VPC. |
|400 |InvalidTag.Disorder |The specified index order of tag is malformed. |The index order format specified for the tag is invalid. |
|400 |InvalidTagKey.Malformed |The specified parameter tag key is invalid. |The tag key is invalid. |
|400 |InvalidTagValue.Malformed |The specified parameter tag value is invalid. |The tag value is invalid. |
|400 |InvalidVpc.InvalidStatus |The specified VPC is not in the correct status for the request. |The specified VPC is in a state that cannot respond to this request. |
|400 |InvalidVpcIPv6Cidr.Malformed |The specified vpc IPv6 cidr is malformed. If you are specifying a vpc IPv6 cidr, ensure the CIDR must fall into the range of the CIDR of the VPC to which the subnet belongs to. |The specified VPC IPv6 CIDR block is invalid. Ensure the subnet CIDR block falls within the CIDR range of its VPC. |
|400 |InvalidZone.Malformed |Gateway service not ready in the specified zone. |The gateway service in the specified zone is not ready. |
|400 |LimitExceeded.Tags |You've reached the limit on the number of tags that you can operate at one time. |The maximum tags that you can operate in a single request have been reached. |
|400 |QuotaExceeded.Subnet |Subnet number of VPC exceeded quota. |The maximum number of subnets that can be created has been reached. |
|400 |QuotaExceeded.SystemRouteEntry |You've reached the limit on the number of system route entries per route table. |The maximum number of system routes that you can create has been reached. |
|403 |Forbidden |You are not authorized to create IPv6 only subnet. |You do not have permission to create IPv6\-only subnets. |
|404 |InvalidVpc.NotFound |The specified VPC does not exist. |The specified VPC does not exist. |
|404 |InvalidZoneId.NotFound |The specified zone does not exist. |The specified availability zone does not exist. |
|409 |InvalidRouteCidr.Conflict |The specified CIDR block conflicts with that of another route in your route table. |The specified CIDR block conflicts with another rule's CIDR block in the same route table. |
|409 |InvalidSubnetCidr.Conflict |The specified CIDR block conflicts with that of another subnet in your VPC. |The specified CIDR block conflicts with another subnet CIDR block in the associated VPC. |
|409 |InvalidSubnetCidr.IPv6Conflict |The specified IPv6 CIDR block conflicts with that of another subnet in your VPC. |The specified IPv6 CIDR block conflicts with another subnet IPv6 CIDR block in the associated VPC. |
|412 |IdempotentProcessing |The request uses the same client token as a previous one that is still in process. |The idempotent request is in process. |
