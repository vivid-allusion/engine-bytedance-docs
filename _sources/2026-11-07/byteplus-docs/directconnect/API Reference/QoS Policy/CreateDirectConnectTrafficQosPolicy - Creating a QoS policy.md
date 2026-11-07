---
title: "CreateDirectConnectTrafficQosPolicy - Creating a QoS policy"
product: "Direct Connect"
product_code: "directconnect"
source: "https://docs.byteplus.com/en/docs/directconnect/CreateDirectConnectTrafficQosPolicy"
---

Call CreateDirectConnectTrafficQosPolicy to create a Quality of Service (QoS) policy.

<span id=".5L2_55So6K-05piO"></span>
## Instructions

For more details and limits about QoS policies, see [QoS Policy overview](https://docs.byteplus.com/en/docs/directconnect/QoS_policy_overview).

<span id=".6LCD6K-V"></span>
## Debug

[去调试](https://api.byteplus.com/api-explorer/debug?action=CreateDirectConnectTrafficQosPolicy&serviceCode=directconnect&version=2020-04-01&groupName=)


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters

The following only details request parameters specific to this API and key common parameters. For more information, see [Common parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).



**Action ** <span data-label="purple">String </span><span data-api-tag="require|fT14N4">必选</span> `Example: CreateDirectConnectTrafficQosPolicy`

The interface name. The current API name is `CreateDirectConnectTrafficQosPolicy`.



**Version ** <span data-label="purple">String </span><span data-api-tag="require|r0Rxnm">必选</span> `Example: 2020-04-01`

The interface version. The current API version is `2020-04-01`.



**DirectConnectTrafficQosPolicyName ** <span data-label="purple">String </span>`optional` `Example: Qos-policy01`

The name of the QoS policy.


* Must start with a Chinese character, letter, or number. May include Chinese characters, letters, numbers, periods (.), underscores (_), and hyphens (\-).

* Must be 1 to 128 characters.

* If left blank, this parameter defaults to the ID of the QoS policy.



**Description ** <span data-label="purple">String </span>`optional` `Example: test-description`

The description for the QoS policy.


* Must start with a Chinese character, letter, or number. May include Chinese characters, letters, numbers, periods (.), spaces ( ), underscores (_), hyphens (\-), equals signs (=), commas (,), Chinese commas (，), and Chinese periods (。).

* Must be 0 to 255 characters.

* If left blank, it defaults to an empty string.



**ClientToken ** <span data-label="purple">String </span>`optional` `Example: 2133cad2-b374-11ee-8599-93bf8a0f4****`

Client Token that is used to ensure the request idempotency.


* You can use the client to automatically generate a token, but must confirm that the tokens for different requests are unique. This prevents repeated actions due to multiple client retries when the call of the API action times out or an internal server error occurs.

* Must not exceed 64 ASCII characters.

* If you do not provide ClientToken, this API call does not verify idempotency.



&nbsp;

<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters

The following only details response parameters specific to this API. For more information, see [Response structure](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response).



**DirectConnectTrafficQosPolicyId ** <span data-label="purple">String </span>`Example: dcq-2fezrjmq3vif459gp67f****`

The ID of the QoS Policy.



&nbsp;

<span id=".6K-35rGC56S65L6L"></span>
## Request examples

```json
GET /?Action=CreateDirectConnectTrafficQosPolicy&DirectConnectTrafficQosPolicyName=traffic-qos&Description=traffic-qos&Version=2020-04-01 HTTP/1.1
Host: directconnect.cn-beijing.byteplusapi.com.cn
X-Date: 20251121T094038Z
Authorization: HMAC-SHA256 Credential=Adfks******wekfwe/20251121/cn-beijing/directconnect/request, SignedHeaders=host;x-date, Signature=47a7d934ff7b37c03938******cd7b8278a40a1057690c401e92246a0e41085f
```


<span id=".6L-U5Zue56S65L6L"></span>
## Response examples

```json
{
    "ResponseMetadata": {
        "RequestId": "20241107154811619C155E4BE5275****",
        "Action": "CreateDirectConnectTrafficQosPolicy",
        "Version": "2020-04-01",
        "Service": "directconnect",
        "Region": "cn-beijing"
    },
    "Result": {
        "RequestId": "20241107154811619C155E4BE5275****",
        "DirectConnectTrafficQosPolicyId": "dcq-2fezrjmq3vif459gp67f****"
    }
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error codes

The table below describes the error codes for this API that are associated with business logic. For more information, see [Common error codes](https://docs.byteplus.com/en/docs/directconnect/Public-error-codes).


|Status code |Error codes |Error message |Description |
|---|---|---|---|
|400 |DryRunOperation |Exception raised to indicate a successfully authorized action when the DryRun flag is set to true. |This request is set to DryRun. The action is authorized but not executed. |
|400 |IdempotentParameterMismatch |Arguments on this idempotent request are inconsistent with arguments used in previous request(s). |The parameters of this idempotent request are inconsistent with those used in the previous request. |
|400 |InvalidDescription.Malformed |The specified description is malformed. Ensure the maximum length of description is 255. |The format of specified description is invalid. A description must not exceed 255 characters. |
|400 |InvalidDescription.Malformed |The specified description is malformed. |The format of specified description is invalid. Correct the description format and retry. |
|400 |InvalidName.Malformed |The specified name is malformed. |The format of the specified name is invalid. Correct the name format and retry. |
|400 |InvalidName.Malformed |The specified name is malformed. Ensure the maximum length of name is 128. |The format of specified name is invalid. A name must not exceed 128 characters. |
|400 |InvalidParameter.ClientTokenMalformed |The specified parameter ClientToken is malformed. |The format of specified CientToken is invalid. It must not exceed 64 ASCII characters. |
|400 |QuotaExceeded.DcTrafficQosPolicy |You've reached the limit on the number of traffic qos policies that you can create. |You have reached the maximum number of QoS policies that can be created. |
|403 |InvalidDirectConnectTrafficQosPolicy.Forbidden |You are not authorized to create a direct connect traffic qos policy. |No permission to create QoS policies. |
|409 |InvalidOperation.Conflict |The specified resource operation conflicts. |The specified resource action conflicted. |
|412 |IdempotentProcessing |The request uses the same client token as a previous one that is still in process. |The idempotent request is in progress. |
