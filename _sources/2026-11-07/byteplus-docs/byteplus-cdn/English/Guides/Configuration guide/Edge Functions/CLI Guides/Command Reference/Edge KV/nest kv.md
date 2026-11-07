---
title: "nest kv"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/cli-ref-nest-kv-en"
---

Manages Edge KV.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">This command requires you to set up your BytePlus account's Access Key ID and Secret Access Key. See <a href="https://docs.byteplus.com/docs/byteplus-cdn/edge-functions-cli-login-en">Setting up your Access Key ID and Secret Access Key</a>.</div>


* <div data-tips="true" data-tips-type="tip">Edge KV data is not saved locally. The Edge Functions CLI manages KV data on the Edge Functions server.</div>



<span id="nest-kv-namespace"></span>
# nest kv namespace

Manage namespaces.

<span id="subcommands"></span>
## Subcommands

<span id="list"></span>
### list

```shell
npx nest kv namespace list --page <page_number> --desc
```


Retrieve the list of namespaces.


* `<page_number>`: *integer, optional*

   * Page number for paginated display. Default is 1.

* `--desc`: *boolean, optional*:

   * Sort by namespace ID in descending order. Default is ascending order.


```shell
$ npx nest kv namespace list
+---------------------------------------------+--------------------------+----------------------------------+-------------------------------------------------------------------+---------------------+
|                   ID:NAME                   |          REGION          |             PROJECT              |                            DESCRIPTION                            |     CREATETIME      |
+---------------------------------------------+--------------------------+----------------------------------+-------------------------------------------------------------------+---------------------+
| 24629043532424120990:ns                     | Outside Chinese Mainland | default                          | more updates                                                      | 2024-12-30 15:21:07 |
| 25540045541653372777:abtest_config          | Outside Chinese Mainland | default                          | testq                                                             | 2025-01-17 17:13:10 |
| 7758139412787918608:gochina                 | Outside Chinese Mainland | default                          |                                                                   | 2025-06-13 18:45:07 |
+---------------------------------------------+--------------------------+----------------------------------+-------------------------------------------------------------------+---------------------+
```


<span id="create"></span>
### create

```shell
npx nest kv namespace create <name> -d <description> -p <project>
```


Create a namespace.


* `<name>`: *string, required*

   * Name of the namespace.

* `<description>`: *string, optional*

   * Description of the namespace.

* `<project>`: *string, optional*:

   * Project to which the namespace belongs. Default is `default`.


```shell
$ npx nest kv namespace create new12345
New namespace "new12345" created!
```


<span id="update"></span>
### update

```shell
npx nest kv namespace update <id:name> -d <description> 
```


Update the description of a specified namespace.


* `<id:name>`: *string, required*

   * ID and name of the namespace. Format is `<id:name>`. For example, `24629*********120990:namespace_name`. You can get the namespace ID and name using `npx nest kv namespace list`.

* `<description>`: *string, optional*

   * Description of the namespace.


```shell
$ npx nest kv namespace update 1677061481998840412:new12345  -d "more updates"
[1677061481998840412:new12345]
>>> the desc is more updates
Namespace 1677061481998840412:new12345 updated!
```


<span id="delete"></span>
### delete

```shell
npx nest kv namespace delete <id:name>
```


Delete a specified namespace.


* `<id:name>`: *string, required*

   * ID and name of the namespace. Format is `<id:name>`. For example, `24629*********120990:namespace_name`. You can get the namespace ID and name using `npx nest kv namespace list`.


<span id="nest-kv-keys"></span>
# nest kv keys

Retrieve the list of key\-value pairs for a specified namespace.

```shell
nest kv keys --namespace <id:name>
```



* `<id:name>`: *string, required*

   * ID and name of the namespace. Format is `<id:name>`. For example, `24629*********120990:namespace_name`. You can get the namespace ID and name using `npx nest kv namespace list`.


<span id="nest-kv-set"></span>
# nest kv set

```shell
nest kv set --namespace <id:name> <key> <value> --ttl <ttl>

nest kv set --namespace <id:name> <key> --file <file_path> --ttl <ttl>
```


Add or update a key\-value pair.


* `<id:name>`: *string, required*

   * ID and name of the namespace. Format is `<id:name>`. For example, `24629*********120990:namespace_name`. You can get the namespace ID and name using `npx nest kv namespace list`.

* `<key>`: *string, required*

   * Key of the key\-value pair.

* `<value>`: *string, optional*

   * Value of the key\-value pair. You need to set either `<value>` or `<file_path>`.

* `<ttl>`: *string, optional*

   * Expiration time of the key\-value pair in seconds. Default is never expire.

* `<file_path>`: *string, optional*

   * File path. The content of this file will be used as the value of the key\-value pair. You need to set either `<value>` or `<file_path>`.


<span id="nest-kv-delete"></span>
# nest kv delete

```shell
nest kv delete --namespace <id:name> <key>
```


Delete a specified key\-value pair.


* `<id:name>`: *string, required*

   * ID and name of the namespace. Format is `<id:name>`. For example, `24629*********120990:namespace_name`. You can get the namespace ID and name using `npx nest kv namespace list`.

* `<key>`: *string, required*

   * Key of the key\-value pair.


<span id="nest-kv-get"></span>
# nest kv get

```shell
nest kv get --namespace <id:name> <key> --save-dev --no-decode
```


Retrieve the value of a key\-value pair.


* `<id:name>`: *string, required*

   * ID and name of the namespace. Format is `<id:name>`. For example, `24629*********120990:namespace_name`. You can get the namespace ID and name using `npx nest kv namespace list`.

* `<key>`: *string, required*

   * Key of the key\-value pair.

* `--save-dev`: *boolean, optional*

   * Save the key\-value pair locally for debugging. Default is not to save.

* `--no-decode`: *boolean, optional*

   * Print the value of the key\-value pair directly in base64 encoded format. By default, it prints the base64 decoded value. If your key\-value pair's value is binary, you can use `--no-decode` to print the base64 encoded value to avoid displaying garbled characters.
