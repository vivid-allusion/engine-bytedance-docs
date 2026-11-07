---
title: "DisassociateCenBandwidthPackage - detach the bandwidth package instance from the Cloud Enterprise Network (CEN) instance"
product: "Cloud Enterprise Network"
product_code: "cen"
source: "https://docs.byteplus.com/en/docs/cen/DisassociateCenBandwidthPackage"
---

Call the DisassociateCenBandwidthPackage API to detach the bandwidth package instance from the Cloud Enterprise Network (CEN) instance.

<span id=".5L2_55So6K-05piO"></span>
## Notes

Ensure no inter\-region bandwidth exists under the target bandwidth package before calling this API; otherwise, the operation will fail.

<span id=".6LCD6K-V"></span>
## Debug

[去调试](https://api.byteplus.com/api-explorer/?action=DisassociateCenBandwidthPackage&groupName=%E5%B8%A6%E5%AE%BD%E5%8C%85&serviceCode=cen&version=2020-04-01)


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters

The following only details request parameters specific to this API and key common parameters. More information can be found in [Common parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).



**Action ** <span data-label="purple">string </span><span data-api-tag="require|zAAMTj">必选</span> `Example value: DisassociateCenBandwidthPackage`

The action you want to perform. Value: DisassociateCenBandwidthPackage.



Version string Example: 2020\-04\-01

The API version. Value: 2020\-04\-01.



**CenId ** <span data-label="purple">string </span><span data-api-tag="require|AcbP62">必选</span> `Example value: cen-7qthudw0ll6jmc****`

Cloud Enterprise Network (CEN) instance ID.

You can call the [DescribeCens](https://docs.byteplus.com/en/docs/cen/DescribeCens) interface to query the Cloud Enterprise Network (CEN) instance ID.



**CenBandwidthPackageId ** <span data-label="purple">string </span><span data-api-tag="require|4pzLcG">必选</span> `Example: cbp-4c2zaavbvh5fx****`

The ID of the bandwidth package.

You can call the [DescribeCenBandwidthPackages](https://docs.byteplus.com/en/docs/cen/DescribeCenBandwidthPackages) API to query the bandwidth package ID.



&nbsp;

<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters

This API does not have specific response parameters. For more information, see [Response structure](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response).

<span id=".6K-35rGC56S65L6L"></span>
## Request examples

```text
GET /?Action=DisassociateCenBandwidthPackage&Version=2020-04-01&CenId=cen-7qthudw0ll6jmc****&CenBandwidthPackageId=cbp-4c2zaavbvh5fx**** HTTP/1.1
Host: cen.byteplusapi.com
X-Date: 20260109T085508Z
Authorization: HMAC-SHA256 Credential=Adfks******wekfwe/20260109/cn-beijing/cen/request, SignedHeaders=host;x-date, Signature=47a7d934ff7b37c03938******cd7b8278a40a1057690c401e92246a0e41085f


```


<span id=".6L-U5Zue56S65L6L"></span>
## Response examples

```json
{
  "ResponseMetadata": {
    "RequestId": "20250815171555044058218036DECD18",
    "Action": "DisassociateCenBandwidthPackage",
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
|400 |InvalidCenBandwidthPackage.InUse |The bandwidth package of the specified geographic regions is in use. |The bandwidth package between specified geographic regions is in use. |
|400 |InvalidCenBandwidthPackage.InvalidStatus |Specified CEN bandwidth package is being operated now. |The specified bandwidth package is in a status that cannot respond to this request. Retry later. |
|404 |InvalidCen.NotFound |The specified CEN does not exist. |The specified CEN instance does not exist. |
|404 |InvalidCenBandwidthPackage.NotFound |The bandwidth package of the specified geographic regions does not exist. |The specified bandwidth package does not exist. |
|404 |InvalidCenBandwidthPackage.NotInUse |Specified bandwidth package has not been associated with any CEN. |This bandwidth package is not associated with a CEN instance. |
|409 |InvalidCen.InvalidStatus |The specified CEN instance is not in the correct status for the request. |The specified Cloud Enterprise Network (CEN) instance status cannot respond to this request. Try again later. |
|500 |InternalError |Request failed with internal server error. |Internal system error. |
