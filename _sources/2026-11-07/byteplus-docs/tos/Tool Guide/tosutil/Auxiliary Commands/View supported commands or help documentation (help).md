---
title: "View supported commands or help documentation (help)"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/View-support-commands-or-help-documentation"
---

You can use the `help` command to view commands supported by the tosutil tool or to check the help documentation for a specific command.

<span id="命令语法"></span>
## Command syntax


<Tabs>
<Tab zoneid="70VwqxEt" title="Linux/macOS">
<TabTitle>Linux/macOS</TabTitle>

&nbsp;

```Bash
./tosutil help [command] [-conf=xxx]
```





</Tab>
<Tab zoneid="2S782CY8" title="Windows">
<TabTitle>Windows</TabTitle>

&nbsp;

```Bash
tosutil help [command] [-conf=xxx]
```





</Tab>
</Tabs>


<span id="参数说明"></span>
## Parameters


|**Parameter name** |**Parameter type** |**Description** |
|---|---|---|
|command |String |Command name, such as `ls`, `mb`, `cp`, `rm`, etc. |


<span id="使用示例"></span>
## Examples


* Command


```Plain
./tosutil help
```



* Back


```Plain
Usage: tosutil [command] [args...] [options...]
You can use "tosutil help command" to see detailed help for each command

Basic commands:
  cp            file_url cloud_url [options...]
                cloud_url file_url [options...]
                cloud_url1 cloud_url2 [options...]
                -recover=xxx [options...]
upload objects, download objects, or copy objects

  ls            [cloud_url] [options...]
list buckets, list objects within a bucket, or list multipart upload tasks within a bucket

  mb            cloud_url [options...]
create a new bucket with the specified bucket name and parameters

  rm            cloud_url [options...]
delete buckets, delete objects, or delete multipart upload tasks

  setmeta       cloud_url [options...]
set object metadata

  stat          cloud_url [options...]
Query bucket properties or query object properties


Auxiliary commands:
  clear         [checkpoint_dir] [options...]
Delete checkpoint files under the specified folder and attempt cloud cleanup

  config        [options...]
Update key configurations in the configuration file

  help          [command] [options...]
View command help

  version
View version number
```
