---
title: "ModifyCenBandwidthPackageAttributes - Modifying the basic information of bandwidth package instances"
product: "Cloud Enterprise Network"
product_code: "cen"
source: "https://docs.byteplus.com/en/docs/cen/ModifyCenBandwidthPackageAttributes"
---

Call the ModifyCenBandwidthPackageAttributes API to modify the basic information of the bandwidth package.

<span id=".6LCD6K-V"></span>
## Debug

[去调试](https://api.byteplus.com/api-explorer/?action=ModifyCenBandwidthPackageAttributes&groupName=%E5%B8%A6%E5%AE%BD%E5%8C%85&serviceCode=cen&version=2020-04-01)


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters

The following only details request parameters specific to this API and key common parameters. More information can be found in [Common parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).



**Action ** <span data-label="purple">string </span><span data-api-tag="require|y0Z1y3">必选</span> `Example: ModifyCenBandwidthPackageAttributes`

Action to execute. Set the value to ModifyCenBandwidthPackageAttributes.



**Version ** <span data-label="purple">string </span><span data-api-tag="require|8CITo1">必选</span> `Example: 2020-04-01`

The API version. Value: 2020\-04\-01.



**Bandwidth ** <span data-label="purple">integer </span>`optional` `Example: 100`

Bandwidth cap of the bandwidth package. The value range is 2 to 10,000, in Mbps.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">The bandwidth value entered should not be less than the size of the allocated inter\-region bandwidth.</div>




**CenBandwidthPackageName ** <span data-label="purple">string </span>`optional` `Example: cbp-test`

Name of the bandwidth package.


* Must start with a letter, number, or Chinese character. May include letters, numbers, Chinese characters, and the following symbols: periods (.), underscores (_), and hyphens (\-).

* Must be 1 to 128 characters.



**Description ** <span data-label="purple">string </span>`optional` `Example: namedesc`

Description of the bandwidth package.


* Must start with a letter, number, or Chinese character. May include letters, numbers, Chinese characters, and the following symbols: commas (,), periods (.), underscores (_), spaces ( ), equal signs (=), hyphens (\-), full\-width commas ( ， ), and full\-width periods ( 。 ).

* Must be 0 to 255 characters.



**CenBandwidthPackageId ** <span data-label="purple">string </span><span data-api-tag="require|7iBjzE">必选</span> `Example: cbp-4c2zaavbvh5fx****`

The instance ID of the bandwidth package.

You can call the [DescribeCenBandwidthPackages](https://docs.byteplus.com/en/docs/cen/DescribeCenBandwidthPackages) API to query the bandwidth package ID.



&nbsp;

<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters

This API does not have specific response parameters. For more information, see [Response structure](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response).

<span id=".6K-35rGC56S65L6L"></span>
## Request examples

```text
GET /?Action=ModifyCenBandwidthPackageAttributes&Version=2020-04-01&CenBandwidthPackageId=cbp-4c2zaavbvh5fx**** HTTP/1.1
Host: cen.byteplusapi.com
X-Date: 20260109T085540Z
Authorization: HMAC-SHA256 Credential=Adfks******wekfwe/20260109/cn-beijing/cen/request, SignedHeaders=host;x-date, Signature=47a7d934ff7b37c03938******cd7b8278a40a1057690c401e92246a0e41085f


```


<span id=".6L-U5Zue56S65L6L"></span>
## Response examples

```json
{
  "ResponseMetadata": {
    "RequestId": "2025071812552225409706722747C5A8",
    "Action": "ModifyCenBandwidthPackageAttributes",
    "Version": "2020-04-01",
    "Service": "cen",
    "Region": "cn-beijing"
  },
  "Result": {}
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error codes

The table below describes the error codes for this API that are associated with business logic. For details, see [Common error codes](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-error-codes).


|Status code |Error codes |Error message |Notes |
|---|---|---|---|
|400 |InvalidParameter |A parameter specified in the request is not valid, is unsupported or cannot be used. |The request contains invalid or unsupported parameters. |
|400 |MissingParameter |The request is missing a required parameter. Ensure that you have supplied all the required parameters for the request. |This request does not contain required parameters. Ensure all required parameters are provided when initiating the request. |
|400 |InvalidCenBandwidthPackage.BandwidthNotEnough |Specified bandwidth is not enough for current inter region bandwidths. |The specified bandwidth value is insufficient for the current inter\-region bandwidth usage. |
|400 |InvalidCenBandwidthPackage.InvalidStatus |Specified CEN bandwidth package is being operated now. |The specified bandwidth package is in a status that cannot respond to this request. Retry later. |
|400 |LimitExceeded.BandwidthOfBandwidthPackage |Specified bandwidth exceeds the range of bandwidth package. |The specified bandwidth exceeds the valid range of the bandwidth package. |
|400 |UnsupportedOperation.BandwidthScaleDown |Specified bandwidth value cannot be less than current value. |Downgrading a bandwidth package is currently not supported. |
|400 |FailedOperation |Failed to obtain CEN bandwidth package billing information. |Failed to retrieve the billing information of the bandwidth package. |
|400 |OrderError |Failed to create an order. |Order placement failed. |
|400 |InvalidName.Malformed |The specified name is malformed. Ensure the maximum length of name is 128. |The format of the specified name is invalid. A name must not exceed 128 characters. |
|400 |InvalidName.Malformed |The specified name is malformed. |The specified name format is invalid. Correct the name format and retry. |
|400 |InvalidDescription.Malformed |The specified description is malformed. |The specified description format is invalid. Correct the description format and retry. |
|400 |InvalidDescription.Malformed |The specified description is malformed. Ensure the maximum length of description is 255. |The specified description format is invalid. A description must not exceed 255 characters. |
|400 |UnsupportedOperation |The payment failed due to the account balance is not enough for this order. |Insufficient account balance. Order payment failed. |
|400 |UnsupportedOperation |The request on the specified instance is denied due to the account in arrears status. |The action request on this instance is denied because the account is in arrears. |
|400 |UnsupportedOperation |The specified request is denied because the type of bandwidth package is POC. |The specified bandwidth package is a package for testing. Action unsupported. |
|400 |UnsupportedOperation |The request on the specified bandwidth package is denied because the bandwidth package is shut down due to arrears. |The specified bandwidth package is suspended due to overdue payments. Action unsupported. |
|400 |UnsupportedOperation |The request on the specified bandwidth package is denied because the bandwidth package is expired. |The specified bandwidth package is expired. Action unsupported. |
|400 |InvalidBandwidthPackage.OrderConflict |The specified Bandwidth package has unpaid order. |The specified bandwidth package has an unpaid order. Please complete the payment for the previous order or wait for it to time out after 24 hours. |
|400 |InvalidCenCrossBorderBandwidthPackage.FrozenStatus |The specified request is denied because your account has been frozen for cross\-border. Please wait for the Service Provider to unfreeze it. |The cross\-border service under your account is suspended. Proceed after the line operator reactivates your service. |
|404 |InvalidCenBandwidthPackage.NotFound |The bandwidth package of the specified geographic regions does not exist. |The specified bandwidth package does not exist. |
|409 |InvalidCen.InvalidStatus |The specified CEN instance is not in the correct status for the request. |The specified CEN instance is in a state that cannot process the request. Please try again later. |
|500 |InternalError |Request failed with internal server error. |Internal system error. |
