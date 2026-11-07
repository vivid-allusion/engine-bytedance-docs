---
title: "EMR Lance-Ray general operation guide"
product: "BytePlus EMR"
product_code: "E-MapReduce"
source: "https://docs.byteplus.com/en/docs/E-MapReduce/EMR_Lance-Ray_general_operation_guide"
---

`lance-ray` is a high\-performance I/O library for the Ray ecosystem, dedicated to reading and writing datasets in `Lance` format. It provides developers with a powerful solution for managing and efficiently reading and writing large\-scale datasets. This article introduces general usage guidance for the BytePlus `Lance-Ray` library.

<span id="51e9ebfb"></span>
# Features and advantages


* **High\-performance random access**: The Lance format natively supports columnar storage and efficient random data access, making it ideal for selective reading scenarios common in machine learning training and data analysis.

* **Efficient writing and appending**: `lance-ray` is optimized for Ray's distributed features, supporting parallel writing, overwrite, and append operations, which simplifies the data ETL process.

* **More distributed interfaces**: Supports more distributed interfaces, such as distributed column addition, distributed compaction, and distributed full\-text indexing (currently used with pylance version 0.39).


<span id="58995114"></span>
# Write Lance data

`lance-ray` provides the `write_lance` function for efficiently writing Ray Datasets in Lance format. It supports writing to the local file system as well as directly to TOS, S3, and other object storage services compatible with the S3 protocol.

<span id="6a38b9da"></span>
## Basic write example

You can easily write a Ray Dataset to a local path or remote object storage.

<span id="87627c2b"></span>
### Example 1: Write to the local file system

```Python
# Create a simple Ray Dataset
import pandas as pd
import ray
import lance
import lance_ray as lr
data = pd.DataFrame({
    "id": range(10),
    "value": [f"value_{i}" for i in range(10)]
})
ds = ray.data.from_pandas(data)

# Define local storage path
local_path = "/tmp/my_lance_dataset.lance"

# Write data using lr.write_lance
lr.write_lance(ds, uri=local_path, mode="overwrite")

print(f"The data has been successfully written to the local path: {local_path}")
```


<span id="7f14cbe6"></span>
### Example 2: Write to TOS/S3 object storage

When writing to object storage, you need to provide the correct `storage_options` to configure access credentials and endpoint.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip"><strong>Note:</strong></div>



* <div data-tips="true" data-tips-type="tip">To access TOS in the Volcano Engine ECS/EMR environment, it is recommended to use the internal endpoint for better performance and to avoid public network traffic charges, such as <code>https://bucket-name.tos-s3-cn-beijing.ivolces.com</code>.</div>


* <div data-tips="true" data-tips-type="tip">To access from the public network, use the public endpoint, such as <code>https://bucket-name.tos-s3-cn-beijing.volces.com</code>.</div>



```Python
# Prepare the Ray Dataset to be written
ds = ray.data.range(100).map(
    lambda x: {"id": x["id"], "str": f"str-{x['id']}"}
)

# Configure the storage_options for TOS/S3
# Replace the placeholders below with your actual information
storage_options = {
    "access_key_id": "YOUR_ACCESS_KEY",
    "secret_access_key": "YOUR_SECRET_KEY",
    "aws_endpoint": "https://your-bucket.tos-s3-your-region.ivolces.com", # Example endpoint, must include bucket
    "aws_region": "your-region",
    "virtual_hosted_style_request": "true"
}

# Define the path on object storage
s3_path = "s3://your-bucket/path/to/dataset.lance"

# Use lr.write_lance to write data to TOS/S3
lr.write_lance(
    ds,
    uri=s3_path,
    storage_options=storage_options,
    mode='overwrite'
)

print(f"The data has been successfully written to the object storage path: {s3_path}")
```


<span id="fcfd79f7"></span>
## Key parameter description

`write_lance` provides a rich set of parameters to control writing behavior. The following are descriptions of commonly used parameters:


|Parameters |Chinese definition |Note and constraints |
|---|---|---|
|`ds` |Ray dataset |The `ray.data.Dataset` object to be written. |
|`uri` |Storage path |The URI of the target Lance dataset, which can be a local path (such as `/path/to/data.lance`) or an object storage path (such as `s3://bucket/data.lance`). |
|`mode` |Write mode |* **`create`** (default): If the path already exists, an error will be reported.<br><br>* **`append`**: Append data to an existing dataset; the path must exist.<br><br>* **`overwrite`**: If the path exists, overwrite the entire dataset. |
|`schema` |Data structure |(Optional) A `pyarrow.Schema` object. If not provided, it will be automatically inferred from the data. For data containing special types (such as Blob), it is recommended to provide it explicitly. |
|`min_rows_per_file` |Minimum rows per file |(Optional) The minimum number of rows contained in each Lance data file. The default is `1024 * 1024`. |
|`max_rows_per_file` |Maximum rows per file |(Optional) The maximum number of rows contained in each Lance data file. The default is `64 * 1024 * 1024`. Reducing this value can generate more, smaller files. |
|`data_storage_version` |Data storage version |(Optional) Specify the storage format version of Lance. Newer versions are more efficient. |
|`storage_options` |Storage configuration |(Optional) A dictionary used to configure access parameters for the underlying file system, such as access keys, endpoint, and so on. |
|`stream` |Streaming write |(Optional) Boolean value, default is `False`. When set to `True`, incremental streaming write is enabled, suitable for memory\-constrained scenarios. |
|`batch_size` |Batch size |(Optional) Takes effect when `stream=True`, defines the size of each micro\-batch. The default is 1024. |
|`resume_rows` |Number of rows to skip for breakpoint resumption |(Optional) Takes effect when `stream=True`, skips the first N rows of the source data for simple breakpoint resumption. |
|`concurrency` |Concurrency |(Optional) The maximum concurrency of the write task. |


<span id="64798710"></span>
# Read Lance data

The `lance-ray` `read_lance` function enables efficient reading of Lance datasets from local or object storage and loads them as Ray Datasets for subsequent distributed computation.

<span id="8301637d"></span>
## Basic read example

You can directly read data by providing the dataset URI.

```Python
# Define the path of the Lance dataset (local or S3)
dataset_uri = "/tmp/my_lance_dataset.lance" # Or "s3://your-bucket/path/to/dataset.lance"

# Configure the storage_options required to access object storage (if needed)
storage_options = {
    "access_key_id": "YOUR_ACCESS_KEY",
    "secret_access_key": "YOUR_SECRET_KEY",
    "aws_endpoint": "https://your-bucket.tos-s3-your-region.ivolces.com",
    "aws_region": "your-region",
    "virtual_hosted_style_request": "true"
}

# Use lr.read_lance to read data
# If using a local file, storage_options can be ignored
ds = lr.read_lance(uri=dataset_uri, storage_options=storage_options)

# View the dataset schema and the first few rows
print("dataset Schema:")
print(ds.schema())

print("\nDataset rows:", ds.count())

print("\nFirst 5 rows:")
ds.show(5)
```


<span id="147815a2"></span>
# Data evolution (Ray)

In data processing and machine learning workflows, we often need to derive new features or add metadata based on existing datasets; this process is known as **Data Evolution**. `lance-ray` provides the `add_columns` function for this purpose, which leverages Ray's distributed computing capabilities to efficiently add new columns to an existing Lance dataset.

This operation is **in\-place**, meaning it appends a new version to the existing dataset without completely rewriting the entire dataset, thereby enabling efficient schema changes.

<span id="de7bd67b"></span>
## Core functionality and use cases

The core of `add_columns` is to batch process data using a user\-defined **transform function**. This function receives a data batch (`pyarrow.RecordBatch`), computes the new columns, and returns a batch containing only the new column data.

**Typical use cases**:


* **Feature engineering**: Compute new feature columns based on one or more original columns. For example, generate embedding vectors from a text column, or derive year, month, and day dimensions from a timestamp column.

* **Data augmentation**: Add a unique ID or default value to each row of the dataset.

* **Data cleaning and normalization**: Process existing columns (such as case conversion or unit conversion) and store the results as new columns.


<span id="e50b7a3f"></span>
## Key parameter description


|**Parameter** |**Chinese explanation** |**Note and constraints** |
|---|---|---|
|`uri` |Dataset path |The URI of the target Lance dataset, supporting local or object storage paths (such as `s3://...`). |
|`transform` |Transformation function |A Python function that takes a `pyarrow.RecordBatch` and returns a `pyarrow.RecordBatch` containing only the new columns. **This is the core for implementing column extension**. |
|`storage_options` |Storage configuration |(Optional) Credentials and endpoint configuration required to access object storage (such as TOS/S3). |
|`read_columns` |Columns to read |(Optional) List of original column names that the transformation function needs to read. Optimize read performance and avoid loading unnecessary columns. |
|`concurrency` |Concurrency |(Optional) Maximum concurrency for Ray Tasks executing the transformation operation. |
|`ray_remote_args` |Ray remote parameters |(Optional) Additional parameters passed to Ray Tasks for resource tuning. See later sections for details. |


<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>



* <div data-tips="true" data-tips-type="warning"><strong>Atomicity and versioning</strong>: The <code>add_columns</code> operation is atomic. After successful execution, a new dataset version will be created. If the operation fails, the dataset will roll back to the previous version to ensure data consistency.</div>


* <div data-tips="true" data-tips-type="warning"><strong>Concurrency safety</strong>: Multiple concurrent <code>add_columns</code> or other write operations on the same dataset may cause conflicts. Lance follows the "last\-writer\-wins" principle.</div>


* <div data-tips="true" data-tips-type="warning"><strong>Purity of the transform function</strong>: The returned <code>RecordBatch</code> <strong>must contain only the new columns</strong>, and the number of rows must match the input batch; otherwise, an error will occur.</div>



<span id="261ebeb7"></span>
## Example: Derive new columns and add them to object storage

The following example demonstrates how to read a dataset stored on TOS/S3 and derive a new string column `id_str` based on the `id` column.

```Python
import lance_ray as lr
import pyarrow as pa
import ray

# Assume we already have a Lance dataset stored on TOS/S3
# ds = ray.data.range(10)
# storage_options = { ... } # Configure your storage_options
# s3_uri = "s3://your-bucket/path/to/my_dataset.lance"
# lr.write_lance(ds, s3_uri, storage_options=storage_options, mode="overwrite")

# --- Now start executing add_columns ---

# 1. Define the transformation function
def id_to_string_transform(batch: pa.RecordBatch) -> pa.RecordBatch:
    """
    Convert the id column to string and add a prefix.
    """
    ids = batch["id"]
    new_col_data = [f"id_{i.as_py()}" for i in ids]
    
    # Create a pyarrow Array for the new column
    new_array = pa.array(new_col_data, type=pa.string())
    
    # Return a RecordBatch containing only the new column
    return pa.RecordBatch.from_arrays([new_array], names=["id_str"])

# 2. Configure storage options
s3_uri = "s3://your-bucket/path/to/my_dataset.lance"
storage_options = {
    "access_key_id": "YOUR_ACCESS_KEY",
    "secret_access_key": "YOUR_SECRET_KEY",
    "aws_endpoint": "https://your-bucket.tos-s3-your-region.ivolces.com",
    "aws_region": "your-region",
    "virtual_hosted_style_request": "true"
}

# 3. Call add_columns
lr.add_columns(
    uri=s3_uri,
    transform=id_to_string_transform,
    read_columns=["id"],  # Explicitly specify that we only need to read the 'id' column
    storage_options=storage_options
)


# 4. Verify the result
ds_new = lr.read_lance(uri=s3_uri, storage_options=storage_options)
print(ds_new.schema())
ds_new.show(5)

# Expected output:
# Dataset schema after adding the new column:
# id: int64
# id_str: string
#
# First 5 rows of data:
# {'id': 0, 'id_str': 'id_0'}
# {'id': 1, 'id_str': 'id_1'}
# {'id': 2, 'id_str': 'id_2'}
# {'id': 3, 'id_str': 'id_3'}
# {'id': 4, 'id_str': 'id_4'}
```


<span id="1a192e28"></span>
# Distributed compaction

As data is continuously appended and deleted, a Lance dataset may accumulate a large number of small fragmented files (fragments), or contain many records marked as deleted but not physically removed. The **distributed compaction** operation is designed to address these issues. It optimizes the dataset using Ray's parallel computing capabilities, with the main objectives including:


* **Merge fragmented files**: Combine multiple small data files into larger, more organized files to improve subsequent read performance.

* **Materialized deletion (materialize_deletions)** : Physically deletes rows that have been marked as "deleted" to reclaim storage space and improve query efficiency.

* **Ensure data integrity**: During the optimization process, ensure that all original data is correctly processed and not lost.


<span id="08917043"></span>
## File\-level compaction: `lr.compact_files`

`lr.compact_files` is the core API for performing distributed file\-level compaction. It can optimize a single Lance dataset (Table).


|Parameters |Chinese definition |Note and constraints |
|---|---|---|
|`uri` or `namespace` group |Target dataset |You can provide the direct `uri` path of the dataset, or locate the dataset via `namespace_impl`, `namespace_properties`, and `table_id`. One of the two must be provided. |
|`compaction_options` |Compaction options |A `lance.optimize.CompactionOptions` object for fine\-grained control of Compaction behavior. |
|`num_workers` |Number of worker nodes |The number of Ray concurrent tasks used to execute Compaction. If the specified quantity exceeds the actual number of required tasks (for example, only one compaction task), the value will be automatically reduced. |
|`ray_remote_args` |Ray remote parameters |(Optional) Additional parameters passed to each Ray Compaction task, such as `{"num_cpus": 2}`, for resource tuning. |
|`storage_options` |Storage configuration |(Optional) Credentials and endpoint configuration required to access object storage (such as TOS/S3). |


After this function executes successfully, it returns a `Metrics` object containing **`fragments_removed`** (number of fragments removed) and **`fragments_added`** (number of new fragments generated). If the dataset is already optimized and no action is required, it returns `None`.

<span id="f53f9b8b"></span>
### Common CompactionOptions configurations

With `CompactionOptions`, you can customize optimization strategies in detail. Common fields include:


|Field |Chinese definition |Note and constraints |
|---|---|---|
|`target_rows_per_fragment` |Target row count |The target number of rows for each merged fragment. This is a key parameter for controlling file size and count. For example, if set to `20_000`, each new fragment is expected to contain approximately 20,000 rows. |
|`materialize_deletions` |Whether to materialize deletions |Boolean value, default is `False`. When set to `True`, the materialized deletion process will be triggered, rewriting fragments that meet the threshold conditions to physically remove deleted rows. |
|`materialize_deletions_threshold` |Deletion threshold |Floating\-point number, range `[0, 1]`. Materialized deletion will only be performed when the proportion of deleted rows in a fragment exceeds this threshold. |
|`num_threads` |Thread count |The number of threads used within each Compaction task for parallel reading, writing, and encoding data. |


<span id="2ba44b84"></span>
### Example: merging small files and concurrency control

The following example demonstrates how to merge a large number of small fragments and set appropriate `num_workers` and `ray_remote_args`:

```Python
import lance
import lance_ray as lr
import pandas as pd
import ray
from lance.optimize import CompactionOptions

ray.init()

# Construct a dataset containing multiple small fragments
fragment_data = [
    pd.DataFrame({"id": range(i * 5, (i + 1) * 5), "value": [f"frag_{i}_row_{j}" for j in range(5)]})
    for i in range(100)
]

# Write each DataFrame as a fragment
uri = "/tmp/compaction_small_files.lance"
first = ray.data.from_pandas(fragment_data[0])
lr.write_lance(first, uri=uri, min_rows_per_file=5, max_rows_per_file=5)
for df in fragment_data[1:]:
    lr.write_lance(
        ray.data.from_pandas(df),
        uri=uri,
        mode="append",
        min_rows_per_file=5,
        max_rows_per_file=5,
    )

dataset = lance.dataset(uri)
print("Sharding number before Compaction:", len(dataset.get_fragments()))
print("row number before Compaction:", dataset.count_rows())

# Configure the Compaction strategy
options = CompactionOptions(
    target_rows_per_fragment=20,
    num_threads=1,
)

metrics = lr.compact_files(
    uri=uri,
    compaction_options=options,
    num_workers=4,
    ray_remote_args={"num_cpus": 1},
)

print("Number of shardings removed:", metrics.fragments_removed)
print("Number of shardings:", metrics.fragments_added)

# Verify data integrity
after = lance.dataset(uri)
assert after.count_rows() == dataset.count_rows()
```


<span id="dc2821c1"></span>
### Important notes

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>



* <div data-tips="true" data-tips-type="warning"><strong>Object storage configuration</strong>: When performing Compaction on datasets stored in TOS/S3, the <code>storage_options</code> parameter must be correctly passed to ensure Ray's remote tasks have access to object storage and the correct endpoint configuration (the configuration method can be reused from the previous write/read sections).</div>


* <div data-tips="true" data-tips-type="warning"><strong>Concurrency and resources</strong>: <code>num_workers</code> controls the number of concurrent tasks, while <code>ray_remote_args</code> controls the resources for each task. These two parameters should be balanced according to the size of the Ray cluster and the dataset to achieve optimal performance and resource utilization.</div>


* <div data-tips="true" data-tips-type="warning"><strong>Data integrity</strong>: Compaction is a stateful operation that creates a new dataset version. Lance guarantees the atomicity of the operation. Before and after execution, you can use <code>count_rows()</code> or use <code>pandas</code> to compare data to verify that no data is lost or corrupted.</div>


* <div data-tips="true" data-tips-type="warning"><strong>Database\-level operation</strong>: <code>compact_database</code> iterates over and processes multiple tables in a single call, making it suitable for offline, full\-database maintenance. It is recommended to execute during off\-peak business hours and monitor changes in storage usage and query latency.</div>



<span id="2f4da8ba"></span>
# Distributed full\-text index (FTS/Inverted)

To accelerate text data retrieval, `lance-ray` supports building **distributed full\-text search (FTS) indexes** for string\-type columns, also known as **inverted indexes (Inverted Index)** . This feature leverages Ray's parallel computing capabilities to distribute index building tasks across multiple workers, efficiently handling large\-scale datasets.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>



* <div data-tips="true" data-tips-type="warning">To use <code>lr.create_scalar_index</code> for building distributed scalar indexes (including FTS), <code>pylance >= 0.36.0</code> is required; if the version is too low, related tests or examples may be skipped.</div>


* <div data-tips="true" data-tips-type="warning">Other types of scalar indexes (such as <code>BTREE</code>) typically require <code>pylance >= 0.37.0</code> or higher. Related notes can be included in the index overview section for unified explanation.</div>



<span id="0cd14be4"></span>
### Main API: `lr.create_scalar_index`

`lr.create_scalar_index` is the unified entry point for building various scalar indexes, including FTS.


|Parameters |Chinese definition |Note and constraints |
|---|---|---|
|`uri` or `namespace` group |Target dataset |You can directly use `uri` to point to a Lance dataset, or locate it by combining `namespace_impl`, `namespace_properties`, and `table_id`. |
|`column` |Target column |The name of the column to be indexed. For FTS indexes, this column must be of string type (such as `pa.string()`). |
|`index_type` |Index type |For full\-text indexes, set this to `'INVERTED'` or `'FTS'`. In most scenarios, it is recommended to use `'INVERTED'` as the default value. |
|`name` |Index name |(Optional) Specify a name for the index to facilitate subsequent `list_indices`, replacement, or deletion. Multiple indexes with different names can exist on the same column. |
|`replace` |Whether to replace an existing index |Boolean value, default is `False`. If set to `False` and an index with the same name exists, an error will be reported; if set to `True`, the new index will overwrite the old one. |
|`num_workers` |Number of worker nodes |The number of Ray tasks for parallel index construction. If the value is set higher than the number of shards, it will be automatically reduced. |
|`ray_remote_args` |Ray remote parameters |(Optional) Resource parameters passed to each index build task, such as `{"num_cpus": 1}`. The specific meaning is consistent with the earlier "Distributed index — Custom Ray parameters" section. |
|`storage_options` |Storage configuration |(Optional) Credentials, endpoint, and Region configuration required to access object storage such as TOS/S3. It is recommended to reuse the configuration method described in the earlier write/read sections. |
|`**kwargs` |Other index parameters |(Optional) Other parameters passed to the underlying index builder, such as `remove_stop_words=False` to control whether to remove stop words. |


<span id="a63a8f32"></span>
### Using FTS indexes for queries

Once the index is built, you can use the `scanner` with the `full_text_query` parameter to perform efficient full\-text search.

```Python
# Assume the index has already been built on the 'text' column
dataset = lance.dataset("/tmp/fts_dataset.lance")

results = dataset.scanner(
    full_text_query="Python",
    columns=["id", "text"],
).to_table()

print(results.to_pandas())
```


<span id="da7546c3"></span>
### Errors and edge cases

Common errors when calling `lr.create_scalar_index` include:


* **Column does not exist**: For example, `ValueError: Column 'nonexistent' not found`, usually caused by a typo in the column name.

* **Column type error**: For example, `TypeError: must be string type`, triggered when attempting to build an FTS index on a non\-string column.

* **Invalid index type**: When `index_type` is not in the supported list (such as `'BTREE'`, `'BITMAP'`, `'LABEL_LIST'`, `'INVERTED'`, `'FTS'`, `'NGRAM'`, `'ZONEMAP'`, and more), a `ValueError` is raised.

* **Invalid** **`num_workers`**: When `num_workers <= 0`, a `ValueError: num_workers must be positive` is raised.


<span id="9f701ddf"></span>
### Example: basic creation and search

```Python
import lance
import lance_ray as lr
import pandas as pd
import ray

ray.init()

# Prepare a dataset containing a text column
text_data = pd.DataFrame({
    "id": range(8),
    "text": [
        "The quick brown fox jumps over the lazy dog",
        "Python is a powerful programming language",
        "Machine learning algorithms are fascinating",
        "Data science requires statistical knowledge",
        "Natural language processing uses text analysis",
        "Distributed computing scales horizontally",
        "Ray framework enables parallel processing",
        "Lance format provides efficient storage",
    ],
})

uri = "/tmp/fts_dataset.lance"
ds = ray.data.from_pandas(text_data)

# Write to Lance dataset
lr.write_lance(ds, uri=uri, mode="overwrite", min_rows_per_file=2, max_rows_per_file=2)

# 1. Build FTS index in distributed mode
indexed_ds = lr.create_scalar_index(
    uri=uri,
    column="text",
    index_type="INVERTED",  # Or 'FTS'
    num_workers=2,
)

# 2. Verify the index has been created
indices = indexed_ds.list_indices()
print("Index created:", indices)

# 3. Perform full-text search using indexes
search_term = "language"
results = indexed_ds.scanner(
    full_text_query=search_term,
    columns=["id", "text"],
).to_table().to_pandas()

print(f"Search '{search_term}':")
print(results)
```
