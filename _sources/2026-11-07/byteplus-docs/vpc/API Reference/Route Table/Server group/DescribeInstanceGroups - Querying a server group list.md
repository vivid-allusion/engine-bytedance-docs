---
title: "DescribeInstanceGroups - Querying a server group list"
product: "Virtual Private Cloud"
product_code: "vpc"
source: "https://docs.byteplus.com/en/docs/vpc/DescribeInstanceGroups"
---

Call the DescribeInstanceGroups API to query server groups that meet the specified conditions.

<span id=".6LCD6K-V"></span>
## Debug

[去调试](https://api.byteplus.com/api-explorer/debug?action=DescribeInstanceGroups&serviceCode=vpc&version=2020-04-01&groupName=)


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters

The following only details request parameters specific to this API and key common parameters. More information can be found in [Common parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).



**Action ** <span data-label="purple">String </span><span data-api-tag="require|wzZahb">必选</span> `Example: DescribeInstanceGroups`

The interface name. The current API name is `DescribeInstanceGroups`.



**Version ** <span data-label="purple">String </span><span data-api-tag="require|jE3sMH">必选</span> `Example: 2020-04-01`

The interface version. the current API version is `2020-04-01`.



**VpcId ** <span data-label="purple">String </span>`optional` `Example: vpc-bp15zkdt37pq72zv****`

ID of the VPC to which the server group belongs.

You can call the [DescribeVpcs](https://docs.byteplus.com/en/docs/vpc/DescribeVpcs) API to query the VPC ID.



**InstanceGroupIds.N ** <span data-label="purple">String </span>`optional` `Example: ig-cb15zckdt37pq66****`

Server group ID.


* Parameter \- N: Represents the serial number of the server group ID. The maximum number of entries per request is 100.

* Separate multiple IDs with ampersands (&).



**InstanceGroupName ** <span data-label="purple">String </span>`optional` `Example: instance-group-A`

Name of the server group.



**NextToken ** <span data-label="purple">String </span>`optional` `Example: caeba0bbb2be03f84eb48b699f0a****`

The pagination token that is used to mark the position in pagination queries.


* If left blank, the query starts from the beginning.

* Provide the `NextToken` returned from a previous call to this API, the query continues from that pagination position.



**MaxResults ** <span data-label="purple">Integer </span>`optional` `Example: 50`

The number of query results. Default: 10. Maximum: 100.



&nbsp;

<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters

Only the response parameters specific to this API are listed below. More information, see [Response structure](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response).



**RequestId ** <span data-label="purple">String </span>`Example: 2021062415303301022514515207C4****`

Request ID.



**InstanceGroups ** <span data-label="purple">Object[] </span>`Example: -`

Details of the server group.


**AccountId ** <span data-label="purple">String </span>`Example: test-account`

The account ID to which the server group belongs.



**VpcId ** <span data-label="purple">String </span>`Example: vpc-bp1b1xjllp3ve5yze****`

ID of the VPC to which the server group belongs.



**InstanceGroupId ** <span data-label="purple">String </span>`Example: ig-1323sadadda***`

Server group ID.



**Status ** <span data-label="purple">String </span>`Example: Available`

Status of the server group.


* Available: Available.

* Pending: In progress



**Name** <span data-label="purple">String</span> `Example: instance-group-A`

Name of the server group.



**Description ** <span data-label="purple">String </span>`Example: instance-group-A-test`

Description of the server group.



**Members ** <span data-label="purple">Object[] </span>`Example: -`

Details of the ECSs within the server group.


**Id ** <span data-label="purple">String </span>`Example: i-1323sadadda***`

Instance ID.



**Type ** <span data-label="purple">String </span>`Example: EcsInstance`

Instance type. Currently only **EcsInstance** is supported.



**Status ** <span data-label="purple">String </span>`Example: Active`

Instance status.


* Active: Normal.

* Inactive: Abnormal.

* Unknown: Checking.



**Weight ** <span data-label="purple">Integer </span>`Example: 100`

The weight of the instance.





**NextToken ** <span data-label="purple">String </span>`Example: caeba0bbb2be03f84eb48b699f0a****`

The pagination token returned by this API call, which marks the position for the next query. An empty return indicates there is no next page.



&nbsp;

<span id=".6K-35rGC56S65L6L"></span>
## Request examples

```json
GET /?Action=DescribeInstanceGroups&Version=2020-04-01&VpcId=vpc-bp15zkdt37pq72zv****&NextToken=caeba0bbb2be03f84eb48b699f0a****&MaxResults=50 HTTP/1.1
Host: vpc.cn-beijing.byteplusapi.com.cn
X-Date: 20250804T033538Z
Authorization: HMAC-SHA256 Credential=Adfks******wekfwe/20250804/cn-beijing/vpc/request, SignedHeaders=host;x-date, Signature=47a7d934ff7b37c03938******cd7b8278a40a1057690c401e92246a0e41085f
```


<span id=".6L-U5Zue56S65L6L"></span>
## Response examples

```json
{
    "ResponseMetadata": {
        "RequestId": "20230604110420****100232280022D31",
        "Action": "DescribeInstanceGroups",
        "Version": "2020-04-01",
        "Service": "vpc",
        "Region": "cn-beijing"
    },
    "Result": {
        "InstanceGroups": [
            {
                "Name": "instance-group-A",
                "VpcId": "vpc-bp1b1xjllp3ve5yze****",
                "Status": "Available",
                "Members": [
                    {
                        "Id": "i-1323sadadda***",
                        "Type": "EcsInstance",
                        "Status": "Active",
                        "Weight": 100
                    }
                ],
                "AccountId": "test-account",
                "Description": "instance-group-A-test",
                "InstanceGroupId": "ig-1323sadadda***"
            }
        ],
        "NextToken": "caeba0bbb2be03f84eb48b699f0a****",
        "RequestId": "2021062415303301022514515207C4****"
    }
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error codes


|Status code |Error codes |Error message |Notes |
|---|---|---|---|
|400 |DryRunOperation |Exception raised to indicate a successfully authorized action when the DryRun flag is set to true. |This request is set to DryRun. The action is authorized but not executed. |
|400 |IdempotentParameterMismatch |Arguments on this idempotent request are inconsistent with arguments used in previous request(s). |The parameters of this idempotent request are inconsistent with those used in the previous request. |
|400 |InvalidMaxResults.Malformed |The specified parameter MaxResults is malformed. |The number of query results is invalid. |
|400 |InvalidNextToken.Malformed |The specified parameter NextToken is invalid. |NextToken is invalid for the query. |
|400 |InvalidPage.Malformed |The specified page is malformed. |The specified pagination parameter is invalid. |
|400 |InvalidParameter.ClientTokenMalformed |The specified parameter ClientToken is malformed. |The format of specified CientToken is invalid. It must not exceed 64 ASCII characters. |
|403 |InvalidInstanceGroup.Forbidden |You are not authorized to perform operations on instance group. |You do not have permission to use the server group. |
|412 |IdempotentProcessing |The request uses the same client token as a previous one that is still in process. |The idempotent request is in progress. |
