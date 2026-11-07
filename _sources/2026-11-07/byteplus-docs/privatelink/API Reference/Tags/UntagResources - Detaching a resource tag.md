---
title: "UntagResources - Detaching a resource tag"
product: "PrivateLink"
product_code: "privatelink"
source: "https://docs.byteplus.com/en/docs/privatelink/UntagResources"
---

Call the UntagResources API to delete custom tags from resources.

## Debug

[去调试](https://api.byteplus.com/api-explorer/debug?action=UntagResources&serviceCode=privatelink&version=2020-04-01&groupName=)

## Request parameters

**Action ** String必选 `Example: UntagResources`

Action to execute. Set the value to **UntagResources**.

**Version ** String必选 `Example: 2020-04-01`

API version. The current version is **2020\-04\-01**.

**ResourceType ** String必选 `Example: endpointservice`

The resource type. Values:

* endpointservice: Endpoint service

* endpoint: Interface endpoint

* gateway endpoint: Gateway endpoint

**ResourceIds.N ** String必选 `Example: epsvc-2fe630gurkl37k5gfuy33****`

The resource ID.

> **tip**

* > You can call the [DescribeVpcEndpointServices](https://docs.byteplus.com/en/docs/privatelink/DescribeVpcEndpointServices) API to get resource IDs of the **endpointservice** type.

* > You can call the [DescribeVpcEndpoints](https://docs.byteplus.com/en/docs/privatelink/DescribeVpcEndpoints) API to get the resource ID of the **endpoint** type.

* > You can call the [DescribeVpcGatewayEndpoints](https://docs.byteplus.com/en/docs/privatelink/DescribeVpcGatewayEndpoints) API to get the resource ID of the **gatewayendpoint** type.

* > N represents the serial number of the resource ID, ranging from 1 to 50.

* > Separate multiple resource IDs with ampersands (&).

**TagKeys.N ** String必选 `Example: k1`

The key of the custom tag to be deleted from the resource.

* N specifies the serial number of the tag key. Valid values: 1\-20.

* Separate multiple resource IDs with ampersands (&).

## Response parameters

**RequestId ** String` optional` `Example: 2021062415303301022514515207C4****`

Request ID.

## Request examples

```JSON
GET /?Action=UntagResources&Version=2020-04-01&ResourceType=endpointservice&ResourceIds.1=epsvc-2fe630gurkl37k5gfuy33****&TagKeys.1=k1
Host: privatelink.cn-guangzhou.byteplusapi.com.cn
X-Date: 20251121T094038Z
Authorization: HMAC-SHA256 Credential=Adfks******wekfwe/20251121/cn-guangzhou/privatelink/request, SignedHeaders=host;x-date, Signature=47a7d934ff7b37c03938******cd7b8278a40a1057690c401e92246a0e41085f
```

## Response examples

```JSON
{
    "ResponseMetadata": {
        "RequestId": "2021062415303301022514515207C4****",
        "Action": "UntagResources",
        "Version": "2020-04-01",
        "Service": "privatelink",
        "Region": "cn-guangzhou"
    },
    "Result": {}
}
```

## Error codes

This section displays only the error codes of the current API. For more error codes, see [Common error codes](https://docs.byteplus.com/en/docs/privatelink/Public-error-codes).

|**Status code** |**Error codes** |**Error message** |**Notes** |
|---|---|---|---|
|400 |MissingParameter |The request is missing a required parameter. Ensure that you have supplied all the required parameters for the request; for example, the 'XXX'. |This request does not contain required parameters. Ensure that your request includes all required parameters, such as *XXX*.<br><br>> **tip**<br><br><br>> Here, XXX represents the name of the missing parameter.<br> |
|400 |InvalidIncorrectOrder.Malformed |The specified index order is malformed. |The specified index order format is invalid. |
|400 |InvalidResourceType.Malformed |The specified ResourceType is malformed. |The specified ResourceType parameter format is invalid. |
|400 |InvalidTagKey.Malformed |The specified TagKey is malformed. |The specified TagKey is invalid. |
|400 |LimitExceeded.Resource |You've reached the limit on the number of resources that you can operate at a time. |You have reached the maximum number of tags that can be processed in a single request. |
|400 |LimitExceeded.TagOperation |You've reached the limit on the number of tags that you can operate at a time. |You have reached the maximum number of tag entries that can be operated on in a single request. |
|404 |InvalidResource.NotFound |The specified resource does not exist. |The specified resource does not exist. |
