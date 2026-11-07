---
title: "创建 OPA 函数项目"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/create_function_project_with_opa_zh-cn"
---

本文档介绍如何使用边缘函数 CLI 创建一个支持[开放策略代理（Open Policy Agent, OPA）](https://www.openpolicyagent.org/)的函数项目。

<span id="什么是-opa"></span>
## 什么是 OPA

OPA 是一个开源的通用策略引擎，统一了云原生技术栈中的策略实施。OPA 提供了一种高级声明性语言 Rego，使您能够将策略编写为代码，并将策略实现从服务本身的逻辑中解耦。

当您的服务需要做出基于策略的决策时，会把输入数据发送给 OPA。OPA 根据预先定义的策略对输入数据进行评估并生成决策结果。这个结果可以是一个简单的布尔值，例如允许或拒绝，也可以是一个更复杂的结构化文档。由于策略是用声明性语言编写的，您可以专注于策略本身的内容，而 OPA 则负责执行这些策略。

<span id="opa-的应用场景"></span>
## OPA 的应用场景

OPA 的灵活性使其适用于多种复杂的应用场景，例如用户请求鉴权和 RBAC 访问控制。

<span id="用户请求鉴权"></span>
### 用户请求鉴权

在边缘计算中，一个常见的需求是在请求到达源站之前对用户进行身份验证和授权。例如，您可以使用 OPA 来保护付费内容，过滤掉未授权的请求，从而增强源站的安全性。

<span id="rbac-访问控制"></span>
### RBAC 访问控制

基于角色的访问控制（RBAC）根据用户的角色和职责来授予对资源的访问权限。例如，在企业内部，可以根据员工的职位和工作职能，授予不同级别的系统访问权限。您可以使用 OPA 来定义和实施复杂的 RBAC 策略。例如，您可以定义一个策略，规定只有管理员角色的用户才能访问某些 API，而访客角色的用户只能访问另外一些 API。这种策略可以集中管理，并轻松应用于多个服务。

<span id="边缘函数如何评估-opa-策略"></span>
## 边缘函数如何评估 OPA 策略

边缘函数通过其运行时中内置的 WebAssembly (Wasm) 模块来评估 OPA 策略。该模块负责加载和执行由 `.rego` 文件编译而来的 `.wasm` 文件。您可以通过边缘函数 CLI 向边缘函数上传该 `.wasm` 文件。当函数接收到 HTTP 请求时，Wasm 模块会根据请求信息进行策略评估，并返回决策结果。

<span>![图片](https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/upload_795486d1f0d9a6e9b5df4d1467e893c4.jpeg) </span>

边缘函数运行时的 Wasm 模块评估 OPA 策略的具体流程如下：


1. **准备输入**：函数监听由 HTTP 请求触发的 `fetch` 事件。`fetch` 事件触发后，函数会从该 HTTP 请求中提取所需数据（如 Header、URL、JWT 等），并基于提取的数据生成一个 JSON 文档作为输入，供 Wasm 模块进行策略评估。例如，一个简单的 JSON 文档如下所示：

   ```json
   {
     "method": "GET"
   }
   ```
   

   该 JSON 文档会传递给 Wasm 模块进行评估。例如，一个简单的策略文件（`policy.rego`）如下所示，它规定了只允许 `GET` 方法：

   ```rego
       package example
       
       default allow := false
       
       allow if {
           input.method == "GET"
       }
   ```
   

2. **执行策略评估**：函数调用 Wasm 模块中已加载的策略，并将生成的 JSON 文档传递给 Wasm 模块。Wasm 模块根据策略逻辑对收到的 JSON 文档进行评估。

3. **返回决策结果**：Wasm 模块返回一个包含决策结果的 JSON 文档。例如，`[{"result": {"allow": true}}]`。

4. **执行决策**：函数接收到决策结果后，便可以根据该结果执行相应的业务逻辑，例如允许或拒绝一个请求、改写 Header 等。

   例如，在执行策略评估后，您可以检查评估结果中的 `allow` 字段。如果为 `true`，则允许请求；否则，返回 403 Forbidden 错误。

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
   


此外，为了简化开发流程，边缘函数 CLI 内置了 OPA 的编译工具链，可将您的 `.rego`文件直接编译成 `.wasm` 文件。这种设计使您无需关心底层的编译和集成细节，在 JavaScript 代码中即可调用 OPA 策略。

<span id="创建、调试和发布一个支持-opa-的函数项目"></span>
## 创建、调试和发布一个支持 OPA 的函数项目

本小节将指导您如何使用边缘函数 CLI 创建、调试和发布一个支持 OPA 的函数项目。

<span id="步骤一：创建一个支持-opa-的函数项目"></span>
### 步骤一：创建一个支持 OPA 的函数项目

在您的设备上运行以下命令。该命令会安装边缘函数 CLI，然后创建一个支持 OPA 的函数项目，并在函数项目中创建一个本地函数。参见 [nest init](https://docs.byteplus.com/docs/byteplus-cdn/cli-ref-nest-init-cn)。

```shell
$ npx @byteplus/nest@latest init
```


您需要根据命令行提示把函数使用的模板设置为 `OPA`，并根据您的需求设置其他参数。本文假设函数的名称为 `opa-demo`。

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


命令执行完成后，函数项目的结构如下：

```Plain Text
opa-demo/
├── src/
│   ├── index.js         # JavaScript 代码的入口文件
│   ├── opa-wasm-sdk/    # OPA Javascript SDK
│   └── opa-demo.rego    # OPA 策略文件
├── nest.json            # 项目配置文件
├── package.json         # Node.js 项目信息
└── node_modules/
```



* **`src/index.js`**: JavaScript 代码的入口文件。您将在此文件中调用 OPA 策略。

* **`src/opa-demo.rego`**: OPA 策略文件，基于 Rego 语言编写。

* **`src/opa-wasm-sdk`**: 边缘函数提供的 OPA JavaScript SDK。该 SDK 基于 [OPA Wasm Javascript Module](https://www.openpolicyagent.org/ecosystem/entry/opa-wasm-js) 开发，但两者并不完全相同。该 SDK 已内嵌在项目中。您可以在 `index.js` 中直接使用该 SDK。

* **`nest.json`**: 函数项目配置文件。


项目创建完成后，下一步是根据您的业务需求编辑 OPA 策略。

<span id="步骤二：编辑-opa-策略"></span>
### 步骤二：编辑 OPA 策略

`OPA` 模板在 `src/opa-demo.rego` 提供了一个初始的 OPA 策略文件。您可以用任意代码编辑器打开该文件，根据需求自行修改代码。

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>



* <div data-tips="true" data-tips-type="warning">边缘函数仅支持 1.4.2 版本的 OPA。因此，您只能使用 1.4.2 版本的 OPA 内置函数。参见 <a href="https://v1-4-2--opa-docs.netlify.app/policy-reference">1.4.2 版本的 Policy Reference</a> 了解如何使用 OPA 内置函数。但是，您可以在 JavaScript 代码中自行实现边缘函数不支持的内置函数或您的自定义函数，并通过 <code>loadPolicy()</code> 方法加载您实现的函数。参见 <a href="https://docs.byteplus.com/en/docs/18/54372#loadpolicy">loadPolicy()</a>。</div>


* <div data-tips="true" data-tips-type="warning">边缘函数 CLI 默认您的 Rego 代码符合 OPA v1 的标准。如果您的 Rego 代码使用了 OPA v0 版本的特性，您需要在 <code>nest.json</code> 文件中通过 <code>attachment.rego_version</code> 字段明确指定所需的兼容性版本。参见 <a href="https://docs.byteplus.com/en/docs/18/54372#rego-%E8%AF%AD%E8%A8%80%E7%89%88%E6%9C%AC%E5%85%BC%E5%AE%B9%E6%80%A7%E8%AF%B4%E6%98%8E">Rego 语言版本兼容性说明</a>。</div>



```rego
package example

default allow := false

allow if {
    input.method == "GET"
}
```


对于 OPA 项目，`nest.json` 文件中的 `attachment` 字段用于定义边缘函数 CLI 处理 OPA 策略文件的方式。


* **`rego_paths`**: 用于指定 OPA 策略文件的路径。Rego 是 OPA 使用的策略语言。因此， `rego_paths` 告诉系统在哪里可以找到包含决策逻辑的 `.rego` 文件。

* **`entrypoints`**: 定义了在 OPA 策略文件中可以被查询的具体规则。当需要进行策略评估时，系统会调用这里定义的具体规则来获取决策结果。


以下是一个`attachment` 字段的配置示例。在示例中：


* `["src/opa-demo.rego"]` 指明了策略文件位于 `src/opa-demo.rego`。

* `["example/allow"]` 指的是在名为 example 的 package 下的 allow 规则。这意味着外部系统可以请求评估 example.allow 这条规则。


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">如果您希望使用一个自定义的、预先编译好的 <code>.wasm</code> 文件，而不是让边缘函数 CLI 从 <code>.rego</code> 文件编译，您可以在 <code>nest.json</code> 中配置 <code>functions.attachment.wasm_path</code> 字段，并将其指向您的 Wasm 文件路径。</div>


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


定义好 OPA 策略后，您需要编辑函数代码，以便在函数中调用 OPA 策略进行决策。

<span id="步骤三：编辑函数代码"></span>
### 步骤三：编辑函数代码

`OPA` 模板在 `src/index.js` 提供了一个初始的 JavaScript 代码文件。该文件加载了 OPA Javascript SDK，并根据 OPA 策略文件定义的规则进行决策。该 SDK 基于 OPA Wasm Javascript Module 开发，但两者并不完全相同。您可以参考 [OPA JavaScript SDK 参考](https://docs.byteplus.com/en/docs/18/54372#opa-javascript-sdk-%E5%8F%82%E8%80%83) 了解如何使用该 SDK，并根据需求自行修改代码。

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


完成代码编辑后，建议您在本地环境中对函数项目进行调试，以确保其行为符合预期。

<span id="步骤四：调试项目"></span>
### 步骤四：调试项目

在函数项目的根目录运行 [nest start](https://docs.byteplus.com/docs/byteplus-cdn/cli-ref-nest-start-cn) 命令。该命令会编译 `.rego` 文件，打包 `.js` 文件，然后运行函数代码。边缘函数 CLI 会为边缘函数 Debugger 启动一个本地 HTTP 代理，并通过 wss 协议与边缘函数 Debugger 建立连接。

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


您通过 cURL 等工具向该地址发送 HTTP 请求时，函数的域名触发器会触发 fetch 事件。您可以通过这种方式验证函数是否按预期工作。

<span id="调试示例"></span>
#### 调试示例

以 OPA 模板提供的 OPA 策略为例。由于 OPA 策略规定只允许 GET 请求，您可以分别发送一个 POST 请求和一个 GET 请求来测试策略的有效性。


1. 运行以下命令，向函数发送一个 GET 请求。


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


预期情况下，您会收到一个 `200 OK` 的响应，表示该请求符合 OPA 策略，已被函数成功处理。


2. 运行以下命令，向函数发送一个 POST 请求。


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


预期情况下，您会收到一个 `403 Forbidden` 的响应，表示该请求已被 OPA 策略成功拦截。

函数项目在本地调试通过后，您可以将函数发布到边缘节点。

<span id="步骤五：发布本地函数"></span>
### 步骤五：发布本地函数

在函数项目根目录运行以下命令把本地函数发布到全球的边缘节点。您必须先将函数全量发布之后，才能将其与域名关联。参见 [nest deploy](https://docs.byteplus.com/docs/byteplus-cdn/cli-ref-nest-deploy-cn)。

```shell
$ npx nest deploy --message "This is a new version"
```


命令行会提示您是否创建一个新的函数 ID。选择 Yes 后按回车键。边缘函数 CLI 会在边缘函数中创建一个对应的远端函数，并将该远端函数与您的本地函数同步。然后，边缘函数 CLI 会把该远端函数发布到全球的边缘节点。

函数发布后，最后一步是验证函数是否按预期工作。

<span id="步骤六：验证函数"></span>
### 步骤六：验证函数

函数发布后，您可以参考**步骤四：调试项目**中的方法，通过向您的域名发送 HTTP 请求来验证函数是否按预期工作。

<span id="opa-javascript-sdk-参考"></span>
## OPA JavaScript SDK 参考

OPA JavaScript SDK 基于 OPA Wasm Javascript Module 开发，但两者并不完全相同。本小节说明了如何使用 OPA JavaScript SDK 中的 `loadPolicy()` 方法、`policy.eval()` 方法、以及 `policy.setData()` 方法。

<span id="loadpolicy"></span>
### `loadPolicy()`

`loadPolicy()` 方法加载一个 OPA 策略，并返回一个可用于评估该策略的实例。

**语法**

```javascript
loadPolicy(customBuiltins)
```


**参数**


* `customBuiltins` *optional*

   一个对象，作为自定义函数的映射。对象的键是您希望在 Rego 策略中使用的函数名（字符串），对象的值是对应的 JavaScript 函数。边缘函数仅支持 [1.4.2 版本的 OPA 内置函数](https://v1-4-2--opa-docs.netlify.app/policy-reference/#built-in-functions)，您可以直接在 Rego 策略中使用这些内置函数。对于边缘函数不支持的内置函数或您的自定义函数，您可以在 JavaScript 中实现它们，并把它们传入 `customBuiltins` 参数。


**返回值**

一个加载后的策略对象实例，该实例包含 `eval()` 和 `setData()` 等方法，可用于执行策略评估。

**示例**

<span id="使用自定义函数"></span>
#### 使用自定义函数

如果您希望在 Rego 策略中使用自定义的函数，您可以在 `loadPolicy()` 方法中传入一个包含自定义函数实现的对象。

例如，假设您想在 Rego 策略中使用一个名为 `custom.path_check` 的函数来检查请求路径是否以 `/test` 开头。


1. 在您的 Rego 策略文件（例如 `example.rego`）中，您可以像下面这样调用该自定义函数：

   ```rego
   package example
   
   default allow := false
   
   allow if {
       input.method == "GET"
       custom.path_check(input.path)
   }
   ```
   

2. 在您的 JavaScript 入口文件（例如 `index.js`）中，您需要在 `loadPolicy()` 方法中提供 `custom.path_check` 函数的实现：

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
   

3. 您需要创建一个 `capabilities.json` 文件来声明自定义函数的签名。这使得 OPA 能够理解您的自定义函数并正确地将其集成到策略评估中。

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
   

4. 在 `nest.json` 文件中，您需要通过 `attachment.capabilities_path` 字段指定 `capabilities.json` 文件的路径。这确保了边缘函数 CLI 在构建和部署您的 OPA 函数时能够找到并使用这个配置文件。

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
           "capabilities_path": "src/capabilities.json"
         },
         "region": "outside_chinese_mainland"
       }
     ],
     "debugger": {}
   }
   ```
   


<span id="使用边缘函数不支持的-opa-内置函数"></span>
#### 使用边缘函数不支持的 OPA 内置函数

对于边缘函数不支持的 OPA 内置函数，其使用方法与自定义函数基本一致。您需要在 `loadPolicy()` 方法中提供该内置函数的 JavaScript 实现。唯一区别在于，您无需提供 `capabilities.json` 文件，因为这些函数已经在 OPA 中预先声明。

<span id="policy-eval"></span>
### `policy.eval()`

`policy.eval()` 方法使用给定的 `input` 来评估策略，并返回结果集。对于同一策略和不同输入的多次评估，应重用此方法。

**语法**

```javascript
policy.eval(input, entrypoint)
```


**参数**


* `input` *required*

   一个 `Object`、原始值（primitive value）或 `ArrayBuffer`。该参数作为策略评估的输入。如果输入是 `ArrayBuffer`，则假定其为一个格式正确的字符串化 JSON。

* `entrypoint` *optional*

   一个 `number` 或 `string`，表示要调用的入口点的 ID 或名称。您可以通过 `this.entrypoints` 原型访问入口点列表。


**返回值**

一个 `Array`，表示评估的结果集。例如 `[{"result":true}]`。

策略评估的输出是一组变量赋值。这些变量赋值指定了满足策略查询中表达式的值。也就是说，如果查询中的变量被替换为赋值中的值，那么查询中的所有表达式都将被定义且不为 false。

当策略被编译为 Wasm 时，用户需要提供应由 Wasm 模块公开的策略决策的路径。策略决策被分配给一个名为 `result` 的变量。策略决策可以是任何 JSON 值（布尔值、字符串、对象等），但最多只有一个赋值。这意味着调用者应首先检查变量赋值集是否为空（表示未定义的策略决策），否则应从变量赋值集中选择 `result` 键。

<span id="policy-setdata"></span>
### `policy.setData()`

`setData()` 方法为策略评估提供一个外部的 `data` document。

**语法**

```javascript
policy.setData(data)
```


**参数**


* `data` *required*

   一个可序列化的 `Object` 或 `ArrayBuffer`。此参数作为策略评估的外部数据源，对应于 Rego 策略中的 `data` document。


**示例**

以下示例演示了如何使用 `setData()` 提供数据，并在 Rego 策略中引用它。

**JavaScript (** **`index.js`** **)** 

```javascript
policy.setData({
  foo: "bar",
});
let r = policy.eval(inputJson);
console.log(JSON.stringify(r));
```


**Rego (** **`policy.rego`** **)** 

```rego
package example

default allow := false

allow if {
    data.foo == "bar"
}
```


<span id="rego-语言版本兼容性说明"></span>
## Rego 语言版本兼容性说明

边缘函数 CLI 默认您的 Rego 代码符合 OPA v1 版本的标准。如果您的 Rego 代码使用了 OPA v0 版本的特性，您需要在 `nest.json` 文件中通过 `attachment.rego_version` 字段明确指定所需的兼容性版本。

关于 v0 和 v1 版本间的具体差异，参见 [v0 Backwards Compatibility](https://www.openpolicyagent.org/docs/v0-compatibility)。

`rego_version` 字段支持以下值：


* **`v1`**: （默认值）仅支持 `v1` 版本的特性。

* **`v0`**: 仅支持 `v0` 版本的特性。

* **`v0v1`**: 同时支持 `v0` 和 `v1` 版本的特性。


**配置示例**

以下示例展示了如何在 `nest.json` 中将 Rego 语言版本设置为 `v0`：

```json
{
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
        "rego_version": "v0"
      },
      "region": "outside_chinese_mainland"
    }
  ],
  "debugger": {}
}

```
