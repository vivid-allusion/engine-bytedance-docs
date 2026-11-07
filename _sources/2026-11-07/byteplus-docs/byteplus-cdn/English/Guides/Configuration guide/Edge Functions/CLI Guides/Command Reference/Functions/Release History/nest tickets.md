---
title: "nest tickets"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/cli-ref-nest-ticket-en"
---

Gets the release history of the local function code.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">This command requires you to set up your BytePlus account's access key ID and secret access key. See <a href="https://docs.byteplus.com/docs/byteplus-cdn/edge-functions-cli-login-en">Set Your Access Key ID and Secret Access Key</a>.</div>


* <div data-tips="true" data-tips-type="tip">This command needs to be run in the root directory of a function project. You need to use <code>nest init</code> to create a function project.</div>


* <div data-tips="true" data-tips-type="tip">The release history of local functions is not saved locally. The Edge Functions CLI manages the release history of local functions on the Edge Functions server. Therefore, ensure that your local function has a function ID when running this command.</div>



<span id="overview"></span>
## Overview

```shell
npx nest tickets -d <description> --function_id <function_id_or_name> --page <page_number> --desc
```


Retrieve the list of release records for the function code.


* `<description>`: *string, optional*

   * Version description.

* `<function_id_or_name>`: *string, optional*

   * Function ID or function name. This is a global parameter. See [--function](https://docs.byteplus.com/docs/byteplus-cdn/edge-functions-global-f-en). Defaults to the default function in the [local function list](https://docs.byteplus.com/docs/byteplus-cdn/cli-ref-nest-function-en#list). If the local function specified by the function name does not yet have a function ID, the Edge Functions CLI will return the error `Error: function id required`.

* `<page_number>`: *integer, optional*

   * Page number for paginated display. Default is 1.

* `--desc`: *boolean, optional*:

   * Sort by version number in descending order. Default is ascending order.


```shell
$ npx nest tickets
+---------+------------+----------------------+-------------+
| VERSION | SCRIPTNAME |       CREATOR        | DESCRIPTION |
+---------+------------+----------------------+-------------+
| 1.0.2   | default    | ******************** |             |
| 1.0.1   | default    | ******************** |             |
+---------+------------+----------------------+-------------+
```


<span id="subcommands"></span>
## Subcommands

<span id="get"></span>
### get

```shell
npx nest tickets get <version> --function <function_id_or_name>
```



* `<version>`: *string, required*

   * Version of the function code. You can obtain the function code version through `npx nest versions list`.

* `<function_id_or_name>`: *string, optional*

   * Function ID or function name. This is a global parameter. See [--function](https://docs.byteplus.com/docs/byteplus-cdn/edge-functions-global-f-en). Defaults to the default function in the [local function list](https://docs.byteplus.com/docs/byteplus-cdn/cli-ref-nest-function-en#list). If the local function specified by the function name does not yet have a function ID, the Edge Functions CLI will return the error `Error: function id required`.


```shell
$ npx nest versions get 1.0.2
(() => {
  // src/index.js
  addEventListener("fetch", (event) => {
    event.respondWith(upgradeToSSL(event));
  });
  async function upgradeToSSL(event) {
    const incommingRequest = event.request;
    const url = new URL(incommingRequest.url);
    if (url.protocol == "http:") {
      url.protocol = "https";
      return fetch(url.toString(), {
        method: incommingRequest.method,
        headers: incommingRequest.headers,
        body: incommingRequest.body
      });
    } else {
      return fetch(incommingRequest);
    }
  }
})();
```
