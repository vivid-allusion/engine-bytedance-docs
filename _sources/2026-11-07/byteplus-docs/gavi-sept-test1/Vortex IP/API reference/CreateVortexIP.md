---
title: "CreateVortexIP"
product: "Vortex IP"
product_code: "gavi-sept-test1"
source: "https://docs.byteplus.com/en/docs/gavi-sept-test1/CreateVortexIP"
---

Call CreateVortexIP to apply for a Vortex IP instance.

<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters


|Parameter name |Type |Required |Example |Description |
|---|---|---|---|---|
|Action |String |Yes |CreateVortexIP |The action that you want to perform. Value: CreateVortexIP. |
|Version |String |Yes |2020\-04\-01 |API version. The current version is 2020\-04\-01. |
|VortexName |String |No |VortexIP\-1 |Name of the Vortex IP instance.<br><br><br>* Must be 1 to 128 characters.<br><br>* Must start with a letter, Chinese character, or number. May include periods (.), underscores (_), and hyphens (\-).<br><br>* If left blank, the parameter defaults to the ID of Vortex IP. |
|Description |String |No |This is a VortexIP |Description of Vortex IP.<br><br><br>* Must be 0 to 255 characters.<br><br>* If left blank, this parameter defaults to an empty string.<br><br>* Must start with a letter, Chinese character, or number. May include commas (,), periods (.), underscores (_), spaces ( ), equal signs (=), hyphens (\-), full\-width commas (，), and full\-width periods (。). |
|Password |String |No |K29e!s0#57@%<br><br> |Authentication password of Vortex IP.<br><br><br>* Must be 12 to 30 characters.<br><br>* If left blank, the system will automatically fill a password.<br><br>* Cannot start with “/” or “$6$”. Must include at least three of the following four elements:<br><br>   * Uppercase letters (A\-Z);<br><br>   * Lowercase letters (a\-z);<br><br>   * Numbers (0\-9);<br><br>   * Symbols. |
|BillingType |Integer |Yes |3 |Billing method. Values:<br><br><br>* 3: Pay\-as\-you\-go. |
|AccessType |String |No |Private |Access mode of Vortex IP. Values:<br><br><br>* Public: Internet mode.<br><br>* Private (default): VPC mode.<br><br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">Vortex IP in Internet mode is currently in the beta stage. If you need a trial, please contact your account manager to apply.</div><br> |
|AutoRouteRules.N |String |No |youtube |Domain name of the Vortex IP smart routing.<br><br>You can call the [DescribeAutoRouteRules](https://docs.byteplus.com/en/docs/gavi-sept-test1/DescribeAutoRouteRules) API to query the collection of domains that support smart routing.<br><br><br>* N represents the sequence number of a smart route. Currently, only one valid value (1). |
|Bandwidth |Integer |No |10 |Maximum bandwidth of Vortex IP. Unit: Mbps. Valid range: 20 to 2000. |
|ServiceType |String |Yes |DataCenter |Service type of the Vortex IP. Values:<br><br><br>* DataCenter: Dynamic data center proxy.<br><br>* ResidentialQuarter: Dynamic residential proxy.<br><br>   > Vortex IPs with **Dynamic residential proxy** are limited to access certain websites. For more information, see [Limits](https://docs.byteplus.com/en/docs/gavi-sept-test1/Constraints#.5L2_55So6ZmQ5Yi2). |
|VpcId |String |No |vpc\-2feypfmenesqo59gp67yz\*\*\*\* |ID of the Virtual Private Cloud (VPC) where the Vortex IP is deployed. When AccessType is set to `Private`, this parameter is required.<br><br>You can call the [DescribeVpcs](https://docs.byteplus.com/en/docs/vpc/DescribeVpcs) API to query the VPC ID. |
|SubnetId |String |No |subnet\-2feypga30rgg059gp67ag\*\*\*\* |ID of the subnet where the Vortex IP is deployed. When AccessType is set to `Private`, this parameter is required.<br><br>You can call the [DescribeSubnets](https://docs.byteplus.com/en/docs/vpc/DescribeSubnets) API to query the subnet ID. |
|WhiteListEntries.N.Cidr |String |No |10.XX.XX.0/24 |Source address segment for allowlist entries must be CIDR blocks.<br><br><br>* N specifies the sequence number of an allowlist entry. Valid range: 1–20.<br><br>* Only support IPv4 entries.<br><br>* Separate multiple IP entries with ampersands (&).<br><br>* When the value of AccessType is `Private`, this parameter is required. |
|WhiteListEntries.N.Description |String |No |This is WhiteListEntries01 |Description of an allowlist entry.<br><br><br>* N specifies the sequence number of an allowlist entry. Valid range: 1–20.<br><br>* Separate multiple IP entries with ampersands (&). |
|Period |String |No |1<br><br> |The purchase duration of the Subscription Vortex IP instance. Unit: Month. Default: 1.<br><br>This parameter can be specified when BillingType is set to 1. |
|AutoRenewal |String |No |false |Specify whether to automatically renew the Subscription Vortex IP instance upon expiration. Values:<br><br><br>* true: Renew.<br><br>* false (default): Do not renew.<br><br><br>This parameter can be specified when BillingType is set to 1. |


<span id=".6L-U5Zue5pWw5o2u"></span>
## Response parameters


|Parameter name |Type |Example |Description |
|---|---|---|---|
|RequestId |String |2021062415303301022514515207C4\*\*\*\* |Request ID. |
|VortexId |String |vt\-bp1o94dp5i6ea\*\*\*\* |ID of a Vortex IP. |


<span id=".6K-35rGC56S65L6L"></span>
## Request examples

```Plain Text
GET /?Action=CreateVortexIP&Version=2020-04-01&VortexName=VortexIP-1&=BillingType=3&ServiceType=DataCenter&VpcId=vpc-2feypfmenesqo59gp67yz****&SubnetId=subnet-2feypga30rgg059gp67ag**** HTTP/1.1
Host: open.volcengineapi.com
Service: fasttrack
Region: ap-southeast-1
```


<span id=".6L-U5Zue56S65L6L"></span>
## Response examples

```Plain Text
{
    "ResponseMetadata": {
        "RequestId": "2021062415303301022514515207C4****",
        "Action": "CreateVortexIP",
        "Version": "2020-04-01",
        "Service": "fasttrack",
        "Region": "ap-southeast-1"
    },
    "Result":{
         "RequestId": "2021062415303301022514515207C4****",
         "VortexId": "vt-bp1o94dp5i6ea****"
     }
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error codes

For more information, see [Common error codes](https://docs.byteplus.com/en/docs/gavi-sept-test1/Public_error_codes).


|HttpCode |Error codes |Error message |Description |
|---|---|---|---|
|400 |AccountArrears |The request on the specified instance is denied due to the account in arrears status. |The action request on this instance is denied because the account is in arrears. |
|400 |BalanceNotEnough |The request on the specified instance is denied due to the account balance not enough. |The action request on this instance is rejected due to insufficient balance. |
|400 |CreatePreOrderError |Failed to create pre order. |The creation of the configuration order failed. |
|400 |InsufficientIpInSubnet |The specified subnet does not contain enough IP addresses. |Available IPs under the specified subnet are insufficient. |
|400 |InvalidAccessType.Malformed |The specified AccessType is malformed. |The format specified for AccessType is invalid. |
|400 |InvalidAutoRouteRule.Conflict |The auto route rules are duplicate. |The specified AutoRouteRules is duplicated. |
|400 |InvalidBandwidth.Malformed |The specified Bandwidth is malformed. |The format specified for Bandwidth is invalid. |
|400 |InvalidBillingType.Malformed |The specified BillingType is malformed. |The specified BillingType format is invalid. |
|400 |InvalidCIDR.Malformed |The specified CIDR is malformed. |The format specified for CIDR is invalid. |
|400 |InvalidCidr.Conflict |The specified Cidr are repeated. |The specified CIDR is duplicated. |
|400 |InvalidCidr.UnSupported |The specified Cidr is not supported. |The specified CIDR is not supported for the current action. |
|400 |InvalidDescription.Malformed |The specified Description is malformed. |The format specified for Description is invalid. |
|400 |InvalidPassword.Malformed |The specified Password is malformed. |The specified Password format is invalid. |
|400 |InvalidPeriod.Malformed |The specified Period is malformed. |The specified Period format is invalid. |
|400 |InvalidServiceType.Malformed |The specified ServiceType is malformed. |The format specified for ServiceType is invalid. |
|400 |InvalidSubnet.UnSupportAction |The specified subnet can not support this action. |The specified subnet does not support the current action. |
|400 |InvalidSubnetZone.UnSupportAction |The specified subnet zone can not support this action. |The current action is unsupported in the availability zone of the specified subnet. |
|400 |InvalidVortexName.Malformed |The specified VortexName is malformed. |The format specified for VortexName is invalid. |
|400 |InvalidVpc.InvalidStatus |The specified Vpc is not in the correct status for the request. |The specified VPC cannot respond to this request due to its status. |
|400 |LimitExceeded.WhiteListEntryNumber |You've reached the limit on the number of WhiteListEntries that you can operate. |You have reached the maximum resources that can be processed. |
|400 |MissingParameter |The request is missing a required parameter. Ensure that you have supplied all the required parameters for the request; for example, the 'VpcId'. |This request is missing a required parameter. Confirm that this request contains all required parameters (such as VpcId). |
|400 |MissingParameter |The request is missing a required parameter. Ensure that you have supplied all the required parameters for the request; for example, the 'SubnetId'. |This request is missing a required parameter. Confirm that this request contains all required parameters (such as SubnetId). |
|400 |OrderError.OrderPay |Failed to create order and pay. |The order payment failed. |
|403 |Forbidden |You are not authorized to perform operations on the specified zone. |No permission to perform actions in this availability zone. |
|403 |Forbidden |You are not authorized to perform operations on the specified service. |You do not have permission to perform operations on the specified service. |
|404 |InvalidSubnet.NotFound |The specified Subnet does not exist. |The specified subnet does not exist. |
|404 |InvalidVPC.NotFound |The specified VPC does not exist. |The specified VPC does not exist. |
