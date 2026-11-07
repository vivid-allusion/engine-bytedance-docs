---
title: "HTTP 响应头设置"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/docs_cn-cdn-response-headers-cn"
---

本文档介绍如何在 BytePlus CDN 中配置 HTTP 响应头。

默认情况下，在对用户请求的响应中，CDN 会包含源站响应中的所有头部。您可以配置 CDN 在用户请求的响应中所包含的头部。

<span id="操作步骤"></span>
## 操作步骤


1. 打开 **HTTP 响应头设置** 配置页面。操作步骤参见 [域名配置](https://docs.byteplus.com/en/docs/byteplus-cdn/domain-management_zh-cn)。

2. 点击 **添加规则**。

   您最多可以添加 50 条规则。

3. 参照以下配置说明。

4. 配置完成后，点击 **保存**。


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/3d438a73a54d4da29a439f3249b4fd45~tplv-goo7wpa0wc-topic.webp) </span>

<span id="配置说明"></span>
## 配置说明


|**配置** |**说明** |
|---|---|
|响应头操作 |表示一个操作类型。该配置有以下选项：<br><br><br>* **设置**：表示设置一个头部。设置操作包括添加与修改。如果源站响应中已包含该头部，该头部的值会被覆盖。如果源站响应中没有包含该头部，该头部会被添加。<br><br>* **删除**：表示删除一个头部。 |
|响应头名称 |表示需要设置或者删除的一个头部。头部名称是大小写不敏感的。您可以从下拉列表中选择一个常用头部，参见 [常用头部](https://docs.byteplus.com/docs/byteplus-cdn/docs_cn-cdn-response-headers-cn#%E5%B8%B8%E7%94%A8%E5%A4%B4%E9%83%A8)。除了 [注意事项](https://docs.byteplus.com/docs/byteplus-cdn/docs_cn-cdn-response-headers-cn#%E6%B3%A8%E6%84%8F%E4%BA%8B%E9%A1%B9) 中列出的那些头部名称之外，您可以输入任意一个头部名称。头部名称不能超过 1,024 个字符，不能包含以下字符：<br><br><br>* 汉字、下划线（_）、空格、双引号（"）、冒号（:） |
|取值方式 |对于您在 **响应头名称** 中指定头部，该配置表示该头部值的类型，有以下选项：<br><br><br>* **常量值**：表示该头部值是一个字符串。<br><br>* **变量**：表示该头部值来自一个变量。<br><br>* **自定义**：表示该头部值是变量与字符串拼接后的一个字符串。 |
|响应请求头的值 |表示您在 **响应头名称** 中指定头部的取值。<br><br><br>* 如果 **取值方式** 是 **常量值**，您需要输入一个字符串。该字符串的长度不能超过 1,024 个字符，不能包含以下字符：<br><br>   * 汉字、下划线（_）、空格、双引号（"）、冒号（:）<br><br>* 如果 **取值方式** 是 **变量**，您需要从列表中选择一个变量。参见 [变量列表](https://docs.byteplus.com/docs/byteplus-cdn/docs_cn-cdn-response-headers-cn#%E5%8F%98%E9%87%8F%E5%88%97%E8%A1%A8)。<br><br>* 如果 **取值方式** 是 **自定义**，您需要输入由变量和字符串拼接后的一个字符串。变量需要包裹在 `{}` 中，由 `$` 开头。例如 `bind${remote_addr}to${host}done`。<br><br><br>如果 **响应头名称** 是 `Access-Control-Allow-Origin`，您可以在 **响应请求头的值** 中输入多个以逗号（,）分隔的来源 IP 和来源域名，表示允许访问您域名的来源 IP 和来源域名。域名可以是泛域名。 |
|跨域校验 |此配置项决定 CDN 是否根据请求头中的 `Origin` 字段来进行跨域校验。该配置项仅在满足以下两个条件时才会出现：<br><br><br>* **头部名称** 为 `Access-Control-Allow-Origin`。<br><br>* **取值方式** 为 **常量**。<br><br><br>`Access-Control-Allow-Origin` 的值支持以下格式：<br><br><br>* **任意来源**：设置为 `*`。<br><br>* **特定来源**：设置单个或多个 IP、域名，或者 IP 与域名的组合。多个来源之间用逗号（,）分隔。来源必须包含协议头 `http://` 或 `https://`，且支持携带端口。<br><br>* **泛域名**：域名支持泛域名格式，例如 `https://*.example.com`。<br><br><br>启用 **跨域校验** 后，CDN 的处理逻辑如下：<br><br><br>* **任意匹配**：如果头部取值设置为 `*`，无论请求中是否携带 `Origin` 头部，也不论 `Origin` 头部的值为何，CDN 都会在响应中返回 `Access-Control-Allow-Origin: *`。<br><br>* **精确匹配**：如果头部取值设置为单个或多个具体的来源，CDN 会检查请求头中的 `Origin` 值是否与设置的任意一个来源精确匹配。<br><br>   * 如果匹配成功，CDN 会在响应中返回 `Access-Control-Allow-Origin` 头部，该头部的值为请求中的 `Origin` 头部的值。<br><br>   * 如果匹配失败，CDN 不会在响应中返回 `Access-Control-Allow-Origin` 头部。<br><br>* **泛域名匹配**：如果头部取值设置了泛域名，CDN 会检查请求头中的 `Origin` 值是否匹配该泛域名。匹配后的处理逻辑与精确匹配相同。<br><br><br>如果不启用 **跨域校验**，CDN 不会检查请求中的 `Origin` 头部，始终将您配置的 `Access-Control-Allow-Origin` 头部添加到响应中。<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">如果 <code>Access-Control-Allow-Origin</code> 的值包含多个来源，强烈建议您开启 <strong>跨域校验</strong>。如果不开启，CDN 会将所有来源作为头部值返回，而浏览器通常只允许 <code>Access-Control-Allow-Origin</code> 包含一个值，导致浏览器报错。</div><br> |


<span id="变量列表"></span>
## 变量列表

CDN 提供了以下变量。


|变量名称 |说明 |示例 |
|---|---|---|
|raw_uri |表示客户端请求 URL 中的路径。 |`/dir/sample.php` |
|request_uri |表示客户端请求 URL 中的路径和查询字符串（query string）。 |`/dir/sample.php?color=red&n=10` |
|remote_addr |表示发起本次请求的客户端的 IP 地址。 |`10.10.10.10` |
|remote_port |表示发起本次请求的客户端的端口。 |`5936` |
|host |表示客户端请求中 host 头部的值。<br><br>&nbsp;<br><br>&nbsp;<br><br>需要留意的是，CDN 在处理请求时可能会修改该头部的值。因此，不建议您使用该头部，而是使用 `http_host`。 |`www.example.com:8080` |
|http_host |表示客户端请求中 host 头部的值。该头部值不会被 CDN 修改。 | |
|args |表示客户端请求 URL 中的查询字符串。 |`color=red&n=10` |
|msec |表示 CDN 设置响应头的时间，格式是 Unix 时间戳，精确到毫秒。该时间戳接近首包的响应时间。 |`1704444754.917` |
|scheme |表示客户端使用的协议。 |`https` |
|cdn_cache_status |表示请求是否命中缓存。<br><br><br>* `edge_hit`：表示请求命中了边缘节点的缓存。<br><br>* `parent_hit`：表示请求命中了回源节点的缓存。<br><br>* `miss`：表示请求没有命中缓存。 |`edge_hit` |


<span id="常用头部"></span>
## 常用头部

CDN 提供了以下常用的头部。

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">这些头部是标准的 HTTP 响应头。如果响应头的值是合法的，客户端浏览器会根据响应头做相应的操作。</div>



|**头部名称** |**说明** |**示例** |
|---|---|---|
|Access\-Control\-Allow\-Origin |指定允许访问您站点资源的来源（Origin）。<br><br><br>* 多个来源使用逗号（,）分隔。<br><br>* 您可以指定 `*`，表示任意来源。<br><br>* 来源中的 host 可以是 IP 地址，也可以是域名。域名可以是泛域名。<br><br>* 来源可以包含端口。<br><br>* 如果您指定的来源不是 `*` 并且 **跨域校验** 为启用，则来源必须符合 URL 规范，也就是说来源必须包含 scheme 和 host。 |示例一<br><br>`*`<br><br>示例二<br><br>`https://www.another-site.com:448,http://10.10.10.10,https://*.example.com` |
|Access\-Control\-Allow\-Methods |指定跨域请求允许使用的 HTTP 请求方法。多个方法使用逗号（,）分隔。 |`GET` |
|Access\-Control\-Allow\-Headers |指定跨域请求允许包含的 HTTP 请求头。多个请求头使用逗号（,）分隔。 |`X-Custom-Header` |
|Access\-Control\-Expose\-Headers |指定在客户端运行的脚本所允许访问的响应头。多个响应头使用逗号（,）分隔。<br><br>&nbsp;<br><br>&nbsp;<br><br>默认情况下，客户端脚本可以访问的响应头有 `Cache-Control`、`Content-Language`、`Content-Type`、`Expires`、`Last-Modified`。如果您需要客户端脚本访问更多的响应头，可以在该头部中指定。 |`Content-Encoding` |
|Access\-Control\-Allow\-Credentials |指定跨域请求是否需要包含鉴权信息。鉴权信息包括 cookie，鉴权请求头或客户端 TLS 证书。 |`true` |
|Access\-Control\-Max\-Age |指定跨域请求时，客户端对请求内容发起的预检请求的缓存时长。单位是秒。在缓存过期前，客户端不用再次发送预检请求。 |`3600` |
|Cache\-Control |对于 CDN 返回的内容，指定该内容在客户端的缓存方式。 |`max-age=3600` |
|Content\-Disposition |指示 CDN 返回给客户端的内容是以下载的方式提供。并指定下载的文件名。 |`attachment;filename=Demo.xlsx` |
|Content\-Language |指示 CDN 返回给客户端的内容语言。 |`zh-CN` |
|Content\-Type |指示 CDN 返回给客户端的内容类型。 |`text/plain` |
|Pragma |对于 HTTP/1.0，指示 CDN 响应在客户端的缓存方式。头部值只能是 `no-cache`，指示客户端不要缓存 CDN 的响应。 |`no-cache` |


<span id="注意事项"></span>
## 注意事项

您设置的响应头名称不能是以下任意头部。


* access\-check

* server\-timing

* via

* x\-request\-ip

* x\-tt\-trace\-tag

* x\-bdcdn\-logid

* byte\-error\-code

* x\-bdcdn\-cache\-status
