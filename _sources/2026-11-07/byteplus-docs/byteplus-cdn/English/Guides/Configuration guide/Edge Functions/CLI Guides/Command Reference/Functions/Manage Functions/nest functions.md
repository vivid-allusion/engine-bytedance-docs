---
title: "nest functions"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/cli-ref-nest-function-en"
---

Performs create, read, update, and delete operations on local or remote functions.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">This command requires you to set up your BytePlus account's access key ID and secret access key. See <a href="https://docs.byteplus.com/docs/byteplus-cdn/edge-functions-cli-login-en">Set Your Access Key ID and Secret Access Key</a>.</div>


* <div data-tips="true" data-tips-type="tip">This command needs to be run in the root directory of a function project. You need to use <code>nest init</code> to create a function project.</div>



<span id="subcommands"></span>
## Subcommands

<span id="get"></span>
### get

```shell
npx nest functions get <function_id_or_name> 

npx nest functions get --remote <function_id> 
```


Retrieve information about a local or remote function.


* `<function_id_or_name>`: *string, required*

   * ID or name of the local function.

* `--remote`: *boolean, optional*

   * Retrieve information about a remote function. By default, retrieves information about a local function:

      * You can use `<function_id>` or `<function_name>` to get information about a local function.

      * You can only use `<function_id>` to get information about a remote function.


<span id="list"></span>
### list

```shell
npx nest function list --page <page_number> --desc -s <status> --remote
```


Get a list of functions.


* `<page_number>`: *integer, optional*

   * Page number for paginated display. Default is 1.

* `--desc`: *boolean, optional*:

   * Sort by function ID in descending order. Default is ascending order.

* `<status>`: *string, optional*

   * Function status.

      * running: Running.

      * unassociated: Not associated with a domain.

      * configuring: Configuring.

* `--remote`: *boolean, optional*:

   * List only includes remote functions. By default, only includes local functions.


```shell
npx nest functions list
+----+------+------+--------------+--------------------------+---------+-------------+---------+
| ID | NAME | TYPE |    ENTRY     |          REGION          | PROJECT | DESCRIPTION | DEFAULT |
+----+------+------+--------------+--------------------------+---------+-------------+---------+
|    | test | js   | src/index.js | Outside Chinese Mainland |         |             | true    |
+----+------+------+--------------+--------------------------+---------+-------------+---------+
```


<span id="create"></span>
### create

```shell
npx nest functions create --name <function_name> --description <function_description> --entry <path_to_entry_file> --project <project> --sync
```


Create a function in the function project. When you run this command, the Edge Functions CLI prompts you to enter the function name, select a function template, specify the location and name of the entry file, choose the associated BytePlus project, provide a function description, and other information. Then, the Edge Functions CLI will create a local function based on the information you input.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">Function names must be unique under each BytePlus account. The naming rules are as follows:</div>


   * <div data-tips="true" data-tips-type="tip">Supports English letters, numbers, and hyphens (\-).</div>


   * <div data-tips="true" data-tips-type="tip">The length must not exceed 128 characters.</div>


* <div data-tips="true" data-tips-type="tip">The function templates available to you depend on whether you have set up your Access Key ID and Secret Access Key:</div>


   * <div data-tips="true" data-tips-type="tip">If you haven't set up your Access Key ID and Secret Access Key, you can only use the HelloWorld template.</div>


   * <div data-tips="true" data-tips-type="tip">If you have set up your Access Key ID and Secret Access Key, you can use all templates supported by edge functions.</div>


* `<function_name>`: *string, required*

   * Function name.

* `<function_description>`: *string, optional*

   * Function description.

* `<path_to_entry_file>`: *string, required*

   * Path to the entry file. The entry file is the starting point for executing the local function. The entry file specified by this parameter must exist.

* `<project>`: *string, optional*

   * Project to which the function belongs. Default is `default`.

* `--sync`: *boolean, optional*

   * Simultaneously create a corresponding remote function. By default, does not create a corresponding remote function.


```shell
$ npx nest functions create --name test0111 --entry src/index.js
==> [info]: Creating a new function test0111 locally.✔
```


<span id="update"></span>
### update

```shell
npx nest functions update <function_id_or_name> --new-name <new_function_name> --new-description <new_function_description> --new-id <new_function_id> --new-entry <path_to_entry_file> --sync
```


Modify function name and description by function ID or name.


* `<function_id_or_name>`: *string, required*

   * ID or name of the local function.

* `<new_function_name>`: *string, optional*

   * New function name.

* `<new_function_description>`: *string, optional*

   * New function description.

* `<path_to_entry_file>`: *string, optional*

   * Path to the entry file. The entry file is the starting point for executing the local function. Default is the entry file path in the project configuration file.

* `--sync`: *boolean, optional*

   * Simultaneously update the corresponding remote function. By default, does not update the corresponding remote function.

* `--default`: *boolean, optional*

   * Set this function as the default function. By default, does not set this function as the default function. In a function project, there can only be one default function.

* `<new_function_id>`: *boolean, optional*

   * New function ID.


<span id="pull"></span>
### pull

```shell
npx nest functions pull <function_id> --env
```


Synchronize the code of a remote function to a local function.


* `<function_id>`: *string, required*

   * Function ID.

* `--env`: *boolean, optional*

   * Synchronize the environment variables of the remote function to the local function. By default, does not synchronize the environment variables.


<span id="delete"></span>
### delete

```shell
npx nest functions delete <function_id> --sync
```


Delete a local function by function ID. This command will delete the configuration information about the specified function ID under the `functions` field in the project configuration file, but will not delete the local function's code.


* `<function_id>`: *string, required*

   * Function ID.

* `--sync`: *boolean, optional*

   * Simultaneously delete the corresponding remote function. By default, does not delete the corresponding remote function.
