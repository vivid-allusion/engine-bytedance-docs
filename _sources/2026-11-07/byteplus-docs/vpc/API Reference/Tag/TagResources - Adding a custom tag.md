---
title: "TagResources - Adding a custom tag"
product: "Virtual Private Cloud"
product_code: "vpc"
source: "https://docs.byteplus.com/en/docs/vpc/TagResources"
---

Call the TagResources API to add custom tags to resources.

## Instructions

* If a tag with the same key is added repeatedly to the same resource, the newly added value will overwrite the previous value.

* Each resource can have a maximum of 50 tags. Each call to this API can add up to 20 tags.

## Debug

[去调试](https://api.byteplus.com/api-explorer/debug?action=TagResources&serviceCode=vpc&version=2020-04-01&groupName=)

## Request parameters

The following only details request parameters specific to this API and key common parameters. More information is available in [Common parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).

**Action ** String必选 `Example value: TagResources`

The interface name. The current API name is `TagResources`.

**Version ** String必选 `Example value: 2020-04-01`

The interface version. The current API version is `2020-04-01`.

**ResourceType ** String必选 `Example value: vpc`

The resource type. Values:

* vpc: Virtual Private Cloud.

* subnet: Subnet.

* eni: Network interface.

* securitygroup: Security group.

* havip: High\-Availability Virtual IP Address.

* routetable: Route table.

* networkacl: Network Access Control List.

* flowlog: Flow Log.

* trafficmirrortarget: Traffic Mirror Target.

* trafficmirrorfilter: Traffic mirror filter.

* trafficmirrorsession: Traffic mirror session.

* eip: Elastic IP (EIP).

* bandwidthpackage: Bandwidth Package.

* ngw: NAT gateway.

* vpngateway: VPN gateway.

* directconnectconnection: Direct Connect Connection.

* directconnectgateway: Direct Connect Gateway.

* directconnectvirtualinterface: Direct Connect Virtual Interface.

**ResourceIds.N ** String必选 `Example value: vpc-273w3e33y2y9s7fap8u2j****`

The resource ID.

* Parameter \- N: Represents the serial number of a resource ID. A maximum of 50 IDs can be specified per single API call.

* Separate multiple resource IDs with ampersands (&).

**Tags.N.Key ** String必选 `Example value: k1`

The tag key of the user tag.

* Parameter \- N: Represents the serial number of a tag key. Value range: 1 to 20.

* Separate multiple tag keys with ampersands (&).

* The key cannot start with `volc:` or `sys:` (including any case variation, e.g., Volc:, SYS:).

* Must be 1 to 128 characters. May include characters in different languages, numbers, spaces ( ), underscores (_), periods (.), half\-width colons (:), slashes (/), equal signs (=), plus signs (+), hyphens (\-), and at signs (@).

* If a tag key contains leading or trailing spaces, the system will automatically delete them.

> **tip**

> Duplicate tag keys are not allowed for the same resource.

**Tags.N.Value ** String`optional` `Example value: v1`

The tag value of the user tag.

* Parameter \- N: Indicates the index of the tag value, value range: 1 to 20.

* Separate multiple tag values with ampersands (&).

* The length ranges from 0 to 256 characters. If left blank, it defaults to an empty value.

* The following characters are allowed: characters from all languages, numbers, spaces ( ), underscores (_), periods (.), colons (:), forward slashes (/), equal signs (=), plus signs (+), hyphens (\-), and the at symbol (@).

* Case\-sensitive.

* If a tag value starts or ends with spaces, the system automatically deletes the space.

> **tip**

> To provide this parameter, provide `Tags.N.Key` first.

## Response parameters

The following only details response parameters specific to this API. For more information, see [Response structure](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response).

**RequestId ** String`optional` `Example value: 2021062415303301022514515207C4****`

Request ID.

## Request examples

```JSON
GET /?Action=TagResources&Version=2020-04-01&ResourceType=vpc&ResourceIds.1=vpc-273w3e33y2y9s7fap8u2j****&ResourceIds.2=vpc-bp15zckdt37pq72zv****&Tags.1.Key=k1&Tags.2.Key=k2&Tags.1.Value=v1&Tags.2.Value=v2 HTTP/1.1
Host: vpc.cn-beijing.byteplusapi.com.cn
X-Date: 20251121T094038Z
Authorization: HMAC-SHA256 Credential=Adfks******wekfwe/20251121/cn-beijing/vpc/request, SignedHeaders=host;x-date, Signature=47a7d934ff7b37c03938******cd7b8278a40a1057690c401e92246a0e41085f
```

## Response examples

```JSON
{
    "ResponseMetadata": {
        "RequestId": "20230604110420****100232280022D31",
        "Action": "TagResources",
        "Version": "2020-04-01",
        "Service": "vpc",
        "Region": "cn-beijing"
    },
    "Result": {
        "RequestId": "2021062415303301022514515207C4****"
    }
}
```

## Error codes

|**Status code** |**Error codes** |**Error message** |**Description** |
|---|---|---|---|
|400 |DryRunOperation |Exception raised to indicate a successfully authorized action when the DryRun flag is set to true. |This request is set to DryRun. The action is authorized but not executed. |
|400 |InvalidResourceType.Malformed |The specified parameter resource type is invalid. |The resource type is invalid. |
|400 |InvalidResourceType.NotFound |The specified resource type does not exist. |The specified resource type does not exist. |
|400 |InvalidTag.Disorder |The specified index order of tag is malformed. |The index order format of the specified tag is invalid |
|400 |InvalidTagAccount.Malformed |The specified parameter tag account is invalid. Account ID cannot be 1. |The tag user is invalid. User ID cannot be 1. |
|400 |InvalidTagKey.Malformed |The specified parameter tag key is invalid. |The tag key is invalid. |
|400 |InvalidTagValue.Malformed |The specified parameter tag value is invalid. |The tag value is invalid. |
|400 |LimitExceeded.Resource |You've reached the limit on the number of resources that you can operate at one time. |You have reached the maximum number of tags that you can manage in a single request. |
|400 |LimitExceeded.Tags |You've reached the limit on the number of tags that you can operate at one time. |You have reached the maximum number of tags that you can manage in a single request. |
|400 |QuotaExceeded.ResourceSystemTags |You've reached the limit on the number of system tags that you can create. |You have reached the maximum number of system tags that you can add to a single resource. |
|400 |QuotaExceeded.ResourceTags |You've reached the limit on the number of resource tags that you can create. |You have reached the maximum number of custom tags that you can add to a single resource. |
|404 |InvalidResource.NotFound |The specified resource does not exist. |The specified resource does not exist. |
