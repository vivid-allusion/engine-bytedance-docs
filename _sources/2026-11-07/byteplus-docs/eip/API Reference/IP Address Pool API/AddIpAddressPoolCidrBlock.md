---
title: "AddIpAddressPoolCidrBlock"
product: "Elastic IP Address"
product_code: "eip"
source: "https://docs.byteplus.com/en/docs/eip/AddIpAddressPoolCidrBlock"
---

Call the AddIpAddressPoolCidrBlock interface to add an IP address CIDR block to the specified IP address pool.

<span id=".6LCD55So6K-05piO"></span>
## Instructions


* Adding occupied IP address CIDR blocks is not supported.

* IP address pools that have been Suspended due to Overdue cannot add IP address segments.


<span id="JHBEB7ra"></span>
## Debug

[去调试](https://api.byteplus.com/api-explorer/?action=CreateIpAddressPool&data=%7B%7D&groupName=%E5%85%AC%E7%BD%91IP&query=%7B%7D&serviceCode=vpc&version=2020-04-01)


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request Parameters


|Parameter |Type |Required |Example Value |Description |
|---|---|---|---|---|
|Action |String |Yes |AddIpAddressPoolCidrBlock |The action that you want to perform. Value: **AddIpAddressPoolCidrBlock**. |
|Version |String |Yes |2020\-04\-01 |The version of the API request. The current version is 2020\-04\-01. |
|CidrBlock |String |No |101.0.XX.XX/24 |IP address CIDR block. Only IPv4 CIDR blocks are supported, and cannot start with 0. Mask value range: 23~30.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">Only supports configuration of <code>CidrBlock</code> or <code>CidrMask</code>, one of which must be selected.</div><br> |
|CidrMask |Integer |No |24 |IP address CIDR block mask, value range: 24~28. After entering the mask, the IP address CIDR block will be automatically allocated.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">Only one of <code>CidrBlock</code> or <code>CidrMask</code> is supported for configuration.</div><br> |
|IpAddressPoolId |String |Yes |ippool\-fda83op\*\*\*\* |ID of the IP address pool.<br><br>You can call the [DescribeIpAddressPools](https://docs.byteplus.com/en/docs/eip/DescribeIpAddressPools) interface to query the ID of the IP address pool. |
|ClientToken |String |No |123e4567\-e89b\-12d3\-a456\-42665544\*\*\*\* |The client token that is used to ensure the idempotence of the request. You can use the client to generate the token, but you must make sure that the token is unique among different requests. This prevents repeated operations due to multiple client retries when the call of the API operation times out or an internal server error occurs. Valid range:<br><br><br>* It cannot exceed 64 ASCII characters in length. |


<span id=".6L-U5Zue5pWw5o2u"></span>
## Response parameters


|Parameter |Type |Example Value |Description |
|---|---|---|---|
|RequestId |String |2021062415303314515207C4\*\*\*\* |ID of the request. |
|CidrBlock |String |101.0.XX.XX/24 |IP address CIDR block. |


<span id=".6K-35rGC56S65L6L"></span>
## Request examples

```Plain Text
GET /?Action=AddIpAddressPoolCidrBlock&Version=2020-04-01&CidrBlock=101.0.XX.XX/24&IpAddressPoolId=ippool-fda83op**** HTTP/1.1
Host: open.volcengineapi.com
Service: vpc
Region: cn-beijing
```


<span id=".6L-U5Zue56S65L6L"></span>
## Response Example

```JSON
{
    "ResponseMetadata": {
        "RequestId": "20210624153033015207C4****",
        "Action": "AddIpAddressPoolCidrBlock",
        "Version": "2020-04-01",
        "Service": "vpc",
        "Region": "cn-beijing"
    },
    "Result":{
         "RequestId": "20210624153033015207C4****",
         "CidrBlock": "101.0.XX.XX/24"
     }
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error codes

For common error codes, [refer to Common error codes](https://docs.byteplus.com/en/docs/eip/Public-error-codes).


|HTTP Code |Error Codes |Error Message |Description |
|---|---|---|---|
|400 |IdempotentParameterMismatch |Arguments on this idempotent request are inconsistent with arguments used in previous request(s). |The parameters in this idempotent request are inconsistent with those in the previous request. |
||InvalidCidr.Malformed |The specified cidr block is malformed. |The specified CIDR block is invalid. |
||InvalidIPPool.CidrBlockResourceNotEnoug |There is not enough CIDR block resource to create an IP address pool. |Insufficient CIDR block resource to create IP address pool. |
||InvalidIPPool.InvalidStatus |The specified IP address pool is not in the correct status for the request. |The status of the specified IP address pool cannot respond to the request. |
||InvalidIPPoolCidrBlock.Malformed |The specified CIDR block is malformed. The mask length must be greater than or equal to 23 and less than or equal to 30. |The specified CIDR block is invalid, and the CIDR block mask must be greater than or equal to 23 and less than or equal to 30. |
||InvalidIPPoolCidrBlock.NotSupportIPv6 |The IP address pool does not support IPv6 CIDR block. |The specified IP address pool does not support the specified IPv6 CIDR block. |
||InvalidIPPoolCidrMask.Malformed |The specified CIDR mask is malformed. The mask length must be greater than or equal to 24 and less than or equal to 28. |The specified mask is invalid. The mask must be greater than or equal to 24 and less than or equal to 28. |
||InvalidParameter |A parameter specified in the request is not valid, is unsupported, or cannot be used. |The request contains an invalid or unsupported parameter. |
||InvalidParameter.ClientTokenMalformed |The specified parameter ClientToken is malformed. |The specified client token is invalid and cannot exceed 64 ASCII characters in length. |
||QuotaExceeded.IPPoolIP |You've reached the limit on the number of IPs of all IP address pools that you can possess. |You have reached the maximum IP address count for all IP address pools. |
|404 |InvalidIPPool.NotFound |The specified IP address pool does not exist. |The specified IP address pool does not exist. |
|412 |IdempotentProcessing |The request uses the same client token as previous one that is still in process. |The idempotent request is being processing. |
