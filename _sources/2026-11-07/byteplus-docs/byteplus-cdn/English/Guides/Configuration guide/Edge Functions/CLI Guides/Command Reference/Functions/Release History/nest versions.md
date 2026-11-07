---
title: "nest versions"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/cli-ref-nest-version-en"
---

Gets released versions of the local function code.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">This command requires you to set up your BytePlus account's access key ID and secret access key. See <a href="https://docs.byteplus.com/docs/byteplus-cdn/edge-functions-cli-login-en">Set Your Access Key ID and Secret Access Key</a>.</div>


* <div data-tips="true" data-tips-type="tip">This command needs to be run in the root directory of a function project. You need to use <code>nest init</code> to create a function project.</div>


* <div data-tips="true" data-tips-type="tip">The release history of local functions is not saved locally. The Edge Functions CLI manages the release history of local functions on the Edge Functions server. Therefore, ensure that your local function has a function ID when running this command.</div>



<span id="subcommands"></span>
## Subcommands

<span id="list"></span>
### list

```shell
npx nest versions list --function <function_id_or_name> --page <page_number>
```


View the list of released code versions for the local function.


* `<function_id_or_name>`: *string, optional*

   * Function ID or function name. This is a global parameter. See [--function](https://docs.byteplus.com/docs/byteplus-cdn/edge-functions-global-f-en). Defaults to the default function in the [local function list](https://docs.byteplus.com/docs/byteplus-cdn/cli-ref-nest-function-en#list). If the local function specified by the function name does not yet have a function ID, the Edge Functions CLI will return the error `Error: function id required`.

* `<page_number>`: *integer, optional*

   * Page number for paginated display. Default is 1.


```shell
$ npx nest versions list
+---------+------+------------+-------------+----------------------+------------------+---------------------+
| VERSION | TYPE |   STATUS   | DESCRIPTION |       CREATOR        | PREVIOUS VERSION |     CREATETIME      |
+---------+------+------------+-------------+----------------------+------------------+---------------------+
| 1.0.2   | Full | Publishing |             | ******************** | 1.0.1            | 2025-01-08 17:35:40 |
| 1.0.1   | Full | Success    |             | ******************** |                  | 2025-01-08 00:55:42 |
+---------+------+------------+-------------+----------------------+------------------+---------------------+
```


<span id="view"></span>
### view

```shell
npx nest versions view <version> --function <function_id_or_name>
```


View the function code of a specified version.


* `<version>`: *string, required*

   * Version of the function code. You can obtain the function code version through `npx nest versions list`.

* `<function_id_or_name>`: *string, optional*

   * Function ID or function name. This is a global parameter. See [--function](https://docs.byteplus.com/docs/byteplus-cdn/edge-functions-global-f-en). Defaults to the default function in the [local function list](https://docs.byteplus.com/docs/byteplus-cdn/cli-ref-nest-function-en#list). If the local function specified by the function name does not yet have a function ID, the Edge Functions CLI will return the error `Error: function id required`.


```shell
$ npx nest versions view 1.0.1
/**
 * Add the necessary event listener
 * @param {Event} fetch event, {Function} async function
 */
addEventListener('fetch', event => {
  event.respondWith(handleRequest(event.request));
})

/**
 * Make a response to client
 * @param {Request} request
 */
async function handleRequest(request) {
  return new Response('Hello World!', { status: 200 });
}
```
