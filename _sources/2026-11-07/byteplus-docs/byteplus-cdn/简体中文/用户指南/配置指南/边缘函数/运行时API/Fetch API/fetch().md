---
title: "fetch()"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/docs_cn-fetch-cn"
---

发送一个 HTTP 或 HTTPS 请求。参见 MDN 文档 [fetch()](https://developer.mozilla.org/docs/Web/API/WindowOrWorkerGlobalScope/fetch)。

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">如果您的函数调用 <code>fetch()</code> 方法获取了 HTTP 响应且对 HTML Body 进行了修改（例如使用 <a href="https://docs.byteplus.com/docs/byteplus-cdn/HtmlStream">createHtmlStream()</a> 流式修改了 HTML Body），建议您删除原始 HTTP 响应中的 <code>Content-Length</code> 头。因为 HTTP 响应的 HTML Body 被修改后，payload 的实际大小可能与 <code>Content-Length</code> 头的值所标示的大小不同。运行时会根据 <code>Content-Length</code> 头的值，仅传输其指定的字节数的 payload。payload 的剩余部分会被丢弃。参见 <a href="https://docs.byteplus.com/en/docs/18/20502#payload">Content\-Length 头如何影响 payload 的传输方式</a> 了解更多信息。</div>


<span id="使用限制"></span>
## 使用限制


* `fetch()` 方法发送的请求使用默认端口。HTTP 请求的默认端口为 80，HTTPS 请求的默认端口为 443。

* 请求地址中不允许包含 IP 地址。

* 请求地址中不能省略 scheme。例如 `fetch("www.example.com")` 是不正确的，您需要将其修改为 `fetch("https://www.example.com")`。


<span id="用法"></span>
## 用法

<span id="访问-byteplus-cdn-域名"></span>
### 访问 BytePlus CDN 域名

`fetch()` 默认通过互联网发送请求。如果 `fetch()` 方法访问的域名是 BytePlus CDN 域名，推荐您通过 `{proxy: "cdn"}` 参数配置 `fetch()` 方法通过边缘节点内部发送请求。由于边缘函数和 BytePlus CDN 共享边缘节点，函数发送的请求会在边缘节点内部被直接转发到 BytePlus CDN。

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">BytePlus CDN 域名是任意一个由 BytePlus CDN 提供内容分发服务的域名。域名在 BytePlus CDN 中的状态必须是 <strong>在线</strong>。</div>


例如，您可以使用以下方式请求 BytePlus CDN 域名 `cdn.example.com` 和第三方 API 服务域名 `api.example.com`：

```js
// 请求 BytePlus CDN 域名 cdn.example.com
const responseCDN = await fetch("https://cdn.example.com", { proxy: "cdn" });

// 请求第三方 API 服务域名 api.example.com
const responseAPI = await fetch("https://api.example.com");
```


下图展示了例子中传入 `{proxy: "cdn"}` 参数和不传入 `{proxy: "cdn"}` 参数所造成的请求路径差异：

<span>![图片](https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/upload_e0b83d3c4f38d9c7c09b64a8673fea6d.png) </span>

下表对比了传入 `{proxy: "cdn"}` 参数和不传入 `{proxy: "cdn"}` 参数的差异：


|差异项 |传入 `{proxy: "cdn"}` |不传入 `{proxy: "cdn"}` (默认) |
|---|---|---|
|**请求路径** |函数发送的请求会在边缘节点内部被直接转发到 BytePlus CDN。 |函数发送的请求会经由互联网，通过 DNS 解析被路由到一个边缘节点。该边缘节点不一定是函数执行所在的边缘节点。 |
|**费用** |不在 BytePlus CDN 侧产生流量费用。 |如果请求的域名是 BytePlus CDN 域名，经由互联网的请求会在 BytePlus CDN 侧产生流量费用。 |
|**适用场景** |仅适用于访问 BytePlus CDN 域名。如果请求的域名不是 BytePlus CDN 域名，请求将失败。`fetch()` 方法会返回 403 错误码。 |适用于访问除 BytePlus CDN 域名外，任何可通过互联网访问的域名。如果请求的域名是 BytePlus CDN 域名，请求可能会受限于域名的访问控制（如 IP 黑白名单、地理位置限制等）。 |


<span id="_3xx-跟随重定向"></span>
### 3xx 跟随重定向

您可以通过 `redirect` 参数配置 `fetch()` 方法如何处理 3xx 重定向。


* `{redirect: "manual"}`（默认）：表示不自动跟随 3xx 重定向。您可以手动处理重定向。

* `{redirect: "follow"}`：表示自动跟随 3xx 重定向。对于同一个请求，`fetch()` 方法默认会跟随最多 4 次重定向，并且允许跨域名和跨协议的重定向。

* `{redirect: "error"}`：表示在遇到 3xx 重定向时直接抛出错误。


下面的例子表示自动跟随 3xx 重定向：

```js
const response = await fetch("https://www.example.com", {redirect: "follow"});
```


针对不同状态码，`fetch()` 方法的重定向跟随行为如下：


|**状态码** |**重定向跟随行为** |
|---|---|
|301、302、303、308 |重定向的请求方法被更改为 GET 方法。请求的 body 内容被忽略。 |
|307 |只跟随 GET 方法。对于使用其他 HTTP 方法发起的请求，该方法不会自动跟随重定向并抛出错误。 |


重定向地址是从 `Location` 响应头中获取的。`Location` 响应头目前接受英文逗号 `,` 分割的列表，但是只有第一个 URL 会被选择跟随，其他 URL 会被忽略。

<span id="解压缩响应数据"></span>
### 解压缩响应数据

`fetch()` 方法目前仅支持解压缩 **gzip** 格式的响应数据。您可以使用 `decompression` 参数配置 `fetch()` 方法是否解压缩响应数据：

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip"><code>fetch()</code> 方法通过响应中的 <code>Content-Encoding</code> 头来识别压缩格式。例如：</div>



* <div data-tips="true" data-tips-type="tip">如果 <code>Content-Encoding</code> 为 <code>gzip</code> 或 <code>gzip, identity</code>，响应将被识别为 gzip 压缩。</div>


* <div data-tips="true" data-tips-type="tip">如果 <code>Content-Encoding</code> 为 <code>brotli, gzip</code>，<code>fetch()</code> 方法只会解压最外层的 gzip 压缩。</div>


* `manual`：**不解压缩**。直接返回原始的响应数据。

* `fallbackIdentity`：（默认）**自动解压缩**。对于不支持的压缩格式将返回原始数据。

* `decompress`：**自动解压缩**。对于不支持的压缩格式将抛出错误。


<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">解压缩后，<code>Content-Length</code> 响应头将不再准确反映数据大小。为了防止数据传输错误，运行时会删除此响应头，并添加 <code>X-Content-Length-Before-Decompression</code> 响应头来记录原始数据大小。</div>


以下示例演示了如何设置 `fetch()` 方法自动解压缩响应数据，并对于不支持的压缩格式返回原始数据：

```js
const response = await fetch("https://www.example.com", {decompression: "fallbackIdentity"});
```


<span id="解压缩后对-content-encoding-头的处理"></span>
#### 解压缩后对 `Content-Encoding` 头的处理

解压缩后，`fetch()` 方法会相应地修改 `Content-Encoding` 响应头：


* `Content-Encoding: identity, gzip` 将被修改为 `Content-Encoding: identity`。

* `Content-Encoding: gzip` 将被删除。

* `Content-Encoding: gzip, identity` 将被删除。

* `Content-Encoding: brotli, gzip` 将被修改为 `Content-Encoding:brotli`。


<span id="更多信息"></span>
## 更多信息

&nbsp;

<span id="content-length-头如何影响-payload-的传输方式"></span>
### Content\-Length 头如何影响 payload 的传输方式

`Request` 对象和 `Response` 对象中的 `Content-Length` 头会影响 payload 的传输方式：


* 如果 `Request` 对象或 `Response` 对象包含 `Content-Length` 头：

   * 如果 `Content-Length` 头的值是一个数字且大于或等于 0：运行时会根据 `Content-Length` 头的值，仅传输其指定的字节数的 payload。payload 的剩余部分会被丢弃。

   * 如果 `Content-Length` 头的值无效：运行时会忽略该 `Content-Length` 头，并使用分块传输编码（chunked transfer encoding）的方式传输 payload。

* 如果 `Request` 对象或 `Response` 对象不包含 `Content-Length` 头，运行时会使用分块传输编码的方式传输 payload。
