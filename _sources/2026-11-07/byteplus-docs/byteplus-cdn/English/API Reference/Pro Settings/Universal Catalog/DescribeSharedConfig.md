---
title: "DescribeSharedConfig"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/DescribeSharedConfig_en"
---

Get the settings of a universal catalog.

<span id="usage-limits"></span>
## Usage Limits

Rate Limit: You can submit up to 20 API requests per second.

<span id="usage"></span>
## Usage


* Request Method: POST

* Request URL: https://cdn.byteplusapi.com/?Action=DescribeSharedConfig&Version=2021\-03\-01


<span id="request-parameters"></span>
## Request Parameters

<span id="query-parameters"></span>
### Query Parameters


|Parameter |Data Type |Required |Description |
|---|---|---|---|
|Action |String |Yes |The action of this API operation. The action is: `DescribeSharedConfig`. |
|Version |String |Yes |The version of this API operation. Current version: `2021-03-01`. |


<span id="request-body"></span>
### Request Body


|Parameter |Data Type |Required |Description |Value |
|---|---|---|---|---|
|ConfigName |String |No |Indicates the name of a universal catalog.<br><br>You can call [ListSharedConfig](https://docs.byteplus.com/en/docs/byteplus-cdn/ListSharedConfig_en) to get the names of existing universal catalogs. |`my_list` |


<span id="response-parameters"></span>
## Response Parameters


|Parameter |Data Type |Description |Value |
|---|---|---|---|
|AllowIpAccessRule |Object |Indicates the configuration of an IP allowlist, corresponding to `ConfigType` as `allow_ip_access_rule`. | |
|Rules |String[] |Indicates the rules in the IP allowlist. |`["xx.xx.xx.xx","xxx.xxx.xx.x/24"]` |
|IpSource |Object |Indicates the configuration for how CDN obtains the client IP address. | |
|SourceList |String[] |Indicates one or more IP sources used when `Type` is `custom`.<br><br>Valid values:<br><br><br>* `x-real-ip`: Indicates the IP address obtained from the `X-Real-IP` request header.<br><br>* `x-forwarded-for`: Indicates the IP address obtained from the `X-Forwarded-For` request header.<br><br>* `client-ip`: Indicates the actual connection IP. The actual connection IP is the IP address of the peer that directly establishes a network connection with the CDN node.<br><br><br>For an IP blocklist, CDN rejects the request if any IP address obtained from the selected sources matches a blocklist rule. For an IP allowlist, CDN allows the request only if all IP addresses obtained from the selected sources match allowlist rules. |`["x-real-ip", "x-forwarded-for"]` |
|Type |String |Indicates the method used to determine the client IP address.<br><br>Valid values:<br><br><br>* `default`: Uses the actual connection IP.<br><br>* `custom`: Uses one or more sources specified in `SourceList`. If CDN cannot obtain an IP address from a selected request header, it uses the actual connection IP for that source. |`custom` |
|AllowRefererAccessRule |Object |Indicates the configuration of a Referer allowlist, corresponding to `ConfigType` as `allow_referer_access_rule`. | |
|AllowEmpty |Boolean |Indicates whether requests with an empty Referer header ("") or without a Referer header are allowed. This parameter has the following values:<br><br><br>* `true`: Indicates allowed.<br><br>* `false`: Indicates not allowed. If the Referer header of the request is empty ("") or does not contain a Referer header, BytePlus CDN rejects the request. |`true` |
|CommonType |Object |Indicates the content of the Referer allowlist. | |
|IgnoreCase |Boolean |Indicates whether the rules in `Rules` are case\-sensitive. This parameter has the following values:<br><br><br>* `true`: Indicates case\-insensitive.<br><br>* `false`: Indicates case\-sensitive. |`true` |
|Rules |String[] |Indicates the rules in the Referer allowlist. |`["x.x.x.x","*.example.com","www.example.com"]` |
|ConfigName |String |Indicates the name of this universal catalog. |`my_list` |
|ConfigType |String |Indicates the type of this universal catalog. This parameter has the following values:<br><br><br>* `deny_ip_access_rule`: Indicates IP blocklist.<br><br>* `allow_ip_access_rule`: Indicates IP allowlist.<br><br>* `deny_referer_access_rule`: Indicates Referer blocklist.<br><br>* `allow_referer_access_rule`: Indicates Referer allowlist.<br><br>* `common_match_list`: Indicates general list.<br><br>* `4xx_error_page`: Indicates custom error page. |`allow_ip_access_rule` |
|DenyIpAccessRule |Object |Indicates the configuration of an IP blocklist, corresponding to `ConfigType` as `deny_ip_access_rule`. | |
|Rules |String[] |Indicates the rules in the IP blocklist. |`["xx.xx.xx.xx","xxx.xxx.x.x"]` |
|IpSource |Object |This parameter's description is the same as `IpSource` under the IP allowlist. | |
|SourceList |String[] |This parameter's description is the same as `SourceList` under the IP allowlist. |`["x-real-ip", "x-forwarded-for"]` |
|Type |String |This parameter's description is the same as `Type` under the IP allowlist. |`custom` |
|DenyRefererAccessRule |Object |Indicates the configuration of a Referer blocklist, corresponding to `ConfigType` as `deny_referer_access_rule`. | |
|AllowEmpty |Boolean |This parameter's description is the same as `AllowEmpty` under the Referer allowlist. |`true` |
|CommonType |Object |Indicates the content of the Referer blocklist. | |
|IgnoreCase |Boolean |This parameter's description is the same as `IgnoreCase` under the Referer allowlist. |`true` |
|Rules |String[] |Indicates the entries in the Referer blocklist. |`["x.x.x.x","*.example.com","www.example.com"]` |
|Project |String |Indicates the project name to which this universal catalog belongs. |`default` |
|CommonMatchList |Object |Indicates the configuration of a general list, corresponding to `ConfigType` as `common_match_list`. | |
|CommonType |Object |Indicates the content of the general list. | |
|IgnoreCase |Boolean |Indicates whether the rules in `Rules` are case\-sensitive. This parameter has the following values:<br><br><br>* `true`: Indicates case\-insensitive.<br><br>* `false`: Indicates case\-sensitive. |`true` |
|Rules |String[] |Indicates the rules in the general list. |`["abc","param"]` |
|CommonListType |String |Indicates how values are matched against the rules in the General List. This parameter cannot be changed after the General List is created.<br><br>Valid values:<br><br><br>* `exact_match`: Matches a value against string rules in `Rules`. A string rule can include the wildcard character \* only at the beginning or end of the string.<br><br>* `regex_match`: Matches a value against regular expression rules in `Rules`.<br><br>* `ip_match`: Matches an IP address against IP address or CIDR block rules in `Rules`. |`ip_match` |
|ErrorPageRule |Object |Indicates the configuration of a custom error page. | |
|RuleContent |String |Indicates the HTML code of this custom error page. |`<html><head><title>Test</title></head><body><h1>Header</h1>Hello World</body></html>` |


<span id="samples"></span>
## Samples

<span id="sample-request"></span>
### Sample request

```json
POST https://cdn.byteplusapi.com/?Action=DescribeSharedConfig&Version=2021-03-01
{
    "ConfigName": "My_List"
}
```


<span id="sample-response"></span>
### Sample response

```json
{
    "ResponseMetadata": {
        "RequestId": "20241209082302440129758BDA68D5D9AF",
        "Action": "DescribeSharedConfig",
        "Version": "2021-03-01",
        "Service": "CDN",
        "Region": "ap-singapore-1"
    },
    "Result": {
        "AllowRefererAccessRule": {
            "AllowEmpty": false,
            "CommonType": {
                "IgnoreCase": true,
                "Rules": [
                    "xxx.xx.xxx.xxx",
                    "www.example.com",
                    "abc.example.com"
                ]
            }
        },
        "ConfigName": "My_List",
        "ConfigType": "allow_referer_access_rule",
        "Project": "default"
    }
}
```
