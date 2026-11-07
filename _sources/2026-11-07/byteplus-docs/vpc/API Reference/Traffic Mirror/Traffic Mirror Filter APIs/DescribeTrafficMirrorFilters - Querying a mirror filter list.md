---
title: "DescribeTrafficMirrorFilters - Querying a mirror filter list"
product: "Virtual Private Cloud"
product_code: "vpc"
source: "https://docs.byteplus.com/en/docs/vpc/DescribeTrafficMirrorFilters"
---

Call the DescribeTrafficMirrorFilters API to query mirror filters that meet the specified conditions.

<span id=".5L2_55So6K-05piO"></span>
## Instructions


* If multiple request parameters are provided, the query will return Mirror Filter entries that match all the specified conditions. If no matching entry is found, an empty value is returned.

* If none of the optional request parameters are provided, the query will be performed under the current logged\-in account and return all Mirror Filters belonging to this account.


<span id=".6LCD6K-V"></span>
## Debug

[去调试](https://api.byteplus.com/api-explorer/debug?action=DescribeTrafficMirrorFilters&serviceCode=vpc&version=2020-04-01&groupName=)


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters

The following only details request parameters specific to this API and key common parameters. More information can be found in [Common parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).



**Action ** <span data-label="purple">String </span><span data-api-tag="require|9xx4Lt">必选</span> `Example: DescribeTrafficMirrorFilters`

The interface name. The current API name is `DescribeTrafficMirrorFilters`.



**Version ** <span data-label="purple">String </span><span data-api-tag="require|MIGJID">必选</span> `Example: 2020-04-01`

The interface version. the current API version is `2020-04-01`.



**TrafficMirrorFilterIds.N ** <span data-label="purple">String </span>`optional` `Example: tmf-bp1opxu1zkhn00123****`

Mirror Filter ID.


* Parameter \- N: Represents the serial number of the filter ID. The maximum number of entries per request is 100.

* Separate multiple Mirror Filter IDs with ampersands (&).



**TrafficMirrorFilterNames.N ** <span data-label="purple">String </span>`optional` `Example: TM_Filter_1`

Name of the traffic mirror filter.


* parameter \- N: Represents the serial number of the Mirror Filter name. The maximum number of entries per request is 100.

* Separate multiple Mirror Filter names with ampersands (&).



**ProjectName ** <span data-label="purple">String </span>`optional` `Example: default`

Project to which the Mirror Filter belongs.



**TagFilters.N.Key ** <span data-label="purple">String </span>`optional` `Example: k1`

The tag key.


* N represents the sequence number of a tag key. Values: 1\-10.

* Separate multiple tag keys with &. Multiple tag keys have a logical AND relationship. The query returns Mirror Filters tagged with all the specified keys.



**TagFilters.N.Values.N ** <span data-label="purple">String </span>`optional` `Example: v1`

The tag value.


* The first N represents the sequence number of a tag key.

* The second N represents the sequence number of a tag value. Valid values: 1–3. Multiple tag values under the same tag key are combined using a logical OR operation, meaning the query returns Mirror Filters that have any of the specified tag values for that key.

* Separate multiple tag values with an ampersand (&).


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">If this parameter is passed in, <code>TagFilters.N.Key</code> must be passed in first.</div>


* <div data-tips="true" data-tips-type="tip">Passing an empty string queries for Mirror Filters with an empty tag value.</div>




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



**TrafficMirrorFilters ** <span data-label="purple">Object[] </span>`Example: -`

Detailed list of traffic mirror filter.


**TrafficMirrorFilterId ** <span data-label="purple">String </span>`Example: tmf-bp1opxu1zkhn00123****`

Mirror Filter ID.



**TrafficMirrorFilterName ** <span data-label="purple">String </span>`Example: TM_Filter_1`

Name of the traffic mirror filter.



**Description ** <span data-label="purple">String </span>`Example: TM_Filter_1_Description`

Description of the Traffic Mirror Filter.



**Status ** <span data-label="purple">String </span>`Example: Available`

Mirror Filter status.


* Available: Available for use.

* Deleting: In the deleting process.

* Creating



**ProjectName ** <span data-label="purple">String </span>`Example: default`

The name of the project to which the Traffic Mirror Filter belongs.



**Tags ** <span data-label="purple">Object[] </span>`Example: -`

Tag information of the Mirror Filter.


**Key ** <span data-label="purple">String </span>`Example: k1`

The tag key.



**Value ** <span data-label="purple">String </span>`Example: v1`

The tag value.




**IngressFilterRules ** <span data-label="purple">Object[] </span>`Example: -`

Detailed list of inbound rule.


**TrafficMirrorFilterId ** <span data-label="purple">String </span>`Example: tmf-bp1opxu1zkhn00123****`

Mirror Filter ID.



**TrafficMirrorFilterRuleId ** <span data-label="purple">String </span>`Example: tmr-j6cmls82xnc86vtpe****`

ID of the Traffic Mirror Filter.



**TrafficDirection ** <span data-label="purple">String </span>`Example: ingress`

Direction of traffic.


* ingress: inbound.

* egress: Outbound.



**Priority ** <span data-label="purple">Integer </span>`Example: 1`

Rule priority.



**Policy ** <span data-label="purple">String </span>`Example: accept`

Traffic collection policy.


* accept: Allow. When traffic from the mirror site matches this rule, it is replicated to the mirror target for monitoring and analysis.

* Reject. When traffic from the mirror site matches this rule, it is not replicated, and monitoring/analysis for this traffic is denied.



**Protocol ** <span data-label="purple">String </span>`Example: TCP`

Traffic protocol.


* all: TCP, UDP, and ICMP protocols.

* tcp: Transmission Control Protocol

* udp: UDP protocol.

* icmp: ICMP protocol.



**SourceCidrBlock ** <span data-label="purple">String </span>`Example: 0.0.0.0/0`

Traffic source CIDR block.



**SourcePortRange ** <span data-label="purple">String </span>`Example: -1/-1`

Traffic source port range.


* When `Protocol` is set to icmp or all, it returns \-1/\-1, indicating no port restrictions.

* When `Protocol` is tcp or udp, use a forward slash (/) to separate the start and end ports.



**DestinationCidrBlock ** <span data-label="purple">String </span>`Example: 0.0.0.0/0`

Destination CIDR block.



**DestinationPortRange ** <span data-label="purple">String </span>`Example: -1/-1`

Traffic destination port range.


* When `Protocol` is set to icmp or all, it returns \-1/\-1, indicating no port restrictions.

* When `Protocol` is tcp or udp, use a forward slash (/) to separate the start and end ports.



**Description ** <span data-label="purple">String </span>`Example: TM_FilterRule_1`

Description of the filter rule.



**Status ** <span data-label="purple">String </span>`Example: Available`

Status of the Traffic Mirror Filter.


* Available: Available for use.

* Deleting: In the deleting process.

* Creating

* Pending: Modifying.



**CreatedAt ** <span data-label="purple">String </span>`Example: 2021-08-05T21:46:55+08:00`

Creation time of the filter rule.



**UpdatedAt ** <span data-label="purple">String </span>`Example: 2021-08-05T21:46:55+08:00`

Update time of the filter rule.




**EgressFilterRules ** <span data-label="purple">Object[] </span>`Example: -`

Detailed list of outbound rule.


**TrafficMirrorFilterId ** <span data-label="purple">String </span>`Example: tmf-bp1opxu1zkhn00123****`

Mirror Filter ID.



**TrafficMirrorFilterRuleId ** <span data-label="purple">String </span>`Example: tmr-j6cmls82xnc86vtpe****`

ID of the Traffic Mirror Filter.



**TrafficDirection ** <span data-label="purple">String </span>`Example: ingress`

Direction of traffic.


* ingress: inbound.

* egress: Outbound.



**Priority ** <span data-label="purple">Integer </span>`Example: 1`

Rule priority.



**Policy ** <span data-label="purple">String </span>`Example: accept`

Traffic collection policy.


* accept: Allow. When traffic from the mirror site matches this rule, it is replicated to the mirror target for monitoring and analysis.

* Reject. When traffic from the mirror site matches this rule, it is not replicated, and monitoring/analysis for this traffic is denied.



**Protocol ** <span data-label="purple">String </span>`Example: TCP`

Traffic protocol.


* all: TCP, UDP, and ICMP protocols.

* tcp: Transmission Control Protocol

* udp: UDP protocol.

* icmp: ICMP protocol.



**SourceCidrBlock ** <span data-label="purple">String </span>`Example: 0.0.0.0/0`

Traffic source CIDR block.



**SourcePortRange ** <span data-label="purple">String </span>`Example: -1/-1`

Traffic source port range.


* When `Protocol` is set to icmp or all, it returns \-1/\-1, indicating no port restrictions.

* When `Protocol` is tcp or udp, use a forward slash (/) to separate the start and end ports.



**DestinationCidrBlock ** <span data-label="purple">String </span>`Example: 0.0.0.0/0`

Destination CIDR block.



**DestinationPortRange ** <span data-label="purple">String </span>`Example: -1/-1`

Traffic destination port range.


* When `Protocol` is set to icmp or all, it returns \-1/\-1, indicating no port restrictions.

* When `Protocol` is tcp or udp, use a forward slash (/) to separate the start and end ports.



**Description ** <span data-label="purple">String </span>`Example: TM_FilterRule_1`

Description of the filter rule.



**Status ** <span data-label="purple">String </span>`Example: Available`

Status of the Traffic Mirror Filter.


* Available: Available for use.

* Deleting: In the deleting process.

* Creating

* Pending: Modifying.



**CreatedAt ** <span data-label="purple">String </span>`Example: 2021-08-05T21:46:55+08:00`

Creation time of the filter rule.



**UpdatedAt ** <span data-label="purple">String </span>`Example: 2021-08-05T21:46:55+08:00`

Update time of the filter rule.




**CreatedAt ** <span data-label="purple">String </span>`Example: 2021-08-05T21:46:55+08:00`

Creation time of the traffic mirror filter.



**UpdatedAt ** <span data-label="purple">String </span>`Example: 2021-08-05T21:46:55+08:00`

Update time of the traffic mirror filter.




&nbsp;

<span id=".6K-35rGC56S65L6L"></span>
## Request examples

```json
GET /?Action=DescribeTrafficMirrorFilters&Version=2020-04-01&NextToken=caeba0bbb2be03f84eb48b699f0a****&MaxResults=50 HTTP/1.1
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
        "Action": "DescribeTrafficMirrorFilters",
        "Version": "2020-04-01",
        "Service": "vpc",
        "Region": "cn-beijing"
    },
    "Result": {
        "NextToken": "caeba0bbb2be03f84eb48b699f0a****",
        "RequestId": "2021062415303301022514515207C4****",
        "TrafficMirrorFilters": [
            {
                "Tags": [
                    {
                        "Key": "k1",
                        "Value": "v1"
                    }
                ],
                "Status": "Available",
                "CreatedAt": "2021-08-05T21:46:55+08:00",
                "UpdatedAt": "2021-08-05T21:46:55+08:00",
                "Description": "TM_Filter_1_Description",
                "ProjectName": "default",
                "EgressFilterRules": [
                    {
                        "Policy": "accept",
                        "Status": "Available",
                        "Priority": 1,
                        "Protocol": "TCP",
                        "CreatedAt": "2021-08-05T21:46:55+08:00",
                        "UpdatedAt": "2021-08-05T21:46:55+08:00",
                        "Description": "TM_FilterRule_1",
                        "SourceCidrBlock": "0.0.0.0/0",
                        "SourcePortRange": "-1/-1",
                        "TrafficDirection": "ingress",
                        "DestinationCidrBlock": "0.0.0.0/0",
                        "DestinationPortRange": "-1/-1",
                        "TrafficMirrorFilterId": "tmf-bp1opxu1zkhn00123****",
                        "TrafficMirrorFilterRuleId": "tmr-j6cmls82xnc86vtpe****"
                    }
                ],
                "IngressFilterRules": [
                    {
                        "Policy": "accept",
                        "Status": "Available",
                        "Priority": 1,
                        "Protocol": "TCP",
                        "CreatedAt": "2021-08-05T21:46:55+08:00",
                        "UpdatedAt": "2021-08-05T21:46:55+08:00",
                        "Description": "TM_FilterRule_1",
                        "SourceCidrBlock": "0.0.0.0/0",
                        "SourcePortRange": "-1/-1",
                        "TrafficDirection": "ingress",
                        "DestinationCidrBlock": "0.0.0.0/0",
                        "DestinationPortRange": "-1/-1",
                        "TrafficMirrorFilterId": "tmf-bp1opxu1zkhn00123****",
                        "TrafficMirrorFilterRuleId": "tmr-j6cmls82xnc86vtpe****"
                    }
                ],
                "TrafficMirrorFilterId": "tmf-bp1opxu1zkhn00123****",
                "TrafficMirrorFilterName": "TM_Filter_1"
            }
        ]
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
|400 |InvalidTrafficMirrorFilter.Malformed |The specified traffic mirror filter is malformed. Ensure that IDs and names cannot be specified at the same time. |The specified Mirror Filter is invalid. Please ensure that the ID and the name cannot be specified simultaneously. |
|400 |LimitExceeded.TagFilterKey |You've reached the limit on the number of tag keys that you can filter. |You have reached the maximum number of filter tag keys that can be specified in a single request. |
|400 |LimitExceeded.TagFilterValue |You've reached the limit on the number of tag values that you can filter. |You have reached the maximum number of filter tag values that can be specified in a single request. |
|400 |LimitExceeded.TrafficMirrorFilterIds |You've reached the limit on the number of traffic mirror filter IDs that you can describe. |The maximum allowed number of Mirror Filter IDs for a single query has been reached. |
|400 |LimitExceeded.TrafficMirrorFilterNames |You've reached the limit on the number of traffic mirror filter names that you can describe. |The maximum allowed number of Mirror Filter names for a single query has been reached. |
