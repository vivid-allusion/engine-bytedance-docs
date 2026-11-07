---
title: "ModifyTransitRouterBandwidthPackageAttributes - Modifying a TR bandwidth package"
product: "Transit Router"
product_code: "transitrouter"
source: "https://docs.byteplus.com/en/docs/transitrouter/ModifyTransitRouterBandwidthPackageAttributes"
---

Call ModifyTransitRouterBandwidthPackageAttributes to modify the basic information of a specified Transit Router (TR) bandwidth package.

<span id=".6LCD6K-V"></span>
## Debug

[去调试](https://api.byteplus.com/api-explorer/debug?action=ModifyTransitRouterBandwidthPackageAttributes&serviceCode=transitrouter&version=2020-04-01&groupName=)


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters

The following only details request parameters specific to this API and key common parameters. For more information, see [Common parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).



**Action ** <span data-label="purple"> String  </span><span data-api-tag="require|sB9r9n">必选</span> `Example: ModifyTransitRouterBandwidthPackageAttributes`

The interface name. The current API name is `ModifyTransitRouterBandwidthPackageAttributes`.



**Version ** <span data-label="purple"> String  </span><span data-api-tag="require|Mn2eVM">必选</span> `Example: 2020-04-01`

The interface version. The current API version is `2020-04-01`.



**TransitRouterBandwidthPackageId ** <span data-label="purple"> String  </span><span data-api-tag="require|SzNgch">必选</span> `Example: tr-bp-4c2zaavbvh5f42****`

The ID of the Transit Router (TR) bandwidth package. You can call [DescribeTransitRouterBandwidthPackages](https://docs.byteplus.com/en/docs/transitrouter/DescribeTransitRouterBandwidthPackages) to obtain the bandwidth package ID.



**TransitRouterBandwidthPackageName** <span data-label="purple">String</span> `optional` `Example: trbp-test`

The name of the TR bandwidth package.


* Must start with a letter, number, or Chinese character. May include letters, numbers, Chinese characters, and the following symbols: periods (.), underscores (_), and hyphens (\-).

* Must be 1 to 128 characters.

* If you do not provide this parameter or leave it unset, the original configuration is retained.



**Description ** <span data-label="purple"> String  </span>`optional` `Example: namedesc`

The description of the TR bandwidth package.


* Must start with a letter, number, or Chinese character. May include letters, numbers, Chinese characters, and the following symbols: commas (,), periods (.), underscores (_), spaces ( ), equal signs (=), hyphens (\-), Chinese commas ( ， ), and Chinese periods ( 。 ).

* Must be 0 to 255 characters.

* If you do not provide this parameter or leave it unset, the original configuration is retained.



**Bandwidth ** <span data-label="purple"> Integer </span>`optional` `Example: 2`

The peak bandwidth of the TR bandwidth package. Valid range: 2 to 10000 Mbps. Default: 2 Mbps.



<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters

This API does not have specific response parameters. For more information, see [Response structure](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response).

<span id=".6K-35rGC56S65L6L"></span>
## Request examples

```JSON
GET /?Action=ModifyTransitRouterBandwidthPackageAttributes&Version=2020-04-01&TransitRouterBandwidthPackageId=tr-bp-4c2zaavbvh5f42**** HTTP/1.1
Host: transitrouter.cn-beijing.byteplusapi.com.cn
X-Date: 20250804T034938Z
Authorization: HMAC-SHA256 Credential=Adfks******wekfwe/20250804/cn-beijing/transitrouter/request, SignedHeaders=host;x-date, Signature=47a7d934ff7b37c03938******cd7b8278a40a1057690c401e92246a0e41085f
```


<span id=".6L-U5Zue56S65L6L"></span>
## Response examples

```JSON
{
  "ResponseMetadata": {
    "RequestId": "202508041149410600890000624DDBD8",
    "Action": "ModifyTransitRouterBandwidthPackageAttributes",
    "Version": "2020-04-01",
    "Service": "transitrouter",
    "Region": "cn-beijing"
  },
  "Result": {}
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error codes

The table below describes the error codes for this API that are associated with business logic. For more information, see [Common error codes](https://docs.byteplus.com/en/docs/transitrouter/Public-error-codes).


|**Status code** |**Error codes** |**Error message** |**Explanation** |
|---|---|---|---|
|400 |FailedOperation |Failed to obtain TransitRouter bandwidth package billing information. |Failed to retrieve the billing information of the bandwidth package. |
|400 |InvalidDescription.Malformed |The specified description is malformed. |The specified description format is invalid. Correct the description format and retry. |
|400 |InvalidDescription.Malformed |The specified description is malformed. Ensure the maximum length of description is 255. |The format of specified description is invalid. A description must not exceed 255 characters. |
|400 |InvalidName.Malformed |The specified name is malformed. |The format of the specified name is invalid. Correct the name format and retry. |
|400 |InvalidName.Malformed |The specified name is malformed. Ensure the maximum length of name is 128. |The format of the specified name is invalid. A name must not exceed 128 characters. |
|400 |InvalidTransitRouterBandwidthPackage.BandwidthNotEnough |Specified bandwidth is not enough for current inter region bandwidths. |The specified bandwidth value is insufficient for the current inter\-region bandwidth usage. |
|400 |InvalidTransitRouterBandwidthPackage.InvalidStatus |The specified TransitRouter bandwidth package is being operated now. |The specified bandwidth package is in a status that cannot respond to this request. Retry later. |
|400 |InvalidTransitRouterCrossBorderBandwidthPackage.FrozenStatus |The specified request is denied because your account has been frozen for cross\-border. Please wait for the Service Provider to unfreeze it. |The cross\-border service under your account is suspended. Proceed after the line operator reactivates your service. |
|400 |LimitExceeded.BandwidthOfBandwidthPackage |The specified bandwidth exceeds the bandwidth limit of Transit Router bandwidth package. |The specified bandwidth exceeds the valid range of the bandwidth package. |
|400 |OrderError |Failed to create an order. |Order placement failed. |
|400 |OrderError |Failed to create an order. |Order placement failed. |
|400 |UnsupportedOperation.ActionOnPocPackage |The specified request is denied because the type of bandwidth package is POC. |The specified bandwidth package is a package for testing. Action unsupported. |
|400 |UnsupportedOperation.ExpiredStatus |The request on the specified bandwidth package is denied because the bandwidth package is expired. |The specified bandwidth package is expired. This action is unsupported. |
|400 |UnsupportedOperation.OverdueStatus |The request on the specified bandwidth package is denied because the bandwidth package is shut down due to arrears. |The specified bandwidth package is suspended due to overdue payments. The action is unsupported. |
|400 |UnsupportedOperation |The payment failed due to the account balance is not enough for this order. |Insufficient account balance. Order payment failed. |
|400 |UnsupportedOperation |The request on the specified instance is denied due to the account in arrears status. |The action request on this instance is denied because the account is in arrears. |
|404 |InvalidTransitRouterBandwidthPackage.NotFound |The specified bandwidth package id does not exist. |The specified bandwidth package does not exist. |
