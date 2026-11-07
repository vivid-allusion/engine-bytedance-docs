---
title: "DescribeCdnConfig"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/DescribeCdnConfig_zh-cn"
---

获取 BytePlus CDN 中一个域名的配置。

<span id="使用限制"></span>
## 使用限制

节流限制：您每秒最多可以提交 20 个 API 请求。

<span id="请求说明"></span>
## 请求说明


* Request Method：POST

* Request URL：https://cdn.byteplusapi.com/?Action=DescribeCdnConfig&Version=2021\-03\-01


<span id="请求参数"></span>
## 请求参数

<span id="query"></span>
### Query


|参数 |类型 |是否必选 |描述 |
|---|---|---|---|
|Action |String |是 |接口名称。当前 API 的名称为 `DescribeCdnConfig`。 |
|Version |String |是 |接口版本。当前 API 的版本为 `2021-03-01`。 |


<span id="body"></span>
### Body


|参数 |类型 |是否必选 |描述 |示例值 |
|---|---|---|---|---|
|Domain |String |是 |表示一个域名，获取该域名的配置。 |`www.example.com` |


<span id="返回参数"></span>
## 返回参数


|参数 |类型 |描述 |示例值 |
|---|---|---|---|
|DomainConfig |Object |表示 `Domain` 的配置。 | |
|Domain |String |表示请求参数中的 `Domain`。 |`www.example.com` |
|Origin |Object[] |表示源站配置。 | |
|OriginAction |Object |表示源站配置,，应用于所有用户请求。 | |
|OriginLines |Object[] |表示一个源站列表。 | |
|Address |String |表示列表中一个源站的地址。 |`www.example.com` |
|InstanceType |String |表示源站的类型。该参数有以下取值：<br><br><br>* `ip`：表示 IP 地址。<br><br>* `domain`：表示域名。<br><br>* `tos`：表示对象存储桶。 |`ip` |
|OriginType |String |表示该源站的类别。该参数有以下取值：<br><br><br>* `primary`：表示主源站。<br><br>* `backup`：表示备源站。 |`primary` |
|HttpPort |String |表示 CDN 使用 HTTP 协议访问该源站时所访问的端口。 |`80` |
|HttpsPort |String |表示 CDN 使用 HTTPS 协议访问该源站时所访问的端口。 |`443` |
|OriginHost |String |表示回源请求访问的站点域名，优先级高于全局 `OriginHost` 参数。 |`img.example.com` |
|PrivateBucketAccess |Boolean |表示存储桶是否是私有桶。该参数仅当 `InstanceType` 为 `tos` 时有效。该参数有以下取值：<br><br><br>* `true`：表示该存储桶是私有桶。<br><br>* `false`：表示该存储桶不是私有桶。 |`false` |
|PrivateBucketAuth |Object |表示访问存储桶的鉴权配置。 | |
|Switch |Boolean |表示存储桶访问是否需要鉴权，该参数有以下取值：<br><br><br>* `true`：表示访问需要鉴权。<br><br>* `false`：表示访问无需鉴权。 |`false` |
|AuthType |String |表示存储桶使用的是哪个对象存储服务所提供的鉴权方式。该参数有以下取值：<br><br><br>* `tos`：表示 BytePlus TOS。<br><br>* `cos`：表示腾讯云 COS。<br><br>* `oss`：表示阿里云 OSS。<br><br>* `azure`：表示 Microsoft Azure。<br><br>* `aws_common`：表示 AWS S3 或者其他使用兼容 S3 鉴权方式的第三方对象存储服务。 |`cos` |
|TosAuthInformation |Object |表示存储桶的访问凭证（AccessKey）。 | |
|AccessKeyId |String |表示访问凭证中的 AccessKey ID，在腾讯云称为 SecretId。 |`xxxxxxxx` |
|AccessKeySecret |String |表示访问凭证中的 AccessKey Secret，在腾讯云称为 SecretKey。 |`xxxxxx` |
|AccountKey |String |表示您 Azure 存储账号的共享密钥（Key）。该参数仅当 `AuthType` 为 `azure` 时有效。 |`xxxxxx` |
|Region |String |表示存储桶所在地域的信息，也就是存储桶的 region code。Region code 参与签名的计算。 |`us-east-1` |
|Weight |String |表示该源站的权重，权重越大，该源站在 CDN 发送回源请求时被选择到的概率也越大。<br><br>该参数仅当 `InstanceType` 为 `ip` 或 `domain` 时才有效。 |`100` |
|BucketName |String |表示您 Azure 存储账号的名称。该参数仅当 `AuthType` 为 `azure` 时有效。 |`mystorageaccount` |
|OriginProtocol |String |表示回源请求使用的协议。该参数有以下取值：<br><br><br>* `http`：表示回源请求使用 HTTP 协议。<br><br>* `https`：表示回源请求使用 HTTPS 协议。<br><br>* `followclient`：表示回源协议与用户请求使用的协议相同。 |`http` |
|AreaAccessRule |Object |表示 "地域访问控制" 特性的配置。 | |
|Area |String[] |表示一个国家和地区的列表，对该列表应用地域访问限制。国家和地区的名称使用简写来表示。您可以调用 [DescribeCdnRegionAndIsp](https://docs.byteplus.com/en/docs/byteplus-cdn/DescribeCdnRegionAndIsp) 并指定 `Area` 为 `Global` 以获取国家和地区的简写。 |`["CHE","AZE"]` |
|RuleType |String |表示 `Area` 的类型。该参数有以下取值：<br><br><br>* `deny`: 表示 `Area` 是一个黑名单。CDN 将阻止来自这些国家和地区的请求。<br><br>* `allow`: 表示 `Area` 是一个白名单。CDN 仅允许来自这些国家和地区的请求。 |`allow` |
|Switch |Boolean |表示是否启用该特性。该参数有以下取值：<br><br><br>* `true`：表示启用该特性。<br><br>* `false`：表示禁用该特性。 |`true` |
|BrowserCache |Object[] |表示 "浏览器缓存" 特性的配置，包含一个规则列表，说明如下：<br><br><br>* 每条规则包含匹配条件配置和操作配置。<br><br>* 规则在列表中出现的顺序表示规则的优先级。列表中第一条规则的优先级最高。<br><br>* 当收到一个用户请求时，CDN 按规则的优先级，从高到低将规则与请求匹配。如果一条规则匹配了请求，CDN 就停止处理其余规则。 | |
|CacheAction |Object |当一个请求满足 `Condition` 中的匹配条件时，CDN 会对请求文件执行指定的操作。该参数定义了该操作相关的配置。 | |
|Action |String |表示浏览器需要执行的操作。当前该参数值只能是 `cache`，表示缓存请求的文件。`DefaultPolicy` 中指定了如何缓存请求的文件。 |`cache` |
|IgnoreCase |Boolean |表示 `Value` 是否是大小写敏感的。<br><br><br>* `true`：表示大小写不敏感。<br><br>* `false`：表示大小写敏感。 |`true` |
|Ttl |Long |表示浏览器需要缓存请求文件的时长，单位是秒。CDN 会在响应头中包含 `Cache-Control: max-age` 头部，头部值就是该参数值。 |`100` |
|DefaultPolicy |String |表示浏览器该如何缓存请求的文件。该参数有以下取值：<br><br><br>* `cache`：表示需要缓存请求的文件。<br><br>* `origin_first`：表示遵循来自源站的缓存策略。该策略会包含在 CDN 的响应中。<br><br>* `no_cache`：表示不需要缓存请求的文件。<br><br><br>关于浏览器缓存策略的详细信息，参见 [浏览器缓存策略](https://docs.byteplus.com/en/docs/byteplus-cdn/docs_cn-browser-caching-cn)。 |`cache` |
|SetCookieNoCache |Boolean |是否设置cookie不缓存，仅支持节点缓存规则 | |
|Condition |Object |表示匹配条件的配置。如果请求匹配了某个条件，CDN 对该请求执行 `CacheAction` 中指定的操作。 | |
|ConditionRule |Object[] |表示匹配条件列表。当前，列表中只能包含一个匹配条件。 | |
|Object |String |表示匹配条件中的匹配类型。该参数有以下取值：<br><br><br>* `filetype`：表示 URL 路径末尾的扩展名。<br><br>* `directory`：表示 URL 路径中的一个目录。<br><br>* `path`：表示完整的 URL 路径。 |`directory` |
|Operator |String |表示匹配类型。该参数的值只能是 `match`，表示如果 `Value` 匹配了请求中的 `Object`，该请求就满足这个匹配条件。 |`match` |
|Type |String |该参数值只能是 `url`，表示 "请求 URL"。 |`url` |
|Value |String |表示一个或者多个匹配值。多个匹配值之间使用分号（;）分隔。 |`png` |
|Cache |Object[] |表示 "缓存规则" 特性的配置，包含一个规则列表，说明如下：<br><br><br>* 列表中规则的顺序定义了规则的优先级。列表中第一条规则的优先级最高。<br><br>* 当收到一个用户请求时，CDN 按规则的优先级，从高到低将规则与请求匹配。如果一条规则匹配了请求，CDN 就停止处理其余规则。 | |
|CacheAction |Object |当一个请求满足 `Condition` 中的匹配条件时，CDN 会对请求文件执行指定的操作。该参数定义了该操作相关的配置。 | |
|Action |String |表示 CDN 执行的操作。当前该参数值只能是 `cache`，表示缓存请求的文件。`DefaultPolicy` 中指定了如何缓存请求的文件。 |`cache` |
|IgnoreCase |Boolean |表示 `Value` 是否是大小写敏感的。该参数有以下取值：<br><br><br>* `true`：表示大小写不敏感。<br><br>* `false`：表示大小写敏感。 |`true` |
|Ttl |Long |表示请求文件的缓存时长，单位为`秒`。<br><br>如果该参数值为 `0`，CDN 在收到匹配规则的请求时，会按以下方式处理：<br><br><br>* 如果文件尚未被缓存，CDN 不会缓存该文件。<br><br>* 如果文件已被缓存，该文件会立即过期，后续对该文件的请求将触发 [回源校验](https://docs.byteplus.com/en/docs/byteplus-cdn/docs_cn-caching-rules-cn#%E5%9B%9E%E6%BA%90%E6%A0%A1%E9%AA%8C)。这种情况通常发生在您修改缓存规则，将一个已缓存文件的缓存时长从非零值改为 `0` 时。 |`100` |
|DefaultPolicy |String |表示 CDN 对请求文件的缓存行为。该参数有以下取值：<br><br><br>* `force_cache`：对应 CDN 控制台中的 **CDN缓存** + **强制缓存（开）**  的配置组合。<br><br>* `default`：对应 CDN 控制台中的 **CDN缓存** + **强制缓存（关）**  的配置组合。<br><br>* `origin_first`：对应 CDN 控制台中的 **遵循源站** + **补充缓存（开）**  的配置组合。<br><br>* `origin_first_Replenish`：对应 CDN 控制台中的 **遵循源站** + **补充缓存（关）**  的配置组合。<br><br>* `no_cache`：对应 CDN 控制台中的 **不缓存** 配置。<br><br><br>关于这些缓存策略的描述，参见 [缓存规则](https://docs.byteplus.com/zh-CN/byteplus-cdn/docs/caching-rules)。 |`force_cache` |
|SetCookieNoCache |Boolean |表示是否缓存包含 `Set-Cookie` 头部的源站响应。该参数有以下取值：<br><br><br>* `true`：表示 CDN 会缓存这类响应。<br><br>* `false`：表示 CDN 不会缓存这类响应。<br><br><br>说明<br><br>如果 `DefaultPolicy` 为 `force_cache`，`SetCookieNoCache` 不生效。 |`true` |
|Condition |Object |表示匹配条件的配置。如果请求匹配了某个条件，CDN 对该请求执行 `CacheAction` 中指定的操作。 | |
|ConditionRule |Object[] |表示匹配条件列表。 | |
|Object |String |表示匹配对象。该参数有以下取值：<br><br><br>* `filetype`：表示请求 URL 中的扩展名。<br><br>* `directory`：表示请求 URL 中的某个目录。<br><br>* `path`：表示请求 URL 中的完整路径。 |`directory` |
|Operator |String |表示匹配类型。该参数的值只能是 `match`，表示如果 `Value` 匹配了请求中的 `Object`，该请求就满足这个匹配条件。 |`match` |
|Type |String |该参数值只能是 `url`，表示 "请求 URL"。 |`url` |
|Value |String |表示一个或者多个匹配值。多个匹配值之间使用分号（;）分隔。 |`png` |
|CacheHost |Object |表示 "共享缓存" 特性的配置。 | |
|CacheHostRule |Object[] |表示一组共享缓存的配置。 | |
|CacheHostAction |Object |表示某个配置的详情。 | |
|CacheHost |String |表示目标域名。 该目标域名必须是您账户下的一个另一个域名。该参数指示 `Domain` 共享 `CacheHost` 的 CDN 缓存。 |`www.test.com` |
|Switch |Boolean |表示是否启用该特性。该参数有以下取值：<br><br><br>* `true`：表示启用该特性。<br><br>* `false`：表示禁用该特性。 |`true` |
|CacheKey |Object[] |表示 "缓存键规则" 特性的配置，包含一个规则列表，说明如下：<br><br><br>* 每条规则包含匹配条件配置和操作配置。<br><br>* 规则在列表中出现的顺序表示规则的优先级。列表中第一条规则的优先级最高。<br><br>* 当收到一个用户请求时，CDN 按规则的优先级，从高到低将规则与请求匹配。如果一条规则匹配了请求，CDN 就停止处理其余规则。 | |
|CacheKeyAction |Object |当一个请求满足 `Condition` 中的匹配条件时，CDN 会为请求文件设置缓存键。该参数表示缓存键的配置。 | |
|CacheKeyComponents |Object[] |缓存键是由请求中的 host、路径和查询字符串等部分组成。该参数表示其中各组成部分的配置。 | |
|Action |String |表示 CDN 如何在请求文件的缓存键中设置查询字符串。该参数有以下取值：<br><br><br>* `exclude`：表示缓存键不包含请求中的任何查询参数。<br><br>* `include`：表示缓存键包含请求中所有的查询参数。缓存键中查询参数的顺序与请求 URL 中的顺序相同。<br><br>* `includePart`：表示缓存键仅包含 `Subobject` 中指定的查询参数。CDN 对包含在缓存键中的查询参数按字母顺序排序后生成缓存键。<br><br>* `excludePart`：表示缓存键包含请求中除了 `Subobject` 中指定的查询参数之外的所有查询参数。CDN 对包含在缓存键中的查询参数按字母顺序排序后生成缓存键。<br><br><br>说明<br><br>缓存键中查询参数的顺序影响缓存匹配。如果请求 URL 中查询参数的顺序与缓存键中的查询参数的顺序不同，则 CDN 判定请求未命中缓存。 |`excludePart` |
|IgnoreCase |Boolean |表示 `Subobject` 是否是大小写敏感的。该参数有以下取值：<br><br><br>* `true`：表示大小写不敏感。<br><br>* `false`：表示大小写敏感。 |`true` |
|Object |String |表示缓存键中的一个组成部分。当前该参数值只能是 `querystring`，表示查询字符串。 |`queryString` |
|Subobject |String |该参数对应于 `Action`，表示 CDN 在缓存键中包含的具体查询参数。该参数的说明如下：<br><br><br>* 如果 `Action` 是 `include` 或者 `exclude`，`Subobject` 是 `*`，表示请求中的全部查询参数。<br><br>* 如果 `Action` 是 `includePart` 或者 `excludePart`，表示需要保留或者不保留的查询参数。多个查询参数之间使用分号（;）分隔。 |`sign;testParams` |
|Condition |Object |表示匹配条件的配置。如果请求匹配了某个条件，CDN 对该请求执行 `CacheKeyAction` 中指定的操作。 | |
|ConditionRule |Object[] |表示匹配条件列表。列表中只能包含一个匹配条件。 | |
|Object |String |表示匹配对象。该参数有以下取值：<br><br><br>* `filetype`：表示请求 URL 中的扩展名。<br><br>* `directory`：表示请求 URL 中的某个目录。<br><br>* `path`：表示请求 URL 中的完整路径。 |`directory` |
|Operator |String |表示匹配类型。该参数的值只能是 `match`，表示如果 `Value` 匹配了请求中的 `Object`，该请求就满足这个匹配条件。 |`match` |
|Type |String |该参数值只能是 `url`，表示 "请求 URL"。 |`url` |
|Value |String |表示一个或者多个匹配值。多个匹配值之间使用分号（;）分隔。 |`png` |
|IgnoreCase |Boolean |表示 `Value` 是否是大小写敏感的。该参数有以下取值：<br><br><br>* `true`：表示大小写不敏感。<br><br>* `false`：表示大小写敏感。 |`true` |
|Compression |Object |表示 "智能压缩" 特性的配置。 | |
|Switch |Boolean |表示是否启用该特性。该参数有以下取值：<br><br><br>* `true`：表示启用该特性。<br><br>* `false`：表示禁用该特性。 |`true` |
|CompressionRules |Object[] |表示一组规则。每条规则包含匹配条件配置以及操作配置。 | |
|CompressionAction |Object |表示当用户请求满足 `Condition` 时，CDN 对请求文件执行的压缩操作的配置。 | |
|CompressionType |String[] |表示 CDN 使用的一个或者多个压缩算法。该参数有以下取值：<br><br><br>* `br`：表示 Brotli 压缩算法。<br><br>* `gzip`：表示 Gzip 压缩算法。<br><br><br>需要留意的是，CDN 基于用户请求中 `Accept-Encoding` 头部来决定是否对请求文件进行压缩以及使用的压缩算法。 |`["gzip","br"]` |
|CompressionFormat |String |表示 CDN 基于请求中的 `Content-Type` 头部对请求进行匹配。该参数有以下取值：<br><br><br>* `default`：表示如果 `Content-Type` 头部值在下方的默认列表中，CDN 对请求文件执行 `CompressionAction` 中配置的操作。<br><br>* `customize`：表示如果 `Content-Type` 头部值在 `CompressionFormat` 指定的头部值中，CDN 对请求文件执行 `CompressionAction` 中配置的操作。<br><br><br>**默认列表**<br><br>text/html、text/xml、text/plain、text/css、application/javascript、application/x\-javascript、application/rss+xml、text/javascript、image/tiff、image/svg+xml、application/json、application/xml、text/plain; charset=utf\-8 |`customize` |
|CompressionTarget |String |表示 `Content-Type` 的过滤值。<br><br><br>* 如果 `CompressionFormat` 为 `default` 或者 `all`，该参数为 `*`。<br><br>* 如果 `CompressionFormat` 为 `customize`，该参数包含一个或者多个文件类型。多个文件类型之间以逗号（,）分隔。 |`application/xml,hello/world` |
|MinFileSizeKB |Long |表示文件大小的最小值，CDN 仅对大小在 `MinFileSizeKB` 和 `MaxFileSizeKB` 所表示的范围内的文件进行压缩。该参数的单位是 KB，使用的进制是 1,024。 |`10` |
|MaxFileSizeKB |Long |表示文件大小的最大值，单位是 KB，使用的进制是 1,024。如果不指定该参数，表示不限制文件大小的上限。 |`1000` |
|Condition |Object |表示匹配条件的配置。如果请求匹配了某个条件，CDN 对该请求执行 `CompressionAction` 中指定的操作。 | |
|ConditionRule |Object[] |表示匹配条件列表。 | |
|Object |String |表示匹配对象。该参数有以下取值：<br><br><br>* `filetype`：表示请求 URL 中的扩展名。<br><br>* `directory`：表示请求 URL 中的某个目录。<br><br>* `path`：表示请求 URL 中的完整路径。 |`directory` |
|Operator |String |表示匹配类型。该参数的值只能是 `match`，表示如果 `Value` 匹配了请求中的 `Object`，该请求就满足这个匹配条件。 |`match` |
|Type |String |该参数值只能是 `url`，表示 "请求 URL"。 |`url` |
|Value |String |表示一个或者多个匹配值。多个匹配值之间使用分号（;）分隔。 |`/img/` |
|CustomErrorPage |Object |表示 "自定义错误页面" 特性的配置。 | |
|Switch |Boolean |表示是否启用该特性。该参数有以下取值：<br><br><br>* `true`：表示启用该特性。<br><br>* `false`：表示禁用该特性。 |`true` |
|ErrorPageRule |Object[] |表示一个配置规则列表。 | |
|ErrorPageAction |Object |表示规则的相关配置。 | |
|Action |String |表示操作的配置。当前该参数值只能为 `redirect`。表示对客户端请求进行重定向。 |`redirect` |
|RedirectCode |String |表示重定向的响应状态码。该参数的取值有 `301`、`302`、`303`、`307`、`308`。<br><br>需要留意的是：<br><br><br>* 对于 301 和 302，如果原请求使用的方法不是 GET，那么客户端向新的URL发送请求时，新请求使用的方法可能变成 GET。<br><br>* 对于 303，新请求使用的方法是 GET。<br><br>* 对于 307 和 308，新请求使用的方法与原请求相同，不会被改变。 |`302` |
|RedirectUrl |String |表示跳转的目标地址。 |`http://www.test.com/friendlyurl.html` |
|StatusCode |String |表示一个状态码，可以是 4xx 或者 5xx。4xx 表示 400\-499 之间的所有状态码。5xx 表示 500\-599 之间的所有状态码。 |`4xx` |
|DownloadSpeedLimit |Object |表示 "下载限速" 特性的配置。 | |
|Switch |Boolean |表示是否启用该特性。该参数有以下取值：<br><br><br>* `true`：表示启用该特性。<br><br>* `false`：表示禁用该特性。 |`true` |
|DownloadSpeedLimitRules |Object[] |表示一个限速规则的列表。该参数的其他说明如下：<br><br><br>* 每条规则包含匹配条件配置和限速配置。<br><br>* 列表中规则的出现顺序表示规则的优先级排序。列表中第一条规则的优先级最高。<br><br>* 当收到一个用户请求时，CDN 按规则的优先级，从高到低将规则与请求匹配。如果一条规则匹配了请求，CDN 就停止处理其余规则。 | |
|DownloadSpeedLimitAction |Object |表示限速配置。 | |
|SpeedLimitRate |Long |表示 CDN 在响应单个请求时的最大数据传输速度，单位是 `B/S`，使用的进制是 `1,024`。 |`500000` |
|SpeedLimitRateAfter |Long |表示一个初始数据量，单位是 `bytes`，使用的进制是 `1,024`。<br><br>当 CDN 对一个请求开始传输数据时，在传输的数据量达到该初始数据量前，该限速规则不会启用。<br><br>如果该参数值是 `0`，表示在 CDN 对一个请求开始传输第一个字节时，该限速规则就启用了。 |`1000` |
|SpeedLimitTime |Object |表示限速规则启用的日期和时间段。 | |
|DayWeek |String |表示该限速规则启用的日期，有以下取值：`monday`，`tuesday`，`wednesday`，`thursday`，`friday`，`saturday`，`sunday`，`unlimited`。<br><br>`unlimited` 表示每天。多个日期之间使用分号（;）分隔。 |`monday;friday` |
|BeginTime |String |表示该限速规则启用的开始时间，格式是 `mm:ss`。 |`05:08` |
|EndTime |String |表示该限速规则启用的结束时间，格式是 `mm:ss`。 |`16:48` |
|Condition |Object |表示匹配条件的配置。如果请求匹配了某个条件，CDN 对该请求执行 `DownloadSpeedLimitAction` 中指定的操作。<br><br>如果该参数未出现或者为 `null`，CDN 对所有请求执行 `DownloadSpeedLimitAction` 中指定的操作。 | |
|ConditionRule |Object[] |表示匹配条件列表。 | |
|Object |String |表示匹配对象。该参数有以下取值：<br><br><br>* `filetype`：表示请求 URL 中的扩展名。<br><br>* `directory`：表示请求 URL 中的某个目录。<br><br>* `path`：表示完整的请求路径。<br><br>* `unlimited`：表示域名下的所有文件。<br><br>* `regex`：表示完整的请求路径，通过正则表达式匹配。 |`filetype` |
|Operator |String |表示匹配类型。该参数的值只能是 `match`，表示如果 `Value` 匹配了请求中的 `Object`，该请求就满足这个匹配条件。 |`match` |
|Type |String |该参数值只能是 `url`，表示 "请求 URL"。 |`url` |
|Value |String |表示一个或者多个匹配值。多个匹配值之间使用分号（;）分隔。 |`/www/img/f1/;/www/doc/` |
|FollowRedirect |Boolean |表示 "回源重定向跟随" 特性的配置。该参数有以下取值：<br><br><br>* `true`：表示启用该特性。<br><br>* `false`：表示禁用该特性。 |`true` |
|HTTPS |Object |表示 HTTPS 加密服务的配置。 | |
|Switch |Boolean |表示是否启用 HTTPS 加密服务。该参数有以下取值：<br><br><br>* `true`：表示启用 HTTPS 加密服务。<br><br>* `false`：表示禁用 HTTPS 加密服务。 |`true` |
|CertInfo |Object |表示要与域名关联的证书。 | |
|CertId |String |表示要关联的证书 ID。 |`cert-eb5d99026753499a8a34d2a4f0a08d92` |
|DisableHttp |Boolean |表示是否允许请求 URL 中 Scheme 是 `HTTP` 的请求。该参数有以下取值：<br><br><br>* `true`：表示允许 Scheme 是 `HTTP` 的请求。<br><br>* `false`：表示不允许 Scheme 是 `HTTP` 的请求。 |`false` |
|ForcedRedirect |Object |表示 "HTTP 强制跳转到 HTTPS" 特性的配置。<br><br>说明<br><br>CDN 提供了两种协议重定向的特性。<br><br><br>* HTTP 重定向到 HTTPS，也就是 `ForcedRedirect` 特性。<br><br>* HTTPS 重定向到 HTTP，也就是 `HttpForcedRedirect` 特性。<br><br><br>这两个协议重定向特性是互斥的。也就是说，其中一个特性启用了，另一个就不能启用。 | |
|EnableForcedRedirect |Boolean |表示是否启用该特性。该参数有以下取值：<br><br><br>* `true`：表示启用该特性。启用后，CDN 会将收到的 HTTP 请求重定向到 HTTPS 请求。<br><br>* `false`：表示禁用该特性。禁用后，CDN 不会将 HTTP 请求重定向到 HTTPS 请求。 |`true` |
|StatusCode |String |表示当收到 HTTPS 请求时 CDN 的重定向响应状态码。该参数有以下取值：<br><br><br>* `301`：表示返回的状态码是 301。<br><br>* `302`：表示返回的状态码是 302。 |`301` |
|HTTP2 |Boolean |表示是否为用户请求启用 HTTP/2 支持。该参数有以下取值：<br><br><br>* `true`：表示启用 HTTP/2。<br><br>* `false`：表示禁用 HTTP/2。 |`true` |
|Hsts |Object |表示 HSTS 特性的配置。 | |
|Subdomain |String |表示 HSTS 配置是否也应用于域名的子域名。该参数有以下取值：<br><br><br>* `include`：表示 HSTS 配置应用于子域名站点。<br><br>* `exclude`：表示 HSTS 配置不应用于子域名站点。 |`include` |
|Switch |Boolean |表示是否启用该特性。该参数有以下取值：<br><br><br>* `true`：表示启用该特性。<br><br>* `false`：表示禁用该特性。 |`true` |
|Ttl |Long |表示 `Strict-Transport-Security` 响应头在浏览器中的缓存过期时间，单位是秒。<br><br>如果该参数值为 `0`，其效果等同于禁用 HSTS 设置。 |`300` |
|OCSP |Boolean |表示是否启用 "OCSP 装订" 特性。该参数有以下取值：<br><br><br>* `true`：表示启用该特性。<br><br>* `false`：表示禁用该特性。 |`true` |
|TlsVersion |String[] |表示 "TLS 版本" 特性的配置。该参数指定用户请求可以使用的 TLS 版本，有以下取值：<br><br><br>* `tlsv1.0`：表示 TLS 1.0。<br><br>* `tlsv1.1`：表示 TLS 1.1。<br><br>* `tlsv1.2`：表示 TLS 1.2。<br><br>* `tlsv1.3`：表示 TLS 1.3。、 |`["tlsv1.1","tlsv1.2"]` |
|CertCheck |Object |表示 "访问双向认证" 特性的配置。 | |
|CertInfoList |Object[] |表示一个 CA 证书列表。列表中最多包含两个 CA 证书。这些 CA 证书必须是已经托管在 CDN 的。CA 证书使用的加密算法可以是 RSA 或者 ECC。 | |
|CertId |String |表示一个 CA 证书的 ID。ID 是以 `cert_hosting-` 开头的。 |`cert_hosting-31869` |
|Switch |Boolean |表示是否启用该特性。该参数有以下取值：<br><br><br>* `true`：表示启用该特性。<br><br>* `false`：表示禁用该特性。<br><br><br>该参数的默认值是 `false`。 |`true` |
|HttpForcedRedirect |Object |表示 "HTTPS 强制跳转到 HTTP" 特性的配置。 | |
|EnableForcedRedirect |Boolean |表示是否启用该特性。该参数有以下取值：<br><br><br>* `true`：表示启用该特性。启用后，CDN 会将收到的 HTTPS 请求重定向到 HTTP 请求。<br><br>* `false`：表示禁用该特性。CDN 不会将 HTTPS 请求重定向到 HTTP 请求。 |`true` |
|StatusCode |String |表示当收到 HTTPS 请求时，CDN 返回的重定向状态码。该参数有以下取值：**301**、**302**、**303**、**307**、**308**。<br><br>需要留意的是：<br><br><br>* 对于 301 和 302，如果原请求使用的方法不是GET，那么客户端向新的URL发送请求时，新请求使用的方法可能变成 GET。<br><br>* 对于 303，新请求使用的方法是 GET。<br><br>* 对于 307 和 308，新请求使用的方法与原请求相同，不会被改变。 |`302` |
|IPv6 |Object |表示 IPv6 配置。 | |
|Switch |Boolean |表示是否为用户请求启用 IPv6 支持。该参数有以下取值：<br><br><br>* `true`：表示启用 IPv6。<br><br>* `false`：表示禁用 IPv6。 |`true` |
|IpAccessRule |Object |表示 "IP 黑白名单" 特性的配置。<br><br>该特性提供了两种配置方式：<br><br><br>* 常规配置：指定 `RuleType` 和 `Ip` 对当前域名进行配置。<br><br>* 全局配置：指定 `SharedConfig` 使用一个全局配置。 | |
|Ip |String[] |表示黑名单或白名单中的 IP 地址。 |`["xx.xxx.xx.xx","x.x.x.x"]` |
|RuleType |String |表示 IP 名单的类型。该参数有以下取值：<br><br><br>* `allow`：表示白名单。<br><br>* `deny`：表示黑名单。 |`deny` |
|Switch |Boolean |表示是否启用该特性。该参数有以下取值：<br><br><br>* `true`：表示启用该特性。<br><br>* `false`：表示禁用该特性。 |`true` |
|SharedConfig |Object |表示一个全局配置。 | |
|ConfigName |String |表示一个全局配置的名称。该全局配置的 `ConfigType` 必须是 `deny_ip_access_rule` 或者 `allow_ip_access_rule`。<br><br><br>* `deny_ip_access_rule`：表示 IP 黑名单。<br><br>* `allow_ip_access_rule`：表示 IP 白名单。<br><br><br>您可以调用 [ListSharedConfig](https://docs.byteplus.com/en/docs/byteplus-cdn/ListSharedConfig_cn) 获取全局配置的列表。 |`my_whitelist` |
|DenyStatusCode |Long |表示 CDN 在拒绝请求时响应的状态码。 |`403` |
|IpSource |Object |表示客户端 IP 地址获取方式的配置。 | |
|SourceList |String[] |表示当 `Type` 为 `custom` 时，用于判断客户端 IP 地址的一个或多个来源。<br><br>取值：<br><br><br>* `x-real-ip`：表示从 `X-Real-IP` 请求头获取的 IP 地址。<br><br>* `x-forwarded-for`：表示从 `X-Forwarded-For` 请求头获取的 IP 地址。<br><br>* `client-ip`：表示真实建连 IP，即与 CDN 节点直接建立网络连接的对端 IP 地址。<br><br><br>对于 IP 黑名单，只要任一指定来源中获取的 IP 地址匹配黑名单规则，CDN 就拒绝请求。对于 IP 白名单，只有所有指定来源中获取的 IP 地址均匹配白名单规则，CDN 才允许请求。 |`["x-real-ip", "x-forwarded-for"]` |
|Type |String |表示 CDN 判断客户端 IP 地址的方式。<br><br>取值：<br><br><br>* `default`：使用真实建连 IP。<br><br>* `custom`：使用 `SourceList` 中指定的一个或多个来源。无法从已选请求头获取 IP 地址时，CDN 对该来源使用真实建连 IP。 |`default` |
|IpFreqLimit |Object |表示 "IP 访问限频" 功能的配置模块。该功能默认为禁用。要使用该功能，[提交工单](https://console.byteplus.com/workorder/create)。 | |
|Switch |Boolean |表示该功能的开关。该参数有以下取值：<br><br><br>* `true`：表示启用该功能。<br><br>* `false`：表示禁用该功能。 |`true` |
|IpFreqLimitRules |Object[] |表示一组限频的规则。当 `Switch` 为 `true` 时，该参数为必填。当前您只能指定一条规则。 | |
|IpFreqLimitAction |Object |表示限频操作的配置。 | |
|Action |String |表示当一个 IP 地址的 QPS 达到 `FreqLimitRate` 时，CDN 的行为。当前，您只能指定该参数值为 `deny`，表示 CDN 拒绝来自该 IP 地址的新请求。 |`deny` |
|FreqLimitRate |Long |指定 IP 的 QPS 阈值。该参数的取值范围是 1\-1,000,000。 |`5000` |
|StatusCode |String |表示当 CDN 拒绝来自某个 IP 地址的请求时， CDN 的响应状态码。当前，该参数值只能为 `403`。 |`403` |
|MethodDeniedRule |Object |表示 "禁用 HTTP Method" 特性的配置。 | |
|Switch |Boolean |表示是否启用该特性。该参数有以下取值：<br><br><br>* `true`：表示启用该特性。<br><br>* `false`：表示禁用该特性。 |`true` |
|Methods |String |表示被禁用的一个或多个 HTTP 请求方法。多个方法使用逗号（,）分隔。该参数有以下取值：<br><br><br>* `get`：表示禁用 GET 请求方法。<br><br>* `post`：表示禁用 POST 请求方法。<br><br>* `delete`：表示禁用 DELETE 请求方法。<br><br>* `put`：表示禁用 PUT 请求方法。<br><br>* `head`：表示禁用 HEAD 请求方法。<br><br>* `patch`：表示 PATCH 请求方法。<br><br>* `connect`：表示 CONNECT 请求方法。<br><br>* `options`：表示 OPTIONS 请求方法。 |`delete,put` |
|NegativeCache |Object[] |表示 "状态码缓存" 特性的配置，包含一个规则列表，说明如下：<br><br><br>* 每条规则包含过匹配条件配置和操作配置。<br><br>* 规则在列表中出现的顺序表示规则的优先级。列表中第一条规则的优先级最高。<br><br>* 当收到一个用户请求时，CDN 按规则的优先级，从高到低将规则与请求匹配。如果一条规则匹配了请求，CDN 就停止处理其余规则。 | |
|NegativeCacheRule |Object |当一个请求满足 `Condition` 中的匹配条件时，CDN 会对请求文件执行指定的操作。该参数定义了该操作相关的配置。 | |
|Action |String |表示 CDN 执行的操作。当前该参数值只能是 `cache`，表示缓存源站的响应状态码。 |`cache` |
|StatusCode |String |表示一个需要缓存的状态码，范围是 `400-599`，可以是 `4xx` 或者 `5xx`。`4xx` 表示 400 到 499 之间的所有状态码。`5xx` 表示 500 到 599 之间的所有状态码。 |`404` |
|Ttl |Long |表示状态码的缓存时间。单位是`秒`。 |`100` |
|IgnoreCase |Boolean |表示 `Value` 是否是大小写敏感的。<br><br><br>* `true`：表示大小写不敏感。<br><br>* `false`：表示大小写敏感。 |`true` |
|Condition |Object |表示匹配条件的配置。如果请求匹配了某个条件，CDN 对该请求执行 `NegativeCacheRule` 中指定的操作。 | |
|ConditionRule |Object[] |表示匹配条件列表。 | |
|Object |String |表示匹配对象。该参数有以下取值：<br><br><br>* `filetype`：表示请求 URL 中的扩展名。<br><br>* `directory`：表示请求 URL 中的某个目录。<br><br>* `path`：表示请求 URL 中的完整路径。 |`directory` |
|Operator |String |表示匹配类型。该参数的值只能是 `match`，表示如果 `Value` 匹配了请求中的 `Object`，该请求就满足这个匹配条件。 |`match` |
|Type |String |该参数值只能是 `url`，表示 "请求 URL"。 |`url` |
|Value |String |表示一个或者多个匹配值。多个匹配值之间使用分号（;）分隔。 |`png` |
|OriginAccessRule |Object |表示 "Origin 黑白名单" 特性的配置。 | |
|AllowEmpty |Boolean |表示当用户请求不包含 Origin 头部时，CDN 处理请求的方式。该参数有以下取值：<br><br><br>* `true`：表示如果请求不包含 Origin 头部，则该请求被认为匹配配置的 Origin 列表。<br><br>* `false`：表示如果请求不包含 Origin 头部，则该请求被认为不匹配配置的 Origin 列表。 |`true` |
|IgnoreCase |Boolean |表示 Origin 列表是否是大小写敏感的。该参数有以下取值：<br><br><br>* `true`: 表示 Origin 列表是大小写不敏感的。<br><br>* `false`: 表示 Origin 列表是大小写敏感的。 |`true` |
|Origins |String[] |表示一个 Origin 列表。 |`["www.test.com"]` |
|RuleType |String |表示 Origin 列表的类型。该参数有以下取值：<br><br><br>* `allow`：表示白名单。<br><br>* `deny`：表示黑名单。 |`deny` |
|Switch |Boolean |表示是否启用该特性。该参数有以下取值：<br><br><br>* `true`：表示启用该特性。<br><br>* `false`：表示禁用该特性。 |`true` |
|OriginArg |Object[] |表示 "回源参数" 配置的规则列表。<br><br><br>* 每条规则包含一个匹配条件（`Condition`）和 CDN 执行操作（`OriginArgAction`）。<br><br>* 列表中规则的顺序定义了规则的优先级。列表中第一条规则的优先级最高。<br><br>* 当收到一个用户请求时，CDN 按规则的优先级，从高到低将规则与请求匹配。如果一条规则匹配了请求，CDN 就停止处理其余规则。 | |
|Condition |Object |表示匹配条件的配置。如果请求满足该匹配条件，CDN 执行 `OriginArgAction` 中指定的操作。 | |
|ConditionRule |Object[] |表示一个匹配条件的列表。 | |
|Object |String |表示匹配类型。该参数有以下取值：<br><br><br>* `filetype`：表示请求 URL 中的扩展名。<br><br>* `directory`：表示请求 URL 中的某个目录。<br><br>* `path`：表示请求 URL 中的完整路径。<br><br>* `regex`：表示请求 URL 中的完整路径，通过正则表达式匹配。 |`directory` |
|Operator |String |表示匹配类型。当前，该参数值只能是 `match`，表示只有匹配成功才算是满足了匹配条件。 |`match` |
|Type |String |该参数值只能是 `url`，表示 "请求 URL"。 |`url` |
|Value |String |表示一个或者多个匹配值。多个匹配值之间使用分号（;）分隔。 |`/` |
|OriginArgAction |Object |表示在请求满足 `Condition` 时 CDN 执行的操作。 | |
|OriginArgComponents |Object[] |表示一个操作列表。这些操作定义了 CDN 如何处理回源请求中的查询参数。 | |
|Action |String |表示 CDN 执行的操作。该参数有以下取值：<br><br><br>* `include`: 表示回源请求 URL 中包含用户请求 URL 中的全部查询参数。<br><br>* `exclude`：表示回源请求 URL 中不包含用户请求 URL 中的任何查询参数。<br><br>* `addPart`：表示回源请求 URL 中包含用户请求 URL 中的全部查询参数，并额外包含 `Subobject` 中指定的查询参数。<br><br>* `includePart`：表示如果用户请求 URL 中包含 `Subobject` 中指定的查询参数，那么回源请求 URL 中包含这些指定的查询参数。<br><br>* `excludePart`：表示回源请求 URL 中包含用户请求 URL 中的全部查询参数，除了`Subobject` 中指定的查询参数。<br><br>* `set`：表示回源请求 URL 中包含用户请求 URL 中的全部查询参数。同时，对于 `Subobject` 中指定的查询参数和参数值，CDN 会执行以下操作:<br><br>   * 如果这些查询参数在用户请求 URL 中，CDN 会在回源请求 URL 中将这些参数的值设置为指定的值。<br><br>   * 如果用户请求 URL 中不包含这些查询参数，CDN 会在回源请求 URL 中添加这些查询参数。 |`exclude` |
|Object |String |表示 CDN 对哪个对象执行 `Action`。当前，该参数值只能是 `queryString`，表示请求 URL 中的查询字符串。 |`queryString` |
|Subobject |String |表示一个或者多个查询参数。多个查询参数之间使用分号（;）分隔。<br><br>在匹配请求 URL 中的查询参数时，`Subobject` 中的参数是大小写敏感的。<br><br>如果 `Subobject` 是 `*`，则表示请求 URL 中的所有查询参数。 |`*` |
|OriginHost |String |如果源站服务器上有多个站点，该参数表示回源请求访问的站点域名。该参数对所有源站配置生效，但是优先级低于源站配置中 `OriginHost` 参数。 |`img.example.com` |
|OriginRange |Boolean |表示 "Range 回源" 特性的配置。该参数有以下取值：<br><br><br>* `true`：表示启用该特性。<br><br>* `false`：表示禁用该特性。 |`true` |
|OriginRewrite |Object |表示 "回源 URL 改写" 特性的配置。 | |
|OriginRewriteRule |Object[] |表示一个规则列表。<br><br><br>* 列表中规则的顺序定义了规则的优先级。列表中第一条规则的优先级最高。<br><br>* 当收到一个用户请求时，CDN 按规则的优先级，从高到低尝试将请求与规则匹配。如果请求匹配了一条规则，CDN 就停止处理其余规则。 | |
|OriginRewriteAction |Object |表示 CDN 执行的动作。 | |
|SourcePath |String |表示一个正则表达式，用于匹配用户请求 URL 中的路径。参见 [配置示例](https://docs.byteplus.com/en/docs/byteplus-cdn/docs_cn-origin-path-rewrite_1-cn#%E8%B7%AF%E5%BE%84%E6%94%B9%E5%86%99%E9%85%8D%E7%BD%AE%E7%A4%BA%E4%BE%8B)。 |`^/img/food.png$` |
|TargetPath |String |表示改写后的路径。参见 [配置示例](https://docs.byteplus.com/en/docs/byteplus-cdn/docs_cn-origin-path-rewrite_1-cn#%E8%B7%AF%E5%BE%84%E6%94%B9%E5%86%99%E9%85%8D%E7%BD%AE%E7%A4%BA%E4%BE%8B)。 |`/png/food.webp` |
|RewriteType |String |表示改写类型。该参数有以下取值：<br><br><br>* `rewrite_path`：表示对请求 URL 中的路径进行改写。<br><br>* `rewrite_url`：表示对请求 URL 中的路径和查询字符串进行改写。 |`rewrite_path` |
|Switch |Boolean |表示是否启用该特性。该参数有以下取值：<br><br><br>* `true`：表示启用该特性。<br><br>* `false`：表示禁用该特性。 |`true` |
|OriginSni |Object |表示 "回源 SNI" 特性的配置。 | |
|SniDomain |String |指定回源 SNI 的域名。 |`img.example.com` |
|Switch |Boolean |表示是否启用该特性。该参数有以下取值：<br><br><br>* `true`：表示启用该特性。<br><br>* `false`：表示禁用该特性。 |`true` |
|PageOptimization |Object |表示 "页面优化" 特性的配置。 | |
|OptimizationType |String[] |表示优化的对象。该参数有以下取值：<br><br><br>* `html`: 表示 HTML 页面。<br><br>* `js`: 表示 Javascript 代码。<br><br>* `css`: 表示 CSS 代码。 |`["html","js"]` |
|Switch |Boolean |表示是否启用该特性。该参数有以下取值：<br><br><br>* `true`：表示启用该特性。<br><br>* `false`：表示禁用该特性。 |`true` |
|Quic |Object |表示 QUIC 配置。 | |
|Switch |Boolean |表示是否为用户请求启用 QUIC。该参数有以下取值：<br><br><br>* `true`：表示启用 QUIC。<br><br>* `false`：表示禁用 QUIC。 |`true` |
|RedirectionRewrite |Object |表示 "URL 重定向改写" 特性的配置。 | |
|Switch |Boolean |表示是否启用该特性。该参数有以下取值：<br><br><br>* `true`：表示启用该特性。<br><br>* `false`：表示禁用该特性。 |`true` |
|RedirectionRule |Object[] |表示一个 URL 重定向改写的规则的列表。列表中第一条规则的优先级最高。<br><br>当收到一个用户请求时，CDN 按规则的优先级，从高到低将规则与请求匹配。如果一条规则匹配了请求，CDN 就停止处理其余规则。 | |
|RedirectionAction |Object |表示一个 URL 重定向改写的规则。 | |
|RedirectCode |String |表示 URL 重定向的响应状态码。该参数的取值有 `301`、`302`、`303`、`307`、`308`。<br><br>需要留意的是：<br><br><br>* 对于 301 和 302，如果原请求使用的方法不是 GET，那么客户端向新的URL发送请求时，新请求使用的方法可能变成 GET。<br><br>* 对于 303，新请求使用的方法是 GET。<br><br>* 对于 307 和 308，新请求使用的方法与原请求相同，不会被改变。 |`301` |
|SourcePath |String |表示文件的原路径。也就是请求中包含的路径。 |`/img/image.png` |
|TargetHost |String |表示目标路径所属的域名或者 IP 地址。 |`www.test.com` |
|TargetPath |String |表示跳转后的目标路径。 |`/png/image.png` |
|TargetProtocol |String |表示 URL重定向后的新请求所使用的协议。该参数有以下取值：<br><br><br>* `followclient`：表示使用原请求的协议。<br><br>* `http`：表示新请求强制使用 HTTP 协议。<br><br>* `https`：表示新请求强制使用 HTTPS 协议。 |`followclient` |
|TargetQueryComponents |Object |表示原请求 URL 中的查询参数的处理方式。 | |
|Action |String |表示原请求 URL 中的查询参数的处理方式。该参数有以下取值：<br><br><br>* `include`：表示在跳转后的 URL 中包含原请求 URL 中的所有查询参数。<br><br>* `exclude`：表示在跳转后的 URL 中不包含原请求 URL 中的任何查询参数。<br><br>* `includePart`：表示在跳转后的 URL 中包含原请求 URL 中特定的查询参数。<br><br>* `excludePart`：表示在跳转后的 URL 中不包含原请求 URL 中特定的查询参数。 |`include` |
|Value |String |表示要保留或删除的查询参数。多个查询参数间使用英文分号（;）分隔。如果 `Value` 是 `*`，表示所有的查询参数。 |`seq` |
|RefererAccessRule |Object |表示 "Referer 黑白名单" 特性的配置。关于不同配置对请求匹配结果的影响，参见 [配置示例](https://docs.byteplus.com/en/docs/byteplus-cdn/docs_cn-referer-restrictions-cn#%E9%85%8D%E7%BD%AE%E7%A4%BA%E4%BE%8B)。 | |
|AllowEmpty |Boolean |表示是否允许 Referer 头部为空（""）或者不包含 Referer 头部的请求。该参数有以下取值：<br><br><br>* `true`：表示允许。<br><br>* `false`：表示不允许。如果请求的 Referer 头部为空（""）或者不包含 Referer 头部，CDN 拒绝请求。 |`true` |
|Referers |String[] |表示一个 Referer 列表。Referers 也可以在 `ReferersType` 中指定。 |`["www.test.com","xxx.xx.x.x","xx.xx.xx.x/24"]` |
|ReferersType |Object |表示一个 `ReferersType` 对象。其包含一个 `CommonType` 对象和一个 `RegularType` 对象，分别表示一个常规 Referer 列表和一个用于匹配 Referer 的正则表达式列表。`CommonType` 和 `RegularType` 可以同时存在。 | |
|CommonType |Object |表示一个 `CommonType` 对象，其包含一个常规 Referer 列表。 | |
|IgnoreCase |Boolean |表示 `CommonType` 下的 `Referers` 列表是否是大小写敏感的。该参数有以下取值：<br><br><br>* `true`: 表示大小写不敏感。<br><br>* `false`: 表示大小写敏感。 |`true` |
|Referers |String[] |表示一个常规 Referer 列表。 |`["www.test.com","xxx.xxx.xx.xxx","1xx.xx.xx.x/24"]` |
|IgnoreScheme |Boolean |表示 CDN 是否对 Referer 中的 scheme 进行校验，也就是校验 Referer 是否包含 `http://` 或者 `https://`。该参数有以下取值：<br><br><br>* `true`: 表示 CDN 不校验 Referer 是否包含 scheme。在这个情况下，无论 Referer 是否包含 scheme，CDN 都会将 Referer 与配置的名单进行匹配校验。<br><br>* `false`: 表示 CDN 会先校验 Referer 是否包含 scheme。只有 Referer 包含 scheme，CDN 才会将 Referer 与配置的名单进行匹配校验。否则，CDN 判定请求与配置的名单不匹配。<br><br><br>该配置对 `RegularType` 下的正则表达式列表不生效，因为 CDN 依赖正则表达式来判断 Referer 是否匹配正则名单。 |`false` |
|RegularType |Object |表示一个 `RegularType` 对象，其包含一个正则表达式列表用来匹配请求中的 Referer 头部。 | |
|Referers |String[] |表示一个用于匹配 Referer 的正则表达式列表。 |`^http://a.com` |
|RuleType |String |表示 Referer 名单的类型。该参数有以下取值：<br><br><br>* `allow`：表示白名单。<br><br>* `deny`：表示黑名单。 |`deny` |
|Switch |Boolean |表示是否启用该特性。该参数有以下取值：<br><br><br>* `true`：表示启用该特性。<br><br>* `false`：表示禁用该特性。 |`true` |
|SharedConfig |Object |表示一个全局配置。 | |
|ConfigName |String |表示一个全局配置的名称。该全局配置的 `ConfigType` 必须是 `deny_referer_access_rule` 或者 `allow_referer_access_rule`。<br><br><br>* `deny_referer_access_rule`：表示 Referer 黑名单。<br><br>* `allow_referer_access_rule`：表示 Referer 白名单。<br><br><br>您可以调用 [ListSharedConfig](https://docs.byteplus.com/en/docs/byteplus-cdn/ListSharedConfig_cn) 获取全局配置的列表。 |`my_allowlist` |
|RemoteAuth |Object |表示 "远程鉴权" 特性的配置。 | |
|Switch |Boolean |表示是否启用该特性。该参数有以下取值：<br><br><br>* `true`：表示启用该特性。<br><br>* `false`：表示禁用该特性。 |`true` |
|RemoteAuthRules |Object[] |表示一个鉴权规则的列表。每条规则包含匹配条件配置和鉴权配置。 | |
|Condition |Object |表示匹配条件的配置。如果一个请求满足匹配条件，CDN 对该请求执行 `RemoteAuthRuleAction` 中指定的操作。 | |
|ConditionRule |Object[] |表示匹配条件列表。<br><br>这些匹配条件之间的关系是 "或"，表示如果一个请求满足任意匹配条件，CDN 就对该请求执行 `RemoteAuthRuleAction` 中指定的操作。 | |
|Object |String |表示匹配对象。该参数有以下取值：<br><br><br>* `filetype`：表示请求 URL 中的扩展名。<br><br>* `directory`：表示请求 URL 中的某个目录。<br><br>* `path`：表示请求 URL 中的完整路径。 |`filetype` |
|Operator |String |表示匹配类型。该参数有以下取值：<br><br><br>* `match`：表示如果 `Value` 匹配了请求中的 `Object`，该请求就满足这个匹配条件。<br><br>* `not_match`：表示如果 `Value` 不匹配请求中的 `Object`，该请求就满足这个匹配条件。 |`match` |
|Type |String |该参数值只能是 `url`，表示 "请求 URL"。 |`url` |
|Value |String |表示一个或者多个匹配值，多个匹配值之间使用分号（;）分隔。 |`png;jpg` |
|RemoteAuthRuleAction |Object |表示鉴权相关的配置。<br><br>当一个请求满足 `Condition` 中的匹配条件时，CDN 会将其发送至鉴权服务器进行鉴权，并基于鉴权的结果接受或者拒绝该请求。 | |
|AuthModeConfig |Object |表示鉴权服务器的配置。 | |
|MasterRemoteAddr |String |表示鉴权服务器的主地址。 |`https://primary.example.com` |
|PathType |String |表示鉴权请求的路径。鉴权地址和请求路径组成了完整的鉴权 URL。CDN 会把用户的请求转发到该鉴权 URL。该参数有以下取值：<br><br><br>* `constant`：表示鉴权请求中的路径与用户请求中的路径相同。<br><br>* `variable`：表示 `pathValue` 中指定的路径。 |`constant` |
|RequestMethod |String |表示在发送鉴权请求时，CDN 所使用的请求方法。该参数有以下取值：<br><br><br>* `default`：表示鉴权请求所使用的方法与用户的请求相同。<br><br>* `get`：表示鉴权请求使用 GET 方法。<br><br>* `post`：表示鉴权请求使用 POST方法。<br><br>* `head`：表示鉴权请求使用 HEAD 方法。 |`get` |
|BackupRemoteAddr |String |表示鉴权服务器的备地址。 |`https://secondary.example.com` |
|PathValue |String |表示一个鉴权请求的路径。 |`/auth` |
|AuthResponseConfig |Object |CDN 需要对鉴权服务器返回的鉴权状态码进行处理。该参数表示相关的配置。 | |
|CacheAction |Object |CDN 可以缓存鉴权状态码。该参数表示相关的配置。 | |
|Action |String |表示 CDN 是否缓存鉴权状态码。该参数有以下取值：<br><br><br>* `nocache`：表示 CDN 不缓存鉴权状态码。<br><br>* `cache`：CDN 缓存鉴权状态码。 |`nocache` |
|Ttl |Long |表示鉴权状态码的缓存时间，单位是秒。 |`5` |
|CacheKey |String[] |缓存 key 指定了用于区分不同请求 URI 的查询参数。每个参数都必须以 `$` 开头。参见 [变量字段说明](https://docs.byteplus.com/en/docs/byteplus-cdn/docs_cn-remote-authentication_1-cn#variables)中的参数。 |`[$URI,$host]` |
|ResponseAction |Object |表示鉴权失败时，CDN 如何响应用户。 | |
|StatusCode |String |表示鉴权失败时，CDN 响应用户的状态码。 |`403` |
|StatusCodeAction |Object |表示 CDN 对鉴权状态码的处理方式。 | |
|DefaultAction |String |表示如果鉴权状态码既不是 `FailCode`，又不是 `SuccessCode` 时，CDN 处理鉴权请求的方式。该参数有以下取值：<br><br><br>* `reject`：表示 CDN 认为鉴权失败。<br><br>* `pass`：表示 CDN 认为鉴权成功。 |`pass` |
|FailCode |String |表示鉴权失败时的鉴权状态码。多个状态码使用英文分号（;）分隔。 |`403` |
|SuccessCode |String |表示鉴权成功时的鉴权状态码。多个状态码使用英文分号（;）分隔。 |`200` |
|TimeOutAction |Object |表示鉴权超时后，CDN 如何处理鉴权请求。 | |
|Action |String |表示鉴权超时后，CDN 处理鉴权请求的策略。该参数有以下取值：<br><br><br>* `reject`：表示 CDN 认为鉴权失败。<br><br>* `pass`：表示 CDN 认为鉴权成功。 |`reject` |
|Time |Long |表示鉴权超时的时间，单位是毫秒。 |`200` |
|QueryStringRules |Object |表示鉴权请求的参数设置。 | |
|QueryStringComponents |Object |表示鉴权请求参数的设置策略。 | |
|Action |String |表示鉴权请求是否包含用户请求 URL 中的查询参数。该参数有以下取值：<br><br><br>* `exclude`：表示鉴权请求不包含任何查询参数。<br><br>* `include`：表示鉴权请求包含所有查询参数。<br><br>* `includePart`：表示鉴权请求包含指定的查询参数。 |`exclude` |
|Value |String |表示 `Action` 参数所对应的参数值。`*` 表示所有查询参数。 |`*` |
|QueryStringInstances |Object[] |表示鉴权请求中额外的参数设置。 | |
|Action |String |表示如何设置鉴权请求参数。当前参数值只能是 `set`。`set` 表示设置参数。`Key` 指定了需要设置的鉴权请求参数。<br><br><br>* 如果指定的鉴权请求参数不存在，CDN 会在鉴权请求中添加该参数。<br><br>* 如果指定的鉴权请求参数已存在，CDN 会使用 `Value` 的值作为该鉴权请求参数的值。 |`set` |
|Key |String |表示需要设置的鉴权请求参数。 |`sign` |
|Value |String |表示鉴权请求参数的值，区分大小写。 |`1235565` |
|ValueType |String |表示 `Key` 指定的鉴权请求参数的类型。`ValueType` 有以下取值：<br><br><br>* `constant`：表示鉴权请求参数是一个常量。<br><br>* `variable`：表示鉴权请求参数的值来自一个变量。参见 `Value` 的说明。<br><br>* `customize`：表示鉴权请求参数的值是一个变量与固定字符串拼接后的字符串。 |`variable` |
|RequestHeaderRules |Object |表示鉴权请求头的设置。 | |
|RequestHeaderComponents |Object |表示鉴权请求头的设置策略。 | |
|Action |String |表示鉴权请求头是否包含用户请求头。该参数有以下取值：<br><br><br>* `exclude`：表示鉴权请求头中不包含任何用户请求头。<br><br>* `include`：表示鉴权请求头中包含所有用户请求头。<br><br>* `includePart`：表示鉴权请求头包含指定的用户请求头。 |`exclude` |
|Value |String |表示 `Action` 参数所对应的参数值。如果参数值是 `*`，表示所有请求头。 |`*` |
|RequestHeaderInstances |Object[] |表示一组鉴权请求头的设置。<br><br>需要留意的是，在 CDN 发起鉴权请求时，请求中可能已经包含了以下头部：<br><br><br>* `X-Forwarded-Protocol`，`X-Forwarded-Proto`，`X-Client-Scheme`：这三个头部都表示用户请求所使用协议，没有区别。<br><br>* `X-Real-IP`：表示用户真实的 IP 地址。该头部的值不会受代理服务器的影响。<br><br>* `X-Forwarded-For`：表示用户的 IP 地址。如果用户的请求经过了代理服务器，该头部的值会变成代理服务器的 IP 地址。 | |
|Action |String |表示如何设置鉴权请求头。当前该参数值只能为 `set`，表示设置请求头。`Key` 指定了需要设置的请求头。<br><br><br>* 如果设置的请求头不存在，CDN 会在鉴权请求中添加该请求头。<br><br>* 如果设置的请求头已存在，CDN 会使用 `Value` 的值作为该请求头的值。 |`set` |
|Key |String |表示需要设置的请求头。 |`x-test-header` |
|ValueType |String |表示请求头的类型。该参数有以下取值：<br><br><br>* `constant`：表示请求头的值是一个常量。<br><br>* `variable`：表示请求头的值来自一个变量。<br><br>* `customize`：表示请求头的值是一个变量与固定字符串拼接后的字符串。 |`variable` |
|Value |String |表示请求头的值。 |`1234fdf` |
|RequestHost |String |表示鉴权请求中 HOST 头部的值。该参数的默认值是 `default`，表示 HOST 头部的值与域名相同。 |`www.example.com` |
|RequestHeader |Object[] |表示 "回源 HTTP 请求头" 特性的配置。 | |
|RequestHeaderAction |Object |表示一个请求头的配置规则列表。每个规则都包含一个头部的相关操作设置。 | |
|RequestHeaderInstances |Object[] |表示一个请求头的配置规则列表。每个规则都包含一个头部的相关操作设置。 | |
|Action |String |表示对请求头的操作。该参数有以下取值：<br><br><br>* `set`：表示设置一个头部。设置操作包括添加与修改。如果请求中已包含该头部，该头部的值会被覆盖。如果请求中没有包含该头部，该头部会被添加。<br><br>* `delete`，表示删除一个头部。 |`set` |
|Key |String |表示一个头部的名称，不区分大小写。 |`Cdn-provider` |
|ValueType |String |表示 `Key` 的取值类型。该参数仅当 `Action` 是 `set` 的时候才有效。该参数有以下取值：<br><br><br>* `constant`：表示 `Key` 的值是一个固定字符串。<br><br>* `variable`：表示 `Key` 的值来自一个变量。<br><br>* `customize`：表示 `Key` 的值是变量与固定字符串拼接后的一个字符串。 |`constant` |
|Value |String |表示 `Key` 的值。 |`bp-cdn` |
|ResponseHeader |Object[] |表示 "HTTP 响应头" 特性的配置。 | |
|ResponseHeaderAction |Object |表示 CDN 在响应用户请求的时候，对响应头的操作。 | |
|ResponseHeaderInstances |Object[] |表示一个响应头的配置规则列表。每个规则都包含一个头部的相关操作设置。 | |
|Action |String |表示对响应头的操作。该参数有以下取值：<br><br><br>* `set`：表示设置一个头部。设置操作包括添加与修改。如果源站响应中已包含该头部，该头部的值会被覆盖。如果源站响应中没有包含该头部，该头部会被添加。<br><br>* `delete`，表示删除一个头部。 |`set` |
|Key |String |表示一个头部的名称。 |`Content-Disposition` |
|ValueType |String |表示 `Key` 的取值类型。该参数仅当 `Action` 是 `set` 的时候才有效。该参数有以下取值：<br><br><br>* `constant`：表示 `Key` 的值是一个字符串。<br><br>* `variable`：表示 `Key` 的值来自一个变量。<br><br>* `customize`：表示 `Key` 的值是一个变量与字符串拼接后的字符串。 |`constant` |
|AccessOriginControl |Boolean |表示在 CDN 响应用户请求时，是否校验请求中的 Origin 头部。<br><br>该参数有以下取值：<br><br><br>* `true`：表示 CDN 会校验 Origin 头部。如果校验成功，CDN 会在响应中包含 Access\-Control\-Allow\-Origin 头部。头部值与 Origin 头部值相同。如果校验失败，响应中不会包含 Access\-Control\-Allow\-Origin 头部。<br><br>* `false`：表示 CDN 不会校验 Origin 头部。在响应中，CDN 会包含 Access\-Control\-Allow\-Origin 头部。头部值是设置的 Access\-Control\-Allow\-Origin 的内容。<br><br><br>该参数仅在以下条件都满足的情况下有效：<br><br><br>* `Action` 是 `set`。<br><br>* `Key` 是 `Access-Control-Allow-Origin`。<br><br>* `ValueType` 是 `constant`。 | |
|Value |String |表示 `Key` 的值。 |`attachment;filename=FileName.xls` |
|ServiceRegion |String |表示域名的服务区域。该参数有以下取值：<br><br><br>* `chinese_mainland`：表示中国内地。<br><br>* `global`：表示全球。<br><br>* `outside_chinese_mainland`：表示全球（不含中国内地）。 |`outside_chinese_mainland` |
|SignedUrlAuth |Object |表示 "URL 鉴权" 特性的配置。 | |
|Switch |Boolean |表示是否启用该特性。该参数有以下取值：<br><br><br>* `true`：表示启用该特性。<br><br>* `false`：表示禁用该特性。 |`true` |
|SignedUrlAuthRules |Object[] |表示一个规则列表。每条规则包含匹配条件配置和鉴权配置。 | |
|Condition |Object |表示匹配条件的配置。CDN 对符合条件的用户请求进行鉴权。 | |
|ConditionRule |Object[] |表示一个匹配条件列表。 | |
|Object |String |表示匹配条件中的匹配类型。该参数有以下取值：<br><br><br>* `filetype`：表示 URL 路径末尾的扩展名。<br><br>* `directory`：表示 URL 路径中的一个目录。<br><br>* `path`：表示完整的 URL 路径。<br><br>* `regex`: 表示完整的 URL 路径，通过正则表达式匹配。 |`directory` |
|Operator |String |表示匹配条件中的匹配方式。该参数有以下取值：<br><br><br>* `match`：表示如果 `object` 匹配 `Value`，该请求就满足了这个匹配条件。<br><br>* `not_match`：表示如果 `object` 不匹配 `Value`，该请求就满足了这个匹配条件。 |`match` |
|Type |String |表示匹配对象。当前该参数值必须是 `url`，表示 URL 请求链接。 |`url` |
|Value |String |表示匹配条件中的匹配值。 |`png;jpg` |
|Connective |String |表示多个 `ConditionRule` 之间的逻辑关系。该参数有以下取值：<br><br><br>* `AND`: 表示逻辑关系是 "AND"。<br><br>* `OR`：表示逻辑关系是 "OR"。 |`OR` |
|SignedUrlAuthAction |Object |表示签名计算的配置。 | |
|Duration |Long |表示签名的有效时间，单位是秒。该参数与请求中包含时间戳搭配使用，用来计算签名的过期时间。签名的过期时间 = 时间戳 + `Duration`。在 CDN 收到某个请求时，如果签名的过期时间小于当前时间，CDN 判定签名已过期。 |`1000` |
|MasterSecretKey |String |表示主密钥。 |`abcdefg` |
|URLAuthType |String |签名类型。该参数有以下取值：`typea`、`typeb`、`typec`、`typed`、`typee`，每种类型得鉴权说明见 [配置 URL 鉴权](https://docs.byteplus.com/en/docs/byteplus-cdn/docs_cn-overview-cn) 。 |`typea` |
|BackupSecretKey |String |表示备密钥。 |`abcdefg` |
|CustomVariableRules |Object |表示自定义签算变量。 | |
|CustomVariableInstances |Object[] |表示一个变量列表。 | |
|Operator |String |表示变量的匹配方式。该参数的取值只能是 `match`。 |`match` |
|Type |String |表示变量的类型。该参数有以下取值：<br><br><br>* `queryString`：表示该变量是请求中的一个查询参数。<br><br>* `requestHeader`：表示该变量是请求中的一个头部字段。 |`queryString` |
|Value |String |表示变量的名称。 |`myparam1` |
|KeepOriginArg |Boolean |表示 CDN 是否在回源请求中包含用户请求中的签名参数。<br><br>该参数有以下取值：<br><br><br>* `true`：表示 CDN 在回源请求中包含签名参数。<br><br>* `false`：表示 CDN 在回源请求中不包含签名参数。 |`true` |
|RewriteM3u8 |Boolean |对于 HLS Manifest (.m3u8) 的请求，该参数表示 CDN 是否要修改 Manifest，从而为每个视频分片生成签名并将签名添加到 URI 中。<br><br>该参数有以下取值：<br><br><br>* `true`：表示需要修改 Manifest。<br><br>* `false`：表示不需要修改 Manifest。 |`true` |
|SignName |String |表示签名参数的名称。 |`sign` |
|SignatureRule |String[] |当 `URLAuthType` 为 `typee` 时，该参数有效，表示需要纳入签名计算的字段。必须纳入签名计算的字段如下：<br><br><br>* `key`：表示`MasterSecretKey`或 `BackupSecretKey` 指定的密钥。<br><br>* `uri`：表示用户请求的 URI，仅包含字路径和查询参数。<br><br>* `TimeName`：表示 `TimeFormat` 指定的时间戳。<br><br><br>可选择纳入签名计算的字段如下：<br><br><br>* `domain`：表示域名。<br><br>* `referer`：表示用户请求携带的 referer 值。<br><br>* `ua`：表示用户请求携带的 User\-Agent 值。<br><br>* `ip`：表示用户请求的客户端 IP。<br><br>* `origin`：表示用户请求携带的 Origin 值。<br><br>* 自定义变量：表示您在 `CustomVariableInstances` 中定义的变量的值。<br><br><br>CDN 按列表中字段的顺序将这些字段拼接成一个字符串，然后计算该字符串的 MD5 值。该 MD5 值就是签名。 |`["domain","ip","key","TimeName","uri"]` |
|TimeFormat |String |表示 `TimeName` 使用的时间格式。该参数有以下取值：<br><br><br>* `basicFormat2m`：格式为 YYYYMMDDHHMM。<br><br>* `decimal`：十进制时间戳。<br><br>* `heximal`：十六进制时间戳。 |`heximal` |
|TimeName |String |表示时间戳参数的名称。 |`TimeParam` |
|RewriteM3u8Rule |Object |表示 "M3U8 改写" 功能的配置。 | |
|DeleteParam |Boolean |表示在改写分片 URL 时是否保留 URL 中原有的参数。该参数有以下取值：<br><br><br>* `true`：表示删除原有参数。<br><br>* `false`：表示保留原有参数。<br><br><br>需要留意的是，该参数的设置影响签名的计算。 |`true` |
|KeepM3u8Param |Boolean |表示是否将来自该 M3U8 文件请求的不表示签名的查询参数添加到分片 URL 中。该参数有以下取值：<br><br><br>* `true`：表示在分片 URL 中添加查询参数。<br><br>* `false`：表示不添加查询参数。<br><br><br>需要留意的是，该参数的设置影响签名的计算。 |`true` |
|RewriteTag |Object |表示 "标签改写" 的配置，定义了除了 `EXTINF` 以外的标签。 | |
|Switch |Boolean |表示是否需要改写额外标签中的分片 URL。该参数有以下取值：<br><br><br>* `true`: 表示需要改写额外标签。<br><br>* `false`：表示无额外标签需要改写。 |`true` |
|Tags |String[] |表示除默认标签外，需要对其下分片 URI 进行改写的额外标签列表。<br><br>列表中最多包含 20 个标签，每个标签的长度为 1\-100 个字符，不能包含 `#` 和 `:`。 |`["EXT-X-MAP", "My-TAG"]` |
|AuthAlgorithm |String |表示签名计算使用的算法。该配置有以下取值：<br><br><br>* `md5`：表示 MD5 算法。<br><br>* `sha256`：表示 SHA\-256 算法。<br><br><br>该参数的默认值是 `md5`。 |`md5` |
|DeleteAuthCacheAndOrigin |Boolean |表示 CDN 是否在回源请求和缓存键中包含用户请求中的签名参数。<br><br>该参数有以下取值：<br><br><br>* `true`：表示回源请求和缓存键中均不包含签名参数。<br><br>* `false`：表示回源请求和缓存键中均包含签名参数。 |`true` |
|AuthRulesF |Object[] |表示 Type\-F 配置，包含一个规则列表。列表中第一条规则的优先级最高。<br><br>当收到一个用户请求时，CDN 按规则的优先级，从高到低将规则与请求匹配。如果一条规则匹配了请求，CDN 就停止处理其余规则。 |`false` |
|RuleName |String |表示规则列表中一条规则的名称。 |`Authentication rule A` |
|Condition |Object |表示匹配条件的配置。如果一个请求符合匹配条件，CDN 对该请求进行 URL 鉴权。 | |
|ConditionRule |Object[] |表示一个匹配条件列表。 | |
|Object |String |表示匹配对象。该参数有以下取值：<br><br><br>* `filetype`：表示请求文件的扩展名。<br><br>* `directory`：表示请求路径中的某个目录。<br><br>* `path`：表示请求的完整路径，不包含查询字符串。<br><br>* `regex`：表示用于匹配完整路径的正则表达式。 |`directory` |
|Operator |String |表示匹配操作符。该参数有以下取值：<br><br><br>* `match`：表示如果 `Value` 匹配了请求中的 `Object`，则该请求符合这个匹配条件。<br><br>* `not_match`：表示如果 `Value` 不匹配请求中的 `Object`，该请求就符合这个匹配条件。 |`match` |
|Type |String |表示匹配对象的来源。当前，该参数值只能是 `url`，表示请求 URL。 |`url` |
|Value |String |表示一个或者多个匹配值。多个匹配值之间使用分号（;）分隔。 |`/chs/foods/;/us/birds/` |
|Connective |String |表示匹配条件之间的关系。该参数有以下取值：<br><br><br>* `OR`：表示关系是 "或"。<br><br>* `AND`：表示关系是 "和"。 |`OR` |
|SecretKey |Object |表示用于计算令牌的密钥。包含一个主密钥和一个备密钥。 | |
|MasterSecretKey |String |表示主密钥。 |`primary-key-123` |
|BackupSecretKey |String |表示备密钥。 |`secondary-key-456` |
|SignCapRule |Object |表示从用户请求中获取令牌的方式。 | |
|ArgSegment |Object |表示基于 `ParamName` 或者 `UriLevel` 获取的内容是否需要被拆分，以提取某个层级的片段。该层级的片段才是需要获取的令牌。 | |
|Switch |Boolean |表示获取到的内容是否需要被拆分。该参数有以下取值：<br><br><br>* `true`：表示内容需要被拆分。<br><br>* `false`：表示内容无需被拆分。 |`true` |
|Level |Long |表示将内容拆分为多个层级的片段后，令牌所在的层级。<br><br>如果层级是负整数，表示从最右边的片段开始向左计数。 |`2` |
|SplitSymbol |String |表示用于拆分内容的分隔符。 |`//` |
|CapMode |String |表示令牌的来源。该参数有以下取值：<br><br><br>* `name`：表示查询参数。相关配置在 `ParamName` 中指定。<br><br>* `uri`：表示请求路径中的一个目录。相关配置在 `UriLevel` 中指定。<br><br>* `header`：表示请求中的一个头部。相关配置在 `CustomValue` 中指定。<br><br>* `cookie`：表示请求中的一个 cookie。相关配置在 `CustomValue` 中指定。 |`name` |
|CustomValue |String |该参数的含义如下：<br><br><br>* 当 `CapMode` 是 `header` 时，该参数表示指定的请求头。<br><br>* 当 `CapMode` 是 `cookie` 时，该参数表示指定的 cookie 的 key，CDN 会获取该 cookie 的 value。 |`myheader` |
|ParamName |String |当 `CapMode` 是 `name` 时，该参数表示要指定的查询参数。 |`myparam` |
|UriLevel |Long |当 `CapMode` 是 `uri` 时，该参数表示指定的目录层级。<br><br>如果层级是负整数，表示从路径最右边的目录开始向左计数。 |`3` |
|ExpireTimeRule |Object |表示令牌过期时间的相关设置。 | |
|Duration |Long |表示令牌的有效时长（TTL），单位是秒。<br><br><br>* 令牌过期时间 = 基于 `ExpTimeCapRule` 获取的令牌时间戳 + `Duration` |`20` |
|ExpTimeCapRule |Object |表示令牌时间戳的获取方式。令牌时间戳是一个 Unix 时间戳。 | |
|CapMode |String |表示令牌时间戳的来源。该参数有以下取值：<br><br><br>* `name`：表示查询参数。相关配置在 `ParamName` 和 `ArgSegment` 中指定。<br><br>* `uri`：表示请求路径中的一个目录。相关配置在 `UriLevel` 和 `ArgSegment` 中指定。<br><br>* `header`：表示请求中的一个头部。相关配置在 `CustomValue` 中指定。<br><br>* `cookie`：表示请求中的一个 cookie。相关配置在 `CustomValue` 中指定。 |`header` |
|ParamName |String |当 `ParamType` 是 `ReqHeader` 时，该参数表示指定的查询参数。 |`myparm1` |
|UriLevel |Long |当 `ParamType` 是 `uri` 时，该参数表示指定的目录层级。<br><br>如果层级是负整数，表示从路径最右边的目录开始向左计数。 |`2` |
|ArgSegment |Object |表示基于 `ParamName` 或者 `UriLevel` 获取的内容是否需要被拆分，以提取某个层级的片段。该层级的片段才是需要获取的令牌时间戳。 | |
|Switch |Boolean |表示获取到的内容是否需要被拆分。该参数有以下取值：<br><br><br>* `true`：表示内容需要被拆分。<br><br>* `false`：表示内容无需被拆分。 |`true` |
|Level |Long |表示将内容拆分为多个层级的片段后，令牌时间戳所在的层级。<br><br>如果层级是负整数，表示从最右边的片段开始向左计数。 |`2` |
|SplitSymbol |String |表示用于拆分内容的分隔符。 |`-` |
|CustomValue |String |该参数的含义如下：<br><br><br>* 当 `CapMode` 是 `header` 时，该参数表示指定的请求头。<br><br>* 当 `CapMode` 是 `cookie` 时，该参数表示指定的 cookie 的 key，CDN 会获取该 cookie 的 value。 |`myheader1` |
|TimeFormat |String |表示令牌时间戳的格式。<br><br><br>* `octal`：表示八进制。例如 `14751410031`。<br><br>* `decimal`：表示十进制。例如 `1738936345`。<br><br>* `heximal`：表示十六进制。例如 `67a61019`。 |`heximal` |
|AuthTokenCalRule |Object |表示令牌计算的设置。<br><br>CDN 使用 `SignJoinSymbol` 将 `SignParam` 中的各对象进行拼接，然后对拼接后的对象应用 `ParamCalRules` 中指定的算法计算令牌，用于与用户请求中包含的令牌进行比较。 | |
|ParamCalRules |String[] |表示计算令牌所使用的算法列表。CDN 按列表中算法的出现顺序生成令牌的计算公式。<br><br>该参数有以下取值：`md5_bin`、`base64url`、`sha256`、`md5`、`base64_encode`、`sha1`、`sha224`、`sha384`、`sha512`、`sha3_224`、`sha3_256`、`sha3_384`、`sha3_512`、`upper_case`、`lower_case`。 |`["sha1"、"md5_bin"、"base64url"]` |
|SignJoinSymbol |String |表示拼接 `SignParam` 中各对象而使用的拼接符。 |`00` |
|SignParam |Object[] |表示 CDN 在计算令牌时使用的对象列表。每个对象由 `ParamType` 和相关配置组成。例如，以下示例表示对象是一个字符串，字符串的值是 `str-for-token-calc`。<br><br>```json```<br>```{```<br>```    "ParamType": "SupString",```<br>```    "SupContent": "str-for-token-calc"```<br>```}```<br> | |
|ParamType |String |表示对象的类型。该参数有以下取值：<br><br><br>* `SecretKey`：表示 `SecretKey` 结构体中的 `MasterSecretKey` 或者 `BackupSecretKey`。当鉴权失败时，CDN 会使用 `BackupSecretKey` 计算令牌，重新对用户请求进行鉴权。<br><br>* `SupString`：表示一个字符串。相关配置在 `SupContent` 中指定。<br><br>* `URI`：表示请求路径中的连续片段。路径不包含查询字符串。相关配置在 `UriParamSup` 与 `ParamSource` 中指定。<br><br>* `URLParam`：表示请求 URL 中的某类对象。对象可以是一个查询参数或者某个目录。相关配置在 `UriParam` 与 `ParamSource` 中指定。<br><br>* `ClientDomain`：表示请求域名。<br><br>* `Referer`：表示用户请求中 Referer 头部的值。<br><br>* `Origin`：表示用户请求中 Origin 头部的值。<br><br>* `ClientIP`：表示发送用户请求的客户端 IP 地址。<br><br>* `UA`：表示用户请求中 Use\-Agent 头部的值。<br><br>* `ReqHeader`：表示用户请求中某个头部的值。相关配置在 `RequestHeader` 中指定。<br><br>* `Cookie`：表示请求中的一个 cookie。相关配置在 `CookieToken` 中指定。<br><br>* `FullURI`：表示请求的完整路径，不包含查询字符串。相关配置在 `ParamSource` 中指定。 |`URI` |
|CookieToken |String |当 `ParamType` 是 `Cookie` 时，该参数表示指定的 cookie 的 key。CDN 会获取该 cookie 的 value。 |`mycookiekey` |
|RequestHeader |String |当 `ParamType` 是 `ReqHeader` 时，该参数表示指定的请求头。 |`myheader2` |
|SupContent |String |当 `ParamType` 是 `SupString` 时，该参数表示指定的字符串。 |`123abc` |
|UriParamSup |Object |表示从请求路径中获取连续片段的方式。<br><br>该参数是一个结构体，包含以下配置：<br><br><br>* 拆分请求路径所使用的分隔符。<br><br>* 所需连续路径片段的开始层级和结束层级。<br><br>* 拼接这些路径片段所使用的拼接符。拼接后的路径片段用于计算令牌。 | |
|SplitSymbol |String |表示拆分请求路径所使用的分隔符。 |`-` |
|StartLevel |Long |表示起始片段所在的层级。 |`2` |
|TermLevel |Long |表示结束片段所在的层级。<br><br>如果 `TermLevel` 是负整数，表示从最右边的片段开始向左计数。 |`3` |
|JoinSymbol |String |表示拼接这些路径片段所使用的拼接符。 |`00` |
|UrlParam |Object |表示从 URL 中获取所需对象的方式。<br><br>该参数是一个结构体，包含对象的来源以及相关配置。 | |
|CapMode |String |表示对象的来源。该参数有以下取值：<br><br><br>* `name`：表示查询参数。相关配置在 `ParamName` 和 `ArgSegment` 中指定。<br><br>* `uri`：表示请求路径中指定的目录。相关配置在 `UriLevel` 和 `ArgSegment` 中指定。 |`uri` |
|ParamName |String |当 `ParamType` 是 `name` 时，该参数表示指定的查询参数。 |`myparam3` |
|UriLevel |Long |当 `ParamType` 是 `uri` 时，该参数表示指定的目录层级。<br><br>如果层级是负整数，表示从最右边的目录开始向左计数。 |`2` |
|ArgSegment |Object |表示基于 `ParamName` 或者 `UriLevel` 获取的内容是否需要被拆分，以提取某个层级的片段。该片段才是需要获取的对象。 | |
|Switch |Boolean |表示获取到的内容是否需要被拆分。该参数有以下取值：<br><br><br>* `true`：表示内容需要被拆分。<br><br>* `false`：表示内容无需被拆分。 |`true` |
|Level |Long |表示将获取到的内容拆分为多个层级的片段后，所需对象所在的层级。<br><br>如果层级是负整数，表示从最右边层级的片段开始向左计数。 |`2` |
|SplitSymbol |String |表示用于拆分内容而使用的分隔符。 |`-` |
|ParamSource |String |对于添加到 Manifest 中的令牌，该参数表示 CDN 在使用该对象计算令牌时，该对象的来源。<br><br>该参数有以下取值：<br><br><br>* `ParentLink`：表示该对象来自用户请求中的 URL。<br><br>* `ChildLink`：表示该对象来自 Manifest 中视频分片的 URI。 |`ParentLink` |
|RewriteM3U8 |Object |表示 HLS Manifest 改写的配置，也就是配置如何在 Manifest 中的视频分片 URI 中添加令牌。 | |
|Switch |Boolean |表示是否需要改写 HLS Manifest。该参数有以下取值：<br><br><br>* `true`：表示需要改写 Manifest。<br><br>* `false`：表示无需改写 Manifest。<br><br><br>默认情况下，CDN 仅对 Manifest 中 `EXTINF` 标签下的视频分片 URI 添加令牌。 |`true` |
|RewriteM3U8Tag |Object |表示额外的标签。对于 `Tags` 中包含的标签，CDN 会将令牌添加到这些标签下的 URL 中。参见 [该设置的示例](https://docs.byteplus.com/en/docs/byteplus-cdn/typef_zh-cn#m3u8-%E9%A2%9D%E5%A4%96%E6%A0%87%E7%AD%BE%E7%9A%84%E6%94%B9%E5%86%99%E7%A4%BA%E4%BE%8B)。 | |
|Switch |Boolean |表示是否需要设置额外的标签。该参数有以下取值：<br><br><br>* `true`：表示需要设置额外的标签。<br><br>* `false`：表示无需设置额外的标签。 |`true` |
|Tags |String[] |表示额外标签的列表。 |`["tag1","tag2","tag3"]` |
|RewriteMPD |Object |表示 DASH Manifest 改写的配置，也就是配置如何在 Manifest 中的视频分片 URI 中添加令牌。 | |
|Switch |Boolean |表示是否需要改写 DASH Manifest。该参数有以下取值：<br><br><br>* `true`：表示需要改写 Manifest。<br><br>* `false`：表示无需改写 Manifest。 |`true` |
|MpdVarExpand |Boolean |表示是否要将 `SegmentTemplate` 下 URI 中的变量替换为实际值。该参数有以下取值：<br><br><br>* `true`：表示启用该配置。该配置启用后，CDN 会先将视频分片 URI 中的变量替换为实际值，然后基于包含实际值的 URI 生成令牌，最后将令牌添加到 URI 中。<br><br>* `false`：表示不启用该配置。变量名本身会作为固定字符串用于生成令牌。<br><br><br>该配置启用后，当前只有满足以下所有条件的变量才会被替换为实际值：<br><br><br>* 变量为 `$RepresentationID$`。<br><br>* `SegmentTemplate` 下存在至少一个 URI 符合以下条件：<br><br>   * 在该 URI 中，至少有一个 `$RepresentationID$` 出现的位置不是 URI 路径中的最后一段。<br><br>* `<SegmentTemplate ... />` 和 `<Representation .../>` 之间不能出现其他内容。<br><br><br>另外，在改写后的 DASH Manifest 中，原始的 `SegmentTemplate` 会被保留。<br><br>参见 [示例](https://docs.byteplus.com/en/docs/byteplus-cdn/typef_zh-cn#dash-mpd-%E5%8F%98%E9%87%8F%E6%89%A9%E5%B1%95-%E7%A4%BA%E4%BE%8B)。 |`true` |
|CustomRewrite |Object |表示视频 Manifest 的扩展改写配置。该配置启用后，CDN 使用 [特殊改写逻辑](https://docs.byteplus.com/en/docs/byteplus-cdn/typef_zh-cn#%E8%A7%86%E9%A2%91-manifest-%E7%9A%84%E7%89%B9%E6%AE%8A%E6%94%B9%E5%86%99%E9%80%BB%E8%BE%91) 覆盖 [默认改写逻辑](https://docs.byteplus.com/en/docs/byteplus-cdn/typef_zh-cn#%E8%A7%86%E9%A2%91-manifest-%E7%9A%84%E9%BB%98%E8%AE%A4%E6%94%B9%E5%86%99%E9%80%BB%E8%BE%91)。 | |
|Switch |Boolean |表示是否启用扩展改写配置。该参数有以下取值：<br><br><br>* `true`：表示启用扩展改写配置。<br><br>* `false`：表示不启用扩展改写配置。 |`true` |
|RewriteParam |Object[] |表示一个对象列表。CDN 将这些对象拼接而生成令牌，添加到视频分片的 URL 中。 | |
|ParamType |String |表示对象的类型。该参数有以下取值：<br><br><br>* `ParentLinkUrlParam`：表示用户请求 URL 中的某类对象。对象可以是一个查询参数或者某个层级的路径目录。相关配置在 `ParentLinkUrlParam` 结构体中指定。<br><br>* `SupString`：表示一个字符串。相关配置在 `SupContent` 中指定。<br><br>* `ParentLinkURI`：表示用户请求路径中的连续片段。路径不包含查询字符串。相关配置在 `ParentLinkUriParamSup` 中指定。<br><br>* `ParentLinkExpire`：表示用户请求中令牌的时间戳。参见 `ExpireTimeRule` 下 `Duration` 参数的说明。<br><br>* `AuthToken`：表示基于 `AuthTokenCalRule` 计算的令牌。<br><br>* `ParentFullURI`：表示用户请求的完整路径，不包含查询字符串。 |`ParentLinkURI` |
|SupContent |String |当 `ParamType` 是 `SupString` 时，该参数表示指定的字符串。 |`abc-13343` |
|ParentLinkUriParamSup |Object |表示从用户请求路径中获取对象的方式。<br><br>该参数是一个结构体，包含以下配置：<br><br><br>* 拆分请求路径所使用的分隔符。<br><br>* 连续路径片段的开始层级和结束层级。<br><br>* 拼接这些路径片段所使用的拼接符。拼接后的路径片段用于生成令牌。 | |
|SplitSymbol |String |表示拆分请求路径所使用的分隔符，要求与 `JoinSymbol` 相同。 |`-` |
|StartLevel |Long |表示起始片段所在的层级。 |`1` |
|TermLevel |Long |表示结束片段所在的层级，要求如下：<br><br><br>* 只能是非 0 的整数。<br><br>* 绝对值不能大于层级总数。<br><br><br>如果 `TermLevel` 是负整数，表示从最右边的片段开始向左计数。 |`3` |
|JoinSymbol |String |表示拼接这些路径片段所使用的拼接符。 |`00` |
|ParentLinkUrlParam |Object |表示从 URL 中获取对象的方式。<br><br>该参数是一个结构体，包含对象的来源以及相关配置。 | |
|CapMode |String |表示对象的来源。该参数有以下取值：<br><br><br>* `name`：表示查询参数。相关配置在 `ParamName` 和 `ArgSegment` 中指定。<br><br>* `uri`：表示请求路径中指定的目录。相关配置在 `UriLevel` 和 `ArgSegment` 中指定。 |`name` |
|ParamName |String |当 `CapMode` 是 `name` 时，该参数表示指定的查询参数。 |`myparam5` |
|UriLevel |Long |当 `CapMode` 是 `uri` 时，该参数表示指定的目录层级。<br><br>如果层级是负整数，表示从最右边的目录开始向左计数。 |`4` |
|ArgSegment |Object |表示基于 `ParamName` 或者 `UriLevel` 获取的内容是否需要被拆分，以提取某个层级的片段。该片段才是需要获取的对象。 | |
|Switch |Boolean |表示获取的内容是否需要被拆分。该参数有以下取值：<br><br><br>* `true`：表示内容需要被拆分。<br><br>* `false`：表示内容无需被拆分。 |`true` |
|Level |Long |表示将获取的内容拆分为多个层级的片段后，需要的片段所在的层级。<br><br>如果层级是负整数，表示从最右边的片段开始向左计数。 |`2` |
|SplitSymbol |String |表示用于拆分内容的分隔符。 |`-` |
|RewriteRule |Object |表示 CDN 在视频分片 URI 中添加令牌的方式。 | |
|CapMode |String |表示 CDN 如何在视频分片 URI 中添加生成的令牌。该参数有以下取值：<br><br><br>* `name`：表示将 URI 中指定的查询参数设置为令牌。相关配置在 `ParamName` 中指定。<br><br>* `uri`：表示在 URI 中指定的目录层级插入一个目录，并将该目录设置为令牌。相关配置在 `UriLevel` 中指定。 |`name` |
|ParamName |String |当 `CapMode` 是 `name` 时，表示指定的查询参数。 |`myparam4` |
|UriLevel |Long |当 `CapMode` 是 `uri` 时，表示指定的目录层级。<br><br>如果层级是负整数，表示从最右边层级的目录开始向左计数。 |`2` |
|SignJoinSymbol |String |表示拼接 `RewriteParam` 中各对象而使用的拼接符。 |`00` |
|ArgumentRule |Object |表示回源参数相关的配置。 | |
|KeepOriginArg |Boolean |表示是否在回源请求中包含基于 `AuthTokenCalRule` 计算的令牌。该参数有以下取值：<br><br><br>* `true`：表示在回源请求中包含令牌。回源请求中令牌出现的位置与 `SignCapRule` 中的设置相同。<br><br>* `false`：表示不在回源请求中包含令牌。 |`true` |
|GeneralParamRule |Object |表示 CDN 设置视频分片 URI 中查询参数的方式。 | |
|ParentLinkParamInherit |String |表示改写后的视频分片 URI 是否包含用户请求 URL 中除表示令牌和令牌时间戳的参数之外的所有查询参数。该参数有以下取值：<br><br><br>* `not_inherit`：表示改写后的分片 URI 不会包含这些查询参数。<br><br>* `inherit`：表示改写后的分片 URI 会包含这些查询参数。 |`not_inherit` |
|SubLinkParamRule |Object |该结构体包含额外的查询参数设置。该结构体包含额外的查询参数设置。 | |
|InheritMode |String |表示当视频分片 URI 和用户请求 URL 中存在相同的查询参数时，CDN 如何设置视频分片 URI 中该参数的值。<br><br>该参数有以下取值：<br><br><br>* `sub_link_first`：表示使用视频分片 URI 中该参数的值。<br><br>* `inherit_first`：表示使用用户请求 URL 中该参数的值。 |`inherit_first` |
|KeepSubLinkArg |String |表示改写后的视频分片 URI 是否保留 URI 中原有的查询参数。该参数有以下取值：<br><br><br>* `delete`：表示改写后的分片 URI 不会保留这些查询参数。<br><br>* `keep`：表示改写后的分片 URI 会保留这些查询参数。 |`delete` |
|RewriteFormat |String |表示改写后的视频分片 URI 格式。该参数有以下取值：<br><br><br>* `default`：该参数值的含义与 `absolute` 相同。<br><br>* `relative`：保持 URI 的当前格式。<br><br>* `absolute`：如果 URI 的格式是相对路径，CDN 将格式转换成绝对路径。如果 URI 是绝对路径或者完整 URL，则保持当前格式。<br><br>* `full`：如果 URI 的格式是绝对路径或者相对路径，CDN 将格式转换成完整 URL。 |`default` |
|Timeout |Object |表示 "回源请求超时" 特性的配置。 | |
|Switch |Boolean |表示是否启用该特性。该参数有以下取值：<br><br><br>* `true`：表示启用该特性。<br><br>* `false`：表示禁用该特性。此时，TCP 请求和 HTTP 请求的超时时间使用默认值，分别是 2 秒和 60 秒。 |`true` |
|TimeoutRules |Object[] |表示一组超时时间的配置。 | |
|TimeoutAction |Object |表示超时时间的配置。 | |
|HttpTimeout |Long |表示 CDN 节点收到源站返回的首个响应字节后，持续未收到后续响应正文数据的最长等待时间，单位是秒。 |`60` |
|TcpTimeout |Long |表示 CDN 节点向源站建立 TCP 连接的最长等待时间，单位是秒。 |`2` |
|HttpFirstByteTimeout |Long |表示 CDN 节点向源站发送 HTTP 请求后，等待源站返回首个响应字节的最长时间，单位是秒。 |`90` |
|UaAccessRule |Object |表示 "UA 黑白名单" 特性的配置。 | |
|AllowEmpty |Boolean |表示是否允许 User\-Agent 头部为空（""）或者不包含 User\-Agent 头部的请求。该参数有以下取值：<br><br><br>* `true`：表示允许。<br><br>* `false`：表示不允许。如果请求的 User\-Agent 头部为空（""）或者不包含 User\-Agent 头部，CDN 拒绝请求。 |`true` |
|IgnoreCase |Boolean |表示 UA 字符串是否是大小写敏感的。该参数有以下取值：<br><br><br>* `true`: 表示 UA 字符串是大小写不敏感的。<br><br>* `false`: 表示 UA 字符串是大小写敏感的。 |`true` |
|RuleType |String |表示 UA 名单的类型。当 `Switch` 是 `true` 时，该参数为必填。该参数有以下取值：<br><br><br>* `allow`：表示白名单。<br><br>* `deny`：表示黑名单。 |`deny` |
|Switch |Boolean |表示是否启用该特性。该参数有以下取值：<br><br><br>* `true`：表示启用该特性。<br><br>* `false`：表示禁用该特性。 |`true` |
|UserAgent |String[] |表示一个 UA 的列表。该参数的说明如下：<br><br><br>* 如果 `RuleType` 是 `allow`，表示仅允许包含列表中的 UA 的请求访问域名。<br><br>* 如果 `RuleType` 是 `deny`，表示如果访问请求包含列表中的 UA，则不允许访问域名。<br><br><br>UA 中的 `*` 表示一个或者多个字符。 |`["*curl*","*Mozilla*"]` |
|VideoDrag |Object |表示 "视频拖拽" 特性的配置。 | |
|Switch |Boolean |表示是否启用该特性。该参数有以下取值：<br><br><br>* `true`：表示启用该特性。<br><br>* `false`：表示禁用该特性。 |`true` |
|OriginIPv6 |String |表示 "IPv6 回源" 的配置。该参数有以下取值：<br><br><br>* `ipv6_first`：表示 CDN 始终尝试获取源站域名的 IPv6 地址。如果无法获取该 IP 地址，CDN 才尝试获取源站域名的 IPv4 地址。<br><br>* `ipv4_first`：表示 CDN 始终尝试获取源站域名的 IPv4 地址。如果无法获取该 IP 地址，CDN 才尝试获取源站域名的 IPv6 地址。<br><br>* `followclient`：表示 CDN 尝试获取与用户请求相同类型的 IP 地址。<br><br><br>由于海外部分 CDN 回源节点不支持向 IPv6 地址发送回源请求，该功能仅适用于位于中国内地的回源节点。 |`followclient` |
|UrlNormalize |Object |表示 "URL 标准化" 特性的配置。 | |
|NormalizeObject |String[] |表示一个 URL 标准化选项列表。当 `Switch` 为 `true` 时，该参数为必填。列表中可以包含以下选项：<br><br><br>* `dot_segments`：表示将请求 URL 中的以下内容进行替换：<br><br>   * `/./`：替换为单个斜杠（/）。<br><br>   * `/../`：如果 `/../` 前还有一个级别的目录，则删除 `/../` 与该目录。如果 `/../` 前没有目录，则保留原 URL。<br><br>* `back_slashes`：表示将请求 URL 中的反斜杠（\）替换为单个斜杠（/）。<br><br>* `successive_slashes`：表示将请求 URL 中连续斜杠（//）替换为单个斜杠（/）。 |`["dot_segments","back_slashes","successive_slashes"]` |
|Switch |Boolean |表示是否启用该特性。该参数有以下取值：<br><br><br>* `true`：表示启用该特性。<br><br>* `false`：表示禁用该特性。 |`true` |
|RequestBlockRule |Object |表示 "自定义拦截" 特性的配置。 | |
|BlockRule |Object[] |表示一个规则列表。列表中第一条规则的优先级最高。<br><br>当收到一个用户请求时，CDN 按规则的优先级，从高到低将规则与请求匹配。如果一条规则匹配了请求，CDN 就停止处理其余规则。 | |
|BlockAction |Object |表示一条规则中 CDN 行为的配置。 | |
|Action |String |表示 CDN 如何处理匹配 `Condition` 的请求。该参数有以下取值：<br><br><br>* `refuse`：表示 CDN 拒绝请求并响应一个 4xx 的错误码。错误码在 `StatusCode` 中指定。<br><br>* `redirect`：表示 CDN 将请求重定向到 `RedirectUrl` 中指定的 URL。 |`refuse` |
|StatusCode |String |表示对于匹配 `Condition` 的用户请求，CDN 的响应状态码。<br><br><br>* 当 `Action` 是 `refuse` 时，该参数表示一个 400\-499 范围内的错误码。<br><br>* 当 `Action` 是 `redirect` 时，该参数有以下取值：<br><br>   * `301`：表示响应状态码是 301。<br><br>   * `302`：表示响应状态码是 302。 |`403` |
|ErrorPage |String |* 当 `Action` 是 `refuse` 时，该参数是可选的，说明如下：<br><br>   * 如果指定该参数，该参数表示 "全局配置" 特性中的一个自定义响应页面的名称。也就是说，当 CDN 拒绝请求时，返回该自定义页面。<br><br>   * 如果不指定该参数，表示 CDN 使用 `StatusCode` 中指定错误码的标准响应正文。 |`GlobalConfigName` |
|RedirectUrl |String |* 当 `Action` 是 `redirect` 时，表示重定向 URL。<br><br>* 当 `Action` 是 `refuse` 时，该参数无效。 |`http://www.example.com` |
|Condition |Object |表示该规则中匹配条件的定义。 | |
|ConditionRule |Object[] |表示一个匹配条件列表，用于匹配请求 URL 中的路径和查询参数、以及请求来自的客户端 IP 地址。每个匹配条件包含匹配类型、对比类型和匹配值。 | |
|Object |String |表示一个匹配类型。<br><br><br>* 当 `Type` 是 `url` 时，该参数有以下取值：<br><br>   * `path`：表示表示请求 URL 中的路径。<br><br>   * `directory`：表示路径中的一个目录。<br><br>   * `filetype`：表示路径末尾的扩展名。<br><br>   * `regex`：表示请求 URL 中的路径，通过正则表达式匹配。<br><br>* 当 `Type` 是 `querystring` 时，该参数有以下取值：<br><br>   * `query_name`：表示请求 URL 中的一个查询参数。<br><br>   * `full_querystring`：表示请求 URL 中的查询字符串。<br><br>* 当 `Type` 是 `client_ip` 时，该参数有以下取值：<br><br>   * `client_ip`：表示客户端的 IP 地址。<br><br>* 当 `Type` 是 `request_header` 时，该参数有以下取值：<br><br>   * `ua`：表示请求中 User\-Agent 头部。<br><br>   * `customize`：表示请求中的自定义头部。 |`filetype` |
|Operator |String |表示一个对比类型。<br><br><br>* 当 `Object` 是 `path`、`directory`、`filetype` 时，该参数有以下取值：<br><br>   * `equal`：表示如果匹配 `Value` 中的任何值，该请求就满足这个匹配条件。<br><br>   * `not_equal`：表示如果不匹配 `Value` 中的所有值，该请求才满足这个匹配条件。<br><br>* 当 `Object` 是 `query_name` 时，该参数有以下取值：<br><br>   * `exist`：表示存在。匹配逻辑与 `equal` 相同。<br><br>   * `not_exist`：表示不存在。匹配逻辑与 `not_equal` 相同。<br><br>   * `belong_shared_config`：表示如果匹配 `Value` 表示的全局配置中所包含的任何值，该请求就满足这个匹配条件。<br><br>   * `not_belong_shared_config`：表示如果不匹配 `Value` 表示的全局配置中的所有值，该请求才满足这个匹配条件。<br><br>   * `empty`：表示值为空。<br><br>   * `not_empty`：表示值不为空。<br><br>   * `equal`：参见以上描述。<br><br>   * `not_equal`：参见以上描述。<br><br>* 当 `Object` 是 `regex`、`full_querystring`、`client_ip` 或 `ua` 时，该参数有以下取值：<br><br>   * `match`：描述与 `equal` 相同。<br><br>   * `not_match`：描述与 `not_equal` 相同。<br><br>* 当 `Object` 是 `ua` 或 `customize` 时，该参数还有以下**额外**取值：<br><br>   * `empty`：参见以上描述。<br><br>   * `not_empty`：参见以上描述。 |`not_equal` |
|Type |String |表示一个匹配对象的类型。该参数有以下取值：<br><br><br>* `url`：表示请求 URL。<br><br>* `querystring`：表示请求 URL 中的查询字符串。<br><br>* `request_header`：表示请求中的头部。 |`url` |
|Value |String |表示一个或者多个匹配值。<br><br><br>* 如果 `Type` 是 `request_header`，多个匹配值之间使用竖线（\|）分隔。<br><br>* 如果 `Type` 不是 `request_header`，多个匹配值之间使用分号（;）分隔。 |`png;txt` |
|Name |String |当 `Object` 是 `query_name` 或者 `customize` 时，该参数有效。<br><br><br>* 如果 `Object` 是 `query_name`，该参数表示一个查询参数的名称。<br><br>* 如果 `Object` 是 `customize`，该参数表示一个自定义请求头的名称。 |`color` |
|Connective |String |表示多条 `ConditionRule` 之间的关系。该参数有以下取值：<br><br><br>* `AND`：表示 "和"。<br><br>* `OR`：表示 "或"。 |`AND` |
|RuleName |String |表示规则的名称。 |`MyRule` |
|Switch |Boolean |表示是否启用该特性。该参数有以下取值：<br><br><br>* `true`：表示启用该特性。<br><br>* `false`：表示禁用该特性。 |`true` |
|OriginCertCheck |Object |表示 "源站证书校验" 特性的配置。<br><br>该特性启用后，CDN 会校验源站证书的合法性，包括证书是否已被吊销、证书是否由可信 CA 签发、证书与源站域名是否匹配等。CDN 内置了常见可信 CA 的根证书。如果源站证书未通过校验，CDN 进行 [回源重试](https://docs.byteplus.com/en/docs/byteplus-cdn/origin_retry-cn)。如果回源重试时源站证书依然未通过校验，CDN 判定无法从该源站获取文件，并对用户请求响应 504 状态码。 | |
|Switch |Boolean |表示是否启用该特性。该参数有以下取值：<br><br><br>* `true`：表示启用该特性。<br><br>* `false`：表示禁用该特性。 |`true` |
|CertInfoList |Object[] |表示一个 CA 证书列表，列表中的 CA 证书托管在 CDN。CDN 使用该列表中的 CA 证书对来自源站的服务器证书进行校验。 | |
|CertId |String |表示列表中一本 CA 证书的 ID，以 `cert_hosting` 开头。 |`cert_hosting-104663` |
|ConditionalOrigin |Object |表示 "条件源站" 特性的配置。 | |
|OriginRules |Object[] |表示一个规则列表。列表中的每条规则中定义了一组匹配条件以及 CDN 对满足匹配条件的请求所执行的操作。<br><br>当收到一个用户请求时，CDN 按规则的优先级，从高到低将规则与请求匹配。如果一条规则匹配了请求，CDN 就停止处理其余规则。 | |
|Actions |Object |表示一条规则中定义的操作配置。 | |
|OriginLines |Object[] |表示一个源站列表。 | |
|Address |String |表示一个源站的地址。<br><br><br>* 当 `InstanceType` 是 `ip` 时，`Address` 表示一个 IPv4 或者 IPv6 地址。<br><br>* 当 `InstanceType` 是 `domain` 时，`Address` 表示一个域名。<br><br>* 当 `InstanceType` 是 `storage` 时，`Address` 表示存储桶域名，可以是云厂商分配的桶域名，也可以是您在云厂商处为存储桶设置的自定义域名。 |`203.0.113.8` |
|HttpPort |String |表示 CDN 使用 HTTP 协议访问该源站时所使用的端口。 |`80` |
|HttpsPort |String |表示 CDN 使用 HTTPS 协议访问该源站时所使用的端口。 |`443` |
|InstanceType |String |表示源站的类型。该参数有以下取值：<br><br><br>* `ip`：表示 IP 地址。<br><br>* `domain`：表示域名。<br><br>* `storage`：表示对象存储桶。 |`ip` |
|OriginHost |String |表示回源请求访问的站点域名，适用于源站服务器上有多个站点的情况。<br><br>该参数的优先级高于全局 `OriginHost` 参数。 |`img.example.com` |
|BucketSource |String |表示存储桶使用的是哪个对象存储服务所提供的鉴权方式。该参数有以下取值：<br><br><br>* `tos`：表示 BytePlus TOS。<br><br>* `cos`：表示腾讯云 COS。<br><br>* `oss`：表示阿里云 OSS。<br><br>* `aws_common`：表示 AWS S3 或者其他使用兼容 S3 鉴权方式的第三方对象存储服务。<br><br>* `azure`：表示 Microsoft Azure。 |`aws_common` |
|PrivateBucketAccess |Boolean |表示存储桶是否是私有桶。该参数仅当 `InstanceType` 为 `storage` 时有效。该参数有以下取值：<br><br><br>* `true`：表示该存储桶是私有桶。<br><br>* `false`：表示该存储桶不是私有桶。 |`true` |
|TosAuthInformation |Object |表示存储桶的访问凭证（AccessKey）。 | |
|AccessKeyId |String |表示访问凭证中的 AccessKey ID，在腾讯云称为 SecretId。 |`xxxxxxxxxxxxxxxxx` |
|AccessKeySecret |String |表示访问凭证中的 AccessKey Secret，在腾讯云称为 SecretKey。 |`xxxxxx` |
|Region |String |表示存储桶所在地域的信息，也就是存储桶的 region code。Region code 参与签名的计算。 |`us-east-1` |
|AccountName |String |表示您 Azure 存储账号的共享密钥（Key）。该参数仅当 `BucketSource` 为 `azure` 时有效。 |`xxxxxxxxxxx` |
|OriginType |String |表示源站的类别。该参数有以下取值：<br><br><br>* `primary`：表示主源站。<br><br>* `backup`：表示备源站。 |`primary` |
|Weight |String |表示该源站的权重，取值范围是 1\-100，默认值是 `1`。权重越大，该源站在 CDN 发送回源请求时被选择到的概率也越大。 |`1` |
|Condition |Object |表示该规则中匹配条件的配置。 | |
|ConditionGroups |Object[] |表示一个匹配条件列表。 | |
|Condition |Object |表示一个匹配条件的配置。 | |
|Object |String |表示一个匹配对象。该参数有以下取值：<br><br><br>* `path`：表示请求 URL 中的完整路径。<br><br>* `directory`：表示请求 URL 中的某个目录。<br><br>* `filetype`：表示请求 URL 中的扩展名。<br><br>* `full_querystring`：表示请求 URL 中的所有查询参数。<br><br>* `client_ip`：表示客户端的 IP 地址。<br><br>* `query_name`：表示请求 URL 中的而某个查询参数。<br><br>* `customize`：表示用户请求中的某个头部。 |`path` |
|Operator |String |表示匹配类型。 |`equal` |
|Value |String[] |表示一个或者多个匹配值。 |`/www/img/my*image.png;/doc` |
|Name |String |* 当 `Object` 为 `query_name` 时，该参数表示指定的查询参数的名称。<br><br>* 当 `Object` 为 `customize` 时，该参数表示指定的请求头的名称。<br><br>* 当 `Object` 为其他值时，该参数无效。 |`myparam` |
|Type |String |* 当 `Object` 为 `query_name` 时，该参数值必须是 `querystring`。<br><br>* 当 `Object` 为 `customize` 时，该参数值必须是 `request_header`。<br><br>* 当 `Object` 为其他值时，该参数无效。 |`request_header` |
|Connective |String |表示这些匹配条件之间的关系。该参数有以下取值：<br><br><br>* `or`：表示关系是 "或"。<br><br>* `and`：表示关系是 "与"。 |`and` |
|IsGroup |Boolean |该参数值是 `true`。 |`true` |
|Switch |Boolean |表示该特性是否已启用。该参数有以下取值：<br><br><br>* `true`：表示该特性已启用。<br><br>* `false`：表示该特性未启用。 |`true` |
|OriginRetry |Object |表示 "回源重试设置" 特性的配置模块。 | |
|StatusCode |String |表示范围在 400\-599 之间的一个或者多个状态码。多个状态码之间使用分号（;）分隔。您可以输入 `4xx` 或者 5xx，表示所有以数字 4 或 数字 5 开头的状态码。 |`404;408;5xx` |
|Switch |Boolean |表示是否启用该特性。该参数有以下取值：<br><br><br>* `true`：表示启用该特性。<br><br>* `false`：表示禁用该特性。<br><br><br>该参数的默认值是 `false`。 |`false` |
|Websocket |Object |表示 Websocket 配置。 | |
|Switch |Boolean |表示是否为用户请求启用 WebSocket 支持。该参数有以下取值：<br><br><br>* `true`：表示启用 WebSocket。该配置启用后，CDN 可以响应来自客户端的 Websocket 请求。<br><br>* `false`：表示禁用 WebSocket。 |`true` |
|Timeout |Long |表示 Websocket 连接的超时时间，单位是秒。 |`60` |
|MultiRange |Object |表示 "多重范围（Multi\-range)" 特性的配置。 | |
|Switch |Boolean |表示是否启用该特性。该参数有以下取值：<br><br><br>* `true`：表示启用该特性。该特性启用后，CDN 允许指定了多重范围的 Range 请求。<br><br>* `false`：表示不启用该特性。如果收到一个指定了多重范围的 Range 请求，CDN 会拒绝该请求并返回 416 响应状态码。 |`true` |
|OfflineCache |Object |表示 "离线缓存" 特性的配置。 | |
|Object |String |表示该特性的触发条件，该参数有以下取值：<br><br><br>* `request_error`：表示回源请求异常。当回源请求出现异常时，CDN 没有获得源站的响应。<br><br>* `error_code`：表示源站响应状态码是 5xx。<br><br>* `request_error,error_code`：表示以上两个条件都包含。 |`request_error,error_code` |
|StatusCode |String |表示一个或者多个响应状态码，范围是 500\-599。多个状态码之间使用分号（;）分隔。`5xx` 表示任意以数字 5 开头的状态码。<br><br>当 `Object` 是 `error_code` 或者 `request_error,error_code` 时，该参数才有效。 |`504;505` |
|Switch |Boolean |表示是否启用该特性。该参数有以下取值：<br><br><br>* `true`：表示启用该特性。<br><br>* `false`：表示禁用该特性。 |`true` |
|OriginResponseHeader |Object[] |表示 "源站响应头设置" 的配置模块。要使用该特性，请 [提交工单](https://console.byteplus.com/workorder/create)。 | |
|OriginResponseHeaderAction |Object |表示 CDN 在收到源站响应时，对响应头的操作。 | |
|OriginResponseHeaderInstances |Object[] |表示一个响应头的配置规则列表。每个规则都包含一个头部的相关操作设置。您最多可以添加 50 条规则。 | |
|Action |String |表示 CDN 对响应头的操作。该参数有以下取值：<br><br><br>* `set`：表示设置一个头部。设置操作包括添加与修改。如果源站响应中已包含该头部，该头部的值会被覆盖。如果源站响应中没有包含该头部，该头部会被添加。<br><br>* `delete`：表示删除一个头部。 |`set` |
|Key |String |表示一个头部的名称。 |`MyHeader` |
|Value |String |表示 `Key` 的值。 |`hello` |
|ValueType |String |表示 `Key` 的取值类型。该参数仅当 `Action` 是 `set` 的时候才有效。如果 `Action` 不是 `set`，该参数无效。该参数有以下取值：<br><br><br>* `constant`：表示 `Key` 的值是一个固定字符串。<br><br>* `variable`：表示 `Key` 的值来自一个变量。<br><br>* `customize`：表示 `Key` 的值是一个变量与固定字符串拼接后的字符串。 |`constant` |
|Object |String |表示该规则对哪些用户请求生效。该参数有以下取值：<br><br><br>* `default`：表示该规则仅对源站响应中包含以下响应码的用户请求生效：<br><br>   * 200、201、204、206、301、302、303、304、307、308<br><br>* `all_request`：表示该规则对所有用户请求生效。<br><br><br>该参数的默认值是 `default`。另外，当 `Action` 是 `delete` 时，该参数的值只能是 `all_request`。 |`default` |
|Cname |String |表示 CDN 为该域名分配的 CNAME。 |`www.example.com.bplslb.com` |
|CreateTime |Long |表示该域名的创建时间，格式是 Unix 时间戳。 |`1636612244` |
|Project |String |表示该域名归属的项目。 |`default` |
|Status |String |表示该域名的状态。该参数有以下取值：<br><br><br>* `online`：表示状态是 正常运行。<br><br>* `configuring`：表示状态是 配置中。<br><br>* `offline`：表示状态是 已下线。 |`offline` |
|UpdateTime |Long |表示该域名配置的最近更新时间，格式是 Unix 时间戳。如果该域名配置在创建后未被更新，该参数值与 `CreateTime` 的值相同。 |`1639621409` |
|ResourceTags |Object[] |表示该域名的标签。 | |
|Key |String |表示一个标签的 Key。 |`key1` |
|Value |String |表示该标签的 Value。 |`value1` |
|ProxyProtocol |Object |表示 PROXY Protocol 的配置。 | |
|Switch |Boolean |表示是否已启用 PROXY Protocol 支持。该参数有以下取值：<br><br><br>* `true`：表示已启用 PROXY Protocol。CDN 对收到的 PROXY 协议头进行解析，以获取客户端的真实 IP 地址。<br><br>* `false`：表示已禁用 PROXY Protocol。 |`true` |
|Range |Object |表示 Range GET 请求中分片大小的设置。 | |
|RangeSize |Long |表示分片的大小。 |`512` |
|Switch |Boolean |表示是否启用了该设置。该参数有以下取值：<br><br><br>* `true`：表示该设置已启用。<br><br>* `false`：表示该设置已禁用。 |`true` |
|Unit |String |表示 `RangeSize` 的单位。该参数有以下取值：<br><br><br>* `KB`<br><br>* `MB` |`KB` |
|ServerSentEvent |Object |表示 SSE 的设置。 | |
|Switch |Boolean |表示是否启用了该设置。该参数有以下取值：<br><br><br>* `true`：表示该设置已启用。<br><br>* `false`：表示该设置已禁用。 |`true` |
|HTMLToMarkdown |Object |表示 "HTML 转 Markdown" 特性的配置。 | |
|Switch |Boolean |表示是否启用该特性。该参数有以下取值：<br><br><br>* `true`：表示启用该特性。<br><br>* `false`：表示禁用该特性。无 |`true` |
|OriginPreconnect |Object |表示 "源站预建连" 特性的配置。 | |
|Switch |Boolean |表示是否启用该特性。该参数有以下取值：<br><br><br>* `true`：表示启用该特性。<br><br>* `false`：表示禁用该特性。 |`true` |
|SmartOriginRouting |Object |表示 "智能路由" 特性的配置。 | |
|Switch |Boolean |表示是否启用该特性。该参数有以下取值：<br><br><br>* `true`：表示启用该特性。<br><br>* `false`：表示禁用该特性。 |`true` |
|AccessOptimise |Object |中国大陆访问优化配置 | |
|AccOptimiseCname |String |无 | |
|Switch |Boolean |无 | |
|VideoPreview |Object |视频试看 | |
|Switch |Boolean |视频试看开关 | |
|PreviewParam |String |试看时长参数 | |


<span id="示例"></span>
## 示例

<span id="请求示例"></span>
### 请求示例

```json
POST https://cdn.byteplusapi.com/?Action=DescribeCdnConfig&Version=2021-03-01
{
    "Domain": "test111.example.com"
}
```


<span id="返回示例"></span>
### 返回示例

```json
{
    "ResponseMetadata": {
        "RequestId": "202508160551554488555F346DC5A960D4",
        "Action": "DescribeCdnConfig",
        "Version": "2021-03-01",
        "Service": "CDN",
        "Region": "ap-singapore-1"
    },
    "Result": {
        "DomainConfig": {
            "AreaAccessRule": {
                "Area": [
                    "CHN",
                    "HKG",
                    "MAC",
                    "TWN",
                    "CHE"
                ],
                "RuleType": "allow",
                "Switch": true
            },
            "ProxyProtocol": {
                "Switch": true
            },
            "BrowserCache": [
                {
                    "CacheAction": {
                        "Action": "cache",
                        "DefaultPolicy": "cache",
                        "IgnoreCase": true,
                        "Ttl": 216000
                    },
                    "Condition": {
                        "ConditionRule": [
                            {
                                "Object": "filetype",
                                "Operator": "match",
                                "Type": "url",
                                "Value": "jpg;png"
                            }
                        ],
                        "Connective": "OR"
                    }
                },
                {
                    "CacheAction": {
                        "Action": "cache",
                        "DefaultPolicy": "origin_first",
                        "IgnoreCase": false,
                        "Ttl": 0
                    },
                    "Condition": {
                        "ConditionRule": [
                            {
                                "Object": "directory",
                                "Operator": "match",
                                "Type": "url",
                                "Value": "/docs/foods/;/dogs/ragdolls/"
                            }
                        ],
                        "Connective": "OR"
                    }
                },
                {
                    "CacheAction": {
                        "Action": "cache",
                        "DefaultPolicy": "no_cache",
                        "IgnoreCase": false,
                        "Ttl": 0
                    },
                    "Condition": {
                        "ConditionRule": [
                            {
                                "Object": "path",
                                "Operator": "match",
                                "Type": "url",
                                "Value": "/docs/file1;/docs/file2"
                            }
                        ],
                        "Connective": "OR"
                    }
                },
                {
                    "CacheAction": {
                        "Action": "cache",
                        "DefaultPolicy": "cache",
                        "IgnoreCase": false,
                        "Ttl": 3000
                    },
                    "Condition": {
                        "ConditionRule": [
                            {
                                "Object": "regex",
                                "Operator": "match",
                                "Type": "url",
                                "Value": "^/a{1,2}(.*)g$"
                            }
                        ],
                        "Connective": "OR"
                    }
                }
            ],
            "Cache": [
                {
                    "CacheAction": {
                        "Action": "cache",
                        "DefaultPolicy": "default",
                        "IgnoreCase": true,
                        "Ttl": 50
                    },
                    "Condition": {
                        "ConditionRule": [
                            {
                                "Object": "filetype",
                                "Operator": "match",
                                "Type": "url",
                                "Value": "jpg;png"
                            }
                        ],
                        "Connective": "OR"
                    }
                },
                {
                    "CacheAction": {
                        "Action": "cache",
                        "DefaultPolicy": "force_cache",
                        "IgnoreCase": false,
                        "Ttl": 80
                    },
                    "Condition": {
                        "ConditionRule": [
                            {
                                "Object": "directory",
                                "Operator": "match",
                                "Type": "url",
                                "Value": "/docs/foods/;/dogs/ragdolls/"
                            }
                        ],
                        "Connective": "OR"
                    }
                },
                {
                    "CacheAction": {
                        "Action": "cache",
                        "DefaultPolicy": "origin_first",
                        "IgnoreCase": false,
                        "Ttl": 40
                    },
                    "Condition": {
                        "ConditionRule": [
                            {
                                "Object": "path",
                                "Operator": "match",
                                "Type": "url",
                                "Value": "/docs/file1;/docs/file2"
                            }
                        ],
                        "Connective": "OR"
                    }
                },
                {
                    "CacheAction": {
                        "Action": "cache",
                        "DefaultPolicy": "origin_first_Replenish",
                        "IgnoreCase": false,
                        "Ttl": 0
                    },
                    "Condition": {
                        "ConditionRule": [
                            {
                                "Object": "regex",
                                "Operator": "match",
                                "Type": "url",
                                "Value": "^/a{1,2}(.*)g$"
                            }
                        ],
                        "Connective": "OR"
                    }
                }
            ],
            "CacheKey": [
                {
                    "CacheKeyAction": {
                        "CacheKeyComponents": [
                            {
                                "Action": "include",
                                "IgnoreCase": false,
                                "Object": "queryString",
                                "Subobject": "*"
                            }
                        ]
                    },
                    "Condition": {
                        "ConditionRule": [
                            {
                                "Object": "filetype",
                                "Operator": "match",
                                "Type": "url",
                                "Value": "jpg;png",
                                "IgnoreCase": true
                            }
                        ],
                        "Connective": "OR"
                    }
                },
                {
                    "CacheKeyAction": {
                        "CacheKeyComponents": [
                            {
                                "Action": "exclude",
                                "IgnoreCase": false,
                                "Object": "queryString",
                                "Subobject": "*"
                            }
                        ]
                    },
                    "Condition": {
                        "ConditionRule": [
                            {
                                "Object": "directory",
                                "Operator": "match",
                                "Type": "url",
                                "Value": "/docs/foods/;/dogs/ragdolls/"
                            }
                        ],
                        "Connective": "OR"
                    }
                },
                {
                    "CacheKeyAction": {
                        "CacheKeyComponents": [
                            {
                                "Action": "includePart",
                                "IgnoreCase": true,
                                "Object": "queryString",
                                "Subobject": "param1;param2"
                            }
                        ]
                    },
                    "Condition": {
                        "ConditionRule": [
                            {
                                "Object": "path",
                                "Operator": "match",
                                "Type": "url",
                                "Value": "/docs/file1;/docs/file2"
                            }
                        ],
                        "Connective": "OR"
                    }
                },
                {
                    "CacheKeyAction": {
                        "CacheKeyComponents": [
                            {
                                "Action": "excludePart",
                                "IgnoreCase": false,
                                "Object": "queryString",
                                "Subobject": "param3;param4"
                            }
                        ]
                    },
                    "Condition": {
                        "ConditionRule": [
                            {
                                "Object": "regex",
                                "Operator": "match",
                                "Type": "url",
                                "Value": "^/a{1,2}(.*)g$"
                            }
                        ],
                        "Connective": "OR"
                    }
                },
                {
                    "CacheKeyAction": {
                        "CacheKeyComponents": [
                            {
                                "Action": "include",
                                "IgnoreCase": true,
                                "Object": "queryString",
                                "Subobject": "*"
                            }
                        ]
                    },
                    "Condition": {
                        "ConditionRule": [
                            {
                                "Object": "directory",
                                "Operator": "match",
                                "Type": "url",
                                "Value": "/"
                            }
                        ],
                        "Connective": "OR"
                    }
                }
            ],
            "Cname": "test111.example.com.bplslb.com",
            "Compression": {
                "CompressionRules": [
                    {
                        "CompressionAction": {
                            "CompressionFormat": "all",
                            "CompressionTarget": "*",
                            "CompressionType": [
                                "gzip",
                                "br"
                            ],
                            "MinFileSizeKB": 10240
                        },
                        "Condition": {
                            "ConditionRule": [
                                {
                                    "Object": "filetype",
                                    "Operator": "match",
                                    "Type": "url",
                                    "Value": "jpg;png"
                                }
                            ],
                            "Connective": "OR"
                        }
                    },
                    {
                        "CompressionAction": {
                            "CompressionFormat": "all",
                            "CompressionTarget": "*",
                            "CompressionType": [
                                "gzip"
                            ],
                            "MinFileSizeKB": 10000
                        },
                        "Condition": {
                            "ConditionRule": [
                                {
                                    "Object": "directory",
                                    "Operator": "match",
                                    "Type": "url",
                                    "Value": "/docs/foods/;/dogs/ragdolls/"
                                }
                            ],
                            "Connective": "OR"
                        }
                    },
                    {
                        "CompressionAction": {
                            "CompressionFormat": "all",
                            "CompressionTarget": "*",
                            "CompressionType": [
                                "br"
                            ],
                            "MinFileSizeKB": 12345
                        },
                        "Condition": {
                            "ConditionRule": [
                                {
                                    "Object": "path",
                                    "Operator": "match",
                                    "Type": "url",
                                    "Value": "/docs/file1;/docs/file2"
                                }
                            ],
                            "Connective": "OR"
                        }
                    }
                ],
                "Switch": true
            },
            "ConditionalOrigin": {
                "OriginRules": [
                    {
                        "Actions": {
                            "OriginLines": [
                                {
                                    "Address": "203.0.113.6",
                                    "HttpPort": "80",
                                    "HttpsPort": "443",
                                    "InstanceType": "ip",
                                    "OriginHost": ""
                                }
                            ]
                        },
                        "Condition": {
                            "ConditionGroups": [
                                {
                                    "Condition": {
                                        "Name": "myparam",
                                        "Object": "query_name",
                                        "Operator": "equal",
                                        "Type": "querystring",
                                        "Value": [
                                            "myvalue"
                                        ]
                                    },
                                    "IsGroup": false
                                }
                            ],
                            "Connective": "and",
                            "IsGroup": true
                        }
                    },
                    {
                        "Actions": {
                            "OriginLines": [
                                {
                                    "Address": "mybucket.s3-ap-southeast-1.amazonaws.com",
                                    "BucketSource": "aws_common",
                                    "HttpPort": "",
                                    "HttpsPort": "",
                                    "InstanceType": "storage",
                                    "OriginHost": "",
                                    "PrivateBucketAccess": true,
                                    "TosAuthInformation": {
                                        "AccessKeyId": "xxxxxxxxxxxxx",
                                        "AccessKeySecret": "xxxxx",
                                        "Region": "ap-southeast-1"
                                    }
                                }
                            ]
                        },
                        "Condition": {
                            "ConditionGroups": [
                                {
                                    "Condition": {
                                        "Name": "myheader",
                                        "Object": "customize",
                                        "Operator": "match",
                                        "Type": "request_header",
                                        "Value": [
                                            "myvalue"
                                        ]
                                    },
                                    "IsGroup": false
                                }
                            ],
                            "Connective": "and",
                            "IsGroup": true
                        }
                    },
                    {
                        "Actions": {
                            "OriginLines": [
                                {
                                    "Address": "mybucket.cos.ap-singapore.myqcloud.com",
                                    "BucketSource": "cos",
                                    "HttpPort": "",
                                    "HttpsPort": "",
                                    "InstanceType": "storage",
                                    "OriginHost": "",
                                    "PrivateBucketAccess": true,
                                    "TosAuthInformation": {
                                        "AccessKeyId": "xxxxxxxxxxxxx",
                                        "AccessKeySecret": "xxxxx"
                                    }
                                }
                            ]
                        },
                        "Condition": {
                            "ConditionGroups": [
                                {
                                    "Condition": {
                                        "Object": "client_ip",
                                        "Operator": "belong",
                                        "Value": [
                                            "HKG",
                                            "CHE"
                                        ]
                                    },
                                    "IsGroup": false
                                }
                            ],
                            "Connective": "and",
                            "IsGroup": true
                        }
                    },
                    {
                        "Actions": {
                            "OriginLines": [
                                {
                                    "Address": "banana-health.tos-ap-southeast-1.bytepluses.com",
                                    "BucketSource": "tos",
                                    "HttpPort": "",
                                    "HttpsPort": "",
                                    "InstanceType": "storage",
                                    "OriginHost": "banana-health.tos-ap-southeast-1.bytepluses.com",
                                    "PrivateBucketAccess": true
                                }
                            ]
                        },
                        "Condition": {
                            "ConditionGroups": [
                                {
                                    "Condition": {
                                        "Object": "filetype",
                                        "Operator": "equal",
                                        "Value": [
                                            "png"
                                        ]
                                    },
                                    "IsGroup": false
                                }
                            ],
                            "Connective": "and",
                            "IsGroup": true
                        }
                    },
                    {
                        "Actions": {
                            "OriginLines": [
                                {
                                    "Address": "www.example.com",
                                    "HttpPort": "80",
                                    "HttpsPort": "443",
                                    "InstanceType": "domain",
                                    "OriginHost": "non-img.example.com"
                                }
                            ]
                        },
                        "Condition": {
                            "ConditionGroups": [
                                {
                                    "Condition": {
                                        "Object": "directory",
                                        "Operator": "not_equal",
                                        "Value": [
                                            "/img/"
                                        ]
                                    },
                                    "IsGroup": false
                                }
                            ],
                            "Connective": "and",
                            "IsGroup": true
                        }
                    },
                    {
                        "Actions": {
                            "OriginLines": [
                                {
                                    "Address": "198.51.100.5",
                                    "HttpPort": "80",
                                    "HttpsPort": "443",
                                    "InstanceType": "ip",
                                    "OriginHost": "img.example.com"
                                }
                            ]
                        },
                        "Condition": {
                            "ConditionGroups": [
                                {
                                    "Condition": {
                                        "Object": "full_querystring",
                                        "Operator": "regex_match",
                                        "Value": [
                                            "^/a{1,2}.*g$"
                                        ]
                                    },
                                    "IsGroup": false
                                }
                            ],
                            "Connective": "and",
                            "IsGroup": true
                        }
                    },
                    {
                        "Actions": {
                            "OriginLines": [
                                {
                                    "Address": "mybucket.oss-ap-southeast-1.aliyuncs.com",
                                    "BucketSource": "oss",
                                    "HttpPort": "",
                                    "HttpsPort": "",
                                    "InstanceType": "storage",
                                    "OriginHost": "",
                                    "PrivateBucketAccess": true,
                                    "TosAuthInformation": {
                                        "AccessKeyId": "xxxxxxxxxxxxx",
                                        "AccessKeySecret": "xxxxx"
                                    }
                                }
                            ]
                        },
                        "Condition": {
                            "ConditionGroups": [
                                {
                                    "Condition": {
                                        "Object": "path",
                                        "Operator": "equal",
                                        "Value": [
                                            "/docs/file1",
                                            "/docs/file2/"
                                        ]
                                    },
                                    "IsGroup": false
                                },
                                {
                                    "Condition": {
                                        "Object": "path",
                                        "Operator": "equal",
                                        "Value": [
                                            "/docs/file3",
                                            "/docs/file4/"
                                        ]
                                    },
                                    "IsGroup": false
                                }
                            ],
                            "Connective": "or",
                            "IsGroup": true
                        }
                    }
                ],
                "Switch": true
            },
            "CreateTime": 1755314680,
            "CustomErrorPage": {
                "ErrorPageRule": [
                    {
                        "ErrorPageAction": {
                            "Action": "redirect",
                            "RedirectCode": "301",
                            "RedirectUrl": "http://www.example.com/newpage1",
                            "StatusCode": "405"
                        }
                    },
                    {
                        "ErrorPageAction": {
                            "Action": "redirect",
                            "RedirectCode": "307",
                            "RedirectUrl": "http://www.example.com/newpage2",
                            "StatusCode": "504"
                        }
                    }
                ],
                "Switch": true
            },
            "Domain": "test111.example.com",
            "DownloadSpeedLimit": {
                "DownloadSpeedLimitRules": [
                    {
                        "Condition": {
                            "ConditionRule": [
                                {
                                    "Object": "unlimited",
                                    "Operator": "match",
                                    "Type": "url"
                                }
                            ],
                            "Connective": "OR"
                        },
                        "DownloadSpeedLimitAction": {
                            "SpeedLimitRate": 100,
                            "SpeedLimitRateAfter": 50,
                            "SpeedLimitTime": {
                                "BeginTime": "01:00",
                                "DayWeek": "unlimited",
                                "EndTime": "02:00"
                            }
                        }
                    },
                    {
                        "Condition": {
                            "ConditionRule": [
                                {
                                    "Object": "filetype",
                                    "Operator": "match",
                                    "Type": "url",
                                    "Value": "jpg;png"
                                }
                            ],
                            "Connective": "OR"
                        },
                        "DownloadSpeedLimitAction": {
                            "SpeedLimitRate": 200,
                            "SpeedLimitRateAfter": 90,
                            "SpeedLimitTime": {
                                "BeginTime": "04:00",
                                "DayWeek": "monday",
                                "EndTime": "06:00"
                            }
                        }
                    },
                    {
                        "Condition": {
                            "ConditionRule": [
                                {
                                    "Object": "directory",
                                    "Operator": "match",
                                    "Type": "url",
                                    "Value": "/docs/foods/;/dogs/ragdolls/"
                                }
                            ],
                            "Connective": "OR"
                        },
                        "DownloadSpeedLimitAction": {
                            "SpeedLimitRate": 300,
                            "SpeedLimitRateAfter": 90,
                            "SpeedLimitTime": {
                                "BeginTime": "04:00",
                                "DayWeek": "tuesday",
                                "EndTime": "06:00"
                            }
                        }
                    },
                    {
                        "Condition": {
                            "ConditionRule": [
                                {
                                    "Object": "path",
                                    "Operator": "match",
                                    "Type": "url",
                                    "Value": "/docs/file1;/docs/file2"
                                }
                            ],
                            "Connective": "OR"
                        },
                        "DownloadSpeedLimitAction": {
                            "SpeedLimitRate": 400,
                            "SpeedLimitRateAfter": 90,
                            "SpeedLimitTime": {
                                "BeginTime": "04:00",
                                "DayWeek": "wednesday",
                                "EndTime": "13:59"
                            }
                        }
                    },
                    {
                        "Condition": {
                            "ConditionRule": [
                                {
                                    "Object": "regex",
                                    "Operator": "match",
                                    "Type": "url",
                                    "Value": "^/a{1,2}(.*)g$"
                                }
                            ],
                            "Connective": "OR"
                        },
                        "DownloadSpeedLimitAction": {
                            "SpeedLimitRate": 500,
                            "SpeedLimitRateAfter": 90,
                            "SpeedLimitTime": {
                                "BeginTime": "04:00",
                                "DayWeek": "thursday",
                                "EndTime": "05:59"
                            }
                        }
                    }
                ],
                "Switch": true
            },
            "FollowRedirect": true,
            "HTTPS": {
                "CertInfo": {
                    "CertId": "cert-7fade0eb4f8d4aadbde5dd25f2ffdf35",
                    "CertName": "1000011991",
                    "EncryType": "inter_cert",
                    "ExpireTime": 1763086346,
                    "Source": "cert_center"
                },
                "DisableHttp": false,
                "ForcedRedirect": {
                    "EnableForcedRedirect": true,
                    "StatusCode": "303"
                },
                "HTTP2": true,
                "Hsts": {
                    "Subdomain": "include",
                    "Switch": true,
                    "Ttl": 50
                },
                "OCSP": true,
                "Switch": true,
                "TlsVersion": [
                    "tlsv1.1",
                    "tlsv1.2"
                ]
            },
            "HttpForcedRedirect": {
                "EnableForcedRedirect": false,
                "StatusCode": "301"
            },
            "IPv6": {
                "Switch": true
            },
            "IpAccessRule": {
                "Switch": true,
                "DenyStatusCode": 402,
                "RuleType": "allow",
                "Ip": [
                    "xxx.xxx.xx.xx",
                    "xxx.xxx.xx.xxx"
                ],
                "IpSource": {
                    "SourceList": [
                        "x-forwarded-for",
                        "x-real-ip"
                    ],
                    "Type": "custom"
                }
            },
            "MethodDeniedRule": {
                "Methods": "POST,DELETE,CONNECT,OPTIONS",
                "Switch": true
            },
            "MultiRange": {
                "Switch": false
            },
            "NegativeCache": [
                {
                    "Condition": {
                        "ConditionRule": [
                            {
                                "Object": "filetype",
                                "Operator": "match",
                                "Type": "url",
                                "Value": "jpg;png"
                            }
                        ],
                        "Connective": "OR"
                    },
                    "NegativeCacheRule": {
                        "Action": "cache",
                        "IgnoreCase": false,
                        "StatusCode": "400",
                        "Ttl": 60
                    }
                },
                {
                    "Condition": {
                        "ConditionRule": [
                            {
                                "Object": "directory",
                                "Operator": "match",
                                "Type": "url",
                                "Value": "/docs/foods/;/dogs/ragdolls/"
                            }
                        ],
                        "Connective": "OR"
                    },
                    "NegativeCacheRule": {
                        "Action": "cache",
                        "IgnoreCase": true,
                        "StatusCode": "401",
                        "Ttl": 59
                    }
                },
                {
                    "Condition": {
                        "ConditionRule": [
                            {
                                "Object": "path",
                                "Operator": "match",
                                "Type": "url",
                                "Value": "/docs/file1;/docs/file2"
                            }
                        ],
                        "Connective": "OR"
                    },
                    "NegativeCacheRule": {
                        "Action": "cache",
                        "IgnoreCase": false,
                        "StatusCode": "402",
                        "Ttl": 70
                    }
                },
                {
                    "Condition": {
                        "ConditionRule": [
                            {
                                "Object": "regex",
                                "Operator": "match",
                                "Type": "url",
                                "Value": "^/a{1,2}(.*)g$"
                            }
                        ],
                        "Connective": "OR"
                    },
                    "NegativeCacheRule": {
                        "Action": "cache",
                        "IgnoreCase": false,
                        "StatusCode": "404",
                        "Ttl": 60
                    }
                }
            ],
            "OfflineCache": {
                "Object": "request_error,error_code",
                "StatusCode": "504;505",
                "Switch": true
            },
            "Origin": [
                {
                    "OriginAction": {
                        "OriginLines": [
                            {
                                "Address": "203.0.113.8",
                                "HttpPort": "80",
                                "HttpsPort": "443",
                                "InstanceType": "ip",
                                "OriginHost": "myorigin.example.com",
                                "OriginType": "primary",
                                "PrivateBucketAccess": false,
                                "Weight": "1"
                            },
                            {
                                "Address": "img.example.com",
                                "HttpPort": "80",
                                "HttpsPort": "443",
                                "InstanceType": "domain",
                                "OriginHost": "myorigin2.example.com",
                                "OriginType": "primary",
                                "PrivateBucketAccess": false,
                                "Weight": "1"
                            },
                            {
                                "Address": "bpcntest.tos-ap-southeast-3.bytepluses.com",
                                "InstanceType": "tos",
                                "OriginHost": "bpcntest.tos-ap-southeast-3.bytepluses.com",
                                "OriginType": "primary",
                                "PrivateBucketAccess": true,
                                "PrivateBucketAuth": {
                                    "AuthType": "tos",
                                    "Switch": true
                                },
                                "Region": "ap-southeast-3",
                                "Weight": "1"
                            },
                            {
                                "Address": "mybucket.oss-ap-southeast-1.aliyuncs.com",
                                "InstanceType": "tos",
                                "OriginHost": "mybucket.oss-ap-southeast-1.aliyuncs.com",
                                "OriginType": "primary",
                                "PrivateBucketAccess": true,
                                "PrivateBucketAuth": {
                                    "AuthType": "oss",
                                    "Switch": true,
                                    "TosAuthInformation": {
                                        "AccessKeyId": "xxxxxxxxxx",
                                        "AccessKeySecret": "xxxxxx"
                                    }
                                },
                                "Region": "oss-ap-southeast-1",
                                "Weight": "2"
                            },
                            {
                                "Address": "mybucket.cos.ap-singapore.myqcloud.com",
                                "InstanceType": "tos",
                                "OriginHost": "mybucket.cos.ap-singapore.myqcloud.com",
                                "OriginType": "primary",
                                "PrivateBucketAccess": true,
                                "PrivateBucketAuth": {
                                    "AuthType": "cos",
                                    "Switch": true,
                                    "TosAuthInformation": {
                                        "AccessKeyId": "xxxxxxxxxxxxxxxxxxx",
                                        "AccessKeySecret": "xxxxxxxxxxxx"
                                    }
                                },
                                "Region": "ap-singapore",
                                "Weight": "3"
                            },
                            {
                                "Address": "my-bucket.s3.ap-southeast-1.amazonaws.com",
                                "InstanceType": "tos",
                                "OriginHost": "my-bucket.s3.ap-southeast-1.amazonaws.com",
                                "OriginType": "primary",
                                "PrivateBucketAccess": true,
                                "PrivateBucketAuth": {
                                    "AuthType": "aws_common",
                                    "Switch": true,
                                    "TosAuthInformation": {
                                        "AccessKeyId": "xxxxxxxxxxxxxxxxxxxxxxxxxxxxx",
                                        "AccessKeySecret": "xxxxxxxxxx"
                                    }
                                },
                                "Region": "ap-southeast-1",
                                "Weight": "5"
                            },
                            {
                                "Address": "myazstorage.blob.core.windows.net",
                                "BucketName": "myazstorage",
                                "InstanceType": "tos",
                                "OriginHost": "myazstorage.blob.core.windows.net",
                                "OriginType": "primary",
                                "PrivateBucketAccess": true,
                                "PrivateBucketAuth": {
                                    "AuthType": "azure",
                                    "Switch": true,
                                    "TosAuthInformation": {
                                        "AccountKey": "xxxxxxxxxxxxxxxx"
                                    }
                                },
                                "Weight": "1"
                            },
                            {
                                "Address": "203.0.113.9",
                                "HttpPort": "80",
                                "HttpsPort": "443",
                                "InstanceType": "ip",
                                "OriginType": "backup",
                                "PrivateBucketAccess": false,
                                "Weight": "1"
                            },
                            {
                                "Address": "img2.example.com",
                                "HttpPort": "80",
                                "HttpsPort": "443",
                                "InstanceType": "domain",
                                "OriginType": "backup",
                                "PrivateBucketAccess": false,
                                "Weight": "1"
                            }
                        ]
                    }
                }
            ],
            "OriginAccessRule": {
                "AllowEmpty": true,
                "IgnoreCase": true,
                "Origins": [
                    "test.example.net",
                    "my.example.net"
                ],
                "RuleType": "deny",
                "Switch": true
            },
            "OriginArg": [
                {
                    "Condition": {
                        "ConditionRule": [
                            {
                                "Object": "regex",
                                "Operator": "match",
                                "Type": "url",
                                "Value": "^/a{1,2}(.*)g$"
                            }
                        ],
                        "Connective": "OR"
                    },
                    "OriginArgAction": {
                        "OriginArgComponents": [
                            {
                                "Action": "set",
                                "Object": "queryString",
                                "Subobject": "key3=val3;key4=val4"
                            }
                        ]
                    }
                },
                {
                    "Condition": {
                        "ConditionRule": [
                            {
                                "Object": "filetype",
                                "Operator": "match",
                                "Type": "url",
                                "Value": "png;jpg"
                            }
                        ],
                        "Connective": "OR"
                    },
                    "OriginArgAction": {
                        "OriginArgComponents": [
                            {
                                "Action": "excludePart",
                                "Object": "queryString",
                                "Subobject": "param1;param2"
                            }
                        ]
                    }
                },
                {
                    "Condition": {
                        "ConditionRule": [
                            {
                                "Object": "directory",
                                "Operator": "match",
                                "Type": "url",
                                "Value": "/docs/foods/;/dogs/ragdolls/"
                            }
                        ],
                        "Connective": "OR"
                    },
                    "OriginArgAction": {
                        "OriginArgComponents": [
                            {
                                "Action": "includePart",
                                "Object": "queryString",
                                "Subobject": "param1;param2"
                            }
                        ]
                    }
                },
                {
                    "Condition": {
                        "ConditionRule": [
                            {
                                "Object": "path",
                                "Operator": "match",
                                "Type": "url",
                                "Value": "/docs/file3;/docs/file4"
                            }
                        ],
                        "Connective": "OR"
                    },
                    "OriginArgAction": {
                        "OriginArgComponents": [
                            {
                                "Action": "addPart",
                                "Object": "queryString",
                                "Subobject": "key1=val1;key2=val2"
                            }
                        ]
                    }
                },
                {
                    "Condition": {
                        "ConditionRule": [
                            {
                                "Object": "path",
                                "Operator": "match",
                                "Type": "url",
                                "Value": "/docs/file1;/docs/file2"
                            }
                        ],
                        "Connective": "OR"
                    },
                    "OriginArgAction": {
                        "OriginArgComponents": [
                            {
                                "Action": "exclude",
                                "Object": "queryString",
                                "Subobject": "*"
                            }
                        ]
                    }
                },
                {
                    "Condition": {
                        "ConditionRule": [
                            {
                                "Object": "directory",
                                "Operator": "match",
                                "Type": "url",
                                "Value": "/"
                            }
                        ],
                        "Connective": "OR"
                    },
                    "OriginArgAction": {
                        "OriginArgComponents": [
                            {
                                "Action": "include",
                                "Object": "queryString",
                                "Subobject": "*"
                            }
                        ]
                    }
                }
            ],
            "OriginCertCheck": {
                "Switch": true
            },
            "OriginHost": "superhost.example.com",
            "OriginIPv6": "ipv6_first",
            "OriginProtocol": "https",
            "OriginRange": true,
            "Range": {
                "Switch": true,
                "RangeSize": "2",
                "Unit": "MB"
            },
            "OriginRewrite": {
                "Switch": false
            },
            "OriginSni": {
                "SniDomain": "superhost.example.com",
                "Switch": true
            },
            "PageOptimization": {
                "OptimizationType": [
                    "html",
                    "js",
                    "css"
                ],
                "Switch": true
            },
            "Project": "default",
            "Quic": {
                "Switch": true
            },
            "RedirectionRewrite": {
                "RedirectionRule": [
                    {
                        "RedirectionAction": {
                            "RedirectCode": "302",
                            "SourcePath": "^/a{1,2}(.*)g$",
                            "TargetHost": "www.example.com",
                            "TargetPath": "/food$1g",
                            "TargetProtocol": "https",
                            "TargetQueryComponents": {
                                "Action": "includePart",
                                "Value": "param1"
                            }
                        }
                    },
                    {
                        "RedirectionAction": {
                            "RedirectCode": "307",
                            "SourcePath": "aaa(.*)",
                            "TargetHost": "www.example.com",
                            "TargetPath": "/food/$1g",
                            "TargetProtocol": "followclient",
                            "TargetQueryComponents": {
                                "Action": "include",
                                "Value": "*"
                            }
                        }
                    }
                ],
                "Switch": true
            },
            "RefererAccessRule": {
                "AllowEmpty": true,
                "Referers": [
                    "www.example.org",
                    "docs.example.com",
                    "^https://test.example.com/a{1,2}bc/.*\\.jpg$"
                ],
                "ReferersType": {
                    "CommonType": {
                        "IgnoreCase": true,
                        "IgnoreScheme": true,
                        "Referers": [
                            "www.example.org",
                            "docs.example.com"
                        ]
                    },
                    "RegularType": {
                        "Referers": [
                            "^https://test.example.com/a{1,2}bc/.*\\.jpg$"
                        ]
                    }
                },
                "RuleType": "allow",
                "Switch": true
            },
            "RemoteAuth": {
                "RemoteAuthRules": [
                    {
                        "Condition": {
                            "ConditionRule": [
                                {
                                    "Object": "filetype",
                                    "Operator": "match",
                                    "Type": "url",
                                    "Value": "bmp;pdf"
                                },
                                {
                                    "Object": "directory",
                                    "Operator": "match",
                                    "Type": "url",
                                    "Value": "/docs/foods/;/dogs/ragdolls/"
                                },
                                {
                                    "Object": "path",
                                    "Operator": "match",
                                    "Type": "url",
                                    "Value": "/docs/file1;/docs/file2"
                                }
                            ],
                            "Connective": "OR"
                        },
                        "RemoteAuthRuleAction": {
                            "AuthModeConfig": {
                                "BackupRemoteAddr": "https://myendpoint2.com",
                                "MasterRemoteAddr": "https://myendpoint1.com",
                                "PathType": "variable",
                                "PathValue": "/sign",
                                "RequestMethod": "post"
                            },
                            "AuthResponseConfig": {
                                "CacheAction": {
                                    "Action": "cache",
                                    "CacheKey": [
                                        "URI",
                                        "content_type"
                                    ],
                                    "IgnoreCase": false,
                                    "Ttl": 40
                                },
                                "ResponseAction": {
                                    "StatusCode": "403"
                                },
                                "StatusCodeAction": {
                                    "DefaultAction": "pass",
                                    "FailCode": "401",
                                    "SuccessCode": "200"
                                },
                                "TimeOutAction": {
                                    "Action": "pass",
                                    "Time": 200
                                }
                            },
                            "QueryStringRules": {
                                "QueryStringComponents": {
                                    "Action": "includePart",
                                    "Value": "size;color"
                                },
                                "QueryStringInstances": [
                                    {
                                        "Action": "set",
                                        "Key": "param1",
                                        "Value": "val1",
                                        "ValueType": "constant"
                                    },
                                    {
                                        "Action": "set",
                                        "Key": "param2",
                                        "Value": "content_type",
                                        "ValueType": "variable"
                                    }
                                ]
                            },
                            "RequestBodyRules": "default",
                            "RequestHeaderRules": {
                                "RequestHeaderComponents": {
                                    "Action": "includePart",
                                    "Value": "header1;header2"
                                },
                                "RequestHeaderInstances": [
                                    {
                                        "Action": "set",
                                        "Key": "hd1",
                                        "Value": "val1",
                                        "ValueType": "constant"
                                    },
                                    {
                                        "Action": "set",
                                        "Key": "hd2",
                                        "Value": "client_ip",
                                        "ValueType": "variable"
                                    }
                                ],
                                "RequestHost": "test.example.com"
                            }
                        }
                    }
                ],
                "Switch": true
            },
            "RequestBlockRule": {
                "BlockRule": [
                    {
                        "BlockAction": {
                            "Action": "refuse",
                            "StatusCode": "404"
                        },
                        "Condition": {
                            "ConditionRule": [
                                {
                                    "Object": "path",
                                    "Operator": "equal",
                                    "Type": "url",
                                    "Value": "/docs/file1;/docs/file2"
                                },
                                {
                                    "Object": "directory",
                                    "Operator": "equal",
                                    "Type": "url",
                                    "Value": "/docs/foods/;/dogs/ragdolls/"
                                },
                                {
                                    "Object": "filetype",
                                    "Operator": "equal",
                                    "Type": "url",
                                    "Value": "jpg;png"
                                },
                                {
                                    "Name": "param1",
                                    "Object": "query_name",
                                    "Operator": "equal",
                                    "Type": "querystring",
                                    "Value": "val1"
                                },
                                {
                                    "Object": "regex",
                                    "Operator": "match",
                                    "Type": "url",
                                    "Value": "/a{1,2}(.*)g$"
                                }
                            ],
                            "Connective": "OR"
                        },
                        "RuleName": "myrule1"
                    },
                    {
                        "BlockAction": {
                            "Action": "redirect",
                            "RedirectUrl": "https://www.example.com/helloworld",
                            "StatusCode": "301"
                        },
                        "Condition": {
                            "ConditionRule": [
                                {
                                    "Object": "full_querystring",
                                    "Operator": "not_match",
                                    "Type": "querystring",
                                    "Value": ".*size=.*\\&.*"
                                },
                                {
                                    "Object": "client_ip",
                                    "Operator": "match",
                                    "Type": "client_ip",
                                    "Value": "203.0.113.2;203.0.113.5"
                                },
                                {
                                    "Object": "ua",
                                    "Operator": "not_empty",
                                    "Type": "request_header"
                                },
                                {
                                    "Name": "myheader",
                                    "Object": "customize",
                                    "Operator": "match",
                                    "Type": "request_header",
                                    "Value": "value1"
                                }
                            ],
                            "Connective": "AND"
                        },
                        "RuleName": "myrule2"
                    }
                ],
                "Switch": true
            },
            "RequestHeader": [
                {
                    "RequestHeaderAction": {
                        "RequestHeaderInstances": [
                            {
                                "Action": "set",
                                "Key": "header1",
                                "Value": "val1",
                                "ValueType": "constant"
                            },
                            {
                                "Action": "set",
                                "Key": "header2",
                                "Value": "uri",
                                "ValueType": "variable"
                            },
                            {
                                "Action": "set",
                                "Key": "header3",
                                "Value": "myval${http_host}is${query_string}",
                                "ValueType": "customize"
                            },
                            {
                                "Action": "delete",
                                "Key": "header4"
                            }
                        ]
                    }
                }
            ],
            "ResourceTags": [
                {
                    "Key": "key1",
                    "Value": "value1"
                },
                {
                    "Key": "key2",
                    "Value": "value2"
                }
            ],
            "ResponseHeader": [
                {
                    "ResponseHeaderAction": {
                        "ResponseHeaderInstances": [
                            {
                                "AccessOriginControl": true,
                                "Action": "set",
                                "Key": "Access-Control-Allow-Origin",
                                "Value": "myval",
                                "ValueType": "constant"
                            },
                            {
                                "AccessOriginControl": false,
                                "Action": "set",
                                "Key": "Access-Control-Allow-Headers",
                                "Value": "raw_uri",
                                "ValueType": "variable"
                            },
                            {
                                "AccessOriginControl": false,
                                "Action": "set",
                                "Key": "Access-Control-Expose-Headers",
                                "Value": "my${host}data${query_string}",
                                "ValueType": "customize"
                            },
                            {
                                "AccessOriginControl": false,
                                "Action": "delete",
                                "Key": "Access-Control-Max-Age"
                            }
                        ]
                    }
                }
            ],
            "RuleEngine": {
                "Rules": [],
                "Switch": false
            },
            "ServiceRegion": "outside_chinese_mainland",
            "ServiceType": "web",
            "SignedUrlAuth": {
                "AuthRulesF": [
                    {
                        "ArgumentRule": {
                            "GeneralParamRule": {
                                "ParentLinkParamInherit": "inherit",
                                "SubLinkParamRule": {
                                    "InheritMode": "inherit_first",
                                    "KeepSubLinkArg": "keep"
                                }
                            },
                            "KeepOriginArg": true
                        },
                        "AuthTokenCalRule": {
                            "ParamCalRules": [
                                "md5_bin",
                                "base64url",
                                "sha256",
                                "md5",
                                "base64_encode"
                            ],
                            "SignJoinSymbol": "abc",
                            "SignParam": [
                                {
                                    "ParamType": "SecretKey"
                                },
                                {
                                    "ParamType": "SupString",
                                    "SupContent": "fixstring"
                                },
                                {
                                    "ParamSource": "ChildLink",
                                    "ParamType": "URI",
                                    "UriParamSup": {
                                        "JoinSymbol": "/",
                                        "SplitSymbol": "-",
                                        "StartLevel": 3,
                                        "TermLevel": 5
                                    }
                                },
                                {
                                    "ParamSource": "ParentLink",
                                    "ParamType": "URLParam",
                                    "UrlParam": {
                                        "ArgSegment": {
                                            "Level": 0,
                                            "Switch": false
                                        },
                                        "CapMode": "uri",
                                        "UriLevel": 3
                                    }
                                },
                                {
                                    "ParamType": "ClientDomain"
                                },
                                {
                                    "ParamType": "Referer"
                                },
                                {
                                    "ParamType": "Origin"
                                },
                                {
                                    "ParamType": "ClientIP"
                                },
                                {
                                    "ParamType": "UA"
                                },
                                {
                                    "ParamType": "ReqHeader",
                                    "RequestHeader": "myheader1"
                                },
                                {
                                    "CookieToken": "mycookie1",
                                    "ParamType": "Cookie"
                                },
                                {
                                    "ParamSource": "ChildLink",
                                    "ParamType": "FullURI"
                                }
                            ]
                        },
                        "Condition": {
                            "ConditionRule": [
                                {
                                    "Object": "filetype",
                                    "Operator": "match",
                                    "Type": "url",
                                    "Value": "jpg;png"
                                },
                                {
                                    "Object": "directory",
                                    "Operator": "not_match",
                                    "Type": "url",
                                    "Value": "/docs/foods/;/dogs/ragdolls/"
                                },
                                {
                                    "Object": "path",
                                    "Operator": "match",
                                    "Type": "url",
                                    "Value": "/docs/file1;/docs/file2"
                                },
                                {
                                    "Object": "regex",
                                    "Operator": "match",
                                    "Type": "url",
                                    "Value": "^/a{1,2}(.*)g$"
                                }
                            ],
                            "Connective": "OR"
                        },
                        "CustomRewrite": {
                            "RewriteParam": [
                                {
                                    "ParamType": "ParentLinkUrlParam",
                                    "ParentLinkUrlParam": {
                                        "ArgSegment": {
                                            "Level": 0,
                                            "Switch": false
                                        },
                                        "CapMode": "name",
                                        "ParamName": "param23"
                                    }
                                },
                                {
                                    "ParamType": "SupString",
                                    "SupContent": "string2"
                                },
                                {
                                    "ParamType": "ParentLinkURI",
                                    "ParentLinkUriParamSup": {
                                        "JoinSymbol": "/",
                                        "SplitSymbol": "-",
                                        "StartLevel": 4,
                                        "TermLevel": 6
                                    }
                                },
                                {
                                    "ParamType": "ParentLinkExpire"
                                },
                                {
                                    "ParamType": "AuthToken"
                                },
                                {
                                    "ParamType": "ParentFullURI"
                                }
                            ],
                            "RewriteRule": {
                                "CapMode": "name",
                                "ParamName": "myparam1"
                            },
                            "SignJoinSymbol": "/",
                            "Switch": true
                        },
                        "ExpireTimeRule": {
                            "Duration": 30,
                            "ExpTimeCapRule": {
                                "ArgSegment": {
                                    "Level": 0,
                                    "Switch": false
                                },
                                "CapMode": "name",
                                "ParamName": "param1"
                            },
                            "TimeFormat": "heximal"
                        },
                        "RewriteFormat": "default",
                        "RewriteM3U8": {
                            "RewriteM3U8Tag": {
                                "Switch": true,
                                "Tags": [
                                    "tag1",
                                    "tag2"
                                ]
                            },
                            "Switch": true
                        },
                        "RewriteMPD": {
                            "MpdVarExpand": true,
                            "Switch": true
                        },
                        "RuleName": "Authentication rule A",
                        "SecretKey": {
                            "BackupSecretKey": "secondarykey",
                            "MasterSecretKey": "primarykey"
                        },
                        "SignCapRule": {
                            "ArgSegment": {
                                "Level": 2,
                                "SplitSymbol": "-",
                                "Switch": true
                            },
                            "CapMode": "uri",
                            "UriLevel": 2
                        }
                    },
                    {
                        "ArgumentRule": {
                            "GeneralParamRule": {
                                "ParentLinkParamInherit": "not_inherit",
                                "SubLinkParamRule": {
                                    "InheritMode": "sub_link_first",
                                    "KeepSubLinkArg": "keep"
                                }
                            },
                            "KeepOriginArg": false
                        },
                        "AuthTokenCalRule": {
                            "ParamCalRules": [
                                "base64url"
                            ],
                            "SignJoinSymbol": "45yu",
                            "SignParam": [
                                {
                                    "ParamType": "SecretKey"
                                }
                            ]
                        },
                        "Condition": {
                            "ConditionRule": [
                                {
                                    "Object": "directory",
                                    "Operator": "match",
                                    "Type": "url",
                                    "Value": "/"
                                }
                            ],
                            "Connective": "OR"
                        },
                        "ExpireTimeRule": {
                            "Duration": 67,
                            "ExpTimeCapRule": {
                                "CapMode": "cookie",
                                "CustomValue": "mycookie56"
                            },
                            "TimeFormat": "octal"
                        },
                        "RewriteFormat": "default",
                        "RuleName": "Authentication rule B",
                        "SecretKey": {
                            "BackupSecretKey": "sk",
                            "MasterSecretKey": "pk"
                        },
                        "SignCapRule": {
                            "CapMode": "header",
                            "CustomValue": "myheader56"
                        }
                    }
                ],
                "Switch": true
            },
            "Status": "online",
            "Timeout": {
                "Switch": true,
                "TimeoutRules": [
                    {
                        "TimeoutAction": {
                            "HttpTimeout": 10,
                            "TcpTimeout": 5,
                            "HttpFirstByteTimeout": 90
                        }
                    }
                ]
            },
            "UaAccessRule": {
                "AllowEmpty": true,
                "IgnoreCase": true,
                "RuleType": "deny",
                "Switch": true,
                "UserAgent": [
                    "*curl*",
                    "*firefox*"
                ]
            },
            "UpdateTime": 1755323476,
            "UrlNormalize": {
                "NormalizeObject": [
                    "back_slashes",
                    "successive_slashes",
                    "dot_segments"
                ],
                "Switch": true
            },
            "VideoDrag": {
                "Switch": true
            },
            "Websocket": {
                "Switch": true,
                "Timeout": 60
            }
        }
    }
}
```
