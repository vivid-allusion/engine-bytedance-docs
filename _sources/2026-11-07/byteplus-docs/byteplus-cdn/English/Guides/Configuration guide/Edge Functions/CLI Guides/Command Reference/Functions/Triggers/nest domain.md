---
title: "nest domain"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/cli-ref-nest-domain-en"
---

Manages domains associated with local functions.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">This command requires you to set up your BytePlus account's access key ID and secret access key. See <a href="https://docs.byteplus.com/docs/byteplus-cdn/edge-functions-cli-login-en">Set Your Access Key ID and Secret Access Key</a>.</div>


* <div data-tips="true" data-tips-type="tip">This command needs to be run in the root directory of a function project. You need to use <code>nest init</code> to create a function project.</div>


* <div data-tips="true" data-tips-type="tip">Domain information associated with local functions is not saved locally. The Edge Functions CLI manages the domains associated with local functions on the Edge Functions server. Therefore, ensure that your local function has a function ID when running this command.</div>



<span id="description"></span>
## Description

When users access a function\-associated domain via HTTP or HTTPS requests, and the user request matches the domain's forwarding rules, the domain trigger will trigger the fetch event in the function code. You need to listen for and handle the fetch event in your code.

A function can be associated with one or more domains. Each domain can also be associated with multiple functions. See [Usage Limits](https://docs.byteplus.com/docs/byteplus-cdn/Usage_Limits_Functions).

<span id="subcommands"></span>
## Subcommands

<span id="list"></span>
### list

```shell
npx nest domain list --all --function <function_id> -page <page_number> --desc
```


View domains associated with the local function.


* `--all`: *boolean, optional*

   * View all domains. By default, only domains associated with the local function are shown.

* `<function_id_or_name>`: *string, optional*

   * Function ID or function name. This is a global parameter. See [--function](https://docs.byteplus.com/docs/byteplus-cdn/edge-functions-global-f-en). Defaults to the default function in the [local function list](https://docs.byteplus.com/docs/byteplus-cdn/cli-ref-nest-function-en#list). If the local function specified by the function name does not yet have a function ID, the Edge Functions CLI will return the error `Error: function id required`.

* `<page_number>`: *integer, optional*

   * Page number for paginated display. Default is 1.

* `--desc`: *boolean, optional*:

   * Sort domains in descending order. Default is ascending order.


After running `npx nest domain list`, you can view information about domains, status, and forwarding rules.

```Plain Text
$ npx nest domain list

+-----------------------------+--------+-----------+-----------+------------+
|           DOMAIN            | STATUS |   TYPE    |  PATTERN  | IGNORECASE |
+-----------------------------+--------+-----------+-----------+------------+
| a.example.com               | Online | directory | /welcome/ | false      |
+-----------------------------+--------+-----------+-----------+------------+
```


After running `npx nest domain list --all`, you can check in the STATUS column whether a domain can be associated with functions.

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


Associate a domain with the local function.

You can use the following parameters to configure forwarding rules for the domain. Only user requests matching the forwarding rules will be forwarded to the edge function. See [Domain Triggers](https://docs.byteplus.com/en/docs/byteplus-cdn/docs-domain-triggers) to learn how to configure forwarding rules.


* `<domain_name>`: *string, required*

   * Domain name.

* `<function_id_or_name>`: *string, optional*

   * Function ID or function name. This is a global parameter. See [--function](https://docs.byteplus.com/docs/byteplus-cdn/edge-functions-global-f-en). Defaults to the default function in the [local function list](https://docs.byteplus.com/docs/byteplus-cdn/cli-ref-nest-function-en#list). If the local function specified by the function name does not yet have a function ID, the Edge Functions CLI will return the error `Error: function id required`.

* `<url_directory>`: *string, optional*

   * Rule type is URL directory. The rule applies to all files in the specified directory. You must set one of `<url_directory>`, `<url_ext>`, or `<url>`.

* `<url_ext>`: *string, optional*

   * Rule type is file extension. The rule applies to all files with the specified extension. You must set one of `<url_directory>`, `<url_ext>`, or `<url>`.

* `<url>`: *string, optional*

   * Rule type is full URL path. The rule applies to the specified file. You must set one of `<url_directory>`, `<url_ext>`, or `<url>`.

* `--ignore-case`: *boolean, optional*

   * Ignore case. Case\-sensitive by default.


For example, the following command associates the domain www.example.com with the local function and sets the forwarding rule type to URL directory. If the URL directory of the user request is `/welcome/`, such as `https://www.example.com/welcome/a.png`, the request matches the forwarding rule.

```shell
npx nest domain bind www.example.com --url-directory /welcome/
```


You can run `npx nest domain list` to check if the domain has been associated.

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


Disassociate a domain from the local function.


* `<domain_name>`: *string, required*

   * The domain to be disassociated.

* `<function_id_or_name>`: *string, optional*

   * Function ID or function name. This is a global parameter. See [--function](https://docs.byteplus.com/docs/byteplus-cdn/edge-functions-global-f-en). Defaults to the default function in the [local function list](https://docs.byteplus.com/docs/byteplus-cdn/cli-ref-nest-function-en#list). If the local function specified by the function name does not yet have a function ID, the Edge Functions CLI will return the error `Error: function id required`.


You can run `npx nest domain list` to check if the domain has been disassociated.

```Plain Text
$ npx nest domain list

+-----------------------------+--------+-----------+-----------+------------+
|           DOMAIN            | STATUS |   TYPE    |  PATTERN  | IGNORECASE |
+-----------------------------+--------+-----------+-----------+------------+
+-----------------------------+--------+-----------+-----------+------------+
```
