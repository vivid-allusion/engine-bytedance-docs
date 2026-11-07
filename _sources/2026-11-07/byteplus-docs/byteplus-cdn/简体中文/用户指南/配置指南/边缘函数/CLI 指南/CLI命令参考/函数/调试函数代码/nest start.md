---
title: "nest start"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/cli-ref-nest-start-cn"
---

运行函数代码。

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">您无需设置 Access Key ID 和 Secret Access Key 就可以运行本命令。</div>


* <div data-tips="true" data-tips-type="tip">本命令需要在一个函数项目的根目录下运行。您需要使用 <a href="https://docs.byteplus.com/docs/byteplus-cdn/cli-ref-nest-init-cn">nest init</a> 创建一个函数项目。</div>


* <div data-tips="true" data-tips-type="tip">与 <a href="https://docs.byteplus.com/docs/byteplus-cdn/cli-ref-nest-debug-cn">nest debug</a> 不同，您更新代码文件后，新的代码文件会被自动同步到边缘函数 Debugger。</div>



<span id="概要"></span>
## 概要

```shell
npx nest start <address> --proxyHost <hostname>
```


<span id="描述"></span>
## 描述


* `<address>`：*string，optional*

   * 本地代理的 IP 地址。默认为 `127.0.0.1`。

* `<hostname>`：*string，optional*

   * 您向 Debugger 发送的 HTTP 请求的域名。默认为 `example.com`。


您运行 `npx nest start` 后，边缘函数 CLI 会为边缘函数 Debugger 启动一个本地 HTTP 代理，并通过 wss 协议与边缘函数 Debugger 建立连接。您通过 cURL 等工具向该地址发送 HTTP 请求时，函数的域名触发器会触发 fetch 事件。

```shell
$ npx nest start
==> Setting up debugger...
==> [info]: connection setup successfully!
==> [info]: loading envrionment variables... ✔
==> [info]: building script "default"...
==> [info]: uploading script 'default': **********/output/index.js... ✔
==> Local http proxy running on http://127.0.0.1:18080
```


您可以使用 cURL 或浏览器等工具向本地代理发送 HTTP 请求并获取函数响应。

```shell
$ curl -s http://127.0.0.1:18080
Hello World!
```
