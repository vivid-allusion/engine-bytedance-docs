---
title: "nest envs"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/cli-ref-nest-env-cn"
---

管理本地函数的环境变量。

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">本命令需要您设置您的 BytePlus 账号的 Access Key ID 和 Secret Access Key。参见 <a href="https://docs.byteplus.com/docs/byteplus-cdn/edge-functions-cli-login-cn">设置您的 Access Key ID 和 Secret Access Key</a>。</div>


* <div data-tips="true" data-tips-type="tip">本命令需要在一个函数项目的根目录下运行。您需要使用 <a href="https://docs.byteplus.com/docs/byteplus-cdn/cli-ref-nest-init-cn">nest init</a> 创建一个函数项目。</div>


* <div data-tips="true" data-tips-type="tip">本地函数的环境变量不保存在本地。边缘函数 CLI 在边缘函数服务端管理本地函数的环境变量。因此，在运行本命令时，确保您的本地函数需要有一个函数 ID。</div>



<span id="子命令"></span>
## 子命令

<span id="list"></span>
### list

```shell
npx nest envs list --function <function_ID_or_name> --save-dev
```


获取本地函数的环境变量列表。


* `<function_id>`：*string，optional*

   * 函数 ID。默认为 [本地函数列表](https://docs.byteplus.com/docs/byteplus-cdn/cli-ref-nest-function-cn#list) 中的默认函数。

* `<--save-dev>`：*boolean，optional*

   * 是否把环境变量保存到本地用于调试。默认不保存到本地。


```shell
$ npx nest envs list
+------+--------+
| KEY  | VALUE  |
+------+--------+
| key1 | value1 |
| key2 | value2 |
+------+--------+
```


<span id="set"></span>
### set

```shell
npx nest envs set <key> <value> --function <function_id_or_name>
```


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">您对环境变量的增删改操作在函数被再次发布后才会生效。</div>


设置环境变量的值。


* `<key>`：*string，required*

   * 环境变量的键。

* `<value>`：*string，required*

   * 环境变量的值。

* `<function_id_or_name>`：*string，optional*

   * 函数 ID 或函数名称。该参数是一个全局参数。参见 [--function](https://docs.byteplus.com/docs/byteplus-cdn/edge-functions-global-f-cn)。默认为 [本地函数列表](https://docs.byteplus.com/docs/byteplus-cdn/cli-ref-nest-function-cn#list) 中的默认函数。如果您通过函数名称指定的本地函数还没有函数 ID，边缘函数 CLI 会返回错误 `Error: function id required`。


<span id="delete"></span>
### delete

```shell
npx nest envs set <key> --function <function_id_or_name>
```


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">您对环境变量的增删改操作在函数被再次发布后才会生效。</div>


删除环境变量。


* `<key>`：*string，required*

   * 环境变量的键。

* `<function_id_or_name>`：*string，optional*

   * 函数 ID 或函数名称。该参数是一个全局参数。参见 [--function](https://docs.byteplus.com/docs/byteplus-cdn/edge-functions-global-f-cn)。默认为 [本地函数列表](https://docs.byteplus.com/docs/byteplus-cdn/cli-ref-nest-function-cn#list) 中的默认函数。如果您通过函数名称指定的本地函数还没有函数 ID，边缘函数 CLI 会返回错误 `Error: function id required`。
