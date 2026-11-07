---
title: "nest deploy"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/cli-ref-nest-deploy-cn-zh-tw"
---

將本地函數部署到邊緣節點。

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">本指令需要您設定您的 BytePlus 帳號的 Access Key ID 和 Secret Access Key。參見 <a href="https://docs.byteplus.com/docs/byteplus-cdn/edge-functions-cli-login-cn-zh-tw">設定您的 Access Key ID 和 Secret Access Key</a>。</div>


* <div data-tips="true" data-tips-type="tip">本指令需要在一個函數專案的根目錄下執行。您需要使用 <a href="https://docs.byteplus.com/docs/byteplus-cdn/cli-ref-nest-init-cn-zh-tw">nest init</a> 建立一個函數專案。</div>



<span id="概要"></span>
## 概要

```shell
npx nest deploy --canary --message <message> --function <function_id_or_name> --all --create
```


<span id="描述"></span>
## 描述

您可以選擇金絲雀發佈或全量發佈：


* `--canary`：*boolean，optional*

   * 金絲雀發佈。金絲雀發佈前，確保您已設定金絲雀發佈節點。金絲雀發佈節點可以透過 [nest canary](https://docs.byteplus.com/docs/byteplus-cdn/cli-ref-nest-canary-cn-zh-tw) 設定。預設為全量發佈。

* `<message>`：*string，optional*

   * 與本次發佈相關的描述資訊。

* `<function_id_or_name>`：*string，optional*

   * 本地函數 ID 或函數名稱。該參數是一個全域參數。參見 [--function](https://docs.byteplus.com/docs/byteplus-cdn/edge-functions-global-f-cn-zh-tw)。預設為 [本地函數清單](https://docs.byteplus.com/docs/byteplus-cdn/cli-ref-nest-function-cn-zh-tw#list) 中的預設函數。如果您透過函數名稱指定的本地函數還沒有函數 ID，邊緣函數 CLI 會提示您是否建立一個新的遠端函數。

* `--all`：*boolean，optional*

   * 發佈當前專案下的全部本地函數。預設僅發佈 `--function` 全域參數指定的本地函數或 [本地函數清單](https://docs.byteplus.com/docs/byteplus-cdn/cli-ref-nest-function-cn-zh-tw#list) 中的預設函數。

* `--create`：*boolean，optional*

   * 建立一個對應的遠端函數。預設不建立對應的遠端函數。


<span id="發佈您手動在-nest-json-檔案中新增的函數設定或邊緣-kv-資料"></span>
## 發佈您手動在 nest.json 檔案中新增的函數設定或邊緣 KV 資料

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">直接修改 <code>nest.json</code> 檔案存在風險。如果您對 <code>nest.json</code> 檔案的結構比較熟悉，且有大量函數需要批次頻繁處理時，可以使用這種方法。</div>


您可以在 `nest.json` 檔案中手動新增本地函數的 Cron 觸發器設定、環境變數及所關聯的網域名稱。另外，您還可以手動新增邊緣 KV 資料。在執行 nest deploy 發佈本地函數時，您可以透過 `--cron`、`--env`、`--kv`、`--domain` 同時發佈這些您手動新增的設定或資料。


* `--cron`：*boolean，optional*

   * 發佈在 nest.json 中手動編輯的 Cron 任務

* `--env`：*boolean，optional*

   * 發佈在 nest.json 中手動編輯的環境變數

* `--kv`：*boolean，optional*

   * 發佈在 nest.json 中手動編輯的邊緣 KV 資料

* `--domain`：*boolean，optional*

   * 發佈在 nest.json 中手動編輯的與函數關聯的網域名稱


下面的範例顯示了一個手動修改過的 `nest.json` 檔案：

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
