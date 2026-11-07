---
title: "CreateRules - Creating a forwarding rule"
product: "Cloud Load Balancer"
product_code: "clb"
source: "https://docs.byteplus.com/en/docs/clb/CreateRules"
---

Call the CreateRules API to add forwarding rules for a specified HTTP/HTTPS listener. These rules are used to forward requests for different domain names or different URLs to different backend server groups.

## Instructions

* A maximum of 50 forwarding rules can be added to each HTTP/HTTPS listener, excluding the default forwarding rule.

* You can add up to 50 forwarding rules in a single API call.

## Debug

[去调试](https://api.byteplus.com/api-explorer/debug?action=CreateRules&serviceCode=clb&version=2020-04-01&groupName=)

## Request parameters

In the following table, the "N" in parameters of the type a.N.b indicates the index of the forwarding rule, ranging from 1 to 50. Separate multiple forwarding rules with ampersands (&).

**Action ** String必选 `Example: CreateRules`

Action to execute. Set the value to **CreateRules**.

**Version ** String必选 `Example: 2020-04-01`

API version. The current version is **2020\-04\-01**.

**ListenerId ** String必选 `Example: lsn-2fea4ayvu2g3k5oxruuz****`

Listener ID.

You can call the [DescribeListeners](https://docs.byteplus.com/en/docs/clb/DescribeListeners) API to query the listener ID.

**Rules.N.Domain ** String`optional` `Example: www.test.com`

Domain names for forwarding rules, supporting wildcard and exact domains. The requirements are as follows:

* Must contain at least one '.' but must not start or end with '.'.

* Only letters, numbers, '.', '\-', and '\*' are allowed.

* Length must be between 1 and 128 characters.

* Wildcard domain: Use "\*" to replace one or more characters.

   * The "\*" must be at the beginning or end of the domain name.

   * "\*" cannot appear twice in the same domain name.

   * No characters other than '.' are allowed before or after '\*'.

   * Valid examples:  *.com, www.test.* .

   * Invalid example: *aaa.com, www.* .com

* Exact Domain Name​​: Must comply with domain name specifications (e.g., www.test.com).

> **tip**

> At least one of `Rules.N.Domain` and `Rules.N.Url` must be specified, and the combination of `Rules.N.Domain` and `Rules.N.Url` must be unique within the same listener.

**Rules.N.Url ** String`optional` `Example: /poo`

URL of the forwarding rule, only absolute paths are supported. The requirements are as follows:

* Must start with a forward slash "/".

* Only characters including letters, digits, `-`, `_`, `/`, `.`, `%`, `?`, `#`, `&`, and `=` are allowed.

* URL supporting regular expressions: must start with` ~`, supports uppercase and lowercase letters, digits, and special characters `. - _ / = ? ~ ^ * $ : ( ) [ ] + |`. The tilde (~) must be placed at the start and may appear only once.

* The character `/` cannot appear consecutively.

* Length limit is 1 to 128 characters.

* If `Domain` is specified, when `Url` is not provided, it defaults to `/`.

> **tip**

* > One of `Rules.N.Domain` or `Rules.N.Url` must be specified. The combination of `Rules.N.Domain` and `Rules.N.Url` parameter values must be unique within the same listener.

* > When `Rules.N.Domain` is set to empty, `Rules.N.Url` must not be only a forward slash "/".

**Rules.N.ActionType ** String`optional` `Example: Forward`

The forwarding action of the forwarding rule. Values:

* Forward: Forward to.

* Redirect: Redirect to.

> **tip**

> When this parameter is set to `Redirect` and the parameter `Rules.N.RedirectConfig.Protocol` is the same as the protocol of the listener to which this forwarding rule belongs, the parameters `Rules.N.RedirectConfig.Host`, `Rules.N.RedirectConfig.Path`, and `Rules.N.RedirectConfig.Port` cannot all be empty.

**Rules.N.ServerGroupId ** String`optional` `Example: rsp-bp1o94dp5i6ea****`

The backend server group ID associated with the forwarding rule. You can call the [DescribeServerGroups](https://docs.byteplus.com/en/docs/clb/DescribeServerGroups) API to get the backend server group ID.

> **tip**

> When the parameter `Rules.N.ActionType` is set to `Forward`, this parameter is required.

**Rules.N.RedirectConfig.Protocol ** String`optional` `Example: HTTPS`

The protocol for the forwarding rule redirection. Values:

* HTTP

* HTTPS (default)

> **tip**

> When the parameter `Rules.N.ActionType` is set to `Redirect`, if this parameter is not specified or no value is provided, it defaults to HTTPS.

**Rules.N.RedirectConfig.Host ** String`optional` `Example: www.test.com`

The domain name for the forwarding rule redirection. Currently, only exact domain names are supported. The requirements are as follows:

* Must contain at least one '.' but must not start or end with '.'.

* Only letters, numbers, '.', and '\-' are allowed.

* Length limit is 1 to 128 characters.

* An exact domain name that conforms to domain name specifications, for example: www.test.com.

> **tip**

> When the parameter `Rules.N.ActionType` is set to `Redirect`, if this parameter is not specified or no value is provided, it defaults to an empty string, and during actual forwarding, it remains consistent with the request domain.

**Rules.N.RedirectConfig.Path ** String`optional` `Example: /abc`

The path for the forwarding rule redirection. The requirements are as follows:

* Must start with a forward slash "/". The character '/' cannot appear consecutively.

* May include letters, numbers, and symbols: '\-', '_', '/', '.', '%', '?', '#', '&', and '='.

* Length limit is 1 to 128 characters.

> **tip**

> When the parameter `Rules.N.ActionType` is set to `Redirect`, if this parameter is not specified or no value is provided, it defaults to an empty string, and during actual forwarding, it remains consistent with the request path.

**Rules.N.RedirectConfig.Port ** String`optional` `Example: 443`

The port for the forwarding rule redirection, valid values range from 1 to 65535.

> **tip**

> When the parameter `Rules.N.ActionType` is set to `Redirect`, if this parameter is not specified or no value is provided, it defaults to an empty string, and during actual forwarding, it remains consistent with the request port.

**Rules.N.RedirectConfig.StatusCode ** String`optional` `Example: 301`

The status code for the forwarding rule redirection. Values:

* 301 (default): Indicates that the requested resource has been permanently moved to a new URL. The client should use the new URL for subsequent requests.

* 302: Indicates that the requested resource has been temporarily moved to a new URL but may change again. The client should use the new URL for subsequent requests.

* 307: Similar to **302**, but requires the client to preserve the request method when redirecting. For example, if the original request is a GET request, it will remain a GET request after redirection.

* 308: Similar to **301**, but requires the client to keep the request method unchanged when redirecting.

> **tip**

> When the parameter `Rules.N.ActionType` is set to `Redirect`, if this parameter is not specified or no value is provided, it defaults to 301.

**Rules.N.Description ** String`optional` `Example: This is a rule.`

The description of the forwarding rule. The default value is an empty string. The requirements are as follows:

* Must start with a letter, number, or Chinese character. May include letters, numbers, Chinese characters, and the following symbols: commas (,), periods (.), underscores (_), spaces ( ), equal signs (=), hyphens (\-), full\-width commas ( ， ), and full\-width periods ( 。 ).

* The length limit is 0 to 255 characters.

**Rules.N.Tags.N.Key ** String`optional` `Example: k1`

The tag key.

* The first N represents the serial number of the forwarding rule, ranging from 1 to 50. Separate multiple forwarding rules with ampersands (&).

* The second N represents the serial number of the tag key. Valid values: 1 to 50. Separate multiple tag keys with &.

* Must not start with `volc:` or `sys:` in any case form.

* Must be 1 to 128 characters. May include characters (any language), numbers, spaces ( ), underscores (_), periods (.), half\-width colons (:), slashes (/), equal signs (=), plus signs (+), hyphens (\-), and at signs (@).

* If a tag key contains leading or trailing spaces, the system will automatically delete them.

> Duplicate tag keys are not allowed for the same resource.

**Rules.N.Tags.N.Value ** String`optional` `Example: v1`

The tag value.

* The first N represents the serial number of the forwarding rule, ranging from 1 to 50. Separate multiple forwarding rules with ampersands (&).

* The second N represents the serial number of the tag value, ranging from 1 to 50. Separate multiple tag values with ampersands (&).

* Must be 0 to 256 characters. If left blank, this parameter defaults to an empty string.

* The following characters are allowed: characters from all languages, numbers, spaces ( ), underscores (_), periods (.), colons (:), forward slashes (/), equal signs (=), plus signs (+), hyphens (\-), and the at symbol (@).

* Case\-sensitive.

* If a tag value starts or ends with a space, the system will automatically delete it.

> If this parameter is specified, the tag key must be specified first.

## Response parameters

**RequestId ** String`Example: 2021081316135705146063000AD724****`

Request ID.

**RuleIds ** String[]`Example: ["rule-2fegss1cplxxc5oxruvvq****","rule-3ciynwkb46c6rrt4jszkd****"]`

Forwarding rule ID.

## Request examples

```json
GET /?Action=CreateRules&Version=2020-04-01&ListenerId=lsn-2fea4ayvu2g3k5oxruuz****&Rules.1.Domain=www.test.com&Rules.1.Url=/poo&Rules.1.ActionType=Forward&Rules.1.ServerGroupId=rsp-bp1o94dp5i6ea****&Rules.1.RedirectConfig.Protocol=HTTPS&Rules.1.RedirectConfig.Host=www.test.com&Rules.1.RedirectConfig.Path=/abc&Rules.1.RedirectConfig.Port=443&Rules.1.RedirectConfig.StatusCode=301&Rules.1.Description=This is a rule.&Rules.1.Tags.1.Key=k1&Rules.1.Tags.1.Value=v1
Host: clb.cn-beijing.byteplusapi.com.cn
X-Date: 20251121T094038Z
Authorization: HMAC-SHA256 Credential=Adfks******wekfwe/20251121/cn-beijing/clb/request, SignedHeaders=host;x-date, Signature=47a7d934ff7b37c03938******cd7b8278a40a1057690c401e92246a0e41085f
```

## Response examples

```json
{
    "ResponseMetadata": {
        "RequestId": "20230604110420****100232280022D31",
        "Action": "CreateRules",
        "Version": "2020-04-01",
        "Service": "clb",
        "Region": "cn-beijing"
    },
    "Result": {
        "RequestId": "2021081316135705146063000AD724****",
        "RuleIds": [
            "rule-2fegss1cplxxc5oxruvvq****",
            "rule-3ciynwkb46c6rrt4jszkd****"
        ]
    }
}
```

## Error codes

This section displays only the error codes of the current API. For more error codes, see [Common error codes](https://docs.byteplus.com/en/docs/clb/Public-error-codes).

|Status code |Error codes |Error message |Notes |
|---|---|---|---|
|400 |InvalidDefaultRule.UnSupportAction |The specified Default Rule does not support this action. |The specified default forwarding rule does not support the current action. |
|400 |InvalidDescription.Malformed |The specified Description is malformed. |The format specified for Description is invalid. |
|400 |InvalidIncorrectOrder.Malformed |The specified index order is malformed. |The specified index order parameter format is invalid. |
|400 |InvalidListener.NotSupportRule |The specified Listener not support rule. |The specified listener does not support forwarding rules. |
|400 |InvalidListenerServerGroup.UnSupportAction |The specified Listener does not support this action. |The specified listener is not bound to a default backend server group, so the current operation is not supported. |
|400 |InvalidLoadBalancer.InvalidStatus |The specified LoadBalancer is not in the correct status for the request. |The specified load balancer cannot respond to this request due to its status. |
|400 |InvalidProtocol.ListenerMismatch |The specified Protocol and Listener are not matched. |The specified protocol does not match the listener. |
|400 |InvalidQuotaCode.Malformed |The specified QuotaCode is malformed. |The specified QuotaCode parameter format is invalid. |
|400 |InvalidRuleRedirectConfig.ActionTypeMismatch |The specified RedirectConfig not match with ActionType. |The specified redirection configuration is inconsistent with the forwarding type. |
|400 |InvalidRules.ActionType.Malformed |The specified Rules.ActionType is malformed. |The specified Rules.ActionType parameter format is invalid. |
|400 |InvalidRules.Domain.Malformed |The specified Rules.Domain is malformed. |The specified Rules.Domain format is invalid. |
|400 |InvalidRules.RedirectConfig.Host.Malformed |The specified Rules.RedirectConfig.Host is malformed. |The specified Rules.RedirectConfig.Host parameter format is invalid. |
|400 |InvalidRules.RedirectConfig.Path.Malformed |The specified Rules.RedirectConfig.Path is malformed. |The specified Rules.RedirectConfig.Path parameter format is invalid. |
|400 |InvalidRules.RedirectConfig.Port.Malformed |The specified Rules.RedirectConfig.Port is malformed. |The specified Rules.RedirectConfig.Port parameter format is invalid. |
|400 |InvalidRules.RedirectConfig.Protocol.Malformed |The specified Rules.RedirectConfig.Protocol is malformed. |The specified Rules.RedirectConfig.Protocol parameter format is invalid. |
|400 |InvalidRules.RedirectConfig.StatusCode.Malformed |The specified Rules.RedirectConfig.StatusCode is malformed. |The specified Rules.RedirectConfig.StatusCode parameter format is invalid. |
|400 |InvalidRules.URL.Malformed |The specified Rules.URL is malformed. |The specified Rules.URL parameter format is invalid. |
|400 |InvalidServerGroup.ActionTypeMismatch |The specified ServerGroup not match with ActionType. |The specified backend server group is inconsistent with the forwarding type. |
|400 |InvalidServerGroup.UnSupportAction |The specified ServerGroup does not support this action. |The specified Server Group does not support the current action. |
|400 |InvalidTagKey.Malformed |The specified TagKey is malformed. |The specified TagKey parameter format is invalid. |
|400 |InvalidTagValue.Malformed |The specified TagValue is malformed. |The specified TagValue parameter format is invalid. |
|400 |LimitExceeded.ServiceManagedTag |You've reached the limit on the number of service managed tags that you can create. |You have reached the limit for the number of managed resource tag key\-value pairs that can be created in a single request. |
|400 |LimitExceeded.TagOperation |You've reached the limit on the number of tags that you can operate at a time. |You have reached the maximum number of tag entries that can be operated on in a single request. |
|400 |MissingParameter |The request is missing a required parameter. Ensure that you have supplied all the required parameters for the request; for example, the 'Rules.RedirectConfig.Host, Rules.RedirectConfig.Path, Rules.RedirectConfig.Port'. |This request is missing a required parameter. Please ensure the request includes all required parameters, such as Rules.RedirectConfig.Host, Rules.RedirectConfig.Path, Rules.RedirectConfig.Port. |
|400 |MissingParameter |The request is missing a required parameter. Ensure that you have supplied all the required parameters for the request; for example, the 'Domain, URL'. |This request is missing a required parameter. Please ensure that all required parameters, such as Domain and URL, are provided in the request. |
|400 |MissingParameter |The request is missing a required parameter. Ensure that you have supplied all the required parameters for the request; for example, the 'ListenerId'. |This request is missing a required parameter. Please ensure the request includes all required parameters, such as ListenerId. |
|400 |MissingParameter |The request is missing a required parameter. Ensure that you have supplied all the required parameters for the request; for example, the ''. |This request does not contain required parameters. Ensure the request includes all required parameters, such as . |
|400 |QuotaExceed.RuleNumberEachListener |You've reached the limit on the number of Rule that you can associate. |The quota limit for the number of forwarding rules that can be associated with the listener has been reached. |
|400 |UnsupportedOperation.AccountArrears |The request on the specified instance is denied due to the account in arrears status. |The action request on this instance is denied because the account is in arrears. |
|403 |Forbidden |You are not authorized to perform operations on the service managed tag. |No permission to tag the specified resource with managed tags. |
|403 |Forbidden |You are not authorized to perform operations on the specified service. |You do not have permission to perform operations on the specified service. |
|403 |Forbidden |You are not authorized to perform operations on the system tag. |No permission to tag the specified resource with a system tag. |
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
