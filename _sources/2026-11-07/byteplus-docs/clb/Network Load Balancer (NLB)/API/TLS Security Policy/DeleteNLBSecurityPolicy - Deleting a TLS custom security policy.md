---
title: "DeleteNLBSecurityPolicy - Deleting a TLS custom security policy"
product: "Cloud Load Balancer"
product_code: "clb"
source: "https://docs.byteplus.com/en/docs/clb/DeleteNLBSecurityPolicy"
---

Call the DeleteNLBSecurityPolicy API to delete the TLS custom security policy.

<span id=".5rOo5oSP5LqL6aG5"></span>
## Precautions

System security policy cannot be deleted.

<span id=".6LCD6K-V"></span>
## Debug

[去调试](https://api.byteplus.com/api-explorer/debug?action=DeleteNLBSecurityPolicy&serviceCode=clb&version=2020-04-01&groupName=)


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters



**Action ** <span data-label="purple">String </span><span data-api-tag="require|cvR4lA">必选</span> `Example: DeleteNLBSecurityPolicy`

Action to execute. Set the value to DeleteNLBSecurityPolicy.



**Version ** <span data-label="purple">String </span><span data-api-tag="require|IUWGXj">必选</span> `Example: 2020-04-01`

Current API version is 2020\-04\-01.



**SecurityPolicyId ** <span data-label="purple">String </span><span data-api-tag="require|esEsmR">必选</span> `Example: secp-wuytp9pa****`

TLS custom security policy ID.

You can call the [DescribeNLBSecurityPolicies](https://docs.byteplus.com/en/docs/clb/DescribeNLBSecurityPolicies) API to query the ID of the TLS custom security policy.



**ClientToken ** <span data-label="purple">String </span>`optional` `Example: 123e4567-e89b-12d3-a456-42665544****`

Client Token that is used to ensure the request idempotency.


* You can use the client to automatically generate a token, but must confirm that the tokens for different requests are unique. This prevents repeated actions due to multiple client retries when the call of the API action times out or an internal server error occurs.

* Must not exceed 64 ASCII characters.

* If you do not provide ClientToken, this API call does not verify idempotency.



&nbsp;

<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters



**RequestId ** <span data-label="purple">String </span>`Example: 20210811152539010225146063030****`

Request ID.



&nbsp;

<span id=".6K-35rGC56S65L6L"></span>
## Request examples

```json
GET /?Action=DeleteNLBSecurityPolicy&Version=2020-04-01&SecurityPolicyId=secp-wuytp9pa****&ClientToken=123e4567-e89b-12d3-a456-42665544**** HTTP/1.1
Host: clb.cn-beijing.byteplusapi.com.cn
Date: 20260310T094038Z
Authorization: HMAC-SHA256 Credential=Adfks******wekfwe/20251121/cn-beijing/clb/request, SignedHeaders=host;x-date, Signature=47a7d934ff7b37c03938******cd7b8278a40a1057690c401e92246a0e41085f
```


<span id=".6L-U5Zue56S65L6L"></span>
## Response examples

```json
{
    "ResponseMetadata": {
        "RequestId": "20230604110420****100232280022D31",
        "Action": "DeleteNLBSecurityPolicy",
        "Version": "2020-04-01",
        "Service": "clb",
        "Region": "cn-beijing"
    },
    "Result": {
        "RequestId": "20210811152539010225146063030****"
    }
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error codes

This section displays only the error codes of the current API. For more error codes, see [Common error codes](https://docs.byteplus.com/en/docs/clb/NLB-Common-Error-Codes).


|Status code |Error codes |Error message |Notes |
|---|---|---|---|
|400 |DryRunOperation |Exception raised to indicate a successfully authorized action when the DryRun flag is set to true. |This request is set to DryRun. The action is authorized but not executed. |
|400 |IdempotentParameterMismatch |Arguments on this idempotent request are inconsistent with arguments used in previous request(s). |The parameters of this idempotent request are inconsistent with those used in the previous request. |
|400 |InvalidClientToken.Malformed |The specified ClientToken is malformed. |The specified ClientToken format is invalid. |
|400 |InvalidSecurityPolicy.InvalidStatus |The specified SecurityPolicy is not in the correct status for the request. |The specified security policy cannot respond to this request due to its status. |
|400 |InvalidSecurityPolicyListener.InUse |The specified SecurityPolicy has dependent resources Listener is in use. |The specified security policy is associated with a listener and is currently in use. |
|400 |QuotaExceed.SecurityPolicyNumber |You've reached the limit on the number of security policies that you can create. |The maximum quota for creating security policies has been reached. |
|403 |InvalidResourceType.ServiceManaged |The specified ResourceType is managed by a service. |The specified resource is a service\-managed resource. |
|404 |InvalidSecurityPolicy.NotFound |The specified SecurityPolicy does not exist. |The specified security policy does not exist. |
|409 |InvalidOperation.Conflict |The specified resource operation conflicts. |The specified resource action conflicted. |
|412 |IdempotentProcessing |The request uses the same client token as a previous one that is still in process. |The idempotent request is in progress. |
