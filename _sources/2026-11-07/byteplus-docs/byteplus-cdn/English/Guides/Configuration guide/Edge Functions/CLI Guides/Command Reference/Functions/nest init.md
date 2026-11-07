---
title: "nest init"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/cli-ref-nest-init-en"
---

Creates a function project in the current directory and then creates a local function within the function project.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">You don't need to set up an access key ID and secret access key to run this command.</div>


<span id="synopsis"></span>
## Synopsis

```shell
npx nest init <dir> --env --sync --function <function_id>
```


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">You can also directly run the following command to quickly install the Edge Functions CLI and create a local function. There's no need to install the Edge Functions CLI before running this command.</div>


<div data-tips="true" data-tips-type="tip">```shell
npx @byteplus/nest init --env --sync --function <function_id>
```
</div>


<div data-tips="true" data-tips-type="tip">This command performs the following operations in order:</div>



1. <div data-tips="true" data-tips-type="tip">Creates a Node.js project in the current directory.</div>


2. <div data-tips="true" data-tips-type="tip">Installs the Edge Functions CLI in the Node.js project.</div>


3. <div data-tips="true" data-tips-type="tip">Runs the Edge Functions CLI to create a function project in the current directory and create a local function within the function project.</div>



<span id="description"></span>
## Description

The npx command will create a function project in the directory where you run `npx nest init`, then prompt you to enter the function name, select a function template, specify the location and name of the entry file, choose the associated BytePlus project, provide a function description, and other information. Then, the Edge Functions CLI will create a local function based on the information you input.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">Function names must be unique under each BytePlus account. The naming rules are as follows:</div>


   * <div data-tips="true" data-tips-type="tip">Supports English letters, numbers, and hyphens (\-).</div>


   * <div data-tips="true" data-tips-type="tip">The length must not exceed 128 characters.</div>


* <div data-tips="true" data-tips-type="tip">The function templates available to you depend on whether you have set up your Access Key ID and Secret Access Key:</div>


   * <div data-tips="true" data-tips-type="tip">If you haven't set up your Access Key ID and Secret Access Key, you can only use the HelloWorld template.</div>


   * <div data-tips="true" data-tips-type="tip">If you have set up your Access Key ID and Secret Access Key, you can use all templates supported by edge functions.</div>


* `<dir>` : string, optional

* The directory where the function project will be created. Defaults to the current directory.

* `--sync`: *boolean, optional*

   * Creates a remote function associated with the current project. By default, no remote function is created.

* `<function_id>`: *string, optional*

   * The function ID of the remote function. If you need to associate the local function with a remote function, you can set the function ID of the remote function using this parameter.

* `--env`: *boolean, optional*

   * Synchronizes the environment variables of the remote function corresponding to `<function_id>` to the local environment. By default, the environment variables of the remote function are not synchronized.


A function project can have multiple local functions. If you need to create new local functions in the function project, you can use the [nest functions create](https://docs.byteplus.com/docs/byteplus-cdn/cli-ref-nest-function-en#create) command.
