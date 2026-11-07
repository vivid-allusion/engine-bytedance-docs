---
title: "nest upload"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/cli-ref-nest-upload-cn"
---

把本地函数的代码上传到远端函数。

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">本命令需要您设置您的 BytePlus 账号的 Access Key ID 和 Secret Access Key。参见 <a href="https://docs.byteplus.com/docs/byteplus-cdn/edge-functions-cli-login-cn">设置您的 Access Key ID 和 Secret Access Key</a>。</div>


* <div data-tips="true" data-tips-type="tip">本命令需要在一个函数项目的根目录下运行。您需要使用 <a href="https://docs.byteplus.com/docs/byteplus-cdn/cli-ref-nest-init-cn">nest init</a> 创建一个函数项目。</div>



<span id="概要"></span>
## 概要

```shell
npx nest upload --no-build --create --function <function_id_or_name>
```


<span id="描述"></span>
## 描述


* `--no-build`：*boolean，optional*

   * 关闭最小化处理。边缘函数 CLI 默认会对代码自动进行最小化处理。

* `--create`：*boolean，optional*

   * 创建一个新的远端函数。默认不创建一个新的远端函数。

* `<function_id_or_name>`：*string，optional*

   * 函数 ID 或函数名称。该参数是一个全局参数。参见 [--function](https://docs.byteplus.com/docs/byteplus-cdn/edge-functions-global-f-cn)。默认为 [本地函数列表](https://docs.byteplus.com/docs/byteplus-cdn/cli-ref-nest-function-cn#list) 中的默认函数。如果您通过函数名称指定的函数还没有函数 ID，边缘函数 CLI 会提示您是否创建一个新的远端函数。
