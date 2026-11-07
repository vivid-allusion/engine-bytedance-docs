---
title: "DescribeSharedConfig"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/DescribeSharedConfig_cn"
---

获取一个全局配置的设置。

<span id="使用限制"></span>
## 使用限制

节流限制：您每秒最多可以提交 20 个 API 请求。

<span id="请求说明"></span>
## 请求说明


* Request Method：POST

* Request URL：https://cdn.byteplusapi.com/?Action=DescribeSharedConfig&Version=2021\-03\-01


<span id="请求参数"></span>
## 请求参数

<span id="query"></span>
### Query


|参数 |类型 |是否必选 |描述 |
|---|---|---|---|
|Action |String |是 |接口名称。当前 API 的名称为 `DescribeSharedConfig`。 |
|Version |String |是 |接口版本。当前 API 的版本为 `2021-03-01`。 |


<span id="body"></span>
### Body


|参数 |类型 |是否必选 |描述 |示例值 |
|---|---|---|---|---|
|ConfigName |String |否 |表示一个全局配置的名称。<br><br>您可以调用 [ListSharedConfig](https://docs.byteplus.com/en/docs/byteplus-cdn/ListSharedConfig_cn) 获取已有的全局配置名称。 |`my_list` |


<span id="返回参数"></span>
## 返回参数


|参数 |类型 |描述 |示例值 |
|---|---|---|---|
|AllowIpAccessRule |Object |表示 IP 白名单的配置，对应 `ConfigType` 是 `allow_ip_access_rule`。 | |
|Rules |String[] |表示该 IP 白名单中的规则。 |`["xx.xx.xx.xx","xxx.xxx.x.x"]` |
|IpSource |Object |表示客户端 IP 地址获取方式的配置。 | |
|SourceList |String[] |表示 CDN 判断客户端 IP 地址的方式。<br><br>取值：<br><br><br>* `default`：使用真实建连 IP。<br><br>* `custom`：使用 `SourceList` 中指定的一个或多个来源。无法从已选请求头获取 IP 地址时，CDN 对该来源使用真实建连 IP。 |`["x-real-ip", "x-forwarded-for"]` |
|Type |String |表示当 `Type` 为 `custom` 时，用于判断客户端 IP 地址的一个或多个来源。<br><br>取值：<br><br><br>* `x-real-ip`：表示从 `X-Real-IP` 请求头获取的 IP 地址。<br><br>* `x-forwarded-for`：表示从 `X-Forwarded-For` 请求头获取的 IP 地址。<br><br>* `client-ip`：表示真实建连 IP，即与 CDN 节点直接建立网络连接的对端 IP 地址。<br><br><br>对于 IP 黑名单，只要任一指定来源中获取的 IP 地址匹配黑名单规则，CDN 就拒绝请求。对于 IP 白名单，只有所有指定来源中获取的 IP 地址均匹配白名单规则，CDN 才允许请求。 |`custom` |
|AllowRefererAccessRule |Object |表示 Referer 白名单的配置，对应 `ConfigType` 是 `allow_referer_access_rule`。 | |
|AllowEmpty |Boolean |表示是否允许 Referer 头部为空（""）或者不包含 Referer 头部的请求。该参数有以下取值：<br><br><br>* `true`：表示允许。<br><br>* `false`：表示不允许。如果请求的 Referer 头部为空（""）或者不包含 Referer 头部，CDN 拒绝请求。 |`true` |
|CommonType |Object |表示该 Referer 白名单的内容。 | |
|IgnoreCase |Boolean |表示 `Rules` 中的规则是否区分大小写。该参数有以下取值：<br><br><br>* `true`：表示不区分大小写。<br><br>* `false`：表示区分大小写。 |`true` |
|Rules |String[] |表示该 Referer 白名单中的规则。 |`["x.x.x.x","*.example.com","www.example.com"]` |
|ConfigName |String |表示该全局配置的名称。 |`my_list` |
|ConfigType |String |表示该全局配置的类型。该参数有以下取值：<br><br><br>* `deny_ip_access_rule`：表示 IP 黑名单。<br><br>* `allow_ip_access_rule`：表示 IP 白名单。<br><br>* `deny_referer_access_rule`：表示 Referer 黑名单。<br><br>* `allow_referer_access_rule`：表示 Referer 白名单。<br><br>* `common_match_list`：表示通用列表。<br><br>* `4xx_error_page`: 表示自定义错误页面。 |`allow_ip_access_rule` |
|DenyIpAccessRule |Object |表示 IP 黑名单的配置，对应 `ConfigType` 是 `deny_ip_access_rule`。 | |
|Rules |String[] |表示该 IP 黑名单中的规则。 |`["xx.xx.xx.xx","xxx.xxx.x.x"]` |
|IpSource |Object |该参数的说明与 IP 白名单下 `IpSource` 的说明相同。 | |
|SourceList |String[] |该参数的说明与 IP 白名单下 `SourceList` 的说明相同。 |`["x-real-ip", "x-forwarded-for"]` |
|Type |String |该参数的说明与 IP 白名单下 `Type` 的说明相同。 |`custom` |
|DenyRefererAccessRule |Object |表示 Referer 黑名单的配置，对应 `ConfigType` 是 `deny_referer_access_rule`。 | |
|AllowEmpty |Boolean |该参数的说明与 Referer 白名单下 `AllowEmpty` 的说明相同。 |`true` |
|CommonType |Object |表示该 Referer 黑名单的内容。 | |
|IgnoreCase |Boolean |该参数的说明与 Referer 白名单下 `IgnoreCase` 的说明相同。 |`true` |
|Rules |String[] |表示该 Referer 黑名单中的规则。 |`["x.x.x.x","*.example.com","www.example.com"]` |
|Project |String |表示该全局配置所归属的项目名称。 |`default` |
|CommonMatchList |Object |表示通用列表的配置，对应 `ConfigType` 是 `common_match_list`。 | |
|CommonType |Object |表示该通用列表的内容。 | |
|IgnoreCase |Boolean |该参数的说明与 Referer 白名单下 `IgnoreCase` 的说明相同。 |`true` |
|Rules |String[] |表示该通用列表中的规则。 |`["abc","param"]` |
|CommonListType |String |表示通用列表使用何种方式将待匹配值与 `Rules` 中的规则进行匹配。<br><br>取值：<br><br><br>* `exact_match`：精确匹配。使用 `Rules` 中的字符串规则匹配待匹配值。字符串规则可在开头或结尾使用通配符 `*` 表示任意字符。<br><br>* `regex_match`：Regex 匹配。使用 `Rules` 中的正则表达式规则匹配待匹配值。<br><br>* `ip_match`：IP 匹配。使用 `Rules` 中的 IP 地址或 CIDR 网段规则匹配 IP 地址。 |`ip_match` |
|ErrorPageRule |Object |表示自定义错误页面的配置。 | |
|RuleContent |String |表示该自定义错误页面的 HTML 代码。 |`<html><head><title>Test</title></head><body><h1>Header</h1>Hello World</body></html>` |


<span id="示例"></span>
## 示例

<span id="请求示例"></span>
### 请求示例

```json
POST https://cdn.byteplusapi.com/?Action=DescribeSharedConfig&Version=2021-03-01
{
    "ConfigName": "My_List"
}
```


<span id="返回示例"></span>
### 返回示例

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
        "CommonMatchList": null,
        "ConfigName": "My_List",
        "ConfigType": "allow_referer_access_rule",
        "Project": "default"
    }
}
```
