---
title: "快速入门：使用 CLI 创建并发布函数"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/edge-functions-cli-quickstart-cn"
---

本教程基于简单的示例场景介绍如何在您的设备上中使用边缘函数 CLI 创建一个本地函数并发布该本地函数。

<span id="示例场景"></span>
## 示例场景

您有一个网站，域名是 `www.example.com`。您在 BytePlus CDN 添加了该域名。您希望通过边缘函数向用户返回自定义页面。

<span id="运行环境要求"></span>
## 运行环境要求

运行边缘函数 CLI 的设备需要满足以下要求：


* 操作系统必须属于以下类型：

   * ARM64 macOS

   * x86\-64 macOS

   * ARM64 Linux

   * x86\-64 Linux

* 安装了 [Node.js](https://nodejs.org/) 和 [npm](https://www.npmjs.com/)。版本要求如下：

   * Node.js：8.17.0+

   * npm：6.13.4+

* 安装了 [wget](https://www.gnu.org/software/wget/) 或 [cURL](https://curl.se/)。


<span id="操作步骤"></span>
## 操作步骤

参见以下步骤在您的设备上使用边缘函数 CLI。

<span>![图片](https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/upload_179a02f459032ea7f59e13c4113f721a.png) </span>


1. **安装边缘函数 CLI 并创建本地函数**：使用 `nest init` 命令安装边缘函数 CLI 并创建一个本地函数。

2. **设置您的 Access Key ID 和 Secret Access Key**：使用边缘函数 CLI 设置您的 BytePlus 账号的 Access Key ID 和 Secret Access Key 。

3. **编辑与调试代码**：编辑和调试本地函数的代码。

4. **发布本地函数**：将本地函数发布到 BytePlus CDN 的全球边缘节点。

5. **关联域名并为域名配置转发规则**：把函数的触发器设置为域名触发器，并在域名触发器中将函数与您的域名关联。同时为您的域名配置转发规则，当 BytePlus CDN 收到匹配转发规则的用户请求时，会将用户请求转发到边缘函数。

6. **验证函数**：验证函数的实际执行结果是否符合预期。


<span id="步骤一：安装边缘函数-cli-并创建本地函数"></span>
### 步骤一：安装边缘函数 CLI 并创建本地函数

在您的设备上运行以下命令。该命令会安装边缘函数 CLI，然后创建一个函数项目，并在函数项目中创建一个本地函数。参见 [nest init](https://docs.byteplus.com/docs/byteplus-cdn/cli-ref-nest-init-cn)。

```shell
$ npx @byteplus/nest@latest init
```


您需要根据命令行提示，把函数名称设置为 `HelloWorld`，其他配置都按回车键设置为默认值。下面的示例中假设你运行命令的目录是 `/Users/MyFolder`。

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


命令运行完成后，您当前的目录结构如下：

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


其中，`HelloWorld` 目录是您创建的函数项目，`HelloWorld/src/index.js` 是您的本地函数的入口文件。

接下来，您需要设置您的 Access Key ID 和 Secret Access Key。

<span id="步骤二：设置您的-access-key-id-和-secret-access-key"></span>
### 步骤二：设置您的 Access Key ID 和 Secret Access Key

在 `HelloWorld` 目录运行以下命令在边缘函数 CLI 中设置您的 Access Key ID 和 Secret Access Key。您可以从 [BytePlus 控制台](https://console.byteplus.com/iam/keymanage)获取 Access Key ID 和 Secret Access Key。参见 [nest config](https://docs.byteplus.com/docs/byteplus-cdn/cli-ref-nest-config-cn)。

```shell
npx nest config set -g cloud.access_key <access_key_id>
npx nest config set -g cloud.secret_key <secret_access_key>
```


接下来，您可以编辑和调试本地函数的代码。

<span id="步骤三：编辑与调试代码"></span>
### 步骤三：编辑与调试代码

参见以下步骤编辑和调试本地函数的代码。


1. 用任意代码编辑器打开 `HelloWorld/src/index.js` 文件，根据需求自行修改代码。本教程使用 HelloWorld 模板提供的代码。

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">代码中调用了 <a href="https://docs.byteplus.com/docs/byteplus-cdn/docs_cn-addEventListener-cn">addEventListener()</a> 用于注册一个事件监听器。参数中传入了 <code>fetch</code> 和一个回调函数 <code>{event.respondWith(handleResponse(event));}</code>。<code>fetch</code> 表示该事件监听器会监听 fetch 事件，如果 fetch 事件被域名触发器触发，则回调函数会被调用。您在步骤五会为函数配置域名触发器。参见 <a href="https://docs.byteplus.com/docs/byteplus-cdn/docs_cn-FetchEvent-cn">FetchEvent</a>。   </div>
   

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
   

2. 在 `HelloWorld` 目录运行以下命令进入 Debugger 命令行对代码进行调试。在调试代码前，您需要运行 `source` 命令把函数代码上传到 Debugger。参见 [nest debug](https://docs.byteplus.com/docs/byteplus-cdn/cli-ref-nest-debug-cn) 了解如何使用 Debugger 命令行。

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">如果您在一段时间内没有操作 Debugggr 命令行，Debugger 命令行会断开连接并报告 <strong>Error: ws connection closed by server for timeout</strong> 错误。您可以运行 <code>npx nest debug</code> 重新启动 Debugger 命令行。   </div>
   

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
   

   例如，下面的例子展示了先运行 source 把函数代码上传到 Debugger，再运行 query 触发函数代码执行。

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
   


函数代码调试完成后，您可以发布本地函数。

<span id="步骤四：发布本地函数"></span>
### 步骤四：发布本地函数

在 `HelloWorld` 目录运行以下命令把本地函数发布到全球的边缘节点。您必须先将函数全量发布之后，才能将其与域名关联。参见 [nest deploy](https://docs.byteplus.com/docs/byteplus-cdn/cli-ref-nest-deploy-cn)。

```shell
npx nest deploy --message "This is a new version"
```


命令行会提示您是否创建一个新的函数 ID。选择 Yes 后按回车键。边缘函数 CLI 会在边缘函数中创建一个对应的远端函数，并将该远端函数与您的本地函数同步。然后，边缘函数 CLI 会把该远端函数发布到全球的边缘节点。

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


接下来，您需要为本地函数关联域名。

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">函数全量发布一般需要 5 ~ 10 分钟。您必须在函数全量发布完成后才能为函数关联域名。</div>


<span id="步骤五：关联域名并为域名配置转发规则"></span>
### 步骤五：关联域名并为域名配置转发规则

在本示例中，您使用域名触发器触发函数的执行。因此，您需要为函数关联域名`www.example.com`。您为域名配置转发规则后，如果 BytePlus CDN 收到一个与转发规则匹配的用户请求，会把该请求转发到边缘函数。而且，域名触发器会触发函数中的 fetch 事件。

运行以下命令为本地函数关联域名`www.example.com` 并为域名配置转发规则。参见 [nest domain](https://docs.byteplus.com/docs/byteplus-cdn/cli-ref-nest-domain-cn)。本示例不对用户请求的 URL 的路径进行限制，因此：


* 规则类型需要被设置为 `--url-directory`，即 URL 目录。

* 规则需要被设置为 `/`，表示匹配域名下的全部路径。


```shell
$ npx nest domain bind www.example.com   --url-directory /
==> [info]: Binding new domains to function...✓
==> [info]: Applying forward rules to domains...✓
```


您需要等待几分钟。然后在 HelloWorld 目录运行 `npx nest domain list` 命令查看本地函数是否已经与域名成功关联且域名触发器是否已经对该本地函数生效。

```shell
$ npx nest domain list
+---------------------------+--------+-----------+---------+------------+
|          DOMAIN           | STATUS |   TYPE    | PATTERN | IGNORECASE |
+---------------------------+--------+-----------+---------+------------+
| www.example.com           | Online | directory | /       | false      |
+---------------------------+--------+-----------+---------+------------+
```


当域名列表中出现了 www.example.com，且该域名的状态为 **Online** 时，表示域名触发器已经对该域名生效。此时，如果用户向该域名发起 HTTP 或 HTTPS 请求且该请求匹配转发规则，那么域名触发器会触发与该域名关联的函数中的 fetch 事件。

接下来，您验证函数的执行结果是否符合预期。

<span id="步骤六：验证函数"></span>
### 步骤六：验证函数

您可以访问 www.example.com，并验证网页的响应内容是否为 `Hello World!`。如果验证无误，则说明您的示例场景已实现。
