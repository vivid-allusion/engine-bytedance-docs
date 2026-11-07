---
title: "DeleteDirectConnectTrafficQosRule - Deleting a specified traffic rule"
product: "Direct Connect"
product_code: "directconnect"
source: "https://docs.byteplus.com/en/docs/directconnect/DeleteDirectConnectTrafficQosRule"
---

Call DeleteDirectConnectTrafficQosRule to delete a specified traffic rule.

<span id=".5L2_55So6K-05piO"></span>
## Instructions

Only manually created traffic rules can be deleted. Default traffic rules cannot be deleted. You can call [DescribeDirectConnectTrafficQosRules](https://docs.byteplus.com/en/docs/directconnect/DescribeDirectConnectTrafficQosRules) to query the traffic rule ID. The queue with DirectConnectTrafficQosRuleName set to **Default** and Priority set to **65535** is a default traffic rule.

<span id=".6LCD6K-V"></span>
## Debug

[去调试](https://api.byteplus.com/api-explorer/debug?action=DeleteDirectConnectTrafficQosRule&serviceCode=directconnect&version=2020-04-01&groupName=)


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters

The following only details request parameters specific to this API and key common parameters. For more information, see [Common parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).



**Action ** <span data-label="purple">String </span><span data-api-tag="require|cvyyjb">必选</span> `Example: DeleteDirectConnectTrafficQosRule`

The interface name. The current API name is `DeleteDirectConnectTrafficQosRule`.



**Version ** <span data-label="purple">String </span><span data-api-tag="require|nLPajz">必选</span> `Example: 2020-04-01`

The interface version. The current API version is `2020-04-01`.



**DirectConnectTrafficQosRuleId ** <span data-label="purple">String </span><span data-api-tag="require|499iQP">必选</span> `Example: dqr-6o5erg54rrg4****`

The ID of the traffic rule to be deleted.

You can call the [DescribeDirectConnectTrafficQosRules](https://docs.byteplus.com/en/docs/directconnect/DescribeDirectConnectTrafficQosRules) API to query the traffic rule ID.



&nbsp;

<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters

This API does not have specific response parameters. For more information, see [Response structure](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response).

<span id=".6K-35rGC56S65L6L"></span>
## Request examples

```json
GET /?Action=DeleteDirectConnectTrafficQosRule&Version=2020-04-01&DirectConnectTrafficQosRuleId=dqr-2fezs9g1xwy6859gp67tyw**** HTTP/1.1
Host: directconnect.cn-beijing.byteplusapi.com.cn
X-Date: 20251121T094038Z
Authorization: HMAC-SHA256 Credential=Adfks******wekfwe/20251121/cn-beijing/directconnect/request, SignedHeaders=host;x-date, Signature=47a7d934ff7b37c03938******cd7b8278a40a1057690c401e92246a0e41085f
```


<span id=".6L-U5Zue56S65L6L"></span>
## Response examples

```json
{
    "ResponseMetadata": {
        "RequestId": "2024110716053568499AEFD8A1035B****",
        "Action": "DeleteDirectConnectTrafficQosRule",
        "Version": "2020-04-01",
        "Service": "directconnect",
        "Region": "cn-beijing"
    },
    "Result": {
        "RequestId": "2024110716053568499AEFD8A1035B****"
    }
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error codes

The table below describes the error codes for this API that are associated with business logic. For details, see [Common error codes](https://docs.byteplus.com/en/docs/directconnect/Public-error-codes).


|Status code |Error codes |Error message |Description |
|---|---|---|---|
|400 |DryRunOperation |Exception raised to indicate a successfully authorized action when the DryRun flag is set to true. |This request is set to DryRun. The action is authorized but not executed. |
|400 |InvalidDirectConnectTrafficQosPolicy.InvalidStatus |The specified direct connect traffic qos policy is not in the correct status for the request. |The specified QoS policy cannot respond to this request due to its status. |
|400 |InvalidDirectConnectTrafficQosQueue.InvalidStatus |The specified direct connect traffic qos queue is not in the correct status for the request. |The specified QoS traffic queue cannot respond to this request due to its status. |
|400 |InvalidDirectConnectTrafficQosRule.DeleteDefaultPriority |It is not supported to delete the direct connect traffic qos rule with default priority. |Deleting QoS traffic rules with default priority is not supported. |
|400 |InvalidDirectConnectTrafficQosRule.InvalidStatus |The specified direct connect traffic qos rule is not in the correct status for the request. |The specified QoS traffic rule cannot respond to this request due to its status. |
|400 |QuotaExceeded.DcTrafficQosRule |You've reached the limit on the number of traffic qos rules that you can create. |You have reached the maximum number of QoS traffic rules that can be created. |
|404 |InvalidDirectConnectTrafficQosRule.NotFound |The specified direct connect traffic qos rule does not exist. |The specified QoS traffic rule does not exist. |
