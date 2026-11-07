---
title: "DisassociateEipAddress"
product: "Elastic IP Address"
product_code: "eip"
source: "https://docs.byteplus.com/en/docs/eip/DisassociateEipAddress"
---

Call the DisassociateEipAddress operation to disassociate an elastic IP address (EIP) from a cloud resource.

<span id=".6LCD55So6K-05piO"></span>
## Instructions

Internet Cloud Load Balancer (CLB) instances do not support EIP disassociation. If you want to disassociate an Internet CLB instance from an EIP, you must call the [ModifyLoadBalancerAttributes](https://docs.byteplus.com/en/docs/clb/ModifyLoadBalancerAttributes) operation to convert the Internet CLB instance to a private CLB instance first.

<span id=".6LCD6K-V"></span>
## Debugging

[去调试](https://api.byteplus.com/api-explorer/?action=DisassociateEipAddress&data=%7B%7D&groupName=%E5%85%AC%E7%BD%91IP&query=%7B%7D&serviceCode=vpc&version=2020-04-01)


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request Parameters


|Parameter Name |Type  |Required |Example Value |Description |
|---|---|---|---|---|
|Action |String |Yes   |DisassociateEipAddress |The action that you want to perform. Value: DisassociateEipAddress. |
|Version |String |Yes   |2020\-04\-01 |The version of the API request. The current version is 2020\-04\-01. |
|AllocationId |String |Yes   |eip\-2ze7ujxscd\*\*\*\* |The ID of the EIP that you want to disassociate.<br><br>You can call the [DescribeEipAddresses](https://docs.byteplus.com/en/docs/eip/DescribeEipAddressAttributes) action to query the ID of an EIP. |
|InstanceType<br><br> |String<br><br> |Yes  <br><br> |EcsInstance<br><br> |The instance type of Elastic IP (EIP) to disassociate.<br><br><br>* NAT: NAT gateway.<br><br>* NetworkInterface: secondary network interface.<br><br>* ClbInstance: Cloud Load Balancer.<br><br>* EcsInstance: Elastic Compute Service (ECS).<br><br>* HAVIP: HAVIP.<br><br>* IpAddress: The private IP address.<br><br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">The EIP associated IP address feature is in beta. If you want to trial, please contact the customer manager.</div><br> |
|InstanceId |String |No |i\-2zebbhyczzaweeval\*\*\*\* |The ID of the cloud resource from which you want to disassociate the EIP. Pass in the ID of the cloud resource of the corresponding `Type` according to the parameters passed in. |
|ClientToken |String |No  |123e4567\-e89b\-12d3\-a456\-42665544\*\*\*\* |The client token that is used to ensure the idempotence of the request. You can use the client to generate the token, but you must make sure that the token is unique among different requests. This prevents repeated operations due to multiple client retries when the call of the API operation times out or an internal server error occurs. Valid range:<br><br><br>* It cannot exceed 64 ASCII characters in length. |


<span id=".6L-U5Zue5pWw5o2u"></span>
## **Response parameters**


|Parameter Name |Type  |Example Value |Description |
|---|---|---|---|
|RequestId |String |2021062415303301022514515207C4\*\*\*\* |ID of the request. |


<span id=".6K-35rGC56S65L6L"></span>
## Request Examples

```Plain Text
GET /?Action=DisassociateEipAddress&Version=2020-04-01&AllocationId=eip-2ze7ujxscd****&InstanceType=EcsInstance HTTP/1.1
Host: open.volcengineapi.com
Service: vpc
Region: cn-beijing
```


<span id=".6L-U5Zue56S65L6L"></span>
## Response Example

```Plain Text
{
    "ResponseMetadata": {
        "RequestId": "2021062415303301022514515207C4****",
        "Action": "DisassociateEipAddress",
        "Version": "2020-04-01",
        "Service": "vpc",
        "Region": "cn-beijing"
    },
    "Result":{
        "RequestId": "2021062415303301022514515207C4****"
    }
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error Codes

For more information on common error codes, refer to [Common error codes](https://docs.byteplus.com/en/docs/eip/Public-error-codes).


|HTTP Code |Error Codes |\*\*Error Message\*\* |Description |
|---|---|---|---|
|400 |IdempotentParameterMismatch |Arguments on this idempotent request are inconsistent with arguments used in previous request(s). |The parameters in this idempotent request are inconsistent with those in the previous request. |
|400 |InvalidEip.InstanceMismatch |The specified elastic ip and instance mismatch. |The specified EIP and instance do not match. |
|400 |InvalidEip.InvalidStatus |The specified elastic ip address is not in the correct status for the request. |The system cannot respond to the request due to the status of the specified EIP. |
|400 |InvalidNatGateway.InvalidStatus |The operation is not supported by the current nat gateway. |The system cannot respond to the request due to the status of the specified NAT gateway. |
|400 |InvalidNatGateway.UnSupportAction |The specified NAT gateway does not support this action. |The specified NAT gateway does not support this operation. |
|400 |IncorrectNatGatewayStatus |The operation is not supported by the current nat gateway. |This operation is not supported. Try again later. |
|400 |InvalidParameter.ClientTokenMalformed |The specified parameter ClientToken is malformed. |The specified client token is invalid and cannot exceed 64 ASCII characters in length. |
|403 |Forbidden |You are not authorized to perform operations on the specified elastic network interface. The specified elastic network interface is a service\-managed elastic network interface. |You are not authorized to perform operations on the specified ENI. The elastic network interface is the elastic network interface managed by the cloud product. |
|403 |Forbidden |You are not authorized to perform operations on the specified elastic ip and public CLB. |You do not have permissions to operate the EIP and public Cloud Load Balancer (CLB) instance. |
|403 |Forbidden |You are not authorized to disassociate elastic ip from Nat gateway. |You do not have permissions to disassociate the EIP from the NAT gateway. |
|403 |Forbidden |You are not authorized to perform operations on the specified elastic ip and private CLB. |You do not have permissions to operate the EIP and private CLB instance. |
|403 |Forbidden |You are not authorized to perform operations on the specified elastic ip and ALB. |You do not have permissions to operate the EIP and Application Load Balancer (ALB) instance. |
|404 |InvalidEip.NotFound |The specified EIP does not exist. |The specified EIP does not exist. |
|404 |InvalidInstance.NotFound |The specified instance does not exist. |The specified instance does not exist. |
|404 |InvalidNatBindEip.NotFound |The specified eip bound with nat does not exist. |The specified EIP associated with NAT does not exist. |
|404 |InvalidNatGateway.NotFound |The specified NAT gateway does not exist. |The specified NAT gateway does not exist. |
|412 |IdempotentProcessing |The request uses the same client token as a previous one that is still in process. |The request uses the same client token as a previous one that is still in process. |
