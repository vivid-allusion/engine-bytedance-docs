---
title: "UntagResources - Deleting a custom tag from resources"
product: "Cloud Load Balancer"
product_code: "clb"
source: "https://docs.byteplus.com/en/docs/clb/ALB-UntagResources"
---

Call the UntagResources API to delete custom tags from resources.

<span id=".5L2_55So6K-05piO"></span>
## Instructions

Submit up to 5 API requests per second.

<span id=".6LCD6K-V"></span>
## Debug

[去调试](https://api.byteplus.com/api-explorer/?action=UntagResources&groupName=%E6%A0%87%E7%AD%BE&serviceCode=alb&version=2020-04-01)


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters

The following only details request parameters specific to this API and key common parameters. More information can be found in [Common parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).



**Action ** <span data-label="purple">string </span><span data-api-tag="require|uCOcFU">必选</span> `Example: UntagResources`

The action to perform. Value: UntagResources.



**Version ** <span data-label="purple">string </span><span data-api-tag="require|AUUqdq">必选</span> `Example: 2020-04-01`

The API version. Value: 2020\-04\-01.



**ResourceIds.N ** <span data-label="purple">string[] </span><span data-api-tag="require|Ur1rWS">必选</span> `Example: ResourceIds.1=alb-273sdsdsxxxxxp8u2j****&ResourceIds.2=alb-2fe6fszjgeznk5oxruv0u****`

The resource ID.


* Parameter \- N: Represents the serial number of a resource ID. A maximum of 50 IDs can be specified per single API call.

* Separate multiple resource IDs with ampersands (&).



**ResourceType ** <span data-label="purple">string </span><span data-api-tag="require|MRcELS">必选</span> `Example: loadbalancer`

The resource type. Valid values:


* loadbalancer: CLB instance.

* listener

* servergroup: Backend server group.

* certificate

* acl: Access Control List.

* healthchecktemplate: Health check template.

* customizedcfg: The custom configuration.



**TagKeys.N ** <span data-label="purple">string[] </span><span data-api-tag="require|MjNXvH">必选</span> `Example: TagKeys.1=k1&TagKeys.2=k2`

Tag keys of the tags to be deleted. The specific rules are as follows:


* Must not start or end with a space.

* Parameter \- N: Represents the serial number of a tag key. A maximum of 50 IDs can be specified per single API call. Separate multiple tag keys with ampersands (&).



&nbsp;

<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters

Only the response parameters specific to this API are listed below. More information, see [Response structure](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response).



**RequestId ** <span data-label="purple">string </span>`Example: 2021062415303301022514515207C4****`

Request ID.



&nbsp;

<span id=".6K-35rGC56S65L6L"></span>
## Request examples

```text
GET /?Action=UntagResources&ResourceType=loadbalancer&ResourceIds.1=alb-r1rvlqgt58u83dvb46c1j2fi&TagKeys.1=yxl12&Version=2020-04-01&AccountId=2100052283" -H "X-Top-Account-Id: 2100052283"
Host: alb.cn-beijing.byteplusapi.com.cn
X-Date: 20251121T094038Z
Authorization: HMAC-SHA256 Credential=Adfks******wekfwe/20251121/cn-beijing/alb/request, SignedHeaders=host;x-date, Signature=47a7d934ff7b37c03938******cd7b8278a40a1057690c401e92246a0e41085f
```


<span id=".6L-U5Zue56S65L6L"></span>
## Response examples

```text
{
    "ResponseMetadata": {
        "RequestId": "94f928f1-0033-4ff2-b407-d91b56282967",
        "Action": "UntagResources",
        "Version": "2020-04-01"
    },
    "Result": {
        "RequestId": "94f928f1-0033-4ff2-b407-d91b56282967"
    }
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error codes

The following table lists the error codes related to the business logic for this API. For details, see [Common error codes](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-error-codes).


|Status code |Error codes |Error message |Notes |
|---|---|---|---|
|400 |Invalid%s.Malformed |MismatchThe specified %s is malformed. |The specified %s parameter format is invalid. |
|400 |MissingParameter |The request is missing a required parameter. Ensure that you have supplied all the required parameters for the request; for example, '%s'. |This request is missing a required parameter. Please ensure the request includes all required parameters, such as: %s. |
|400 |InvalidParameter |Data unmarshal failed. |Failed to parse the request. |
|400 |LimitExceed.TagKey |You've reached the limit on the number of tag keys that you can operate at a time. |You have reached the maximum number of tag keys that can be operated on in a single request. |
|400 |LimitExceed.Resource |You've reached the limit on the number of resources that you can operate at a time. |The maximum number of resources that can be operated on in a single request has been reached. |
|400 |InvalidResourceType.Malformed |The specified ResourceType is malformed. |The specified ResourceType format is invalid. |
|400 |MissingParameter |The request is missing a required parameter. Ensure that you have supplied all the required parameters for the request; for example, 'TagKeys'. |This request is missing a required parameter. Please ensure your request includes all required parameters, such as TagKeys. |
|400 |InvalidTagKeys.Malformed |The specified TagKeys is malformed. |The specified TagKeys parameter format is invalid. |
|404 |InvalidResource.NotFound |The specified Resource does not exist. |The specified resource does not exist. |
|500 |InternalError |An internal error has occurred. |An internal error occurred. Please try again later or contact an engineer for further consultation. |
