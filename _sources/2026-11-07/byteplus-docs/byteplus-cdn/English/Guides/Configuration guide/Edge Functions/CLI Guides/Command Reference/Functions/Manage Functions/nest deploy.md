---
title: "nest deploy"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/cli-ref-nest-deploy-en"
---

Deploys a local function to edge nodes.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">This command requires you to set up your BytePlus account's access key ID and secret access key. See <a href="https://docs.byteplus.com/docs/byteplus-cdn/edge-functions-cli-login-en">Set Your Access Key ID and Secret Access Key</a>.</div>


* <div data-tips="true" data-tips-type="tip">This command needs to be run in the root directory of a function project. You need to use <code>nest init</code> to create a function project.</div>



<span id="synopsis"></span>
## Synopsis

```shell
npx nest deploy --canary --message <message> --function <function_id_or_name> --all --create
```


<span id="description"></span>
## Description

You can choose between a canary release or a full release.


* `--canary`: *boolean, optional*

   * Canary release. Before performing a canary release, ensure that you have set up canary release nodes. Canary release nodes can be set up using [nest canary](https://docs.byteplus.com/docs/byteplus-cdn/cli-ref-nest-canary-en). The default is a full release.

* `<message>`: *string, optional*

   * Description related to this release.

* `<function_id_or_name>`: *string, optional*

   * Local function ID or function name. This parameter is a global parameter. See [--function](https://docs.byteplus.com/docs/byteplus-cdn/edge-functions-global-f-en). The default is the default function in the [local function list](https://docs.byteplus.com/docs/byteplus-cdn/cli-ref-nest-function-en#list). If the local function you specify by name doesn't have a function ID yet, the Edge Functions CLI will prompt you to create a new remote function.

* `--all`: *boolean, optional*

   * Deploy all local functions under the current project. By default, only the local function specified by the `--function` global parameter or the default function in the [local function list](https://docs.byteplus.com/docs/byteplus-cdn/cli-ref-nest-function-en#list) is deployed.

* `--create`: *boolean, optional*

   * Create a corresponding remote function. By default, a corresponding remote function is not created.


<span id="deploy-function-configurations-or-edge-kv-data-manually-added-to-the-nest-json-file"></span>
## Deploy function configurations or Edge KV data manually added to the nest.json file

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">Directly modifying the <code>nest.json</code> file carries risks. You can use this method if you are familiar with the structure of the <code>nest.json</code> file and need to process a large number of functions frequently in batch.</div>


You can manually add Cron trigger configurations, environment variables, and associated domains for local functions in the `nest.json` file. Additionally, you can manually add Edge KV data. When running nest deploy to deploy local functions, you can use `--cron`, `--env`, `--kv`, and `--domain` to simultaneously deploy these manually added configurations or data.


* `--cron`: *boolean, optional*

   * Deploy Cron tasks manually edited in nest.json.

* `--env`: *boolean, optional*

   * Deploy environment variables manually edited in nest.json.

* `--kv`: *boolean, optional*

   * Deploy Edge KV data manually edited in nest.json.

* `--domain`: *boolean, optional*

   * Deploy domains associated with functions manually edited in nest.json.


The following example shows a manually modified `nest.json` file.

```json
{
  "work_dir": "/Users/HelloWorld",
  "src_dir": "src",
  "output_dir": "output",
  "cloud": {
    "api_server": "https://open.byteplusapi.com",
    "debug_server": "wss://byteplusef-debugger.byteintlapi.com",
    "api_version": "2021-03-01",
    "api_region": "ap-singapore-1",
    "api_timeout": 5000,
    "key_manager_url": "https://console.byteplus.com/iam/keymanage",
    "product": "CDN",
    "access_key": "xxx",
    "secret_key": "xxx"
  },
  "kv": {
      "24629043532424120990:ns": {
          "ENV": "boe",
          "port": "8383",
          "DEBUG": "true"
      }
  },
  "functions": [
    {
      "id": "10c5a0e*********1b8d90896",
      "name": "function1",
      "description": "",
      "type": "js",
      "entry": "index.js",
      "format": "",
      "project": ""
    },
    {
      "id": "",
      "name": "function2",
      "description": "",
      "type": "js",
      "entry": "test.js",
      "format": "",
      "envs": {
          "ENV": "boe",
          "port": "8383",
          "DEBUG": "true"
      },
      "domains": [
          {
              "names": [
                  "test.example.com"
              ],
              "type": "directory",
              "pattern": "/a/"
          }
      ],
      "crons": [
          {
              "name": "cron job name",
              "cron": "*/10 * * * *"
              "params": "",
              "global": false,
              "description": "description for this cron job",
          }
      ],
      "project": ""
    },
    {
      "id": "02581*********8247b5",
      "name": "function3",
      "description": "",
      "type": "js",
      "entry": "index.js",
      "format": "",
      "domains": [
          {
              "domains": [
                  "www.example.com"
              ],
              "type": "directory",
              "pattern": "/hello/"
          }
      ],
      "project": ""
    }
  ],
  "debugger": {}
}
```
