---
title: "nest tickets"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/cli-ref-nest-ticket-cn"
---

获取本地函数代码的发布记录。

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">本命令需要您设置您的 BytePlus 账号的 Access Key ID 和 Secret Access Key。参见 <a href="https://docs.byteplus.com/docs/byteplus-cdn/edge-functions-cli-login-cn">设置您的 Access Key ID 和 Secret Access Key</a>。</div>


* <div data-tips="true" data-tips-type="tip">本命令需要在一个函数项目的根目录下运行。您需要使用 <a href="https://docs.byteplus.com/docs/byteplus-cdn/cli-ref-nest-init-cn">nest init</a> 创建一个函数项目。</div>


* <div data-tips="true" data-tips-type="tip">本地函数的发布历史不保存在本地。边缘函数 CLI 在边缘函数服务端管理本地函数的发布历史。因此，在运行本命令时，确保您的本地函数需要有一个函数 ID。</div>



<span id="概述"></span>
## 概述

```shell
npx nest tickets -d <description> --function <function_id_or_name> --page <page_number> --desc
```


获取函数代码的发布记录列表。


* `<description>`：*string，optional*

   * 版本描述。

* `<function_id_or_name>`：*string，optional*

   * 函数 ID 或函数名称。该参数是一个全局参数。参见 [--function](https://docs.byteplus.com/docs/byteplus-cdn/edge-functions-global-f-cn)。默认为 [本地函数列表](https://docs.byteplus.com/docs/byteplus-cdn/cli-ref-nest-function-cn#list) 中的默认函数。如果您通过函数名称指定的本地函数还没有函数 ID，边缘函数 CLI 会返回错误 `Error: function id required`。

* `<page_number>`：*integer，optional*

   * 列表分页显示的页码。默认为 1。

* `--desc`：*boolean，optional*：

   * 按版本号降序排序。默认为按版本号升序排序。


```shell
$ npx nest tickets
+---------+------------+----------------------+-------------+
| VERSION | SCRIPTNAME |       CREATOR        | DESCRIPTION |
+---------+------------+----------------------+-------------+
| 1.0.2   | default    | ******************** |             |
| 1.0.1   | default    | ******************** |             |
+---------+------------+----------------------+-------------+
```


<span id="子命令"></span>
## 子命令

<span id="get"></span>
### get

```shell
npx nest tickets get <version> --function <function_id_or_name>
```



* `<version>`：*string，required*

   * 函数代码的版本。您可以通过 `npx nest versions list` 获取函数代码的版本。

* `<function_id_or_name>`：*string，optional*

   * 函数 ID 或函数名称。该参数是一个全局参数。参见 [--function](https://docs.byteplus.com/docs/byteplus-cdn/edge-functions-global-f-cn)。默认为 [本地函数列表](https://docs.byteplus.com/docs/byteplus-cdn/cli-ref-nest-function-cn#list) 中的默认函数。如果您通过函数名称指定的本地函数还没有函数 ID，边缘函数 CLI 会返回错误 `Error: function id required`。


```shell
$ npx nest versions get 1.0.2
(() => {
  // src/index.js
  addEventListener("fetch", (event) => {
    event.respondWith(upgradeToSSL(event));
  });
  async function upgradeToSSL(event) {
    const incommingRequest = event.request;
    const url = new URL(incommingRequest.url);
    if (url.protocol == "http:") {
      url.protocol = "https";
      return fetch(url.toString(), {
        method: incommingRequest.method,
        headers: incommingRequest.headers,
        body: incommingRequest.body
      });
    } else {
      return fetch(incommingRequest);
    }
  }
})();
```
