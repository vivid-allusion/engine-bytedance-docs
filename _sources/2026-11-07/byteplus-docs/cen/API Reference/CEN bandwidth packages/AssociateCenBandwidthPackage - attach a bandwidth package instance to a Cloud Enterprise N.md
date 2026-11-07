---
title: "AssociateCenBandwidthPackage - attach a bandwidth package instance to a Cloud Enterprise Network (CEN) instance"
product: "Cloud Enterprise Network"
product_code: "cen"
source: "https://docs.byteplus.com/en/docs/cen/AssociateCenBandwidthPackage"
---

Call the AssociateCenBandwidthPackage API to attach a bandwidth package instance to a Cloud Enterprise Network (CEN) instance.

<span id=".5L2_55So6K-05piO"></span>
## Notes


* Each Cloud Enterprise Network (CEN) instance supports binding multiple bandwidth packages from different interchange zones.

* Each bandwidth package can only be attached to one Cloud Enterprise Network (CEN) instance.


<span id=".6LCD6K-V"></span>
## Debug

[去调试](https://api.byteplus.com/api-explorer/?action=AssociateCenBandwidthPackage&groupName=%E5%B8%A6%E5%AE%BD%E5%8C%85&serviceCode=cen&version=2020-04-01)


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters

The following only details request parameters specific to this API and key common parameters. More information can be found in [Common parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).



**Action ** <span data-label="purple">string </span><span data-api-tag="require|je8KK1">必选</span> `Example value: AssociateCenBandwidthPackage`

The action to perform, value: AssociateCenBandwidthPackage.



Version string Example: 2020\-04\-01

The API version. Value: 2020\-04\-01.



**CenId ** <span data-label="purple">string </span><span data-api-tag="require|q2xc9L">必选</span> `Example: cen-7qthudw0ll6jmc****`

Cloud Enterprise Network instance ID.



**CenBandwidthPackageId ** <span data-label="purple">string </span><span data-api-tag="require|Mf86M8">必选</span> `Example: cbp-4c2zaavbvh5fx****`

ID of the CEN bandwidth package.

You can call the [DescribeCenBandwidthPackages](https://docs.byteplus.com/en/docs/cen/DescribeCenBandwidthPackages) interface to query the bandwidth package ID.



&nbsp;

<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters

This API does not have specific response parameters. For more information, see [Response structure](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response).

<span id=".6K-35rGC56S65L6L"></span>
## Request examples

```text
GET /?Action=AssociateCenBandwidthPackage&Version=2020-04-01&CenId=cen-7qthudw0ll6jmc****&CenBandwidthPackageId=cbp-4c2zaavbvh5fx**** HTTP/1.1
Host: cen.byteplusapi.com
X-Date: 20260109T085034Z
Authorization: HMAC-SHA256 Credential=Adfks******wekfwe/20260109/cn-beijing/cen/request, SignedHeaders=host;x-date, Signature=47a7d934ff7b37c03938******cd7b8278a40a1057690c401e92246a0e41085f


```


<span id=".6L-U5Zue56S65L6L"></span>
## Response examples

```json
{
  "ResponseMetadata": {
    "RequestId": "202508151714480082511741341A66E8",
    "Action": "AssociateCenBandwidthPackage",
    "Version": "2020-04-01",
    "Service": "cen",
    "Region": "cn-beijing"
  },
  "Result": {}
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error codes

The table below describes the error codes for this API that are associated with business logic. For more information, see [Common error codes](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-error-codes).


|Status code |Error codes |Error message |Explanation |
|---|---|---|---|
|400 |MissingParameter |The request is missing a required parameter. Ensure that you have supplied all the required parameters for the request. |This request does not contain required parameters. Ensure all required parameters are provided when initiating the request. |
|400 |InvalidParameter |A parameter specified in the request is not valid, is unsupported or cannot be used. |The request contains invalid or unsupported parameters. |
|400 |InvalidCenBandwidthPackage.InUse |Specified bandwidth package has been associated with a CEN. |The specified bandwidth package is already attached to another Cloud Enterprise Network instance. |
|400 |InvalidCenBandwidthPackage.InvalidStatus |Specified CEN bandwidth package is being operated now. |The specified bandwidth package is in a status that cannot respond to this request. Retry later. |
|400 |UnsupportedOperation |The request on the specified bandwidth package is denied because the bandwidth package is expired. |The specified bandwidth package is expired. Action unsupported. |
|400 |UnsupportedOperation |The request on the specified bandwidth package is denied because the bandwidth package is shut down due to arrears. |The specified bandwidth package is suspended due to overdue payments. Action unsupported. |
|400 |InvalidCenCrossBorderBandwidthPackage.FrozenStatus |The specified request is denied because your account has been frozen for cross\-border. Please wait for the Service Provider to unfreeze it. |The cross\-border service under your account is suspended. Proceed after the line operator reactivates your service. |
|404 |InvalidCen.NotFound |The specified CEN does not exist. |The specified Cloud Enterprise Network instance does not exist. |
|404 |InvalidCenBandwidthPackage.NotFound |The bandwidth package of the specified geographic regions does not exist. |The specified bandwidth package does not exist. |
|409 |InvalidCen.InvalidStatus |The specified CEN instance is not in the correct status for the request. |The specified Cloud Enterprise Network (CEN) instance is in a state that cannot respond to this request. Retry later. |
|409 |InvalidCenBandwidthPackage.RegionSetConflict |Specified geographic region set of the bandwidth package conflicts with that of another bandwidth package. |The Cloud Enterprise Network (CEN) already has a CEN bandwidth package between the specified regions. |
|500 |InternalError |Request failed with internal server error. |Internal system error. |
