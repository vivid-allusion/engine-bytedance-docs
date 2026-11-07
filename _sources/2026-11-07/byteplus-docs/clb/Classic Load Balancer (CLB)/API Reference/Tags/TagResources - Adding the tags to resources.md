---
title: "TagResources - Adding the tags to resources"
product: "Cloud Load Balancer"
product_code: "clb"
source: "https://docs.byteplus.com/en/docs/clb/TagResources"
---

Call the TagResources API to add custom tags to resources.

## Instructions

* If a tag with the same key is added repeatedly to the same resource, the newly added value will overwrite the previous value.

* Each resource can have up to 50 custom tags added, and each call to this API can add up to 20 custom tags.

* In parameters of the type Tags.N.a, N represents the sequence number of the tag information, which must be filled in numerical order starting from 1, with a value range of 1 to 20. Separate multiple tags with ampersands (&).

## Debug

[去调试](https://api.byteplus.com/api-explorer/debug?action=TagResources&serviceCode=clb&version=2020-04-01&groupName=)

## Request parameters

**Action ** String必选 `Example: TagResources`

Action to execute. Set the value to **TagResources**.

**Version ** String必选 `Example: 2020-04-01`

API version. The current version is **2020\-04\-01**.

**ResourceType ** String必选 `Example: clb`

The resource type. Values:

* clb: CLB instance.

* listener

* servergroup: Backend server group.

* acl: Access control.

* certificate

**ResourceIds.N ** String必选`Example: clb-273sdsdsxxxxxp8u2j****`

The resource ID.

* Parameter \- N: Represents the serial number of a resource ID. A maximum of 50 IDs can be specified per single API call.

* Separate multiple resource IDs with ampersands (&).

* You can call the following API to obtain the resource ID:

   * [DescribeLoadBalancers](https://docs.byteplus.com/en/docs/clb/DescribeLoadBalancers)

   * [DescribeListeners](https://docs.byteplus.com/en/docs/clb/DescribeListeners)

   * [DescribeServerGroups](https://docs.byteplus.com/en/docs/clb/DescribeServerGroups)

   * [DescribeAcls](https://docs.byteplus.com/en/docs/clb/DescribeAcls)

   * [DescribeCertificates](https://docs.byteplus.com/en/docs/clb/DescribeCertificates)

**Tags.N.Key ** String必选 `Example: k1`

The tag key of the custom tag.

* Must be 1 to 128 characters.

* Case\-sensitive. Must not start with `volc:` or `sys:` in any case form.

* Must not start or end with a space.

* May include characters (any language), numbers, spaces ( ), underscores (_), periods (.), half\-width colons (:), slashes (/), equal signs (=), plus signs (+), minus signs (\-) and at signs (@).

> Duplicate tag keys are not allowed for the same resource. If the applied `Tags.N.Key` duplicates an existing tag key, the most recent tag overwrites any previous ones.​

**Tags.N.Value ** String`optional` `Example: v1`

The tag value of the custom tag.

* Must be 1 to 256 characters.

* Case\-sensitive. Must not start or end with a space.

* May include characters (any language), numbers, spaces ( ), underscores (_), periods (.), half\-width colons (:), slashes (/), equal signs (=), plus signs (+), minus signs (\-) and at signs (@).

> To provide this parameter, provide `Tags.N.Key` first.

## Response parameters

**RequestId ** String`Example: 2021062415303301022514515207C4****`

Request ID.

## Request examples

```json
GET /?Action=TagResources&Version=2020-04-01&ResourceType=clb&ResourceIds.1=clb-273sdsdsxxxxxp8u2j****&Tags.1.Key=k1&Tags.1.Value=v1
Host: clb.cn-beijing.byteplusapi.com.cn
X-Date: 20251121T094038Z
Authorization: HMAC-SHA256 Credential=Adfks******wekfwe/20251121/cn-beijing/clb/request, SignedHeaders=host;x-date, Signature=47a7d934ff7b37c03938******cd7b8278a40a1057690c401e92246a0e41085f
```

## Response examples

```json
{
    "ResponseMetadata": {
        "RequestId": "20230604110420****100232280022D31",
        "Action": "TagResources",
        "Version": "2020-04-01",
        "Service": "clb",
        "Region": "cn-beijing"
    },
    "Result": {
        "RequestId": "2021062415303301022514515207C4****"
    }
}
```

## Error codes

This section displays only the error codes of the current API. For more error codes, see [Common error codes](https://docs.byteplus.com/en/docs/clb/Public-error-codes).

|Status code |Error codes |Error message |Notes |
|---|---|---|---|
|400 |InvalidDefaultRule.UnSupportAction |The specified Default Rule does not support this action. |The specified default forwarding rule does not support the current action. |
|400 |InvalidIncorrectOrder.Malformed |The specified index order is malformed. |The specified index order parameter format is invalid. |
|400 |InvalidResourceType.Malformed |The specified ResourceType is malformed. |The specified ResourceType format is invalid. |
|400 |InvalidTagKey.Malformed |The specified TagKey is malformed. |The specified TagKey parameter format is invalid. |
|400 |InvalidTagValue.Malformed |The specified TagValue is malformed. |The specified TagValue parameter format is invalid. |
|400 |LimitExceeded.Resource |You've reached the limit on the number of resources that you can operate at a time. |You have reached the maximum number of tags that can be processed in a single request. |
|400 |LimitExceeded.ServiceManagedTag |You've reached the limit on the number of service managed tags that you can create. |You have reached the limit for the number of managed resource tag key\-value pairs that can be created in a single request. |
|400 |LimitExceeded.TagOperation |You've reached the limit on the number of tags that you can operate at a time. |You have reached the maximum number of tag entries that can be operated on in a single request. |
|400 |MissingParameter |The request is missing a required parameter. Ensure that you have supplied all the required parameters for the request; for example, the 'ResourceIds'. |This request is missing a required parameter. Please ensure your request includes all required parameters, such as ResourceIds. |
|400 |MissingParameter |The request is missing a required parameter. Ensure that you have supplied all the required parameters for the request; for example, the 'Tags'. |This request does not contain required parameters. Please ensure the request includes all required parameters, such as Tags. |
|400 |MissingParameter |The request is missing a required parameter. Ensure that you have supplied all the required parameters for the request; for example, the 'ResourceType'. |This request is missing a required parameter. Please ensure your request includes all required parameters, such as ResourceType. |
|400 |MissingParameter |The request is missing a required parameter. Ensure that you have supplied all the required parameters for the request; for example, the ''. |This request is missing a required parameter. Ensure the request includes all required parameters, such as . |
|400 |QuotaExceeded.ResourceCustomTags |You've reached the limit on the number of resource tags that you can create. |You have reached the maximum number of custom tags that you can add to a single resource. |
|400 |QuotaExceeded.ResourceSystemTags |You've reached the limit on the number of system tags that you can create. |You have reached the maximum number of system tags that can be created per resource. |
|403 |Forbidden |You are not authorized to perform operations on the service managed tag. |No permission to tag the specified resource with managed tags. |
|403 |Forbidden |You are not authorized to perform operations on the system tag. |No permission to tag the specified resource with a system tag. |
|403 |InvalidResourceType.ServcieManaged |The specified ResourceType is managed by a service. |The specified resource is a service\-managed resource. |
|404 |InvalidResource.NotFound |The specified resource does not exist. |The specified resource does not exist. |
|500 |InternalError |An internal error has occurred. |An internal error occurred. |
