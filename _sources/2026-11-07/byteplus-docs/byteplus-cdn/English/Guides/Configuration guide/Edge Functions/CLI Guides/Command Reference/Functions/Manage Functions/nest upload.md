---
title: "nest upload"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/cli-ref-nest-upload-en"
---

Uploads the code of a local function to a remote function.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">This command requires you to set up your BytePlus account's access key ID and secret access key. See <a href="https://docs.byteplus.com/docs/byteplus-cdn/edge-functions-cli-login-en">Set Your Access Key ID and Secret Access Key</a>.</div>


* <div data-tips="true" data-tips-type="tip">This command needs to be run in the root directory of a function project. You need to use <code>nest init</code> to create a function project.</div>



<span id="synopsis"></span>
## Synopsis

```shell
npx nest upload --no-build --create --function <function_id_or_name>
```


<span id="description"></span>
## Description


* `--no-build`: *boolean, optional*

   * Disable minification. By default, the Edge Functions CLI automatically minifies the code.

* `--create`: *boolean, optional*

   * Create a new remote function. By default, a new remote function is not created.

* `<function_id_or_name>`: *string, optional*

   * Function ID or function name. This parameter is a global parameter. See [--function](https://docs.byteplus.com/docs/byteplus-cdn/edge-functions-global-f-en). The default is the default function in the [local function list](https://docs.byteplus.com/docs/byteplus-cdn/cli-ref-nest-function-en#list). If the function you specify by name doesn't have a function ID yet, the Edge Functions CLI will prompt you to create a new remote function.
