---
title: "DeleteInstanceGroup - Deleting a server group"
product: "Virtual Private Cloud"
product_code: "vpc"
source: "https://docs.byteplus.com/en/docs/vpc/DeleteInstanceGroup"
---

Call the DeleteInstanceGroup API to delete the server group.

<span id=".5L2_55So6K-05piO"></span>
## Instructions

DeleteInstanceGroup is an asynchronous API. When a request ID is returned, the system is still configuring in the background. You can call [DescribeInstanceGroups](https://docs.byteplus.com/en/docs/vpc/DescribeInstanceGroups) API to check the status of a route entry. `Pending` indicates the route entry is being deleted, and a query failure indicates the deletion was successful.

<span id=".6LCD6K-V"></span>
## Debug

[去调试](https://api.byteplus.com/api-explorer/debug?action=DeleteInstanceGroup&serviceCode=vpc&version=2020-04-01&groupName=)


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters

The following only details request parameters specific to this API and key common parameters. More information is available in [Common parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).



**Action ** <span data-label="purple"> String </span><span data-api-tag="require|8B0y5A">必选</span> `Example value: DeleteInstanceGroup`

The interface name. The current API name is `DeleteInstanceGroup`.



**Version ** <span data-label="purple"> String </span><span data-api-tag="require|MlV31w">必选</span> `Example value: 2020-04-01`

The interface version. The current API version is `2020-04-01`.



**InstanceGroupId ** <span data-label="purple"> String </span><span data-api-tag="require|8gp8kB">必选</span> `Example value: ig-cb15zckdt37pq66****`

ID of the server group to be deleted.

You can call the [DescribeInstanceGroups](https://docs.byteplus.com/en/docs/vpc/DescribeInstanceGroups) API to query the server group ID.



**ClientToken ** <span data-label="purple">String</span> `optional` `Example: 123e4567-e89b-12d3-a456-42665544****`

Client Token that is used to ensure the request idempotency.


* You can use the client to automatically generate a token, but must confirm that the tokens for different requests are unique. This prevents repeated actions due to multiple client retries when the call of the API action times out or an internal server error occurs.

* Must not exceed 64 ASCII characters.

* If you do not provide ClientToken, this API call does not verify idempotency.



<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters

The following only details response parameters specific to this API. For more information, see [Response structure](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response).



**RequestId ** <span data-label="purple"> String </span>`optional` `Example value: 2021062415303301022514515207C4****`

Request ID.



<span id=".6K-35rGC56S65L6L"></span>
## Request examples

```JSON
GET /?Action=DeleteInstanceGroup&Version=2020-04-01&InstanceGroupId=ig-cb15zckdt37pq66**** HTTP/1.1
Host: vpc.cn-beijing.byteplusapi.com.cn
X-Date: 20251121T094038Z
Authorization: HMAC-SHA256 Credential=Adfks******wekfwe/20251121/cn-beijing/vpc/request, SignedHeaders=host;x-date, Signature=47a7d934ff7b37c03938******cd7b8278a40a1057690c401e92246a0e41085f
```


<span id=".6L-U5Zue56S65L6L"></span>
## Response examples

```JSON
{
    "ResponseMetadata": {
        "RequestId": "2021062415303301022514515207C4****",
        "Action": "DeleteInstanceGroup",
        "Version": "2020-04-01",
        "Service": "vpc",
        "Region": "cn-beijing"
    },
    "Result": {
        "RequestId": "2021062415303301022514515207C4****"
    }
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error codes


|**Status code** |**Error codes** |**Error message** |**Description** |
|---|---|---|---|
|400 |DryRunOperation |Exception raised to indicate a successfully authorized action when the DryRun flag is set to true. |This request is set to DryRun. The action is authorized but not executed. |
|400 |IdempotentParameterMismatch |Arguments on this idempotent request are inconsistent with arguments used in previous request(s). |The parameters of this idempotent request are inconsistent with those used in the previous request. |
|400 |InvalidInstanceGroup.HasMembers |The specified instance group has members. |The specified server group contains member instances. |
|400 |InvalidInstanceGroup.InvalidStatus |The specified instance group is not in the correct status for the request. |The specified server group is in a status that cannot respond to the request. |
|400 |InvalidParameter.ClientTokenMalformed |The specified parameter ClientToken is malformed. |The format of specified CientToken is invalid. It must not exceed 64 ASCII characters. |
|400 |InvalidVpc.InvalidStatus |The specified VPC is not in the correct status for the request. |The specified VPC is in a state that cannot respond to this request. |
|400 |QuotaExceeded.InstanceGroup |Instance group number exceeded quota. |The number of server groups has exceeded the quota limit. |
|403 |InvalidInstanceGroup.Forbidden |You are not authorized to perform operations on instance group. |You do not have permission to use the server group. |
|404 |InvalidInstanceGroup.NotFound |The specified instance group does not exist. |The specified server group does not exist. |
|412 |IdempotentProcessing |The request uses the same client token as a previous one that is still in process. |The idempotent request is in progress. |
