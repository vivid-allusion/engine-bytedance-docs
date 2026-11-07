---
title: "DeleteRules - Deleting a forwarding rule"
product: "Cloud Load Balancer"
product_code: "clb"
source: "https://docs.byteplus.com/en/docs/clb/DeleteRules"
---

Call the DeleteRules API to delete forwarding rules from the specified HTTP/HTTPS listener.

<span id=".5L2_55So6K-05piO"></span>
## Instructions

You can delete up to 50 forwarding rules in a single API call.

<span id=".6LCD6K-V"></span>
## Debug

[去调试](https://api.byteplus.com/api-explorer/debug?action=DeleteRules&serviceCode=clb&version=2020-04-01&groupName=)


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters



**Action ** <span data-label="purple">String </span><span data-api-tag="require|i7hxb5">必选</span>`Example: DeleteRules`

Action to execute. Set the value to **DeleteRules**.



**Version ** <span data-label="purple">String </span><span data-api-tag="require|YK7Vmw">必选</span> `Example: 2020-04-01`

API version. The current version is **2020\-04\-01**.



**ListenerId ** <span data-label="purple">String </span><span data-api-tag="require|YKrZ1E">必选</span> `Example: lsn-2fek3rgsxhrsw5oxruwec****`

Listener ID.

You can call the [DescribeListeners](https://docs.byteplus.com/en/docs/clb/DescribeListeners) API to query the listener ID.



**RuleIds.N ** <span data-label="purple">String </span><span data-api-tag="require|2AZ68G">必选</span> `Example: rule-2fegss1cplxxc5oxruvvq****`

The ID of the forwarding rule. The forwarding rule must belong to the corresponding listener.

You can call the [DescribeRules](https://docs.byteplus.com/en/docs/clb/DescribeRules) API to query forwarding rule IDs.


* Parameter \- N: Represents the serial number of the forwarding rule, ranging from 1 to 50.

* Separate multiple forwarding rules with ampersands (&).



&nbsp;

<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters



**RequestId ** <span data-label="purple">String </span>`Example: 20210811152539010225146063030****`

Request ID.



&nbsp;

<span id=".6K-35rGC56S65L6L"></span>
## Request examples

```json
GET /?Action=DeleteRules&Version=2020-04-01&ListenerId=lsn-2fek3rgsxhrsw5oxruwec****&RuleIds.1=rule-2fegss1cplxxc5oxruvvq****
Host: clb.cn-beijing.byteplusapi.com.cn
X-Date: 20251121T094038Z
Authorization: HMAC-SHA256 Credential=Adfks******wekfwe/20251121/cn-beijing/clb/request, SignedHeaders=host;x-date, Signature=47a7d934ff7b37c03938******cd7b8278a40a1057690c401e92246a0e41085f
```


<span id=".6L-U5Zue56S65L6L"></span>
## Response examples

```json
{
    "ResponseMetadata": {
        "RequestId": "20230604110420****100232280022D31",
        "Action": "DeleteRules",
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

This section displays only the error codes of the current API. For more error codes, see [Common error codes](https://docs.byteplus.com/en/docs/clb/Public-error-codes).


|Status code |Error codes |Error message |Notes |
|---|---|---|---|
|400 |InvalidDefaultRule.UnSupportAction |The specified Default Rule does not support this action. |The specified default forwarding rule does not support the current action. |
|400 |InvalidLoadBalancer.InvalidStatus |The specified LoadBalancer is not in the correct status for the request. |The specified load balancer cannot respond to this request due to its status. |
|400 |MissingParameter |The request is missing a required parameter. Ensure that you have supplied all the required parameters for the request; for example, the 'ListenerId'. |This request is missing a required parameter. Please ensure the request includes all required parameters, such as ListenerId. |
|400 |MissingParameter |The request is missing a required parameter. Ensure that you have supplied all the required parameters for the request; for example, the ''. |This request is missing a required parameter. Ensure the request includes all required parameters, such as . |
|403 |Forbidden |You are not authorized to perform operations on the specified service. |You do not have permission to perform operations on the specified service. |
|403 |InvalidResourceType.ServcieManaged |The specified ResourceType is managed by a service. |The specified resource is a service\-managed resource. |
|404 |InvalidListener.NotFound |The specified Listener does not exist. |The specified listener does not exist. |
|404 |InvalidLoadBalancer.NotFound |The specified LoadBalancer does not exist. |The specified load balancer does not exist. |
|404 |InvalidRule.NotFound |The specified Rule does not exist. |The specified forwarding rule does not exist. |
|409 |InvalidRule.Conflict |The specified Rule already exists. |The specified forwarding rule already exists. |
|500 |InternalError |An internal error has occurred. |An internal error occurred. |
