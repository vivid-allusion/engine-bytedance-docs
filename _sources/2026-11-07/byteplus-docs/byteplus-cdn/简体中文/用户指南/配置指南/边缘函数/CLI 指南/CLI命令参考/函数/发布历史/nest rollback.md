---
title: "nest rollback"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/cli-ref-nest-rollback-cn"
---

将本地函数的代码回滚到您指定的版本。

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">本命令需要您设置您的 BytePlus 账号的 Access Key ID 和 Secret Access Key。参见 <a href="https://docs.byteplus.com/docs/byteplus-cdn/edge-functions-cli-login-cn">设置您的 Access Key ID 和 Secret Access Key</a>。</div>


* <div data-tips="true" data-tips-type="tip">本命令需要在一个函数项目的根目录下运行。您需要使用 <a href="https://docs.byteplus.com/docs/byteplus-cdn/cli-ref-nest-init-cn">nest init</a> 创建一个函数项目。</div>


* <div data-tips="true" data-tips-type="tip">本地函数的发布历史不保存在本地。边缘函数 CLI 在边缘函数服务端管理本地函数的发布历史。因此，在运行本命令时，确保您的本地函数需要有一个函数 ID。</div>



<span id="概述"></span>
## 概述

```shell
npx nest rollback <version> --canary -d <description> -f <function_id> 
```


<span id="描述"></span>
## 描述


* `<version>`：*string，required*

   * 函数代码的版本。您可以通过 [nest versions](https://docs.byteplus.com/docs/byteplus-cdn/cli-ref-nest-version-cn) 获取函数代码的版本。

* `--canary`：*boolean，optional*

   * 回滚的代码仅发布到灰度环境。默认为全量环境。

* `<description>`：*string，optional*

   * 版本描述。

* `<function_id_or_name>`：*string，optional*

   * 函数 ID 或函数名称。该参数是一个全局参数。参见 [--function](https://docs.byteplus.com/docs/byteplus-cdn/edge-functions-global-f-cn)。默认为 [本地函数列表](https://docs.byteplus.com/docs/byteplus-cdn/cli-ref-nest-function-cn#list) 中的默认函数。如果您通过函数名称指定的本地函数还没有函数 ID，边缘函数 CLI 会返回错误 `Error: function id required`。
