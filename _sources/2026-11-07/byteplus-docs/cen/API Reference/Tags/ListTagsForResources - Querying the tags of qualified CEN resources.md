---
title: "ListTagsForResources - Querying the tags of qualified CEN resources"
product: "Cloud Enterprise Network"
product_code: "cen"
source: "https://docs.byteplus.com/en/docs/cen/ListTagsForResources"
---

Call the ListTagsForResources API to query tags of Cloud Enterprise Network (CEN) resources that meet specified conditions.

## Debug

[去调试](https://api.byteplus.com/api-explorer/?action=ListTagsForResources&groupName=%E6%A0%87%E7%AD%BE&serviceCode=cen&version=2020-04-01)

## Request parameters

The following only details request parameters specific to this API and key common parameters. More information can be found in [Common parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).

**Action ** string必选 `Example: ListTagsForResources`

Action to execute. Set the value to ListTagsForResources.

**Version ** string必选 `Example: 2020-04-01`

The API version. Value: 2020\-04\-01.

**ResourceType ** string必选 `Example: cen`

The CEN resource. Values:

* cen: CEN instance.

* cenbandwidthpackage: Bandwidth package.

**ResourceIds.N ** string[]`optional` `Example: cen-273w3e33y2y9s7fap8u2j****`

CEN resource ID.

* You can call the [DescribeCens](https://docs.byteplus.com/en/docs/cen/DescribeCens) API to query the resource ID of the "cen" type.

* You can call the [DescribeCenBandwidthPackages](https://docs.byteplus.com/en/docs/cen/DescribeCenBandwidthPackages) API to query the resource ID of the "cenbandwidthpackage" type.

* Parameter \- N: Represents the serial number of a resource ID. A maximum of 50 IDs can be specified per single API call.

* Separate multiple CEN resource IDs with ampersands (&).

**NextToken ** string`optional` `Example: caeba0bbb2be03f84eb48b699f0a****`

The token to start the next query.

**MaxResults ** integer`optional` `Example: 50`

The number of results to return per query. Default: 10, Maximum: 100.

**TagFilters.N.Key ** string[]`optional` `Example: k1`

The tag key.

* N specifies the serial number of the tag key. Valid values: 1\-10.

* Separate multiple tag keys with ampersands (&). Multiple tag keys have a logical AND relationship. The query returns resources tagged with all the specified keys.

* The tag key must be unique.

**TagFilters.N.Values.N ** string[]`optional` `Example: v1`

The tag value.

* The first N specifies the serial number of a tag key. Valid values: 1–10.

* The second N represents the serial number of the tag value. Valid values: 1–3. The relationship between multiple tag values for the same tag key is a logical "OR". That is, the query returns resources tagged with any one of the specified values for that key.

* Separate multiple tag values with ampersands (&).

* To provide this parameter, provide `TagFilters.N.Key` first.

* Passing an empty string queries for resources with an empty tag value.

**TagType ** string`optional` `Example: custom`

Tag type. Valid values:

* custom: Custom tag

* system: System tag.

* Leaving this parameter unset means querying all types of tags.

## Response parameters

The following only details response parameters specific to this API. More information, see [Response structure](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response).

**NextToken ** string`Example: caeba0bbb2be03f84eb48b699f0a****`

Determine whether there is a token to start the next query based on NextToken.

* If NextToken is empty, it indicates there is no next query.

* If NextToken has a value, that value is the token to start the next query.

**ResourceTags ** object[]`Example: -`

Resource and its associated tag information.

**ResourceType ** string`Example: cen`

The type of CEN resource.

* cen: Represents a CEN instance.

* cenbandwidthpackage: Represents a CEN bandwidth package.

**TagKey ** string`Example: k1`

The tag key attached to the CEN resource.

**TagValue ** string`Example: v1`

The tag value attached to the CEN resource.

**ResourceId ** string`Example: cen-273w3e33y2y9s7fap8u2j****`

CEN resource ID.

## Request examples

```text
GET /?Action=ListTagsForResources&Version=2020-04-01&ResourceType=cen&ResourceIds.1=cen-273w3e33y2y9s7fap8u2j****&NextToken=caeba0bbb2be03f84eb48b699f0a****&MaxResults=50&TagFilters.1.Key=k1&TagFilters.1.Values.1=v1&TagType=custom HTTP/1.1
Host: cen.byteplusapi.com
X-Date: 20250815T082933Z
Authorization: HMAC-SHA256 Credential=Adfks******wekfwe/20250815/cn-beijing/cen/request, SignedHeaders=host;x-date, Signature=47a7d934ff7b37c03938******cd7b8278a40a1057690c401e92246a0e41085f


```

## Response examples

```json
{
  "ResponseMetadata": {
    "RequestId": "2025081516293801307203013704D858",
    "Action": "ListTagsForResources",
    "Version": "2020-04-01",
    "Service": "cen",
    "Region": "cn-beijing"
  },
  "Result": {
    "NextToken": "caeba0bbb2be03f84eb48b699f0a****",
    "ResourceTags": [
      {
        "ResourceType": "cen",
        "TagKey": "k1",
        "TagValue": "v1",
        "ResourceId": "cen-273w3e33y2y9s7fap8u2j****"
      }
    ]
  }
}
```

## Error codes

The table below describes the error codes for this API that are associated with business logic. For details, see [Common error codes](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-error-codes).

|Status code |Error codes |Error message |Notes |
|---|---|---|---|
|400 |MissingParameter |The request is missing a required parameter. Ensure that you have supplied all the required parameters for the request. |This request does not contain required parameters. Ensure all required parameters are provided when initiating the request. |
|400 |InvalidParameter |A parameter specified in the request is not valid, is unsupported or cannot be used. |The request contains invalid or unsupported parameters. |
|400 |LimitExceeded.Resource |You've reached the limit on the number of resources that you can operate at a time. |You have reached the maximum number of tags that you can manage in a single request. |
|400 |InvalidResourceType.Malformed |The specified parameter resource type is invalid. |The resource type is invalid. |
|400 |InvalidTagType.Malformed |The specified parameter tag type is invalid. |The tag type is invalid. |
|400 |InvalidTagFilterKey.Malformed |The specified parameter tag filter key is invalid. |The tag filter key is invalid. |
|400 |InvalidTagFilterValue.Malformed |The specified parameter tag filter value is invalid. |The tag filter value is invalid. |
|400 |LimitExceeded.TagFilterKey |You've reached the limit on the number of tag keys that you can filter. |You have reached the maximum number of tag keys that you can specify for filtering in a single request. |
|400 |LimitExceeded.TagFilterValue |You've reached the limit on the number of tag values that you can filter. |You have reached the maximum number of tag values that you can specify for filtering in a single request. |
|400 |InvalidNextToken.Malformed |The specified parameter NextToken is invalid. |The NextToken queried is invalid. |
|400 |InvalidMaxResults.Malformed |The specified parameter MaxResults is malformed. |The number of query results is invalid. |
|400 |InvalidTagFilter.Disorder |The specified index order of tag filter is malformed. |The index order format of the specified tag filter is invalid. |
|404 |InvalidResource.NotFound |The specified resource does not exist. |The specified resource does not exist. |
|500 |InternalError |Request failed with internal server error. |Internal system error. |
