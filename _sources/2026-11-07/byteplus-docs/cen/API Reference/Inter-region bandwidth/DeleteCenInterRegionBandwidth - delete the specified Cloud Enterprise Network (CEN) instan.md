---
title: "DeleteCenInterRegionBandwidth - delete the specified Cloud Enterprise Network (CEN) instance inter-region bandwidth"
product: "Cloud Enterprise Network"
product_code: "cen"
source: "https://docs.byteplus.com/en/docs/cen/DeleteCenInterRegionBandwidth"
---

Call the DeleteCenInterRegionBandwidth interface to delete the specified inter\-region bandwidth.

<span id=".6LCD6K-V"></span>
## Debug

[去调试](https://api.byteplus.com/api-explorer/?action=DeleteCenInterRegionBandwidth&groupName=%E5%9F%9F%E9%97%B4%E5%B8%A6%E5%AE%BD&serviceCode=cen&version=2020-04-01)


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters

The following only details request parameters specific to this API and key common parameters. More information can be found in [Common parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).



**Action ** <span data-label="purple">string </span><span data-api-tag="require|zwQ22M">必选</span> `Example value: DeleteCenInterRegionBandwidth`

The action to perform. Value: DeleteCenInterRegionBandwidth.



Version string Example: 2020\-04\-01

The API version. Value: 2020\-04\-01.



**InterRegionBandwidthId ** <span data-label="purple">string </span><span data-api-tag="require|npWMRm">必选</span> `Example value: cirb-3tex2x1cwd4c6c0v****`

Inter\-region bandwidth ID.

You can call the [DescribeCenInterRegionBandwidths](https://docs.byteplus.com/en/docs/cen/DescribeCenInterRegionBandwidths) interface to query the inter\-region bandwidth ID.



&nbsp;

<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters

This API does not have specific response parameters. For more information, see [Response structure](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response).

<span id=".6K-35rGC56S65L6L"></span>
## Request examples

```text
GET /?Action=DeleteCenInterRegionBandwidth&Version=2020-04-01&InterRegionBandwidthId=cirb-3tex2x1cwd4c6c0v**** HTTP/1.1
Host: cen.byteplusapi.com
X-Date: 20260109T083339Z
Authorization: HMAC-SHA256 Credential=Adfks******wekfwe/20260109/cn-beijing/cen/request, SignedHeaders=host;x-date, Signature=47a7d934ff7b37c03938******cd7b8278a40a1057690c401e92246a0e41085f


```


<span id=".6L-U5Zue56S65L6L"></span>
## Response examples

```json
{
  "ResponseMetadata": {
    "RequestId": "20250815172501100041013001719588",
    "Action": "DeleteCenInterRegionBandwidth",
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
|404 |InvalidInterRegionBandwidth.NotFound |The specified inter\-region bandwidth does not exist. |The specified inter\-region bandwidth does not exist. |
|409 |InvalidCen.InvalidStatus |The specified CEN instance is not in the correct status for the request. |The specified CEN instance is in a state that cannot respond to this request. Please try again later. |
|500 |InternalError |Request failed with internal server error. |Internal system error. |
