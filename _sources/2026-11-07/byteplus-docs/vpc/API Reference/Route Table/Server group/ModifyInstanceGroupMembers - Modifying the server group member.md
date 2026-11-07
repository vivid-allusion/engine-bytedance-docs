---
title: "ModifyInstanceGroupMembers - Modifying the server group member"
product: "Virtual Private Cloud"
product_code: "vpc"
source: "https://docs.byteplus.com/en/docs/vpc/ModifyInstanceGroupMembers"
---

Call the ModifyInstanceGroupMembers API to update the Elastic Compute Service within the server group.

<span id=".5L2_55So6K-05piO"></span>
## Instructions

ModifyInstanceGroupMembers is an asynchronous API. When a request ID is returned, the system is still configuring in the background. You can call [DescribeInstanceGroups](https://docs.byteplus.com/en/docs/vpc/DescribeInstanceGroups) API to view the status of route entries. `Pending` means updating, and `Available` means update is complete.

<span id=".6LCD6K-V"></span>
## Debug

[去调试](https://api.byteplus.com/api-explorer/debug?action=ModifyInstanceGroupMembers&serviceCode=vpc&version=2020-04-01&groupName=)


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters

The following only details request parameters specific to this API and key common parameters. More information is available in [Common parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).



**Action ** <span data-label="purple"> String  </span><span data-api-tag="require|bqCWGx">必选</span> `Example value: ModifyInstanceGroupMembers`

The interface name. The current API name is `ModifyInstanceGroupMembers`.



**Version ** <span data-label="purple"> String  </span><span data-api-tag="require|BWttO_">必选</span> `Example: 2020-04-01`

The interface version. The current API version is `2020-04-01`.



**InstanceGroupId ** <span data-label="purple"> String  </span><span data-api-tag="require|0fneW4">必选</span> `Example: ig-cb15zckdt37pq66****`

ID of the server group.

You can call the [DescribeInstanceGroups](https://docs.byteplus.com/en/docs/vpc/DescribeInstanceGroups) API to query the server group ID.



**AppendMembers.N.Id ** <span data-label="purple"> String </span>`optional` `Example: i-wijfn35c****`

Add ECS to the server group.


* Parameter \- N: represents the serial number of an ECS instance ID. A maximum of 32 IDs can be specified per single API call.

* Separate multiple IDs with ampersands (&).



**RemoveMembers.N.Id ** <span data-label="purple"> String </span>`optional` `Example value: i-wijfn35d****`

Remove the ECS from the server group.


* Parameter \- N: represents the serial number of an ECS instance ID. A maximum of 32 IDs can be specified per single API call.

* Separate multiple IDs with ampersands (&).



**ClientToken ** <span data-label="purple"> String </span>`optional` `Example value: 123e4567-e89b-12d3-a456-42665544****`

Client Token that is used to ensure the request idempotency.


* You can use the client to automatically generate a token, but must confirm that the tokens for different requests are unique. This prevents repeated actions due to multiple client retries when the call of the API action times out or an internal server error occurs.

* Must not exceed 64 ASCII characters.

* If you do not provide ClientToken, this API call does not verify idempotency.



<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters

The following only details response parameters specific to this API. For more information, see [Response structure](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response).



**RequestId ** <span data-label="purple"> String  </span>`optional` `Example: 2021062415303301022514515207C4****`

Request ID.



<span id=".6K-35rGC56S65L6L"></span>
## Request examples

```JSON
GET /?Action=ModifyInstanceGroupMembers&Version=2020-04-01&InstanceGroupId=ig-cb15zckdt37pq66****&AppendMembers.1.Id=i-wijfn35c**** HTTP/1.1
Host: vpc.cn-beijing.byteplusapi.com.cn
X-Date: 20251121T094038Z
Authorization: HMAC-SHA256 Credential=Adfks******wekfwe/20251121/cn-beijing/vpc/request, SignedHeaders=host;x-date, Signature=47a7d934ff7b37c03938******cd7b8278a40a1057690c401e92246a0e41085f
```


<span id=".6L-U5Zue56S65L6L"></span>
## Response examples

```JSON
{
    "ResponseMetadata": {
        "RequestId": "20230604110420****100232280022D31",
        "Action": "ModifyInstanceGroupMembers",
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
|400 |InvalidEni.InvalidStatus |The specified elastic network interface is not in the correct status for the request. |The specified Elastic Network Interface is not in a status that can respond to this request. |
|400 |InvalidInstanceGroup.InvalidStatus |The specified instance group is not in the correct status for the request. |The specified server group is in a status that cannot respond to the request. |
|400 |InvalidMember.Duplicated |The specified member duplicated. |Duplicate member instances were specified. |
|400 |InvalidMember.EniIPv4Disabled |The ENI of member to append is IPv4 disabled. |The ENI of the member instance to be added has IPv4 disabled. |
|400 |InvalidMember.EniNotFound |The ENI of specified member is not found. |The specified member instance's ENI does not exist. |
|400 |InvalidMember.Existed |The member to append exists in the specified instance group. |The member instance to be added already exists in the specified server group. |
|400 |InvalidMember.IdMalformed |The ID of specified member is malformed. |The specified member instance ID is invalid. |
|400 |InvalidMember.TypeMalformed |The type of specified member is malformed. |The specified member instance type is invalid. |
|400 |InvalidMember.VpcMismatch |The member to append and specified instance group are in different VPCs. |The member instance to be added and the specified server group resides in different VPCs. |
|400 |InvalidMember.WeightMalformed |The weight of specified member is malformed. |The specified member instance weight is invalid. |
|400 |InvalidParameter.ClientTokenMalformed |The specified parameter ClientToken is malformed. |The format of specified CientToken is invalid. It must not exceed 64 ASCII characters. |
|400 |InvalidVpc.InvalidStatus |The specified VPC is not in the correct status for the request. |The specified VPC is in a state that cannot respond to this request. |
|400 |QuotaExceeded.InstanceMember |You've reached the limit on the number of members per instance group. |The maximum number of member instances allowed for the server group has been reached. |
|403 |InvalidInstanceGroup.Forbidden |You are not authorized to perform operations on instance group. |You do not have permission to use the server group. |
|404 |InvalidInstanceGroup.NotFound |The specified instance group does not exist. |The specified server group does not exist. |
|404 |InvalidMember.NotFound |The specified member is not found in instance group. |The specified member instance does not exist in the server group. |
|412 |IdempotentProcessing |The request uses the same client token as a previous one that is still in process. |The idempotent request is in progress. |
