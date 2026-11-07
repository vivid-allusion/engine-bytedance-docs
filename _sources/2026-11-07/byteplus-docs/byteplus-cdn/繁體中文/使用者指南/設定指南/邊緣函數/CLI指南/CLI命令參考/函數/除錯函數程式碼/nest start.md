---
title: "nest start"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/cli-ref-nest-start-cn-zh-tw"
---

執行函數程式碼。

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">您無需設定 Access Key ID 和 Secret Access Key 就可以執行本指令</div>


* <div data-tips="true" data-tips-type="tip">本指令需要在一個函數專案的根目錄下執行。您需要使用 <a href="https://docs.byteplus.com/docs/byteplus-cdn/cli-ref-nest-init-cn-zh-tw">nest init</a> 建立一個函數專案</div>


* <div data-tips="true" data-tips-type="tip">與 <a href="https://docs.byteplus.com/docs/byteplus-cdn/cli-ref-nest-debug-cn-zh-tw">nest debug</a> 不同，您更新程式碼檔案後，新的程式碼檔案會被自動同步到邊緣函數 Debugger</div>



<span id="概要"></span>
## 概要

```shell
npx nest start <address> --proxyHost <hostname>
```


<span id="描述"></span>
## 描述


* `<address>`：*string，optional*

   * 本地代理的 IP 位址。預設為 `127.0.0.1`

* `<hostname>`：*string，optional*

   * 您向 Debugger 傳送的 HTTP 請求的網域名稱。預設為 `example.com`


您執行 `npx nest start` 後，邊緣函數 CLI 會為邊緣函數 Debugger 啟動一個本地 HTTP 代理，並透過 wss 協定與邊緣函數 Debugger 建立連線。您透過 cURL 等工具向該位址傳送 HTTP 請求時，函數的網域名稱觸發器會觸發 fetch 事件

```shell
$ npx nest start
==> Setting up debugger...
==> [info]: connection setup successfully!
==> [info]: loading envrionment variables... ✔
==> [info]: building script "default"...
==> [info]: uploading script 'default': **********/output/index.js... ✔
==> Local http proxy running on http://127.0.0.1:18080
```


您可以使用 cURL 或瀏覽器等工具向本地代理傳送 HTTP 請求並取得函數回應

```shell
$ curl -s http://127.0.0.1:18080
Hello World!
```
