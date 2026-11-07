---
title: "nest kv"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/cli-ref-nest-kv-cn"
---

管理边缘 KV。

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">本命令需要您设置您的 BytePlus 账号的 Access Key ID 和 Secret Access Key。参见 <a href="https://docs.byteplus.com/docs/byteplus-cdn/edge-functions-cli-login-cn">设置您的 Access Key ID 和 Secret Access Key</a>。</div>


* <div data-tips="true" data-tips-type="tip">边缘 KV 的数据不保存在本地。边缘函数 CLI 在边缘函数服务端管理 KV 数据。</div>



<span id="nest-kv-namespace"></span>
# nest kv namespace

管理存储空间。

<span id="子命令"></span>
## 子命令

<span id="list"></span>
### list

```shell
npx nest kv namespace list --page <page_number> --desc
```


获取存储空间列表。


* `<page_number>`：*integer，optional*

   * 列表分页显示的页码。默认为 1。

* `--desc`：*boolean，optional*：

   * 按存储空间 ID 降序排序。默认为按存储空间 ID 升序排序。


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
npx nest kv namespace create <name> -d <description> -p <project> --cn
```


创建一个存储空间。


* `<name>`：*string，required*

   * 存储空间的名称。

* `<description>`：*string，optional*

   * 存储空间的描述。

* `<project>`：*string，optional*：

   * 存储空间所属的项目。默认为 `default`。

* `--cn`：*boolean，optional*

   * KV 数据的存储地域是否仅限于中国内地。默认不限制 KV 数据的存储地域。


```shell
$ npx nest kv namespace create new12345
New namespace "new12345" created!
```


<span id="update"></span>
### update

```shell
npx nest kv namespace update <id:name> -d <description> 
```


更新指定的存储空间的描述。


* `<id:name>`：*string，required*

   * 存储空间的 ID 和名称。格式为 `<id:name>`。例如 `24629*********120990:namespace_name`。您可以通过 `npx nest kv namespace list` 获取存储空间的 ID 和名称。

* `<description>`：*string，optional*

   * 存储空间的描述。


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


删除指定的存储空间。


* `<id:name>`：*string，required*

   * 存储空间的 ID 和名称。格式为 `<id:name>`。例如 `24629*********120990:namespace_name`。您可以通过 `npx nest kv namespace list` 获取存储空间的 ID 和名称。


<span id="nest-kv-keys"></span>
# nest kv keys

获取指定存储空间的键值对列表。

```shell
nest kv keys --namespace <id:name>
```



* `<id:name>`：*string，required*

   * 存储空间的 ID 和名称。格式为 `<id:name>`。例如 `24629*********120990:namespace_name`。您可以通过 `npx nest kv namespace list` 获取存储空间的 ID 和名称。


<span id="nest-kv-set"></span>
# nest kv set

```shell
nest kv set --namespace <id:name> <key> <value> --ttl <ttl>

nest kv set --namespace <id:name> <key> --file <file_path> --ttl <ttl>
```


添加或更新键值对。


* `<id:name>`：*string，required*

   * 存储空间的 ID 和名称。格式为 `<id:name>`。例如 `24629*********120990:namespace_name`。您可以通过 `npx nest kv namespace list` 获取存储空间的 ID 和名称。

* `<key>`：*string，required*

   * 键值对的键。

* `<value>`：*string，optional*

   * 键值对的值。您至少需要设置 `<value>` 和 `<file_path>` 其中的一个。

* `<ttl>`：*string，optional*

   * 键值对的过期时间。单位为秒。默认为永不过期。

* `<file_path>`：*string，optional*

   * 文件路径。该文件的内容将作为键值对的值。您至少需要设置 `<value>` 和 `<file_path>` 其中的一个。


<span id="nest-kv-delete"></span>
# nest kv delete

```shell
nest kv delete --namespace <id:name> <key>
```


删除指定的键值对。


* `<id:name>`：*string，required*

   * 存储空间的 ID 和名称。格式为 `<id:name>`。例如 `24629*********120990:namespace_name`。您可以通过 `npx nest kv namespace list` 获取存储空间的 ID 和名称。

* `<key>`：*string，required*

   * 键值对的键。


<span id="nest-kv-get"></span>
# nest kv get

```shell
nest kv get --namespace <id:name> <key> --save-dev --no-decode
```


获取键值对的值。


* `<id:name>`：*string，required*

   * 存储空间的 ID 和名称。格式为 `<id:name>`。例如 `24629*********120990:namespace_name`。您可以通过 `npx nest kv namespace list` 获取存储空间的 ID 和名称。

* `<key>`：*string，required*

   * 键值对的键。

* `--save-dev`：*boolean，optional*

   * 把键值对保存到本地用于调试。默认不保存。

* `--no-decode`：*boolean，optional*

   * 直接以 base64 编码格式打印键值对的值。默认打印 base64 解码后的值。如果您的键值对的值是二进制类型，为了避免打印的内容显示为乱码，您可以使用 `--no-decode` 打印值的 base64 编码。
