---
title: "Create HaVip - Creating a HaVip"
product: "Virtual Private Cloud"
product_code: "vpc"
source: "https://docs.byteplus.com/en/docs/vpc/CreateHaVip"
---

Call the CreateHaVip API to create a high\-availability virtual IP (HaVip).

## Notes

* A single account can create a maximum of 20 HaVips per region.

* A maximum of 5 HaVips can be created within a single VPC.

* CreateHaVip is an asynchronous API. When a request ID is returned, the system is still creating in the background. You can call [DescribeHaVips](https://docs.byteplus.com/en/docs/vpc/DescribePrefixLists) API to view the HaVip status. `Creating` means it is being created, and `Available` means creation is complete.

## Debug

[去调试](https://api.byteplus.com/api-explorer/debug?action=CreateHaVip&serviceCode=vpc&version=2020-04-01&groupName=)

## Request parameters

The table below lists only the request parameters unique to this interface and some common parameters. For more information, see [Common parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).

**Action ** String必选 `Example: CreateHaVip`

Interface name. The current API name is `CreateHaVip`.

**Version ** String必选 `Example: 2020-04-01`

The interface version. The current API version is `2020-04-01`.

**SubnetId ** String必选 `Example: subnet-bp1s5fn4gn2tws03****`

The ID of the subnet to which the HaVip belongs. This subnet will provide the IP address for the HaVip.

You can call the [DescribeSubnets](https://docs.byteplus.com/en/docs/vpc/DescribeSubnets) API to query the subnet ID.

**IpAddress ** String`optional` `Example: 192.XX.XX.10`

IP address of the HaVip.

* If you specify this parameter, the entered IP address must be an unused address within the CIDR block of the `SubnetId`.

* If you do not specify this parameter, the platform will automatically assign an unused IP address from the CIDR block of the `SubnetId`.

**HaVipName ** String`optional` `Example: havip-1`

The name of the HaVip.

* Must be 1 to 128 characters in length.

* Must start with a letter, Chinese character, or digit. May include periods (.), underscores (_), and hyphens (\-).

* If left blank, it defaults to the HaVip ID.

**Description ** String`optional` `Example: This is my HaVip.`

Description of the HaVip.

* Length limit: 0 to 255 characters.

* Must start with a letter, Chinese character, or number. It may include half\-width commas (,), periods (.), underscores (_), spaces ( ), equal signs (=), hyphens (\-), full\-width commas (，), and full\-width periods (。).

* If left blank, it defaults to an empty string.

**Tags.N.Key ** String`optional` `Example: key1`

The tag key of the custom tag.

* N represents the serial number of a tag key. Valid range: 1–50.

* Separate multiple tag keys with ampersands ( & ).

* Must not start with `volc:` or `sys:` in any case form.

* Must be 1 to 128 characters. May include characters in different languages, numbers, spaces ( ), underscores (_), periods (.), half\-width colons (:), slashes (/), equal signs (=), plus signs (+), hyphens (\-), and at signs (@).

* If a tag key contains leading or trailing spaces, the system will automatically delete them.

> **tip**

> Duplicate tag keys are not allowed for the same resource.

**Tags.N.Value ** String`optional` `Example: value1`

The tag value of the custom tag.

* N specifies the serial number of the tag value. Valid range: 1–50.

* Separate multiple tag values with ampersands (&).

* The value can be 0 to 256 characters in length. If left blank, the parameter defaults to an empty value.

* May include multilingual characters, digits, spaces ( ), underscores (_), periods (.), half\-width colons (:), slashes (/), equal signs (=), plus signs (+), hyphens (\-), and at signs (@).

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

**HaVipId ** String`Example: havip-2zeo05qre24nhrqpy****`

The ID of the newly created HaVip.

**IpAddress ** String`Example: 192.XX.XX.10`

IP address of newly created HaVip.

**RequestId ** String`Example: C44F62BE-9CE7-4277-B117-69243F39****`

Request ID.

## Request example

```json
GET /?Action=CreateHaVip&Version=2020-04-01&SubnetId=subnet-ina9r9xnfpc08gbs****&IpAddress=192.XX.XX.10&HaVipName=havip-1 HTTP/1.1
Host: vpc.cn-beijing.byteplusapi.com.cn
X-Date: 20251121T094038Z
Authorization: HMAC-SHA256 Credential=Adfks******wekfwe/20251121/cn-beijing/vpc/request, SignedHeaders=host;x-date, Signature=47a7d934ff7b37c03938******cd7b8278a40a1057690c401e92246a0e41085f
```

## Response example

```json
{
    "ResponseMetadata": {
        "RequestId": "202201271634510102251100110614****",
        "Action": "CreateHaVip",
        "Version": "2020-04-01",
        "Service": "vpc",
        "Region": "cn-beijing"
    },
    "Result": {
        "RequestId": "202201271634510102251100110614****",
        "HaVipId": "havip-12awu7gcpmdxc17q7y23q****",
        "IpAddress": "192.XX.XX.10"
    }
}
```

## Error codes

|Status code |Error codes |Error message |Description |
|---|---|---|---|
|400 |DryRunOperation |Exception raised to indicate a successfully authorized action when the DryRun flag is set to true. |This request is set to DryRun. The action is authorized but not executed. |
|400 |IdempotentParameterMismatch |Arguments on this idempotent request are inconsistent with arguments used in previous request(s). |The parameters of this idempotent request are inconsistent with those used in the previous request. |
|400 |InsufficientIpInSubnet |The specified subnet does not contain enough free private IP addresses to fulfill your request. |Insufficient available IPs under the specified subnet. |
|400 |InvalidDescription.Malformed |The specified description is malformed. |The specified description format is invalid. Correct the description format and retry. |
|400 |InvalidDescription.Malformed |The specified description is malformed. Ensure the maximum length of description is 255. |The specified description format is invalid. A description cannot exceed 255 characters. |
|400 |InvalidEniIp.Malformed |The specified elastic network interface ip is malformed. If you are specifying an IP of an elastic network interface, ensure it must fall into the range of the CIDR block of the subnet to which the elastic network interface belongs to. |The specified Elastic Network Interface (ENI) IP is invalid. Please ensure the ENI IP falls within the CIDR range of its subnet. |
|400 |InvalidHaVip.CreateInIpv6Subnet |You are not allowed to create HaVip in IPv6 only subnet. |Creating a HaVip in an IPv6\-only subnet is not allowed. |
|400 |InvalidIp.Malformed |The specified ip is malformed. |The specified IP is invalid. |
|400 |InvalidIpAddress.Malformed |The specified IP address is malformed. Ensure that the IP address of the HaVip is in the range of the CIDR block of the subnet. |The specified HaVip is invalid. Ensure the IP address of the HaVip falls within the CIDR block of its subnet. |
|400 |InvalidName.Malformed |The specified name is malformed. |The specified name format is invalid. Correct the name format and retry. |
|400 |InvalidName.Malformed |The specified name is malformed. Ensure the maximum length of name is 128. |The specified name format is invalid. The name cannot exceed 128 characters. |
|400 |InvalidParameter.ClientTokenMalformed |The specified parameter ClientToken is malformed. |The specified ClientToken is invalid. It cannot be more than 64 ASCII characters. |
|400 |InvalidPrivateIp.Malformed |The specified private ip is malformed. |The specified private IP address is invalid. |
|400 |InvalidSubnet.InvalidStatus |The specified subnet is not in the correct status for the request. |The specified subnet is in a state that cannot process this request. |
|400 |InvalidTag.Disorder |The specified index order of tag is malformed. |The index order format specified for the tag is invalid. |
|400 |InvalidTagKey.Malformed |The specified parameter tag key is invalid. |The tag key is invalid. |
|400 |InvalidTagValue.Malformed |The specified parameter tag value is invalid. |The tag value is invalid. |
|400 |LimitExceeded.Tags |You've reached the limit on the number of tags that you can operate at one time. |You have reached the maximum number of tags that can be processed in a single request. |
|400 |QuotaExceeded.HaVip |HaVip number exceeded quota. |The current account has reached the maximum number of HaVips allowed in this region. |
|400 |QuotaExceeded.HaVip |HaVip number of VPC exceeded quota. |The current VPC has reached the maximum number of HaVips allowed. |
|404 |InvalidSubnet.NotFound |The specified subnet does not exist. |The specified subnet does not exist. |
|404 |InvalidZoneId.NotFound |The specified zone does not exist. |The specified availability zone does not exist. |
|409 |InvalidIpAddress.InUse |The specified IP address is in use. |The specified IP address is already in use. |
|412 |IdempotentProcessing |The request uses the same client token as a previous one that is still in process. |The idempotent request is in process. |
