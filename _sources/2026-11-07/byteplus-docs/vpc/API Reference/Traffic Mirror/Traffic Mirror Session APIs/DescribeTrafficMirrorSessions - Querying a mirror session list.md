---
title: "DescribeTrafficMirrorSessions - Querying a mirror session list"
product: "Virtual Private Cloud"
product_code: "vpc"
source: "https://docs.byteplus.com/en/docs/vpc/DescribeTrafficMirrorSessions"
---

Call the DescribeTrafficMirrorSessions API to query mirror sessions that meet the specified conditions.

## Instructions

* If multiple request parameters are provided, the query will return Mirror Session entries that match all the specified conditions. If no matching entry is found, an empty value is returned.

* If none of the optional request parameters are provided, the query will be performed under the current logged\-in account and return all Mirror Sessions belonging to this account.

## Debug

[去调试](https://api.byteplus.com/api-explorer/debug?action=DescribeTrafficMirrorSessions&serviceCode=vpc&version=2020-04-01&groupName=)

## Request parameters

The table below lists only the request parameters unique to this interface and some common parameters. For more information, see [Common parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).

**Action ** String必选 `Example: DescribeTrafficMirrorSessions`

Interface name. The current API name is `DescribeTrafficMirrorSessions`.

**Version ** String必选 `Example: 2020-04-01`

The interface version. The current API version is `2020-04-01`.

**TrafficMirrorSessionNames.N ** String`optional` `Example: TM_Session_1`

Name of the Traffic Mirror Session.

**TrafficMirrorSessionIds.N ** String`optional` `Example: tms-j6cmls82xnc86vtpe****`

ID of the Traffic Mirror Session.

* Parameter \- N: Represents the serial number of the Traffic Mirror Session ID. The maximum number of entries per request is 100.

* Separate multiple Mirror Session IDs with ampersands (&).

**NetworkInterfaceId ** String必选 `Example: eni-bp1fgnh68xyz9****`

Network Interface ID of the mirror site. You can call [DescribeNetworkInterfaces](https://docs.byteplus.com/en/docs/vpc/DescribeNetworkInterfaces) API to query Network Interfaces that meet the conditions.

**TrafficMirrorTargetId ** String`optional` `Example: tmt-35bvae1r7rv283dy2w2ll****`

ID of the Traffic Mirror Target.

You can call the [DeleteTrafficMirrorTarget](https://docs.byteplus.com/en/docs/vpc/DeleteTrafficMirrorTarget) API to query the ID of the traffic mirror target.

**TrafficMirrorFilterId ** String`optional` `Example: tmf-bp1opxu1zkhn00123****`

ID of the Traffic Mirror Filter.

You can call the [DescribeTrafficMirrorFilters](https://docs.byteplus.com/en/docs/vpc/DescribeTrafficMirrorFilters) API to query the ID of the traffic mirror filter.

**VirtualNetworkId ** Integer`optional` `Example: 2`

VNI of Traffic Mirror Session.

**PacketLength ** Integer`optional` `Example: 9600`

Data packet size of the traffic mirror session.

**Priority ** Integer`optional` `Example: 1`

Set the priority of the Traffic Mirror Session.

**ProjectName ** String`optional` `Example: default`

Project to which the traffic mirror session belongs.

**TagFilters.N.Key ** String`optional` `Example: k1`

The tag key.

* N represents the serial number of a tag key. Valid values: 1–10.

* Separate multiple tag keys with ampersands ( & ). Multiple tag keys have a logical AND relationship. The query returns Traffic Mirror Sessions tagged with all the specified keys.

**TagFilters.N.Values.N ** String`optional` `Example: v1`

The tag value.

* The first N specifies the serial number of the tag key.

* The second N represents the serial number of the tag value. Valid values: 1–3. Multiple tag values under the same tag key are combined using a logical OR operation, meaning the query returns Traffic Mirror Sessions that have any of the specified tag values for that key.

* Separate multiple tag values with ampersands (&).

> **tip**

* > If this parameter is provided, `TagFilters.N.Key` must be provided first.

* > Passing an empty string queries for Traffic Mirror Sessions with an empty tag value.

**NextToken ** String`optional` `Example: caeba0bbb2be03f84eb48b699f0a****`

The pagination token that is used to mark the position in paginated queries.

* If left blank, the query starts from the beginning.

* Provide the `NextToken` returned from a previous call to this API, the query continues from that pagination position.

**MaxResults ** Integer`optional` `Example: 50`

The number of query results. Default: 10. Maximum: 100.

## Response parameters

Only the response parameters specific to this API are listed below. For more information, see [Response structure](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response).

**RequestId ** String`Example: 2021062415303301022514515207C4****`

Request ID.

**NextToken ** String`Example: caeba0bbb2be03f84eb48b699f0a****`

The pagination token returned by this API call, which marks the position for the next query. An empty return indicates there is no next page.

**TrafficMirrorSessions ** Object[]`Example: -`

Details of TrafficMirrorSessions.

**TrafficMirrorSessionId ** String`Example: tms-j6cmls82xnc86vtpe****`

ID of the Traffic Mirror Session.

**TrafficMirrorTargetId ** String`Example: tmt-35bvae1r7rv283dy2w2ll****`

ID of the Traffic Mirror Target.

**TrafficMirrorFilterId ** String`Example: tmf-bp1opxu1zkhn00123****`

ID of the Traffic Mirror Filter.

**TrafficMirrorSourceIds ** String[]`Example: eni-35bvae1r7rv283dy2w2ll****`

Network interface list of mirror site.

> Currently, a single mirror session supports associating with only one mirror site.

**Priority ** Integer`Example: 1`

Traffic mirror session priority.

**PacketLength ** Integer`Example: 9600`

Data packet size of the traffic mirror session.

**TrafficMirrorSessionName ** String`Example: TM_Session_1`

Traffic Mirror Session name.

**Description ** String`Example: TM_Session_1_Description`

Description of the Traffic Mirror Session.

**Status ** String`Example: Active`

Traffic Mirror Session status.

* Creating

* Deleting

* Pending: Modifying.

* Active: Available.

* Inactive: Suspended.

**BusinessStatus ** String`Example: Normal`

Billing status of the Traffic Mirror Session.

* Normal

* FinancialLocked: Being locked.

**LockReason ** String`Example: Financial`

Reason of locked.

* financial: Being locked due to arrears.

* unlock: In the process of recharge recovery after being suspended due to arrears.

**VirtualNetworkId ** Integer`Example: 2`

VNI of Traffic Mirror Session.

**CreatedAt ** String`Example: 2021-08-05T21:46:55+08:00`

Creation time of the Traffic Mirror Session.

**UpdatedAt ** String`Example: 2021-08-05T21:46:55+08:00`

Update time of Traffic Mirror Session.

**ProjectName ** String`Example: default`

Name of the project to which the Traffic Mirror Session belongs.

**Tags ** Object[]`Example: -`

Tag information of the mirror session.

**Key ** String`Example: k1`

The tag key.

**Value ** String`Example: v1`

The tag value.

## Request example

```json
GET /?Action=DescribeTrafficMirrorSessions&Version=2020-04-01&NetworkInterfaceId=eni-bp1fgnh68xyz9****&NextToken=caeba0bbb2be03f84eb48b699f0a****&MaxResults=50 HTTP/1.1
Host: vpc.cn-beijing.byteplusapi.com.cn
X-Date: 20250804T033538Z
Authorization: HMAC-SHA256 Credential=Adfks******wekfwe/20250804/cn-beijing/vpc/request, SignedHeaders=host;x-date, Signature=47a7d934ff7b37c03938******cd7b8278a40a1057690c401e92246a0e41085f
```

## Response example

```json
{
    "ResponseMetadata": {
        "RequestId": "20230604110420****100232280022D31",
        "Action": "DescribeTrafficMirrorSessions",
        "Version": "2020-04-01",
        "Service": "vpc",
        "Region": "cn-beijing"
    },
    "Result": {
        "NextToken": "caeba0bbb2be03f84eb48b699f0a****",
        "RequestId": "2021062415303301022514515207C4****",
        "TrafficMirrorSessions": [
            {
                "Tags": [
                    {
                        "Key": "k1",
                        "Value": "v1"
                    }
                ],
                "Status": "Active",
                "Priority": 1,
                "CreatedAt": "2021-08-05T21:46:55+08:00",
                "UpdatedAt": "2021-08-05T21:46:55+08:00",
                "LockReason": "Financial",
                "Description": "TM_Session_1_Description",
                "ProjectName": "default",
                "PacketLength": 9600,
                "BusinessStatus": "Normal",
                "VirtualNetworkId": 2,
                "TrafficMirrorFilterId": "tmf-bp1opxu1zkhn00123****",
                "TrafficMirrorTargetId": "tmt-35bvae1r7rv283dy2w2ll****",
                "TrafficMirrorSessionId": "tms-j6cmls82xnc86vtpe****",
                "TrafficMirrorSourceIds": [
                    "eni-35bvae1r7rv283dy2w2ll****"
                ],
                "TrafficMirrorSessionName": "TM_Session_1"
            }
        ]
    }
}
```

## Error codes

|Status code |Error codes |Error message |Description |
|---|---|---|---|
|400 |DryRunOperation |Exception raised to indicate a successfully authorized action when the DryRun flag is set to true. |This request is set to DryRun action. The action has been authorized but has not been executed. |
|400 |InvalidMaxResults.Malformed |The specified parameter MaxResults is malformed. |The number of queries is invalid. |
|400 |InvalidNextToken.Malformed |The specified parameter NextToken is invalid. |NextToken is invalid for the query. |
|400 |InvalidPage.Malformed |The specified page is malformed. |The specified pagination parameter is invalid. |
|400 |InvalidTagFilter.Disorder |The specified index order of tag filter is malformed. |The index order format specified for the tag filter is invalid. |
|400 |InvalidTagFilterKey.Malformed |The specified parameter tag filter key is invalid. |The tag key for filtering is invalid. |
|400 |InvalidTagFilterValue.Malformed |The specified parameter tag filter value is invalid. |The tag filter value is invalid. |
|400 |InvalidTrafficMirrorSession.Malformed |The specified traffic mirror session is malformed. Ensure that IDs and names cannot be specified at the same time. |The specified Traffic Mirror Session is invalid. Please ensure that the ID and the name cannot be specified simultaneously. |
|400 |LimitExceeded.TagFilterKey |You've reached the limit on the number of tag keys that you can filter. |The maximum number of filter tag keys that can be specified in a single request has been reached. |
|400 |LimitExceeded.TagFilterValue |You've reached the limit on the number of tag values that you can filter. |The maximum number of filter tag values that can be specified in a single request has been reached. |
|400 |LimitExceeded.TrafficMirrorSessionIds |You've reached the limit on the number of traffic mirror session IDs that you can describe. |The maximum allowed number of mirror session IDs for a single query has been reached. |
|400 |LimitExceeded.TrafficMirrorSessionNames |You've reached the limit on the number of traffic mirror session names that you can describe. |The maximum allowed number of mirror session names for a single query has been reached. |
