---
title: "nest canary"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/cli-ref-nest-canary-en"
---

Manages the canary environment for local functions.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">This command requires you to set up your BytePlus account's access key ID and secret access key. See <a href="https://docs.byteplus.com/docs/byteplus-cdn/edge-functions-cli-login-en">Set Your Access Key ID and Secret Access Key</a>.</div>


* <div data-tips="true" data-tips-type="tip">This command needs to be run in the root directory of a function project. You need to use <a href="https://docs.byteplus.com/docs/byteplus-cdn/cli-ref-nest-init-en">nest init</a> to create a function project.</div>


* <div data-tips="true" data-tips-type="tip">The environment variables of local functions are not saved locally. The Edge Functions CLI manages the environment variables of local functions on the Edge Functions server. Therefore, ensure that your local function has a function ID when running this command.</div>



<span id="subcommands"></span>
## Subcommands

<span id="list"></span>
### list

```shell
npx nest canary list --canary --continents <continent1,continent2,...> --countries <country1,country2,...> --function <function_id_or_name>
```


Retrieve the edge nodes in the canary environment.


* `--canary`: *boolean, optional*

   * Whether to display only the edge nodes in the canary environment. Default is false.

* `<continent1,continent2,...>`: *string, optional*

   * The continents where the edge nodes are located. Separate multiple continent names with commas. For example, `Asia,Europe`.

* `<country1,country2,...>`: *string, optional*

   * The countries or regions where the edge nodes are located. Separate multiple country or region names with commas. For example, `China,France`.

* `<function_id_or_name>`: *string, optional*

   * Function ID or function name. This is a global parameter. See [--function](https://docs.byteplus.com/docs/byteplus-cdn/edge-functions-global-f-en). Defaults to the default function in the [local function list](https://docs.byteplus.com/docs/byteplus-cdn/cli-ref-nest-function-en#list). If the local function specified by the function name does not yet have a function ID, the Edge Functions CLI will return the error `Error: function id required`.


```shell
$ npx nest canary list
+---------+-----------+--------+
| COUNTRY | CONTINENT | CANARY |
+---------+-----------+--------+
| China   | Asia      | NO     |
+---------+-----------+--------+
```


<span id="add"></span>
### add

```shell
npx nest canary add --countries <country1,country2,...> --function <function_id_or_name>
```


Add edge nodes located in specified countries or regions to the canary environment.


* `<country1,country2,...>`: *string, required*

   * The countries or regions where the edge nodes are located. Separate multiple country or region names with commas. For example, `China,France`.

* `<function_id_or_name>`: *string, optional*

   * Function ID or function name. This is a global parameter. See [--function](https://docs.byteplus.com/docs/byteplus-cdn/edge-functions-global-f-en). Defaults to the default function in the [local function list](https://docs.byteplus.com/docs/byteplus-cdn/cli-ref-nest-function-en#list). If the local function specified by the function name does not yet have a function ID, the Edge Functions CLI will return the error `Error: function id required`.


<span id="delete"></span>
### delete

```shell
npx nest canary delete --countries <country1,country2,...> --function <function_id_or_name>
```


Remove edge nodes located in specified countries or regions from the canary environment.


* `<country1,country2,...>`: *string, required*

   * The countries or regions where the edge nodes are located. Separate multiple country or region names with commas. For example, `China,France`.

* `<function_id_or_name>`: *string, optional*

   * Function ID or function name. This is a global parameter. See [--function](https://docs.byteplus.com/docs/byteplus-cdn/edge-functions-global-f-en). Defaults to the default function in the [local function list](https://docs.byteplus.com/docs/byteplus-cdn/cli-ref-nest-function-en#list). If the local function specified by the function name does not yet have a function ID, the Edge Functions CLI will return the error `Error: function id required`.
