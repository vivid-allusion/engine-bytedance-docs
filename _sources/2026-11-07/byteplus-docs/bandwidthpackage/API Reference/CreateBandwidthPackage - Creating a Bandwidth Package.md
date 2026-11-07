---
title: "CreateBandwidthPackage - Creating a Bandwidth Package"
product: "Bandwidth Package"
product_code: "bandwidthpackage"
source: "https://docs.byteplus.com/en/docs/bandwidthpackage/CreateBandwidthPackage"
---

Call the CreateBandwidthPackage API to create a Bandwidth Package instance.

<span id=".5L2_55So6K-05piO"></span>
## Notes


* Ensure that the sum of both your [available balance](https://docs.byteplus.com/en/docs/6269/100429) and the coupons available for Bandwidth Package is not less than USD 100.00, and the available balance must be no less than 0. For specific procedure, see [Recharge guide](https://docs.byteplus.com/en/docs/6269/100434).

* You can create a maximum of 5 Bandwidth Packages in a single region under a single account.

* For other tag actions, see [TagResources](https://docs.byteplus.com/en/docs/vpc/TagResources), [UntagResources](https://docs.byteplus.com/en/docs/vpc/UntagResources), and [ListTagsForResources](https://docs.byteplus.com/en/docs/vpc/ListTagsForResources).


<span id=".6LCD6K-V"></span>
## Debug

[去调试](https://api.byteplus.com/api-explorer/debug?action=CreateBandwidthPackage&serviceCode=vpc&version=2020-04-01&groupName=)


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters



**Action ** <span data-label="purple">String </span><span data-api-tag="require|WJ0cQb">必选</span> `Example: CreateBandwidthPackage`

The action that you want to perform. Value: **CreateBandwidthPackage**.



**Version** <span data-label="purple">String</span> <span data-api-tag="require|oSMAx2">必选</span> `Example: 2020-04-01`

API version. The current version is **2020\-04\-01**.



**BandwidthPackageName ** <span data-label="purple">String </span>`optional` `Example: bwp-01`

Name of the Bandwidth Package.


* Must be 1 to 128 characters.

* Must start with a letter, Chinese character, or number. May include periods (.), underscores (_), and hyphens (\-).

* If left blank, it defaults to the Bandwidth Package ID.



**Description ** <span data-label="purple">String </span>`optional` `Example: This is a bandwidthpackage`

Description of the Bandwidth Package.


* Must be 0 to 255 characters.

* If left blank, this parameter defaults to an empty string.

* Must start with a letter, Chinese character, or number. May include commas (,), periods (.), underscores (_), spaces ( ), equal signs (=), hyphens (\-), full\-width commas (，), and full\-width periods (。).



**ISP ** <span data-label="purple">String </span>`optional` `Example: BGP`

Internet Service Provider (ISP). Default: BGP.


* BGP (Multi\-ISP).

* If your account has applied for and been enabled for static single\-ISP permission, you can specify the following values:

   * ChinaMobile: Static single\-ISP provided by China Mobile.

   * ChinaTelecom: Static single\-ISP provided by China Telecom.

   * ChinaUnicom: Static single\-ISP provided by China Unicom.

* If your account has applied for and been enabled for BGP single\-ISP permission, you can specify "SingleLine_BGP"

* If your account has applied for and been enabled for premium BGP permission, you can specify "Premium_BGP".

* If your account has applied for and been enabled for fusion BGP permission, you can specify "Fusion_BGP".

* If your account has applied for and been enabled for static preferential single\-ISP permission, you can specify the following values:

   * ChinaMobile_Value: The static preferential single\-ISP provided by China Mobile.

   * ChinaUnicom_Value: The static preferential single\-ISP provided by China Unicom.

   * ChinaTelecom_Value: The static preferential single\-ISP provided by China Telecom.



**BillingType ** <span data-label="purple">Integer </span>`optional` `Example: 4`

Metering method of the Bandwidth Package. Values:


* 1: Subscription.

* 2: Pay\-by\-bandwidth (default).

* 3: Pay\-by\-main\-traffic.

* 4: Pay\-by\-95th\-peak (Guaranteed ratio defaults to 20%).



**Protocol ** <span data-label="purple">String </span>`optional` `Example: IPv4`

IP protocol of the Bandwidth Package. Values:


* Dual\-stack: IPv4 and IPv6

* IPv4: Internet Protocol version 4

> Dual_stack is supported for this parameter only if `BillingType` is set to 2 or 4.



**Bandwidth** <span data-label="purple">Integer</span> <span data-api-tag="require|0C53t9">必选</span> `Example: 10`

The maximum bandwidth of the Bandwidth Package. Unit: Mbps.


* Set `BillingType` to 1: Value ranges from 5 to 5000.

* Set `BillingType` to 2: The value ranges from 2 to 5000.

* Set `BillingType` to 3: Value ranges from 2 to 2000.

* Set `BillingType` to 4: Value ranges from 2 to 5000.



**PeriodUnit** <span data-label="purple">Integer</span> `optional` `Example: 1`

The duration unit for Subscription Bandwidth Package. Values:


* 1: Month (default).

* 2: Year.



**Period** <span data-label="purple">Integer</span> `optional` `Example: 1`

The purchase duration for Subscription Bandwidth Package. Default: 1.


* When `PeriodUnit` is set to "1", the valid values of `Period` are 1–9, 12, 24, and 36.

* When `PeriodUnit` is set to "2", the valid values of `Period` are 1–3.



**SecurityProtectionTypes.N ** <span data-label="purple">String </span>`optional` `Example: AntiDDoS_Enhanced`

Protection type of the Bandwidth Package.


* N represents the sequence number of a protection type. Currently, only "1" is supported.

* Values:

   * AntiDDoS_Enhanced: Create a Bandwidth Package with enhanced protection, supporting adding EIPs with the enhanced protection type.

   * Leaving it blank means creating a Bandwidth Package with basic protection, supporting adding EIPs with the basic protection type.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">A Bandwidth Package only supports adding an EIP with the same protection type. The protection type cannot be converted after creation. Proceed with caution.</div>




**ProjectName ** <span data-label="purple">String </span>`optional` `Example: Project_1`

Name of the project to which the Bandwidth Package belongs. If left blank, this parameter defaults to the default project.



**Tags.N.Key** <span data-label="purple">String</span> `optional` `Example: key1`

The tag key of the custom tag.


* N represents the sequence number of a tag key. Valid values: 1–50.

* Separate multiple tag keys with ampersands (&).

* Must not start with `volc:` or `sys:` in any case form.

* Must be 1 to 128 characters. May include characters (any language), numbers, spaces ( ), underscores (_), periods (.), half\-width colons (:), slashes (/), equal signs (=), plus signs (+), hyphens (\-), and at signs (@).

* If a tag key contains leading or trailing spaces, the system will automatically delete them.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Duplicate tag keys are not allowed for the same resource.</div>




**Tags.N.Value ** <span data-label="purple">String </span>`optional` `Example: value1`

The tag value of the custom tag.


* N represents the sequence number of a tag value. Valid values: 1–50.

* Separate multiple tag values with ampersands (&).

* Must be 0 to 256 characters in length. If left blank, this parameter defaults to an empty string.

* The following characters are allowed: characters from all languages, numbers, spaces ( ), underscores (_), periods (.), colons (:), forward slashes (/), equal signs (=), plus signs (+), hyphens (\-), and the at symbol (@).

* Case\-sensitive.

* If a tag value starts or ends with spaces, the system will automatically delete them.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">To specify this parameter, first provide <code>TagFilters.N.Key</code>.</div>




&nbsp;

<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters



**RequestId ** <span data-label="purple">String </span>`Example: 2021062415303301022514515207C4****`

Request ID.



**BandwidthPackageId ** <span data-label="purple">String </span>`Example: bwp-2zeo05qre24nhrqpy****`

ID of the new Bandwidth Package instance.



&nbsp;

<span id=".6K-35rGC56S65L6L"></span>
## Request examples

```json
GET /?Action=CreateBandwidthPackage&Version=2020-04-01&BandwidthPackageName=bwp-01&ISP=BGP&Bandwidth=10 HTTP/1.1
Host: vpc.cn-beijing.byteplusapi.com.cn
Service: vpc
Region: cn-beijing
```


<span id=".6L-U5Zue56S65L6L"></span>
## Response examples

```json
{
    "ResponseMetadata": {
        "RequestId": "2021062415303301022514515207C4****",
        "Action": "CreateBandwidthPackage",
        "Version": "2020-04-01",
        "Service": "vpc",
        "Region": "cn-beijing"
    },
    "Result": {
        "RequestId": "2021062415303301022514515207C4****",
        "BandwidthPackageId": "bwp-2zeo05qre24nhrqpy****"
    }
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error codes

For more information, see [Common error codes](https://docs.byteplus.com/en/docs/bandwidthpackage/Public-error-codes).


|Status code |Error codes |Error message |Explanation |
|---|---|---|---|
|400 |DryRunOperation |Exception raised to indicate a successfully authorized action when the DryRun flag is set to true. |This request is set to DryRun. The action is authorized but not executed. |
|400 |InsufficientIspBandwidthPackage |The specified ISP does not contain enough free bandwidth package to fulfill your request. |The specified ISP does not have sufficient Bandwidth Package resources. |
|400 |InvalidBandwidth.Malformed |The specified bandwidth is malformed. Ensure that bandwidth is not smaller than the limit. |The specified bandwidth is invalid. Ensure the bandwidth is not less than the restriction. |
|400 |InvalidBillingType.Malformed |The specified billing type is malformed. |The specified billing method is invalid. |
|400 |InvalidDescription.Malformed |The specified description is malformed. Ensure the maximum length of description is 255. |The format of specified description is invalid. A description must not exceed 255 characters. |
|400 |InvalidDescription.Malformed |The specified description is malformed. |The format of specified description is invalid. Correct the description format and retry. |
|400 |InvalidDualStackSpecificEgress.Malformed |The specified bandwidth package with specific egress does not support dual\-stack. |The Bandwidth Package with a specified egress does not support enabling dual\-stack. |
|400 |InvalidISP.NotSupport |Dual\-stack bandwidth package does not support specified isp. |The dual\-stack Bandwidth Package does not support the specified ISP. |
|400 |InvalidMonthPeriod.Malformed |The specified monthly period is malformed. Monthly period only supports 1~9, 12, 24, 36. |The specified prepaid purchase duration in months is invalid. The valid prepaid purchase durations in months are 1 to 9, 12, 24, and 36. |
|400 |InvalidName.Malformed |The specified name is malformed. |The format of the specified name is invalid. Correct the name format and retry. |
|400 |InvalidName.Malformed |The specified name is malformed. Ensure the maximum length of name is 128. |The format of the specified name is invalid. A name must not exceed 128 characters. |
|400 |InvalidPeriodUnit.Malformed |The specified period unit is malformed. Pre billing period unit can only be Month or Year. |The specified unit for the subscription duration is invalid. The subscription duration unit must be Month or Year. |
|400 |InvalidProtocol.Malformed |The specified protocol is malformed. AntiDDoS enhanced bandwidth package only supports IPv4. |The specified protocol type is not supported. Bandwidth Packages with enhanced protection support only IPv4. |
|400 |InvalidProtocol.Malformed |The specified protocol is malformed. |The specified protocol type is invalid. |
|400 |InvalidRenewType.Malformed |The specified renew type is malformed. Renew type must be 1, 2, or 3. |The specified renewal type is invalid. The value for renewal type must be 1, 2, or 3. |
|400 |InvalidSecurityProtectionTypes.Malformed |The specified security protection type is malformed. Security protection type only support AntiDDoS_Enhanced. |The specified protection type is not supported. Currently, the protection type supports only AntiDDoS_Enhanced. |
|400 |InvalidTag.Disorder |The specified index order of tag is malformed. |The index order format of the specified tag is invalid |
|400 |InvalidTagKey.Malformed |The specified parameter tag key is invalid. |The tag key is invalid. |
|400 |InvalidTagValue.Malformed |The specified parameter tag value is invalid. |The tag value is invalid. |
|400 |InvalidYearPeriod.Malformed |The specified yearly period is malformed. Yearly period only supports 1~3. |The specified purchase duration in years is invalid. The valid values for purchase duration in years are 1 to 3. |
|400 |LimitExceeded.Bandwidth |You've reached the limit on the bandwidth that you can create. |The bandwidth cap has been reached. |
|400 |LimitExceeded.SecurityProtectionTypes |You've reached the limit on the number of security protection types. |You have reached the maximum of security protection types. |
|400 |LimitExceeded.Tags |You've reached the limit on the number of tags that you can operate at one time. |You have reached the maximum of tags that can be processed in a single request. |
|400 |MissingParameter |The request is missing a required parameter. |This request does not contain required parameters. |
|400 |OrderError |Failed to create an order in one step. |Failed to create and pay for the order. |
|400 |PreOrderError |Failed to create pre order. |The creation of the configuration order failed. |
|400 |QuotaExceeded.BandwidthPackage |You've reached the limit on the number of bandwidth package that you can create. |You have reached the maximum of Bandwidth Packages that you can create. |
|400 |QuotaExceeded.DualStackBandwidthPackage |You've reached the limit on the number of dual\-stack bandwidth package that you can create. |You have reached the maximum of dual\-stack Bandwidth Packages that you can create. |
|400 |QuotaExceeded.PremiumBGPBandwidthPackage |You've reached the limit on the number of premium BGP bandwidth package that you can create. |You have reached the maximum of Bandwidth Packages with premium BGP that you can create. |
|400 |UnsupportedOperation |The request on the specified instance is denied due to the account in arrears status. |The action request on this instance is denied because the account is in arrears. |
|400 |UnsupportedOperation |The request on the specified instance is denied due to the account balance and available vouchers are less than 100 yuan in total. |The action request on this instance is denied due to the sum of both account balance and available coupons being less than USD 100. |
|403 |Forbidden |The premium BGP line specific egress function is not support. |The feature of specified egress for premium BGP is not supported. |
|403 |Forbidden |You are not authorized to create BGP SingleLine elastic IP address. |No permission to create an EIP with the BGP single\-ISP. |
|403 |Forbidden |You are not authorized to create single\-line value elastic IP address. |No permission to create an EIP with static preferential single\-ISP. |
|403 |Forbidden |You are not authorized to use specific egress. |No permission to use the IP specified exit feature. |
|403 |Forbidden |You are not authorized to perform operations on create IPv6 gateway. |No permission to create an IPv6 gateway. |
|403 |Forbidden |You are not authorized to create Anti DDos bandwidth package. |No permission to create a Bandwidth Package with enhanced protection. |
|403 |Forbidden |You are not authorized to create premium BGP elastic IP address. |No permission to create an EIP with the premium BGP. |
|403 |Forbidden |You are not authorized to create fusion BGP elastic IP address. |No permission to create an EIP with fusion BGP. |
|403 |Forbidden |You are not authorized to create Static BGP elastic IP address. |No permission to create an EIP with the static BGP. |
|403 |Forbidden |You are not authorized to create single\-line elastic IP address. |No permission to create an EIP with static single\-ISP. |
|403 |Forbidden |You are not authorized to create bandwidth package. |No permission to create a Bandwidth Package. |
|403 |Forbidden.Ipv6IspType |You are not authorized to create this type IPv6 CIDR. |You do not have permission to create an IPv6 CIDR block for the specified ISP type. |
|404 |InvalidISP.NotFound |The specified ISP does not exist. |The specified ISP does not exist. |
|404 |InvalidProject.NotFound |The specified Project does not exist. |The specified project does not exist. |
|404 |InvalidSpecificEgress.NotFound |The specific egress does not exist. |The specified exit does not exist. |
|409 |InvalidOperation.Conflict |The specified resource operation conflicts. |The specified resource action conflicted. |
|500 |InternalError |An internal error has occurred. |An internal error occurred. |
