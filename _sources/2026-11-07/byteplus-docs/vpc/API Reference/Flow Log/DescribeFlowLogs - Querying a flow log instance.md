---
title: "DescribeFlowLogs - Querying a flow log instance"
product: "Virtual Private Cloud"
product_code: "vpc"
source: "https://docs.byteplus.com/en/docs/vpc/DescribeFlowLogs"
---

Call the DescribeFlowLogs API to query flow logs that meet specified conditions.

<span id=".6LCD6K-V"></span>
## Debug

[去调试](https://api.byteplus.com/api-explorer/debug?action=DescribeFlowLogs&serviceCode=vpc&version=2020-04-01&groupName=)


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters

The following only details request parameters specific to this API and key common parameters. More information can be found in [Common parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).



**Action ** <span data-label="purple">String </span><span data-api-tag="require|OKNxkk">必选</span> `Example: DescribeFlowLogs`

The interface name. The current API name is `DescribeFlowLogs`.



**Version ** <span data-label="purple">String </span><span data-api-tag="require|bFgDGX">必选</span> `Example: 2020-04-01`

The interface version. The current API version is `2020-04-01`.



**FlowLogIds.N ** <span data-label="purple">String </span>`optional` `Example: fl-123456****`

Flow log ID


* Parameter \- N: Indicates the serial number of the flow log ID, with a maximum of 100 per call.

* Separate multiple IDs with ampersands (&).



**FlowLogName ** <span data-label="purple">String </span>`optional` `Example: FlowLog-1`

Flow log name.



**Description ** <span data-label="purple">String </span>`optional` `Example: FlowLog_VPC`

Description of the flow log.



**Resource type** <span data-label="purple">String</span> `optional` `Example: vpc`

The resource type from which to collect traffic. Valid values:


* vpc: Virtual Private Cloud.

* subnet: Subnet.

* eni: Network interface.



**ResourceId ** <span data-label="purple">String </span>`optional` `Example: vpc-123456****`

ID of the resource from which to capture traffic.



**TrafficType ** <span data-label="purple">String </span>`optional` `Example: All`

The type of traffic to collect. Valid values:


* **All**: Total traffic.

* **Allow**: Traffic permitted by the network ACL and security group.

* **Drop**: Traffic denied by the network ACL and security group.



**LogProjectId ** <span data-label="purple">String </span>`optional` `Example: fc69****`

ID of the flow log project.



**LogTopicId ** <span data-label="purple">String </span>`optional` `Example: c6*****`

ID of the flow log topic.



**AggregationInterval ** <span data-label="purple">Integer </span>`optional` `Example: 10`

Sampling interval of the flow log. Valid values:


* 1: 1 minute.

* 5: 5 minutes.

* 10: 10 minutes.



**Status ** <span data-label="purple">String </span>`optional` `Example: Active`

The status of the flow log. Valid values:


* Active: Started/running state.

* Pending: Action in progress​.

* Inactive: Not started.

* Creating

* Deleting



**VpcId ** <span data-label="purple">String </span>`optional` `Example: vpc-123456****`

ID of the VPC for which to view the Flow Logs.

You can call the [DescribeVpcs](https://docs.byteplus.com/en/docs/vpc/DescribeVpcs) API to query the VPC ID.



**ProjectName ** <span data-label="purple">String </span>`optional` `Example: default`

Project to which the flow log belongs.



**TagFilters.N.Key ** <span data-label="purple">String </span>`optional` `Example: k1`

The tag key.


* N represents the sequence number of a tag key. Values: 1\-10.

* Separate multiple tag keys with &. Multiple tag keys have a logical AND relationship. The query returns flow logs tagged with all the specified keys.



**TagFilters.N.Values.N ** <span data-label="purple">String </span>`optional` `Example: v1`

The tag value.


* The first N represents the sequence number of a tag key.

* The second N represents the sequence number of a tag value. Valid range: 1–3. Multiple tag values under the same tag key are combined using a logical OR operation, meaning the query returns flow logs that have any of the specified tag values for that key.

* Separate multiple tag values with an ampersand (&).


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">If this parameter is passed in, <code>TagFilters.N.Key</code> must be passed in first.</div>


* <div data-tips="true" data-tips-type="tip">Passing an empty string queries for flow logs with an empty tag value.</div>




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



**NextToken ** <span data-label="purple">String </span>`Example: caeba0bbb2be03f84eb48b699f0a****`

The pagination token returned by this API call, which marks the position for the next query. An empty return indicates there is no next page.



**FlowLogs ** <span data-label="purple">Object[] </span>`Example: -`

List of detailed flow log information.


**FlowLogId ** <span data-label="purple">String </span>`Example: fl-123456****`

Flow Log ID.



**FlowLogName ** <span data-label="purple">String </span>`Example: FlowLog-1`

Flow log name.



**Description ** <span data-label="purple">String </span>`Example: FlowLog_VPC`

Description of the flow log.



**ResourceType ** <span data-label="purple">String </span>`Example: vpc`

The resource type to capture traffic.



**Resource ID ** <span data-label="purple">String </span>`Example: vpc-123456****`

ID of the resource from which to capture traffic.



**TrafficType ** <span data-label="purple">String </span>`Example: All`

The type of traffic to collect.



**AggregationInterval ** <span data-label="purple">Integer </span>`Example: 10`

Sampling interval of the flow log. Unit: min.



**LogProjectId ** <span data-label="purple">String </span>`Example: fc69****`

ID of the flow log project.



**LogTopicId ** <span data-label="purple">String </span>`Example: c6*****`

ID of the flow log topic.



**Status ** <span data-label="purple">String </span>`Example: Active`

The status of the flow log.



**BusinessStatus** <span data-label="purple">String</span> `Example: FinancialLocked`

Whether the Flow Log is locked.


* Normal

* FinancialLocked: Being locked.



**LockReason ** <span data-label="purple">String </span>`Example: financial`

Reason the Flow Logs instance is locked.


* financial: Being locked due to overdue payments.

* unlock: In the process of recharge recovery after being suspended due to arrears.

* Empty: Not locked.



**VpcId ** <span data-label="purple">String </span>`Example: vpc-123456****`

ID of the VPC for which to view the Flow Logs.



**ProjectName ** <span data-label="purple">String </span>`Example: default`

Name of the flow log project.



**Tags ** <span data-label="purple">Object[] </span>`Example: -`

The tag information of the flow log.


**Key ** <span data-label="purple">String </span>`Example: k1`

The tag key.



**Value ** <span data-label="purple">String </span>`Example: v1`

The tag value.




**CreatedAt ** <span data-label="purple">String </span>`Example: 2021-08-05T21:48:55+08:00`

Creation time of flow log.



**UpdatedAt ** <span data-label="purple">String </span>`Example: 2021-08-05T21:48:55+08:00`

Update time of flow log.




&nbsp;

<span id=".6K-35rGC56S65L6L"></span>
## Request examples

```json
GET /?Action=DescribeFlowLogs&Version=2020-04-01&NextToken=caeba0bbb2be03f84eb48b699f0a****&MaxResults=50 HTTP/1.1
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
        "Action": "DescribeFlowLogs",
        "Version": "2020-04-01",
        "Service": "vpc",
        "Region": "cn-beijing"
    },
    "Result": {
        "FlowLogs": [
            {
                "Tags": [
                    {
                        "Key": "k1",
                        "Value": "v1"
                    }
                ],
                "VpcId": "vpc-123456****",
                "Status": "Active",
                "CreatedAt": "2021-08-05T21:48:55+08:00",
                "FlowLogId": "fl-123456****",
                "UpdatedAt": "2021-08-05T21:48:55+08:00",
                "LockReason": "financial",
                "LogTopicId": "c6*****",
                "ResourceId": "vpc-123456****",
                "Description": "FlowLog_VPC",
                "FlowLogName": "FlowLog-1",
                "ProjectName": "default",
                "TrafficType": "All",
                "LogProjectId": "fc69****",
                "ResourceType": "vpc",
                "BusinessStatus": "FinancialLocked",
                "AggregationInterval": 10
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
|400 |InvalidMaxResults.Malformed |The specified parameter MaxResults is malformed. |The number of query results is invalid. |
|400 |InvalidNextToken.Malformed |The specified parameter NextToken is invalid. |NextToken is invalid for the query. |
|400 |InvalidPage.Malformed |The specified page is malformed. |The specified pagination parameter is invalid. |
|400 |InvalidTagFilter.Disorder |The specified index order of tag filter is malformed. |The index order format of the specified tag filter is invalid. |
|400 |InvalidTagFilterKey.Malformed |The specified parameter tag filter key is invalid. |The tag filter key is invalid. |
|400 |InvalidTagFilterValue.Malformed |The specified parameter tag filter value is invalid. |The tag filter value is invalid. |
|400 |LimitExceeded.FlowLogIDs |You've reached the limit on the number of flow log IDs that you can describe. |The maximum allowed number of flow log IDs for a single query has been reached. |
|400 |LimitExceeded.TagFilterKey |You've reached the limit on the number of tag keys that you can filter. |You have reached the maximum number of filter tag keys that can be specified in a single request. |
|400 |LimitExceeded.TagFilterValue |You've reached the limit on the number of tag values that you can filter. |You have reached the maximum number of filter tag values that can be specified in a single request. |
