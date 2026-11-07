---
title: "ModifyNetworkInterfaceAttributes - Modifying the network interface information"
product: "Virtual Private Cloud"
product_code: "vpc"
source: "https://docs.byteplus.com/en/docs/vpc/ModifyNetworkInterfaceAttributes"
---

Call the ModifyNetworkInterfaceAttributes API to modify the network interface (ENI) name, description, security groups, source/destination check, and whether to delete along with the ECS instance.

## Instructions

* If the following optional parameters are not configured, the existing configurations will be preserved.

* [BytePlus service network interface](https://docs.byteplus.com/en/docs/vpc/Network-interface-overview#.572R5Y2h57G75Z6L) cannot be modified.

* Each ENI can be associated with up to 5 security groups by default. If the default quota cannot meet your needs, go to [Quota Center](https://console.byteplus.com/quota/productList/coParameterList?ProviderCode=VPC) to increase the corresponding quota.

## Debug

[去调试](https://api.byteplus.com/api-explorer/debug?action=ModifyNetworkInterfaceAttributes&serviceCode=vpc&version=2020-04-01&groupName=)

## Request parameters

The table below lists only the request parameters unique to this interface and some common parameters. For more information, see [Common parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).

**Action ** String必选 `Example: ModifyNetworkInterfaceAttributes`

Interface name. The current API name is `ModifyNetworkInterfaceAttributes`.

**Version ** String必选 `Example: 2020-04-01`

The interface version. The current API version is `2020-04-01`.

**NetworkInterfaceId ** String必选 `Example: eni-bp1fgnh68xyz9****`

ENI ID.

You can call the [DescribeNetworkInterfaces](https://docs.byteplus.com/en/docs/vpc/DescribeNetworkInterfaces) API to query the ENI ID.

**NetworkInterfaceName ** String`optional` `Example: eni-1`

Name of the ENI.

* Must be 1 to 128 characters in length.

* Must start with a letter, Chinese character, or digit. May include periods (.), underscores (_), and hyphens (\-).

**Description ** String`optional` `Example: eni-1-description`

Description of the ENI.

* Must be 0 to 255 characters.

* Must start with a letter, Chinese character, or number. May include commas (,), periods (.), underscores (_), spaces ( ), equal signs (=), hyphens (\-), full\-width commas (，), and full\-width periods (。).

**SecurityGroupIds.N ** String`optional` `Example: sg-3cj59dpb0msxs6c6rrt1u****`

List of security groups associated with the ENI.

You can call the [DescribeSecurityGroups](https://docs.byteplus.com/en/docs/vpc/DescribeSecurityGroups) API to query the security group IDs.

* The specified security group must be in the same VPC as the ENI.

* N specifies the serial number of a Security Group ID. You can call a maximum of 5 IDs in a single request.

* Separate security group IDs with ampersands ( & ).

**PortSecurityEnabled** Boolean `optional` `Example: false`

Enable source/destination check for the ENI. When enabled, the system will automatically block traffic whose source or destination address is not the current ENI.

Please input the enumerated values strictly in case as follows, and do not pass in other values.

* true: Yes.

* false: No.

**DeleteOnTermination ** Boolean`optional` `Example: false`

Enable delete with ECS instance.

Please input the enumerated values strictly in case as follows, and do not pass in other values.

* true: Enable.

* false: Disable.

**TcpEstablishedTimeout ** Integer`optional` `Example: 910`

Configure TCP connection idle timeout. This specifies the maximum length of time a TCP connection can be retained without data transmission. When the timeout is reached, the connection is automatically disconnected and session resources are released.

Value range: 30–7200 seconds.

**TcpClosedAndTimeWaitTimeout ** Integer`optional` `Example: 3`

Configure TCP connection close timeout. This specifies the maximum length of time to wait for responses during the TCP four\-way handshake termination process. If the handshake is not completed before the timeout, the connection is forcibly disconnected and session resources are released.

Value range: 3 to 15 seconds.

**UdpTimeout ** Integer`optional` `Example: 32`

Configure UDP flow timeout period. This specifies the maximum idle retention duration for a bidirectional UDP session with no round\-trip traffic. When the timeout is reached, the session is automatically deleted and resources are released.

Value range: 10 to 180 seconds.

## Response parameters

Only the response parameters specific to this API are listed below. For more information, see [Response structure](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response).

**RequestId ** String`Example: 2021062415303301022514515207C4****`

Request ID.

## Request example

```json
GET /?Action=ModifyNetworkInterfaceAttributes&Version=2020-04-01&NetworkInterfaceId=eni-bp1fgnh68xyz9****&NetworkInterfaceName=ENI_1 HTTP/1.1
Host: vpc.cn-beijing.byteplusapi.com.cn
X-Date: 20251121T094038Z
Authorization: HMAC-SHA256 Credential=Adfks******wekfwe/20251121/cn-beijing/vpc/request, SignedHeaders=host;x-date, Signature=47a7d934ff7b37c03938******cd7b8278a40a1057690c401e92246a0e41085f
```

## Response example

```json
{
    "ResponseMetadata": {
        "RequestId": "20230604110420****100232280022D31",
        "Action": "ModifyNetworkInterfaceAttributes",
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
|400 |DryRunOperation |Exception raised to indicate a successfully authorized action when the DryRun flag is set to true. |This request is set to DryRun. The action is authorized but not executed. |
|400 |Forbidden.TrafficMode |You are not authorized to perform operations on the specified network interface. |You do not have permission to perform operations on the specified ENI. |
|400 |InvalidDescription.Malformed |The specified description is malformed. |The specified description format is invalid. Correct the description format and retry. |
|400 |InvalidDescription.Malformed |The specified description is malformed. Ensure the maximum length of description is 255. |The specified description format is invalid. A description must not exceed 255 characters. |
|400 |InvalidEni.InvalidStatus |The specified elastic network interface is not in the correct status for the request. |The specified ENI is not in a status that can respond to this request. |
|400 |InvalidEni.InvalidType |The type of specified elastic network interface is illegal for the request. |The specified ENI type cannot respond to this request. |
|400 |InvalidInstance.InvalidStatus |The specified instance is not in the correct status for the request. |The specified ECS instance is in a state that cannot process this request. |
|400 |InvalidInstance.InvalidType |The specified instance type is invalid for the request. |The specified ECS instance type cannot respond to the request. |
|400 |InvalidInstance.Malformed |The specified instance does not support vRDMA currently. |The specified ECS instance does not currently support vRDMA. |
|400 |InvalidName.Malformed |The specified name is malformed. |The specified name format is invalid. Correct the name format and try again. |
|400 |InvalidName.Malformed |The specified name is malformed. Ensure the maximum length of name is 128. |The specified name format is invalid. The name cannot exceed 128 characters. |
|400 |InvalidNetworkInterface.InvalidType |The type of specified elastic network interface is illegal for the request. |The specified ENI type cannot respond to this request. |
|400 |InvalidNetworkInterfaceTrafficMode.InvalidAvailabilityZone |The specified elastic network interface availability zone does not support vRDMA currently. |The availability zone of the specified ENI does not currently support vRDMA. |
|400 |InvalidSecurityGroup.InvalidStatus |The specified security group is not in the correct status for the request. |The specified security group is in a state that cannot respond to this request. |
|400 |InvalidSecurityGroup.VpcMismatch |The specified security group and elastic network interface are not in the same VPC. |The specified security group and the ENI are not in the same VPC. |
|400 |InvalidVrdmaEnable.JumboFrameMismatch |The specified instance is not supported to enable vRDMA without jumbo frame enabled. |The specified instance does not support enabling vRDMA when JumboFrame is not enabled. |
|400 |LimitExceeded.HighPerformanceEnisPerInstance |You've reached the limit on the number of high performance elastic network interfaces that can be attached to the specified instance. |The maximum number of high\-performance ENIs that can be bound to the ECS instance has been reached. |
|400 |QuotaExceeded.EniSecurityGroup |You've reached the limit on the number of elastic network interfaces that a security group can associate. |The maximum number of ENIs that can be associated with the security group has been reached. |
|400 |QuotaExceeded.SecurityGroup |The number of security groups bound to the ENI exceeded quota. |The current ENI has reached the maximum number of security groups that can be created. |
|400 |QuotaExceeded.SecurityGroupIp |The number of IP addresses bound to the security group exceeded quota. |The maximum number of IP addresses bound to the security group has been reached. |
|403 |Forbidden |You are not authorized to perform operations on ESI related resources. |Insufficient permissions to manage resources associated with the Elastic Reservation Instance (ESI). |
|403 |Forbidden |You are not authorized to perform operations on the specified ENI. Only ENI attached to an ECS instance is supported. |No permission to perform actions on the specified ENI. Only ENIs attached to ECS instances can have their binding information modified. |
|403 |Forbidden |You are not authorized to perform operations on the specified elastic network interface. The specified elastic network interface is a service\-managed elastic network interface. |No permission to perform actions on the specified ENI. The specified ENI is managed by a cloud product. |
|403 |Forbidden |You are not authorized to perform operations on the specified security group. The specified security group is a service\-managed security group. |No sufficient permissions to perform this operation on the specified security group. The specified security group is managed by the cloud product. |
|404 |InvalidEniId.NotFound |The specified elastic network interface does not exist. |The specified ENI does not exist. |
|404 |InvalidInstance.NotFound |The specified instance does not exist. |The specified ECS instance does not exist. |
|404 |InvalidSecurityGroupId.NotFound |The specified security group does not exist. |The specified security group does not exist. |
|404 |InvalidSubnet.NotFound |The specified subnet does not exist. |The specified subnet does not exist. |
|409 |InvalidSecurityGroupId.Conflict |The specified security group is duplicated with another security group associated with the same elastic network interface. |The specified security group is already associated with this ENI and cannot be bound again. |
