---
title: "CreateIpAddressPool"
product: "Elastic IP Address"
product_code: "eip"
source: "https://docs.byteplus.com/en/docs/eip/CreateIpAddressPool"
---

Call the CreateIpAddressPool API to create an IP address pool.

<span id=".6LCD6K-V"></span>
## Debug

[去调试](https://api.byteplus.com/api-explorer/?action=CreateIpAddressPool&data=%7B%7D&groupName=%E5%85%AC%E7%BD%91IP&query=%7B%7D&serviceCode=vpc&version=2020-04-01)


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameter


|Parameter name |Type |Required |Example value |Description |
|---|---|---|---|---|
|Action |String |Yes |CreateIpAddressPool |The action that you want to perform. Value: **CreateIpAddressPool**. |
|Version |String |Yes |2020\-04\-01 |The API version. The current version is 2020\-04\-01. |
|CidrBlock |String |No |101.0.XX.XX/24 |IP address CIDR block. Only support IPv4 CIDR block. Cannot start with 0. Mask range: 23 to 30.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">Only one of <code>CidrBlock</code> or <code>CidrMask</code> can be configured.</div><br> |
|CidrMask |Integer |No |24 |IP address subnet mask. Valid values: 24\-28. After typing the mask, the CIDR block will be allocated automatically.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">Only one of <code>CidrBlock</code> or <code>CidrMask</code> can be configured.</div><br> |
|ISP |String |Yes |BGP |Internet Service Provider (ISP). Values:<br><br><br>* BGP: BGP (Multi\-ISP).<br><br>* If your account has applied for and enabled permission for the static single\-ISP, you can pass in the following values:<br><br>   * ChinaMobile: China Mobile static single\-ISP.<br><br>   * ChinaTelecom: China Telecom static single\-ISP.<br><br>   * ChinaUnicom: China Unicom static single\-ISP.<br><br>* If your account has applied for and enabled permission for the BGP single\-ISP, you can pass in SingleLine_BGP.<br><br>* If your account has applied for and enabled permission for the premium BGP, you can pass in Premium_BGP.<br><br>* If your account has applied for and enabled permission for the fusion BGP, you can pass in Fusion_BGP.<br><br>* If your account has applied for and enabled permission for the static preferential single\-ISP, you can pass in the following values:<br><br>   * ChinaMobile_Value: The static preferential single\-ISP provided by China Mobile.<br><br>   * ChinaUnicom_Value: The static preferential single\-ISP provided by China Unicom.<br><br>   * ChinaTelecom_Value: The static preferential single\-ISP provided by China Telecom. |
|Name |String |No |IpAddressPool01 |Name of the IP address pool.<br><br><br>* Must be 1 to 128 characters.<br><br>* Must start with a letter, Chinese character, or number. Cannot start with "http://" or "https://.". May include letters, numbers, colons (:), underscores (_), and hyphens (\-).<br><br>* If left blank, the parameter defaults to an empty value. |
|Description |String |No |238q08230\*\*\* |Description of the IP address pool.<br><br><br>* Must be 1 to 255 characters.<br><br>* Must start with a letter, Chinese character, or number. Cannot start with "http://" or "https://.". May include English commas (,), periods (.), underscores (_), spaces ( ), equal signs (=), hyphens (\-), Chinese commas (，), and Chinese periods (。).<br><br>* If left blank, the parameter defaults to an empty value. |
|ProjectName |String |No |Project_1 |The name of the project to which the EIP belongs. If left blank, it defaults to the default project. |
|Tags.N.Key |String |No |Tags.1.Key=key1&Tags.2.Key=key2 |The tag key of the user tag.<br><br><br>* N specifies the serial number of a tag key. Valid values: 1–50.<br><br>* Separate multiple tag keys with ampersands (&).<br><br>* Cannot start with `volc:` or `sys:` in any case form.<br><br>* Must be 1 to 128 characters. May include characters in different languages, numbers, spaces ( ), underscores (_), periods (.), half\-width colons (:), slashes (/), equal signs (=), plus signs (+), hyphens (\-), and at signs (@).<br><br>* If a tag value starts or ends with a space, the system automatically deletes the space.<br><br><br>> Tag keys of the same resource must be unique. |
|Tags.N.Value |String |No |Tags.1.Value=value1&Tags.2.Value=value2 |The tag value of the user tag.<br><br><br>* N specifies the serial number of a tag value. Valid values: 1–50.<br><br>* Separate multiple tag values with ampersands (&).<br><br>* The length ranges from 0 to 256 characters. If left blank, it defaults to an empty value.<br><br>* May contain characters in different languages, numbers, spaces ( ), underscores (_), periods (.), half\-width colons (:), slashes (/), equal signs (=), plus signs (+), hyphens (\-), and at signs (@).<br><br>* Case\-sensitive.<br><br>* If a tag value starts or ends with a space, the system automatically deletes the space.<br><br><br>> To pass in this parameter, pass in `Tags.N.Key` first. |
|ClientToken |String |No |123e4567\-e89b\-12d3\-a456\-42665544\*\*\*\* |Ensure the request idempotency. You can use the client to automatically generate a token, but you must make sure that the token is unique among different requests. This prevents repeated actions due to multiple client retries when the call of the API action times out or an internal server error occurs. Values:<br><br><br>* Not more than 64 ASCII characters. |


<span id=".6L-U5Zue5pWw5o2u"></span>
## Response parameter


|Parameter name |Type |Example value |Description |
|---|---|---|---|
|RequestId |String |2021062415303314515207C4\*\*\*\* |The request ID |
|IpAddressPoolId |String |ippool\-fda83op\*\*\*\* |The ID of the IP address pool. |


<span id=".6K-35rGC56S65L6L"></span>
## Sample request

```Plain Text
GET /?Action=CreateIpAddressPool&Version=2020-04-01&CidrBlock=101.0.XX.XX/24&ISP=BGP HTTP/1.1
Host: open.volcengineapi.com
Service: vpc
Region: cn-beijing
```


<span id=".6L-U5Zue56S65L6L"></span>
## Response example

```Plain Text
{
    "ResponseMetadata": {
        "RequestId": "20210624153033015207C4****",
        "Action": "CreateIpAddressPool",
        "Version": "2020-04-01",
        "Service": "vpc",
        "Region": "cn-beijing"
    },
    "Result":{
         "RequestId": "2021062415303314515207C4****",
         "IpAddressPoolId": "ippool-fda83op****"
     }
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error code

For the common error code, see [Common error codes](https://docs.byteplus.com/en/docs/eip/Public-error-codes).


|HttpCode |Error code |Error message |Description |
|---|---|---|---|
|400 |IdempotentParameterMismatch |Arguments on this idempotent request are inconsistent with arguments used in previous request(s). |The parameters of this idempotent request are inconsistent with those used in the previous request. |
||InvalidCidr.Malformed |The specified cidr block is malformed. |The specified CIDR block is malformed. |
||InvalidDescription.Malformed |The specified description is malformed. |The specified description is malformed. Correct the description format and try again. |
||InvalidDescription.Malformed |The specified description is malformed. Ensure the maximum length of description is 255. |The specified description is malformed. The description cannot be more than 255 characters. |
||InvalidIPPool.CidrBlockResourceNotEnough |There is not enough CIDR block resource to create an IP address pool. |The available subnet resources are insufficient for creating the IP address pool. |
||InvalidIPPoolCidrBlock.Malformed |The specified CIDR block is malformed. The mask length must be greater than or equal to 23 and less than or equal to 30. |The specified CIDR block is invalid. The subnet mask must be between 23 and 30 inclusive. |
||InvalidIPPoolCidrBlock.NotSupportIPv6 |The IP address pool does not support IPv6 CIDR block. |The IP address pool does not support the specified IPv6 CIDR block. |
||InvalidIPPoolCidrMask.Malformed |The specified CIDR mask is malformed. The mask length must be greater than or equal to 24 and less than or equal to 28. |The specified mask is invalid. The mask must be between 24 and 28 inclusive. |
||InvalidName.Malformed |The specified name is malformed. |The specified name is malformed. Correct the name format and try again. |
||InvalidName.Malformed |The specified name is malformed. Ensure the maximum length of name is 128. |The specified name is malformed. The name cannot be more than 128 characters. |
||InvalidParameter |A parameter specified in the request is not valid, is unsupported or cannot be used. |The request contains invalid or unsupported parameters. |
||InvalidParameter.ClientTokenMalformed |The specified parameter ClientToken is malformed. |The specified CientToken is malformed. It cannot be more than 64 ASCII characters. |
||InvalidTag.Disorder |The specified index order of tag is malformed. |The index order of the specified tag is malformed. |
||InvalidTagKey.Malformed |The specified parameter tag key is invalid. |The tag key is invalid. |
||InvalidTagValue.Malformed |The specified parameter tag value is invalid. |The tag value is invalid. |
||LimitExceeded.Tags |You've reached the limit on the number of tags that you can operate at one time. |The maximum tags that you can operate in a single request have been reached. |
||QuotaExceeded.IPPool |You've reached the limit on the number of IP address pools that you can create. |The number of IP address pools exceeds the quota limit. |
||QuotaExceeded.IPPoolIP |You've reached the limit on the number of IPs of all IP address pools that you can possess. |The maximum IP addresses of all IP address pools have been reached. |
||UnsupportedOperation |The request on the specified instance is denied due to the account in arrears status. |The action request on this instance is rejected because the account is in arrears. |
||UnsupportedOperation |The request on the specified instance is denied due to the account balance and available vouchers are less than 100 yuan in total. |The action request on this instance is rejected because the sum of both account balance and available coupons are less than USD 100. |
|403 |Forbidden |You are not authorized to create BGP SingleLine elastic IP address. |No permission to create an EIP with the BGP single\-ISP. |
||Forbidden |You are not authorized to access the IP address pool. |No permission to access the IP address pool. |
||Forbidden |You are not authorized to create fusion BGP elastic IP address. |No permission to create an EIP with the fusion BGP. |
||Forbidden |You are not authorized to create Static BGP elastic IP address. |No permission to create an EIP with the static BGP.<br><br> |
||Forbidden |You are not authorized to create premium BGP elastic IP address. |No permission to create an EIP with the premium BGP. |
||Forbidden |You are not authorized to create single\-line value elastic IP address. |No permission to create an EIP with a static preferential single\-ISP. |
||Forbidden |You are not authorized to create single\-line elastic IP address. |No permission to create an EIP with the static single\-ISP. |
||Forbidden.PurchaseLimited |The account is not authorized to purchase the resource. |This account has no permission to purchase resources. |
|404<br><br> |InvalidIPPool.ISPNotFound |The specified ISP does not exist. |The specified ISP does not exist. |
||InvalidProject.NotFound |The specified Project does not exist. |The specified project does not exist. |
|409 |InvalidElasticIpPool.Allocated |Specified elastic ip pool has been allocated |The CIDR block of Eip pool is in use. |
|412 |IdempotentProcessing |The request uses the same client token as a previous one that is still in process. |The idempotent request is in process. |
