---
title: "UpdateSharedConfig"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/UpdateSharedConfig_en"
---

Modify a universal catalog.

<span id="usage-limits"></span>
## Usage Limits

Rate Limit: You can submit up to 20 API requests per second.

<span id="usage"></span>
## Usage


* Request Method: POST

* Request URL: https://cdn.byteplusapi.com/?Action=UpdateSharedConfig&Version=2021\-03\-01


<span id="request-parameters"></span>
## Request Parameters

<span id="query-parameters"></span>
### Query Parameters


|Parameter |Data Type |Required |Description |
|---|---|---|---|
|Action |String |Yes |The action of this API operation. The action is: `UpdateSharedConfig`. |
|Version |String |Yes |The version of this API operation. Current version: `2021-03-01`. |


<span id="request-body"></span>
### Request Body


|Parameter |Data Type |Required |Description |Value |
|---|---|---|---|---|
|ConfigName |String |Yes |Indicates the name of a universal catalog.<br><br>You can call [ListSharedConfig](https://docs.byteplus.com/en/docs/byteplus-cdn/ListSharedConfig_en) to get the names of existing universal catalogs. |`my_list` |
|AllowIpAccessRule |Object |No |Indicates the configuration of an IP allowlist, corresponding to `ConfigType` as `allow_ip_access_rule`. | |
|Option |String |No |Indicates the type of modification operation. This parameter has the following values:<br><br><br>1. `overlap`: Indicates full coverage of existing rules.<br><br>2. `add`: Indicates adding rules.<br><br>3. `delete`: Indicates deleting specified rules.<br><br><br>The default value of this parameter is `overlap`. |`add` |
|Rules |String[] |No |Indicates a list of rules. Each rule is an IP address or CIDR segment. IP addresses and segments can be in IPv4 and IPv6 formats.<br><br>The list limits are as follows:<br><br><br>* If `Option` is `overlap`, the number of rules in the list cannot exceed 30,000.<br><br>* If `Option` is `add`, the total number of rules in the list and the existing rules in `ConfigName` cannot exceed 30,000. You can call [DescribeSharedConfig](https://docs.byteplus.com/en/docs/byteplus-cdn/DescribeSharedConfig_en) to calculate the number of existing rules in this universal catalog.<br><br><br>When BytePlus CDN updates `ConfigName`, duplicate rules in the list will be removed. Duplicate rules do not count towards the limit. |`["xx.xxx.xxx.xx","xxx.xxx.xxx.xxx"]` |
|IpSource |Object |No |Indicates the configuration for how CDN obtains the client IP address. | |
|SourceList |String[] |No |Indicates one or more IP sources used when `Type` is `custom`.<br><br>Valid values:<br><br><br>* `x-real-ip`: Indicates the IP address obtained from the `X-Real-IP` request header.<br><br>* `x-forwarded-for`: Indicates the IP address obtained from the `X-Forwarded-For` request header.<br><br>* `client-ip`: Indicates the actual connection IP. The actual connection IP is the IP address of the peer that directly establishes a network connection with the CDN node.<br><br><br>For an IP blocklist, CDN rejects the request if any IP address obtained from the selected sources matches a blocklist rule. For an IP allowlist, CDN allows the request only if all IP addresses obtained from the selected sources match allowlist rules. |`["x-real-ip", "x-forwarded-for"]` |
|Type |String |No |Indicates the method used to determine the client IP address.<br><br>Valid values:<br><br><br>* `default`: Uses the actual connection IP.<br><br>* `custom`: Uses one or more sources specified in `SourceList`. If CDN cannot obtain an IP address from a selected request header, it uses the actual connection IP for that source.<br><br><br>The default value is `default`. |`custom` |
|DenyIpAccessRule |Object |No |Indicates the configuration of an IP blocklist, corresponding to `ConfigType` as `deny_ip_access_rule`. | |
|Option |String |No |This parameter's description is the same as `Option` under the IP allowlist configuration. |`overlap` |
|Rules |String[] |No |This parameter's description is the same as `Rules` under the IP allowlist configuration. |`["xx.xxx.xxx.xx","xxx.xxx.xxx.xxx/24"]` |
|IpSource |Object |No |This parameter's description is the same as `IpSource` under the IP allowlist configuration. | |
|SourceList |String[] |No |This parameter's description is the same as `SourceList` under the IP allowlist configuration. |`["x-real-ip", "x-forwarded-for"]` |
|Type |String |No |This parameter's description is the same as `Type` under the IP allowlist configuration. |`custom` |
|AllowRefererAccessRule |Object |No |Indicates the configuration of a Referer allowlist, corresponding to `ConfigType` as `allow_referer_access_rule`. | |
|AllowEmpty |Boolean |No |Indicates whether requests with an empty Referer header ("") or without a Referer header are allowed. This parameter has the following values:<br><br><br>* `true`: Indicates allowed.<br><br>* `false`: Indicates not allowed. If the Referer header of the request is empty ("") or does not contain a Referer header, BytePlus CDN rejects the request.<br><br><br>The default value of this parameter is `false`. |`true` |
|CommonType |Object |No |Indicates the content of the Referer allowlist. | |
|IgnoreCase |Boolean |No |Indicates whether the rules in `Rules` are case\-sensitive. This parameter has the following values:<br><br><br>* `true`: Indicates case\-insensitive.<br><br>* `false`: Indicates case\-sensitive.<br><br><br>The default value of this parameter is `true`. |`true` |
|Option |String |No |Indicates the type of modification operation. This parameter has the following values:<br><br><br>1. `overlap`: Indicates full coverage of existing rules.<br><br>2. `add`: Indicates adding rules.<br><br>3. `delete`: Indicates deleting specified rules.<br><br><br>The default value of this parameter is `overlap`. |`overlap` |
|Rules |String[] |No |Indicates a list of rules. Each rule is an IP address or domain name. IP addresses can be in IPv4 and IPv6 formats, and domain names can be wildcard domain names.<br><br>The list limits are as follows:<br><br><br>* If `Option` is `overlap`, the number of rules in the list cannot exceed 4,000.<br><br>* If `Option` is `add`, the total number of rules in the list and the existing rules in `ConfigName` cannot exceed 4,000. You can call [DescribeSharedConfig](https://docs.byteplus.com/en/docs/byteplus-cdn/DescribeSharedConfig_en) to calculate the number of existing rules in this universal catalog.<br><br><br>When BytePlus CDN updates `ConfigName`, duplicate rules in the list will be removed. Duplicate rules do not count towards the limit. |`["xxx.xx.xx.xxx","*.example.com"]` |
|DenyRefererAccessRule |Object |No |Indicates the configuration of a Referer blocklist, corresponding to `ConfigType` as `deny_referer_access_rule`. | |
|AllowEmpty |Boolean |No |This parameter's description is the same as `AllowEmpty` under the IP allowlist configuration. |`true` |
|CommonType |Object |No |Indicates the content of the Referer blocklist. | |
|IgnoreCase |Boolean |No |This parameter's description is the same as `IgnoreCase` under the IP allowlist configuration. |`true` |
|Option |String |No |This parameter's description is the same as `Option` under the IP allowlist configuration. |`overlap` |
|Rules |String[] |No |This parameter's description is the same as `Rules` under the IP allowlist configuration. |`["xxx.xx.xx.xxx","*.example.com"]` |
|CommonMatchList |Object |No |Indicates the configuration of a general list, corresponding to `ConfigType` as `common_match_list`. | |
|CommonType |Object |No |Indicates the content of the general list. | |
|IgnoreCase |Boolean |No |Indicates whether the rules in `Rules` are case\-sensitive. This parameter has the following values:<br><br><br>* `true`: Indicates case\-insensitive.<br><br>* `false`: Indicates case\-sensitive.<br><br><br>The default value of this parameter is `true`. |`false` |
|Option |String |No |Indicates the update operation. CDN uses `Rules` to update the existing rules in the General List identified by `ConfigName`.<br><br>Valid values:<br><br><br>1. `overlap`: Replaces all existing rules with `Rules`. The deduplicated `Rules` must comply with the rule formats and limits for the current `CommonListType`.<br><br>2. `add`: Adds `Rules` to the existing rules. After the rules are added and deduplicated, the total number of rules and their combined length must comply with the limits for the current `CommonListType`. You can call [DescribeSharedConfig](https://docs.byteplus.com/en/docs/byteplus-cdn/DescribeSharedConfig_en) to retrieve the existing rules in the General List.<br><br>3. `delete`: Deletes `Rules` from the existing rules. `Rules` must comply with the rule format for the current `CommonListType`.<br><br><br>The default value is `overlap`. |`overlap` |
|Rules |String[] |No |Indicates the rules to delete, add, or replace. Each rule is a string.<br><br>After the update, the General List must comply with the rule formats and limits for the `CommonListType` of the General List identified by `ConfigName`.<br><br><br>* When `CommonListType` is `exact_match`, each rule is a string. You can use the wildcard character `*` to represent any characters only at the beginning or end of a string. The General List can contain up to `4,000` rules with a combined length of up to `200,000` characters.<br><br>* When `CommonListType` is `regex_match`, each rule is a regular expression. The General List can contain up to `30,000` rules with a combined length of up to `200,000` characters.<br><br>* When `CommonListType` is `ip_match`, each rule is an IP address or CIDR block. The General List can contain up to `30,000` rules.<br><br><br>CDN automatically removes duplicate rules when updating the General List identified by `ConfigName`. Duplicate rules do not count toward the rule limit. |`["param1","param2"]` |


<span id="response-parameters"></span>
## Response Parameters

<span id="samples"></span>
## Samples

<span id="sample-request"></span>
### Sample request

```json
POST https://cdn.byteplusapi.com/?Action=UpdateSharedConfig&Version=2021-03-01
{
    "ConfigName": "My_List",
    "DenyRefererAccessRule": {
        "CommonType": {
            "Option": "add",
            "Rule": [
                "xx.xxx.xxx.xx",
                "xxx.xxx.xxx.xx"
            ]
        }
    }
}
```
