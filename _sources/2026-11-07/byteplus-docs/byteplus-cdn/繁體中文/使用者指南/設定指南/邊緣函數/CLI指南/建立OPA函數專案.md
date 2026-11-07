---
title: "建立OPA函數專案"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/create_function_project_with_opa_zh-tw"
---

本文檔介紹如何使用邊緣函數 CLI 建立一個支援[開放策略代理（Open Policy Agent, OPA）](https://www.openpolicyagent.org/)的函數專案。

<span id="什麼是-opa"></span>
## 什麼是 OPA

OPA 是一個開源的通用策略引擎，統一了雲端原生技術堆疊中的策略實施。OPA 提供了一種高階宣告性語言 Rego，使您能夠將策略編寫為程式碼，並將策略實現從服務本身的邏輯中解耦。

當您的服務需要做出基於策略的決策時，會把輸入資料發送給 OPA。OPA 根據預先定義的策略對輸入資料進行評估並生成決策結果。這個結果可以是一個簡單的布林值，例如允許或拒絕，也可以是一個更複雜的結構化文件。由於策略是用宣告性語言編寫的，您可以專注於策略本身的內容，而 OPA 則負責地執行這些策略。

<span id="opa-的應用場景"></span>
## OPA 的應用場景

OPA 的靈活性使其適用於多種複雜的應用場景，例如使用者請求驗證和 RBAC 存取控制。

<span id="使用者請求驗證"></span>
### 使用者請求驗證

在邊緣計算中，一個常見的需求是在請求到達來源伺服器之前對使用者進行身分驗證和授權。例如，您可以使用 OPA 來保護付費內容，過濾掉未授權的請求，從而增強來源伺服器的安全性。

<span id="rbac-存取控制"></span>
### RBAC 存取控制

基於角色的存取控制（RBAC）根據使用者的角色和職責來授予對資源的存取權限。例如，在企業內部，可以根據員工的職位和工作職能，授予不同層級的系統存取權限。您可以使用 OPA 來定義和實施複雜的 RBAC 策略。例如，您可以定義一個策略，規定只有管理員角色的使用者才能存取某個 API，而訪客角色的使用者只能讀取資料。這種策略可以集中管理，並輕鬆應用於多個服務。

<span id="邊緣函數如何評估-opa-策略"></span>
## 邊緣函數如何評估 OPA 策略

邊緣函數通過其運行時期中內建的 WebAssembly (Wasm) 模組來評估 OPA 策略。該模組負責載入和執行由 `.rego` 檔案編譯而來的 `.wasm` 檔案。您可以通過邊緣函數 CLI 向邊緣函數上傳該 `.wasm` 檔案。當函數接收到 HTTP 請求時，Wasm 模組會根據請求資訊進行策略評估，並返回決策結果。

<span>![图片](https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/upload_795486d1f0d9a6e9b5df4d1467e893c4.jpeg) </span>

邊緣函數運行時期的 Wasm 模組評估 OPA 策略的具體流程如下：


1. **準備輸入**：函數監聽由 HTTP 請求觸發的 `fetch` 事件。`fetch` 事件觸發後，函數會從該 HTTP 請求中提取所需資料（如 Header、URL、JWT 等），並基於提取的資料生成一個 JSON 資料作為輸入，供 Wasm 模組進行策略評估。例如，一個簡單的 JSON 資料如下所示：

   ```json
   {
     "method": "GET"
   }
   ```
   

   該 JSON 資料會傳遞給 Wasm 模組進行評估。例如，一個簡單的策略檔案（`policy.rego`）如下所示，它規定了只允許 `GET` 方法：

   ```rego
       package example
       
       default allow := false
       
       allow if {
           input.method == "GET"
       }
   ```
   

2. **執行策略評估**：函數呼叫 Wasm 模組中已載入的策略，並將生成的 JSON 資料傳遞給它。Wasm 模組根據策略邏輯對收到的 JSON 資料進行評估。

3. **返回決策結果**：Wasm 模組返回一個包含決策結果的 JSON 資料。例如，`[{"result": {"allow": true}}]`。

4. **執行決策**：函數接收到決策結果後，便可以根據該結果執行相應的業務邏輯，例如允許或拒絕一個請求、改寫標頭等。

   例如，在執行策略評估後，您可以檢查評估結果中的 `allow` 欄位。如果為 `true`，則允許請求；否則，返回 403 Forbidden 錯誤。

   ```javascript
   const r = policy.eval(input);
   
   let allow = false;
   if (r.length === 1 && r[0]["result"] === true) {
     allow = true;
   }
   
   if (!allow) {
     return new Response("Forbidden", {
       status: 403,
       statusText: "Forbidden",
     });
   }
   
   return new Response("OK", { status: 200, statusText: "OK" });
   ```
   


此外，為了簡化開發流程，邊緣函數 CLI 內建了 OPA 的編譯工具鏈，可將您的 `.rego`檔案直接編譯成 `.wasm` 檔案。這種設計使您無需關心底層的編譯和整合細節，只需在 JavaScript 程式碼中即可方便地呼叫 OPA 策略。

<span id="建立、偵錯和發布一個支援-opa-的函數專案"></span>
## 建立、偵錯和發布一個支援 OPA 的函數專案

本小節將指導您如何使用邊緣函數 CLI 建立、偵錯和發布一個支援 OPA 的函數專案。

<span id="步驟一：建立一個支援-opa-的函數專案"></span>
### 步驟一：建立一個支援 OPA 的函數專案

在您的裝置上執行以下命令。該命令會安裝邊緣函數 CLI，然後建立一個支援 OPA 的函數專案，並在函數專案中建立一個本地函數。參見 [nest init](https://docs.byteplus.com/docs/byteplus-cdn/cli-ref-nest-init-cn-zh-tw)。

```shell
$ npx @byteplus/nest@latest init
```


您需要根據命令列提示把函數使用的範本設定為 `OPA`，並根據您的需求設定其他參數。本文假設函數的名稱為 `opa-demo`。

```bash
$ npx @byteplus/nest@latest init opa  
✓ Name: opa-demo
==> [info]: No AK&SK found, you can login to get more function templates. see also `nest config -h`
✓ Select a template you want to start with: OPA
✓ Put code file in src/ directory?: Yes
✓ Entry File in src/ (optional, default is index.js): index.js
✓ Project Name (optional, default is "default"): 
✓ Description: An OPA function project
```


命令執行完成後，函數專案的結構如下：

```Plain Text
opa-demo/
├── src/
│   ├── index.js         # JavaScript 程式碼的入口檔案
│   ├── opa-wasm-sdk/    # OPA Javascript SDK
│   └── opa-demo.rego    # OPA 策略檔案
├── nest.json            # 專案設定檔
├── package.json         # Node.js 專案資訊
└── node_modules/
```



* **`src/index.js`**: JavaScript 程式碼的入口檔案。您將在此檔案中呼叫 OPA 策略。

* **`src/opa-demo.rego`**: OPA 策略檔案，基於 Rego 語言編寫。

* **`src/opa-wasm-sdk`**: 邊緣函數提供的 OPA JavaScript SDK。該 SDK 基於 [OPA Wasm Javascript Module](https://www.openpolicyagent.org/ecosystem/entry/opa-wasm-js) 開發，但兩者並不完全相同。該 SDK 已內嵌在專案中。您可以在 `index.js` 中直接使用該 SDK。

* **`nest.json`**: 函數專案設定檔。


專案建立完成後，下一步是根據您的業務需求編輯 OPA 策略。

<span id="步驟二：編輯-opa-策略"></span>
### 步驟二：編輯 OPA 策略

`OPA` 範本在 `src/opa-demo.rego` 提供了一個初始的 OPA 策略檔案。您可以用任意程式碼編輯器開啟該檔案，根據需求自行修改程式碼。

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>



* <div data-tips="true" data-tips-type="warning">邊緣函數僅支援 1.4.2 版本的 OPA。因此，您只能使用 1.4.2 版本的 OPA 內建函數。參見 <a href="https://v1-4-2--opa-docs.netlify.app/policy-reference">1.4.2 版本的 Policy Reference</a> 了解如何使用 OPA 內建函數。但是，您可以在 JavaScript 程式碼中自行實現邊緣函數不支援的內建函數或您的自訂函數，並透過 <code>loadPolicy()</code> 方法載入您實現的函數。參見 <a href="https://docs.byteplus.com/en/docs/18/57423#loadpolicy">loadPolicy()</a>。</div>


* <div data-tips="true" data-tips-type="warning">邊緣函數 CLI 預設您的 Rego 程式碼符合 OPA v1 的標準。如果您的 Rego 程式碼使用了 OPA v0 版本的特性，您需要在 <code>nest.json</code> 檔案中透過 <code>attachment.rego_version</code> 欄位明確指定所需的相容性版本。參見 <a href="https://docs.byteplus.com/en/docs/18/57423#rego-%E8%AA%9E%E8%A8%80%E7%89%88%E6%9C%AC%E7%9B%B8%E5%AE%B9%E6%80%A7%E8%AA%AA%E6%98%8E">Rego 語言版本相容性說明</a>。</div>



```rego
package example

default allow := false

allow if {
    input.method == "GET"
}
```


對於 OPA 專案，`nest.json` 檔案中的 `attachment` 欄位用於定義邊緣函數 CLI 處理 OPA 策略檔案的方式。


* **`rego_paths`**: 用於指定 OPA 策略檔案的路徑。Rego 是 OPA 使用的策略語言。因此， `rego_paths` 告訴系統在哪裡可以找到包含決策邏輯的 `.rego` 檔案。

* **`entrypoints`**: 定義了在 OPA 策略檔案中可以被查詢的具體規則。當需要進行策略評估時，系統會呼叫這裡定義的具體規則來取得決策結果。


以下是一個`attachment` 欄位的設定範例。在範例中：


* `["src/opa-demo.rego"]` 指明了策略檔案位於 `src/opa-demo.rego`。

* `["example/allow"]` 指的是在名為 example 的 package 下的 allow 規則。這意味著外部系統可以請求評估 example.allow 這條規則。


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">如果您希望使用一個自訂的、預先編譯好的 <code>.wasm</code> 檔案，而不是讓邊緣函數 CLI 從 <code>.rego</code> 檔案編譯，您可以在 <code>nest.json</code> 中設定 <code>functions.attachment.wasm_path</code> 欄位，並將其指向您的 Wasm 檔案路徑。</div>


```json
  "functions": [
    {
      "id": "",
      "name": "opa-demo",
      "type": "opa",
      "entry": "src/index.js",
      "attachment": {
        "rego_paths": [
          "src/opa-demo.rego"
        ],
        "entrypoints": [
          "example/allow"
        ]
      },
      "region": "outside_chinese_mainland"
    }
  ]
```


定義好 OPA 策略後，您需要編輯函數程式碼，以便在函數中呼叫 OPA 策略進行決策。

<span id="步驟三：編輯函數程式碼"></span>
### 步驟三：編輯函數程式碼

`OPA` 範本在 `src/index.js` 提供了一個初始的 JavaScript 程式碼檔案。該檔案載入了 OPA Javascript SDK，並根據 OPA 策略檔案定義的規則進行決策。該 SDK 基於 OPA Wasm Javascript Module 開發，但兩者並不完全相同。您可以參考 [OPA JavaScript SDK 參考](https://docs.byteplus.com/en/docs/18/57423#opa-javascript-sdk-%E5%8F%83%E8%80%83) 了解如何使用該 SDK，並根據需求自行修改程式碼。

```JavaScript
const { loadPolicy } = require("opa-wasm-sdk");

addEventListener("fetch", (event) =>
  event.respondWith(handleRequest(event.request))
);

// initialize a global opa policy
let policy = null;

/**
 * Takes in a custom function map and returns a loaded policy which can be
 * used to evaluate the policy.
 *
 * @param { Object[string, Function] } customBuiltins a map from name to custom builtins function
 * @returns {class} a loaded policy which can be used to evaluate the policy
 */
policy = loadPolicy();

function handleRequest(request) {
  if (policy == null) {
    return new Response("Policy not ready", {
      status: 503,
      statusText: "Service Unavailable",
    });
  }

  let inputJson = {
    method: request.method,
  };
  console.log(inputJson);

  /**
   * Evaluates the policy with any the given `input` and return the result set.
   * This should be re-used for multiple evaluations of the same policy with
   * different inputs.
   *
   * To call a non-default entrypoint in Wasm specify it as the second param. A
   * list of entrypoints can be accessed with the `this.entrypoints` prototype.
   *
   * The output of policy evaluation is a set of variable assignments. The
   * variable assignments specify values that satisfy the expressions in the
   * policy query (i.e., if the variables in the query are replaced with the
   * values from the assignments, all of the expressions in the query would be
   * defined and not false.)
   *
   * When policies are compiled into Wasm, the user provides the path of the
   * policy decision that should be exposed by the Wasm module. The policy
   * decision is assigned to a variable named result. The policy decision can
   * be ANY JSON value (boolean, string, object, etc.) but there will be
   * at-most-one assignment. This means that callers should first check if the
   * set of variable assignments is empty (indicating an undefined policy decision)
   * otherwise they should select the "result" key out of the variable assignment
   * set.
   *
   * @param {Object | ArrayBuffer>} input `input` parameter maybe an `object`,
   * primitive literal or `ArrayBuffer`, which assumed to be a well-formed stringified JSON.
   * @param {number | string>} entrypoints  ID or name of the entrypoint to call (optional)
   * @returns {Array} result set of evaluation（i.e.，[{"result": <value of example/allow>}]）
   */
  let r = policy.eval(inputJson);
  console.log(JSON.stringify(r));

  let allow = false;
  if (r.length === 1 && r[0]["result"] === true) {
    allow = true;
  }

  if (!allow) {
    return new Response("Forbidden", {
      status: 403,
      statusText: "Forbidden",
    });
  }

  return new Response("OK", { status: 200, statusText: "OK" });
}
```


完成程式碼編輯後，建議您在本地環境中對函數專案進行偵錯，以確保其行為符合預期。

<span id="步驟四：偵錯專案"></span>
### 步驟四：偵錯專案

在函數專案的根目錄執行 [nest start](https://docs.byteplus.com/docs/byteplus-cdn/cli-ref-nest-start-cn-zh-tw) 命令。該命令會編譯 `.rego` 檔案，打包 `.js` 檔案，然後執行函數程式碼。邊緣函數 CLI 會為邊緣函數 Debugger 啟動一個本地 HTTP 代理，並透過 wss 協定與邊緣函數 Debugger 建立連線。

```shell
$ npx nest start
==> Local http proxy running on 127.0.0.1:18080
==> Setting up debugger on wss://byteplusef-debugger.byteintlapi.com/f6663e0c-feb0-425f-b876-cea949946cdc...
==> [info]: Connection setup successfully!
==> [info]: Loading environment variables... ✓
==> [info]: Loading KV... ✓
==> [info]: Building function "opa-demo"...
==> [info]: Compile policies [/Users/example/opa-demo/src/example.rego] to [/Users/example/opa-demo/output/opa-demo/bundle.tar.gz] .
==> [info]: unpacking bundle to [/Users/example/opa-demo/output/opa-demo/bundle] .
==> [info]: Uploading function 'opa-demo': /Users/example/opa-demo/output/opa-demo/index.js... ✓
```


您透過 cURL 等工具向該位址傳送 HTTP 請求時，函數的網域名稱觸發器會觸發 fetch 事件。您可以透過這種方式驗證函數是否按預期工作。

<span id="偵錯範例"></span>
#### 偵錯範例

以 OPA 範本提供的 OPA 策略為例。由於 OPA 策略規定只允許 GET 請求，您可以分別傳送一個 POST 請求和一個 GET 請求來測試策略的有效性。


1. 執行以下命令，向函數傳送一個 GET 請求。


```shell
$ curl 127.0.0.1:18080 -v
*   Trying 127.0.0.1:18080...
* Connected to 127.0.0.1 (127.0.0.1) port 18080
> GET / HTTP/1.1
> Host: 127.0.0.1:18080
> User-Agent: curl/8.7.1
> Accept: */*
>
* Request completely sent off
< HTTP/1.1 200 OK
< Content-Type: text/plain;charset=UTF-8
< Date: Wed, 09 Jul 2025 07:11:07 GMT
< Server: Sparrow
< Transfer-Encoding: chunked
<
* Connection #0 to host 127.0.0.1 left intact
```


預期情況下，您會收到一個 `200 OK` 的回應，表示該請求符合 OPA 策略，已被函數成功處理。


2. 執行以下命令，向函數傳送一個 POST 請求。


```shell
$ curl -X POST 127.0.0.1:18080 -v
*   Trying 127.0.0.1:18080...
* Connected to 127.0.0.1 (127.0.0.1) port 18080
> POST / HTTP/1.1
> Host: 127.0.0.1:18080
> User-Agent: curl/8.7.1
> Accept: */*
>
* Request completely sent off
< HTTP/1.1 403 Forbidden
< Content-Type: text/plain;charset=UTF-8
< Date: Wed, 09 Jul 2025 07:17:16 GMT
< Server: Sparrow
< Transfer-Encoding: chunked
<
* Connection #0 to host 127.0.0.1 left intact
```


預期情況下，您會收到一個 `403 Forbidden` 的回應，表示該請求已被 OPA 策略成功攔截。

函數專案偵錯通過後，您可以將函數發布到邊緣伺服器。

<span id="步驟五：發布本地函數"></span>
### 步驟五：發布本地函數

在函數專案根目錄執行以下命令把本地函數發布到全球的邊緣伺服器。您必須先將函數全量發布之後，才能將其與網域名稱關聯。參見 [nest deploy](https://docs.byteplus.com/docs/byteplus-cdn/cli-ref-nest-deploy-cn-zh-tw)。

```shell
$ npx nest deploy --message "This is a new version"
```


命令列會提示您是否建立一個新的函數 ID。選擇 Yes 後按 Enter 鍵。邊緣函數 CLI 會在邊緣函數中建立一個對應的遠端函數，並將該遠端函數與您的本地函數同步。然後，邊緣函數 CLI 會把該遠端函數發布到全球的邊緣伺服器。

函數發布後，最後一步是驗證函數是否按預期工作。

<span id="步驟六：驗證函數"></span>
### 步驟六：驗證函數

函數發布後，您可以參考**步驟四：偵錯專案**中的方法，透過向您的網域名稱傳送 HTTP 請求來驗證函數是否按預期工作。

<span id="opa-javascript-sdk-參考"></span>
## OPA JavaScript SDK 參考

OPA JavaScript SDK 基於 OPA Wasm Javascript Module 開發，但兩者並不完全相同。本小節說明了如何使用 OPA JavaScript SDK 中的 `loadPolicy()` 方法、`policy.eval()` 方法、以及 `policy.setData()` 方法。

<span id="loadpolicy"></span>
### `loadPolicy()`

`loadPolicy()` 方法載入一個 OPA 策略，並返回一個可用於評估該策略的執行個體。

**語法**

```javascript
loadPolicy(customBuiltins)
```


**參數**


* `customBuiltins` *optional*

   一個物件，作為自訂函數的對應。物件的鍵是您希望在 Rego 策略中使用的函數名（字串），物件的值是對應的 JavaScript 函數。邊緣函數僅支援 [1.4.2 版本的 OPA 內建函數](https://v1-4-2--opa-docs.netlify.app/policy-reference/#built-in-functions)，您可以直接在 Rego 策略中使用這些內建函數。對於邊緣函數不支援的內建函數或您的自訂函數，您可以在 JavaScript 中實現它們，並把它們傳入 `customBuiltins` 參數。


**傳回值**

一個載入後的策略物件執行個體，該執行個體包含 `eval()` 和 `setData()` 等方法，可用於執行策略評估。

**範例**

<span id="使用自訂函數"></span>
#### 使用自訂函數

如果您希望在 Rego 策略中使用自訂的函數，您可以在 `loadPolicy()` 方法中傳入一個包含自訂函數實現的物件。

例如，假設您想在 Rego 策略中使用一個名為 `custom.path_check` 的函數來檢查請求路徑是否以 `/test` 開頭。


1. 在您的 Rego 策略檔案（例如 `example.rego`）中，您可以像下面這樣呼叫該自訂函數：

   ```rego
   package example
   
   default allow := false
   
   allow if {
       input.method == "GET"
       custom.path_check(input.path)
   }
   ```
   

2. 在您的 JavaScript 入口檔案（例如 `index.js`）中，您需要在 `loadPolicy()` 方法中提供 `custom.path_check` 函數的實現：

   ```javascript
   const { loadPolicy } = require("opa-wasm-sdk");
   
   addEventListener("fetch", (event) =>
     event.respondWith(handleRequest(event.request))
   );
   
   let policy = null;
   // Initialize a global opa policy
   policy = loadPolicy({
     "custom.path_check": (path) => {
       return path.startsWith("/test");
     },
   });
   
   function handleRequest(request) {
     if (policy == null) {
       return new Response("Policy not ready", {
         status: 503,
         statusText: "Service Unavailable",
       });
     }
   
     let url = new URL(request.url);
   
     let inputJson = {
       method: request.method,
       path: url.pathname,
     };
     console.log(inputJson);
   
     let r = policy.eval(inputJson);
     console.log(JSON.stringify(r));
   
     let allow = false;
     if (r.length === 1 && r[0]["result"] === true) {
       allow = true;
     }
   
     if (!allow) {
       return new Response("Forbidden", {
         status: 403,
         statusText: "Forbidden",
       });
     }
   
     return new Response("OK", { status: 200, statusText: "OK" });
   }
   ```
   

3. 您需要建立一個 `capabilities.json` 檔案來宣告自訂函數的簽章。這使得 OPA 能夠理解您的自訂函數並正確地將其整合到策略評估中。

   ```json
   {
     "builtins": [
       {
         "name": "custom.path_check",
         "decl": {
           "type": "function",
           "args": [
             { "type": "string" }
           ],
           "result": {
             "type": "boolean"
           }
         }
       }
     ]
   }
   ```
   

4. 在 `nest.json` 檔案中，您需要透過 `attachment.capabilities_path` 欄位指定 `capabilities.json` 檔案的路徑。這確保了邊緣函數 CLI 在建置和部署您的 OPA 函數時能夠找到並使用這個設定檔。

   ```json
   {
     "work_dir": "/Users/example/opa-demo",
     "src_dir": "src",
     "output_dir": "output",
     "cloud": {
       "api_server": "https://cdn.byteplusapi.com",
       "debug_server": "wss://byteplusef-debugger.byteintlapi.com",
       "api_version": "2021-03-01",
       "api_region": "ap-singapore-1",
       "api_timeout": 5000,
       "key_manager_url": "https://console.byteplus.com/iam/keymanage",
       "product": "CDN",
       "access_key": "",
       "secret_key": ""
     },
     "functions": [
       {
         "id": "",
         "name": "opa-test",
         "type": "opa",
         "entry": "src/index.js",
         "attachment": {
           "rego_paths": [
             "src/example.rego"
           ],
           "entrypoints": [
             "example/allow"
           ],
           "capabilities_path": "capabilities.json"
         },
         "region": "outside_chinese_mainland"
       }
     ]
   }
   ```
   


<span id="policy-eval"></span>
### `policy.eval()`

`policy.eval()` 方法使用給定的輸入評估載入的策略，並返回結果集。

**語法**

```javascript
policy.eval(input, entrypoint)
```


**參數**


* `input` *required*

   策略評估的輸入參數。它可以是一個 `object`、一個原始文字或一個 `ArrayBuffer`（假定為格式正確的字串化 JSON）。

* `entrypoint` *optional*

   要呼叫的進入點的 ID 或名稱。如果未指定，將使用預設進入點。


**傳回值**

一個表示評估結果集的陣列。例如，`[{"result": <value of example/allow>}]`。

**範例**

參見[步驟三：編輯函數程式碼](https://docs.byteplus.com/en/docs/18/57423#%E6%AD%A5%E9%A9%9F%E4%B8%89%E7%B7%A8%E8%BC%AF%E5%87%BD%E6%95%B8%E7%A8%8B%E5%BC%8F%E7%A2%BC)中的範例。

<span id="policy-setdata"></span>
### `policy.setData()`

`policy.setData()` 方法設定策略使用的資料。

**語法**

```javascript
policy.setData(data)
```


**參數**


* `data` *required*

   策略要使用的資料。它可以是一個 `object`、一個原始文字或一個 `ArrayBuffer`（假定為格式正確的字串化 JSON）。


**傳回值**

無。

**範例**

假設您有一個策略，檢查使用者是否在允許的使用者清單中。您可以使用 `policy.setData()` 來設定允許的使用者清單。


1. 在您的 Rego 策略檔案（例如 `example.rego`）中，您可以使用 `data` 關鍵字存取資料。

   ```rego
   package example
   
   default allow := false
   
   allow if {
       input.user in data.allowed_users
   }
   ```
   

2. 在您的 JavaScript 入口檔案（例如 `index.js`）中，您可以使用 `policy.setData()` 來設定 `allowed_users` 資料。

   ```javascript
   const { loadPolicy } = require("opa-wasm-sdk");
   
   addEventListener("fetch", (event) =>
     event.respondWith(handleRequest(event.request))
   );
   
   let policy = null;
   // Initialize a global opa policy
   policy = loadPolicy();
   
   // Set the data for the policy
   policy.setData({
       "allowed_users": ["alice", "bob"]
   });
   
   function handleRequest(request) {
     if (policy == null) {
       return new Response("Policy not ready", {
         status: 503,
         statusText: "Service Unavailable",
       });
     }
   
     let inputJson = {
       user: request.headers.get("user"),
     };
     console.log(inputJson);
   
     let r = policy.eval(inputJson);
     console.log(JSON.stringify(r));
   
     let allow = false;
     if (r.length === 1 && r[0]["result"] === true) {
       allow = true;
     }
   
     if (!allow) {
       return new Response("Forbidden", {
         status: 403,
         statusText: "Forbidden",
       });
     }
   
     return new Response("OK", { status: 200, statusText: "OK" });
   }
   ```
   


<span id="rego-語言版本相容性說明"></span>
## Rego 語言版本相容性說明

邊緣函數 CLI 預設您的 Rego 程式碼符合 OPA v1 的標準。如果您的 Rego 程式碼使用了 OPA v0 版本的特性，您需要在 `nest.json` 檔案中透過 `attachment.rego_version` 欄位明確指定所需的相容性版本。

例如，如果您的 Rego 程式碼使用了 `opa.runtime()` 內建函數，這是 OPA v0 的一個特性，您需要將 `attachment.rego_version` 設定為 `v0`。

```json
  "functions": [
    {
      "id": "",
      "name": "opa-demo",
      "type": "opa",
      "entry": "src/index.js",
      "attachment": {
        "rego_paths": [
          "src/opa-demo.rego"
        ],
        "entrypoints": [
          "example/allow"
        ],
        "rego_version": "v0"
      },
      "region": "outside_chinese_mainland"
    }
  ]
```
