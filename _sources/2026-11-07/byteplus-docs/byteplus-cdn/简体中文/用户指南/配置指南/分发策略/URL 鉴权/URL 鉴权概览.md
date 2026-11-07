---
title: "URL 鉴权概览"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/docs_cn-overview-cn"
---

<span id="url-鉴权概览"></span>
# URL 鉴权概览

URL 鉴权通过校验请求中的签名和有效期，保护 CDN 内容，降低资源被盗用的风险。

<span id="适用前提"></span>
## 适用前提

使用 URL 鉴权前，请确认以下条件：


* 您已明确需要保护的 CDN 资源，而不是允许任意用户直接访问。

* 客户端或签名服务器能够根据 CDN 配置生成签名，并使用与 CDN 一致的 Key、算法、时间戳和签名规则。

* 您已明确 URL 鉴权的生效对象范围。请求未命中生效对象时，不执行 URL 鉴权；命中但未携带有效签名时，CDN 返回 403。


<span id="工作原理"></span>
## 工作原理


1. 客户端或签名服务器生成符合 CDN 配置要求的时间戳和签名，并将其写入请求。

2. CDN 收到请求后，先判断请求是否命中生效对象。未命中的请求不执行 URL 鉴权。

3. 对命中的请求，CDN 使用主 Key 按同一规则重新计算签名并检查有效期。主 Key 校验不通过且配置了备 KEY 时，CDN 再使用备 KEY 校验。

4. 签名有效且请求未过期时，CDN 继续处理请求；否则返回 403。


<span id="选择鉴权类型"></span>
## 选择鉴权类型

先根据鉴权信息的位置，以及计算输入是否需要扩展，选择类型；再阅读对应类型文档完成配置和签名生成。


|类型 |鉴权信息位置 |时间戳 |计算输入 |选择建议 |
|---|---|---|---|---|
|A |单个查询参数 |十进制 Unix 时间戳，秒级 |`uri-timestamp-rand-uid-key` |需要在一个查询参数中携带时间戳、随机串和签名。 |
|B |URL 路径，时间戳在前、签名在后 |`YYYYMMDDHHMM`（东八区时间，UTC+8）、十进制或十六进制 Unix 时间戳 |`key + timestamp + uri` |签名信息必须放在路径中，且需要多种时间格式。 |
|C |URL 路径，签名在前、时间戳在后 |十六进制 Unix 时间戳，秒级 |`key + uri + timestamp` |签名信息必须放在路径中，且可使用固定的十六进制时间戳。 |
|D |独立的签名和时间查询参数 |十进制或十六进制 Unix 时间戳，秒级 |`key + uri + timestamp` |需要独立查询参数，且签名计算顺序固定。 |
|E |独立的签名和时间查询参数 |十进制或十六进制 Unix 时间戳，秒级 |按 CDN 配置的参数和顺序拼接 |除路径和时间戳外，还需要让请求参数、请求头部等信息参与签名。 |
|F |查询参数、路径层级、请求头或 Cookie |可独立配置获取方式，支持八进制、十进制和十六进制 Unix 时间戳 |可组合密钥、固定字符串、URI 片段、请求参数、请求头、Cookie 和客户端信息，并串联多个算法 |需要自定义签名或时间戳的获取方式、计算输入或算法链，或需要改写 HLS、DASH Manifest。 |


公式中的 `+` 表示直接拼接参数值，不是实际字符。

<span id="签名-url-示例代码"></span>
## 签名 URL 示例代码

客户端请求中的签名 URL 可以由可信的签名服务器生成，也可以由客户端生成。以下示例展示如何使用 PHP、Go、Python 和 Java 为 A–E 类型生成签名 URL。使用时，Key、算法、时间格式、参数名以及参与签名的字段和拼接顺序必须与 CDN 配置一致。

对于 E 类型，示例支持按配置顺序组合 Key、客户端域名、`uri`、时间戳、请求参数、请求头部和客户端信息。自定义请求参数参与签名时会追加到 URL；请求头部仅参与签名，实际请求必须携带相同的请求头和值。

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Python 示例代码要求 Python 3。</div>


<Attachment link="https://sf-bpcms.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/20260901083438-1597800222483.txt" name="URL-Auth-for-Go.txt">URL-Auth-for-Go.txt</Attachment>


<Attachment link="https://sf-bpcms.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/20260901083442-187002061058.txt" name="URL-Auth-for-Java.txt">URL-Auth-for-Java.txt</Attachment>


<Attachment link="https://sf-bpcms.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/20260901083446-306248061067.txt" name="URL-Auth-for-PHP.txt">URL-Auth-for-PHP.txt</Attachment>


<Attachment link="https://sf-bpcms.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/20260901083451-1580514399555.txt" name="URL-Auth-for-Python.txt">URL-Auth-for-Python.txt</Attachment>


<span id="缓存键和回源"></span>
## 缓存键和回源

下表说明各类型默认的缓存键和回源行为，以及两者的调整方式。


|类型 |默认缓存键 |缓存键调整方式 |默认回源请求 |回源请求调整方式 |
|---|---|---|---|---|
|A、D |不包含签名和时间戳 |可在缓存键特性中设置是否包含签名和时间戳；通常无需保留。 |不包含签名和时间戳 |不可调整。 |
|B、C |不包含签名和时间戳 |不可调整。 |不包含签名和时间戳 |不可调整。 |
|E |包含签名和时间戳 |在 URL 鉴权配置中通过 **去除鉴权参数缓存和回源** 调整。 |包含签名和时间戳 |在 URL 鉴权配置中通过 **去除鉴权参数缓存和回源** 调整。 |
|F |不包含签名和时间戳 |在缓存键特性中调整。 |不包含签名和时间戳 |在 URL 鉴权配置中调整。 |


<span id="共用行为"></span>
## 共用行为


* CDN 比较签名时，会将计算结果和请求中的签名转换为小写后比较。

* 鉴权失败时可依据 HTTP 403 判断请求被拒绝，但错误响应正文可能随服务版本调整，业务逻辑不可依赖其内容。


<span id="使用提示"></span>
## 使用提示


* Key 仅用于签名计算，不应放入请求 URL。客户端或签名服务器使用 Key 生成签名；CDN 使用已配置的主 Key 或备 KEY 按相同规则计算签名并比对。仅向可信的客户端或签名服务器提供 Key。

* 生效对象决定是否执行鉴权。范围过小会留下未受保护的资源，范围过大可能使原本无需签名的请求返回 403。

* 客户端或签名服务器必须与 CDN 配置使用完全一致的类型、Key、算法、时间格式、参数名和拼接顺序；E 类型还必须保证参与计算的请求参数、请求头部和客户端信息的字段值一致。

* 如果源站也需要校验签名，请结合所选类型的缓存和回源行为，确认源站是否能收到签名参数。


<span id="选择后继续阅读"></span>
## 选择后继续阅读


* [配置 A 类型 URL 鉴权](https://docs.byteplus.com/zh-CN/docs/byteplus-cdn/docs_cn-type-a-cn)

* [配置 B 类型 URL 鉴权](https://docs.byteplus.com/zh-CN/docs/byteplus-cdn/docs_cn-type-b-cn)

* [配置 C 类型 URL 鉴权](https://docs.byteplus.com/zh-CN/docs/byteplus-cdn/docs_cn-type-c-cn)

* [配置 D 类型 URL 鉴权](https://docs.byteplus.com/zh-CN/docs/byteplus-cdn/docs_cn-type-d-cn)

* [配置 E 类型 URL 鉴权](https://docs.byteplus.com/zh-CN/docs/byteplus-cdn/docs_cn-type-e-cn)

* [配置 F 类型 URL 鉴权](https://docs.byteplus.com/zh-CN/docs/byteplus-cdn/typef_zh-cn)

* [域名配置](https://docs.byteplus.com/zh-CN/docs/byteplus-cdn/domain-management_zh-cn)
