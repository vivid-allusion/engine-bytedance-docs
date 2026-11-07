---
title: "DescribeTrafficMirrorTargets - Querying a traffic mirror target"
product: "Virtual Private Cloud"
product_code: "vpc"
source: "https://docs.byteplus.com/en/docs/vpc/DescribeTrafficMirrorTargets"
---

Call the DescribeTrafficMirrorTargets API to query mirror targets that meet specified conditions.

## Instructions

* If multiple request parameters are provided, the query will return Mirror Target entries that match all the specified conditions. If no matching entry is found, an empty value is returned.

* If none of the optional request parameters are provided, the query will be performed under the current logged\-in account and return all Mirror Targets belonging to this account.

## Debug

[去调试](https://api.byteplus.com/api-explorer/debug?action=DescribeTrafficMirrorTargets&serviceCode=vpc&version=2020-04-01&groupName=)

## Request parameters

The following only details request parameters specific to this API and key common parameters. More information can be found in [Common parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).

**Action ** String必选 `Example: DescribeTrafficMirrorTargets`

The interface name. The current API name is `DescribeTrafficMirrorTargets`.

**Version ** String必选 `Example: 2020-04-01`

The interface version. the current API version is `2020-04-01`.

**TrafficMirrorTargetName ** String`optional` `Example: TM_Target_1`

Name of the mirror target.

**TrafficMirrorTargetIds.N ** String`optional` `Example: tmt-35bvae1r7rv283dy2w2ll****`

Mirror Target ID.

* Parameter \- N: Represents the serial number of the Traffic Mirror Target ID. The maximum number of entries per request is 100.

* Separate multiple Mirror Target IDs with ampersands (&).

**ProjectName ** String`optional` `Example: default`

The project to which the Traffic Mirror Target belongs.

**TagFilters.N.Key ** String`optional` `Example: k1`

The tag key.

* N represents the sequence number of a tag key. Values: 1\-10.

* Separate multiple tag keys with &. Multiple tag keys have a logical AND relationship. The query returns Traffic Mirror Targets tagged with all the specified keys.

**TagFilters.N.Values.N ** String`optional` `Example: v1`

The tag value.

* The first N represents the sequence number of a tag key.

* The second N represents the sequence number of a tag value. Valid values: 1–3. Multiple tag values under the same tag key are combined using a logical OR operation, meaning the query returns Traffic Mirror Targets that have any of the specified tag values for that key.

* Separate multiple tag values with ampersands (&).

> **tip**

* > If this parameter is passed in, `TagFilters.N.Key` must be passed in first.

* > Passing an empty string queries for Traffic Mirror Targets with an empty tag value.

**NextToken ** String`optional` `Example: caeba0bbb2be03f84eb48b699f0a****`

The pagination token that is used to mark the position in pagination queries.

* If left blank, the query starts from the beginning.

* Provide the `NextToken` returned from a previous call to this API, the query continues from that pagination position.

**MaxResults ** Integer`optional` `Example: 50`

The number of query results. Default: 10. Maximum: 100.

## Response parameters

Only the response parameters specific to this API are listed below. More information, see [Response structure](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response).

**RequestId ** String`Example: 2021062415303301022514515207C4****`

Request ID.

**NextToken ** String`Example: caeba0bbb2be03f84eb48b699f0a****`

The pagination token returned by this API call, which marks the position for the next query. An empty return indicates there is no next page.

**TrafficMirrorTargets ** Object[]`Example: -`

Details of TrafficMirrorTargets.

**InstanceType ** String`Example: NetworkInterface`

Resource type of the Traffic Mirror Target.

* NetworkInterface: Elastic network interface.

* ClbInstance: Classic Load Balancer.

**InstanceId ** String`Example: eni-171l3vhbti9ds4d1w34rq****`

Resource ID of the Traffic Mirror Target.

**TrafficMirrorTargetId ** String`Example: tmt-35bvae1r7rv283dy2w2ll****`

Mirror Target ID.

**TrafficMirrorTargetName ** String`Example: TM_Target_1`

Traffic Mirror Target name.

**Description ** String`Example: TM_Target_1_Description`

Description of the traffic mirror target.

**Status ** String`Example: Available`

Status of the Traffic Mirror Target.

* Available

* Creating

**CreatedAt ** String`Example: 2021-08-05T21:46:55+08:00`

Creation time of the Traffic Mirror Session.

**UpdatedAt ** String`Example: 2021-08-05T21:46:55+08:00`

Update time of Traffic Mirror Session.

**ProjectName ** String`Example: default`

The name of the project to which the Mirror Target belongs.

**Tags ** Object[]`Example: -`

Tag information for the Traffic Mirror Target.

**Key ** String`Example: k1`

The tag key.

**Value ** String`Example: v1`

The tag value.

## Request examples

```json
GET /?Action=DescribeTrafficMirrorTargets&Version=2020-04-01&NextToken=caeba0bbb2be03f84eb48b699f0a****&MaxResults=50 HTTP/1.1
Host: vpc.cn-beijing.byteplusapi.com.cn
X-Date: 20250804T033538Z
Authorization: HMAC-SHA256 Credential=Adfks******wekfwe/20250804/cn-beijing/vpc/request, SignedHeaders=host;x-date, Signature=47a7d934ff7b37c03938******cd7b8278a40a1057690c401e92246a0e41085f
```

## Response examples

```json
{
    "ResponseMetadata": {
        "RequestId": "20230604110420****100232280022D31",
        "Action": "DescribeTrafficMirrorTargets",
        "Version": "2020-04-01",
        "Service": "vpc",
        "Region": "cn-beijing"
    },
    "Result": {
        "NextToken": "caeba0bbb2be03f84eb48b699f0a****",
        "RequestId": "2021062415303301022514515207C4****",
        "TrafficMirrorTargets": [
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
                "InstanceId": "eni-171l3vhbti9ds4d1w34rq****",
                "Description": "TM_Target_1_descirption",
                "ProjectName": "default",
                "InstanceType": "NetworkInterface",
                "TrafficMirrorTargetId": "tmt-35bvae1r7rv283dy2w2ll****",
                "TrafficMirrorTargetName": "TM_Target_1"
            }
        ]
    }
}
```

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
|400 |LimitExceeded.TagFilterKey |You've reached the limit on the number of tag keys that you can filter. |You have reached the maximum number of filter tag keys that can be specified in a single request. |
|400 |LimitExceeded.TagFilterValue |You've reached the limit on the number of tag values that you can filter. |You have reached the maximum number of filter tag values that can be specified in a single request. |
|400 |LimitExceeded.TrafficMirrorTargetIds |You've reached the limit on the number of traffic mirror target IDs that you can describe. |The maximum allowed number of traffic mirror target IDs for a single query has been reached. |
