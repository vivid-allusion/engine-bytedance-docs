---
title: "file"
product: "ByteHouse"
product_code: "bytehouse"
source: "https://docs.byteplus.com/en/docs/bytehouse/file-function"
---

Create a table from the file. This function behaves similarly to url and hdfs.
`File` function can be used to perform SELECT and INSERT queries on data in the File table.`SELECT and INSERT querieINSERT queries on data in the File` table.
**Grammar**
```sql
file(path, format, structure)
```

**Parameter**
`Path` — the relative path of files in user_files_path. In read-only mode, the file path supports the following wildcards: `*`, `?`, `{abc,def}`, and `{N..M}`, where `N` and `M` are numbers, and 'abc', 'def'` are strings.
`Format` — the format of the file.
`Structure` — table structure. Format `'column1_name column1_type, column2_name column2_type, ...'`.
**Return Value**
A table with a specified structure for reading or writing data in a specified file.
**Example**
Set `user_files_path` and the contents of file `test.csv`:
```bash
$ grep user_files_path /etc/clickhouse-server/config.xml
    /var/lib/clickhouse/user_files/

$ cat /var/lib/clickhouse/user_files/test.csv
    1,2,3
    3,2,1
    78,43,45
```

Retrieve data from the table in `test.csv` and select the first two rows from the table:
```sql
SELECT * FROM file('test.csv', 'CSV', 'column1 UInt32, column2 UInt32, column3 UInt32') LIMIT 2;
```

```text
┌─column1─┬─column2─┬─column3─┐
│       1 │       2 │       3 │
│       3 │       2 │       1 │
└─────────┴─────────┴─────────┘
```

Get the first 10 rows of a table from a CSV file containing 3 columns of UInt32 type:
```sql
SELECT * FROM file('test.csv', 'CSV', 'column1 UInt32, column2 UInt32, column3 UInt32') LIMIT 10;
```

Insert data from the file into the table:
```sql
INSERT INTO FUNCTION file('test.csv', 'CSV', 'column1 UInt32, column2 UInt32, column3 UInt32') VALUES (1, 2, 3), (3, 2, 1);
SELECT * FROM file('test.csv', 'CSV', 'column1 UInt32, column2 UInt32, column3 UInt32');
```

```text
┌─column1─┬─column2─┬─column3─┐
│       1 │       2 │       3 │
│       3 │       2 │       1 │
└─────────┴─────────┴─────────┘
```

**Wildcard in the Path**
Multiple path components can have wildcards. Files to be processed must exist and match the entire path pattern (not just the suffix or prefix).

* `*` — replaces any number of any characters, except `/`, including the empty string.
* `?` — replaces any single character.
* `{some_string,another_string,yet_another_one}` — replaces any of the strings `'some_string', 'another_string', 'yet_another_one'`.
* `{N..M}` — replaces any number within the range from N to M (inclusive of both boundaries).

Using `{}` constructs is similar to the remote table function.
**Example**
Suppose we have several files with the following relative paths:

* ‘some_dir/some_file_1’
* ‘some_dir/some_file_2’
* ‘some_dir/some_file_3’
* ‘another_dir/some_file_1’
* ‘another_dir/some_file_2’
* ‘another_dir/some_file_3’

Count the lines in these files:
```sql
SELECT count(*)
FROM file('{some,another}_dir/some_file_{1..3}', 'TSV', 'name String, value UInt32')
```

Count the lines in all files in these two directories:
```sql
SELECT count(*)
FROM file('{some,another}_dir/*', 'TSV', 'name String, value UInt32')
```

!!! warning "Warning"
If your file list includes numeric ranges with leading zeros, use the structure with braces for each number or use `?`.
**Example**
Query data from files named `file000`, `file001`, ..., `file999`:
```sql
SELECT count(*)
FROM file('big_dir/file{0..9}{0..9}{0..9}', 'CSV', 'name String, value UInt32')
```

<span id="虚拟列 {#virtual-columns}"></span>
## Virtual column
`_path` — File path.
`_file` — File name.
