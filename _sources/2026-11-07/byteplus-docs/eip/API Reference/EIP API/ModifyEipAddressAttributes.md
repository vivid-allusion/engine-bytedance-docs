---
title: "ModifyEipAddressAttributes"
product: "Elastic IP Address"
product_code: "eip"
source: "https://docs.byteplus.com/en/docs/eip/ModifyEipAddressAttributes"
---

Call the ModifyEipAddressAttributes operation to change the name, description, and maximum bandwidth of an Elastic IP Address (EIP).

<span id=".6LCD55So6K-05piO"></span>
## Instructions


* Reducing the maximum bandwidth may affect business traffic and cause packet loss. Please fully assess the potential impact on business and proceed with caution.

* If you do not specify the following optional parameters, leave them empty.


<span id=".6LCD6K-V"></span>
## Debugging

[去调试](https://api.byteplus.com/api-explorer/?action=ModifyEipAddressAttributes&data=%7B%7D&groupName=%E5%85%AC%E7%BD%91IP&query=%7B%7D&serviceCode=vpc&version=2020-04-01)


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request Parameters


|Parameter Name |Type |Required |Example Value |Description |
|---|---|---|---|---|
|Action |String |Yes |ModifyEipAddressAttributes |The action that you want to perform. Value: ModifyEipAddressAttributes. |
|Version |String |Yes |2020\-04\-01 |The version of the API request. The current version is 2020\-04\-01. |
|AllocationId |String |Yes |eip\-2zb7u8xscd\*\*\*\* |ID of an EIP.<br><br>You can call the [DescribeEipAddresses](https://docs.byteplus.com/en/docs/eip/DescribeEipAddressAttributes) action to query the ID of an EIP. |
|Name |String |No |eip\-1 |The name of the EIP.<br><br><br>* The length limit is 1 to 128 characters.<br><br>* The name starts with a letter, Chinese character or number, and can contain periods ( . ), underscores ( _ ), and hyphens ( \- ). |
|DirectMode |Boolean |No |false |Whether to enable bypass mode when associating the EIP. Valid value:<br><br><br>* false (default): Do not use bypass mode.<br><br>* true: Use bypass mode.<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">The EIP directly\-connect feature is currently in Beta. If you need a trial, please contact your account manager to apply.</div><br> |
|Description |String |No |This is an eip |The description of the EIP.<br><br><br>* The description can be 0 to 255 characters in length.<br><br>* Must begin with a letter, Chinese character, or number. It can include English commas (,), periods (.), underscores (_), spaces ( ), equal signs (=), hyphens (\-), chinese commas (，), and Chinese periods (。). |
|Bandwidth |Integer |No |10 |Select the maximum bandwidth for the EIP, in Mbps.<br><br><br>* Pay\-by\-data\-transfer: Value range 1 ~ 200.<br><br>* Pay\-by\-bandwidth: Value range 1 ~ 1000.<br><br>* Subscription billing: Value range 1 ~ 1000. |


<span id=".6L-U5Zue5pWw5o2u"></span>
## Response parameters


|Parameter Name |Type |Example Value |Description |
|---|---|---|---|
|RequestId |String |2021062415303301022514515207C4\*\*\*\* |ID of the request. |


<span id=".6K-35rGC56S65L6L"></span>
## Request Examples

```Plain Text
GET /?Action=ModifyEipAddressAttributes&Version=2020-04-01&AllocationId=eip-2zb7uj8xscd****&Bandwidth=10 HTTP/1.1
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
        "Action": "ModifyEipAddressAttributes",
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


|HTTP Code |Error Codes |Error Message |Description |
|---|---|---|---|
|400 |DryRunOperation |Exception raised to indicate a successfully authorized action when the DryRun flag is set to true. |Exception raised to indicate a successfully authorized action when the DryRun flag is set to true. |
||InvaildIpv6.NotSupport |The specified IPv6 address does not support this operation. |The specified IPv6 address does not support this operation. |
||InvalidBandwidth.Malformed |The specified bandwidth is malformed. Ensure that bandwidth is not smaller than 1. |The specified bandwidth is malformed. Ensure that bandwidth is not smaller than 1. |
||InvalidBandwidth.Malformed<br><br> |The specified bandwidth is malformed. During the temporary upgrade period, the bandwidth can only be greater。 |The specified bandwidth is invalid. During Temporary Modify Instance Spec, only increasing bandwidth is allowed. |
||InvalidDescription.Malformed |The specified description is malformed. Ensure the maximum length of description is 255. |The specified description is invalid. Ensure the maximum length of description is 255. |
||InvalidDescription.Malformed |The specified description is malformed. |The specified description is malformed. Please correct the description format and retry. |
||InvalidDirectModeEip.EIPInBindedMode |EIP in binded mode can not be modified to direct mode. |IP addresses in BINDED mode cannot be changed to direct mode. |
||InvalidDirectModeEip.IPv4GatewayEnabled |EIP not allowed to open direct mode when VPC has enabled IPv4 gateway. |Enabled IPv4 gateway for VPC, Enabled passthrough mode for EIP. |
||InvalidDirectModeEip.InstanceMismatch |The specified instance type does not support direct mode EIP. |The specified instance Type does not support pass\-through EIP. |
||InvalidDirectModeEip.InvalidBindInstanceType |Only elastic network interface bound to ECS support associating direct mode EIP. |Only the elastic network interface associated with ECS supports associating direct EIP. |
||InvalidDirectModeEip.InvalidStatus |Only attached EIP support modifying direct mode. |Only EIPs in the associated status support modifying the direct connection mode. |
||InvalidEip.InUse |The specified EIP is being operated by another request. |The specified EIP is being operated by another request. Please try again later. |
||InvalidEip.InvalidStatus |The specified elastic ip is not in the correct status for the request. The specified elastic ip is in freeze. |The specified EIP or Virtual Private Cloud (VPC) status cannot respond to this request. The current EIP is frozen. |
||InvalidEip.InvalidStatus |The specified elastic ip is not in the correct status for the request. |The system cannot respond to the request due to the status of the specified EIP. |
||InvalidEip.NotSupported |The specified elastic IP does not support temporary upgrade. |The specified EIP does not support Temporary Modify Instance Spec.<br><br> |
||InvalidEni.InvalidStatus |The specified elastic network interface is not in the correct status for the request. |The specified elastic network interface is not in the correct status for the request. |
||InvalidModeEip.DirectMode |EIP not allowed to open direct mode. |EIP Could Not Enable Passthrough Mode. |
||InvalidName.Malformed |The specified name is malformed. Ensure the maximum length of name is 128. |The specified name is malformed. Ensure the maximum length of name is 128. |
||InvalidName.Malformed |The specified name is malformed. |The specified name is malformed. Please correct the name format and retry. |
||InvalidOperation.InvalidBindInstanceType |Only EIPs bound to ECS support releasing with instances. |The EIP release with instance feature only takes effect for Associated ECS instances. |
||InvalidOperation.InvalidEipBillingType |Only postpaid EIPs support releasing with instances. |Only pay\-per\-use EIP supports the release\-on\-instance feature. |
||InvalidVpc.InvalidStatus |The specified VPC is not in the correct status for the request. |The VPC in the current state cannot respond to the request. |
||LimitExceeded.BandwidthPerEip |You've reached the limit on the bandwidth of elastic ip that you can create. |The bandwidth of the EIP has reached the upper limit. |
||OrderError |Failed to create an order in one step. |Failed to create and pay for the order. |
||PreOrderError |Failed to create pre order. |Failed to create pre order. |
||UnsupportedOperation |The request on the specified instance is denied due to the account balance and available vouchers are less than 100 yuan in total. |The request to operate on this instance is rejected because the account balance and available coupons are less than USD100. |
||UnsupportedOperation |The request on the specified instance is denied due to the account in arrears status. |The instance operation request is denied because the account is in arrears. |
|403 |Forbidden |You are not authorized to associate direct mode EIP with ECS. |No permission to associate a direct\-connected EIP to the ECS. |
||Forbidden |You are not authorized to perform operations on the specified EIP. The specified EIP is a service\-managed EIP. |No permission to perform actions on the specified EIP. The specified EIP is the Cloud Product Entrusted EIP. |
||Forbidden.PurchaseLimited |The account is not authorized to purchase the resource. |You do not have permissions to purchase resources with the account. |
|404 |InvalidEip.GetInstanceDetail |Get instance detail failed. |Failed to obtain the instance information. |
||InvalidEip.NotFound |The specified EIP does not exist. |The specified EIP does not exist. |
