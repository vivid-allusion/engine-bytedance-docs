---
title: "DescribeNLBSecurityPolicies - Querying the qualified TLS custom security policy"
product: "Cloud Load Balancer"
product_code: "clb"
source: "https://docs.byteplus.com/en/docs/clb/DescribeNLBSecurityPolicies"
---

Call the DescribeNLBSecurityPolicies API to query TLS custom security policies that meet the specified criteria.

## Instructions

This API is only used to query custom TLS security policies. To query system security policies, please call [DescribeNLBSystemSecurityPolicies](https://docs.byteplus.com/en/docs/clb/DescribeNLBSystemSecurityPolicies).

## Debug

[去调试](https://api.byteplus.com/api-explorer/debug?action=DescribeNLBSecurityPolicies&serviceCode=clb&version=2020-04-01&groupName=)

## Request parameters

**Action ** String必选 `Example: DescribeNLBSecurityPolicies`

Action to execute. Set value to DescribeNLBSecurityPolicies.

**Version ** String必选 `Example: 2020-04-01`

Current API version is 2020\-04\-01.

**SecurityPolicyName ** String`optional` `Example: TLSCipherPolicy`

Name of the TLS custom security policy.

**SecurityPolicyIds.N ** String`optional` `Example: secp-wuytp9pa****`

TLS custom security policy ID.

* Parameter \- N specifies the serial number of the TLS custom security policy. The value range is 1 to 20.

* Separate multiple TLS custom security policy IDs with ampersands (&).

**ProjectName ** String`optional` `Example: default`

Name of the project to which the TLS security policy belongs.

**TagFilters.N.Key ** String`optional` `Example: k1`

The tag key. If multiple tag keys are specified, this API returns NLB instances that contain all of the specified tag keys.

* N specifies the serial number of a tag key. Valid values: 1\-10.

* Separate multiple tag keys with ampersands ( & ).

**TagFilters.N.Values.N ** String`optional` `Example: v1`

The tag value.

* The first N specifies the serial number of a tag key. Valid values: 1\-10.

* The second N specifies the serial number of a tag value. Valid values: 1\-3. The relationship between multiple tag values for the same tag key is a logical "OR". That is, the query returns resources tagged with any one of the specified values for that key.

* Separate multiple tags with ampersands (&).

> **tip**

* > To provide this parameter, you must first provide `TagFilters.N.Key`.

* > When an empty value is set for this parameter, it means querying resources where the tag value is empty under the specified tag key.

**NextToken ** String`optional` `Example: caeba0bbb2be03f84eb48b699f0a****`

The pagination token that is used to mark the position in pagination queries.

* If left blank, the query starts from the beginning.

* Provide the NextToken returned from a previous call to this API, the query continues from that pagination position.

**MaxResults ** Integer`optional` `Example: 50`

The number of query results. Default: 10. Maximum: 100.

## Response parameters

**RequestId ** String`Example: 20210811152539010225146063030****`

Request ID.

**NextToken ** String`Example: caeba0bbb2be03f84eb48b699f0a****`

Pagination token used to mark the position in paginated results. Leave this empty for the initial API call. For subsequent queries, set this value to the NextToken parameter returned by the previous API call.

**SecurityPolicies ** Object[]`Example: -`

Detailed information on the TLS security policies that meet the criteria.

**CreateTime ** String`Example: 2024-08-11T16:37:37Z`

Creation time of the TLS security policy.

**UpdateTime ** String`Example: 2024-08-11T16:37:37Z`

Last modified time of TLS security policy.

**SecurityPolicyId ** String`Example: secp-wuytp9pa******`

TLS custom security policy ID.

**AccountId ** String`Example: 210012****`

The account ID to which the TLS security policy belongs.

**ProjectName ** String`Example: default`

Name of the project to which the TLS security policy belongs.

**Status ** String`Example: Active`

TLS security policy status

**SecurityPolicyName ** String`Example: "test"`

Name of TLS security policy;

**TlsVersions ** String[]`Example: ["TLSv1.0", "TLSv1.1"]`

TLS protocol version.

**Ciphers ** String[]`Example: ["ECDHE-ECDSA-AES128-SHA", "ECDHE-ECDSA-AES256-SHA"]`

Supported cipher suite list.

**RelatedListenerIds ** String[]`Example: ["lsn-2zeo05qre24nhrqpy****", "lsn-b2weev3esweer8mt****"]`

Listeners associated with the TLS security policy;

**Tags ** Object[]`Example: --`

Tag information of the TLS security policy.

**Key ** String`Example: k1`

The tag key.

**Value ** String`Example: v1`

The tag value.

## Request examples

```json
GET /?Action=DescribeNLBSecurityPolicies&Version=2020-04-01&SecurityPolicyName=TLSCipherPolicy&SecurityPolicyIds.1=secp-wuytp9pa****&ProjectName=default&TagFilters.1.Key=k1&TagFilters.1.Values.1=v1&NextToken=caeba0bbb2be03f84eb48b699f0a****&MaxResults=50 HTTP/1.1
Host: clb.cn-beijing.byteplusapi.com.cn
Date: 20260310T094038Z
Authorization: HMAC-SHA256 Credential=Adfks******wekfwe/20251121/cn-beijing/clb/request, SignedHeaders=host;x-date, Signature=47a7d934ff7b37c03938******cd7b8278a40a1057690c401e92246a0e41085f
```

## Response examples

```json
{
    "ResponseMetadata": {
        "RequestId": "20230604110420****100232280022D31",
        "Action": "DescribeNLBSecurityPolicies",
        "Version": "2020-04-01",
        "Service": "clb",
        "Region": "cn-beijing"
    },
    "Result": {
        "NextToken": "caeba0bbb2be03f84eb48b699f0a****",
        "RequestId": "20210811152539010225146063030****",
        "SecurityPolicies": [
            {
                "Tags": [
                    {
                        "Key": "k1",
                        "Value": "v1"
                    }
                ],
                "Status": "Active",
                "Ciphers": [
                    "ECDHE-ECDSA-AES128-SHA",
                    "ECDHE-ECDSA-AES256-SHA"
                ],
                "AccountId": "210012****",
                "CreateTime": "2024-08-11T16:37:37Z",
                "UpdateTime": "2024-08-11T16:37:37Z",
                "ProjectName": "default",
                "TlsVersions": [
                    "TLSv1.0",
                    "TLSv1.1"
                ],
                "SecurityPolicyId": "secp-wuytp9pa******",
                "RelatedListenerIds": [
                    "lsn-2zeo05qre24nhrqpy****",
                    "lsn-b2weev3esweer8mt****"
                ],
                "SecurityPolicyName": "\"test\""
            }
        ]
    }
}
```

## Error codes

This section displays only the error codes of the current API. For more error codes, see [Common error codes](https://docs.byteplus.com/en/docs/clb/NLB-Common-Error-Codes).

|Status code |Error codes |Error message |Notes |
|---|---|---|---|
|400 |DryRunOperation |Exception raised to indicate a successfully authorized action when the DryRun flag is set to true. |This request is set to DryRun. The action is authorized but not executed. |
|400 |IdempotentParameterMismatch |Arguments on this idempotent request are inconsistent with arguments used in previous request(s). |The parameters of this idempotent request are inconsistent with those used in the previous request. |
|400 |InvalidClientToken.Malformed |The specified ClientToken is malformed. |The specified ClientToken format is invalid. |
|400 |InvalidIncorrectOrder.Malformed |The specified index order is malformed. |The specified index order parameter format is invalid. |
|400 |InvalidMaxResult.Malformed |The specified MaxResult is malformed. |The specified MaxResult parameter format is invalid. |
|400 |InvalidMaxResults.Malformed |The specified MaxResults is malformed. |The specified MaxResults parameter format is invalid. |
|400 |InvalidNextToken.Malformed |The specified NextToken is malformed. |The specified NextToken parameter format is invalid. |
|400 |InvalidPaging.Malformed |The specified PageNumber or PageSize is malformed. |The format specified for pagination parameter is invalid. |
|400 |InvalidSecurityPolicyName.Malformed |The specified SecurityPolicyName is malformed. |The specified SecurityPolicyName parameter format is invalid. |
|400 |InvalidTagKey.Malformed |The specified TagKey is malformed. |The specified TagKey parameter format is invalid. |
|400 |InvalidTagValue.Malformed |The specified TagValue is malformed. |The specified TagValue parameter format is invalid. |
|400 |LimitExceeded.SecurityPolicyId |You've reached the limit on the number of SecurityPolicyId that you can operate. |The maximum number of resources that can be operated on security policies in a single request has been reached. |
|400 |LimitExceeded.TagFilterKey |You've reached the limit on the number of tag keys that you can filter. |You have reached the maximum number of tag keys that you can specify for filtering in a single request. |
|400 |LimitExceeded.TagFilterValues |You've reached the limit on the number of tag values that you can filter. |The maximum tag key\-value pairs for filtering in a single request has been reached. |
|409 |InvalidOperation.Conflict |The specified resource operation conflicts. |The specified resource action conflicted. |
|412 |IdempotentProcessing |The request uses the same client token as a previous one that is still in process. |The idempotent request is in progress. |
