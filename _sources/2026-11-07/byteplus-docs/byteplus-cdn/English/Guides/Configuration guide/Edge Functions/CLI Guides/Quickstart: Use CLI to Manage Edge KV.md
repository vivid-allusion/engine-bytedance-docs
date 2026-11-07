---
title: "Quickstart: Use CLI to Manage Edge KV"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/edge-functions-cli-kv-quickstart-en"
---

This tutorial introduces how to manage Edge KV using the Edge Functions CLI based on a simple example scenario.

Edge KV service is a distributed key\-value storage service on BytePlus's global edge nodes. After a key\-value pair is written to Edge KV through the Edge Functions console, OpenAPI, or runtime API, it is automatically synchronized to all edge nodes. Functions can quickly read key\-value pairs located on the same edge node through the runtime API.

<span id="example-scenario"></span>
## Example scenario

Your website supports A/B testing functionality, which can return different versions of web pages based on the user's geographic location. The version switching configuration information is stored in Edge KV. You want to be able to read the version switching configuration information from the function's code. In this tutorial, assume the configuration information is as follows:

```json
{
  "us": "versionA",
  "eu": "versionB",
  "asia": "versionA"
}
```


<span id="runtime-environment-requirements"></span>
## Runtime Environment Requirements

The device running the Edge Functions CLI needs to meet the following requirements:


* The operating system must be one of the following types:

   * ARM64 macOS

   * x86\-64 macOS

   * ARM64 Linux

   * x86\-64 Linux

* [Node.js](https://nodejs.org/) and [npm](https://www.npmjs.com/) are installed. Version requirements are as follows:

   * Node.js: 8.17.0+

   * npm: 6.13.4+

* [wget](https://www.gnu.org/software/wget/) or [cURL](https://curl.se/) is installed.


<span id="steps"></span>
## Steps

<span>![图片](https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/upload_2427084f60d06f81cfcb0a49312e0274.png) </span>

You need to complete the following steps to implement the example scenario.


1. **Install Edge Functions CLI**: Create a blank Node.js project and install the Edge Functions CLI in the project.

2. **Set your access key ID and secret access key**: Use the Edge Functions CLI to set your BytePlus account's Access Key ID and Secret Access Key.

3. **Create a namespace**: Use the Edge Functions CLI to create a namespace.

4. **Create a key\-value pair**: Use the Edge Functions CLI to create a key\-value pair in the namespace.

5. **Read the value of the key\-value pair in the function code**: Read the value of the key\-value pair in the function code.


<span id="step-1-install-edge-functions-cli"></span>
### Step 1: Install Edge Functions CLI

Follow these steps to install the Edge Functions CLI.


1. Use `npm init` to create a blank Node.js project.


```shell
$ npm init
This utility will walk you through creating a package.json file.
It only covers the most common items, and tries to guess sensible defaults.

See `npm help init` for definitive documentation on these fields
and exactly what they do.

Use `npm install <pkg>` afterwards to install a package and
save it as a dependency in the package.json file.

Press ^C at any time to quit.
package name: (test) 
version: (1.0.0) 
description: 
entry point: (index.js) 
test command: 
git repository: 
keywords: 
author: 
license: (ISC) 
About to write to /Users/MyFolder/package.json:

{
  "name": "test",
  "version": "1.0.0",
  "main": "index.js",
  "scripts": {
    "test": "echo \"Error: no test specified\" && exit 1"
  },
  "author": "",
  "license": "ISC",
  "description": ""
}


Is this OK? (yes) 
```



2. Run `npm i --save-dev @byteplus/nest` in the Node.js project directory to install the Edge Functions CLI.


```shell
$ npm i --save-dev @byteplus/nest

added 1 package, and audited 2 packages in 739ms

found 0 vulnerabilities
```


Next, you need to set your access key ID and secret access key.

<span id="step-2-set-your-access-key-id-and-secret-access-key"></span>
### Step 2: Set your access key ID and secret access key

Run the following commands in the `HelloWorld` directory to set your access key ID and secret access key in the Edge Functions CLI. You can obtain your access key ID and secret access key from the [BytePlus Console](https://console.byteplus.com/iam/keymanage). See [nest config](https://docs.byteplus.com/docs/byteplus-cdn/cli-ref-nest-config-en).

```shell
npx nest config set -g cloud.access_key <access_key_id>
npx nest config set -g cloud.secret_key <secret_access_key>
```


<span id="step-3-create-a-namespace"></span>
### Step 3: Create a namespace

Run `nest kv namespace create` in the Node.js project directory to create a namespace named `abtest_config`.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">You can only create namespaces using the console, OpenAPI, or CLI. You cannot create namespaces using the runtime API.</div>


```shell
$ npx nest kv namespace create abtest_config
New namespace "abtest_config" created!
```


You can run `nest kv namespace list` to view the created namespaces.

```shell
$ npx nest kv namespace list
+---------------------------------------------------------------+--------------+----------------------+---------------------+
|                            ID:NAME                            |   PROJECT    |     DESCRIPTION      |     CREATETIME      |
+---------------------------------------------------------------+--------------+----------------------+---------------------+
| 25540045541653372777:abtest_config                            | default      |                      | 2025-01-17 17:13:10 |
+---------------------------------------------------------------+--------------+----------------------+---------------------+
```


<span id="step-4-create-a-key-value-pair-in-the-namespace"></span>
### Step 4: Create a key\-value pair in the namespace

Run `nest kv set` in the Node.js project directory to create a key\-value pair under the `abtest_config` namespace. The key of the key\-value pair is `config_key`; the value of the key\-value pair is the JSON value `{"us":"versionA","eu":"versionB","asia":"versionA"}` from the example scenario.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">You can create key\-value pairs using the console, OpenAPI, or runtime API.</div>


```shell
$ npx nest kv set --namespace 25540045541653372777:abtest_config config_key {"us":"versionA","eu":"versionB","asia":"versionA"}
```


You can run `nest kv get` to view the key\-value pair you created.

```Plain Text
$ npx nest kv get --namespace 25540045541653372777:abtest_config config_key
+-------+---------------+
| ITEM  |     VALUE     |
+-------+---------------+
| Key   | config_key    |
| Value | us:versionA   |
| DDL   | Never expires |
+-------+---------------+
```


<span id="step-5-read-the-value-of-the-key-value-pair-in-the-function-code"></span>
### Step 5: Read the value of the key\-value pair in the function code

Follow these steps to read the value of the key\-value pair in the function code.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">You can read the value of key\-value pairs using the console, OpenAPI, or runtime API.</div>


In the function code, you call [KV.get()](https://docs.byteplus.com/docs/byteplus-cdn/docs-EdgeKV-RuntimeAPI) to get the value of the key\-value pair.

```JavaScript
const config = await KV.get("abtest_config","config_key",{type:"string"});
```


You can debug the above code in the Debugger command line using the Edge Functions CLI's [nest debug](https://docs.byteplus.com/docs/byteplus-cdn/cli-ref-nest-debug-en) command:


1. Run `setkv` to add the key\-value pair in the Debugger.


```shell
nest: setkv abtest_config config_key {"us":"versionA","eu":"versionB","asia":"versionA"}
```



2. Run `query` to trigger function execution.


```shell
nest: query
==> HttpResponse ✓
status: 200

statusText: OK

header:
  content-type => text/plain;charset=UTF-8
  date => Fri, 17 Jan 2025 09:53:26 GMT
  server => Sparrow
  transfer-encoding => chunked

body:
{us:versionA,eu:versionB,asia:versionA}
```
