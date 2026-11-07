---
title: "A 类型"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/docs_cn-type-a-cn"
---

<span id="类型特点"></span>
## 类型特点

A 类型将时间戳、随机字符串和签名合并为一个查询参数的值，适用于需要以单个查询参数携带完整鉴权信息的场景。

<span id="上线建议"></span>
## 上线建议

建议先规划独立测试文件或目录，验证客户端或签名服务器及 CDN 配置后，再在生效对象中配置正式业务中需要鉴权的资源范围，避免配置错误影响全部资源访问。

<span id="配置生效对象"></span>
## 配置生效对象

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/81669e6faab34d8ca7d03e4e9ea74e03~tplv-goo7wpa0wc-topic.webp) </span>

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/09c48f29500543b0a74527d77a79909d~tplv-goo7wpa0wc-topic.webp) </span>

开启 **URL 鉴权** 并选择 **A 类型**，然后在 **生效对象** 标签页配置。默认包含一条**文件目录**为 `/` 的规则，不能删除。您可以修改该规则的类型和内容，也可以新增规则，最多配置 10 条；多条规则可按 **或**（默认，命中任一条件）或 **且**（同时命中全部条件）组合。仅命中生效对象的请求需要鉴权。


|支持范围 |输入格式 |
|---|---|
|文件后缀 |一个或多个后缀，以分号（`;`）分隔，不带句点。例如：`png;txt`。 |
|文件目录 |一个或多个目录，以分号分隔；每项以 `/` 开头和结尾。例如：`/video/;/image/`。 |
|文件全路径 |一个或多个路径，以分号（`;`）分隔；每项以 `/` 开头，可使用 `*` 匹配一个或多个字符，包括 `/`。例如：`/video/*;/image/logo.png`。 |
|全路径正则 |一个或多个正则表达式，以分号分隔。使用前需[提交工单](https://console.byteplus.com/workorder/create)开通。 |


非正则规则不区分大小写；全路径正则区分大小写。单个条件的匹配值总长度不超过 1,024 个字符，且不能包含 `//`、空格、`$` 或 `?`。

<span id="配置鉴权"></span>
## 配置鉴权

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/135f61925d26461399ee29dd6d423a75~tplv-goo7wpa0wc-topic.webp) </span>

在 **鉴权配置** 标签页配置以下参数。

<span id="基础参数"></span>
### 基础参数


|配置项 |说明 |
|---|---|
|主 Key |必填，长度为 1–120 个字符，仅支持英文字母、数字和英文半角符号；不支持空格、中文或全角字符。客户端或签名服务器使用主 Key 生成签名；CDN 使用主 Key 按相同规则计算签名，并与请求中的签名比对。 |
|备 KEY |可选。当 CDN 使用主 Key 计算的签名与请求中的签名不一致时，使用备 KEY 按相同规则再次计算并比对；输入要求与主 Key 相同。可用于平滑轮换 Key。 |
|签名有效时间 |单位为秒，默认 `1800`，范围为 0–315,360,000。CDN 在 `timestamp + 有效时间 < 收到请求的时间` 时判定 URL 过期。 |
|鉴权算法 |MD5 或 SHA256，默认 MD5。客户端或签名服务器必须与 CDN 配置保持一致。 |


<span id="签名字段"></span>
### 签名字段

`rand` 和 `uid` 不需要在控制台配置。客户端或签名服务器将其写入签名参数值，CDN 收到请求后解析这些值并参与签名校验。


|配置项 |说明 |
|---|---|
|签名参数名 |承载完整鉴权信息，默认 `sign`。区分大小写，长度为 1–100 个字符，可包含字母、数字、`_`、`-`、`.`、`,`、`!`，且至少包含一个字母。 |
|时间戳进制 |固定为十进制 Unix 时间戳，精确到秒。 |


<span id="m3u8-改写"></span>
## M3U8 改写

A 类型支持 **M3U8 改写**。启用后，CDN 会使用 A 类型的签名计算方式为播放列表中的资源 URI 添加签名，以支持 HLS 播放。客户端或签名服务器只需为 `.m3u8` 请求生成签名。

<span id="改写条件"></span>
### 改写条件

启用后，M3U8 改写仅在以下条件同时满足时生效：


* **生效对象**的**文件后缀**包含 `m3u8`，以及播放列表中需要通过 URL 鉴权访问的资源后缀。例如，播放列表引用 `.ts` 分片以及 `.mp4` 文件时，在 **生效对象**的**文件后缀**中配置 `m3u8;ts;mp4`。播放列表中的资源 URI 只要文件后缀命中，CDN 就会执行 URL 鉴权；即使资源 URI 不匹配其他生效条件，CDN 仍会执行 URL 鉴权。

* 源站返回的 `.m3u8` 响应不包含 `Content-Encoding`，且 `.m3u8` 请求不命中 **智能压缩**的生效条件，因为 CDN 不会改写经压缩的 M3U8。


播放列表中的资源 URI 可以是完整 URL、以 `/` 开头的路径或相对路径。资源 URI 为相对路径时，改写后仍为相对路径。

例如，播放列表路径为 `/a-type-m3u8-rewrite-test/playlist.m3u8`，资源 URI 为 `segment-1.ts` 时，改写后为 `segment-1.ts?<签名参数名>=<timestamp>-<rand>-0-<SIGNATURE>`。

<span id="配置改写参数"></span>
### 配置改写参数


|配置项 |说明 |
|---|---|
|分片 URI 原参数 |控制是否保留播放列表中资源 URI 原有的查询参数。 |
|继承 M3U8 非签名参数 |控制是否将 `.m3u8` 请求 URL 中除签名参数外的查询参数添加到播放列表中的资源 URI。 |
|M3U8 标签改写 |默认情况下，CDN 仅改写 `EXTINF` 标签下的资源 URI。启用后，可指定需要改写其下资源 URI 的额外标签。播放列表必须包含 `EXTINF` 标签；否则 CDN 不会改写已指定其他标签下的资源 URI。自定义标签最多 20 个，每个长度为 1–100 个字符，且不能包含 `#` 或 `:`。 |


**分片 URI 原参数**和**继承 M3U8 非签名参数**共同决定改写后资源 URI 的查询参数。例如，资源 URI 为 `/video.ts?version=1`，设置为删除原参数并开启继承，且 `.m3u8` 请求 URL 包含 `q_m3u8=cool` 时，改写后的资源 URI 为 `/video.ts?q_m3u8=cool&<签名参数名>=<timestamp>-<rand>-0-<SIGNATURE>`。如果设置为保留原参数，改写后的资源 URI 为 `/video.ts?version=1&q_m3u8=cool&<签名参数名>=<timestamp>-<rand>-0-<SIGNATURE>`。

<span id="构造签名-url"></span>
## 构造签名 URL

<span id="url-格式"></span>
### URL 格式

```text
scheme://host<uri>?<签名参数名>=<timestamp>-<rand>-<uid>-<SIGNATURE>
```


原始 URL 已含查询参数时，使用 `&` 追加签名参数：

```text
scheme://host<uri>?version=1&<签名参数名>=<timestamp>-<rand>-<uid>-<SIGNATURE>
```


`timestamp`、`rand`、`uid` 和 `SIGNATURE` 间的 `-` 是实际字符。

<span id="签名计算公式"></span>
### 签名计算公式

```text
MD5:    md5(uri-timestamp-rand-uid-key)
SHA256: sha256(uri-timestamp-rand-uid-key)
```


<span id="参数说明"></span>
### 参数说明


|参数 |说明 |
|---|---|
|`uri` |以 `/` 开头的请求路径，不含协议、域名和查询参数。含中文时使用实际发送的编码后路径。 |
|`timestamp` |十进制 Unix 时间戳（秒）。与签名有效时间共同决定签名是否过期。 |
|`rand` |长度为 1–100 的随机字符串，仅可含字母或数字。 |
|`uid` |必须为 `0`。 |
|`key` |主 Key 或备 KEY，仅参与签名计算。 |
|`SIGNATURE` |待签名字符串的哈希值。 |


示例：

```text
https://www.example.com/img/image.png?sign=1644406401-2e1ca42a1bb248408fc9cf435e5af744-0-54959c1ec3448bf8e992554476248fab
```


<span id="缓存和回源"></span>
## 缓存和回源

默认情况下，CDN 不将 A 类型签名参数计入缓存键，且签名参数不包含在回源请求中。URL 鉴权配置不能调整此行为。

<span id="验证"></span>
## 验证


1. 保存后，使用 **鉴权计算器** 选择 A 类型，输入当前域名下未带签名、且命中生效对象的完整原始 URL。

2. 输入已配置的签名参数名、Key、有效时间、算法、`rand` 和开始时间（用于生成 `timestamp`），生成未过期 URL；配置备 KEY 时，同时验证使用备 KEY 生成的 URL。

3. 使用客户端或签名服务器生成 URL，并与 **鉴权计算器** 的结果比对。`uri`、`timestamp`、`rand`、`uid`、Key 和算法必须与计算器设置一致；有效时间不参与签名计算。

4. 请求测试文件，确认可访问；分别使用篡改 `SIGNATURE` 的请求和过期 URL 请求，均应返回 403。

5. 确认源站请求不包含签名参数。

6. 使用 HLS 时，确认播放列表中的资源 URI 已被签名，且相关资源可访问。


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/14d4cee529504cffbb67e2f903d69fa8~tplv-goo7wpa0wc-topic.webp) </span>

<span id="cdn-校验规则"></span>
## CDN 校验规则


* 比对签名时，CDN 会将计算结果和请求中的 `SIGNATURE` 转为小写。

* 缺少或格式错误的签名、签名不一致、签名过期均返回 403。


<span id="上线和回滚"></span>
## 上线和回滚

首次上线时，先只将生效对象覆盖测试文件或目录，验证客户端或签名服务器、CDN 配置和 HLS 播放后，再逐步扩大范围。

轮换 Key 时，先将新 Key 配置为备 KEY，并让客户端或签名服务器使用新 Key 生成签名进行验证；随后将新 Key 升为主 Key、旧 Key 暂留为备 KEY，待旧 URL 全部过期后移除旧 Key。若出现大量非预期 403，立即缩小或删除生效对象；必要时关闭 URL 鉴权并保存，使未签名请求恢复访问。
