---
title: "ModifyBandwidthPackageAttributes - Modifying a Bandwidth Package"
product: "Bandwidth Package"
product_code: "bandwidthpackage"
source: "https://docs.byteplus.com/en/docs/bandwidthpackage/ModifyBandwidthPackageSpec"
---

Call the ModifyBandwidthPackageAttributes API to modify the name, description, and protocol type for a Bandwidth Package instance.

<span id=".5L2_55So6K-05piO"></span>
## Instructions

If you do not configure the following optional parameters, their current values remain unchanged.

<span id=".6LCD6K-V"></span>
## Debug

[去调试](https://api.byteplus.com/api-explorer/debug?action=ModifyBandwidthPackageAttributes&serviceCode=vpc&version=2020-04-01&groupName=)


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters



**Action ** <span data-label="purple">String </span><span data-api-tag="require|bxDCrs">必选</span> `Example: ModifyBandwidthPackageAttributes`

The action that you want to perform. Value: **ModifyBandwidthPackageAttributes**.



**Version ** <span data-label="purple">String </span><span data-api-tag="require|ziYE3c">必选</span> `Example: 2020-04-01`

The API version. The current version is **2020\-04\-01**.



**BandwidthPackageId ** <span data-label="purple">String </span><span data-api-tag="require|TGCUk4">必选</span> `Example: bwp-2zeo05qre24nhrqpy****`

The ID of the Bandwidth Package.

You can call the [DescribeBandwidthPackages](https://docs.byteplus.com/en/docs/bandwidthpackage/DescribeBandwidthPackages) API to query the Bandwidth Package ID.



**BandwidthPackageName ** <span data-label="purple">String </span>`optional` `Example: bwp-01`

The name of the Bandwidth Package.


* Must be 1 to 128 characters in length.

* Must start with a letter, Chinese character, or number. May include periods (.), underscores (_), and hyphens (\-).



**Enable dual\-stack ** <span data-label="purple">Boolean </span>`optional` `Example: true`

Specify whether to enable dual\-stack for the specified Bandwidth Package. Type the enumerated values strictly in the case form as follows. Do not set other values.


* true: Enable dual\-stack.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">The dual\-stack feature is in the beta stage. To request a trial, please contact your account manager.</div>




**Description ** <span data-label="purple">String </span>`optional` `Example: This is a bandwidthpackage`

The description of the Bandwidth Package.


* Must be 0 to 255 characters.

* Must start with a letter, Chinese character, or number. May include commas (,), periods (.), underscores (_), spaces ( ), equal signs (=), hyphens (\-), full\-width commas (，), and full\-width periods (。).



&nbsp;

<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters



**RequestId ** <span data-label="purple">String </span>`Example: 2021062415303301022514515207C4****`

Request ID.



&nbsp;

<span id=".6K-35rGC56S65L6L"></span>
## Request examples

```json
GET /?Action=ModifyBandwidthPackageAttributes&Version=2020-04-01&BandwidthPackageId=bwp-2zeo05qre24nhrqpy****&BandwidthPackageName=bwp-01 HTTP/1.1
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
        "Action": "ModifyBandwidthPackageAttributes",
        "Version": "2020-04-01",
        "Service": "vpc",
        "Region": "cn-beijing"
    },
    "Result": {
        "RequestId": "2021062415303301022514515207C4****"
    }
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error codes

For more information, see [Common error codes](https://docs.byteplus.com/en/docs/bandwidthpackage/Public-error-codes).


|Status code |Error codes |Error message |Description |
|---|---|---|---|
|400 |DryRunOperation |Exception raised to indicate a successfully authorized action when the DryRun flag is set to true. |This request is set to DryRun. The action is authorized but not executed. |
|400 |InvalidDescription.Malformed |The specified description is malformed. |The format specified for the description is invalid. Correct the description format and retry. |
|400 |InvalidDescription.Malformed |The specified description is malformed. Ensure the maximum length of description is 255. |The format specified for the description is invalid. A description must not exceed 255 characters. |
|400 |InvalidDualStackBillingType.Malformed |The specified billing type is malformed, only support 2, 3 or 4. |The specified billing method is invalid for the Bandwidth Package. Enabling dual\-stack is supported only for Pay\-by\-bandwidth, Pay\-by\-main\-traffic and Pay\-by\-95th\-peak Bandwidth Packages. |
|400 |InvalidDualStackBwp.Malformed |The specified dual\-stack bandwidth package is not supported to disable. |The specified dual\-stack Bandwidth Package cannot be disabled. |
|400 |InvalidDualStackISP.Malformed |The specified ISP does not support dual\-stack. |The specified ISP for the Bandwidth Package is invalid. This ISP does not support enabling dual\-stack. |
|400 |InvalidDualStackProtocol.Malformed |The specified protocol is malformed, only support IPv4. |The specified protocol type for the Bandwidth Package is not valid. Only IPv4 supports enabling dual\-stack. |
|400 |InvalidDualStackSecurityProtectionTypes.Malformed |The specified Anti DDos bandwidth package does not support dual\-stack. |Bandwidth Package with enhanced protection does not support enabling dual\-stack. |
|400 |InvalidEip.InUse |The specified EIP is being operated by another request. |The specified EIP is being processed by another request. Try again later. |
|400 |InvalidName.Malformed |The specified name is malformed. |The format specified for the name is invalid. Correct the name format and retry. |
|400 |InvalidName.Malformed |The specified name is malformed. Ensure the maximum length of name is 128. |The format of specified name is invalid. A name must not exceed 128 characters in length. |
|400 |MissingParameter |The request is missing a required parameter. |This request is missing a required parameter. |
|400 |QuotaExceeded.BandwidthPackage |You've reached the limit on the number of bandwidth package that you can create. |You have reached the maximum of Bandwidth Packages that you can create. |
|400 |QuotaExceeded.DualStackBandwidthPackage |You've reached the limit on the number of dual\-stack bandwidth package that you can create. |You have reached the maximum of dual\-stack Bandwidth Packages that you can create. |
|403 |Forbidden |You are not authorized to enable dual stack. |No permission to enable dual\-stack Bandwidth Package. |
|403 |Forbidden.Ipv6IspType |You are not authorized to create this type IPv6 CIDR. |You do not have permission to create an IPv6 CIDR block for the specified ISP type. |
|404 |InvalidBandwidthPackage.NotFound |The specified bandwidth package does not exist. |The specified Bandwidth Package does not exist. |
|409 |InvalidOperation.Conflict |The specified resource operation conflicts. |The specified resource action conflicted. |
|500 |InternalError |An internal error has occurred. |An internal error occurred. |
