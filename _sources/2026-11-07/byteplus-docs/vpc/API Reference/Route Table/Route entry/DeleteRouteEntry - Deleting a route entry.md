---
title: "DeleteRouteEntry - Deleting a route entry"
product: "Virtual Private Cloud"
product_code: "vpc"
source: "https://docs.byteplus.com/en/docs/vpc/DeleteRouteEntry"
---

Call the DeleteRouteEntry API to delete a custom route entry.

## Instructions

DeleteRouteEntry is an asynchronous interface; when a request ID is returned, the system is still configuring in the background. You can call [DescribeRouteEntryList](https://docs.byteplus.com/en/docs/vpc/DescribeRouteEntryList) API to check the status of a route entry. `Pending` indicates the route entry is being deleted, and a query failure (Returns NotFound). indicates the deletion was successful.

## Debug

[去调试](https://api.byteplus.com/api-explorer/debug?action=DeleteRouteEntry&serviceCode=vpc&version=2020-04-01&groupName=)

## Request parameters

The following only details request parameters specific to this API and key common parameters. More information is available in [Common parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).

**Action ** String必选 `Example value: DeleteRouteEntry`

The interface name. The current API name is `DeleteRouteEntry`.

**Version ** String必选 `Example value: 2020-04-01`

The interface version. The current API version is `2020-04-01`.

**RouteEntryId ** String必选`Example value: rte-3tj9gw2pwq3vj0x****`</a\>

The ID of the route entry to be deleted.

You can call the [DescribeRouteEntryList](https://docs.byteplus.com/en/docs/vpc/DescribeRouteEntryList) API to query the route entry ID.

## Response parameters

The following only details response parameters specific to this API. For more information, see [Response structure](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response).

**RequestId ** String`optional` `Example value: 2021062415303301022514515207C4****`

Request ID.

## Request examples

```JSON
GET /?Action=DeleteRouteEntry&Version=2020-04-01&RouteEntryId=rte-3tj9gw2pwq3vj0x**** HTTP/1.1
Host: vpc.cn-beijing.byteplusapi.com.cn
X-Date: 20251121T094038Z
Authorization: HMAC-SHA256 Credential=Adfks******wekfwe/20251121/cn-beijing/vpc/request, SignedHeaders=host;x-date, Signature=47a7d934ff7b37c03938******cd7b8278a40a1057690c401e92246a0e41085f
```

## Response examples

```JSON
{
    "ResponseMetadata": {
        "RequestId": "2021062415303301022514515207C4****",
        "Action": "DeleteRouteEntry",
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
|400 |IdempotentParameterMismatch |Arguments on this idempotent request are inconsistent with arguments used in previous request(s). |The parameters of this idempotent request are inconsistent with those used in the previous request. |
|400 |InvalidParameter.ClientTokenMalformed |The specified parameter ClientToken is malformed. |The format of specified CientToken is invalid. It must not exceed 64 ASCII characters. |
|400 |InvalidVpc.InvalidStatus |The specified VPC is not in the correct status for the request. |The specified VPC is in a state that cannot respond to this request. |
|403 |Forbidden |You are not authorized to perform operations on the specified route entry. The specified route entry is a system route entry. |No sufficient permissions to perform this operation on the specified route entry. The specified route entry is a system route entry. |
|404 |InvalidPrefixList.NotFound |The specified prefix list does not exist. |The specified Prefix List does not exist. |
|404 |InvalidPrefixListAssociation.NotFound |The specified prefix list is not associated with the specified resource. |The specified prefix list is not referenced by this resource. |
|404 |InvalidRouteEntry.NotFound |The specified route entry does not exist. |The specified route entry does not exist. |
|412 |IdempotentProcessing |The request uses the same client token as a previous one that is still in process. |The idempotent request is in progress. |
