---
title: "UpdateSharedConfig"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/UpdateSharedConfig_cn"
---

修改一个全局配置。

<span id="使用限制"></span>
## 使用限制

节流限制：您每秒最多可以提交 20 个 API 请求。

<span id="请求说明"></span>
## 请求说明


* Request Method：POST

* Request URL：https://cdn.byteplusapi.com/?Action=UpdateSharedConfig&Version=2021\-03\-01


<span id="请求参数"></span>
## 请求参数

<span id="query"></span>
### Query


|参数 |类型 |是否必选 |描述 |
|---|---|---|---|
|Action |String |是 |接口名称。当前 API 的名称为 `UpdateSharedConfig`。 |
|Version |String |是 |接口版本。当前 API 的版本为 `2021-03-01`。 |


<span id="body"></span>
### Body


|参数 |类型 |是否必选 |描述 |示例值 |
|---|---|---|---|---|
|ConfigName |String |是 |表示一个全局配置的名称。<br><br>您可以调用 [ListSharedConfig](https://docs.byteplus.com/en/docs/byteplus-cdn/ListSharedConfig_cn) 获取已有的全局配置名称。 |`MySharedConfig` |
|AllowIpAccessRule |Object |否 |表示 IP 白名单的配置，对应 `ConfigType` 是 `allow_ip_access_rule`。 | |
|Option |String |否 |表示修改操作的类型。该参数有以下取值：<br><br><br>1. `overlap`：表示全量覆盖已有规则。<br><br>2. `add`：表示增加规则。<br><br>3. `delete`：表示删除指定的规则。<br><br><br>该参数的默认值为 `overlap`。 |`add` |
|Rules |String[] |否 |表示一个规则列表。每条规则是一个 IP 地址或 CIDR 网段。IP 地址和网段可以是 IPv4 和 IPv6 格式。<br><br>列表的额度如下：<br><br><br>* 如果 `Option` 是 `overlap`，列表中规则的数量不能超过 30,000 个。<br><br>* 如果 `Option` 是 `add`，列表中规则与 `ConfigName` 中已有规则总计不能超过 30,000 个。您可以调用 [DescribeSharedConfig](https://docs.byteplus.com/en/docs/byteplus-cdn/DescribeSharedConfig_cn) 计算该全局配置中已有的规则数量。<br><br><br>当 CDN 在更新 `ConfigName` 时，会将列表中重复的规则删除。重复规则不占额度。 |`["xx.xxx.xxx.xx","xxx.xxx.xxx.xxx"]` |
|IpSource |Object |否 |表示客户端 IP 地址获取方式的配置。 | |
|SourceList |String[] |否 |表示当 `Type` 为 `custom` 时，用于判断客户端 IP 地址的一个或多个来源。<br><br>取值：<br><br><br>* `x-real-ip`：表示从 `X-Real-IP` 请求头获取的 IP 地址。<br><br>* `x-forwarded-for`：表示从 `X-Forwarded-For` 请求头获取的 IP 地址。<br><br>* `client-ip`：表示真实建连 IP，即与 CDN 节点直接建立网络连接的对端 IP 地址。<br><br><br>对于 IP 黑名单，只要任一指定来源中获取的 IP 地址匹配黑名单规则，CDN 就拒绝请求。对于 IP 白名单，只有所有指定来源中获取的 IP 地址均匹配白名单规则，CDN 才允许请求。 |`["x-real-ip", "x-forwarded-for"]` |
|Type |String |否 |表示 CDN 判断客户端 IP 地址的方式。<br><br>取值：<br><br><br>* `default`：使用真实建连 IP。<br><br>* `custom`：使用 `SourceList` 中指定的一个或多个来源。无法从已选请求头获取 IP 地址时，CDN 对该来源使用真实建连 IP。<br><br><br>该参数的默认值是 `default`。 |`custom` |
|DenyIpAccessRule |Object |否 |表示 IP 黑名单的配置，对应 `ConfigType` 是 `deny_ip_access_rule`。 | |
|Option |String |否 |该参数的说明与 IP 白名单配置下 `Option` 的说明相同。 |`overlap` |
|Rules |String[] |否 |该参数的说明与 IP 白名单配置下 `Rules` 的说明相同。 |`["xx.xxx.xxx.xx","xxx.xxx.xxx.xxx/24"]` |
|IpSource |Object |否 |该参数的说明与 IP 白名单下 `IpSource` 的说明相同。 | |
|SourceList |String[] |否 |该参数的说明与 IP 白名单下 `SourceList` 的说明相同。 |`["x-real-ip", "x-forwarded-for"]` |
|Type |String |否 |该参数的说明与 IP 白名单下 `Type` 的说明相同。 |`custom` |
|AllowRefererAccessRule |Object |否 |表示 Referer 白名单的配置，对应 `ConfigType` 是 `allow_referer_access_rule`。 | |
|AllowEmpty |Boolean |否 |表示是否允许 Referer 头部为空（""）或者不包含 Referer 头部的请求。该参数有以下取值：<br><br><br>* `true`：表示允许。<br><br>* `false`：表示不允许。如果请求的 Referer 头部为空（""）或者不包含 Referer 头部，CDN 拒绝请求。<br><br><br>该参数的默认值是 `false`。 |`true` |
|CommonType |Object |否 |表示该 Referer 白名单的内容。 | |
|IgnoreCase |Boolean |否 |表示 `Rules` 中的规则是否区分大小写。该参数有以下取值：<br><br><br>* `true`：表示不区分大小写。<br><br>* `false`：表示区分大小写。<br><br><br>该参数的默认值是 `true`。 |`true` |
|Option |String |否 |表示修改操作的类型。该参数有以下取值：<br><br><br>1. `overlap`：表示全量覆盖已有规则。<br><br>2. `add`：表示增加规则。<br><br>3. `delete`：表示删除指定的规则。<br><br><br>该参数的默认值为 `overlap`。 |`overlap` |
|Rules |String[] |否 |表示一个规则列表。每条规则是一个 IP 地址或域名。IP 地址可以是 IPv4 和 IPv6 格式，域名可以是泛域名。<br><br>列表的额度如下：<br><br><br>* 如果 `Option` 是 `overlap`，列表中规则的数量不能超过 4,000 个。<br><br>* 如果 `Option` 是 `add`，列表中规则与 `ConfigName` 中已有规则总计不能超过 4,000 个。您可以调用 [DescribeSharedConfig](https://docs.byteplus.com/en/docs/byteplus-cdn/DescribeSharedConfig_cn) 计算该全局配置中已有的规则数量。<br><br><br>当 CDN 在更新 `ConfigName` 时，会将列表中重复的规则删除。重复规则不占额度。 |`["xxx.xx.xx.xxx","*.example.com"]` |
|DenyRefererAccessRule |Object |否 |表示 Referer 黑名单的配置，对应 `ConfigType` 是 `deny_referer_access_rule`。 | |
|AllowEmpty |Boolean |否 |该参数的说明与 Referer 白名单配置下 `AllowEmpty` 的说明相同。 |`true` |
|CommonType |Object |否 |表示该 Referer 黑名单的内容。 | |
|IgnoreCase |Boolean |否 |该参数的说明与 Referer 白名单配置下 `IgnoreCase` 的说明相同。 |`true` |
|Option |String |否 |该参数的说明与 IP 白名单配置下 `Option` 的说明相同。 |`overlap` |
|Rules |String[] |否 |该参数的说明与 Referer 白名单配置下 `Rules` 的说明相同。 |`["xxx.xx.xx.xxx","*.example.com"]` |
|CommonMatchList |Object |否 |表示通用列表的配置，对应 `ConfigType` 是 `common_match_list`。 | |
|CommonType |Object |否 |表示该通用列表的内容。 | |
|IgnoreCase |Boolean |否 |表示 `Rules` 中的规则是否区分大小写。该参数有以下取值：<br><br><br>* `true`：表示不区分大小写。<br><br>* `false`：表示区分大小写。<br><br><br>该参数的默认值是 `true`。 |`false` |
|Option |String |否 |表示修改操作的类型。CDN 根据该参数使用 `Rules` 更新 `ConfigName` 对应通用列表中的已有规则。<br><br>取值：<br><br><br>1. `overlap`：使用 `Rules` 替换所有已有规则。去重后的 `Rules` 必须符合 `CommonListType` 对应的规则格式和额度。<br><br>2. `add`：将 `Rules` 添加到已有规则中。添加并去重后，通用列表中的规则总数和总长度必须符合 `CommonListType` 对应的额度。您可以调用 [DescribeSharedConfig](https://docs.byteplus.com/en/docs/byteplus-cdn/DescribeSharedConfig_cn) 获取通用列表中的已有规则。<br><br>3. `delete`：从已有规则中删除 `Rules`。`Rules` 必须符合 `CommonListType` 对应的规则格式。<br><br><br>默认值为 `overlap`。 |`overlap` |
|Rules |String[] |否 |表示需要删除、添加或替换的规则。每个规则为字符串。<br><br>更新完成后的通用列表必须符合 `ConfigName` 对应通用列表的 `CommonListType` 所规定的规则格式和额度。<br><br><br>* 当 `CommonListType` 为 `exact_match` 时，规则为字符串。字符串首尾可使用通配符 `*` 表示任意字符，通配符不能位于字符串中间。通用列表最多包含 `4,000` 条规则，所有规则的总长度不超过 `200,000` 个字符。<br><br>* 当 `CommonListType` 为 `regex_match` 时，规则为正则表达式。通用列表最多包含 `30,000` 条规则，所有规则的总长度不超过 `200,000` 个字符。<br><br>* 当 `CommonListType` 为 `ip_match` 时，规则为 IP 地址或 CIDR 网段。通用列表最多包含 `30,000` 条规则。<br><br><br>CDN 更新 `ConfigName` 时会自动删除重复规则。重复规则不占用规则额度。 |`["param1","param2"]` |


<span id="返回参数"></span>
## 返回参数

<span id="示例"></span>
## 示例

<span id="请求示例"></span>
### 请求示例

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
