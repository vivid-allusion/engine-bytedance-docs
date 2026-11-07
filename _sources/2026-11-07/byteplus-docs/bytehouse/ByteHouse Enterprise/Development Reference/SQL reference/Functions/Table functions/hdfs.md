---
title: "hdfs"
product: "ByteHouse"
product_code: "bytehouse"
source: "https://docs.byteplus.com/en/docs/bytehouse/hdfs-function"
---

Create a table based on files in HDFS. This table function is similar to URL and file.
```SQL
hdfs(URI, format, structure)
```

**Input parameters**

* `URI` — the relative URI of files in HDFS. In read-only mode, the path supports the following wildcard characters: `*`, `?`, `{abc,def}` and `{N..M}`, of which `N`, `M` are numbers, 'abc', 'def'` are strings.
* `format` — the format of the file.
* `structure` — the structure of the table. Format `'column1_name column1_type, column2_name column2_type, ...'`.

**Return value**
Table with a specified structure for reading or writing data in a specified file.
**Example**
Table comes from `hdfs://hdfs1:9000/test` and selects the first two rows:
```SQL
SELECT * FROM hdfs('hdfs://hdfs1:9000/test', 'TSV', 'column1 UInt32, column2 UInt32, column3 UInt32')LIMIT 2
```

```Plain
┌─column1─┬─column2─┬─column3─┐
│       1 │       2 │       3 │
│       3 │       2 │       1 │
└─────────┴─────────┴─────────┘
```

**Wildcard character in path**
Multiple path components can have wildcard characters. The files to be processed must exist and match the entire path pattern (not just the suffix or prefix).

* `*` — Replaces any number of any characters, except `/` including the empty string.
* `?` — Replaces any single character.
* `{some_string,another_string,yet_another_one}` — Replace any string `'some_string', 'another_string', 'yet_another_one'`.
* `{N..M}` — Replace any number ranging from N to M (inclusive).

**Example**

1. Suppose we have several files on HDFS with the following URIs:
* ‘hdfs://hdfs1:9000/some_dir/some_file_1’
* ‘hdfs://hdfs1:9000/some_dir/some_file_2’
* ‘hdfs://hdfs1:9000/some_dir/some_file_3’
* ‘hdfs://hdfs1:9000/another_dir/some_file_1’
* ‘hdfs://hdfs1:9000/another_dir/some_file_2’
* ‘hdfs://hdfs1:9000/another_dir/some_file_3’
2. Search the number of lines in these files:

```SQL
SELECT count(*) FROM hdfs('hdfs://hdfs1:9000/{some,another}_dir/some_file_{1..3}', 'TSV', 'name String, value UInt32')
```


3. Search the number of lines in all files in these two directories:

```SQL
SELECT count(*) FROM hdfs('hdfs://hdfs1:9000/{some,another}_dir/*', 'TSV', 'name String, value UInt32')
```

:::danger
If your file list includes numerical ranges with leading zeros, use a structure with braces for each number or use `?`.
:::
**Example**
Search data from files named `file000`, `file001`, … , `file999`:
```SQL
SELECT count(*) FROM hdfs('hdfs://hdfs1:9000/big_dir/file{0..9}{0..9}{0..9}', 'CSV', 'name String, value UInt32')
```

<span id="0583ecf7"></span>
## Virtual columns

* `_path` — Path of the file.
* `_file` — Name of the file.
