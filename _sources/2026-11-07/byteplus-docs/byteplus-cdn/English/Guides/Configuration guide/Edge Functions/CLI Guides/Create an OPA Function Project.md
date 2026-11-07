---
title: "Create an OPA Function Project"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/create_function_project_with_opa_en"
---

This document describes how to use the Edge Functions CLI to create a function project that supports [Open Policy Agent (OPA)](https://www.openpolicyagent.org/).

<span id="what-is-opa"></span>
## What is OPA

OPA is an open\-source, general\-purpose policy engine that unifies policy enforcement across the cloud\-native technology stack. OPA provides a high\-level declarative language, Rego, that allows you to write policies as code and decouple policy implementation from the logic of the service itself.

When your service needs to make policy\-based decisions, it sends input data to OPA. OPA evaluates the input data based on predefined policies and generates decision results. This result can be a simple boolean value such as allow or deny, or a more complex structured document. Since policies are written in a declarative language, you can focus on the content of the policy itself, while OPA is responsible for executing these policies.

<span id="opa-application-scenarios"></span>
## OPA application scenarios

The flexibility of OPA makes it suitable for a variety of complex application scenarios, such as user request authentication and RBAC access control.

<span id="user-request-authentication"></span>
### User request authentication

In edge computing, a common requirement is to authenticate and authorize users before requests reach the origin server. For example, you can define a policy specifying that only users with administrator roles can access certain APIs, while users with visitor roles can only access other APIs.

<span id="rbac-access-control"></span>
### RBAC access control

Role\-based access control (RBAC) grants access to resources based on the user's role and responsibilities. For example, within an enterprise, different levels of system access can be granted based on employee positions and job functions. You can use OPA to define and implement complex RBAC policies. For example, you can define a policy that specifies that only users with the administrator role can access a certain API, while users with the guest role can only read data. This policy can be centrally managed and easily applied to multiple services.

<span id="how-edge-functions-evaluate-opa-policies"></span>
## How Edge Functions evaluate OPA policies

Edge Functions evaluate OPA policies through a built\-in WebAssembly (Wasm) module in its runtime. This module is responsible for loading and executing `.wasm` files compiled from `.rego` files. You can upload these `.wasm` files to Edge Functions using the Edge Functions CLI. When a function receives an HTTP request, the Wasm module evaluates the policy based on the request information and returns the decision result.

<span>![图片](https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/upload_795486d1f0d9a6e9b5df4d1467e893c4.jpeg) </span>

The specific process of how the Wasm module in Edge Functions runtime evaluates OPA policies is as follows:


1. **Prepare input**: The function listens for `fetch` events triggered by HTTP requests. After a `fetch` event is triggered, the function extracts the required data (such as Headers, URL, JWT, etc.) from the HTTP request and generates a JSON document based on the extracted data as input for policy evaluation by the Wasm module. For example, a simple JSON document is shown below:

   ```json
   {
     "method": "GET"
   }
   ```
   

   This JSON document will be passed to the Wasm module for evaluation. For example, a simple policy file (`policy.rego`) is as follows, which specifies that only the `GET` method is allowed:

   ```rego
       package example
       
       default allow := false
       
       allow if {
           input.method == "GET"
       }
   ```
   

2. **Execute policy evaluation**: The function calls the loaded policy in the Wasm module and passes the generated JSON document to it. The Wasm module evaluates the received JSON document according to the policy logic.

3. **Return decision result**: The Wasm module returns a JSON document containing the decision result, such as `[{"result": {"allow": true}}]`.

4. **Execute decision**: After receiving the decision result, the function can execute the corresponding business logic based on the result, such as allowing or denying a request, rewriting the Header, etc.

   For example, after executing the policy evaluation, you can check the `allow` field in the evaluation result. If it is `true`, the request is allowed; otherwise, a 403 Forbidden error is returned.

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
   


In addition, to simplify the development process, the Edge Functions CLI has a built\-in OPA compilation toolchain that can directly compile your `.rego` file into a `.wasm` file. This design allows you to not have to worry about the underlying compilation and integration details, and you can call OPA policies in your JavaScript code.

<span id="create-debug-and-publish-a-function-project-that-supports-opa"></span>
## Create, debug, and publish a function project that supports OPA

This section will guide you on how to use the Edge Functions CLI to create, debug, and publish a function project that supports OPA.

<span id="step-1-create-a-function-project-that-supports-opa"></span>
### Step 1: Create a function project that supports OPA

Run the following command on your device. This command will install the Edge Functions CLI, then create a function project that supports OPA, and create a local function in the function project. See [nest init](https://docs.byteplus.com/docs/byteplus-cdn/cli-ref-nest-init-en).

```shell
$ npx @byteplus/nest@latest init
```


You need to set the template used by the function to `OPA` according to the command line prompts, and set other parameters according to your needs. This article assumes that the name of the function is `opa-demo`.

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


After the command is executed, the structure of the function project is as follows:

```Plain Text
opa-demo/
├── src/
│   ├── index.js         # Entry file for JavaScript code
│   ├── opa-wasm-sdk/    # OPA Javascript SDK
│   └── opa-demo.rego    # OPA policy file
├── nest.json            # Project configuration file
├── package.json         # Node.js project information
└── node_modules/
```



* **`src/index.js`**: The entry file for the JavaScript code. You will call the OPA policy in this file.

* **`src/opa-demo.rego`**: The OPA policy file, written in the Rego language.

* **`src/opa-wasm-sdk`**: The OPA JavaScript SDK provided by Edge Functions. This SDK is developed based on the [OPA Wasm Javascript Module](https://www.openpolicyagent.org/ecosystem/entry/opa-wasm-js), but the two are not exactly the same. This SDK is already embedded in the project. You can use this SDK directly in `index.js`.

* **`nest.json`**: The function project configuration file.


After the project is created, the next step is to edit the OPA policy according to your business needs.

<span id="step-2-edit-the-opa-policy"></span>
### Step 2: Edit the OPA policy

The `OPA` template provides an initial OPA policy file in `src/opa-demo.rego`. You can open this file with any code editor and modify the code according to your needs.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>



* <div data-tips="true" data-tips-type="warning">Edge Functions only support version 1.4.2 of OPA. Therefore, you can only use the built\-in functions of OPA version 1.4.2. See <a href="https://v1-4-2--opa-docs.netlify.app/policy-reference">Policy Reference for version 1.4.2</a> to learn how to use OPA built\-in functions. However, you can implement built\-in functions not supported by Edge Functions or your custom functions in JavaScript code, and load your implemented functions through the <code>loadPolicy()</code> method. See <a href="https://docs.byteplus.com/en/docs/18/57425#loadpolicy">loadPolicy()</a>.</div>


* <div data-tips="true" data-tips-type="warning">The Edge Functions CLI defaults to your Rego code complying with the OPA v1 standard. If your Rego code uses features of OPA v0, you need to explicitly specify the required compatibility version through the <code>attachment.rego_version</code> field in the <code>nest.json</code> file. See <a href="https://docs.byteplus.com/en/docs/18/57425#rego-language-version-compatibility-description">Rego Language Version Compatibility Description</a>.</div>



```rego
package example

default allow := false

allow if {
    input.method == "GET"
}
```


For OPA projects, the `attachment` field in the `nest.json` file is used to define how the Edge Functions CLI handles OPA policy files.


* **`rego_paths`**: Used to specify the path of the OPA policy file. Rego is the policy language used by OPA. Therefore, `rego_paths` tells the system where to find the `.rego` file containing the decision logic.

* **`entrypoints`**: Defines the specific rules that can be queried in the OPA policy file. When a policy evaluation is required, the system will call the specific rules defined here to obtain the decision result.


The following is a configuration example of the `attachment` field. In the example:


* `["src/opa-demo.rego"]` indicates that the policy file is located at `src/opa-demo.rego`.

* `["example/allow"]` refers to the allow rule in the package named example. This means that an external system can request to evaluate the example.allow rule.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">If you want to use a custom, pre\-compiled <code>.wasm</code> file instead of letting the Edge Functions CLI compile from a <code>.rego</code> file, you can configure the <code>functions.attachment.wasm_path</code> field in <code>nest.json</code> and point it to your Wasm file path.</div>


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


After defining the OPA policy, you need to edit the function code so that you can call the OPA policy in the function to make decisions.

<span id="step-3-edit-the-function-code"></span>
### Step 3: Edit the function code

The `OPA` template provides an initial JavaScript code file in `src/index.js`. This file loads the OPA Javascript SDK and makes decisions based on the rules defined in the OPA policy file. This SDK is developed based on the OPA Wasm Javascript Module, but the two are not exactly the same. You can refer to [OPA JavaScript SDK Reference](https://docs.byteplus.com/en/docs/18/57425#opa-javascript-sdk-reference) to learn how to use this SDK and modify the code according to your needs.

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


After completing the code editing, it is recommended that you debug the function project in a local environment to ensure that its behavior meets expectations.

<span id="step-4-debug-the-project"></span>
### Step 4: Debug the project

Run the [nest start](https://docs.byteplus.com/docs/byteplus-cdn/cli-ref-nest-start-en) command in the root directory of the function project. This command will compile the `.rego` file, package the `.js` file, and then run the function code. The Edge Functions CLI will start a local HTTP proxy for the Edge Function Debugger and establish a connection with the Edge Function Debugger through the wss protocol.

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


When you send an HTTP request to this address through a tool such as cURL, the function's domain name trigger will trigger the fetch event. You can use this method to verify whether the function is working as expected.

<span id="debugging-example"></span>
#### Debugging example

Take the OPA policy provided by the OPA template as an example. Since the OPA policy only allows GET requests, you can send a POST request and a GET request respectively to test the validity of the policy.


1. Run the following command to send a GET request to the function.


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


Under normal circumstances, you will receive a `200 OK` response, indicating that the request complies with the OPA policy and has been successfully processed by the function.


2. Run the following command to send a POST request to the function.


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


Under normal circumstances, you will receive a `403 Forbidden` response, indicating that the request has been successfully intercepted by the OPA policy.

After the local function project passes debugging, you can publish the function to the edge nodes.

<span id="step-5-publish-the-local-function"></span>
### Step 5: Publish the local function

Run the following command in the root directory of the function project to publish the local function to the global edge nodes. You must first fully publish the function before you can associate it with a domain name. See [nest deploy](https://docs.byteplus.com/docs/byteplus-cdn/cli-ref-nest-deploy-en).

```shell
$ npx nest deploy --message "This is a new version"
```


The command line will prompt you whether to create a new function ID. Select Yes and press Enter. The Edge Functions CLI will create a corresponding remote function in the Edge Function and synchronize the remote function with your local function. Then, the Edge Functions CLI will publish the remote function to the global edge nodes.

After the function is published, the final step is to verify that the function is working as expected.

<span id="step-6-verify-the-function"></span>
### Step 6: Verify the function

After the function is published, you can refer to the method in **Step 4: Debug the Project** to verify whether the function is working as expected by sending an HTTP request to your domain name.

<span id="opa-javascript-sdk-reference"></span>
## OPA JavaScript SDK reference

The OPA JavaScript SDK is developed based on the OPA Wasm Javascript Module, but the two are not exactly the same. This section explains how to use the `loadPolicy()` method, the `policy.eval()` method, and the `policy.setData()` method in the OPA JavaScript SDK.

<span id="loadpolicy"></span>
### `loadPolicy()`

The `loadPolicy()` method loads an OPA policy and returns an instance that can be used to evaluate the policy.

**Syntax**

```javascript
loadPolicy(customBuiltins)
```


**Parameters**


* `customBuiltins` *optional*

   An object that serves as a mapping for custom functions. The keys of the object are the function names (strings) you want to use in the Rego policy, and the values are the corresponding JavaScript functions. Edge Functions only support [OPA built-in functions of version 1.4.2](https://v1-4-2--opa-docs.netlify.app/policy-reference/#built-in-functions), and you can use these built\-in functions directly in the Rego policy. For built\-in functions not supported by Edge Functions or your custom functions, you can implement them in JavaScript and pass them to the `customBuiltins` parameter.


**Return value**

A loaded policy object instance, which contains methods such as `eval()` and `setData()` that can be used to perform policy evaluation.

**Example**

<span id="using-custom-functions"></span>
#### Using custom functions

If you want to use custom functions in your Rego policy, you can pass an object containing the implementation of the custom functions to the `loadPolicy()` method.

For example, suppose you want to use a function named `custom.path_check` in your Rego policy to check if the request path starts with `/test`.


1. In your Rego policy file (e.g., `example.rego`), you can call this custom function as follows:

   ```rego
   package example
   
   default allow := false
   
   allow if {
       input.method == "GET"
       custom.path_check(input.path)
   }
   ```
   

2. In your JavaScript entry file (e.g., `index.js`), you need to provide the implementation of the `custom.path_check` function in the `loadPolicy()` method:

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
   

3. You need to create a `capabilities.json` file to declare the signature of the custom function. This allows OPA to understand your custom function and integrate it correctly into the policy evaluation.

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
   

4. In the `nest.json` file, you need to specify the path of the `capabilities.json` file through the `attachment.capabilities_path` field. This ensures that the Edge Functions CLI can find and use this configuration file when building and deploying your OPA function.

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

The `policy.eval()` method evaluates the loaded policy with the given input and returns the result set.

**Syntax**

```javascript
policy.eval(input, entrypoint)
```


**Parameters**


* `input` *required*

   The input parameter for the policy evaluation. It can be an `object`, a primitive literal, or an `ArrayBuffer` (which is assumed to be a well\-formed stringified JSON).

* `entrypoint` *optional*

   The ID or name of the entrypoint to call. If not specified, the default entrypoint will be used.


**Return value**

An array representing the result set of the evaluation. For example, `[{"result": <value of example/allow>}]`.

**Example**

See the example in [Step 3: Edit the Function Code](https://docs.byteplus.com/en/docs/18/57425#step-3-edit-the-function-code).

<span id="policy-setdata"></span>
### `policy.setData()`

The `policy.setData()` method sets the data used by the policy.

**Syntax**

```javascript
policy.setData(data)
```


**Parameters**


* `data` *required*

   The data to be used by the policy. It can be an `object`, a primitive literal, or an `ArrayBuffer` (which is assumed to be a well\-formed stringified JSON).


**Return value**

None.

**Example**

Suppose you have a policy that checks if a user is in a list of allowed users. You can use `policy.setData()` to set the list of allowed users.


1. In your Rego policy file (e.g., `example.rego`), you can access the data using the `data` keyword.

   ```rego
   package example
   
   default allow := false
   
   allow if {
       input.user in data.allowed_users
   }
   ```
   

2. In your JavaScript entry file (e.g., `index.js`), you can use `policy.setData()` to set the `allowed_users` data.

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
   


<span id="rego-language-version-compatibility"></span>
## Rego language version compatibility

The Edge Functions CLI defaults to your Rego code complying with the OPA v1 standard. If your Rego code uses features of OPA v0, you need to explicitly specify the required compatibility version through the `attachment.rego_version` field in the `nest.json` file.

For example, if your Rego code uses the `opa.runtime()` built\-in function, which is a feature of OPA v0, you need to set `attachment.rego_version` to `v0`.

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
