---
title: "nest config"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/cli-ref-nest-config-en"
---

Manages project configuration files.

<span id="synopsis"></span>
## Synopsis

```shell
npx nest config

npx nest config set <parameter> <value>

npx nest config set -g <parameter> <value>
```


<span id="description"></span>
## Description

Project configuration includes information about the function project's working directory, entry code file directory, information about all local functions in the function project, and Edge KV data. Project configurations can be categorized into function project configurations and global project configurations. The Edge Functions CLI prioritizes retrieving configurations from the function project configuration. If not found, it retrieves from the global project configuration.


* `npx nest config set` is used to set parameters in the function project configuration file.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">You can use the global parameter <code>-c <config_file_path></code> to specify a function configuration file for the current command.   </div>
   

* `npx nest config set -g` is used to set parameters in the global project configuration file.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">It is recommended to set only parameters starting with <code>cloud</code> in the global project configuration file, such as <code>cloud.access_key</code> and <code>cloud.secret_key</code>. These parameters are related configurations for the Edge Functions OpenAPI service and apply to all functions under the same BytePlus account.   </div>
   

You can view the effective Edge Functions CLI configuration in the current function project by using `npx nest config`.

<span id="subcommands"></span>
## Subcommands

<span id="set"></span>
### set

Modify parameters of the Edge Functions CLI configuration, for example, `npx nest config set name example-function`.

You can use `-g` to modify the global project configuration file of the Edge Functions CLI.

<span id="parameter-descriptions"></span>
#### Parameter Descriptions


|Parameter |Description |
|---|---|
|work_dir |Working directory of the function project. |
|src_dir |Directory of the function entry code file. |
|output_dir |Directory of the function execution code file. When you run a local function using nest debug or nest start, the Edge Functions CLI generates a function execution code file in the directory specified by `output_dir` based on the function entry code file. Compared to the function entry code file, the function execution code file will have an Immediately Invoked Function Expression (IIFE) added. |
|cloud.api_server |Edge Functions OpenAPI service URL. This parameter is fixed and does not need to be modified. |
|cloud.debug_server |Edge Functions Debugger service URL. This parameter is fixed and does not need to be modified. |
|cloud.api_version |Edge Functions OpenAPI service version. This parameter is fixed and does not need to be modified. |
|cloud.api_region |Edge Functions OpenAPI service region. This parameter is fixed and does not need to be modified. |
|cloud.api_timeout |Edge Functions OpenAPI timeout. Default is 5000 ms. |
|cloud.key_manager_url |URL of the API access key page in the BytePlus console. This parameter is fixed and does not need to be modified. |
|cloud.product |Edge Functions OpenAPI product type. This parameter is fixed and does not need to be modified. |
|cloud.access_key |Your BytePlus account's Access Key ID. You can obtain the Access Key ID from the [BytePlus Console](https://console.byteplus.com/iam/keymanage). |
|cloud.secret_key |Your BytePlus account's Secret Access Key. You can obtain the Secret Access Key from the [BytePlus Console](https://console.byteplus.com/iam/keymanage). |
|functions.[N].id |ID of the Nth local function in the project list. |
|functions.[N].name |Name of the Nth local function in the project list. |
|functions.[N].type |Entry code file type of the Nth local function in the project list. |
|functions.[N].entry |Entry code file name of the Nth local function in the project list. |
