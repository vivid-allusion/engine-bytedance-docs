---
title: "HTTP 请求头"
product: "BytePlus MediaLive"
product_code: "byteplus-media-live"
source: "https://docs.byteplus.com/en/docs/byteplus-media-live/docs-http-request-headers-zh-CN"
---

要向源站传递特定信息（如客户端类型或认证信息），可以在拉流回源任务中添加自定义 HTTP 请求头。本主题介绍如何为拉流域名配置这些请求头。配置完成后，该域名的所有拉流回源请求将自动包含指定的请求头，从而实现与源站更灵活且安全的通信。关于拉流回源的更多信息，请参见[配置拉流回源任务](https://docs.byteplus.com/docs/byteplus-media-live/docs-configuring-origin-pull-settings)。

HTTP 请求头由客户端（如浏览器）在发送 HTTP 请求时自动添加，用于向服务器提供额外信息，例如客户端类型、语言和偏好设置。例如，可以设置`Accept` 字段以指定客户端可接受的响应类型。

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">请求头字段匹配不区分大小写。如果原始请求头中已存在该字段，新字段值将覆盖原有字段值。</div>


<span id="37a45946"></span>
## 适用范围

拉流域名。

<span id="7372d48b"></span>
## 前提条件

已添加拉流域名。更多信息，请参见[添加域名](https://docs.byteplus.com/docs/byteplus-media-live/docs-domain-zh-CN)。

<span id="c7be96cf"></span>
## 操作步骤


1. 登录 [BytePlus MediaLive 控制台](https://console.byteplus.com/live)。

2. 在左侧导航栏，点击**域名**。

3. 找到需要查看的域名，在**操作**列点击**设置**。

4. 点击**拉流回源**标签页。

5. 在**HTTP 请求头**开关右侧，点击**编辑**。

6. 在**HTTP 请求头设置**对话框中，添加所需的请求头。

   * **参数**：最多可添加 20 个请求头。请求头名称不能超过 1024 个字符。

   * **值**：可将常量或变量指定为请求头值。

      * 常量不能超过 1024 个字符。

      * 对于变量，可以从下拉列表中选择预定义变量，或手动输入变量。

         支持的变量包括：

      
      |**变量** |**描述** |**示例值** |
      |---|---|---|
      |$ |表示拉流回源请求的源站主机名。 |example.com |
      |$ |表示拉流回源请求中不包含查询参数的路径。如果请求被重写，该变量表示重写后的路径。 |`/dir/sample.php` |
      |$ |表示拉流回源请求中的查询参数。如果请求被重写，该变量表示重写后的参数。 |`color=red&n=10` |
      |$ |表示发送请求的客户端 IP 地址。 |`192.0.2.1` |
      

7. 点击**确认**。
