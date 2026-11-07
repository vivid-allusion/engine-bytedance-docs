---
title: "ListTagsForResources - Querying the resource tag list"
product: "Cloud Load Balancer"
product_code: "clb"
source: "https://docs.byteplus.com/en/docs/clb/ALB-ListTagsForResources"
---

Call the ListTagsForResources API to query the list of resource tag.

## Instructions

Submit up to 50 API requests per second.

## Debug

[去调试](https://api.byteplus.com/api-explorer/?action=ListTagsForResources&groupName=%E6%A0%87%E7%AD%BE&serviceCode=alb&version=2020-04-01)

## Request parameters

The following only details request parameters specific to this API and key common parameters. More information can be found in [Common parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).

**Action ** string必选 `Example: ListTagsForResources`

The action to perform. Value: ListTagsForResources.

**Version ** string必选 `Example: 2020-04-01`

The API version. Value: 2020\-04\-01.

**ResourceType ** string必选 `Example: loadbalancer`

The resource type. Valid values:

* loadbalancer: CLB instance.

* listener

* servergroup: Backend server group.

* certificate

* acl: Access Control List.

* healthchecktemplate: Health check template.

* customizedcfg: The custom configuration.

**ResourceIds.N ** string[]`optional` `Example: ResourceIds.1=alb-273sdsdsxxxxxp8u2j****&ResourceIds.2=alb-2fe6fszjgeznk5oxruv0u****`

The resource ID.

* Parameter \- N: Represents the serial number of a resource ID. A maximum of 50 IDs can be specified per single API call.

* Separate multiple resource IDs with ampersands (&).

**TagFilters.N.Key ** string[]`optional` `Example: TagFilters.1.Key=k1&TagFilters.2.Key=k2`

The specified tag key when querying resources by tag. Parameter \- N: Represents the serial number of a tag key. A maximum of 10 IDs can be specified per single API call. Separate multiple tag keys with ampersands ( & ). When multiple tag keys are specified, it means to query resources that contain all of the specified tag keys simultaneously.

**TagFilters.N.Values.N ** string[]`optional` `Example: TagFilters.1.Values.1=v1&TagFilters.2.Values.1=v4`

Tag value of a resource. Each tag key can have up to 3 tag values. When this parameter is not passed, it means to query resources associated with tags corresponding to all tag values under the specified tag key. When multiple tag values are specified for the same tag key, it means to query the union of resources associated with the tags corresponding to each tag value.

> To provide this parameter, you must first provide TagFilters.N.Key.

**MaxResults ** integer`optional` `Example: 10`

The number of results to return per query. Default: 10, Maximum: 100.

**NextToken ** string`optional` `Example: OTk5OTk5OQ==`

Pagination token used to mark the position in paginated results. Leave this empty for the initial API call. For subsequent queries, set this value to the NextToken parameter returned by the previous API call.

## Response parameters

Only the response parameters specific to this API are listed below. More information, see [Response structure](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response).

**RequestId ** string`Example: 2021062415303301022514515207C4****`

Request ID.

**NextToken ** string`Example: OTk5OTk5OQ==`

The query token returned by this API call. An empty value indicates that there is no next page.

**ResourceTags ** object[]`Example: --`

Resource and its associated tag information.

**ResourceID ** string`Example: alb-2e0b1cayeha81fi56*****`

The resource ID.

**ResourceType ** string`Example: listener`

The resource type.

**TagKey ** string`Example: K1`

The key of the tag attached to the resource.

**TagValue ** string`Example: Val1`

The value of the tag attached to the resource.

## Request examples

```text
GET /?Action=ListTagsForResources&Version=2020-04-01&ResourceType=loadbalancer&ResourceIds.1=alb-2e0b1cayeha81fi56cp*****&ResourceIds.2=alb-1tzhdsteithq84gwgtb***** HTTP/1.1
Host: alb.cn-beijing.byteplusapi.com.cn
X-Date: 20251121T094038Z
Authorization: HMAC-SHA256 Credential=Adfks******wekfwe/20251121/cn-beijing/alb/request, SignedHeaders=host;x-date, Signature=47a7d934ff7b37c03938******cd7b8278a40a1057690c401e92246a0e41085f
```

## Response examples

```text
{
    "ResponseMetadata": {
        "RequestId": "2024062415303301022514515207C4****",
        "Action": "ListTagsForResources",
        "Version": "2020-04-01",
        "Service": "alb",
        "Region": "cn-beijing"
    },
    "Result": {
        "RequestId": "2024062415303301022514515207C4****",
        "NextToken": "hj4l32hj4gjvgo430f5****",
        "ResourceTags": [
            {
                "ResourceType": "loadbalancer",
                "ResourceID": "alb-2e0b1cayeha81fi56cp*****",
                "TagKey": "k1",
                "TagValue": "v1"
            },
            {
                "ResourceType": "loadbalancer",
                "ResourceID": "alb-1tzhdsteithq84gwgtb*****",
                "TagKey": "k2",
                "TagValue": "v2"
            }
        ]
    }
}
```

## Error codes

The following table lists the error codes related to the business logic for this API. For details, see [Common error codes](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-error-codes).

|Status code |Error codes |Error message |Notes |
|---|---|---|---|
|400 |InvalidParameter |Data unmarshal failed. |Failed to parse the request. |
|400 |MissingParameter |The request is missing a required parameter. Ensure that you have supplied all the required parameters for the request; for example, '%s'. |This request is missing a required parameter. Ensure that your request includes all required parameters, such as: %s. |
|400 |Invalid%s.Malformed |MismatchThe specified %s is malformed. |The specified %s parameter format is invalid. |
|400 |InvalidTags.Value.Malformed |The specified Tags.Value is malformed. |The specified Tags.Value parameter format is invalid. |
|400 |InvalidTags.Key.Malformed |The specified Tags.Key is malformed. |The specified Tags.Key parameter format is invalid. |
|400 |LimitExceed.Resource |You've reached the limit on the number of resources that you can operate at a time. |The maximum number of resources that can be operated on in a single request has been reached. |
|400 |InvalidMaxResults.Malformed |The specified MaxResults is malformed. |The specified MaxResults parameter format is invalid. |
|400 |MissingParameter |The request is missing a required parameter. Ensure that you have supplied all the required parameters for the request; for example, 'ResourceType'. |This request does not contain required parameters. Please ensure your request includes all required parameters, such as ResourceType. |
|400 |InvalidResourceType.Malformed |The specified ResourceType is malformed. |The specified ResourceType format is invalid. |
|400 |InvalidTagFilters.Key.Malformed |The specified TagFilters.Key is malformed. |The specified TagFilters.Key parameter format is invalid. |
|400 |LimitExceed.TagFilters.Values |You've reached the limit on the number of tag filter values that you can operate at a time. |You have reached the maximum number of tag values that can be operated on in a single request. |
|400 |LimitExceed.TagFilters |You've reached the limit on the number of tag filters that you can operate at a time. |The maximum number of tag filters that can be operated on at one time has been reached. |
|500 |InternalError |An internal error has occurred. |An internal error occurred. Please try again later or contact an engineer for further consultation. |
