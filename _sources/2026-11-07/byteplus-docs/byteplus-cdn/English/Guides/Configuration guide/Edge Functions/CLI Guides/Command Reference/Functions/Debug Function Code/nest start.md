---
title: "nest start"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/cli-ref-nest-start-en"
---

Runs function code.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">You don't need to set up an access key ID and secret access key to run this command.</div>


* <div data-tips="true" data-tips-type="tip">This command needs to be run in the root directory of a function project. You need to use <code>nest init</code> to create a function project.</div>


* <div data-tips="true" data-tips-type="tip">Unlike <code>nest debug</code>, when you update a code file, the new code file is automatically synchronized to the Edge Functions Debugger.</div>



<span id="synopsis"></span>
## Synopsis

```shell
npx nest start <address> --proxyHost <hostname>
```


<span id="description"></span>
## Description

After you run `npx nest start`, the Edge Functions CLI will start a local HTTP proxy for the Edge Functions Debugger, and establish a connection with the Edge Functions Debugger using the wss protocol. When you send HTTP requests to this address using tools like cURL, the function's domain trigger will trigger a fetch event.


* `<address>`: *string, optional*

   * The IP address of the local proxy. Default is `127.0.0.1`.

* `<hostname>`: *string, optional*

   * The hostname of the request URL. Default is `example.com`.


```shell
$ npx nest start
==> Setting up debugger...
==> [info]: connection setup successfully!
==> [info]: loading envrionment variables... ✔
==> [info]: building script "default"...
==> [info]: uploading script 'default': **********/output/index.js... ✔
==> Local http proxy running on http://127.0.0.1:18080
```


You can use tools like cURL or a browser to send HTTP requests to the local proxy and receive function responses.

```shell
$ curl -s http://127.0.0.1:18080
Hello World!
```
