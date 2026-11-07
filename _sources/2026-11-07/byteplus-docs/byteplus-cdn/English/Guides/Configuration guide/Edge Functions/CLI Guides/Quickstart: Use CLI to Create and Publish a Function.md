---
title: "Quickstart: Use CLI to Create and Publish a Function"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/edge-functions-cli-quickstart-en"
---

This tutorial introduces how to create a local function using the Edge Functions CLI on your device and publish it, based on a simple example scenario.

<span id="example-scenario"></span>
## Example scenario

You have a website with the domain name `www.example.com`. You have added this domain to BytePlus CDN. You want to use Edge Functions to return a custom page to users.

<span id="runtime-environment-requirements"></span>
## Runtime environment requirements

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

Follow these steps to use the Edge Functions CLI on your device.

<span>![图片](https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/upload_cdcecfccb43fddb6171ea16ef3f6c254.png) </span>


1. **Install Edge Functions CLI and create a local function**: Use the `nest init` command to install the Edge Functions CLI and create a local function.

2. **Set your access key ID and secret access key**: Use the Edge Functions CLI to set your BytePlus account's Access Key ID and Secret Access Key.

3. **Edit and debug code**: Edit and debug the code of the local function.

4. **Publish the local function**: Publish the local function to BytePlus CDN's global edge nodes.

5. **Associate domain and configure forwarding rules**: Set the function's trigger as a domain trigger and associate the function with your domain in the domain trigger. At the same time, configure forwarding rules for your domain. When BytePlus CDN receives a user request that matches the forwarding rules, it will forward the user request to the Edge Function.

6. **Verify the function**: Verify if the actual execution result of the function meets expectations.


<span id="step-1-install-edge-functions-cli-and-create-a-local-function"></span>
### Step 1: Install Edge Functions CLI and create a local function

Run the following command on your device. This command will install the Edge Functions CLI, then create a function project, and create a local function within the function project. See [nest init](https://docs.byteplus.com/docs/byteplus-cdn/cli-ref-nest-init-en).

```shell
$ npx @byteplus/nest@latest init
```


You need to set the function name to `HelloWorld` according to the command line prompt, and press Enter to set other configurations to default values. The following example assumes that the directory where you run the command is `/Users/MyFolder`.

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


After the command is executed, your current directory structure will be as follows:

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


Here, the `HelloWorld` directory is the function project you created, and `HelloWorld/src/index.js` is the entry file for your local function.

Next, you need to set your Access Key ID and Secret Access Key.

<span id="step-2-set-your-access-key-id-and-secret-access-key"></span>
### Step 2: Set your access key ID and secret access key

Run the following commands in the `HelloWorld` directory to set your Access Key ID and Secret Access Key in the Edge Functions CLI. You can obtain your Access Key ID and Secret Access Key from the [BytePlus Console](https://console.byteplus.com/iam/keymanage). See [nest config](https://docs.byteplus.com/docs/byteplus-cdn/cli-ref-nest-config-en).

```shell
npx nest config set -g cloud.access_key <access_key_id>
npx nest config set -g cloud.secret_key <secret_access_key>
```


Next, you can edit and debug the code of the local function.

<span id="step-3-edit-and-debug-code"></span>
### Step 3: Edit and debug code

Follow these steps to edit and debug the code of the local function.


1. Open the `HelloWorld/src/index.js` file with any code editor and modify the code according to your needs. This tutorial uses the code provided by the HelloWorld template.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">The code calls <a href="https://docs.byteplus.com/docs/byteplus-cdn/docs-addEventListener">addEventListener()</a> to register an event listener. The parameters passed include <code>fetch</code> and a callback function <code>{event.respondWith(handleResponse(event));}</code>. <code>fetch</code> indicates that this event listener will listen for fetch events, and if a fetch event is triggered by a domain trigger, the callback function will be called. You will configure the domain trigger for the function in step five. See <a href="https://docs.byteplus.com/docs/byteplus-cdn/docs-FetchEvent">FetchEvent</a>.   </div>
   

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
   

2. Run the following command in the `HelloWorld` directory to enter the Debugger command line to debug the code. Before debugging the code, you need to run the `source` command to upload the function code to the Debugger. See [nest debug](https://docs.byteplus.com/docs/byteplus-cdn/cli-ref-nest-debug-en) to learn how to use the Debugger command line.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">If you don't operate the Debugger command line for a period of time, the Debugger command line will disconnect and report an <strong>Error: ws connection closed by server for timeout</strong> error. You can run <code>npx nest debug</code> to restart the Debugger command line.   </div>
   

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
   

   For example, the following example shows running `source` first to upload the function code to the Debugger, then running `query` to trigger the function code execution.

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
   


After debugging the function code, you can publish the local function.

<span id="step-4-publish-the-local-function"></span>
### Step 4: Publish the local function

Run the following command in the `HelloWorld` directory to publish the local function to global edge nodes. You must fully publish the function before you can associate it with a domain. See [nest deploy](https://docs.byteplus.com/docs/byteplus-cdn/cli-ref-nest-deploy-en).

```shell
npx nest deploy --message "This is a new version"
```


The command line will prompt you whether to create a new function ID. Select Yes and press Enter. The Edge Functions CLI will create a corresponding remote function in Edge Functions and synchronize it with your local function. Then, the Edge Functions CLI will publish this remote function to global edge nodes.

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


Next, you need to associate a domain with the local function.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">Full function publication generally takes 5 to 10 minutes. You must wait for the function to be fully published before associating a domain with the function.</div>


<span id="step-5-associate-domain-and-configure-forwarding-rules"></span>
### Step 5: Associate domain and configure forwarding rules

In this example, you use a domain trigger to trigger the function execution. Therefore, you need to associate the function with the domain `www.example.com`. After you configure forwarding rules for the domain, if BytePlus CDN receives a user request that matches the forwarding rules, it will forward that request to the Edge Function. Moreover, the domain trigger will trigger the fetch event in the function.

Run the following command to associate the local function with the domain `www.example.com` and configure forwarding rules for the domain. See [nest domain](https://docs.byteplus.com/docs/byteplus-cdn/cli-ref-nest-domain-en). This example does not restrict the path of the user request URL, so:


* The rule type needs to be set to `--url-directory`, which means URL directory.

* The rule needs to be set to `/`, indicating a match for all paths under the domain.


```shell
$ npx nest domain bind www.example.com   --url-directory /
==> [info]: Binding new domains to function...✓
==> [info]: Applying forward rules to domains...✓
```


You need to wait for a few minutes. Then run the `npx nest domain list` command in the HelloWorld directory to check if the local function has been successfully associated with the domain and if the domain trigger has taken effect for this local function.

```shell
$ npx nest domain list
+---------------------------+--------+-----------+---------+------------+
|          DOMAIN           | STATUS |   TYPE    | PATTERN | IGNORECASE |
+---------------------------+--------+-----------+---------+------------+
| www.example.com           | Online | directory | /       | false      |
+---------------------------+--------+-----------+---------+------------+
```


When www.example.com appears in the domain list and its status is **Online**, it indicates that the domain trigger has taken effect for this domain. At this point, if a user sends an HTTP or HTTPS request to this domain and the request matches the forwarding rules, the domain trigger will trigger the fetch event in the function associated with this domain.

Next, you verify if the function's execution result meets expectations.

<span id="step-6-verify-the-function"></span>
### Step 6: Verify the function

You can visit www.example.com and verify if the webpage's response content is `Hello World!`. If the verification is successful, it means your example scenario has been implemented.
