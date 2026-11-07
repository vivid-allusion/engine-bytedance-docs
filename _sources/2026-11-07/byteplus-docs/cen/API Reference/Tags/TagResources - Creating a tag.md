---
title: "TagResources - Creating a tag"
product: "Cloud Enterprise Network"
product_code: "cen"
source: "https://docs.byteplus.com/en/docs/cen/TagResources"
---

Call the TagResources API to add custom tags to Cloud Enterprise Network (CEN) resources.

## Instructions

* ​​If multiple tags with the same key are applied to a resource, the most recent value overwrites any previous ones.​

* Each resource can have a maximum of 50 tags. Each call to this API can add up to 20 tags.

* In the table below, "N" in the Tags.N.a parameter represents the serial number of the tag information. It must be entered starting from 1 in numerical order, with a maximum limit of 20 entries per call. Separate multiple tags with ampersands (&). Each tag key pairs one tag value.

## Debug

[去调试](https://api.byteplus.com/api-explorer/?action=TagResources&groupName=%E6%A0%87%E7%AD%BE&serviceCode=cen&version=2020-04-01)

## Request parameters

The following only details request parameters specific to this API and key common parameters. More information can be found in [Common parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).

**Action ** string必选 `Example: TagResources`

Action to execute. Set the value to TagResources.

**Version ** string必选 `Example: 2020-04-01`

The API version. Value: 2020\-04\-01.

**Tags.N.Key ** string[]必选`Example: k1`

The tag key of the custom tag.

* Must be 1 to 128 characters.

* Case\-sensitive. Must not start with `volc:` or `sys:` in any case form.

* Must not start or end with a space.

* May include letters, numbers, spaces ( ), underscores (_), periods (.), half\-width colons (:), slashes (/), equal signs (=), plus signs (+), and at signs (@).

> Duplicate tag keys are not allowed for the same resource.

**Tags.N.Value ** string[]`optional` `Example: v1`

The tag value of the custom tag.

* The length limit is 0 to 256 characters.

* Case\-sensitive. Must not start or end with a space.

* May include letters, numbers, spaces ( ), underscores (_), periods (.), half\-width colons (:), slashes (/), equal signs (=), plus signs (+), minus signs (\-) and at signs (@).

**Resource type ** string必选 `Example: cen`

The resource type. Values:

* cen: CEN instance.

* cenbandwidthpackage: Bandwidth package.

**ResourceIds.N ** string[]必选 `Example: cen-273w3e33y2y9s7fap8u2j****`

The resource ID.

* You can call the [DescribeCens](https://docs.byteplus.com/en/docs/cen/DescribeCens) API to query the resource ID of the "cen" type.

* You can call the [DescribeCenBandwidthPackages](https://docs.byteplus.com/en/docs/cen/DescribeCenBandwidthPackages) API to query the resource ID of the "cenbandwidthpackage" type.

* Parameter \- N: Represents the serial number of a resource ID. A maximum of 50 IDs can be specified per single API call.

* Separate multiple CEN resource IDs with ampersands (&).

## Response parameters

This API does not have specific response parameters. For more information, see [Response structure](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response).

## Request examples

```text
GET /?Action=TagResources&Version=2020-04-01&ResourceType=cen&ResourceIds.1=cen-273w3e33y2y9s7fap8u2j**** HTTP/1.1
Host: cen.byteplusapi.com
X-Date: 20260109T082150Z
Authorization: HMAC-SHA256 Credential=Adfks******wekfwe/20260109/cn-beijing/cen/request, SignedHeaders=host;x-date, Signature=47a7d934ff7b37c03938******cd7b8278a40a1057690c401e92246a0e41085f


```

## Response examples

```json
{
    "ResponseMetadata": {
        "RequestId": "2021062415303301022514515207C4****",
        "Action": "TagResources",
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
|400 |InvalidTagValue.Malformed |The specified parameter tag value is invalid. |The tag value is invalid. |
|400 |LimitExceeded.Tags |You've reached the limit on the number of tags that you can operate at a time. |You have reached the maximum of tags that can be processed in a single request. |
|400 |LimitExceeded.Resource |You've reached the limit on the number of resources that you can operate at a time. |You have reached the maximum number of tags that can be processed in a single request. |
|400 |InvalidResourceType.Malformed |The specified parameter resource type is invalid. |The resource type is invalid. |
|400 |QuotaExceeded.ResourceTags |You've reached the limit on the number of resource tags that you can create. |You have reached the maximum number of custom tags that you can add to a single resource. |
|400 |QuotaExceeded.ResourceSystemTags |You've reached the limit on the number of system tags that you can create. |You have reached the maximum number of system tags that you can add to a single resource. |
|400 |InvalidTag.Disorder |The specified index order of tag is malformed. |The index order format of the specified tag is invalid. |
|404 |InvalidResource.NotFound |The specified resource does not exist. |The specified resource does not exist. |
|500 |InternalError |Request failed with internal server error. |Internal system error. |
