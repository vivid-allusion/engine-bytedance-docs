---
title: "ModifyRules - Modifying a forwarding rule"
product: "Cloud Load Balancer"
product_code: "clb"
source: "https://docs.byteplus.com/en/docs/clb/ModifyRules"
---

Call the ModifyRules API to replace the backend server group corresponding to a forwarding rule in a specified HTTP/HTTPS listener, and to modify the description of the forwarding rule.

<span id=".5L2_55So6K-05piO"></span>
## Instructions


* The maximum number of rules that can be modified in a single API call is 50.

* When the `ServerGroupId` parameter is configured in the [CreateRules](https://docs.byteplus.com/en/docs/clb/CreateRules) API, a default forwarding rule is created to forward traffic to the specified backend server group. The default forwarding rule only supports modification of the backend server group.

* After August 30, 2021, the default backend server group feature was introduced for layer\-7 listeners. Existing layer\-7 listeners must configure a default backend server group for the listener by referring to the [ModifyListenerAttributes](https://docs.byteplus.com/en/docs/clb/ModifyListenerAttributes) API; otherwise, forwarding rules with empty domain names will be created.


<span id=".6LCD6K-V"></span>
## Debug

[去调试](https://api.byteplus.com/api-explorer/debug?action=ModifyRules&serviceCode=clb&version=2020-04-01&groupName=)


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters

In the following table, the "N" in parameters of the type a.N.b indicates the index of the forwarding rule, ranging from 1 to 50. Separate multiple forwarding rules with ampersands (&).



**Action ** <span data-label="purple">String </span><span data-api-tag="require|Z1puYp">必选</span> `Example: ModifyRules`

Action to execute. Set the value to **ModifyRules**.



**Version ** <span data-label="purple">String </span><span data-api-tag="require|FrzCd5">必选</span> `Example: 2020-04-01`

API version. The current version is **2020\-04\-01**.



**ListenerId ** <span data-label="purple">String </span><span data-api-tag="require|5rIgne">必选</span> `Example: lsn-2fek3rgsxhrsw5oxruwec****`

Listener ID.

You can call the [DescribeListeners](https://docs.byteplus.com/en/docs/clb/DescribeListeners) API to get the listener ID.



**Rules.N.RuleId ** <span data-label="purple">String </span><span data-api-tag="require|sSUr3s">必选</span> `Example: rule-2fegss1cplxxc5oxruvvq****`

ID of the forwarding rule.

You can call the [DescribeRules](https://docs.byteplus.com/en/docs/clb/DescribeRules) API to get the forwarding rule ID.



**Rules.N.ActionType ** <span data-label="purple">String </span>`optional` `Example: Forward`

The forwarding action of the forwarding rule. Valid values:


* Forward: Forward to.

* Redirect: Redirect to.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">The forwarding action of the default forwarding rule defaults to <code>Forward</code> and cannot be modified.</div>


* <div data-tips="true" data-tips-type="tip">When this parameter is set to <code>Redirect</code> and the parameter <code>Rules.N.RedirectConfig.Protocol</code> is the same as the protocol of the listener to which this forwarding rule belongs, the parameters <code>Rules.N.RedirectConfig.Host</code>, <code>Rules.N.RedirectConfig.Path</code>, and <code>Rules.N.RedirectConfig.Port</code> cannot all be empty.</div>




**Rules.N.ServerGroupId ** <span data-label="purple">String </span>`optional` `Example: rsp-bp1o94dp5i6ea****`

Backend server group ID. You can call the [DescribeServerGroups](https://docs.byteplus.com/en/docs/clb/DescribeServerGroups) API to get the backend server group ID.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">When the parameter <code>Rules.N.ActionType</code> is set to <code>Forward</code>, this parameter is required.</div>




**Rules.N.RedirectConfig.Protocol ** <span data-label="purple">String </span>`optional` `Example: HTTP`

The protocol for the forwarding rule redirection. Valid values:


* HTTP

* HTTPS


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">When the value of parameter <code>Rules.N.ActionType</code> is changed from <code>Forward</code> to <code>Redirect</code>, if this parameter is not passed or no value is passed, it defaults to HTTPS.</div>




**Rules.N.RedirectConfig.Host ** <span data-label="purple">String </span>`optional` `Example: www.test.com`

The domain name for the forwarding rule redirection. Currently, only exact domain names are supported. The requirements are as follows:


* Must contain at least one '.' but must not start or end with '.'.

* Only letters, numbers, '.', and '\-' are allowed.

* Length limit is 1 to 128 characters.

* An exact domain name that conforms to domain name specifications, for example: www.test.com.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">When the value of parameter <code>Rules.N.ActionType</code> is changed from <code>Forward</code> to <code>Redirect</code>, if this parameter is not passed or no value is passed, it defaults to an empty string, and during actual forwarding, it will be consistent with the request domain name.</div>




**Rules.N.RedirectConfig.Path ** <span data-label="purple">String </span>`optional` `Example: /abc`

The path for the forwarding rule redirection. The requirements are as follows:


* Must start with a forward slash "/". The character '/' cannot appear consecutively.

* May include letters, numbers, and symbols: '\-', '_', '/', '.', '%', '?', '#', '&', and '='.

* Length limit is 1 to 128 characters.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">When the value of parameter <code>Rules.N.ActionType</code> is changed from <code>Forward</code> to <code>Redirect</code>, if this parameter is not passed or no value is passed, it defaults to an empty string, and during actual forwarding, it will be consistent with the request path.</div>




**Rules.N.RedirectConfig.Port ** <span data-label="purple">String </span>`optional` `Example: 443`

The port for the forwarding rule redirection, valid values range from 1 to 65535.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">When the value of parameter <code>Rules.N.ActionType</code> is changed from <code>Forward</code> to <code>Redirect</code>, if this parameter is not passed or no value is passed, it defaults to an empty string, and during actual forwarding, it will be consistent with the request port.</div>




**Rules.N.RedirectConfig.StatusCode ** <span data-label="purple">String </span>`optional` `Example: 302`

The status code for the forwarding rule redirection. Valid values:


* 301: Indicates that the requested resource has been permanently moved to a new URL. The client should use the new URL for subsequent requests.

* 302: Indicates that the requested resource has been temporarily moved to a new URL. The client should use the new URL for subsequent requests, but it may change again in the future.

* 307: Similar to **302**, but requires the client to preserve the request method when redirecting. For example, if the original request is a GET request, it will remain a GET request after redirection.

* 308: Similar to **301**, but requires the client to keep the request method unchanged when redirecting.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">When the value of parameter <code>Rules.N.ActionType</code> is changed from <code>Forward</code> to <code>Redirect</code>, if this parameter is not passed or no value is passed, it defaults to 301.</div>




**Rules.N.Description ** <span data-label="purple">String </span>`optional` `Example: rule1`

Description of the forwarding rule. The requirements are as follows:


* Must start with a letter, number, or Chinese character. May include letters, numbers, Chinese characters, and the following symbols: commas (,), periods (.), underscores (_), spaces ( ), equal signs (=), hyphens (\-), full\-width commas ( ， ), and full\-width periods ( 。 ).

* The length limit is 0 to 255 characters.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">The default forwarding rule does not support modifying this parameter.</div>




&nbsp;

<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters



**RequestId ** <span data-label="purple">String </span>`Example: 20210811152539010225146063030****`

Request ID.



&nbsp;

<span id=".6K-35rGC56S65L6L"></span>
## Request examples

```json
GET /?Action=ModifyRules&Version=2020-04-01&ListenerId=lsn-2fek3rgsxhrsw5oxruwec****&Rules.1.RuleId=rule-2fegss1cplxxc5oxruvvq****&Rules.1.ServerGroupId=rsp-bp1o94dp5i6ea****&Rules.1.Description=test HTTP/1.1
Host: clb.cn-beijing.byteplusapi.com.cn
X-Date: 20251121T094038Z
Authorization: HMAC-SHA256 Credential=Adfks******wekfwe/20251121/cn-beijing/clb/request, SignedHeaders=host;x-date, Signature=47a7d934ff7b37c03938******cd7b8278a40a1057690c401e92246a0e41085f
```


<span id=".6L-U5Zue56S65L6L"></span>
## Response examples

```json
{
    "ResponseMetadata": {
        "RequestId": "20210811152539010225146063030****",
        "Action": "ModifyRules",
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
|400 |InvalidDescription.Malformed |The specified Description is malformed. |The format specified for Description is invalid. |
|400 |InvalidIncorrectOrder.Malformed |The specified index order is malformed. |The specified index order parameter format is invalid. |
|400 |InvalidLoadBalancer.InvalidStatus |The specified LoadBalancer is not in the correct status for the request. |The specified load balancer cannot respond to this request due to its status. |
|400 |InvalidRuleRedirectConfig.ActionTypeMismatch |The specified RedirectConfig not match with ActionType. |The specified redirection configuration is inconsistent with the forwarding type. |
|400 |InvalidRules.ActionType.Malformed |The specified Rules.ActionType is malformed. |The specified Rules.ActionType parameter format is invalid. |
|400 |InvalidRules.RedirectConfig.Host.Malformed |The specified Rules.RedirectConfig.Host is malformed. |The specified Rules.RedirectConfig.Host parameter format is invalid. |
|400 |InvalidRules.RedirectConfig.Path.Malformed |The specified Rules.RedirectConfig.Path is malformed. |The specified Rules.RedirectConfig.Path parameter format is invalid. |
|400 |InvalidRules.RedirectConfig.Port.Malformed |The specified Rules.RedirectConfig.Port is malformed. |The specified Rules.RedirectConfig.Port parameter format is invalid. |
|400 |InvalidRules.RedirectConfig.Protocol.Malformed |The specified Rules.RedirectConfig.Protocol is malformed. |The specified Rules.RedirectConfig.Protocol parameter format is invalid. |
|400 |InvalidRules.RedirectConfig.StatusCode.Malformed |The specified Rules.RedirectConfig.StatusCode is malformed. |The specified Rules.RedirectConfig.StatusCode parameter format is invalid. |
|400 |InvalidServerGroup.ActionTypeMismatch |The specified ServerGroup not match with ActionType. |The specified backend server group is inconsistent with the forwarding type. |
|400 |InvalidServerGroup.UnSupportAction |The specified ServerGroup does not support this action. |The specified Server Group does not support the current action. |
|400 |LimitExceeded.Rule |You've reached the limit on the number of rules that you can operate. |The upper limit on the number of operable forwarding rules has been reached. |
|400 |MissingParameter |The request is missing a required parameter. Ensure that you have supplied all the required parameters for the request; for example, the 'Rules.RedirectConfig.Host, Rules.RedirectConfig.Path, Rules.RedirectConfig.Port'. |This request is missing a required parameter. Please ensure the request includes all required parameters, such as Rules.RedirectConfig.Host, Rules.RedirectConfig.Path, Rules.RedirectConfig.Port. |
|400 |MissingParameter |The request is missing a required parameter. Ensure that you have supplied all the required parameters for the request; for example, the ''. |This request is missing a required parameter. Ensure the request includes all required parameters, such as . |
|400 |MissingParameter |The request is missing a required parameter. Ensure that you have supplied all the required parameters for the request; for example, the 'ListenerId'. |This request is missing a required parameter. Please ensure the request includes all required parameters, such as ListenerId. |
|400 |UnsupportedOperation.AccountArrears |The request on the specified instance is denied due to the account in arrears status. |The action request on this instance is denied because the account is in arrears. |
|403 |Forbidden |You are not authorized to perform operations on the specified service. |You do not have permission to perform operations on the specified service. |
|403 |InvalidResourceType.ServcieManaged |The specified ResourceType is managed by a service. |The specified resource is a service\-managed resource. |
|404 |InvalidExclusiveCluster.NotFound |The specified ExclusiveCluster does not exist. |The specified Exclusive Cluster does not exist. |
|404 |InvalidListener.NotFound |The specified Listener does not exist. |The specified listener does not exist. |
|404 |InvalidLoadBalancer.NotFound |The specified LoadBalancer does not exist. |The specified load balancer does not exist. |
|404 |InvalidRule.NotFound |The specified Rule does not exist. |The specified forwarding rule does not exist. |
|404 |InvalidServerGroup.NotFound |The specified ServerGroup does not exist. |The specified server group does not exist. |
|409 |InvalidRule.Conflict |The specified Rule already exists. |The specified forwarding rule already exists. |
|412 |InvalidExclusiveCluster.Expired |The specified ExclusiveCluster has expired. |The specified Exclusive Cluster has expired. |
|412 |InvalidExclusiveCluster.UnPurchased |The specified ExclusiveCluster is not purchased. |The specified Exclusive Cluster is not purchased. |
|412 |InvalidLoadBalancer.Expired |The specified LoadBalancer has expired. |The specified CLB has expired. |
|500 |InternalError |An internal error has occurred. |An internal error occurred. |
