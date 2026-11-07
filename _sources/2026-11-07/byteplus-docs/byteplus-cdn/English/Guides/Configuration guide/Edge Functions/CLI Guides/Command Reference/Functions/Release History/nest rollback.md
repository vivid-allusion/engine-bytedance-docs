---
title: "nest rollback"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/cli-ref-nest-rollback-en"
---

Rolls back the local function's code to a version you specify.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">This command requires you to set up your BytePlus account's access key ID and secret access key. See <a href="https://docs.byteplus.com/docs/byteplus-cdn/edge-functions-cli-login-en">Set Your Access Key ID and Secret Access Key</a>.</div>


* <div data-tips="true" data-tips-type="tip">This command needs to be run in the root directory of a function project. You need to use <code>nest init</code> to create a function project.</div>


* <div data-tips="true" data-tips-type="tip">The release history of local functions is not saved locally. The Edge Functions CLI manages the release history of local functions on the Edge Functions server. Therefore, ensure that your local function has a function ID when running this command.</div>



<span id="overview"></span>
## Overview

```shell
npx nest rollback <version> --canary -d <description> -f <function_id> 
```


<span id="description"></span>
## Description


* `<version>`: *string, required*

   * Version of the function code. You can obtain the function code version through [nest versions](https://docs.byteplus.com/docs/byteplus-cdn/cli-ref-nest-version-en).

* `--canary`: *boolean, optional*

   * The rolled\-back code is only published to the canary environment. Default is the production environment.

* `<description>`: *string, optional*

   * Version description.

* `<function_id_or_name>`: *string, optional*

   * Function ID or function name. This is a global parameter. See [--function](https://docs.byteplus.com/docs/byteplus-cdn/edge-functions-global-f-en). Defaults to the default function in the [local function list](https://docs.byteplus.com/docs/byteplus-cdn/cli-ref-nest-function-en#list). If the local function specified by the function name does not yet have a function ID, the Edge Functions CLI will return the error `Error: function id required`.
