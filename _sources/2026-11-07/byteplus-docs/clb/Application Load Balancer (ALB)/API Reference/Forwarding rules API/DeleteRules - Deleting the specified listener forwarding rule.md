---
title: "DeleteRules - Deleting the specified listener forwarding rule"
product: "Cloud Load Balancer"
product_code: "clb"
source: "https://docs.byteplus.com/en/docs/clb/ALB-DeleteRules"
---

Call the DeleteRules API to delete specified listener forwarding rules.

<span id=".5L2_55So6K-05piO"></span>
## Instructions

Submit up to 5 API requests per second.

<span id=".6LCD6K-V"></span>
## Debug

[去调试](https://api.byteplus.com/api-explorer/?action=DeleteRules&groupName=%E8%BD%AC%E5%8F%91%E8%A7%84%E5%88%99&serviceCode=alb&version=2020-04-01)


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters

The following only details request parameters specific to this API and key common parameters. More information can be found in [Common parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).



**Action ** <span data-label="purple">string </span><span data-api-tag="require|izDCGs">必选</span> `Example: DeleteRules`

Action to execute. Set the value to DeleteRules.



**Version ** <span data-label="purple">string </span><span data-api-tag="require|AH7s8h">必选</span> `Example: 2020-04-01`

The API version. Value: 2020\-04\-01.



**RuleIds.N ** <span data-label="purple">string[] </span><span data-api-tag="require|G2LzhB">必选</span> `Example: RuleIds.1=rule-****&RuleIds.2=rule-****`

The ID of the forwarding rule. The forwarding rule must belong to the corresponding listener. If none of the specified forwarding rules exist, then an error is returned.


* Parameter \- N: N represents the serial number of the forwarding rule, ranging from 1 to 20.

* Separate multiple forwarding rules with ampersands (&).



**ListenerId ** <span data-label="purple">string </span><span data-api-tag="require|i6VhB5">必选</span> `Example: lsn-2fea4ayvu2g3k5oxruuz****`

Listener ID.



&nbsp;

<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters

Only the response parameters specific to this API are listed below. More information, see [Response structure](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response).



**RequestId ** <span data-label="purple">string </span>`Example: 20210811152539010225146063030****`

Request ID.



&nbsp;

<span id=".6K-35rGC56S65L6L"></span>
## Request examples

```text
GET /?Action=DeleteRules&ListenerId=lsn-1g0puwcx****8g8ibuxxw2pmf7&RuleIds.1=rule-1g0pux***a9s8ibuxy0p2l88&Version=2020-04-01 HTTP/1.1
Host: alb.cn-beijing.byteplusapi.com.cn
X-Date: 20251121T094038Z
Authorization: HMAC-SHA256 Credential=Adfks******wekfwe/20251121/cn-beijing/alb/request, SignedHeaders=host;x-date, Signature=47a7d934ff7b37c03938******cd7b8278a40a1057690c401e92246a0e41085f
```


<span id=".6L-U5Zue56S65L6L"></span>
## Response examples

```text
{
    "ResponseMetadata": {
        "RequestId": "2021081317494****22514214202F3FE94",
        "Action": "DeleteRules",
        "Version": "2020-04-01",
        "Service": "alb",
        "Region": "cn-beijing"
    },
    "Result": {
        "RequestId": "2021081317494801022514214202F3FE94"
    }
}

```


<span id=".6ZSZ6K-v56CB"></span>
## Error codes

The following table lists the error codes related to the business logic for this API. For details, see [Common error codes](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-error-codes).


|Status code |Error codes |Error message |Notes |
|---|---|---|---|
|400 |Invalid%s.Malformed |MismatchThe specified %s is malformed. |The specified %s parameter format is invalid. |
|400 |MissingParameter |The request is missing a required parameter. Ensure that you have supplied all the required parameters for the request; for example, '%s'. |This request is missing a required parameter. Please ensure the request includes all required parameters, such as: %s. |
|400 |InvalidParameter |Data unmarshal failed. |Failed to parse the request. |
|400 |LimitExceed.Rule |You've reached the limit on the number of rules that you can operate at a time. |The maximum number of forwarding rules that can be operated in a single instance has been reached. |
|400 |InvalidRuleIds.Duplicated |The specified RuleIds is duplicated. |The specified RuleIds is duplicated. |
|400 |InvalidLoadBalancer.InvalidStatus |The specified LoadBalancer is not in the correct status for the request. |The specified ALB is in a state that cannot respond to this request. |
|400 |InvalidServerGroup.InvalidStatus |The specified ServerGroup is not in the correct status for the request. |The specified server group is in a status that cannot respond to the request. |
|403 |Forbidden |You are not authorized to perform operations on the default rule. |You do not have permission to operate the default forwarding rule. |
|404 |InvalidListener.NotFound |The specified Listener does not exist. |The specified listener does not exist. |
|404 |InvalidRule.NotFound |The specified Rule does not exist. |The specified forwarding rule does not exist. |
|500 |InternalError |An internal error has occurred. |An internal error occurred. Please try again later or contact an engineer for further consultation. |
