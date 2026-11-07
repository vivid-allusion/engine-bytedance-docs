---
title: "nest deploy"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/cli-ref-nest-deploy-cn"
---

把本地函数部署到边缘节点。

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">本命令需要您设置您的 BytePlus 账号的 Access Key ID 和 Secret Access Key。参见 <a href="https://docs.byteplus.com/docs/byteplus-cdn/edge-functions-cli-login-cn">设置您的 Access Key ID 和 Secret Access Key</a>。</div>


* <div data-tips="true" data-tips-type="tip">本命令需要在一个函数项目的根目录下运行。您需要使用 <a href="https://docs.byteplus.com/docs/byteplus-cdn/cli-ref-nest-init-cn">nest init</a> 创建一个函数项目。</div>



<span id="概要"></span>
## 概要

```shell
npx nest deploy --canary --message <message> --function <function_id_or_name> --all --create
```


<span id="描述"></span>
## 描述

您可以选择灰度发布或全量发布。


* `--canary`：*boolean，optional*

   * 灰度发布。灰度发布前，确保您已经设置了灰度发布节点。灰度发布节点可以通过 [nest canary](https://docs.byteplus.com/docs/byteplus-cdn/cli-ref-nest-canary-cn) 设置。默认为全量发布。

* `<message>`：*string，optional*

   * 与本次发布相关的描述信息。

* `<function_id_or_name>`：*string，optional*

   * 本地函数 ID 或函数名称。该参数是一个全局参数。参见 [--function](https://docs.byteplus.com/docs/byteplus-cdn/edge-functions-global-f-cn)。默认为 [本地函数列表](https://docs.byteplus.com/docs/byteplus-cdn/cli-ref-nest-function-cn#list) 中的默认函数。如果您通过函数名称指定的本地函数还没有函数 ID，边缘函数 CLI 会提示您是否创建一个新的远端函数。

* `--all`：*boolean，optional*

   * 发布当前项目下的全部本地函数。默认仅发布 `--function` 全局参数指定的本地函数或 [本地函数列表](https://docs.byteplus.com/docs/byteplus-cdn/cli-ref-nest-function-cn#list) 中的默认函数。

* `--create`：*boolean，optional*

   * 创建一个对应的远端函数。默认不创建一个对应的远端函数。


<span id="发布您手动在-nest-json-文件中添加的函数配置或边缘-kv-数据"></span>
## 发布您手动在 nest.json 文件中添加的函数配置或边缘 KV 数据

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">直接修改 <code>nest.json</code> 文件存在风险。如果您对 <code>nest.json</code> 文件的结构比较熟悉，且有大量函数需要批量频繁处理时，可以使用这种方法。</div>


您可以在 `nest.json` 文件中手动添加本地函数的 Cron 触发器配置、环境变量及所关联的域名。另外，您还可以手动添加边缘 KV 数据。在运行 nest deploy 发布本地函数时，您可以通过 `--cron`、`--env`、`--kv`、`--domain` 同时发布这些您手动添加的配置或数据。


* `--cron`：*boolean，optional*

   * 发布在 nest.json 中手动编辑的 Cron 任务。

* `--env`：*boolean，optional*

   * 发布在 nest.json 中手动编辑的环境变量。

* `--kv`：*boolean，optional*

   * 发布在 nest.json 中手动编辑的边缘 KV 数据。

* `--domain`：*boolean，optional*

   * 发布在 nest.json 中手动编辑的与函数关联的域名。


下面的例子显示了一个手动修改过的 `nest.json` 文件。

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
