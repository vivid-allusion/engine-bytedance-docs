---
title: "DescribeNetworkInterfaceAttributes - Querying the details of the network interface"
product: "Virtual Private Cloud"
product_code: "vpc"
source: "https://docs.byteplus.com/en/docs/vpc/DescribeNetworkInterfaceAttributes"
---

Call the DescribeNetworkInterfaceAttributes API to view details of the specified network interface (ENI).

## Debug

[去调试](https://api.byteplus.com/api-explorer/debug?action=DescribeNetworkInterfaceAttributes&serviceCode=vpc&version=2020-04-01&groupName=)

## Request parameters

The table below lists only the request parameters unique to this API and some common parameters. For more information, see [Common parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters)

**Action ** String必选 `Example: DescribeNetworkInterfaceAttributes`

API name. The current API name is `DescribeNetworkInterfaceAttributes`.

**Version ** String必选 `Example: 2020-04-01`

The API version. The current API version is `2020-04-01`.

**NetworkInterfaceId ** String必选 `Example: eni-bp1fgnh68xyz9****`

ENI ID.

You can call the [DescribeNetworkInterfaces](https://docs.byteplus.com/en/docs/vpc/DescribeNetworkInterfaces) API to query the ENI ID.

## Response parameters

Only the response parameters specific to this API are listed below. For more information, see [Response structure](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response).

**RequestId ** String`Example: 2021062415303301022514515207C4****`

Request ID.

**AccountId ** String`Example: 2010****`

The ID of the account to which the ENI belongs.

**NetworkInterfaceId ** String`Example: eni-bpacfmxazb4p****`

ENI ID.

**NetworkInterfaceName ** String`Example: eniTestName`

Name of the network interface.

**Description ** String`Example: TestDescription`

Description of the ENI.

**VpcId ** String`Example: vpc-bpacfmxazb4p****`

ID of the VPC to which the ENI belongs.

**VpcName ** String`Example: vpc-name`

The name of the VPC to which the ENI belongs.

**ZoneId ** String`Example: cn-****`

ID of the availability zone to which the ENI belongs.

**SubnetId ** String`Example: subnet-128fhnvjjgg****`

The subnet to which the ENI belongs.

**MacAddress ** String`Example: XX.XX.XX.XX.XX.XX`

The MAC address of the ENI.

**DeviceId ** String`Example: i-hjkib****9`

The ID of the instance to which the ENI is attached. If the ENI is not attached or the `ServiceManaged` parameter is `true`, the returned value for `DeviceId` is empty.

**Type ** String`Example: secondary`

The network interface type.

* primary: Primary network interface

* secondary: Secondary network interface

**PrimaryIpAddress ** String`Example: 192.XX.XX.10`

The primary private IPv4 address of the ENI.

**AssociatedElasticIp ** Object`Example: -`

Information about the EIP associated with the ENI's primary private IPv4 address.

**AllocationId ** String`Example: eip-3tc6w4446mctiq****`

The ID of the EIP.

**EipAddress ** String`Example: 101.XX.XX.199`

The address of the EIP.

**ReleaseWithInstance** Boolean `Example: true`

Whether the EIP is deleted along with the ECS instance. Only the pay\-as\-you\-go EIP bound to the primary private IP address of the primary ENI is valid. When enabled, the EIP will be automatically released when the ECS instance is reclaimed by the system (in 24 hours after unsubscription, due to expiration, or due to arrears) or when the [DeleteInstances](https://docs.byteplus.com/en/docs/ecs/DeleteInstances) API is called.

* true: Yes.

* false: No.

**PrivateIpSets ** Object`Example: -`

The list of private IPv4 addresses for the ENI.

**PrivateIpSet ** Object[]`Example: -`

List of the ENI's private IPv4 addresses.

**PrivateIpAddress ** String`Example: 192.XX.XX.10`

Private IP address of the ENI.

**Primary ** Boolean`Example: true`

Whether it is the primary private IPv4 address.

* true: Primary private IPv4 address

* false: Secondary private IPv4 address

**AssociatedElasticIp ** Object`Example: -`

EIP associated with the ENI's private IPv4 address.

**AllocationId ** String`Example: eip-3tc6w4446mctiq****`

The ID of the EIP.

**EipAddress ** String`Example: 101.XX.XX.199`

The address of the EIP.

**ReleaseWithInstance** Boolean `Example: true`

Whether the EIP is deleted along with the ECS instance. Only the pay\-as\-you\-go EIP bound to the primary private IP address of the primary ENI is valid. When enabled, the EIP will be automatically released when the ECS instance is reclaimed by the system (in 24 hours after unsubscription, due to expiration, or due to arrears) or when the [DeleteInstances](https://docs.byteplus.com/en/docs/ecs/DeleteInstances) API is called.

* true: Yes.

* false: No.

**IPv6Sets ** String[]`Example: 2408::153:3921:XX:XX:7b12:1c5f`

Private IPv6 address of the ENI.

**Status ** String`Example: InUse`

Binding state of the ENI.

* Creating

* Available: Unattached

* Attaching

* InUse: Attached

* Detaching

* Deleting

**PortSecurityEnabled ** Boolean`Example: true`

Enable source/destination check for the ENI. When enabled, the system will automatically block traffic whose source or destination address is not the current ENI.

* true: Yes.

* false: No.

**Attachment** Object `Example: -`

Specify whether to delete with the Elastic Compute Service (ECS) instance.

**DeleteOnTermination ** Boolean`Example: false`

Enable delete with ECS instance.

* true: Enable.

* false: Disable.

**InstanceId ** String`Example: i-wijfn35c****`

ID of the ECS instance.

**ServiceManaged ** Boolean`Example: false`

Whether it is an official BytePlus service ENI. This refers to an ENI automatically created by the system when services like Transit Router, PrivateLink, or VPN Connection are established, providing VPC for the respective backend services.

* true: Yes.

* false: No.

**SecurityGroupIds ** String[]`Example: sg-3ztdcid****90cjtjb`

The ID of the security group associated with the ENI.

**ProjectName ** String`Example: default`

The name of the project to which the ENI belongs.

**Tags ** Object[]`Example: -`

Tag information of the ENI.

**Key ** String`Example: k1`

The tag key.

**Value ** String`Example: v1`

The tag value.

**CreatedAt ** String`Example: 2021-04-09T08:36:47+08:00`

Creation time of the ENI.

**UpdatedAt ** String`Example: 2021-04-09T10:20:41+08:00`

Update time of ENI.

**TcpClosedAndTimeWaitTimeout ** Integer`Example: 2`

TCP connection close timeout. This specifies the maximum length of time to wait for responses during the TCP four\-way handshake termination process. If the handshake is not completed before the timeout, the connection is forcibly disconnected and session resources are released.

**TcpEstablishedTimeout ** Integer`Example: 910`

TCP connection idle timeout. This specifies the maximum length of time a TCP connection can be retained without data transmission. When the timeout is reached, the connection is automatically disconnected and session resources are released.

**UdpTimeout ** Integer`Example: 32`

UDP flow timeout period. This specifies the maximum idle retention duration for a bidirectional UDP session with no round\-trip traffic. When the timeout is reached, the session is automatically deleted and resources are released.

## Request example

```json
GET /?Action=DescribeNetworkInterfaceAttributes&Version=2020-04-01&NetworkInterfaceId=eni-bp1fgnh68xyz9**** HTTP/1.1
Host: vpc.cn-beijing.byteplusapi.com.cn
X-Date: 20251121T094038Z
Authorization: HMAC-SHA256 Credential=Adfks******wekfwe/20251121/cn-beijing/vpc/request, SignedHeaders=host;x-date, Signature=47a7d934ff7b37c03938******cd7b8278a40a1057690c401e92246a0e41085f
```

## Response example

```json
{
    "ResponseMetadata": {
        "RequestId": "2021062415303301022514515207C4****",
        "Action": "DescribeNetworkInterfaceAttributes",
        "Version": "2020-04-01",
        "Service": "vpc",
        "Region": "cn-beijing"
    },
    "Result": {
        "RequestId": "2021062415303301022514515207C4****",
        "AccountId": "210000****",
        "NetworkInterfaceId": "eni-2ff3dn0hbrfuo5oxruuqp****",
        "NetworkInterfaceName": "test-eni-1",
        "Description": "",
        "VpcId": "vpc-3tj9fo0uqy3vj0x2****",
        "VpcName": "test",
        "ZoneId": "cn-****",
        "SubnetId": "subnet-3tj9fva4dm3vj0x2****",
        "MacAddress": "XX:XX:XX:XX:XX:XX",
        "DeviceId": "i-3tkkmwa1t63vj0x0****",
        "Type": "primary",
        "PrimaryIpAddress": "172.XX.XX.16",
        "AssociatedElasticIp": {
            "AllocationId": "eip-3tczde6w4449q06m****",
            "EipAddress": "101.XX.XX.199",
            "ReleaseWithInstance": true
        },
        "PrivateIpSets": {
            "PrivateIpSet": [
                {
                    "PrivateIpAddress": "10.XX.XX.245",
                    "Primary": true,
                    "AssociatedElasticIp": {
                        "EipAddress": "101.XX.XX.199",
                        "AllocationId": "eip-3tczde6w4449q06m****",
                        "ReleaseWithInstance": true
                    }
                }
            ]
        },
        "IPv6Sets": [
            "2408::153:3921:XX:XX:7b12:1c5f",
            "2408:4008:2cf:XX:XX:dd1e:2a22:5ddf"
        ],
        "Status": "InUse",
        "PortSecurityEnabled": false,
        "Attachment": {
            "DeleteOnTermination": false,
            "InstanceId": "i-wijfn35c****"
        },
        "ServiceManaged": false,
        "SecurityGroupIds": [
            "sg-3tj9fo0uqy3vj0x2****"
        ],
        "ProjectName": "default",
        "Tags": [
            {
                "Key": "k1",
                "Value": "v1"
            },
            {
                "Key": "k2",
                "Value": ""
            }
        ],
        "CreatedAt": "2021-07-23T17:49:21+08:00",
        "UpdatedAt": "2021-07-23T17:49:24+08:00"
    }
}
```

## Error codes

|Status code |Error codes |Error message |Description |
|---|---|---|---|
|400 |DryRunOperation |Exception raised to indicate a successfully authorized action when the DryRun flag is set to true. |This request is set to DryRun action. The action has been authorized but has not been executed. |
|400 |Forbidden.TrafficMode |You are not authorized to perform operations on the specified network interface. |You do not have permission to perform operations on the specified ENI. |
|403 |Forbidden |You are not authorized to perform operations on the specified elastic network interface. |No sufficient permissions to perform this operation on the specified ENI. |
|404 |InvalidEniId.NotFound |The specified elastic network interface does not exist. |The specified ENI does not exist. |
|429 |RateLimited |Too many requests, please try again later. |Too many requests, try again later. |
