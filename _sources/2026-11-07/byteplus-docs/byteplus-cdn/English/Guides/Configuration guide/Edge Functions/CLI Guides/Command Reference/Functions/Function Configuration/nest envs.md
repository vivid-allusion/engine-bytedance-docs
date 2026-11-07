---
title: "nest envs"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/cli-ref-nest-env-en"
---

Manages environment variables for local functions.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">This command requires you to set up your BytePlus account's Access Key ID and Secret Access Key. See <a href="https://docs.byteplus.com/docs/byteplus-cdn/edge-functions-cli-login-en">Setting up your Access Key ID and Secret Access Key</a>.</div>


* <div data-tips="true" data-tips-type="tip">This command needs to be run in the root directory of a function project. You need to use <a href="https://docs.byteplus.com/docs/byteplus-cdn/cli-ref-nest-init-en">nest init</a> to create a function project.</div>


* <div data-tips="true" data-tips-type="tip">The environment variables of local functions are not saved locally. The Edge Functions CLI manages the environment variables of local functions on the Edge Functions server. Therefore, ensure that your local function has a function ID when running this command.</div>



<span id="subcommands"></span>
## Subcommands

<span id="list"></span>
### list

```shell
npx nest envs list --function <function_id_or_name> --save-dev
```


Retrieve the list of environment variables for the local function.


* `<function_id_or_name>`: *string, optional*

   * Function ID or function name. This is a global parameter. See [--function](https://docs.byteplus.com/docs/byteplus-cdn/edge-functions-global-f-en). Defaults to the default function in the [local function list](https://docs.byteplus.com/docs/byteplus-cdn/cli-ref-nest-function-en#list). If the local function specified by the function name does not yet have a function ID, the Edge Functions CLI will return the error `Error: function id required`.

* `<--save-dev>`: *boolean, optional*

   * Whether to save the environment variables locally for debugging. By default, they are not saved locally.


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


<div data-tips="true" data-tips-type="tip">Add, delete, and update operations on environment variables will not take effect until the function is released again.</div>


Set the value of an environment variable.


* `<key>`: *string, required*

   * The key of the environment variable.

* `<value>`: *string, required*

   * The value of the environment variable.

* `<function_id_or_name>`: *string, optional*

   * Function ID or function name. This is a global parameter. See [--function](https://docs.byteplus.com/docs/byteplus-cdn/edge-functions-global-f-en). Defaults to the default function in the [local function list](https://docs.byteplus.com/docs/byteplus-cdn/cli-ref-nest-function-en#list). If the local function specified by the function name does not yet have a function ID, the Edge Functions CLI will return the error `Error: function id required`.


<span id="delete"></span>
### delete

```shell
npx nest envs set <key> --function <function_id_or_name>
```


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Add, delete, and update operations on environment variables will not take effect until the function is released again.</div>


Delete an environment variable.


* `<key>`: *string, required*

   * The key of the environment variable.

* `<function_id_or_name>`: *string, optional*

   * Function ID or function name. This is a global parameter. See [--function](https://docs.byteplus.com/docs/byteplus-cdn/edge-functions-global-f-en). Defaults to the default function in the [local function list](https://docs.byteplus.com/docs/byteplus-cdn/cli-ref-nest-function-en#list). If the local function specified by the function name does not yet have a function ID, the Edge Functions CLI will return the error `Error: function id required`.
