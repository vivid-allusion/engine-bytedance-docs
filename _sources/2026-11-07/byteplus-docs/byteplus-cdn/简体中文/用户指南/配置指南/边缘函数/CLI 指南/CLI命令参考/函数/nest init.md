---
title: "nest init"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/cli-ref-nest-init-cn"
---

在当前目录创建一个函数项目并在函数项目中创建一个本地函数。

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">您无需设置 Access Key ID 和 Secret Access Key 就可以运行本命令。</div>


<span id="概要"></span>
## 概要

```shell
npx nest init <dir> --env --sync --function <function_id> --cn
```


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">您也可以直接运行以下命令快速安装边缘函数 CLI 并创建本地函数。运行以下命令前无需安装边缘函数 CLI。</div>


<div data-tips="true" data-tips-type="tip">```shell
npx @byteplus/nest init --env --sync --function <function_id>
```
</div>


<div data-tips="true" data-tips-type="tip">该命令按顺序执行以下操作：</div>



1. <div data-tips="true" data-tips-type="tip">在当前目录创建一个 Node.js 项目。</div>


2. <div data-tips="true" data-tips-type="tip">在 Node.js 项目中安装边缘函数 CLI。</div>


3. <div data-tips="true" data-tips-type="tip">运行边缘函数 CLI 在当前目录创建一个函数项目并在函数项目中创建一个本地函数。</div>



<span id="描述"></span>
## 描述

npx 命令会在您运行 `npx nest init` 的目录创建一个函数项目，然后提示您输入函数名称、选择函数模板、入口文件的位置和名称、所属 BytePlus 项目、函数描述等信息。然后，边缘函数 CLI 会根据您输入的信息创建一个本地函数。

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">每个 BytePlus 账号下的函数名称需唯一。名称的规则如下：</div>


   * <div data-tips="true" data-tips-type="tip">支持英文字母、数字和连字符（\-）。</div>


   * <div data-tips="true" data-tips-type="tip">长度不超过 128 个字符。</div>


* <div data-tips="true" data-tips-type="tip">您可以选择的函数模板取决于您是否设置了 Access Key ID 和 Secret Access Key：</div>


   * <div data-tips="true" data-tips-type="tip">如果您没有设置 Access Key ID 和 Secret Access Key，您只能使用 HelloWorld 模板。</div>


   * <div data-tips="true" data-tips-type="tip">如果您设置了 Access Key ID 和 Secret Access Key ，您可以使用边缘函数支持的所有模板。</div>


* `<dir>`：*string，optional*

   * 函数项目的创建目录。默认为当前目录。

* `--sync`：*boolean，optional*

   * 创建一个与当前项目关联的远端函数。默认不创建远端函数。

* `<function_id>`：*string，optional*

   * 远端函数的函数 ID。如果您需要把本地函数与远端函数关联，可以通过该参数设置远端函数的函数 ID。

* `--env`：*boolean，optional*

   * 把 `<function_id>` 对应的远端函数的环境变量同步到本地。默认不同步远端函数的环境变量。

* `--cn`：*boolean，optional*

   * 函数的发布地域是否仅限于中国内地。默认不限制函数的发布地域。


一个函数项目下可以有多个本地函数。如果您需要在函数项目中创建新的本地函数，可以使用 [nest functions create](https://docs.byteplus.com/docs/byteplus-cdn/cli-ref-nest-function-cn#create) 命令。
