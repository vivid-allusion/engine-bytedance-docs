---
title: "UntagResources - Deleting a tag"
product: "Cloud Enterprise Network"
product_code: "cen"
source: "https://docs.byteplus.com/en/docs/cen/UntagResources"
---

Call the UntagResources API to delete custom tags from Cloud Enterprise Network (CEN) resources.

## Debug

[去调试](https://api.byteplus.com/api-explorer/?action=UntagResources&groupName=%E6%A0%87%E7%AD%BE&serviceCode=cen&version=2020-04-01)

## Request parameters

The following only details request parameters specific to this API and key common parameters. More information can be found in [Common parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).

**Action ** string必选 `Example: UntagResources`

Action to execute. Set the value to UntagResources.

**Version ** string必选 `Example: 2020-04-01`

The API version. Value: 2020\-04\-01.

**TagKeys.N ** string[]必选 `Example: k1`

The key of the custom tag to be deleted from the CEN resource.

* Parameter \- N: Represents the serial number of a Tag key. A maximum of 20 IDs can be specified per single API call.

* Separate multiple Tag keys with ampersands (&).

**ResourceType ** string必选 `Example: cen`

The CEN resource. Values:

* cen: Indicates a CEN instance.

* cenbandwidthpackage: Indicates a bandwidth package.

**ResourceIds.N ** string[]必选 `Example: cen-273w3e33y2y9s7fap8u2j****`

ID of the CEN resource.

* You can call the [DescribeCens](https://docs.byteplus.com/en/docs/cen/DescribeCens) API to query the resource ID of the "cen" type.

* You can call the [DescribeCenBandwidthPackages](https://docs.byteplus.com/en/docs/cen/DescribeCenBandwidthPackages) API to query the resource ID of the "cenbandwidthpackage" type.

* Parameter \- N: Represents the serial number of a resource ID. A maximum of 50 IDs can be specified per single API call.

* Separate multiple CEN resource IDs with ampersands (&).

## Response parameters

This API does not have specific response parameters. For more information, see [Response structure](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response).

## Request examples

```text
GET /?Action=UntagResources&Version=2020-04-01&TagKeys.1=k1&ResourceType=cen&ResourceIds.1=cen-273w3e33y2y9s7fap8u2j**** HTTP/1.1
Host: cen.byteplusapi.com
X-Date: 20260109T082453Z
Authorization: HMAC-SHA256 Credential=Adfks******wekfwe/20260109/cn-beijing/cen/request, SignedHeaders=host;x-date, Signature=47a7d934ff7b37c03938******cd7b8278a40a1057690c401e92246a0e41085f


```

## Response examples

```json
{
    "ResponseMetadata": {
        "RequestId": "2021062415303301022514515207C4****",
        "Action": "UntagResources",
        "Version": "2020-04-01",
        "Service": "cen",
        "Region": "cn-beijing"
    },
    "Result": {}
}
```

## Error codes

The table below describes the error codes for this API that are associated with business logic. For details, see [Common error codes](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-error-codes).

|Status code |Error codes |Error message |Notes |
|---|---|---|---|
|400 |MissingParameter |The request is missing a required parameter. Ensure that you have supplied all the required parameters for the request. |This request does not contain required parameters. Ensure all required parameters are provided when initiating the request. |
|400 |InvalidParameter |A parameter specified in the request is not valid, is unsupported or cannot be used. |The request contains invalid or unsupported parameters. |
|400 |InvalidTagKey.Malformed |The specified parameter tag key is invalid. |The tag key is invalid. |
|400 |LimitExceeded.Tags |You've reached the limit on the number of tags that you can operate at a time. |You have reached the maximum of tags that can be processed in a single request. |
|400 |LimitExceeded.Resource |You've reached the limit on the number of resources that you can operate at a time. |You have reached the maximum number of tags that can be processed in a single request. |
|400 |InvalidResourceType.Malformed |The specified parameter resource type is invalid. |The resource type is invalid. |
|404 |InvalidResource.NotFound |The specified resource does not exist. |The specified resource does not exist. |
|500 |InternalError |Request failed with internal server error. |Internal system error. |
