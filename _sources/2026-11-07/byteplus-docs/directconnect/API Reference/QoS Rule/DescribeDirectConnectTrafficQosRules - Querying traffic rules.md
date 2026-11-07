---
title: "DescribeDirectConnectTrafficQosRules - Querying traffic rules"
product: "Direct Connect"
product_code: "directconnect"
source: "https://docs.byteplus.com/en/docs/directconnect/DescribeDirectConnectTrafficQosRules"
---

Call DescribeDirectConnectTrafficQosRules to query traffic rules that meet the specified conditions.

<span id=".6LCD6K-V"></span>
## Debug

[去调试](https://api.byteplus.com/api-explorer/debug?action=DescribeDirectConnectTrafficQosRules&serviceCode=directconnect&version=2020-04-01&groupName=)


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters

The following only details request parameters specific to this API and key common parameters. For more information, see [Common parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).



**Action ** <span data-label="purple">String </span><span data-api-tag="require|Z8r7qt">必选</span>`Example: DescribeDirectConnectTrafficQosRules`

The interface name. The current API name is `DescribeDirectConnectTrafficQosRules`.



**Version ** <span data-label="purple">String </span><span data-api-tag="require|byL8gK">必选</span> `Example: 2020-04-01`

The interface version. The current API version is `2020-04-01`.



**DirectConnectTrafficQosRuleIds.N ** <span data-label="purple">String </span>`optional` `Example: dqr-bwbhc****`

The ID of the traffic rule.


* N represents the sequence number of a traffic rule.

* Separate multiple IDs with ampersands (&).



**DirectConnectTrafficQosQueueId ** <span data-label="purple">String </span>`optional` `Example: dcq-i718g7fap8t1t****`

The ID of the QoS policy to which the traffic rule belongs.

You can call [DescribeDirectConnectTrafficQosPolicies](https://docs.byteplus.com/en/docs/directconnect/DescribeDirectConnectTrafficQosPolicies) to query the QoS policy ID.



**DirectConnectTrafficQosRuleName ** <span data-label="purple">String </span>`optional` `Example: dcq-test`

The name of the QoS policy to which the traffic rule belongs.



**Priority ** <span data-label="purple">Integer </span>`optional` `Example: 1`

The priority of the traffic rule.



**Protocol ** <span data-label="purple">String </span>`optional` `Example: TCP`

The protocol type. Values:


* ICMP

* ICMPV6

* TCP

* UDP

* GRE

* ALL



**MatchDscp ** <span data-label="purple">Integer </span>`optional` `Example: 1`

The original DSCP value.



**RemarkingDscp ** <span data-label="purple">Integer </span>`optional` `Example: 2`

The retagged DSCP value.



**PageNumber ** <span data-label="purple">Integer </span>`optional` `Example: 1`

The page number of the list.


* Set a non\-negative integer to this parameter.

* If you omit it or set it to 0, the value defaults to 1.



**PageSize ** <span data-label="purple">Integer </span>`optional` `Example: 20`

The number of entries per page in a pagination query. Maximum: 100. Default: 20.



&nbsp;

<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters

The following only details response parameters specific to this API. For more information, see [Response structure](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response).



**PageSize ** <span data-label="purple">Integer </span>`Example: 20`

Number of entries per page in the current pagination.



**PageNumber ** <span data-label="purple">Integer </span>`Example: 1`

The current page number.



**TotalCount ** <span data-label="purple">Integer </span>`Example: 1`

The total number of traffic rules meeting the query conditions.



**DirectConnectTrafficQosRules ** <span data-label="purple">Object[] </span>`Example: -`

The list of traffic rules.


**Status ** <span data-label="purple">String </span>`Example: Available`

The status of the traffic rule.


* Creating

* Deleting

* Pending: ​​Configuration in progress.

* Available



**Priority ** <span data-label="purple">Integer </span>`Example: 10`

The priority of the traffic rule.



**Protocol ** <span data-label="purple">String </span>`Example: TCP`

The protocol type.



**MatchDscp ** <span data-label="purple">Integer </span>`Example: 10`

The value of Match DSCP.



**Description ** <span data-label="purple">String </span>`Example: test dqr`

The description of the traffic rule.



**RemarkingDscp ** <span data-label="purple">Integer </span>`Example: 16`

The retagged DSCP value.



**SourcePortEnd ** <span data-label="purple">Integer </span>`Example: 100`

The end value of the source port number range.



**SourceCidrBlock ** <span data-label="purple">String </span>`Example: 10.XX.XX.0/24`

The source CIDR block.



**SourcePortStart ** <span data-label="purple">Integer </span>`Example: 1`

The start value of the source port number range.



**DestinationPortEnd ** <span data-label="purple">Integer </span>`Example: 100`

The end value of the destination port number range.



**DestinationCidrBlock ** <span data-label="purple">String </span>`Example: 20.XX.XX.0/24`

The destination CIDR block.



**DestinationPortStart ** <span data-label="purple">Integer </span>`Example: 1`

The start value of the destination port number range.



**DirectConnectTrafficQosRuleId ** <span data-label="purple">String </span>`Example: dqr-18agtw13n58ycd09u****`

The ID of the traffic rule.



**DirectConnectTrafficQosQueueId ** <span data-label="purple">String </span>`Example: dqq-1gta6t1cwd4c8rh0***`

The ID of the traffic queue associated with the traffic rule.



**DirectConnectTrafficQosPolicyId ** <span data-label="purple">String </span>`Example: dcq-59agtw20n57ycd0ay****`

The ID of the QoS policy to which the traffic rule belongs.



**DirectConnectTrafficQosRuleName ** <span data-label="purple">String </span>`Example: dqr-18agtw1ycd09u****`

The name of the traffic rule.




&nbsp;

<span id=".6K-35rGC56S65L6L"></span>
## Request examples

```json
GET /?DirectConnectTrafficQosRuleName=dcq-test&DirectConnectTrafficQosQueueId=dqq-in0gqqzwvi808gbssy****&Action=DescribeDirectConnectTrafficQosRules&Version=2020-04-01&DirectConnectTrafficQosRuleIds.1=dqr-2fezsa5pcdnuo59gp68x**** HTTP/1.1
Host: directconnect.cn-beijing.byteplusapi.com.cn
X-Date: 20251121T094038Z
Authorization: HMAC-SHA256 Credential=Adfks******wekfwe/20251121/cn-beijing/directconnect/request, SignedHeaders=host;x-date, Signature=47a7d934ff7b37c03938******cd7b8278a40a1057690c401e92246a0e41085f
```


<span id=".6L-U5Zue56S65L6L"></span>
## Response examples

```json
{
    "ResponseMetadata": {
        "RequestId": "20230604110420****100232280022D31",
        "Action": "DescribeDirectConnectTrafficQosRules",
        "Version": "2020-04-01",
        "Service": "directconnect",
        "Region": "cn-north-1"
    },
    "Result": {
        "DirectConnectTrafficQosRules": [
            {
                "Status": "Available",
                "Priority": 10,
                "Protocol": "TCP",
                "MatchDscp": 10,
                "Description": "test dqr",
                "RemarkingDscp": 16,
                "SourcePortEnd": 100,
                "SourceCidrBlock": "10.XX.XX.0/24",
                "SourcePortStart": 1,
                "DestinationPortEnd": 100,
                "DestinationCidrBlock": "20.XX.XX.0/24",
                "DestinationPortStart": 1,
                "DirectConnectTrafficQosRuleId": "dqr-18agtw13n58ycd09u****",
                "DirectConnectTrafficQosQueueId": "dqq-1gta6t1cwd4c8rh0***",
                "DirectConnectTrafficQosPolicyId": "dcq-59agtw20n57ycd0ay****",
                "DirectConnectTrafficQosRuleName": "dqr-18agtw1ycd09u****"
            }
        ],
        "PageNumber": 1,
        "PageSize": 20,
        "TotalCount": 1
    }
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error codes

The table below describes the error codes for this API that are associated with business logic. For details, see [Common error codes](https://docs.byteplus.com/en/docs/directconnect/Public-error-codes).


|Status code |Error codes |Error message |Description |
|---|---|---|---|
|400 |DryRunOperation |Exception raised to indicate a successfully authorized action when the DryRun flag is set to true. |This request is set to DryRun. The action is authorized but not executed. |
|400 |InvalidPage.Malformed |The specified page is malformed. |The specified pagination parameter is invalid. |
|400 |LimitExceeded.DirectConnectTrafficQosRuleId |You've reached the limit on the number of direct connect traffic qos rule IDs that you can describe. |You have reached the maximum number of QoS traffic rules that can be queried. |
