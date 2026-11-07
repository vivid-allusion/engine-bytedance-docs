---
title: "S3 external table"
product: "ByteHouse"
product_code: "bytehouse"
source: "https://docs.byteplus.com/en/docs/bytehouse/s3-external-table"
---

ByteHouse's S3 engine integrates with ecosystems of S3\-compatible object storage, including systems like BytePlus ToS, Amazon S3, and others.

<span id="34a49924"></span>
# Create table

```SQL
CREATE TABLE s3_engine_table (name String, value UInt32)
ENGINE = S3(path, [access_key_id, secret_access_key,] format, [compression])
```


<span id="d752add6"></span>
## Engine parameters


* `path` \- URL and Path of the bucket, common format: `https://{Bucket Name}.{s3 endpoint Name}/{Path}`. Supports the following wildcard characters: `*, ?, {abc,def}` and `{N..M}`.


<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">BytePlus TOS provides an Endpoint that differs from the S3 Endpoint. As shown below, the link copied from the BytePlus TOS Console cannot be used directly and must have its domain changed to the S3 Endpoint domain name, see <a href="https://docs.byteplus.com/en/docs/tos/docs-region-and-endpoint">BytePlus TOS supported regions and URL Full Domains</a> for details.</div>


<div data-tips="true" data-tips-type="warning">For example, the Endpoint URL link <code>https://tos-{REGION}.bytepluses.com/xxx</code> retrieved from BytePlus Console needs to be changed to <code>https://tos-s3-{REGION}.bytepluses.com/xxx</code> format.</div>


<div data-tips="true" data-tips-type="warning"><img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/7fc8ee65a2fe4f779281291c614345f4~tplv-goo7wpa0wc-image.image" width="1844px" /></div>



* `format` \- File format, refer to [Input⧸Output formats](https://docs.byteplus.com/docs/bytehouse/input-output-formats).

* `access_key_id`, `secret_access_key` \- Long\-term credentials for object storage account users, see [View AKSK information](https://docs.byteplus.com/en/docs/byteplus-platform/docs-creating-an-accesskey).

* `compression` — Optional compression type. Supported values: none, gzip/gz, brotli/br, xz/LZMA, zstd/zst. By default, it automatically detects the compression type through the file extension.


<span id="5a8afa58"></span>
## Example

Set up s3_engine_table table:

```SQL
CREATE TABLE s3_engine_table (name String, value UInt32) ENGINE=S3('https://storage.yandexcloud.net/my-test-bucket-768/test-data.csv.gz', 'CSV', 'gzip');
```


Insert data:

```SQL
INSERT INTO s3_engine_table VALUES ('one', 1), ('two', 2), ('three', 3); 
```


Query data:

```SQL
SELECT * FROM s3_engine_table LIMIT 2;
 
┌─name─┬─value─┐
│ one  │ 1     │
│ two  │ 2     │
└──────┴───────┘
```


<span id="4ccf793f"></span>
# Virtual column

`_path` — The path of the file.

`_file` — The name of the file.

<span id="c15019c6"></span>
# Wildcard character in the path

`The 'path'` parameter can use class bash\-like wildcard characters to specify multiple files. The files to be processed must exist and match the complete path pattern. The list of files is determined at the time of SELECT, not at the time of CREATE.


* `*` — represents any number of any characters, including an empty string, but excluding `/`.

* `?` — replaces any single character.

* `{some_string,another_string,yet_another_one}` — substitutes any one of the strings 'some_string', 'another_string', 'yet_another_one'.

* `{N..M}` — substitutes any number within the range from N to M, including both endpoints. N and M can have leading zeros, such as 000..078.


Constructs with {} are similar to remote table functions.

<span id="71a414c6"></span>
# Example of use

Assuming we have several CSV files on S3, their URIs are as follows:


* ‘https://storage.yandexcloud.net/my\-test\-bucket\-768/some_prefix/some_file_1.csv’

* ‘https://storage.yandexcloud.net/my\-test\-bucket\-768/some_prefix/some_file_2.csv’

* ‘https://storage.yandexcloud.net/my\-test\-bucket\-768/some_prefix/some_file_3.csv’

* ‘https://storage.yandexcloud.net/my\-test\-bucket\-768/another_prefix/some_file_1.csv’

* ‘https://storage.yandexcloud.net/my\-test\-bucket\-768/another_prefix/some_file_2.csv’

* ‘https://storage.yandexcloud.net/my\-test\-bucket\-768/another_prefix/some_file_3.csv’


There are several ways to create a table containing all six files:

First method:

```SQL
CREATE TABLE table_with_range (name String, value UInt32) ENGINE = S3('https://storage.yandexcloud.net/my-test-bucket-768/{some,another}_prefix/some_file_{1..3}', 'CSV');
```


Another method:

```SQL
CREATE TABLE table_with_question_mark (name String, value UInt32) ENGINE = S3('https://storage.yandexcloud.net/my-test-bucket-768/{some,another}_prefix/some_file_?', 'CSV'); 
```


The table contains all files in two directories (all files must satisfy the format and mode described in the query):

```SQL
CREATE TABLE table_with_asterisk (name String, value UInt32) ENGINE = S3('https://storage.yandexcloud.net/my-test-bucket-768/{some,another}_prefix/*', 'CSV'); 
```


Create a file table named file\-000.csv, file\-001.csv, … , file\-999.csv:

```SQL
CREATE TABLE big_table (name String, value UInt32) ENGINE = S3('https://storage.yandexcloud.net/my-test-bucket-768/big_prefix/file-{000..999}.csv', 'CSV'); 
```
