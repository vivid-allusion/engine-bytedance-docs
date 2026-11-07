---
title: "EMR Daft integration with Lance: operation guide and best practices"
product: "BytePlus EMR"
product_code: "E-MapReduce"
source: "https://docs.byteplus.com/en/docs/E-MapReduce/emr_daft_integration_with_lance"
---

<span id="13dc60e9"></span>
## Introduction

Lance is a next\-generation columnar storage format designed for multimodal data, such as images, videos, audio, and general columnar data. It supports local POSIX file systems and cloud object storage (such as S3 and GCS), and is renowned for its extremely fast random access, zero\-copy reads, deep integration with Daft/DuckDB, and outstanding performance in vector retrieval workloads.

**Daft** provides robust support for Lance, with core capabilities including:


* **Parallel and distributed reading**: Daft can read Lance datasets in parallel using the default multithreaded or distributed Ray Runner.

* **Data skipping**: By leveraging `df.where()` predicates and file/fragment statistics, Daft efficiently skips non\-matching data to accelerate queries.

* **Version and time slice reading**: Using the `version` and `asof` parameters, you can precisely read specific versions of Lance datasets or the latest version before a given point in time.

* **Scan and cache optimization**: Supports adjusting scan efficiency via `fragment_group_size`, and fine\-tuning cache behavior with parameters such as `index_cache_size` and `metadata_cache_size_bytes` to optimize performance for large\-scale datasets.


This guide provides a detailed explanation of how to use Daft to read and write Lance datasets, with a focus on configuring integration with Volcano Engine TOS (S3 compatible), and provides best practice code examples that can be directly copied and run in environments where only `pylance` and `daft` are installed.

<span id="d51d6135"></span>
## Installation and environment preparation


* Enable Serverless EMR: Serverless EMR currently supports the Daft/Ray computing engine. You can use serverless Ray to submit jobs. For job submission methods, refer to [Serverless Ray user guide](https://www.volcengine.com/docs/6491/1353774?lang=zh). Distributed Daft runs on the Ray engine.

* [Enable TOS service](https://www.volcengine.com/docs/6349/74830?lang=zh) for data storage.


<span id="b153e6e9"></span>
### EMR cloud environment


* The Serverless Ray image of EMR comes with daft and pylance pre\-installed, so users do not need to install them separately.

* To install the standalone version on your own machine and verify that the code works correctly, follow these steps.

* If your image does not include daft, refer to [Build and use custom images](https://www.volcengine.com/docs/6491/1348513?lang=zh) to install the required packages by building a custom image.


<span id="c1a5c23b"></span>
### Build a local development environment

You can prepare your local Python environment for single\-machine code debugging by following these steps.

```Bash
# Install core dependencies: Daft and Lance Python SDK (pylance)
pip install -U pylance daft
```


<span id="4235a1a5"></span>
## TOS environment configuration

<span id="9401b30a"></span>
### S3/TOS configuration and access

Daft provides flexible S3 configuration options, supporting both the standard credential chain and manual `IOConfig` configuration.

<span id="f5dcdcb7"></span>
### Credential discovery mechanism


1. **Environment/CLI credential chain (recommended)** : Daft automatically searches for standard AWS environment variables (such as `AWS_ACCESS_KEY_ID`) or AWS CLI configuration files (`~/.aws/credentials`).

2. **Manual** **`IOConfig`**: Construct an `IOConfig` object and pass it via the `io_config` parameter in `read_lance` or `write_lance` calls.


The following code snippet defines the configuration required to access Volcano Engine TOS. It is recommended to inject sensitive information via environment variables. For demonstration purposes, default values for testing are provided here. All subsequent examples will reuse this configuration.

```Python
import os
import daft
from daft.io import IOConfig, S3Config

# It is recommended to inject environment variables. The following are default values for testing (for PoC demonstration only):
AWS_ENDPOINT = os.getenv("AWS_ENDPOINT", "https://tos-s3-cn-shanghai.volces.com")  # No bucket prefix
AWS_KEY_ID = os.getenv("AWS_KEY_ID", "your_ak")
AWS_ACCESS_KEY = os.getenv("AWS_ACCESS_KEY", "your_sk")
AWS_REGION = os.getenv("AWS_REGION", "cn-beijing")
BUCKET = os.getenv("BUCKET", "your bucket name")

# io_config used for Daft read/write
io_config = IOConfig(
    s3=S3Config(
        endpoint_url=AWS_ENDPOINT,
        region_name=AWS_REGION,
        key_id=AWS_KEY_ID,
        access_key=AWS_ACCESS_KEY,
        force_virtual_addressing=True,  # Automatically rewritten to bucket.endpoint format
        verify_ssl=True,
    )
)

# Unified TOS path prefix
TOS = f"s3://{BUCKET}"
```


<span id="8414c559"></span>
### Detailed explanation of key `S3Config` parameters

`S3Config` offers a wide range of parameters to customize S3 access behavior:


* **`region_name`** (str): AWS region, for example `"us-west-2"`.

* **`endpoint_url`** (str): S3 endpoint URL. For AWS S3, this usually does not need to be set. For S3\-compatible storage (such as TOS), this is a required field.

* **`key_id`** (str): Access Key ID。

* **`access_key`** (str): Secret Access Key。

* **`force_virtual_addressing`** (bool): Whether to force the use of virtual\-host style addressing (`bucket.endpoint`). Some S3\-compatible services require this to be set to `True`. When it is `True`, Daft internally converts `endpoint_url` from `https://host` to `https://bucket.host` format.


<span id="413adc3b"></span>
## Read Lance dataset

The `daft.read_lance()` function allows you to easily read Lance datasets from the cloud.

<span id="a373089a"></span>
### Basic reading

This example first uses `daft.from_pydict` to create a Daft DataFrame, then writes it to TOS with `df.write_lance`, and finally reads it back using `daft.read_lance`.

```Python
import daft

# (Reuse the configuration from the previous section)

# 1. Create a Daft DataFrame
df = daft.from_pydict({"a": [1, 2, 3], "b": ["x", "y", "z"]})

# 2. Write data to TOS (overwrite)
path = f"{TOS}/demo/my_lance_dataset"
df.write_lance(path, io_config=io_config, mode="overwrite")

# 3. Read from TOS
print("### 从 TOS 读取数据集:")
df_tos = daft.read_lance(path, io_config=io_config)
df_tos.show()
```


<span id="1e2c45d0"></span>
#### Execution result

The following is a snippet of the actual output, for reference only.

```Plain
### 从 TOS 读取数据集:
╭───────┬────────╮
│ a     ┆ b      │
│ ---   ┆ ---    │
│ Int64 ┆ String │
╞═══════╪════════╡
│ 1     ┆ x      │
├╌╌╌╌╌╌╌┼╌╌╌╌╌╌╌╌┤
│ 2     ┆ y      │
├╌╌╌╌╌╌╌┼╌╌╌╌╌╌╌╌┤
│ 3     ┆ z      │
╰───────┴────────╯

(Showing first 3 of 3 rows)
```


<span id="26ebdf80"></span>
### Specify version and time slice

Lance supports data version control. You can use the `version` parameter to read a specific version, or use the `asof` parameter to query by point in time.

```Python
import daft
from datetime import datetime

# (Reuse the configuration from the previous section)

# 1. Create and write two versions of the dataset
base_path = f"{TOS}/demo/versioned_dataset"
df_v1 = daft.from_pydict({"a": [1, 2]})
df_v1.write_lance(base_path, mode="overwrite", io_config=io_config)

df_v2 = daft.from_pydict({"a": [3, 4]})
df_v2.write_lance(base_path, mode="append", io_config=io_config)

# 2. Read the latest version (version 2)
print("### 读取最新版本:")
df_latest = daft.read_lance(base_path, io_config=io_config)
df_latest.show()

# 3. Read by version number (version 1)
print("\n### 按版本号读取 (版本 1):")
df_v1_read = daft.read_lance(base_path, version=1, io_config=io_config)
df_v1_read.show()

# 4. Read by timestamp (asof) - example
# The asof parameter requires a datetime object or a string conforming to RFC3339/ISO8601
# Assume a timestamp before v2 is written
# df_asof = daft.read_lance(base_path, asof="2025-12-01T00:00:00Z", io_config=io_config)
# print("\n### Read by timestamp (asof):")
# df_asof.show() # Expected to display only data from version 1
```


<span id="f29c6d38"></span>
#### Execution result

The following is a snippet of the actual output, for reference only.

```Plain
### 读取最新版本:
╭───────╮
│ a     │
│ ---   │
│ Int64 │
╞═══════╡
│ 1     │
├╌╌╌╌╌╌╌┤
│ 2     │
├╌╌╌╌╌╌╌┤
│ 3     │
├╌╌╌╌╌╌╌┤
│ 4     │
╰───────╯

(Showing first 4 of 4 rows)

### 按版本号读取 (版本 1):
╭───────╮
│ a     │
│ ---   │
│ Int64 │
╞═══════╡
│ 1     │
├╌╌╌╌╌╌╌┤
│ 2     │
╰───────╯

(Showing first 2 of 2 rows)
```


<span id="1957b5fd"></span>
### Filter, projection, and limit pushdown

Daft automatically pushes `where()`, `select()`, and `limit()` operations down to the Lance scanner to enable efficient data filtering, column selection, and limiting the number of rows. You can use `explain(True)` to view the physical plan and confirm whether pushdown is effective.

```Python
import daft
from daft.expressions import col

# (Reuse the configuration from the previous section)

# 1. Prepare data
base_path = f"{TOS}/demo/pushdown_dataset"
df = daft.from_pydict({"id": list(range(100)), "value": [i * 0.1 for i in range(100)]})
df.write_lance(base_path, mode="overwrite", io_config=io_config)

# 2. Enable strict filter pushdown
daft.context.set_planning_config(enable_strict_filter_pushdown=True)

# 3. Read and apply filter, projection, and limit
df_read = daft.read_lance(base_path, io_config=io_config)
filtered_df = df_read.where(col("id") > 50).select("value").limit(5)

# 4. View execution plan
print("### 执行计划:")
filtered_df.explain(True)

# Expect to see Pushdowns information in the explain output, indicating that operations have been pushed down
# LanceScanOperator:
#   Pushdowns:
#     filter: (col(id) > 50)
#     limit: 5
#     projection: [value]
```


<span id="d429d19c"></span>
#### Execution result

The following is a snippet of the actual output, for reference only.

```Plain
### 执行计划:
== Unoptimized Logical Plan ==

* Limit: 5
|
* Project: col(value)
|
* Filter: col(id) > lit(50)
|
* PythonScanOperator: LanceDBScanOperator(s3://lance-poc/demo/pushdown_dataset)
|   File schema = id#Int64, value#Float64
|   Partitioning keys = []
|   Output schema = id#Int64, value#Float64


== Optimized Logical Plan ==

* Num Scan Tasks = 1
|   File schema = id#Int64, value#Float64
|   Partitioning keys = []
|   Projection pushdown = [value]
|   Filter pushdown = col(id) > lit(50)
|   Limit pushdown = 5
|   Output schema = value#Float64
|   Stats = { Approx num rows = 0, Approx size bytes = 0 B, Accumulated selectivity
|     = 0.30 }


== Physical Plan ==

* ScanTaskSource:
|   Num Scan Tasks = 1
|   Estimated Scan Bytes = 0
|   Num Parallel Scan Tasks = 1
|   Pushdowns: {projection: [value], filter: col(id) > lit(50), limit: 5}
|   Schema: {id#Int64, value#Float64}
|   Scan Tasks: [
|   {daft.io.lance.lance_scan:_lancedb_table_factory_function}
|   ]
|   Stats = { Approx num rows = 0, Approx size bytes = 0 B, Accumulated selectivity
|     = 0.30 }
|   Batch Size = Range(0, 131072]
```


<span id="561eb1fd"></span>
### Scan optimization: `fragment_group_size`

For Lance datasets containing a large number of small files (fragments), frequent I/O and task scheduling incur significant overhead. By setting the `fragment_group_size` parameter, you can group multiple fragments into a single scan task for processing, thereby effectively reducing overhead.

```Python
import daft

# (Reuse the configuration from the previous section)

# 1. Create a dataset containing multiple fragments
base_path = f"{TOS}/demo/fragments_dataset"
for i in range(10):
    df = daft.from_pydict({"id": [i]})
    df.write_lance(base_path, mode="append" if i > 0 else "overwrite", io_config=io_config)

# 2. Read without grouping, each fragment corresponds to a partition
df_no_grouping = daft.read_lance(base_path, io_config=io_config)
print(f"不分组的分区数: {df_no_grouping.num_partitions()}")  # Expected to be 10

# 3. Group every 3 fragments together
df_grouped = daft.read_lance(base_path, fragment_group_size=3, io_config=io_config)
print(f"分组后的分区数: {df_grouped.num_partitions()}")  # Expected to be 4 (ceil(10/3))
```


<span id="2db21c24"></span>
#### Execution results

The following is an excerpt of the actual output for reference only.

```Plain
不分组的分区数: 10
分组后的分区数: 4
```


<span id="c9445ebd"></span>
## Write to Lance dataset

Use the `DataFrame.write_lance()` method to write a Daft DataFrame in Lance format.

<span id="0be00844"></span>
### Write modes and file splitting parameters

`write_lance` supports three write modes and provides parameters to control file splitting, which is critical for managing small files.


* **`mode`**:

   * `create`: Create a new dataset. If the path already exists, the operation fails.

   * `append`: Append data to an existing dataset. If the path does not exist, the operation fails.

   * `overwrite`: Overwrite or create a new dataset.

* **File splitting parameters**:

   * **`max_rows_per_file`** (int): Maximum number of rows per Lance file.

   * **`max_bytes_per_file`** (int): Maximum number of bytes per Lance file (approximate value).

   * **`max_rows_per_group`** (int): Maximum number of rows per Row Group. Row Group is the internal read/write unit in Lance.


```Python
import daft

# (Reuse the configuration from the previous section)

path = f"{TOS}/demo/my_lance_table.lance"
df = daft.from_pydict({"a": list(range(10000))})

# 1. Create a new table and limit each file to a maximum of 8192 rows
print("### 创建模式 (max_rows_per_file):")
meta_create = df.write_lance(path, mode="create", io_config=io_config, max_rows_per_file=8192)
meta_create.show()

# 2. Overwrite, and limit each file to a maximum of 1KB (for demonstration only, actual value should be larger)
print("\n### 覆盖模式 (max_bytes_per_file):")
meta_overwrite = df.write_lance(path, mode="overwrite", io_config=io_config, max_bytes_per_file=1024)
meta_overwrite.show()

# 3. Append write, and limit each Row Group to a maximum of 1024 rows
print("\n### 追加模式 (max_rows_per_group):")
meta_append = df.write_lance(path, mode="append", io_config=io_config, max_rows_per_group=1024)
meta_append.show()
```


<span id="65311cd4"></span>
#### Execution results

The following is an excerpt of the actual output for reference only.

```Plain
### 创建模式 (max_rows_per_file):
╭───────────────┬──────────────────┬─────────────────┬─────────╮
│ num_fragments ┆ num_deleted_rows ┆ num_small_files ┆ version │
│ ---           ┆ ---              ┆ ---             ┆ ---     │
│ Int64         ┆ Int64            ┆ Int64           ┆ Int64   │
╞═══════════════╪══════════════════╪═════════════════╪═════════╡
│ 2             ┆ 0                ┆ 0               ┆ 1       │
╰───────────────┴──────────────────┴─────────────────┴─────────╯

(Showing first 1 of 1 rows)

### 覆盖模式 (max_bytes_per_file):
╭───────────────┬──────────────────┬─────────────────┬─────────╮
│ num_fragments ┆ num_deleted_rows ┆ num_small_files ┆ version │
│ ---           ┆ ---              ┆ ---             ┆ ---     │
│ Int64         ┆ Int64            ┆ Int64           ┆ Int64   │
╞═══════════════╪══════════════════╪═════════════════╪═════════╡
│ 1             ┆ 0                ┆ 0               ┆ 2       │
╰───────────────┴──────────────────┴─────────────────┴─────────╯

(Showing first 1 of 1 rows)

### 追加模式 (max_rows_per_group):
╭───────────────┬──────────────────┬─────────────────┬─────────╮
│ num_fragments ┆ num_deleted_rows ┆ num_small_files ┆ version │
│ ---           ┆ ---              ┆ ---             ┆ ---     │
│ Int64         ┆ Int64            ┆ Int64           ┆ Int64   │
╞═══════════════╪══════════════════╪═════════════════╪═════════╡
│ 2             ┆ 0                ┆ 0               ┆ 3       │
╰───────────────┴──────────────────┴─────────────────┴─────────╯

(Showing first 1 of 1 rows)
```


<span id="32e8593d"></span>
### Schema control

`write_lance` allows you to precisely control the schema for writing via Daft's `Schema` object, including type, order, and nullability.

```Python
from daft_tos_config import io_config, TOS
import daft

df = daft.from_pydict({
    "id": [1],
    "compressible_text": ["a" * 200],
    "image_bytes": [b"very-large-image-data..."]
})
path = f"{TOS}/demo/schema_lance_dataset"
df.write_lance(path, mode="overwrite", io_config=io_config)

df_read = daft.read_lance(path, io_config=io_config)
print("### 写入后的 Schema:")
print(df_read.schema())
```


<span id="8b45ce27"></span>
#### Execution results

The following is an excerpt of the actual output for reference only.

```Plain
### 写入后的 Schema:
╭───────────────────┬────────╮
│ column_name       ┆ type   │
╞═══════════════════╪════════╡
│ id                ┆ Int64  │
├╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌┼╌╌╌╌╌╌╌╌┤
│ compressible_text ┆ String │
├╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌┼╌╌╌╌╌╌╌╌┤
│ image_bytes       ┆ Binary │
╰───────────────────┴────────╯
```


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip"><strong>About advanced encoding metadata</strong> The specification of advanced encoding metadata (such as <code>zstd</code> compression, Blob storage, and more) requires the use of PyArrow's Schema metadata capabilities. If your environment only has <code>pylance</code> and <code>daft</code> installed, this example will not demonstrate this feature to ensure general applicability of the code. To enable this feature, install <code>pyarrow</code> and refer to related articles.</div>


Note: Advanced encoding metadata (such as zstd compression and Blob) requires PyArrow's metadata capabilities. In a local environment with only pylance and daft installed, the example shows the default inferred schema.

<span id="8b576d9f"></span>
## Lance file splitting and small file management

**Core principle: Avoid generating excessive small files (fragments).**  A large number of small files leads to significantly increased I/O overhead, complicated metadata management, and ultimately severe degradation of query performance, especially on object storage.

<span id="978e2a36"></span>
### Best practices recommendation


|Dimension |Recommended range |Note |
|---|---|---|
|**Rows per file** |**8,000 – 1,000,000** |Adjust according to column width and query pattern. For wide tables or scan\-intensive tasks, larger files are preferred. **Generally, fewer than 4096 rows is not recommended**. |
|**File size** |**64MB – 512MB** |This is the best practices range for object storage. Files that are too small will significantly increase API request overhead and metadata read latency. |


<span id="f7561bbd"></span>
### Write parameter recommendations


* **Using Daft (**  **`df.write_lance`** **)** :

   * **`max_bytes_per_file`**: **Preferred parameter**. Directly controls file size, which is most consistent with best practices for object storage.

   * **`max_rows_per_file`**: Can be used as an alternative when row sizes are relatively uniform.

   * **`max_rows_per_group`**: Controls the granularity of Row Groups. A file can contain multiple Row Groups. A reasonable Row Group size (typically recommended between 20,000 and 100,000 rows) facilitates predicate pushdown.


<span id="af4c5717"></span>
### Read and optimization strategies


* **Read optimization**: If there are already a large number of small fragments, use the `daft.read_lance` **`fragment_group_size`** parameter when reading. It can merge multiple small files into a single scan task, reducing I/O and scheduling overhead.

* **Offline governance**: Periodically rewrite (compaction process) fragmented datasets. During rewriting, standardize write parameters (such as `max_bytes_per_file`) and compression strategies to generate a new version with a healthy structure.


<span id="527d7539"></span>
## Common questions and troubleshooting


* **Q: Are you encountering 403 Forbidden or 404 Not Found errors?** 

   **A**: This is usually a permissions issue. Please check credentials, bucket policies, and IAM policies.

* **Q:**  **`create`** ** mode write failed?** 

   **A**: Ensure the target path is not an existing file or Lance dataset.

* **Q:**  **`append`** ** mode write failed?** 

   **A**: Ensure the target path is an existing Lance dataset, and the schema of the data to be appended is compatible with the target table.
