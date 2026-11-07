---
title: "DeleteCenBandwidthPackage - Deleting a bandwidth package instance"
product: "Cloud Enterprise Network"
product_code: "cen"
source: "https://docs.byteplus.com/en/docs/cen/DeleteCenBandwidthPackage"
---

Call the DeleteCenBandwidthPackage API to delete the specified bandwidth package.

<span id=".6LCD6K-V"></span>
## Debug

[去调试](https://api.byteplus.com/api-explorer/?action=DeleteCenBandwidthPackage&groupName=%E5%B8%A6%E5%AE%BD%E5%8C%85&serviceCode=cen&version=2020-04-01)


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters

The following only details request parameters specific to this API and key common parameters. More information can be found in [Common parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).



**Action ** <span data-label="purple">string </span><span data-api-tag="require|54yJfU">必选</span> `Example: DeleteCenBandwidthPackage`

Action to execute. Set the value to DeleteCenBandwidthPackage.



**Version ** <span data-label="purple">string </span><span data-api-tag="require|e35u82">必选</span> `Example: 2020-04-01`

The API version. Value: 2020\-04\-01.



**CenBandwidthPackageId ** <span data-label="purple">string </span><span data-api-tag="require|mtavQw">必选</span> `Example: cbp-4c2zaavbvh5f42****`

ID of the bandwidth package.

You can call the [DescribeCenBandwidthPackages](https://docs.byteplus.com/en/docs/cen/DescribeCenBandwidthPackages) API to query the bandwidth package ID.



&nbsp;

<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters

This API does not have specific response parameters. For more information, see [Response structure](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response).

<span id=".6K-35rGC56S65L6L"></span>
## Request examples

```text
GET /?Action=DeleteCenBandwidthPackage&Version=2020-04-01&CenBandwidthPackageId=cbp-4c2zaavbvh5f42**** HTTP/1.1
Host: cen.byteplusapi.com
X-Date: 20260109T085601Z
Authorization: HMAC-SHA256 Credential=Adfks******wekfwe/20260109/cn-beijing/cen/request, SignedHeaders=host;x-date, Signature=47a7d934ff7b37c03938******cd7b8278a40a1057690c401e92246a0e41085f


```


<span id=".6L-U5Zue56S65L6L"></span>
## Response examples

```json
{
  "ResponseMetadata": {
    "RequestId": "20250815171900131035074242415AB2",
    "Action": "DeleteCenBandwidthPackage",
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
|400 |MissingParameter |The request is missing a required parameter. Ensure that you have supplied all the required parameters for the request. |This request does not contain required parameters. Ensure all required parameters are provided when initiating the request. |
|400 |InvalidParameter |A parameter specified in the request is not valid, is unsupported or cannot be used. |The request contains invalid or unsupported parameters. |
|400 |InvalidCenBandwidthPackage.InUse |The bandwidth package of the specified geographic regions is in use. |The bandwidth package between the specified geographic regions is currently in use. |
|400 |InvalidCenBandwidthPackage.InvalidStatus |Specified CEN bandwidth package is being operated now. |The specified bandwidth package is in a status that cannot respond to this request. Retry later. |
|400 |UnsupportedOperation.PrepaidInstance |Specified bandwidth package is a prepaid one and cannot be deleted. |The specified bandwidth package is a prepaid instance and does not support deleting. |
|400 |UnsupportedOperation |The specified request is denied because the type of bandwidth package is POC. |The specified bandwidth package is a package for testing. Action unsupported. |
|404 |InvalidCenBandwidthPackage.NotFound |The bandwidth package of the specified geographic regions does not exist. |The specified bandwidth package does not exist. |
|409 |InvalidCen.InvalidStatus |The specified CEN instance is not in the correct status for the request. |The specified CEN instance is in a state that cannot process the request. Please try again later. |
|500 |InternalError |Request failed with internal server error. |Internal system error. |
