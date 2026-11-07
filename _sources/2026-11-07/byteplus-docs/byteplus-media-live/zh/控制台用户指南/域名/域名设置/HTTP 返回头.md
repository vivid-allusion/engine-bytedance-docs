---
title: "HTTP 返回头"
product: "BytePlus MediaLive"
product_code: "byteplus-media-live"
source: "https://docs.byteplus.com/en/docs/byteplus-media-live/docs-http-response-headers-zh-CN"
---

你可以为边缘服务器发送给客户端的返回调用结果添加自定义 HTTP 头部。完成配置后，这些头部将应用于发送到该域名的所有请求的返回调用结果。

HTTP 返回头是一组在主要返回调用结果体之前由服务器发送的字段。这些字段提供关于返回调用结果的元数据，例如状态码、内容类型、缓存控制规则、Content\-Encoding 和 Content\-Disposition。通过配置合适的 HTTP 返回头，可以增强安全性、优化性能、提升用户体验，并满足合规性或浏览器交互需求。

默认情况下，我们的缓存节点在处理用户拉流请求时会透传来自你的源站的返回头。该功能允许你配置、添加或修改这些返回头参数。

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">返回头字段匹配不区分大小写。如果原始返回头中已存在该字段，则新字段值会覆盖原字段值。</div>


<span id="ba3aed7d"></span>
## 适用范围

拉流域名。

<span id="437cee91"></span>
## 前提条件

你已添加拉流域名。更多信息，请参见[添加域名](https://docs.byteplus.com/docs/byteplus-media-live/docs-domain-zh-CN)。

<span id="d55ece96"></span>
## 操作步骤


1. 登录[BytePlus MediaLive 控制台](https://console.byteplus.com/live)。

2. 在左侧导航栏，点击**域名**。

3. 找到你要查看的域名，在**操作**列点击**设置**。

4. 点击**访问控制**标签页。

5. 在**HTTP 返回头**开关右侧点击**编辑**。

6. 在弹出的**HTTP 返回头设置**对话框中，按需添加返回头。

   * **参数**：从下拉列表中选择常用头部，或自定义输入。最多可添加 20 个头部。头部名称不能超过 1024 个字符。

      你可以从下拉列表中选择以下参数：

      
      |**参数** |**接口行为** |**示例** |
      |---|---|---|
      |Content\-Type |返回给客户端的内容类型。 |`text/plain` |
      |Cache\-Control |用于控制缓存行为的指令。 |`max-age=3600` |
      |Content\-Disposition |返回给客户端的下载文件名。 |`attachment;filename=Demo.xlsx` |
      |Content\-Language |返回给客户端的内容语言。 |`zh-CN` |
      |Expires |返回对象的过期时间。 |`Wed, 21 Oct 2015 07:28:00 GMT` |
      |Access\-Control\-Allow\-Origin |可被跨域请求访问的来源。 |`https://www.another-site.com` |
      |Access\-Control\-Allow\-Headers |跨域请求可包含的请求头。 |`X-Custom-Header` |
      |Access\-Control\-Allow\-Methods |可用于跨域请求的请求方式。 |`GET` |
      |Access\-Control\-Max\-Age |预检请求结果可被缓存的时长。 |`3600` |
      |Access\-Control\-Expose\-Headers |跨域请求中客户端可访问的返回头。 |`Content-Encoding`。如需客户端访问更多返回头，可在此字段中指定。多个返回头用英文逗号（,）分隔。 |
      

   * **值**：指定常量或变量作为头部值。

      * 常量不能超过 1024 个字符。

      * 对于变量，可以从下拉列表中选择常用变量，或手动输入变量。

         你可以从下拉列表中选择以下变量：

         
         |**变量** |**接口行为** |**示例值** |
         |---|---|---|
         |$ |表示客户端请求中的域名。 |example.com |
         |$ |表示客户端请求路径（不含查询参数）。如果客户端请求被重写，该变量表示重写后的路径。 |`/dir/sample.php` |
         |$ |表示客户端请求中的查询参数。如果客户端请求被重写，该变量表示重写后的参数。 |`color=red&n=10` |
         |$ |表示发送请求的客户端的 IP 地址。 |`192.0.2.1` |
         |$ |表示响应客户端请求的边缘服务器的 IP 地址。 |`192.0.2.1` |
         

7. 点击**确认**。
