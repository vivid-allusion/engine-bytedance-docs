---
title: "快速入門：使用CLI建立並發佈函數"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/edge-functions-cli-quickstart-cn-zh-tw"
---

本教學基於簡單的範例場景介紹如何在您的裝置上使用邊緣函數 CLI 建立一個本地函數並發佈該本地函數。

<span id="範例場景"></span>
## 範例場景

您有一個網站，網域名稱是 `www.example.com`。您在 BytePlus CDN 新增了該網域名稱。您希望透過邊緣函數向用戶端返回自訂頁面。

<span id="執行環境要求"></span>
## 執行環境要求

執行邊緣函數 CLI 的裝置需要滿足以下要求：


* 作業系統必須屬於以下類型：

   * ARM64 macOS

   * x86\-64 macOS

   * ARM64 Linux

   * x86\-64 Linux

* 安裝了 [Node.js](https://nodejs.org/) 和 [npm](https://www.npmjs.com/)。版本要求如下：

   * Node.js：8.17.0 或更高版本

   * npm：6.13.4 或更高版本

* 安裝了 [wget](https://www.gnu.org/software/wget/) 或 [cURL](https://curl.se/)。


<span id="操作步驟"></span>
## 操作步驟

參見以下步驟在您的裝置上使用邊緣函數 CLI。


1. **安裝邊緣函數 CLI 並建立本地函數**：使用 `nest init` 指令安裝邊緣函數 CLI 並建立一個本地函數。

2. **設定您的 Access Key ID 和 Secret Access Key**：使用邊緣函數 CLI 設定您的 BytePlus 帳號的 Access Key ID 和 Secret Access Key 。

3. **編輯與偵錯程式碼**：編輯和偵錯本地函數的程式碼。

4. **發佈本地函數**：將本地函數發佈到 BytePlus CDN 的全球邊緣節點。

5. **關聯網域名稱並為網域名稱設定轉發規則**：把函數的觸發器設定為網域名稱觸發器，並在網域名稱觸發器中將函數與您的網域名稱關聯。同時為您的網域名稱設定轉發規則，當 BytePlus CDN 收到符合轉發規則的用戶端請求時，會將用戶端請求轉發到邊緣函數。

6. **驗證函數**：驗證函數的實際執行結果是否符合預期。


<span id="步驟一：安裝邊緣函數-cli-並建立本地函數"></span>
### 步驟一：安裝邊緣函數 CLI 並建立本地函數

在您的裝置上執行以下指令。該指令會安裝邊緣函數 CLI，然後建立一個函數專案，並在函數專案中建立一個本地函數。參見 [nest init](https://docs.byteplus.com/docs/byteplus-cdn/cli-ref-nest-init-cn-zh-tw)。

```shell
$ npx @byteplus/nest@latest init
```


您需要根據指令行提示，把函數名稱設定為 `HelloWorld`，其他設定都按 Enter 鍵設定為預設值。下面的範例中假設您執行指令的目錄是 `/Users/MyFolder`。

```shell
Need to install the following packages:
@byteplus/nest@1.0.0
Ok to proceed? (y) y
    
==> [debug]: Loading function from file "nest.json"
==> [debug]: Failed to load function config, read file "nest.json" error: open nest.json: no such file or directory
==> [debug]: Temporary function configuration will be used
✓ Name: HelloWorld
==> [info]: No AK&SK found, you can login to get more function templates. see also `nest config -h`
✓ Select a template you want to start with: Hello World
✓ Put code file in src/ directory?: Yes
✓ Entry File in src/ (optional, default is index.js): index.js
✓ Project Name (optional, default is "default"): 
✓ Description: 
==> 🛠️  Creating a BytePlus Function `HelloWorld` in directory /Users/MyFolder/HelloWorld ...
==> [info]: 📦  Generating package.json...
==> [info]: 🧾  Generating nest.json for project...
==> [info]: 🖨️  Generating code files from template...✓
==> [info]: 📥  Installing dependencies...✓
==> [info]: 👏  Done!, New function created at ./HelloWorld
    
==> Continue Developing
==> [info]: Change directory: cd ./HelloWorld
==> [info]: Start dev server: npm run start
    
==> Publish Function
==> [info]: Setting access_key: npm run nest config -g set cloud.access_key <your_access_key>
==> [info]: Setting secret_key: npm run nest config -g set cloud.secret_key <your_secret_key>
==> [info]: Deploy function: npm run deploy
==> [info]: 💡  You can find your AKSK at BytePlus(https://console.byteplus.com/iam/keymanage)
```


指令執行完成後，您當前的目錄結構如下：

```markdown
└── 📁MyFolder
    └── 📁HelloWorld
        └── nest.json
        └── package-lock.json
        └── package.json
        └── 📁src
            └── index.js
    └── package.json
```


其中，`HelloWorld` 目錄是您建立的函數專案，`HelloWorld/src/index.js` 是您的本地函數的入口檔案。

接下來，您需要設定您的 Access Key ID 和 Secret Access Key。

<span id="步驟二：設定您的-access-key-id-和-secret-access-key"></span>
### 步驟二：設定您的 Access Key ID 和 Secret Access Key

在 `HelloWorld` 目錄執行以下指令在邊緣函數 CLI 中設定您的 Access Key ID 和 Secret Access Key。您可以從 [BytePlus 控制台](https://console.byteplus.com/iam/keymanage)獲取 Access Key ID 和 Secret Access Key。參見 [nest config](https://docs.byteplus.com/docs/byteplus-cdn/cli-ref-nest-config-cn-zh-tw)。

```shell
npx nest config set -g cloud.access_key <access_key_id>
npx nest config set -g cloud.secret_key <secret_access_key>
```


接下來，您可以編輯和偵錯本地函數的程式碼。

<span id="步驟三：編輯與偵錯程式碼"></span>
### 步驟三：編輯與偵錯程式碼

參見以下步驟編輯和偵錯本地函數的程式碼。


1. 用任意程式碼編輯器開啟 `HelloWorld/src/index.js` 檔案，根據需求自行修改程式碼。本教學使用 HelloWorld 範本提供的程式碼。

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">程式碼中呼叫了 <a href="https://docs.byteplus.com/docs/byteplus-cdn/docs_cn-addEventListener-cn-zh-tw">addEventListener()</a> 用於註冊一個事件監聽器。參數中傳入了 <code>fetch</code> 和一個回呼函數 <code>{event.respondWith(handleResponse(event));}</code>。<code>fetch</code> 表示該事件監聽器會監聽 fetch 事件，如果 fetch 事件被網域名稱觸發器觸發，則回呼函數會被呼叫。您在步驟五會為函數設定網域名稱觸發器。參見 <a href="https://docs.byteplus.com/docs/byteplus-cdn/docs_cn-FetchEvent-cn-zh-tw">FetchEvent</a>。   </div>
   

   ```JavaScript
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
   

2. 在 `HelloWorld` 目錄執行以下指令進入 Debugger 命令列對程式碼進行偵錯。在偵錯程式碼前，您需要執行 `source` 指令把函數程式碼上傳到 Debugger。參見 [nest debug](https://docs.byteplus.com/docs/byteplus-cdn/cli-ref-nest-debug-cn-zh-tw) 了解如何使用 Debugger 命令列。

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">如果您在一段時間內沒有操作 Debugggr 命令列，Debugger 命令列會斷開連接並報告 <strong>Error: ws connection closed by server for timeout</strong> 錯誤。您可以執行 <code>npx nest debug</code> 重新啟動 Debugger 命令列。   </div>
   

   ```shell
   $ npx nest debug
     ______    _              ______                _   _             
    |  ____|  | |            |  ____|              | | (_)            
    | |__   __| | __ _  ___  | |__ _   _ _ __   ___| |_ _  ___  _ __  
    |  __| / _` |/ _` |/ _ \ |  __| | | | '_ \ / __| __| |/ _ \| '_ \ 
    | |___| (_| | (_| |  __/ | |  | |_| | | | | (__| |_| | (_) | | | |
    |______\__,_|\__, |\___| |_|   \__,_|_| |_|\___|\__|_|\___/|_| |_|
                  __/ |                                               
                 |___/                                                
                 
   ==> Setting up debugger...
   ==> [info]: connection setup successfully!
   ==> [info]: loading envrionment variables... ✓
   nest:  
   ```
   

   例如，下面的例子展示了先執行 source 把函數程式碼上傳到 Debugger，再執行 query 觸發函數程式碼執行。

   ```shell
   nest: source
   ==> [info]: building function "HelloWorld"... 
   ==> Uploading functions: [HelloWorld]... 
   nest: query
   ==> HttpResponse ✓
   status: 200
   
   statusText: OK
   
   header:
     content-type => text/plain;charset=UTF-8
     date => Fri, 17 Jan 2025 06:07:53 GMT
     server => Sparrow
     transfer-encoding => chunked
   
   body:
   Hello World!
   ```
   


函數程式碼偵錯完成後，您可以發佈本地函數。

<span id="步驟四：發佈本地函數"></span>
### 步驟四：發佈本地函數

在 `HelloWorld` 目錄執行以下指令把本地函數發佈到全球的邊緣節點。您必須先將函數全量發佈之後，才能將其與網域名稱關聯。參見 [nest deploy](https://docs.byteplus.com/docs/byteplus-cdn/cli-ref-nest-deploy-cn-zh-tw)。

```shell
npx nest deploy --message "This is a new version"
```


命令列會提示您是否建立一個新的函數 ID。選擇 Yes 後按 Enter 鍵。邊緣函數 CLI 會在邊緣函數中建立一個對應的遠端函數，並將該遠端函數與您的本地函數同步。然後，邊緣函數 CLI 會把該遠端函數發佈到全球的邊緣節點。

```shell
$ npx nest deploy --message "This is a new version"
==> Deploying function "HelloWorld"...
✓ Function HelloWorld has no id, create a new one for it?: Yes
==> [info]: Register function on remote cloud...✓
==> [info]: Building function "HelloWorld", entry=/Users/MyFolder/HelloWorld/src/index.js ... ✓
==> [info]: function "HelloWorld" was built into /Users/MyFolder/HelloWorld/output/HelloWorld/index.js .
==> [info]: Uploading "/Users/MyFolder/HelloWorld/output/HelloWorld/index.js" to remote cloud...✓
==> [info]: Publishing function code to edge node...✓
==> [info]: Function HelloWorld publish started, the ticket is 1887
==> [info]: Loading deploy ticket status...✓
==> [info]: The Full publish now is Publishing, version is: 1.0.1
==> [info]: Run `nest tickets 1887` to get more details

==> All functions were deployed successfully.
```


接下來，您需要為本地函數關聯網域名稱。

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">函數全量發佈一般需要 5 ~ 10 分鐘。您必須在函數全量發佈完成後才能為函數關聯網域名稱。</div>


<span id="步驟五：關聯網域名稱並為網域名稱設定轉發規則"></span>
### 步驟五：關聯網域名稱並為網域名稱設定轉發規則

在本示例中，您使用網域名稱觸發器觸發函數的執行。因此，您需要為函數關聯網域名稱`www.example.com`。您為網域名稱設定轉發規則後，如果 BytePlus CDN 收到一個與轉發規則匹配的用戶端請求，會把該請求轉發到邊緣函數。而且，網域名稱觸發器會觸發函數中的 fetch 事件。

執行以下指令為本地函數關聯網域名稱`www.example.com` 並為網域名稱設定轉發規則。參見 [nest domain](https://docs.byteplus.com/docs/byteplus-cdn/cli-ref-nest-domain-cn-zh-tw)。本示例不對用戶端請求的 URL 的路徑進行限制，因此：


* 規則類型需要被設定為 `--url-directory`，即 URL 目錄。

* 規則需要被設定為 `/`，表示匹配網域名稱下的全部路徑。


```shell
$ npx nest domain bind www.example.com   --url-directory /
==> [info]: Binding new domains to function...✓
==> [info]: Applying forward rules to domains...✓
```


您需要等待幾分鐘。然後在 HelloWorld 目錄執行 `npx nest domain list` 指令查看本地函數是否已經與網域名稱成功關聯且網域名稱觸發器是否已經對該本地函數生效。

```shell
$ npx nest domain list
+---------------------------+--------+-----------+---------+------------+
|          DOMAIN           | STATUS |   TYPE    | PATTERN | IGNORECASE |
+---------------------------+--------+-----------+---------+------------+
| www.example.com           | Online | directory | /       | false      |
+---------------------------+--------+-----------+---------+------------+
```


當網域名稱清單中出現了 www.example.com，且該網域名稱的狀態為 **Online** 時，表示網域名稱觸發器已經對該網域名稱生效。此時，如果用戶端向該網域名稱發起 HTTP 或 HTTPS 請求且該請求匹配轉發規則，那麼網域名稱觸發器會觸發與該網域名稱關聯的函數中的 fetch 事件。

接下來，您驗證函數的執行結果是否符合預期。

<span id="步驟六：驗證函數"></span>
### 步驟六：驗證函數

您可以存取 www.example.com，並驗證網頁的回應內容是否為 `Hello World!`。如果驗證無誤，則說明您的示例場景已實現。
