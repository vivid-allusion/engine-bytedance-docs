---
title: "AllocateEipAddress - Applying for an EIP"
product: "Elastic IP Address"
product_code: "eip"
source: "https://docs.byteplus.com/en/docs/eip/AllocateEipAddress"
---

Call the AllocateEipAddress API to apply for an Elastic IP Address (EIP).

<span id=".5L2_55So6K-05piO"></span>
## Instructions

<span id=".I-WJjeaPkOadoeS7tg=="></span>
#### Prerequisites


* You have registered a BytePlus account and completed real\-name authentication.

* The total value of your account's [available balance](https://docs.byteplus.com/en/docs/6269/100429) and vouchers applicable to the EIP is not less than USD 100.00, and the available balance must be no less than 0. For details, see [Recharge guide](https://docs.byteplus.com/en/docs/6269/100434).


<span id=".I-S9v-eUqOmZkOWItg=="></span>
#### Limits


* By default, you can create a maximum of 20 EIPs in a single region under a single account. If the default quota does not meet your needs, go to the [Quota Center](https://console.byteplus.com/quota/productList/coParameterList?ProviderCode=EIP) to request a quota increase.

* The maximum daily calls to this API per account per region are twice the number of EIPs that you can apply for.

* For other tag actions, see [TagResources](https://docs.byteplus.com/en/docs/vpc/TagResources), [UntagResources](https://docs.byteplus.com/en/docs/vpc/UntagResources), and [ListTagsForResources](https://docs.byteplus.com/en/docs/vpc/ListTagsForResources).


<span id=".6LCD6K-V"></span>
## Debug

[去调试](https://api.byteplus.com/api-explorer/debug?action=AllocateEipAddress&serviceCode=vpc&version=2020-04-01&groupName=)


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters

The following only details request parameters specific to this API and key common parameters. For more information, see [Common parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).



**Action ** <span data-label="purple">String </span><span data-api-tag="require|R7Otwk">必选</span> `Example: AllocateEipAddress`

Operation to perform: **AllocateEipAddress**.



**Version ** <span data-label="purple">String </span><span data-api-tag="require|qjyHqk">必选</span> `Example: 2020-04-01`

The API version. The current version is **2020\-04\-01**.



**Name ** <span data-label="purple">String </span>`optional` `Example: eip-1`

The name of the EIP.


* Must be 1 to 128 characters.

* Must start with a letter, Chinese character, or number. May include periods (.), underscores (_), and hyphens (\-).

* If left blank, it defaults to the EIP ID.



**Description ** <span data-label="purple">String </span>`optional` `Example: This is an eip`

The description of the EIP.


* The length limit is 0 to 255 characters.

* If left blank, this parameter defaults to an empty string.

* Must start with a letter, Chinese character, or number. May include commas (,), periods (.), underscores (_), spaces ( ), equal signs (=), hyphens (\-), Chinese commas (，), and Chinese periods (。).



**ISP ** <span data-label="purple">String </span>`optional` `Example: BGP`

Internet Service Provider (ISP). Default: BGP.


* BGP: BGP (Multi\-ISP).

* If your account has applied for and enabled permission for the static single\-ISP, you can pass in the following values:

   * ChinaMobile: China Mobile static single\-ISP.

   * ChinaTelecom: China Telecom static single\-ISP.

   * ChinaUnicom: China Unicom static single\-ISP.

* If your account has applied for and enabled permission for the BGP single\-ISP, you can pass in SingleLine_BGP.

* If your account has applied for and enabled permission for the premium BGP, you can pass in Premium_BGP.

* If your account has applied for and enabled permission for the fusion BGP, you can pass in Fusion_BGP.

* If your account has applied for and enabled permission for the static preferential single\-ISP, you can pass in the following values:

   * ChinaMobile_Value: The static preferential single\-ISP provided by China Mobile.

   * ChinaUnicom_Value: The static preferential single\-ISP provided by China Unicom.

   * ChinaTelecom_Value: The static preferential single\-ISP provided by China Telecom.



**IpAddress ** <span data-label="purple">String </span>`optional` `Example: 12.XX.XX.89`

Apply for the specified EIP. Only supports specifying IP addresses released after use. Leaving it blank means automatic allocation.



**BillingType ** <span data-label="purple">Integer </span>`optional` `Example: 2`

The billing method of the EIP. Valid values:


* 1: Subscription.

* 2: Pay\-by\-bandwidth.

* 3: Pay\-by\-data\-transfer.



**IpAddressPoolId ** <span data-label="purple">String </span>`optional` `Example: ippool-2zeerra***`

The ID of the IP address pool.

You can call the [DescribeIpAddressPools](https://docs.byteplus.com/en/docs/eip/DescribeIpAddressPools) API to query the ID of the IP address pool.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">The IP address pool is in the beta stage. To request a trial, please contact your account manager.</div>




**PeriodUnit ** <span data-label="purple">Integer </span>`optional` `Example: 1`

The duration unit for the Subscription EIP. Valid values:


* 1 (default): Month.

* 2: Year.



**Period ** <span data-label="purple">Integer </span>`optional` `Example: 1`

The purchase duration for the Subscription EIP. Default: 1.


* When `PeriodUnit` is 1, `Period` value range: 1~9, 12, 24, 36, 48, 60.

* When `PeriodUnit` is 2, `Period` value range: 1 to 5.



**BandwidthPackageId ** <span data-label="purple">String </span>`Optional` `Example: bwp-2zeo05qre24nhrqpy****`

The ID of the Bandwidth Package, which indicates adding the EIP to the Bandwidth Package.

You can call [DescribeBandwidthPackages](https://docs.byteplus.com/en/docs/bandwidthpackage/DescribeBandwidthPackages) to query the ID of the Bandwidth Package.

To add the EIP to the Bandwidth Package, the following conditions must be met:


* Both have the same protection type.

* Both are in the same region.

* The metering method for the EIP must be Pay\-as\-you\-go.

* The Bandwidth Package is IPv4.



**Bandwidth ** <span data-label="purple">Integer </span>`optional` `Example: 1`

The bandwidth cap of the EIP. Default: 1 Mbps.


* If the `BillingType` is set to 1, the valid range is 1\-500.

* If the `BillingType` is set to 2, the valid range is 1\-500.

* If the `BillingType` is set to 3, the valid range is 1\-200.



**SecurityProtectionTypes.N** <span data-label="purple">String</span> `optional` `Example: AntiDDoS_Enhanced`

The security protection type of the EIP.


* N represents the sequence number of a protection type. Currently, only 1 is supported.

* Values:

   * AntiDDoS_Enhanced: Apply for an EIP with enhanced protection, which can be associated with an Anti\-DDoS Origin (Enterprise Edition) instance.

      <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="2">tip      </div>
      

      * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="2">If <code>SecurityProtectionTypes.N</code> is set to AntiDDoS_Enhanced, <code>BillingType</code> must be 2 or 3, and <code>ISP</code> must be BGP.      </div>
      

      * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="2">EIPs with enhanced protection type are in the beta stage. If you need a trial, contact your account manager.      </div>
      

   * Leaving it blank means applying for an EIP with default protection.



**SecurityProtectionInstanceId ** <span data-label="purple">Integer </span>`Optional` `Example: 20`

The ID of Anti\-DDoS Origin (Enterprise Edition).

You can call the [DescInstanceList](https://docs.byteplus.com/en/docs/6352/1282918) interface to query the ID of Anti\-DDoS Origin (Enterprise Edition).

This parameter is required when `SecurityProtectionTypes` is set to AntiDDoS_Enhanced.



**RenewType ** <span data-label="purple">Integer </span>`optional` `Example: 1`

The renewal method of the Subscription EIP. Valid values:


* 1 (default): Manual renewal.

* 2: Automatic renewal.

* 3: Non\-renewal upon expiration.



**RenewPeriodTimes ** <span data-label="purple">Integer </span>`optional` `Example: 1`

The length for automatic renewal, with valid values of 1, 2, 3, 6, and 12 month(s).

> If `RenewType` is 2, `RenewPeriodTimes` must be provided.



**ProjectName ** <span data-label="purple">String </span>`optional` `Example: Project_1`

The name of the project to which the EIP belongs. If left blank, this parameter defaults to the default project.



**Tags.N.Key ** <span data-label="purple">String </span>`optional` `Example: key1`

The key of the custom tag.


* N represents the sequence number of a tag key. Valid values: 1–50.

* Separate multiple tag keys with ampersands (&).

* Cannot start with `volc:` or `sys:` in any case form.

* Must be 1 to 128 characters. May include characters in any language, numbers, spaces ( ), underscores (_), periods (.), half\-width colons (:), slashes (/), equal signs (=), plus signs (+), hyphens (\-), and at signs (@).

* If a tag key starts or ends with spaces, the system automatically deletes them.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Tag keys of the same resource must be unique.</div>




**Tags.N.Value ** <span data-label="purple">String </span>`optional` `Example: value1`

The value of the custom tag.


* N represents the sequence number of a tag value. Valid values: 1–50.

* Separate multiple tag values with ampersands (&).

* The value can be 0 to 256 characters in length. If left blank, the parameter defaults to an empty value.

* May include characters in different languages, numbers, spaces ( ), underscores (_), periods (.), half\-width colons (:), slashes (/), equal signs (=), plus signs (+), hyphens (\-), and at signs (@).

* Case\-sensitive.

* If a tag value starts or ends with a space, the system automatically deletes the space.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">To provide this parameter, you must first provide <code>Tags.N.Key</code>.</div>




**ClientToken ** <span data-label="purple">String </span>`optional` `Example: 123e4567-e89b-12d3-a456-42665544****`

Ensure the request idempotency. You can use the client to automatically generate a token, but you must make sure that the token is unique among different requests. This prevents repeated actions due to multiple client retries when the call of the API action times out or an internal server error occurs. Values:


* Must not exceed 64 ASCII characters.



&nbsp;

<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters

The following only details response parameters specific to this API. For more information, see [Response parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response).



**RequestId ** <span data-label="purple">String </span>`Example: 2021062415303301022514515207C4****`

Request ID.



**EipAddress ** <span data-label="purple">String </span>`Example: 12.XX.XX.89`

The address of the EIP.



**AllocationId ** <span data-label="purple">String </span>`Example: eip-2ziwb7ujxscd****`

The ID of the EIP.



&nbsp;

<span id=".6K-35rGC56S65L6L"></span>
## Request example

```json
GET /?Action=AllocateEipAddress&Version=2020-04-01&Name=eip-1&ISP=BGP&BillingType=2&Bandwidth=10 HTTP/1.1
Host: vpc.cn-beijing.byteplusapi.com.cn
Service: vpc
Region: cn-beijing
```


<span id=".6L-U5Zue56S65L6L"></span>
## Response example

```json
{
    "ResponseMetadata": {
        "RequestId": "20230604110420****100232280022D31",
        "Action": "AllocateEipAddress",
        "Version": "2020-04-01",
        "Service": "vpc",
        "Region": "cn-north-1"
    },
    "Result": {
        "AllocationId": "eip-2ziwb7ujxscd****",
        "EipAddress": "12.XX.XX.89",
        "RequestId": "2021062415303301022514515207C4****"
    }
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error code

For more information, see [Common error codes](https://docs.byteplus.com/en/docs/eip/Public-error-codes).


|Status code |Error code |Error message |Description |
|---|---|---|---|
|400 |DryRunOperation |Exception raised to indicate a successfully authorized action when the DryRun flag is set to true. |This request is set to DryRun. The action is authorized but not executed. |
|400 |IdempotentParameterMismatch |Arguments on this idempotent request are inconsistent with arguments used in previous request(s). |The parameters of this idempotent request are inconsistent with those used in the previous request. |
|400 |InsufficientIspEip |The specified ISP does not contain enough free elastic IP addresses to fulfill your request. |Insufficient EIP resources under the specified ISP. |
|400 |InvalidBandwidth.Malformed |The specified bandwidth is malformed.Ensure that bandwidth is not smaller than 1. |The specified bandwidth is invalid. Ensure the value is not less than 1 when specifying bandwidth. |
|400 |InvalidBandwidthPackage.InvalidStatus |The specified bandwidth package is not in the correct status for the request. The specified bandwidth package is in freeze. |The specified Bandwidth Package is in a status that cannot respond to this request. The current Bandwidth Package is frozen. |
|400 |InvalidBillingType.Malformed |The specified billing type of EIP is malformed. |The specified billing method is not supported. EIPs with enhanced protection only support billing methods of Pay\-by\-bandwidth and Pay\-by\-data\-transfer. |
|400 |InvalidBillingType.Malformed |The specified billing type is malformed. |The specified billing method is invalid. |
|400 |InvalidBillingType.Malformed |The specified billing type is malformed. AntiDDoS enhanced eip billing type only support 2 and 3. |The specified billing method is invalid. |
|400 |InvalidDescription.Malformed |The specified description is malformed. |The specified description format is invalid. Correct the description format and retry. |
|400 |InvalidDescription.Malformed |The specified description is malformed. Ensure the maximum length of description is 255. |The specified description format is invalid. The description cannot exceed 255 characters. |
|400 |InvalidEip.Allocated |The specified ip address has been allocated |The specified EIP has been allocated. |
|400 |InvalidEip.CountTooLarge |EIP count reach its limits. |EIP quantity exceeds the limit. |
|400 |InvalidEip.CountTooSmall |EIP count cannot be smaller than 1. |The minimum quantity of EIPs is 1. |
|400 |InvalidEip.IPFormatError |IP format error |The IP is malformed. |
|400 |InvalidEip.ISPMismatch |The specified isp does not contain the specified ip address |The specified EIP does not belong to the specified ISP. |
|400 |InvalidEip.InvalidStatus |The specified elastic ip is not in the correct status for the request. EIP post billing type don't support renew. |The specified EIP is in a status that cannot respond to this request. Pay\-as\-you\-go EIPs do not support renewal. |
|400 |InvalidIPAddress.NotSupported |The specified IP address doesn't support this operation. |This IP address does not support this action. |
|400 |InvalidIPPool.IPResourceNotEnough |The specified IP address pool does not have enough available IP address. |Insufficient available IP addresses under the specified IP address pool. |
|400 |InvalidIPPool.InvalidStatus |The specified IP address pool is not in the correct status for the request. |The specified IP address pool cannot respond to this request due to its status. |
|400 |InvalidMonthPeriod.Malformed |The specified monthly period is malformed. Monthly period only supports 1~9, 12, 24, 36, 48, 60. |The specified prepaid purchase duration in months is invalid. The valid values for purchase duration in months are 1 to 9, 12, 24, 36, 48, and 60. |
|400 |InvalidName.Malformed |The specified name is malformed. Ensure the maximum length of name is 128. |The specified name is malformed. Correct the name format and try again. |
|400 |InvalidName.Malformed |The specified name is malformed. |The format of the specified name is invalid. The name cannot exceed 128 characters. |
|400 |InvalidParameter |A parameter specified in the request is not valid, is unsupported or cannot be used. |The request contains invalid or unsupported parameters. |
|400 |InvalidParameter.ClientTokenMalformed |The specified parameter ClientToken is malformed. |The specified ClientToken is invalid. It cannot be more than 64 ASCII characters. |
|400 |InvalidPeriodUnit.Malformed |The specified period unit is malformed. Pre billing period unit can only be 1 or 2. |The specified unit for the subscription duration is invalid. The subscription duration unit must be 1 or 2. |
|400 |InvalidProtocol.Mismatch |The protocol of the bandwidth package does not match with the EIP. |The protocol type of the Bandwidth Package does not match that of the EIP. |
|400 |InvalidRenewPeriodTimes.Malformed |The specified renew period times is malformed. Renew period times only support 1, 2, 3, 6, 12. |The specified automatic renewal cycle is invalid. The value for the automatic renewal cycle must be 1, 2, 3, 6, or 12 months. |
|400 |InvalidRenewType.Malformed |The specified renew type is malformed. Renew type must be 1, 2, or 3. |The specified renewal type is invalid. The renewal type must be 1, 2, or 3. |
|400 |InvalidSecurityProtectionInstance.InvalidStatus |The specified security protection instance is not in the correct status for the request. |The specified security protection instance is in a status that cannot respond to this request. |
|400 |InvalidSecurityProtectionInstance.RegionMismatch |The specified security protection instance is not in the specified region. |The specified security protection instance does not belong to the specified region. |
|400 |InvalidSecurityProtectionInstance.SpecificationsMismatch |The specified security protection instance and EIP are in different specifications. |The specified security instance does not match the EIP specification. |
|400 |InvalidSecurityProtectionTypes.Malformed |The specified security protection type is malformed. Security protection type only support AntiDDoS_Enhanced. |The specified protection type is not supported. Currently, the protection type supports only AntiDDoS_Enhanced. |
|400 |InvalidSpecificEgress.Mismatch |The specific egress of the bandwidth package does not match with the EIP. |The IP address pool does not match the specified egress of the EIP. |
|400 |InvalidSpecificEgress.Mismatch |The specific egress of the ip pool does not match with the EIP. |The IP address pool does not match the specified egress of the EIP. |
|400 |InvalidTag.Disorder |The specified index order of tag is malformed. |The index order format of the specified tag is invalid. |
|400 |InvalidTagKey.Malformed |The specified parameter tag key is invalid. |The specified tag key is invalid. |
|400 |InvalidTagValue.Malformed |The specified parameter tag value is invalid. |The tag value is invalid. |
|400 |InvalidYearPeriod.Malformed |The specified yearly period is malformed. Yearly period only supports 1~5. |The specified purchase duration in years is invalid. The valid values for purchase duration in years are 1 to 5. |
|400 |LimitExceeded.BandwidthPerEip |You've reached the limit on the bandwidth of elastic ip that you can create. |The EIP bandwidth cap has been reached. |
|400 |LimitExceeded.MonthlyAddressRetrieveQuota |You've reached the limit on the number of retrieving EIP addresses this month. |The monthly retrieval quota limit has been reached. |
|400 |LimitExceeded.SecurityProtectionTypes |You've reached the limit on the number of security protection types. |You have reached the maximum number of security protection types. |
|400 |LimitExceeded.Tags |You've reached the limit on the number of tags that you can operate at one time. |You have reached the maximum number of tags that you can manage in a single request. |
|400 |MissingParameter |The request is missing a required parameter. |This request lacks required parameters. |
|400 |OrderError |Failed to create an order in one step. |Failed to create and pay for the order. |
|400 |PreOrderError |Failed to create pre order. |The creation of the preorder failed. |
|400 |QuotaExceeded.BandwidthPackage |You've reached the limit on the EIP number of that you can add to bandwidth package. |You have reached the maximum of EIPs that you can add to a Bandwidth Package. |
|400 |QuotaExceeded.Eip |EIP number exceeded quota. |You have reache the maximum EIPs that can be applied. |
|400 |QuotaExceeded.ExceedLimit |Interface call exceeds limit. |The number of API calls exceeds the quota. |
|400 |QuotaExceeded.PremiumBGPEip |Premium BGP EIP number exceeded quota. |You have reached the maximum of EIPs with premium BGP that you can apply for. |
|400 |QuotaExceeded.SecurityProtectionInstance |You've reached the limit on the number of security protection instance that you can add. |You have reached the maximum number of security protection instances that can be added. |
|400 |UnsupportedOperation |The request on the specified instance is denied due to the account in arrears status. |The request to operate on this instance is rejected because the sum of both account balance and available coupons is less than USD 100. |
|400 |UnsupportedOperation |The request on the specified instance is denied due to the account balance and available vouchers are less than 100 yuan in total. |The action request on this instance is denied because the account is in arrears. |
|400 |UnsupportedOperation.AllocateHistoricalEIP |Only support applying for historical EIPs used by this account. |Only EIPs that have been used by this account are supported for application. |
|403 |Forbidden |You are not authorized to create an elastic IP address with the specified billing type. |No permission to create an EIP address with the fusion BGP. |
|403 |Forbidden |You are not authorized to use specific egress. |The specified egress feature for Premium BGP is not supported. |
|403 |Forbidden |You are not authorized to create single\-line value elastic IP address. |No permission to create an EIP with the premium BGP. |
|403 |Forbidden |You are not authorized to create single\-line elastic IP address. |No permission to perform actions on the specified Bandwidth Package. The protection type of the specified EIP is inconsistent with that of the Bandwidth Package. |
|403 |Forbidden |You are not authorized to create fusion BGP elastic IP address. |No permission to create an EIP with the static BGP. |
|403 |Forbidden |You are not authorized to create premium BGP elastic IP address. |No permission to apply for an EIP with enhanced protection. |
|403 |Forbidden |You are not authorized to perform operations on the specified bandwidth package. The ISP of EIP and bandwidth package is not same. |The ISP of the EIP is inconsistent with that of the Bandwidth Package. |
|403 |Forbidden |You are not authorized to create BGP SingleLine elastic IP address. |No permission to create an EIP with static single\-ISP. |
|403 |Forbidden |You are not authorized to create Anti DDos elastic IP address. |No permission to create an EIP with the BGP single\-ISP. |
|403 |Forbidden |The premium BGP line specific egress function is not support. |No permission to create an EIP with the specified billing method. |
|403 |Forbidden |You are not authorized to create Static BGP elastic IP address. |No permission to create an EIP address with a static preferential single\-ISP. |
|403 |Forbidden |You are not authorized to perform operations on the specified bandwidth package. Because of SecurityProtectionTypesInconsistent. |No permission to perform actions on the specified Bandwidth Package. The protection type of the specified EIP is inconsistent with that of the Bandwidth Package. |
|404 |InvalidBandwidthPackage.NotFound |The specified bandwidth package does not exist. |The specified Shared Bandwidth Package does not exist. |
|404 |InvalidIPPool.ISPMismatch |The specified ISP of EIP does not match the IP address pool. |The ISP of the EIP does not match that of the IP address pool. |
|404 |InvalidIPPool.NotFound |The specified IP address pool does not exist. |The specified IP address pool does not exist. |
|404 |InvalidISP.NotFound |The specified ISP does not exist. |The specified ISP does not exist. |
|404 |InvalidProject.NotFound |The specified Project does not exist. |The specified project does not exist. |
|404 |InvalidSecurityProtectionInstance.NotFound |The specified security protection instance does not exist. |The specified security protection instance does not exist. |
|404 |InvalidSpecificEgress.NotFound |The specific egress does not exist. |The specified egress does not exist. |
|409 |InvalidOperation.Conflict |The specified resource operation conflicts. |The specified action on the resource conflicts. |
|412 |IdempotentProcessing |The request uses the same client token as a previous one that is still in process. |The idempotent request is in process. |
|500 |InternalError |An internal error has occurred. |An internal error occurred. |
