---
title: "AddSharedConfig"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/AddSharedConfig_cn"
---

创建一个全局配置。

<span id="使用限制"></span>
## 使用限制

节流限制：您每秒最多可以提交 20 个 API 请求。

<span id="请求说明"></span>
## 请求说明


* Request Method：POST

* Request URL：https://cdn.byteplusapi.com/?Action=AddSharedConfig&Version=2021\-03\-01


<span id="请求参数"></span>
## 请求参数

<span id="query"></span>
### Query


|参数 |类型 |是否必选 |描述 |
|---|---|---|---|
|Action |String |是 |接口名称。当前 API 的名称为 `AddSharedConfig`。 |
|Version |String |是 |接口版本。当前 API 的版本为 `2021-03-01`。 |


<span id="body"></span>
### Body


|参数 |类型 |是否必选 |描述 |示例值 |
|---|---|---|---|---|
|ConfigName |String |是 |表示全局配置的名称。名称有以下要求：<br><br><br>* 名称可以包含汉字、字母、数字、下划线（_），长度在 3\-45 个字符之间。一个汉字占 3 个字符。<br><br>* 名称不能与主账号下某个已有的全局配置的名称相同。 |`my_list` |
|ConfigType |String |是 |表示该全局配置的类型。该参数有以下取值：<br><br><br>* `deny_ip_access_rule`：表示 IP 黑名单。<br><br>* `allow_ip_access_rule`：表示 IP 白名单。<br><br>* `deny_referer_access_rule`：表示 Referer 黑名单。<br><br>* `allow_referer_access_rule`：表示 Referer 白名单。<br><br>* `common_match_list`：表示通用列表。 |`allow_ip_access_rule` |
|AllowIpAccessRule |Object |否 |表示一个 IP 白名单的配置，对应 `ConfigType` 是 `allow_ip_access_rule`。 | |
|Rules |String[] |否 |表示一个规则列表，列表中的每条规则是一个 IP 地址或 CIDR 网段。IP 地址和网段可以是 IPv4 和 IPv6 格式。<br><br>列表的额度如下：<br><br><br>* 列表最多可以包含 30,000 个规则。<br><br><br>CDN 在创建该全局配置时，会将列表中重复的规则删除。重复规则不占额度。 |`["x.x.x.x","xx.xx.xx.xx/24"]` |
|IpSource |Object |否 |表示客户端 IP 地址获取方式的配置。 | |
|SourceList |String[] |否 |表示当 `Type` 为 `custom` 时，用于判断客户端 IP 地址的一个或多个来源。<br><br>取值：<br><br><br>* `x-real-ip`：表示从 `X-Real-IP` 请求头获取的 IP 地址。<br><br>* `x-forwarded-for`：表示从 `X-Forwarded-For` 请求头获取的 IP 地址。<br><br>* `client-ip`：表示真实建连 IP，即与 CDN 节点直接建立网络连接的对端 IP 地址。<br><br><br>对于 IP 黑名单，只要任一指定来源中获取的 IP 地址匹配黑名单规则，CDN 就拒绝请求。对于 IP 白名单，只有所有指定来源中获取的 IP 地址均匹配白名单规则，CDN 才允许请求。 |`["x-real-ip", "x-forwarded-for"]` |
|Type |String |否 |表示 CDN 判断客户端 IP 地址的方式。<br><br>取值：<br><br><br>* `default`：使用真实建连 IP。<br><br>* `custom`：使用 `SourceList` 中指定的一个或多个来源。无法从已选请求头获取 IP 地址时，CDN 对该来源使用真实建连 IP。<br><br><br>该参数的默认值是 `default`。 |`custom` |
|AllowRefererAccessRule |Object |否 |表示一个 Referer 白名单的配置，对应 `ConfigType` 是 `allow_referer_access_rule`。 | |
|AllowEmpty |Boolean |否 |表示是否允许 Referer 头部为空（""）或者不包含 Referer 头部的请求。该参数有以下取值：<br><br><br>* `true`：表示允许。<br><br>* `false`：表示不允许。如果请求的 Referer 头部为空（""）或者不包含 Referer 头部，CDN 拒绝请求。<br><br><br>该参数的默认值是 `false`。 |`false` |
|CommonType |Object |否 |表示该 Referer 白名单的内容。 | |
|IgnoreCase |Boolean |否 |表示 `Rules` 中的规则是否区分大小写。该参数有以下取值：<br><br><br>* `true`：表示不区分大小写。<br><br>* `false`：表示区分大小写。<br><br><br>该参数的默认值是 `true`。 |`true` |
|Rules |String[] |否 |表示一个规则列表，列表中的每条规则是一个域名或 IP 地址。域名可以是泛域名，IP 地址可以是 IPv4 和 IPv6 格式。<br><br>列表的额度如下：<br><br><br>* 列表最多可以包含 4,000 条规则。<br><br><br>CDN 在创建该全局配置时，会将列表中重复的规则删除。重复规则不占额度。 |`["xx.xx.xx.xx","*.example.com"]` |
|ContMainDomain |Boolean |否 |无 | |
|IgnoreScheme |Boolean |否 |无 | |
|DenyIpAccessRule |Object |否 |表示一个 IP 黑名单的配置，对应 `ConfigType` 是 `deny_ip_access_rule`。 | |
|Rules |String[] |否 |该参数的说明与 IP 白名单下 `Rules` 的说明相同。 |`["x.x.x.x","xx.xx.xxx.xx"]` |
|IpSource |Object |否 |该参数的说明与 IP 白名单下 `IpSource` 的说明相同。 | |
|SourceList |String[] |否 |该参数的说明与 IP 白名单下 `SourceList` 的说明相同。 |`["x-real-ip", "x-forwarded-for"]` |
|Type |String |否 |该参数的说明与 IP 白名单下 `Type` 的说明相同。 |`custom` |
|DenyRefererAccessRule |Object |否 |表示一个 Referer 黑名单的配置，对应 `ConfigType` 是 `deny_referer_access_rule`。 | |
|AllowEmpty |Boolean |否 |该参数的说明与 Referer 白名单下 `AllowEmpty` 的说明相同。 |`true` |
|CommonType |Object |否 |表示该 Referer 黑名单的内容。 | |
|IgnoreCase |Boolean |否 |该参数的说明与 Referer 白名单下 `IgnoreCase` 的说明相同。 |`true` |
|Rules |String[] |否 |该参数的说明与 Referer 白名单下 `Rules` 的说明相同。 |`["x.x.x.xxx","*.example.com"]` |
|Project |String |否 |表示该全局配置所归属的项目名称，默认值是 `default`。<br><br>您可以访问 [项目管理](https://console.byteplus.com/iam/resourcemanage/project) 查看已创建的项目以及每个项目包含的资源。 |`default` |
|CommonMatchList |Object |否 |表示一个通用列表的配置，对应 `ConfigType` 是 `common_match_list`。 | |
|CommonType |Object |否 |表示该通用列表的内容。 | |
|IgnoreCase |Boolean |否 |表示 `Rules` 中的规则是否区分大小写。该参数有以下取值：<br><br><br>* `true`：表示不区分大小写。<br><br>* `false`：表示区分大小写。<br><br><br>该参数的默认值是 `true`。 |`true` |
|Rules |String[] |否 |表示通用列表中的规则。规则格式和限制由 `CommonListType` 决定。<br><br><br>* 当 `CommonListType` 为 `exact_match` 时，每个数组元素必须是字符串。字符串首尾可使用通配符 `*` 表示任意字符，通配符不能出现在字符串中间。最多 4,000 个元素；所有元素的总长度不超过 200,000 个字符。<br><br>* 当 `CommonListType` 为 `regex_match` 时，每个数组元素必须是正则表达式。最多 30,000 个元素；所有元素的总长度不超过 200,000 个字符。<br><br>* 当 `CommonListType` 为 `ip_match` 时，每个数组元素必须是 IP 地址或 CIDR 网段。最多 30,000 个元素。<br><br><br>重复规则会自动去重，不计入规则数量限制。 |`["param1","param2"]` |
|CommonListType |String |否 |表示通用列表使用何种方式将待匹配值与 `Rules` 中的规则进行匹配。通用列表创建后，不能修改该参数。<br><br>取值：<br><br><br>* `exact_match`：精确匹配。使用 `Rules` 中的字符串规则匹配待匹配值。字符串规则可在开头或结尾使用通配符 `*` 表示任意字符。<br><br>* `regex_match`：Regex 匹配。使用 `Rules` 中的正则表达式规则匹配待匹配值。<br><br>* `ip_match`：IP 匹配。使用 `Rules` 中的 IP 地址或 CIDR 网段规则匹配 IP 地址。<br><br><br>该参数的默认值是 `exact_match`。 |`ip_match` |


<span id="返回参数"></span>
## 返回参数

<span id="示例"></span>
## 示例

<span id="请求示例"></span>
### 请求示例

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
