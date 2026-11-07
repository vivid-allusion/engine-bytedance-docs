---
title: "TagResources - Adding the custom tags to resources"
product: "Cloud Load Balancer"
product_code: "clb"
source: "https://docs.byteplus.com/en/docs/clb/ALB-TagResources"
---

Call the TagResources API to add custom tags to resources.

## Instructions

Submit up to 5 API requests per second.

## Debug

[去调试](https://api.byteplus.com/api-explorer/?action=TagResources&groupName=%E6%A0%87%E7%AD%BE&serviceCode=alb&version=2020-04-01)

## Request parameters

The following only details request parameters specific to this API and key common parameters. More information can be found in [Common parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).

**Action ** string必选 `Example: TagResources`

Action to execute. Set the value to TagResources.

**Version ** string必选 `Example: 2020-04-01`

The API version. Value: 2020\-04\-01.

**ResourceIds.N ** string[]必选 `Example: ResourceIds.1=alb-273sdsdsxxxxxp8u2j****&ResourceIds.2=alb-2fe6fszjgeznk5oxruv0u****`

The resource ID.

* Parameter \- N: Represents the serial number of a resource ID. A maximum of 50 IDs can be specified per single API call.

* Separate multiple resource IDs with ampersands (&).

**ResourceType ** string必选 `Example: loadbalancer`

The resource type. Valid values:

* loadbalancer: CLB instance.

* listener

* servergroup: Backend server group.

* certificate

* acl: Access Control List.

* healthchecktemplate: Health check template.

* customizedcfg: The custom configuration.

**Tags.N.Key ** string[]必选 `Example: Tags.1.Key=k1&Tags.2.Key=k2`

The tag key. Rules:

* Must be 1 to 128 characters.

* Case\-sensitive, cannot start with any case combination of "volc:".

* Must not start or end with a space.

* May include characters (any language), numbers, spaces ( ), underscores (_), periods (.), half\-width colons (:), slashes (/), equal signs (=), plus signs (+), minus signs (\-) and at signs (@).

* Duplicate tag keys are not allowed for the same resource.

**Tags.N.Value ** string[]必选 `Example: Tags.1.Value=v1&Tags.2.Value=v2`

The tag value. The specific rules are as follows:

* The length limit is 0 to 256 characters.

* Case\-sensitive. Must not start or end with a space.

* May include characters (any language), numbers, spaces ( ), underscores (_), periods (.), half\-width colons (:), slashes (/), equal signs (=), plus signs (+), minus signs (\-) and at signs (@).

* To provide this parameter, provide Tags.N.Key first.

## Response parameters

Only the response parameters specific to this API are listed below. More information, see [Response structure](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response).

**RequestId ** string`Example: 2021062415303301022514515207C4****`

Request ID.

## Request examples

```text
GET /?Action=TagResources&Version=2020-04-01&ResourceIds.1=ResourceIds.1%3Dalb-273sdsdsxxxxxp8u2j****%26ResourceIds.2%3Dalb-2fe6fszjgeznk5oxruv0u****&ResourceType=loadbalancer HTTP/1.1
Host: alb.cn-beijing.byteplusapi.com.cn
X-Date: 20261027T124457Z
Authorization: HMAC-SHA256 Credential=Adfks******wekfwe/20261027/cn-beijing/alb/request, SignedHeaders=host;x-date, Signature=47a7d934ff7b37c03938******cd7b8278a40a1057690c401e92246a0e41085f
```

## Response examples

```text
{
    "ResponseMetadata": {
        "RequestId": "a295610f-5602-4ba8-ab73-84158c7b5dd7",
        "Action": "TagResources",
        "Version": "2020-04-01"
    },
    "Result": {
        "RequestId": "a295610f-5602-4ba8-ab73-84158c7b5dd7"
    }
}
```

## Error codes

The following table lists the error codes related to the business logic for this API. For details, see [Common error codes](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-error-codes).

|Status code |Error codes |Error message |Notes |
|---|---|---|---|
|400 |Invalid%s.Malformed |MismatchThe specified %s is malformed. |The specified %s parameter format is invalid. |
|400 |MissingParameter |The request is missing a required parameter. Ensure that you have supplied all the required parameters for the request; for example, '%s'. |This request is missing a required parameter. Please ensure the request includes all required parameters, such as: %s. |
|400 |InvalidParameter |Data unmarshal failed. |Failed to parse the request. |
|400 |LimitExceed.Tag |You've reached the limit on the number of tags that you can operate at a time. |You have reached the maximum number of tags that can be operated on in a single request. |
|400 |InvalidResourceType.Malformed |The specified ResourceType is malformed. |The specified ResourceType format is invalid. |
|400 |LimitExceed.Resource |You've reached the limit on the number of resources that you can operate at a time. |The maximum number of resources that can be operated on in a single request has been reached. |
|400 |MissingParameter |The request is missing a required parameter. Ensure that you have supplied all the required parameters for the request; for example, 'Tags'. |This request is missing a required parameter. Please ensure the request includes all required parameters, such as Tags. |
|400 |InvalidIndexOrder.Malformed |The specified index order is malformed. |The specified index order parameter format is invalid. |
|400 |InvalidTags.Key.Malformed |The specified Tags.Key is malformed. |The specified Tags.Key parameter format is invalid. |
|400 |InvalidTags.Value.Malformed |The specified Tags.Value is malformed. |The specified Tags.Value parameter format is invalid. |
|400 |InvalidTags.Key.Duplicated |The specified Tags.Key is duplicated. |The specified Tags.Key is duplicated. |
|404 |InvalidResource.NotFound |The specified Resource does not exist. |The specified resource does not exist. |
|500 |InternalError |An internal error has occurred. |An internal error occurred. Please try again later or contact an engineer for further consultation. |
