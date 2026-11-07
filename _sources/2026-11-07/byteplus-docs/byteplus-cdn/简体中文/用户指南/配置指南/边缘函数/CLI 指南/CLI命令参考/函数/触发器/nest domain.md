---
title: "nest domain"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/cli-ref-nest-domain-cn"
---

管理本地函数关联的域名。

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">本命令需要您设置您的 BytePlus 账号的 Access Key ID 和 Secret Access Key。参见 <a href="https://docs.byteplus.com/docs/byteplus-cdn/edge-functions-cli-login-cn">设置您的 Access Key ID 和 Secret Access Key</a>。</div>


* <div data-tips="true" data-tips-type="tip">本命令需要在一个函数项目的根目录下运行。您需要使用 <a href="https://docs.byteplus.com/docs/byteplus-cdn/cli-ref-nest-init-cn">nest init</a> 创建一个函数项目。</div>


* <div data-tips="true" data-tips-type="tip">本地函数所关联的域名信息不保存在本地。边缘函数 CLI 在边缘函数服务端管理本地函数关联的域名。因此，在运行本命令时，确保您的本地函数需要有一个函数 ID。</div>



<span id="描述"></span>
## 描述

当用户通过 HTTP 或 HTTPS 请求访问函数关联的域名，且用户请求与域名的转发规则匹配时，域名触发器会触发函数代码中的 fetch 事件。您需要在代码中监听并处理 fetch 事件。

一个函数可以关联一个或多个域名。每个域名也可以关联多个函数。参见 [使用限制](https://docs.byteplus.com/docs/byteplus-cdn/functions-usage-limits)。

<span id="子命令"></span>
## 子命令

<span id="list"></span>
### list

```shell
npx nest domain list --all --function <function_id> -page <page_number> --desc
```


查看本地函数关联的域名。


* `--all`：*boolean，optional*

   * 查看所有域名。默认仅查看本地函数已关联的域名。

* `<function_id_or_name>`：*string，optional*

   * 函数 ID 或函数名称。该参数是一个全局参数。参见 [--function](https://docs.byteplus.com/docs/byteplus-cdn/edge-functions-global-f-cn)。默认为 [本地函数列表](https://docs.byteplus.com/docs/byteplus-cdn/cli-ref-nest-function-cn#list) 中的默认函数。如果您通过函数名称指定的本地函数还没有函数 ID，边缘函数 CLI 会返回错误 `Error: function id required`。

* `<page_number>`：*integer，optional*

   * 列表分页显示的页码。默认为 1。

* `--desc`：*boolean，optional*：

   * 按域名降序排序。默认为按域名升序排序。


您运行 `npx nest domain list` 后，可以查看域名、状态和转发规则的信息。

```Plain Text
$ npx nest domain list

+-----------------------------+--------+-----------+-----------+------------+
|           DOMAIN            | STATUS |   TYPE    |  PATTERN  | IGNORECASE |
+-----------------------------+--------+-----------+-----------+------------+
| a.example.com               | Online | directory | /welcome/ | false      |
+-----------------------------+--------+-----------+-----------+------------+
```


您运行 `npx nest domain list --all` 后，可以在 STATUS 列查看域名是否可以被函数关联。

```shell
$ npx nest domain list --all

+--------------------------------------+-----------------+
|                DOMAIN                |     STATUS      |
+--------------------------------------+-----------------+
| a.example.com                        | Can be Bound    |
| a.example.org                        | Cannot be Bound |
+--------------------------------------+-----------------+
```


<span id="bind"></span>
### bind

```shell
npx nest domain bind <domain_name> --function <function_id> --url-directory <url_directory> --ignore-case

npx nest domain bind <domain_name> --function <function_id> --url-ext <url_ext> --ignore-case

npx nest domain bind <domain_name> --function <function_id> --url-match <url> --ignore-case
```


为本地函数关联一个域名。

您可以使用以下参数为域名配置转发规则。只有匹配转发规则的用户请求才能被转发到边缘函数。参见 [域名触发器](https://docs.byteplus.com/docs/byteplus-cdn/docs_cn-domain-triggers-cn) 了解如何配置转发规则。


* `<domain_name>`：*string，required*

   * 域名。

* `<function_id_or_name>`：*string，optional*

   * 函数 ID 或函数名称。该参数是一个全局参数。参见 [--function](https://docs.byteplus.com/docs/byteplus-cdn/edge-functions-global-f-cn)。默认为 [本地函数列表](https://docs.byteplus.com/docs/byteplus-cdn/cli-ref-nest-function-cn#list) 中的默认函数。如果您通过函数名称指定的本地函数还没有函数 ID，边缘函数 CLI 会返回错误 `Error: function id required`。

* `<url_directory>`：*string，optional*

   * 规则类型是 URL 目录。规则应用于指定目录下的所有文件。您必须设置 `<url_directory>`、`<url_ext>` 或 `<url>` 其中之一。

* `<url_ext>`：*string，optional*

   * 规则类型是文件后缀。规则应用于具有指定后缀名的所有文件。您必须设置 `<url_directory>`、`<url_ext>` 或 `<url>` 其中之一。

* `<url>`：*string，optional*

   * 规则类型是 URL 全路径。规则应用于指定文件。您必须设置 `<url_directory>`、`<url_ext>` 或 `<url>` 其中之一。

* `--ignore-case`：*boolean，optional*

   * 忽略大小写。默认不忽略大小写。


例如，下面的命令为本地函数关联域名 `www.example.com`，并把转发规则的类型设置为 URL 目录。如果用户请求的 URL 目录是 `/welcome/`，例如 `https://www.example.com/welcome/a.png`，则该请求匹配转发规则。

```shell
npx nest domain bind www.example.com --url-directory /welcome/
```


您可以运行 `npx nest domain list` 查看域名是否被关联。

```Plain Text
$ npx nest domain list

+-----------------------------+--------+-----------+-----------+------------+
|           DOMAIN            | STATUS |   TYPE    |  PATTERN  | IGNORECASE |
+-----------------------------+--------+-----------+-----------+------------+
| www.example.com             | Online | directory | /welcome/ | false      |
+-----------------------------+--------+-----------+-----------+------------+
```


<span id="unbind"></span>
### unbind

```shell
npx nest domain unbind <domain_name> --function <function_id>
```


将域名与本地函数取消关联。


* `<domain_name>`：*string，required*

   * 需要取消关联的域名。

* `<function_id_or_name>`：*string，optional*

   * 函数 ID 或函数名称。该参数是一个全局参数。参见 [--function](https://docs.byteplus.com/docs/byteplus-cdn/edge-functions-global-f-cn)。默认为 [本地函数列表](https://docs.byteplus.com/docs/byteplus-cdn/cli-ref-nest-function-cn#list) 中的默认函数。如果您通过函数名称指定的本地函数还没有函数 ID，边缘函数 CLI 会返回错误 `Error: function id required`。


您可以运行 `npx nest domain list` 查看域名是否被取消关联。

```Plain Text
$ npx nest domain list

+-----------------------------+--------+-----------+-----------+------------+
|           DOMAIN            | STATUS |   TYPE    |  PATTERN  | IGNORECASE |
+-----------------------------+--------+-----------+-----------+------------+
+-----------------------------+--------+-----------+-----------+------------+
```
