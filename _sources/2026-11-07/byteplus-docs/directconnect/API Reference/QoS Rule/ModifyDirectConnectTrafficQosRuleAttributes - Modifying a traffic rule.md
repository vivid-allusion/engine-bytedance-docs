---
title: "ModifyDirectConnectTrafficQosRuleAttributes - Modifying a traffic rule"
product: "Direct Connect"
product_code: "directconnect"
source: "https://docs.byteplus.com/en/docs/directconnect/ModifyDirectConnectTrafficQosRuleAttributes"
---

Call ModifyDirectConnectTrafficQosRuleAttributes to update information for a specified default traffic rule.

<span id=".5L2_55So6K-05piO"></span>
## Instructions


* This API only supports modifying default traffic rules. Manually added traffic rules cannot be modified. To modify, call [DeleteDirectConnectTrafficQosRule](https://docs.byteplus.com/en/docs/directconnect/DeleteDirectConnectTrafficQosRule) to delete the rule and then call [CreateDirectConnectTrafficQosRule](https://docs.byteplus.com/en/docs/directconnect/CreateDirectConnectTrafficQosRule) to recreate it.

* Only the retagged DSCP of the default traffic rule can be modified. Other information cannot be changed.


<span id=".6LCD6K-V"></span>
## Debug

[去调试](https://api.byteplus.com/api-explorer/debug?action=ModifyDirectConnectTrafficQosRuleAttributes&serviceCode=directconnect&version=2020-04-01&groupName=)


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters

The following only details request parameters specific to this API and key common parameters. For more information, see [Common parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).



**Action ** <span data-label="purple">String </span><span data-api-tag="require|6dhDgx">必选</span> `Example: ModifyDirectConnectTrafficQosRuleAttributes`

The interface name. The current API name is `ModifyDirectConnectTrafficQosRuleAttributes`.



**Version ** <span data-label="purple">String </span><span data-api-tag="require|IFwG2R">必选</span> `Example: 2020-04-01`

The interface version. The current API version is `2020-04-01`.



**DirectConnectTrafficQosRuleId** <span data-label="purple">String</span> <span data-api-tag="require|RWhGDr">必选</span> `Example: dqr-1jfwefksx5****`

The ID of the default traffic rule.

You can call [DescribeDirectConnectTrafficQosRules](https://docs.byteplus.com/en/docs/directconnect/DescribeDirectConnectTrafficQosRules) to query the traffic rule ID. The queue with `DirectConnectTrafficQosRuleName` set to `Default` and `Priority` set to `65535` is a default traffic rule.



**Remarking DSCP ** <span data-label="purple">Integer </span><span data-api-tag="require|FUVSZ4">必选</span> `Example: 53`

Modify the DSCP value in the traffic. Value range: 0\-63. Use \-1 if not effective.



&nbsp;

<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters

This API does not have specific response parameters. For more information, see [Response structure](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response).

<span id=".6K-35rGC56S65L6L"></span>
## Request examples

```json
GET /?Action=ModifyDirectConnectTrafficQosRuleAttributes&Version=2020-04-01&DirectConnectTrafficQosRuleId=dqr-in0gq79lqygw8gbssy0q****&RemarkingDscp=45 HTTP/1.1
Host: directconnect.cn-beijing.byteplusapi.com.cn
X-Date: 20251121T094038Z
Authorization: HMAC-SHA256 Credential=Adfks******wekfwe/20251121/cn-beijing/directconnect/request, SignedHeaders=host;x-date, Signature=47a7d934ff7b37c03938******cd7b8278a40a1057690c401e92246a0e41085f
```


<span id=".6L-U5Zue56S65L6L"></span>
## Response examples

```json
{
    "ResponseMetadata": {
        "RequestId": "20241107160755EC1FDE4A8330156****",
        "Action": "ModifyDirectConnectTrafficQosRuleAttributes",
        "Version": "2020-04-01",
        "Service": "directconnect",
        "Region": "cn-beijing"
    },
    "Result": {
        "RequestId": "20241107160755EC1FDE4A8330156****"
    }
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error codes

The table below describes the error codes for this API that are associated with business logic. For more information, see [Common error codes](https://docs.byteplus.com/en/docs/directconnect/Public-error-codes).


|Status code |Error codes |Error message |Description |
|---|---|---|---|
|400 |DryRunOperation |Exception raised to indicate a successfully authorized action when the DryRun flag is set to true. |This request is set to DryRun. The action is authorized but not executed. |
|400 |InvalidDirectConnectTrafficQosPolicy.InvalidStatus |The specified direct connect traffic qos policy is not in the correct status for the request. |The specified QoS policy cannot respond to this request due to its status. |
|400 |InvalidDirectConnectTrafficQosQueue.InvalidStatus |The specified direct connect traffic qos queue is not in the correct status for the request. |The specified QoS traffic queue cannot respond to this request due to its status. |
|400 |InvalidDirectConnectTrafficQosRule.CustomRuleUnsupported |It is not supported to modify the direct connect traffic qos rule with custom priority. |Modifying custom QoS traffic rules is not supported. |
|400 |InvalidDirectConnectTrafficQosRule.InvalidRemarkingDscp |The specified remarking dscp of the direct connect traffic qos rule is invalid. Remarking dscp only support \-1, 0~63. |The retagged DSCP of the specified QoS traffic rule is invalid. It must be \-1 or an integer between 0 and 63. |
|400 |InvalidDirectConnectTrafficQosRule.InvalidStatus |The specified direct connect traffic qos rule is not in the correct status for the request. |The specified QoS traffic rule cannot respond to this request due to its status. |
|404 |InvalidDirectConnectTrafficQosRule.NotFound |The specified direct connect traffic qos rule does not exist. |The specified QoS traffic rule does not exist. |
