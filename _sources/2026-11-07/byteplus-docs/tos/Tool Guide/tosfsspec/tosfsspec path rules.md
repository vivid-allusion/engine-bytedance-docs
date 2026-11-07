---
title: "tosfsspec path rules"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/tosfsspec_path_rules"
---

This topic describes the URL and path conventions used by tosfsspec in TOS. tosfsspec uses a standard URI format to locate TOS resources. It is essential to understand these path rules in order to use the library correctly.

<span id="5f9313ab"></span>
## Scheme

All paths pointing to TOS resources must use the `tos://` scheme as a prefix.

<span id="f0be897c"></span>
## Path structure

The standard path structure for tosfsspec is as follows:

```Plain Text
tos://<bucket_name>/<object_key>
```



* **`bucket_name`**: The name of your TOS bucket.

* **`object_key`**: The full path to the object within the bucket. It can be a multi\-level directory, such as `data/raw/2023/log.txt`.


Example:


* Pointing to an object: `tos://my-bucket/documents/report.pdf`.

* Pointing to a directory: `tos://my-bucket/images/`. The trailing `/` is optional. However, we recommend using it to explicitly indicate that the path is a directory.

* Pointing to the root directory of a bucket: `tos://my-bucket` or `tos://my-bucket/`.


<span id="6a06f99d"></span>
## Special paths

<span id="677bcbd5"></span>
### Root paths (`/` or `''`)

tosfsspec exhibits special behavior when the provided path is the root path (`'/'`) or an empty string (`''`). The primary use case is listing all buckets under the current account.

```Python
# The following two methods can be used to list all buckets.
all_buckets_1 = fs.ls('/')

all_buckets_2 = fs.ls('')

print([b['name'] for b in all_buckets_1])
```


<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">Except for a few operations, such as <code>fs.ls</code><code>()</code>, most file operations (e.g., <code>open()</code>, <code>touch()</code>, and <code>rm()</code>) do not directly support the root path. You must explicitly specify a bucket.</div>


<span id="7391c8e4"></span>
### Specifying only the bucket

In most cases, providing only the bucket name (with or without the scheme) is equivalent to referencing the root directory of that bucket.

```Python
# The following two formats are equivalent when used with ls(). Both formats will list the top-level files and directories within my-bucket.
fs.ls('tos://my-bucket')
fs.ls('tos://my-bucket/')
```


<span id="330d49b0"></span>
## Path parsing

Internally, tosfsspec parses the input URL into two components: `bucket` and `key`.


* `tos://my-data/input.csv` \-\> `bucket='my-data'`, `key='input.csv'`

* `tos://archive-logs/2023/q1/` \-\> `bucket='archive-logs'`, `key='2023/q1/'`

* `tos://assets` \-\> `bucket='assets'`, `key=''`


Understanding this parsing rule can help you troubleshoot issues caused by incorrect path formats.
