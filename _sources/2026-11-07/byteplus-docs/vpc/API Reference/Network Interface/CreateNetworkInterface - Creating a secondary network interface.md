---
title: "CreateNetworkInterface - Creating a secondary network interface"
product: "Virtual Private Cloud"
product_code: "vpc"
source: "https://docs.byteplus.com/en/docs/vpc/CreateNetworkInterface"
---

Call the CreateNetworkInterface API to create a secondary network interface (ENI).

## Instructions

* By default, a maximum of 5,000 secondary ENIs can be created per account per region. If the default quota cannot meet your needs, go to the [Quota Center](https://console.byteplus.com/quota/productList/coParameterList?ProviderCode=VPC) to increase the corresponding quota.

* This API supports only the creation of secondary ENIs.

* You can also call the [RunInstances](https://docs.byteplus.com/en/docs/ecs/RunInstances) API, specify `NetworkInterfaces.N.SubnetId` as needed to create an ECS instance along with secondary ENIs attached to it.

* CreateNetworkInterface is an asynchronous API. When a request ID is returned, the system is still creating in the background. You can call [DescribeNetworkInterfaceAttributes](https://docs.byteplus.com/en/docs/vpc/DescribeNetworkInterfaceAttributes) to check the ENI status. `Creating` means it is being created, and `Available` means configuration is complete.

## Debug

[去调试](https://api.byteplus.com/api-explorer/debug?action=CreateNetworkInterface&serviceCode=vpc&version=2020-04-01&groupName=)

## Request parameters

The table below lists only the request parameters unique to this interface and some common parameters. For more information, see [Common parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).

**Action ** String必选 `Example: CreateNetworkInterface`

Interface name. The current API name is `CreateNetworkInterface`.

**Version ** String必选 `Example: 2020-04-01`

The interface version. The current API version is `2020-04-01`.

**NetworkInterfaceName ** String`optional` `Example: eni-1`

Name of the secondary ENI.

* Length must be 1 to 128 characters.

* Must start with a letter, Chinese character, or number. May include periods (.), underscores (_), and hyphens (\-).

* If left blank, the secondary ENI ID is used by default.

**Description ** String`optional` `Example: eni-1-description`

Description of the secondary ENI.

* Length limit: 0 to 255 characters.

* Must start with a letter, Chinese character, or number. It may include half\-width commas (,), periods (.), underscores (_), spaces ( ), equal signs (=), hyphens (\-), full\-width commas (，), and full\-width periods (。).

* If left blank, this defaults to an empty string.

**SubnetId ** String必选 `Example: subnet-h256yg29j****`

The ID of the subnet where the secondary ENI will be located.

You can call the [DescribeSubnets](https://docs.byteplus.com/en/docs/vpc/DescribeSubnets) API to query the subnet ID.

**PrimaryIpAddress ** String`optional` `Example: 192.XX.XX.10`

The primary private IPv4 address for the secondary ENI.

* If specified, it must be an available private IPv4 address within the corresponding subnet.

* If not specified, an available private IPv4 address will be automatically allocated from the corresponding subnet.

**SecondaryPrivateIpAddressCount ** Integer`optional` `Example: 1`

The number of secondary private IPv4 addresses to assign to the secondary ENI. Valid range: 1 to 49.

If this parameter is provided, the system will automatically allocate the specified number of available IPv4 addresses from the ENI's subnet as secondary private IPv4 addresses for the newly created ENI.

> **tip**

> Parameters `SecondaryPrivateIpAddressCount` and `PrivateIpAddress.N` cannot be specified simultaneously.

**PrivateIpAddress.N ** String`optional` `Example: 192.168.XX.10`

Specify a secondary private IPv4 address for the ENI.

* N represents the serial number of a secondary private IPv4 address. The valid range is 1 to 49.

* Separate multiple private IPv4 addresses with ampersands (&).

* The specified private IPv4 addresses must be available addresses within the ENI's subnet.

> **tip**

> Parameters `SecondaryPrivateIpAddressCount` and `PrivateIpAddress.N` cannot be specified simultaneously.

**Ipv6AddressCount ** Integer`optional` `Example: 2`

The number of private IPv6 addresses to assign to the ENI.

If this parameter is provided, the system will automatically allocate the corresponding number of available private IPv6 addresses from the ENI's subnet as its private IPv6 addresses.

> **tip**

* > Parameters `Ipv6Address.N` and `Ipv6AddressCount` cannot be specified simultaneously.

* > The assignment of IPv6 addresses to ENIs is currently in Invite\-only Beta stage. If you need a trial, please contact your account manager.

**Ipv6Address.N ** String`optional` `Example: I2408:4008:55b:XXXX:XXXX:922:96c4:e0`

Assign a private IPv6 address to the ENI.

* N: Indicates the serial number of the private IPv6 address, and its range of values is determined by the ENI status.

   * When the ENI is in the Available (unattached) state, the value range is 1 to 10.

   * When the ENI is in the InUse (attached) state, the value range for N is constrained by the instance type specifications. For more details, please see the [Instance type overview](https://docs.byteplus.com/en/docs/ecs/Introduction-to-instance-types).

* Separate multiple private IPv6 addresses with ampersands ( & ).

* The specified IP address must be an available (unused) IP within the ENI's subnet.

> **tip**

* > Parameters `Ipv6Address.N` and `Ipv6AddressCount` cannot be specified simultaneously.

* > The assignment of IPv6 addresses to ENIs is currently in Invite\-only Beta stage. If you need a trial, please contact your account manager.

**SecurityGroupIds.N ** String`optional` `Example: sg-123edfgt8hhvj****`

IDs of the security groups to which the secondary ENI will be added.

You can call the [DescribeSecurityGroups](https://docs.byteplus.com/en/docs/vpc/DescribeSecurityGroups) API to query security group IDs.

* The security group(s) must reside in the same VPC as the secondary ENI.

* N specifies the serial number of a Security Group ID. You can call a maximum of 5 IDs in a single request.

* Separate security group IDs with ampersands ( & ).

**PortSecurityEnabled ** Boolean`optional` `Example: false`

Enable source/destination check for the ENI. When enabled, the system will automatically block traffic whose source or destination address is not the current ENI.

Please input the enumerated values strictly in case as follows, and do not pass in other values.

* true: Yes.

* false (default): No.

**ProjectName ** String`optional` `Example: default`

The name of the project to which the ENI belongs. If left blank, it defaults to the default project.

**Tags.N.Key ** String`optional` `Example: key1`

The tag key of the custom tag.

* N represents the serial number of the tag key. Valid range: 1–50.

* Separate multiple tag keys with ampersands (&).

* Must not start with `volc:` or `sys:` in any case form.

* Must be 1 to 128 characters. Allowed characters include multilingual letters, numbers, spaces ( ), underscores (_), periods (.), half\-width colons (:), slashes (/), equal signs (=), plus signs (+), hyphens (\-), and at signs (@).

* If a tag key contains leading or trailing spaces, the system will automatically delete them.

> **tip**

> Duplicate tag keys are not allowed for the same resource.

**Tags.N.Value ** String`optional` `Example: value1`

The tag value of the custom tag.

* N represents the serial number of the tag value. Valid values: 1–50.

* Separate multiple tag values with ampersands (&).

* The value can be 0 to 256 characters in length. If left blank, the parameter defaults to an empty value.

* May include multilingual characters, numbers, spaces ( ), underscores (_), periods (.), half\-width colons (:), slashes (/), equal signs (=), plus signs (+), hyphens (\-), and at signs (@).

* Case\-sensitive.

* If a tag value starts or ends with a space, the system will automatically delete them.

> **tip**

> To provide this parameter, provide `Tags.N.Key` first.

**ClientToken ** String`optional` `Example: 123e4567-e89b-12d3-a456-42665544****`

Client token: Used to ensure request idempotency.

* You can use the client to automatically generate a token, but you must make sure that the token is unique among different requests. This prevents repeated actions due to multiple client retries when the call of the API action times out or an internal server error occurs.

* Must not exceed 64 ASCII characters.

* If no ClientToken passed in, the API call does not verify idempotency.

**TcpEstablishedTimeout ** Integer`optional` `Example: 910`

Configure the TCP connection idle timeout period. This specifies the maximum length of time a TCP connection can be retained without data transmission. When the timeout is reached, the connection is automatically disconnected and session resources are released.

* Value range: 30–7200 seconds.

* Default: 910 seconds.

**TcpClosedAndTimeWaitTimeout ** Integer`optional` `Example: 3`

Configure TCP connection close timeout. This specifies the maximum length of time to wait for responses during the TCP four\-way handshake termination process. If the handshake is not completed before the timeout, the connection is forcibly disconnected and session resources are released.

* Value range: 3 to 15 seconds.

* Default: 3 seconds.

**UdpTimeout ** Integer`optional` `Example: 32`

Configure the UDP flow timeout. This specifies the maximum idle retention duration for a bidirectional UDP session with no round\-trip traffic. When the timeout is reached, the session is automatically deleted and resources are released.

* Value range: 10 to 180 seconds.

* Default: 32 seconds.

## Response parameters

Only the response parameters specific to this API are listed below. For more information, see [Response structure](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response).

**RequestId ** String`Example: 2021062415303301022514515207C4****`

Request ID.

**NetworkInterfaceId ** String`Example: eni-bp1fgnh68xyz9****`

The ID of the newly created secondary ENI.

## Request example

```json
GET /?Action=CreateNetworkInterface&Version=2020-04-01&SubnetId=subnet-h256yg29j****&SecurityGroupIds.1=sg-123edfgt8hhvj****&PrimaryIpAddress=192.XX.XX.10&NetworkInterfaceName=eni-1 HTTP/1.1
Host: vpc.cn-beijing.byteplusapi.com.cn
X-Date: 20251121T094038Z
Authorization: HMAC-SHA256 Credential=Adfks******wekfwe/20251121/cn-beijing/vpc/request, SignedHeaders=host;x-date, Signature=47a7d934ff7b37c03938******cd7b8278a40a1057690c401e92246a0e41085f
```

## Response example

```json
{
    "ResponseMetadata": {
        "RequestId": "20230604110420****100232280022D31",
        "Action": "CreateNetworkInterface",
        "Version": "2020-04-01",
        "Service": "vpc",
        "Region": "cn-beijing"
    },
    "Result": {
        "NetworkInterfaceId": "eni-bp1fgnh68xyz9****",
        "RequestId": "2021062415303301022514515207C4****"
    }
}
```

## Error codes

|Status code |Error codes |Error message |Description |
|---|---|---|---|
|400 |DryRunOperation |Exception raised to indicate a successfully authorized action when the DryRun flag is set to true. |This request is set to DryRun action. The action has been authorized but has not been executed. |
|400 |Forbidden.TrafficMode |You are not authorized to perform operations on the specified network interface. |You do not have permission to perform operations on the specified ENI. |
|400 |IdempotentParameterMismatch |Arguments on this idempotent request are inconsistent with arguments used in previous request(s). |The parameters of this idempotent request are inconsistent with those used in the previous request. |
|400 |InsufficientIpInSubnet |The specified subnet does not contain enough free private IP addresses to fulfill your request. |Insufficient available IPs under the specified subnet. |
|400 |InvalidDescription.Malformed |The specified description is malformed. |The specified description format is invalid. Correct the description format and retry. |
|400 |InvalidDescription.Malformed |The specified description is malformed. Ensure the maximum length of description is 255. |The specified description format is invalid. Description cannot exceed 255 characters. |
|400 |InvalidEniIp.Malformed |The specified elastic network interface ip is malformed. If you are specifying an IP of an elastic network interface, ensure it must fall into the range of the CIDR block of the subnet to which the elastic network interface belongs to. |The specified ENI IP is invalid. Please ensure the ENI IP falls within the CIDR range of its subnet. |
|400 |InvalidEniIpPrefix.Malformed |The specified elastic network interface IP prefix is malformed. ensure it must fall into the range of the CIDR block of the subnet. |The specified ENI IP prefix is invalid. Please ensure the ENI IP prefix falls within the CIDR range of its subnet. |
|400 |InvalidEniType.Malformed |The specified elastic network interface type is malformed. |The specified ENI type is invalid. |
|400 |InvalidIp.Malformed |The specified ip is malformed. |The specified IP is invalid. |
|400 |InvalidIpPrefix.Malformed |The specified ipv4 prefix is malformed. |The specified IPv4 prefix is invalid. |
|400 |InvalidIpv6.Malformed |The specified IPv6 address is malformed. |The specified IPv6 address is invalid. |
|400 |InvalidIpv6Prefix.Malformed |The specified ipv6 prefix is malformed. |The specified IPv6 prefix is invalid. |
|400 |InvalidName.Malformed |The specified name is malformed. |The specified name format is invalid. Correct the name format and try again. |
|400 |InvalidName.Malformed |The specified name is malformed. Ensure the maximum length of name is 128. |The specified name format is invalid. The name cannot exceed 128 characters in length. |
|400 |InvalidNetworkInterface.InvalidType |The type of specified elastic network interface is illegal for the request. |The specified type of ENI cannot process this request. |
|400 |InvalidNetworkInterfaceTrafficMode.InvalidAvailabilityZone |The specified elastic network interface availability zone does not support vRDMA currently. |The availability zone of the specified ENI does not currently support vRDMA. |
|400 |InvalidParameter.ClientTokenMalformed |The specified parameter ClientToken is malformed. |The format of the specified ClientToken is invalid. It cannot exceed 64 ASCII characters. |
|400 |InvalidParameter.ENIVtepIp |The specified VTEP IP is invalid. |The specified ENI VTEP IP is invalid. |
|400 |InvalidPrivateIp.Malformed |The specified private ip is malformed. |The specified private IP address is invalid. |
|400 |InvalidSecurityGroup.InvalidStatus |The specified security group is not in the correct status for the request. |The specified security group is in a state that cannot respond to this request. |
|400 |InvalidSecurityGroup.VpcMismatch |The specified security group and elastic network interface are not in the same VPC. |The specified security group and the ENI are not in the same VPC. |
|400 |InvalidSubnet.DisableIpv6 |Specified subnet disable IPv6 |This subnet does not have IPv6 enabled. |
|400 |InvalidSubnet.IPv4Disabled |IPv4 has been disabled for the specified subnet. |IPv4 has been disabled for the specified subnet. |
|400 |InvalidSubnet.InvalidStatus |The specified subnet is not in the correct status for the request. |The specified subnet is in a state that cannot process this request. |
|400 |InvalidTag.Disorder |The specified index order of tag is malformed. |The index order format specified for the tag is invalid. |
|400 |InvalidTagKey.Malformed |The specified parameter tag key is invalid. |The tag key is invalid. |
|400 |InvalidTagValue.Malformed |The specified parameter tag value is invalid. |The tag value is invalid. |
|400 |LimitExceeded.Ipv6AddressesPerEni |You've reached the limit on the number of IPv6 addresses per ENI that you can assign. |The maximum number of assignable IPv6 addresses for the ENI has been reached. |
|400 |LimitExceeded.PrivateIpsPerEni |You've reached the limit on the number of private IPs per ENI that you can assign. |The maximum number of assignable secondary IP addresses for the ENI has been reached. |
|400 |LimitExceeded.Tags |You've reached the limit on the number of tags that you can operate at one time. |The maximum tags that you can operate in a single request have been reached. |
|400 |QuotaExceeded.Eni |ENI number exceeded quota. |Reached the maximum network interfaces that you can create. |
|400 |QuotaExceeded.EniSecurityGroup |You've reached the limit on the number of elastic network interfaces that a security group can associate. |The maximum number of ENIs that can be associated with the security group has been reached. |
|400 |QuotaExceeded.SecurityGroup |The number of security groups bound to the ENI exceeded quota. |The current ENI has reached the maximum number of security groups that can be created. |
|400 |QuotaExceeded.SecurityGroupIp |The number of IP addresses bound to the security group exceeded quota. |The maximum number of IP addresses bound to the security group has been reached. |
|403 |Forbidden.IpPrefix |You are not authorized to allocate ip prefix. |You do not have permission to assign ENI prefixes. |
|403 |Forbidden.MacAddress |You are not authorized to specify MAC address. |You do not have permission to specify a MAC address. |
|403 |Forbidden.ShareENI |You are not authorized to perform operations on the specified elastic network interface. The specified elastic network interface in shared subnet does not support this operation. |No permission to perform actions on the specified ENI. This operation is not supported for the specified ENI in a shared subnet. |
|403 |Forbidden |You are not authorized to perform operations on eni trunking. |No permission to use ENI Trunking. |
|403 |Forbidden |You are not authorized to perform operations on the specified security group. The specified security group is a service\-managed security group. |No permission to perform this operation on the specified security group. The specified security group is managed by the cloud product. |
|404 |InvalidProject.NotFound |The specified Project does not exist. |The specified project does not exist. |
|404 |InvalidSecurityGroupId.NotFound |The specified security group does not exist. |The specified security group does not exist. |
|404 |InvalidSubnet.NotFound |The specified subnet does not exist. |The specified subnet does not exist. |
|404 |InvalidZoneId.NotFound |The specified zone does not exist. |The specified availability zone does not exist. |
|409 |InvalidIPv4Prefix.Conflict |The specified IPv4 prefix is in use. |The specified IPv4 prefix is currently in use. |
|409 |InvalidIPv6Prefix.Conflict |The specified IPv6 prefix is in use. |The specified IPv6 prefix is in use. |
|409 |InvalidIpAddress.InUse |The specified IP address is in use. |The specified IP address is already in use. |
|409 |InvalidIpPrefix.Conflict |The parameters for IP prefix number and IP prefixes cannot be specified at the same time. |The request cannot include both an IP prefix count and specific IP prefixes simultaneously. |
|409 |InvalidMacAddress.Conflict |The specified MAC address already exists. |The specified MAC address already exists. |
|409 |InvalidParameter.ParameterConflict |The parameters for IP address number and IP addresses cannot be specified at the same time. |The request cannot include both an IP address count and specific IP addresses simultaneously. |
|409 |InvalidSecurityGroupId.Conflict |The specified security group is duplicated with another security group associated with the same elastic network interface. |The specified security group is already associated with this ENI and cannot be bound again. |
|412 |IdempotentProcessing |The request uses the same client token as a previous one that is still in process. |The idempotent request is in process. |
