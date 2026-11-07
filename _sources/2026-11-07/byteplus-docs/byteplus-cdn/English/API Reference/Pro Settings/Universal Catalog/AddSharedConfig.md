---
title: "AddSharedConfig"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/AddSharedConfig_en"
---

Create a universal catalog.

<span id="usage-limits"></span>
## Usage Limits

Rate Limit: You can submit up to 20 API requests per second.

<span id="usage"></span>
## Usage


* Request Method: POST

* Request URL: https://cdn.byteplusapi.com/?Action=AddSharedConfig&Version=2021\-03\-01


<span id="request-parameters"></span>
## Request Parameters

<span id="query-parameters"></span>
### Query Parameters


|Parameter |Data Type |Required |Description |
|---|---|---|---|
|Action |String |Yes |The action of this API operation. The action is: `AddSharedConfig`. |
|Version |String |Yes |The version of this API operation. Current version: `2021-03-01`. |


<span id="request-body"></span>
### Request Body


|Parameter |Data Type |Required |Description |Value |
|---|---|---|---|---|
|ConfigName |String |Yes |Indicates the name of the universal catalog. The name has the following requirements:<br><br><br>* The name can contain Chinese characters, letters, numbers, and underscores (_), with a length of 3\-45 characters. One Chinese character counts as 3 characters.<br><br>* The name cannot be the same as an existing universal catalog name under the main account. |`my_list` |
|ConfigType |String |Yes |Indicates the type of this universal catalog. This parameter has the following values:<br><br><br>* `deny_ip_access_rule`: Indicates IP blocklist.<br><br>* `allow_ip_access_rule`: Indicates IP allowlist.<br><br>* `deny_referer_access_rule`: Indicates Referer blocklist.<br><br>* `allow_referer_access_rule`: Indicates Referer allowlist.<br><br>* `common_match_list`: Indicates general list. |`allow_ip_access_rule` |
|AllowIpAccessRule |Object |No |Indicates the configuration of an IP allowlist, corresponding to `ConfigType` as `allow_ip_access_rule`. | |
|Rules |String[] |No |Indicates a list of rules, each rule in the list is an IP address or CIDR segment. IP addresses and segments can be in IPv4 and IPv6 formats.<br><br>The list limits are as follows:<br><br><br>* The list can contain up to 30,000 rules.<br><br><br>When CDN creates this universal catalog, duplicate rules in the list will be removed. Duplicate rules do not count towards the limit. |`["x.x.x.x","xxx.xx.xx.xx/24"]` |
|IpSource |Object |No |Indicates the configuration for how CDN obtains the client IP address. | |
|SourceList |String[] |No |Indicates one or more IP sources used when `Type` is `custom`.<br><br>Valid values:<br><br><br>* `x-real-ip`: Indicates the IP address obtained from the `X-Real-IP` request header.<br><br>* `x-forwarded-for`: Indicates the IP address obtained from the `X-Forwarded-For` request header.<br><br>* `client-ip`: Indicates the actual connection IP. The actual connection IP is the IP address of the peer that directly establishes a network connection with the CDN node.<br><br><br>For an IP blocklist, CDN rejects the request if any IP address obtained from the selected sources matches a blocklist rule. For an IP allowlist, CDN allows the request only if all IP addresses obtained from the selected sources match allowlist rules. |`["x-real-ip", "x-forwarded-for"]` |
|Type |String |No |Indicates the method used to determine the client IP address.<br><br>Valid values:<br><br><br>* `default`: Uses the actual connection IP.<br><br>* `custom`: Uses one or more sources specified in `SourceList`. If CDN cannot obtain an IP address from a selected request header, it uses the actual connection IP for that source.<br><br><br>The default value is `default`. |`custom` |
|AllowRefererAccessRule |Object |No |Indicates the configuration of a Referer allowlist, corresponding to `ConfigType` as `allow_referer_access_rule`. | |
|AllowEmpty |Boolean |No |Indicates whether requests with an empty Referer header ("") or without a Referer header are allowed. This parameter has the following values:<br><br><br>* `true`: Indicates allowed.<br><br>* `false`: Indicates not allowed. If the Referer header of the request is empty ("") or does not contain a Referer header, BytePlus CDN rejects the request.<br><br><br>The default value of this parameter is `false`. |`false` |
|CommonType |Object |No |Indicates the content of the Referer allowlist. | |
|IgnoreCase |Boolean |No |Indicates whether the rules in `Rules` are case\-sensitive. This parameter has the following values:<br><br><br>* `true`: Indicates case\-insensitive.<br><br>* `false`: Indicates case\-sensitive.<br><br><br>The default value of this parameter is `true`. |`true` |
|Rules |String[] |No |Indicates a list of rules, each rule in the list is a domain name or IP address. Domain names can be wildcard domain names, and IP addresses can be in IPv4 and IPv6 formats.<br><br>The list limits are as follows:<br><br><br>* The list can contain up to 4,000 rules.<br><br><br>When BytePlus CDN creates this universal catalog, duplicate rules in the list will be removed. Duplicate rules do not count towards the limit. |`["x.x.x.xx","*.example.com"]` |
|DenyIpAccessRule |Object |No |Indicates the configuration of an IP blocklist, corresponding to `ConfigType` as `deny_ip_access_rule`. | |
|Rules |String[] |No |This parameter's description is the same as `Rules` under the IP allowlist. |`["x.x.x.x","xx.xx.xx.xx"]` |
|IpSource |Object |No |This parameter's description is the same as `IpSource` under the IP allowlist. | |
|SourceList |String[] |No |This parameter's description is the same as `SourceList` under the IP allowlist. |`["x-real-ip", "x-forwarded-for"]` |
|Type |String |No |This parameter's description is the same as `Type` under the IP allowlist. |`custom` |
|DenyRefererAccessRule |Object |No |Indicates the configuration of a Referer blocklist, corresponding to `ConfigType` as `deny_referer_access_rule`. | |
|AllowEmpty |Boolean |No |This parameter's description is the same as `AllowEmpty` under the IP allowlist. |`true` |
|CommonType |Object |No |Indicates the content of the Referer blocklist. | |
|IgnoreCase |Boolean |No |This parameter's description is the same as `IgnoreCase` under the Referer allowlist. |`true` |
|Rules |String[] |No |This parameter's description is the same as `Rules` under the Referer allowlist. |`["xx.xx.x.xxx","*.example.com"]` |
|Project |String |No |Indicates the project name to which this universal catalog belongs, the default value is `default`.<br><br>You can visit [Project Management](https://console.byteplus.com/iam/resourcemanage/project) to view the created projects and the resources contained in each project. |`default` |
|CommonMatchList |Object |No |Indicates the configuration of a general list, corresponding to `ConfigType` as `common_match_list`. | |
|CommonType |Object |No |Indicates the content of the general list. | |
|IgnoreCase |Boolean |No |Indicates whether the rules in `Rules` are case\-sensitive. This parameter has the following values:<br><br><br>* `true`: Indicates case\-insensitive.<br><br>* `false`: Indicates case\-sensitive.<br><br><br>The default value of this parameter is `true`. |`true` |
|Rules |String[] |No |Indicates the rules in the General List. Rule formats and limits depend on `CommonListType`.<br><br><br>* When `CommonListType` is `exact_match`, each array element must be a string. You can use the wildcard character `*` to represent any characters only at the beginning or end of a string. A maximum of 4,000 rules is supported, with a combined length of up to 200,000 characters.<br><br>* When `CommonListType` is `regex_match`, each array element must be a regular expression. A maximum of 30,000 rules is supported, with a combined length of up to 200,000 characters.<br><br>* When `CommonListType` is `ip_match`, each array element must be an IP address or CIDR block. A maximum of 30,000 rules is supported.<br><br><br>Duplicate rules are automatically removed and do not count toward the rule limit. |`["param1","param2"]` |
|CommonListType |String |No |Indicates how values are matched against the rules in the General List. This parameter cannot be changed after the General List is created.<br><br>Valid values:<br><br><br>* `exact_match`: Matches a value against string rules in `Rules`. A string rule can include the wildcard character \* only at the beginning or end of the string.<br><br>* `regex_match`: Matches a value against regular expression rules in `Rules`.<br><br>* `ip_match`: Matches an IP address against IP address or CIDR block rules in `Rules`.<br><br><br>The default value is `exact_match`. |`ip_match` |


<span id="response-parameters"></span>
## Response Parameters

<span id="samples"></span>
## Samples

<span id="sample-request"></span>
### Sample request

```json
POST https://cdn.byteplusapi.com/?Action=AddSharedConfig&Version=2021-03-01
{
    "ConfigName": "My_List",
    "ConfigType": "allow_referer_access_rule",
    "AllowRefererAccessRule": {
        "CommonType": {
            "Rules": [
                "xxx.xx.xxx.xxx",
                "www.example.com",
                "abc.example.com"
            ]
        }
    }
}
```
