---
title: "TagNLBResources - Adding a custom tag to NLB resources"
product: "Cloud Load Balancer"
product_code: "clb"
source: "https://docs.byteplus.com/en/docs/clb/TagNLBResources"
---

You can call the TagNLBResources API to add custom tags to NLB resources.

## Instructions

Each resource supports up to 50 custom tags, while a single API call can add a maximum of 20 tags.​​

## Debug

[去调试](https://api.byteplus.com/api-explorer/debug?action=TagNLBResources&serviceCode=clb&version=2020-04-01&groupName=)

## Request parameters

**Action ** String必选 `Example: TagNLBResources`

Action to execute. Set the value to TagNLBResources.

**Version ** String必选 `Example: 2020-04-01`

Current API version is 2020\-04\-01.

**ResourceType ** String必选 `Example: nlb`

The resource type. Valid values:

* nlb: NLB instance.

* nlb_listener: Listener.

* nlb_servergroup: Server group.

* nlb_security_policy: TLS custom security policy.

**ResourceIds.N ** String必选 `Example: nlb-273sdsdswrfdp8u2j****`

The resource ID.

* Parameter \- N: Indicates the serial number of the resource ID, ranging from 1 to 20.

* Separate multiple resource IDs with ampersands (&).

> **tip**

* > You can call the [DescribeNetworkLoadBalancers](https://docs.byteplus.com/en/docs/clb/DescribeNetworkLoadBalancers) API to query the ID of NLB instance.

* > You can call the [DescribeNLBListeners](https://docs.byteplus.com/en/docs/clb/DescribeNLBListeners) API to query listener IDs.

* > You can call the [DescribeNLBServerGroups](https://docs.byteplus.com/en/docs/clb/DescribeNLBServerGroups) API to query server group IDs.

* > You can call the [DescribeNLBSecurityPolicies](https://docs.byteplus.com/en/docs/clb/DescribeNLBSecurityPolicies) API to query IDs of TLS custom security policies.

**Tags.N.Key ** String必选 `Example: key1`

The tag key of the custom tag.

* N represents the sequence number of a tag key. Valid range: 1 to 20.

* Separate multiple tag keys with &.

* Must not start with `volc:` or `sys:` in any case form.

* Must be 1 to 128 characters. May include characters (any language), numbers, spaces ( ), underscores (_), periods (.), half\-width colons (:), slashes (/), equal signs (=), plus signs (+), hyphens (\-), and at signs (@).

* If a tag key contains leading or trailing spaces, the system will automatically delete them.

> **tip**

> Duplicate tag keys are not allowed for the same resource.

**Tags.N.Value ** String`optional` `Example: value1`

The tag value of the custom tag.

* N represents the sequence number of a tag value. Valid range: 1–20.

* Separate multiple tag values with ampersands (&).

* Must be 0 to 256 characters. If left blank, this parameter defaults to an empty string.

* The following characters are allowed: characters from all languages, numbers, spaces ( ), underscores (_), periods (.), colons (:), forward slashes (/), equal signs (=), plus signs (+), hyphens (\-), and the at symbol (@).

* Case\-sensitive.

* If a tag value starts or ends with a space, the system will automatically delete it.

> **tip**

> To pass in this parameter, pass in `Tags.N.Key` first.

## Response parameters

**RequestId ** String`Example: 2024062415303301022514515207C4****`

Request ID.

## Request examples

```json
GET /?Action=TagNLBResources&Version=2020-04-01&ResourceType=nlb&ResourceIds.1=nlb-273sdsdswrfdp8u2j****&Tags.1.Key=key1&Tags.1.Value=value1 HTTP/1.1
Host: clb.cn-beijing.byteplusapi.com.cn
Date: 20260310T094038Z
Authorization: HMAC-SHA256 Credential=Adfks******wekfwe/20251121/cn-beijing/clb/request, SignedHeaders=host;x-date, Signature=47a7d934ff7b37c03938******cd7b8278a40a1057690c401e92246a0e41085f
```

## Response examples

```json
{
    "ResponseMetadata": {
        "RequestId": "20230604110420****100232280022D31",
        "Action": "TagNLBResources",
        "Version": "2020-04-01",
        "Service": "clb",
        "Region": "cn-beijing"
    },
    "Result": {
        "RequestId": "2024062415303301022514515207C4****"
    }
}
```

## Error codes

This section displays only the error codes of the current API. For more error codes, see [Common error codes](https://docs.byteplus.com/en/docs/clb/NLB-Common-Error-Codes).

|Status code |Error codes |Error message |Notes |
|---|---|---|---|
|400 |InvalidIncorrectOrder.Malformed |The specified index order is malformed. |The specified index order parameter format is invalid. |
|400 |InvalidResourceType.Malformed |The specified ResourceType is malformed. |The specified ResourceType parameter format is invalid. |
|400 |InvalidTagKey.Malformed |The specified TagKey is malformed. |The specified TagKey parameter format is invalid. |
|400 |InvalidTagValue.Malformed |The specified TagValue is malformed. |The specified TagValue parameter format is invalid. |
|400 |LimitExceeded.Resource |You've reached the limit on the number of resources that you can operate at a time. |You have reached the maximum number of tags that can be processed in a single request. |
|400 |LimitExceeded.ServiceManagedTag |You've reached the limit on the number of service managed tags that you can create. |You have reached the limit for the number of managed resource tag key\-value pairs that can be created in a single request. |
|400 |LimitExceeded.TagOperation |You've reached the limit on the number of tags that you can operate at a time. |You have reached the maximum number of tag entries that can be operated on in a single request. |
|400 |QuotaExceeded.ResourceCustomTags |You've reached the limit on the number of resource tags that you can create. |You have reached the maximum number of custom tags that you can add to a single resource. |
|400 |QuotaExceeded.ResourceSystemTags |You've reached the limit on the number of system tags that you can create. |You have reached the maximum number of system tags that can be created per resource. |
|403 |Forbidden |You are not authorized to perform operations on the service managed tag. |No permission to tag the specified resource with managed tags. |
|403 |Forbidden |You are not authorized to perform operations on the system tag. |No permission to tag the specified resource with a system tag. |
|403 |InvalidResourceType.ServiceManaged |The specified ResourceType is managed by a service. |The specified resource is a service\-managed resource. |
|404 |InvalidResource.NotFound |The specified resource does not exist. |The specified resource does not exist. |
