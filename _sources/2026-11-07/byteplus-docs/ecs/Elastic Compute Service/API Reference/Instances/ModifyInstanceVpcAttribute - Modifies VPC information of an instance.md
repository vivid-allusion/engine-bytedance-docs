---
title: "ModifyInstanceVpcAttribute - Modifies VPC information of an instance"
product: "Elastic Compute Service"
product_code: "ecs"
source: "https://docs.byteplus.com/en/docs/ecs/ModifyInstanceVpcAttribute"
---

Call the ModifyInstanceVpcAttribute operation to modify the VPC, subnet, or security group of an instance.

<span id=".5rOo5oSP5LqL6aG5"></span>
## Usage notes

When you call this operation, refer to [Changing VPC or subnet](https://docs.byteplus.com/en/docs/ecs/Changing-the-VPC-or-subnet-of-an-ECS-instance#.5YmN5o-Q5p2h5Lu2) for the conditions that the target instance and VPC must meet.

<span id=".6K-35rGC6K-05piO"></span>
## Request description

The common scenarios for this operation are as follows:


* VPC change scenario: Changing the VPC is strongly associated with changing the subnet and security group. When you specify a new value for `VpcId`, you need to specify both the subnet and security group parameters.

* Non\-VPC change scenario: When you do not configure `VpcId`, the VPC is not changed. However, you can change only the subnet, or change both the subnet and security group.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">The security group can only be changed when the subnet is changed. The <code>SubnetId</code> parameter in this operation is required, and its value must be the new subnet ID.</div>


<span id=".6LCD6K-V"></span>
## Debugging

[去调试](https://api.byteplus.com/api-explorer/?action=ModifyInstanceVpcAttribute&groupName=%E5%AE%9E%E4%BE%8B&serviceCode=ecs&version=2020-04-01)


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters

Only the request parameters specific to this operation and some common parameters are listed below. For details, refer to [Common parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).



**Action ** <span data-label="purple">string </span><span data-api-tag="require|R4oUJo">必选</span> `Sample value: ModifyInstanceVpcAttribute`

The operation that you want to perform. Valid value: ModifyInstanceVpcAttribute.



**Version ** <span data-label="purple">string </span><span data-api-tag="require|k3Ajan">必选</span> `Sample value: 2020-04-01`

The API version. Value: 2020\-04\-01.



**ClientToken ** <span data-label="purple">string </span>`Optional` `Sample value: 333456899ff****`

The ClientToken is used to ensure the request idempotency. The client automatically generates a token to ensure that the token is unique among different requests. This prevents repeated actions due to multiple client retries when the call of the API action times out or an internal server error occurs.

Value: Only ASCII characters are supported. The length is no more than 64 ASCII characters.



**InstanceId ** <span data-label="purple">string </span><span data-api-tag="require|NaPWwa">必选</span> `Sample value: i-bp1iudwa5b1tqag1****`

The instance ID.



**PrimaryIpAddress ** <span data-label="purple">string </span>`Optional` `Sample value: 172.17.XX.XX`

The new primary private IP address must be within the CIDR block of the subnet.


* You can call [DescribeNetworkInterfaceAttributes](https://docs.byteplus.com/en/docs/vpc/ModifyNetworkInterfaceAttributes) to query the primary private IP address of the network interface.

* If you do not configure this parameter, the primary private IP address is randomly allocated from the CIDR block of the subnet.



**SecurityGroupIds.N ** <span data-label="purple">string[] </span>`Optional` `Sample value: SecurityGroupIds.1=sg-33gf6al0psvsw1pz2ij8e****&SecurityGroupIds.2=sg-o6w9l8bc8dgmkw87****`

The ID of the security group to which the instance is added after the VPC is changed.


* Parameter \- N: Specifies the serial number of the security group. Valid range: 1\-5.

* Use & to separate multiple security group IDs.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">This parameter is required if and only if <code>VpcId</code> is specified.</div>


* <div data-tips="true" data-tips-type="tip">You can call <a href="https://docs.byteplus.com/en/docs/vpc/DescribeSecurityGroups">DescribeSecurityGroups</a> to query security group IDs.</div>




**SubnetId ** <span data-label="purple">string </span><span data-api-tag="require|fDlLMS">必选</span> `Sample value: subnet-33gf6b2rztdkw1pz2ijvq****`

The ID of the new subnet.


* You cannot specify the ID of the current subnet of the instance.

* When `VpcId` is empty, the new subnet and the original subnet must belong to the same availability zone in the same VPC. You can call [DescribeSubnets](https://docs.byteplus.com/en/docs/vpc/DescribeSubnets) to query the IDs of the subnets in the same VPC and availability zone as the original subnet.

* When `VpcId` is not empty, the subnet ID passed in by using this parameter must belong to that VPC and be in the same availability zone as the original subnet.



**VpcId ** <span data-label="purple">string </span>`Optional` `Sample value: vpc-33gf6af3mgpvk1pz2ijlf****`

The ID of the target VPC.


* If you do not configure this parameter, the subnet is changed to another one within the same VPC.

* You can call [DescribeVpcs](https://docs.byteplus.com/en/docs/vpc/DescribeVpcs) to query available VPCs in the same region as the instance.



&nbsp;

<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters

Only the response parameters specific to this operation are listed below. For more information, refer to the [response structure](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response).



**NetworkInterfaceId ** <span data-label="purple">string </span>`Sample value: eni-3tiu4lmhwq4e8i4q****`

The ID of the new network interface.



&nbsp;

<span id=".6K-35rGC56S65L6L"></span>
## Sample request

```text
GET /?Action=ModifyInstanceVpcAttribute&Version=2020-04-01&InstanceId=i-ybuweywu4xk2c1x5****&SubnetId=subnet-33gf6b2rztdkw1pz2ijvq****&SecurityGroupIds.1=sg-33gf6al0psvsw1pz2ij8e****&VpcId=vpc-33gf6af3mgpvk1pz2ijlf**** HTTP/1.1
Host: ecs.cn-beijing.byteplusapi.com.cn
Region: cn-beijing
ServiceName: ecs
```


<span id=".6L-U5Zue56S65L6L"></span>
## Sample response

```json
{
    "ResponseMetadata": {
        "RequestId": "2021062415303301022514515207C4****",
        "Action": "ModifyInstanceVpcAttribute",
        "Version": "2020-04-01",
        "Service": "ecs",
        "Region": "cn-beijing"
    },
    "Result": {
        "NetworkInterfaceId": "eni-3tiu4lmhwq4e8i4q****"
    }
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error codes

The table below lists the business\-related error codes of the operation. For more information, refer to [Common error codes](https://docs.byteplus.com/en/docs/ecs/Public-error-codes).


|Status code |Error code |Error message |Description |
|---|---|---|---|
|400 |IdempotentParameterMismatch |The request uses the same client token as a previous, but non\-identical request. Do not reuse a client token with different requests, unless the requests are identical. |The idempotent parameters are inconsistent. |
|400 |Insufficient.Balance |The request is denied due to the lack of balance. |The account balance is insufficient. |
|400 |InvalidArgument |The specified argument is invalid. |The specified parameter is invalid. |
|400 |InvalidClientToken.Malformed |The specified ClientToken is malformed. |The specified ClientToken is invalid. |
|400 |InvalidInstanceStatus |The status of the specified instance does not support this request. |The current status of the instance does not support this operation. |
|400 |InvalidIp |The specified ip is not valid, is unsupported, or cannot be used. |The specified IP address is invalid. |
|400 |InvalidSecurityGroupType.Malformed |The specified SecurityGroupType is malformed. |The specified security group type is invalid. |
|400 |InvalidSubnet.VpcMismatch |The specified subnet is not in the specified VPC. |The specified subnet is not in the specified VPC. |
|400 |LimitExceeded.MaximumSubnetIps |The number of specified subnet IP addresses exceeds the maximum limit. |The specified number of subnet IP addresses reaches the maximum limit. |
|400 |MissingParameter.InstanceId |The required parameter InstanceId is not supplied. |The parameter InstanceId cannot be left empty. |
|400 |MissingParameter.SecurityGroupIds |The required parameter SecurityGroupIds is not supplied. |The security group ID cannot be empty. |
|400 |MissingParameter.SubnetId |The required parameter SubnetId is not supplied. |The subnet ID cannot be left empty. |
|400 |QuotaExceeded.MaximumSecurityGroupNetworkInterfaces |You've reached the limit on the number of SecurityGroupEnis that you can create, please submit ticket to request an increase in quota. |The quota for network interfaces that can be associated with the security group is insufficient. Please submit a ticket to request a quota increase. |
|400 |QuotaExceeded.MaximumSecurityGroups |You've reached the limit on the number of SecurityGroups that you can create, please submit ticket to request an increase in quota. |Security group quota is insufficient. Please submit a ticket to request a quota increase. |
|404 |InvalidInstance.EniNotFound |The specified instance ENI not found. |The specified instance network interface does not exist. |
|404 |InvalidInstance.NotFound |The specified instance does not exist. |The specified instance does not exist. |
|404 |InvalidSecurityGroup.NotFound |The specified SecurityGroup does not exist. |The specified security group does not exist. |
|404 |InvalidSubnet.NotFound |The specified subnet does not exist. |The specified subnet does not exist. |
|404 |InvalidVpc.NotFound |The specified VPC does not exist. |The specified VPC does not exist. |
|409 |InvalidPrimaryIpAddress.Conflict |The specified PrimaryIpAddress already exists. |The specified PrimaryIpAddress already exists. |
|409 |InvalidSecurityGroupId.Conflict |The specified security group is duplicated with another security group associated with the same elastic network interface. |The specified security group has already been associated with the network interface and cannot be associated again. |
|409 |InvalidSubnet.Conflict |The specified instance already in target subnet. |The specified instance is already in the target subnet. |
|412 |IdempotentProcessing |The request uses the same client token as a previous one that is still in process. |The previous idempotent request is still in process. Please try again later. |
|412 |InvalidInstance.DependenceAnycastEipExit |The specified instance has a dependency on anycast elastic ip. |The specified instance has a dependency on an anycast EIP. Therefore, the request cannot be processed. |
|412 |InvalidInstance.DependenceClbExit |The specified instance has a dependency on CLB. |The specified instance has a dependency on CLB. Therefore, the request cannot be processed. |
|412 |InvalidInstance.DependenceEipExit |The specified instance has a dependency on elastic ip address in binded mode. |The specified instance has a dependency on the EIP visibility mode. Therefore, the request cannot be processed. |
|412 |InvalidInstance.DependenceEniExist |The specified instance has a dependency on elastic network interface. |The specified instance has a dependency on the elastic network interface. Therefore, the request cannot be processed. |
|412 |InvalidInstance.DependenceHaVipExist |The specified instance has a dependency on HaVip. |The specified instance has a dependency on a High\-Availability Virtual IP Address. Therefore, the request cannot be processed. |
|412 |InvalidInstance.DependenceIpv6Exit |The specified instance has a dependency on IPv6 address. |The specified instance has a dependency on an IPv6 address. Therefore, the request cannot be processed. |
|412 |InvalidInstance.DependenceMultiPrivateIpExist |The specified instance has a dependency on multiple private IP addresses. |The specified instance has dependencies on multiple private IP addresses. Therefore, the request cannot be processed. |
|412 |InvalidInstance.DependenceRouteEntryExist |The specified instance has a dependency on custom route entry. |The specified instance has a dependency on the custom route entry. Therefore, the request cannot be processed. |
|412 |InvalidSecurityGroup.SubnetMismatch |The specified SecurityGroup and Subnet do not match. |The security group and the VPC of subnet do not match. |
|412 |InvalidSubnet.ZoneMismatch |The specified subnet and instance are in different Availability Zones. |The availability zone associated with the subnet is different from the one where the instance resides. |
|412 |OperationDenied.ResourceLocked |The specified operation is denied as your resource is locked for another operation. |The specified operation is rejected because your resource has been locked by another operation. |
|412 |OperationDenied.SpecifiedSecurityGroupNotAuthorized |You are not authorized to perform operations on the specified security group. The specified security group is a service\-managed security group. |As the specified security group is a service\-managed security group, the user has no permission to perform actions on the specified security group. |
|500 |InternalError |An internal error has occurred. |An internal error occurred. Try again. If multiple attempts fail, submit a ticket. |
