---
title: "DescribeNLBSystemSecurityPolicies - Querying the TLS system security policy"
product: "Cloud Load Balancer"
product_code: "clb"
source: "https://docs.byteplus.com/en/docs/clb/DescribeNLBSystemSecurityPolicies"
---

Call the DescribeNLBSystemSecurityPolicies API to query the TLS system security policy.

## Instructions

This API is only used to query TLS system security policies. To query custom security policies, please call [DescribeNLBSecurityPolicies](https://docs.byteplus.com/en/docs/clb/DescribeNLBSecurityPolicies).

## Debug

[去调试](https://api.byteplus.com/api-explorer/debug?action=DescribeNLBSystemSecurityPolicies&serviceCode=clb&version=2020-04-01&groupName=)

## Request parameters

**Action ** String必选 `Example: DescribeNLBSystemSecurityPolicies`

Action to execute. Set the value to DescribeNLBSystemSecurityPolicies.

**Version ** String必选 `Example: 2020-04-01`

Current API version is 2020\-04\-01.

**SecurityPolicyIds.N ** String`optional` `Example: SecurityPolicyIds.1=tls_cipher_policy_1_0`

TLS system security policy ID.

* Parameter \- N specifies the serial number of the TLS system security policy, with a range from 1 to 20.

* Separate multiple TLS system security policy IDs with ampersands ( & ).

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

Detailed information on TLS system security policies that meet the condition.

**SecurityPolicyId ** String`Example: tls_cipher_policy_1_0`

TLS system security policy ID.

**SecurityPolicyName ** String`Example: tls_cipher_policy_1_0`

TLS system security policy ID.

**TlsVersions ** String[]`Example: ["TLSv1.0", "TLSv1.1","TLSv1.2"]`

TLS protocol version.

**Ciphers ** String[]`Example: ["ECDHE-ECDSA-AES256-GCM-SHA384", "ECDHE-ECDSA-AES128-GCM-SHA256", "ECDHE-ECDSA-AES256-SHA384","ECDHE-ECDSA-AES128-SHA256","ECDHE-RSA-AES256-GCM-SHA384","ECDHE-RSA-AES128-GCM-SHA256", "ECDHE-RSA-AES256-SHA384","ECDHE-RSA-AES128-SHA256", "AES256-GCM-SHA384", "AES128-GCM-SHA256","AES256-SHA256", "AES128-SHA256","ECDHE-ECDSA-AES256-SHA","ECDHE-ECDSA-AES128-SHA","ECDHE-RSA-AES256-SHA", "ECDHE-RSA-AES128-SHA","AES256-SHA","AES128-SHA", "DES-CBC3-SHA"]`

Supported cipher suite list.

## Request examples

```json
GET /?Action=DescribeNLBSystemSecurityPolicies&Version=2020-04-01&SecurityPolicyIds.1=tls_cipher_policy_1_0&NextToken=caeba0bbb2be03f84eb48b699f0a****&MaxResults=50 HTTP/1.1 
Host: clb.cn-beijing.byteplusapi.com.cn 
Date: 20260310T094038Z 
Authorization: HMAC-SHA256 Credential=Adfks******wekfwe/20251121/cn-beijing/clb/request, SignedHeaders=host;x-date, Signature=47a7d934ff7b37c03938******cd7b8278a40a1057690c401e92246a0e41085f
```

## Response examples

```json
{
    "ResponseMetadata": {
        "RequestId": "20230604110420****100232280022D31",
        "Action": "DescribeNLBSystemSecurityPolicies",
        "Version": "2020-04-01",
        "Service": "clb",
        "Region": "cn-beijing"
    },
    "Result": {
        "NextToken": "caeba0bbb2be03f84eb48b699f0a****",
        "RequestId": "20210811152539010225146063030****",
        "SecurityPolicies": [
            {
                "Ciphers": [
                    "ECDHE-ECDSA-AES256-GCM-SHA384",
                    "ECDHE-ECDSA-AES128-GCM-SHA256",
                    "ECDHE-ECDSA-AES256-SHA384",
                    "ECDHE-ECDSA-AES128-SHA256",
                    "ECDHE-RSA-AES256-GCM-SHA384",
                    "ECDHE-RSA-AES128-GCM-SHA256",
                    "ECDHE-RSA-AES256-SHA384",
                    "ECDHE-RSA-AES128-SHA256",
                    "AES256-GCM-SHA384",
                    "AES128-GCM-SHA256",
                    "AES256-SHA256",
                    "AES128-SHA256",
                    "ECDHE-ECDSA-AES256-SHA",
                    "ECDHE-ECDSA-AES128-SHA",
                    "ECDHE-RSA-AES256-SHA",
                    "ECDHE-RSA-AES128-SHA",
                    "AES256-SHA",
                    "AES128-SHA",
                    "DES-CBC3-SHA"
                ],
                "TlsVersions": [
                    "TLSv1.0",
                    "TLSv1.1",
                    "TLSv1.2"
                ],
                "SecurityPolicyId": "tls_cipher_policy_1_0",
                "SecurityPolicyName": "tls_cipher_policy_1_0"
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
|400 |InvalidMaxResult.Malformed |The specified MaxResult is malformed. |The specified MaxResult parameter format is invalid. |
|400 |InvalidMaxResults.Malformed |The specified MaxResults is malformed. |The specified MaxResults parameter format is invalid. |
|400 |InvalidNextToken.Malformed |The specified NextToken is malformed. |The specified NextToken parameter format is invalid. |
|400 |InvalidPaging.Malformed |The specified PageNumber or PageSize is malformed. |The format specified for pagination parameter is invalid. |
|400 |LimitExceeded.SecurityPolicyId |You've reached the limit on the number of SecurityPolicyId that you can operate. |The maximum number of resources that can be operated on security policies in a single request has been reached. |
|400 |MissingParameter |The request is missing a required parameter. Ensure that you have supplied all the required parameters for the request; for example, the ''. |This request does not contain required parameters. Ensure the request includes all required parameters, such as . |
|409 |InvalidOperation.Conflict |The specified resource operation conflicts. |The specified resource action conflicted. |
|412 |IdempotentProcessing |The request uses the same client token as a previous one that is still in process. |The idempotent request is in progress. |
|500 |InternalError |An internal error has occurred. |An internal error occurred. |
