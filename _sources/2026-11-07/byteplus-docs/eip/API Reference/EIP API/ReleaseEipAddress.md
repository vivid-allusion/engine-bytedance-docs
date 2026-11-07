---
title: "ReleaseEipAddress"
product: "Elastic IP Address"
product_code: "eip"
source: "https://docs.byteplus.com/en/docs/eip/ReleaseEipAddress"
---

Call the ReleaseEipAddress API to release a specified elastic IP address (EIP).

<span id=".6LCD55So6K-05piO"></span>
## Instructions

To release an EIP using this API, the following conditions must be met:


* The EIP uses the billing method of Pay\-as\-you\-go, or the Subscription EIP has expired. This API cannot release Subscription EIPs before expiration. To release, see the [Unsubscription](https://docs.byteplus.com/en/docs/eip/Unsubscription).

* The EIP is not associated with any cloud resource.

   You can call [DescribeEipAddressAttributes](https://docs.byteplus.com/en/docs/eip/DescribeEipAddresses) to check if it is associated with any cloud resource. If associated, call the [DisassociateEipAddress](https://docs.byteplus.com/en/docs/eip/DisassociateEipAddress) API to disassociate it.

* The EIP is not added to any Bandwidth Package.

   You can call [DescribeEipAddressAttributes](https://docs.byteplus.com/en/docs/eip/DescribeEipAddresses) to check if it is added to any Bandwidth Package. If added, call the [RemoveBandwidthPackageIp](https://docs.byteplus.com/en/docs/bandwidthpackage/RemoveBandwidthPackageIp) API to remove it from the Bandwidth Package.


<span id=".6LCD6K-V"></span>
## Debug

[去调试](https://api.byteplus.com/api-explorer/?action=ReleaseEipAddress&data=%7B%7D&groupName=%E5%85%AC%E7%BD%91IP&query=%7B%7D&serviceCode=vpc&version=2020-04-01)


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameter


|Parameter name |Type |Required |Example value |Description |
|---|---|---|---|---|
|Action |String |Yes |ReleaseEipAddress |The action that you want to perform. Value: ReleaseEipAddress. |
|Version |String |Yes |2020\-04\-01 |The API version. The current version is 2020\-04\-01. |
|AllocationId |String |Yes |eip\-2zewb7ujxscd\*\*\*\* |The ID of the EIP to be released.<br><br>You can call [DescribeEipAddresses](https://docs.byteplus.com/en/docs/eip/DescribeEipAddressAttributes) to query the EIP ID. |
|ClientToken |String |No |123e4567\-e89b\-12d3\-a456\-42665544\*\*\*\* |Ensure the request idempotency. You can use the client to automatically generate a token, but you must make sure that the token is unique among different requests. This prevents repeated actions due to multiple client retries when the call of the API action times out or an internal server error occurs. Values:<br><br><br>* Not more than 64 ASCII characters. |


<span id=".6L-U5Zue5pWw5o2u"></span>
## Response parameter


|Parameter name |Type |Example value |Description |
|---|---|---|---|
|RequestId |String |2021062415303301022514515207C4\*\*\*\* |The request ID |


<span id=".6K-35rGC56S65L6L"></span>
## Sample request

```Plain Text
GET /?Action=ReleaseEipAddress&Version=2020-04-01&AllocationId=eip-2zewb7ujxscd**** HTTP/1.1
Host: open.volcengineapi.com
Service: vpc
Region: cn-beijing
```


<span id=".6L-U5Zue56S65L6L"></span>
## Response example

```Plain Text
{
    "ResponseMetadata": {
        "RequestId": "2021062415303301022514515207C4****",
        "Action": "ReleaseEipAddress",
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
## Error code

For the common error code, see [Common error codes](https://docs.byteplus.com/en/docs/eip/Public-error-codes).


|HttpCode |Error code |Error message |Description |
|---|---|---|---|
|400 |IdempotentParameterMismatch |Arguments on this idempotent request are inconsistent with arguments used in previous request(s). |The parameters of this idempotent request are inconsistent with those used in the previous request. |
|400 |InvaildIpv6.NotSupport |The specified IPv6 address does not support this operation. |The specified IPv6 address does not support this action. |
|400 |InvalidBillingType.Malformed |The specified billing type is malformed. |The specified metering method is invalid. |
|400 |InvalidEip.InTemporaryUpgrade |The specified eip is in temporary upgrade. |The specified EIP is undergoing a temporary upgrade. |
|400 |InvalidEip.InUse |The specified elastic ip is in use. |The specified EIP is in use. |
|400 |InvalidEip.InUse |The specified EIP is being operated by another request. |The specified EIP is being operated by another request. Try again later. |
|400 |InvalidEip.InUse |The specified EIP has dependent resource of a bandwidth package. |The specified EIP has been added to a Bandwidth Package and cannot be released. |
|400 |InvalidEipOrNat.InvalidStatus |The specified elastic ip or Nat is not in the correct status for the request. |The specified EIP or NAT gateway is in a status that cannot respond to this request. |
|400 |InvalidEip.InvalidStatus |The specified elastic ip is not in the correct status for the request. |The specified EIP is in a status that cannot respond to this request. |
|400 |InvalidIPPool.InvalidStatus |The specified IP address pool is not in the correct status for the request. |The specified IP address pool is in a status that cannot respond to this request. |
|400 |InvalidNatGateway.InvalidStatus |The specified NAT gateway is not in the correct status for the request. |The specified NAT gateway is in a status that cannot respond to this request. |
|400 |InvalidNatGateway.UnSupportAction |The specified NAT gateway does not support this action. |The specified NAT gateway does not support the current actions. |
|400 |InvalidParameter.ClientTokenMalformed |The specified parameter ClientToken is malformed. |The specified CientToken is malformed. It cannot be more than 64 ASCII characters. |
|400 |PreOrderError |Failed to create preorder. |Failed to create a configuration order. |
|403 |Forbidden |You are not authorized to perform operations on the specified elastic ip and public CLB. |No permission to operate this EIP and the public Classic Load Balancer (CLB). |
|403 |Forbidden |You are not authorized to disassociate elastic ip from Nat gateway. |No permission to disassociate the EIP from the NAT gateway. |
|403 |Forbidden |You are not authorized to perform operations on the specified elastic ip and ALB. |No permission to operate this EIP and the Application Load Balancer (ALB). |
|400 |QuotaExceeded.PremiumBGPEip |Premium BGP EIP number exceeded quota. |The maximum premium BGP EIPs that you can apply for have been reached. |
|403 |Forbidden |You are not authorized to perform operations on the specified elastic ip and private CLB. |No permission to operate this EIP and the private CLB. |
|403 |Forbidden |You are not authorized to perform operations on the specified elastic network interface. The specified elastic network interface is a service\-managed elastic network interface. |No permission to perform actions on the specified elastic network interface. The specified elastic network interface is managed by a cloud product. |
|404 |InvalidIPPool.NotFound |The specified IP address pool does not exist. |The specified IP address pool does not exist. |
|404 |InvalidInstance.NotFound |The specified instance does not exist. |The specified instance does not exist. |
|404 |InvalidEip.GetInstanceDetail |Get instance detail failed |Failed to retrieve instance information |
|404 |InvalidEip.NotFound |The specified EIP does not exist. |The specified EIP does not exist. |
|404 |InvalidNatBindEip.NotFound |The specified eip bound with nat does not exist. |The specified EIP that is associated with the NAT does not exist. |
|404 |InvalidNatGateway.NotFound |The specified NAT gateway does not exist. |The specified NAT Gateway does not exist. |
|412 |IdempotentProcessing |The request uses the same client token as a previous one that is still in process. |The idempotent request is in process. |
