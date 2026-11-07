---
title: "ListTagsForResources - Querying the resource tags"
product: "PrivateLink"
product_code: "privatelink"
source: "https://docs.byteplus.com/en/docs/privatelink/ListTagsForResources"
---

Call the ListTagsForResources API to query the information of tags that meets specified conditions.

## Debug

[去调试](https://api.byteplus.com/api-explorer/debug?action=ListTagsForResources&serviceCode=privatelink&version=2020-04-01&groupName=)

## Request parameters

**Action ** String必选 `Example: ListTagsForResources`

Action to execute. Set the value to **ListTagsForResources**.

**Version ** String必选 `Example: 2020-04-01`

API version. The current version is **2020\-04\-01**.

**ResourceType ** String必选 `Example: endpointservice`

The resource type. Values:

* endpointservice: Endpoint service

* endpoint: Interface endpoint

* Gateway endpoint

**ResourceIds.N ** String`optional` `Example: epsvc-2fe630gurkl37k5gfuy33****`

The resource ID.

> **tip**

* > You can call the [DescribeVpcEndpointServices](https://docs.byteplus.com/en/docs/privatelink/DescribeVpcEndpointServices) API to obtain the resource ID of the **endpointservice** type.

* > You can call the [DescribeVpcEndpoints](https://docs.byteplus.com/en/docs/privatelink/DescribeVpcEndpoints) API to obtain the resource ID of the **endpoint** type.

* > You can call the [DescribeVpcGatewayEndpoints](https://docs.byteplus.com/en/docs/privatelink/DescribeVpcGatewayEndpoints) API to obtain the resource ID of the **gatewayendpoint** type.

* > N represents the serial number of the resource ID, ranging from 1 to 50.

* > Separate multiple resource IDs with ampersands (&).

**TagFilters.N.Key ** String`optional` `Example: k1`

The specified tag key when querying resources by tag.

Specifying multiple tag keys means querying the resources that contain all specified tag keys.

**NextToken ** String`optional` `Example: caeba0bbb2be03f84eb48b699f0a****`

The token to start the next query.

**MaxResults ** Integer`optional` `Example: 50`

The number of results per query. Default: 10. Maximum: 100.

**TagType ** String`optional` `Example: custom`

Tag type. Valid values:

* custom: Custom tag

* system: System tag.

* Leaving this parameter unset means querying all types of tags.

**TagFilters.N.Values.N ** String`optional` `Example: v1`

The specified tag value when querying resources by tag. Each tag key can have up to 3 tag values.

* If this parameter is not passed, it indicates that the query will retrieve endpoints or endpoint service instances associated with all tag values under the specified tag key.

* If this parameter is left empty, it indicates that the query will retrieve endpoints or endpoint service instances associated with the specified tag key where the tag value is empty.

* When multiple tag values are specified for the same tag key, it indicates that the query will retrieve the set of endpoints or endpoint service instances associated with each tag value.

> **tip**

> To provide this parameter, you must first provide `TagFilters.N.Key`.

## Response parameters

**RequestId ** String`Example: 2021062415303301022514515207C4****`

Request ID.

**NextToken ** String`Example: caeba0bbb2be03f84eb48b699f0a****`

The query token returned by this API call. An empty value indicates that there is no next page.

**ResourceTags ** Object[]`Example: -`

Resource and its associated tag information.

**ResourceType ** String`Example: CLB`

The resource type.

* endpointservice: Endpoint service

* endpoint: Interface endpoint

* Gateway endpoint

**ResourceId ** String`Example: epsvc-2fe6fszjgeznk5oxruv0u****`

The resource ID.

**TagKey ** String`Example: k1`

The key of a tag attached to the resource.

**TagValue ** String`Example: v1`

The value of a tag attached to the resource.

## Request examples

```JSON
GET /?Action=ListTagsForResources&Version=2020-04-01&ResourceType=endpointservice&ResourceIds.1=epsvc-2fe630gurkl37k5gfuy33****&TagFilters.1.Key=k1&NextToken=caeba0bbb2be03f84eb48b699f0a****&MaxResults=50&TagType=custom&TagFilters.1.Values.1=v1
Host: privatelink.cn-guangzhou.byteplusapi.com.cn
X-Date: 20251121T094038Z
Authorization: HMAC-SHA256 Credential=Adfks******wekfwe/20251121/cn-guangzhou/privatelink/request, SignedHeaders=host;x-date, Signature=47a7d934ff7b37c03938******cd7b8278a40a1057690c401e92246a0e41085f
```

## Response examples

```json
{
    "ResponseMetadata": {
        "RequestId": "2021062415303301022514515207C4****",
        "Action": "ListTagsForResources",
        "Version": "2020-04-01",
        "Service": "privatelink",
        "Region": "cn-guangzhou"
    },
    "Result": {
        "NextToken": "caeba0bbb2be03f84eb48b699f0a****",
        "ResourceTags": [
            {
                "ResourceType": "endpointservice",
                "ResourceId": "epsvc-273w3e33y2y9s7fap8u2j****",
                "TagKey": "k1",
                "TagValue": "v1"
            }
        ]
    }
}
```

## Error codes

This section displays only the error codes of the current API. For more error codes, see [Common error codes](https://docs.byteplus.com/en/docs/privatelink/Public-error-codes).

|Status code |Error codes |Error message |Notes |
|---|---|---|---|
|400 |MissingParameter |The request is missing a required parameter. Ensure that you have supplied all the required parameters for the request; for example, the 'XXX'. |This request is missing a required parameter. Ensure that your request includes all required parameters, such as XXX.<br><br>> **tip**<br><br><br>> Here, XXX represents the name of the missing parameter.<br> |
|400 |InvalidIncorrectOrder.Malformed |The specified index order is malformed. |The specified index order parameter format is invalid. |
|400 |InvalidMaxResult.Malformed |The specified MaxResult is malformed. |The specified MaxResult parameter format is invalid. |
|400 |InvalidNextToken.Malformed |The specified NextToken is malformed. |The specified NextToken parameter format is invalid. |
|400 |InvalidResourceType.Malformed |The specified ResourceType is malformed. |The specified ResourceType parameter format is invalid. |
|400 |InvalidTagKey.Malformed |The specified TagKey is malformed. |The specified TagKey parameter format is invalid. |
|400 |InvalidTagType.Malformed |The specified TagType is malformed. |The specified TagType parameter format is invalid. |
|400 |InvalidTagValue.Malformed |The specified TagValue is malformed. |The specified TagValue parameter format is invalid. |
|400 |LimitExceeded.Resource |You've reached the limit on the number of resources that you can operate at a time. |You have reached the maximum number of tags that can be processed in a single request. |
|400 |LimitExceeded.TagFilterKey |You've reached the limit on the number of tag keys that you can filter. |The maximum number of filter tag keys that can be specified in a single request has been reached. |
|400 |LimitExceeded.TagFilterValues |You've reached the limit on the number of tag values that you can filter. |The maximum tag key\-value pairs for filtering in a single request has been reached. |
|404 |InvalidResource.NotFound |The specified resource does not exist. |The specified resource does not exist. |
