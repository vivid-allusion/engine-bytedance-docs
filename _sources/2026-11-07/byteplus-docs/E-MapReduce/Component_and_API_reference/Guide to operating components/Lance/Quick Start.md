---
title: "Quick Start"
product: "BytePlus EMR"
product_code: "E-MapReduce"
source: "https://docs.byteplus.com/en/docs/E-MapReduce/Quick_Start"
---

This article is intended only for local Python package testing. For operations using Ray on EMR, refer to [Operate Lance data with Ray](https://docs.byteplus.com/docs/E-MapReduce/109328).

This article mainly describes how to perform Python package testing locally, including installing the SDK locally, creating datasets, version control, vector data preparation, and more. It also provides detailed instructions on a series of operations for Lance datasets, such as writing, deleting rows, updating rows, upsert, schema evolution (renaming columns, changing column data types, adding new columns, adding new columns using merge, deleting columns), reading (including iterative reading, filter pushdown, random access), table maintenance, and object storage configuration. For version control, you can append or overwrite data, as well as create and check out tags.

<span id="8ef34622"></span>
## **Preparation**

The SDK has been installed locally. If not installed, refer to the following steps.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Please use a Linux environment to install the PyLance package.</div>


```Bash
pip install ve-pylance
```


<span id="ac6b84b1"></span>
## Instructions

<span id="7ad66ff5"></span>
### Create a dataset

```Python
import lance
import pyarrow as pa

table = pa.Table.from_pylist([{"name": "Alice", "age": 20},
                              {"name": "Bob", "age": 30}])
lance.write_dataset(table, "./alice_and_bob.lance")
```


This will create an alice_and_bob.lance directory in the local directory, which contains a data directory for actual data, a _versions directory for version management, and a _transactions directory for transaction management.

```Bash
alice_and_bob.lance
|-- data
|   `-- 527881ac-cbaf-4519-a5a6-e39bffae5c79.lance
|-- _transactions
|   `-- 0-89006b07-e468-4f4f-9ca1-35a0f3786af0.txn
`-- _versions
    `-- 1.manifest
```


Create a DataFrame

```Python
df = pd.DataFrame({"a": [5]})
```


Write it to Lance

```Python
shutil.rmtree("/tmp/test.lance", ignore_errors=True)
dataset = lance.write_dataset(df, "/tmp/test.lance")
dataset.to_table().to_pandas()
```


Convert from Parquet to Lance and read a Parquet file

```Python
shutil.rmtree("/tmp/test.parquet", ignore_errors=True)
shutil.rmtree("/tmp/test.lance", ignore_errors=True)
tbl = pa.Table.from_pandas(df)
pa.dataset.write_dataset(tbl, "/tmp/test.parquet", format='parquet')
parquet = pa.dataset.dataset("/tmp/test.parquet")
parquet.to_table().to_pandas()
```


Write to a new Lance dataset

```Python
dataset = lance.write_dataset(parquet, "/tmp/test.lance")
```


Validate and print the data

```Bash
确保数据一致
dataset.to_table().to_pandas()
```


<span id="1b5bf33b"></span>
### Read a Lance dataset

The Lance dataset API follows the PyArrow API conventions.


* Query a dataset


```Python
dataset = lance.dataset("./alice_and_bob.lance")
# View the number of rows in the dataset
dataset.count_rows()

# View the schema of the dataset
dataset.schema

# View all contents of the dataset
dataset.to_table()
 
# Scan data based on conditions
dataset.scanner(filter="age > 25").to_table()
 
# Scan data based on conditions and return only the name column
dataset.scanner(columns=["name"], filter="age > 25").to_table()
```


<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/79c8080f28414755be2e87f7e0802a94~tplv-goo7wpa0wc-image.image" width="1242px" /></div>


To open a Lance dataset, use the `lance.dataset()` function:

```Bash
import lance
ds = lance.dataset("s3://bucket/path/imagenet.lance")或者本地路径
ds = lance.dataset("./imagenet.lance")
```


The most direct way to read a Lance dataset is to use the `lance.LanceDataset.to_table()` method to load the entire dataset into memory.

Because Lance is a high\-performance columnar format, it can efficiently read subsets of the dataset by leveraging column (projection) pushdown and filter (predicate) pushdown.

```Python
table = ds.to_table(
    columns=["image", "label"],filter="label = 2 AND text IS NOT NULL",
    limit=1000,
    offset=3000)
```


Lance understands the cost of reading heavy columns such as `image`. Therefore, it uses an optimized query plan to execute operations efficiently.

<span id="401f80fe"></span>
#### Iterative reading

If the dataset is too large to load into memory at once, use the `lance.LanceDataset.to_batches()` method to read in batches:

```Bash
for batch in ds.to_batches(columns=["image"], filter="label = 10"):对批次进行处理
    compute_on_batch(batch)
```


<span id="f7b1a304"></span>
#### Filter pushdown

Lance uses standard SQL expressions as predicates for dataset filtering. By pushing SQL predicates directly down to the storage system, I/O load during scanning can be significantly reduced.

code sample

```Python
table = ds.to_table(columns=["image", "label"],
filter="label = 2 AND text IS NOT NULL",limit=1000,offset=3000)
```


Currently, Lance supports a growing number of expressions.


* `>`, `>=`, `<`, `<=`, `=`

* `AND`, `OR`, `NOT`

* `IS NULL`, `IS NOT NULL`

* `IS TRUE`, `IS NOT TRUE`, `IS FALSE`, `IS NOT FALSE`

* `IN`

* `LIKE`, `NOT LIKE`

* `regexp_match(column, pattern)`

* `CAST`


Nested fields can be accessed using subscripts. Struct fields can be accessed using field name subscripts, while list fields can be accessed using index subscripts.

If a column name contains special characters or is an SQL keyword, it can be escaped using backticks (```). For nested fields, each part of the path must be enclosed in backticks.

Literals for dates, timestamps, and decimals can be written as string values following the type name. For example:

```Plain
date_col = date '2021-01-01'
and timestamp_col = timestamp '2021-01-01 00:00:00'
and decimal_col = decimal(8,3) '1.000'
```


For timestamp columns, the precision can be specified in the type parameter. The default precision is microseconds (6).

Internally, Lance stores data in Arrow format. The mapping from SQL types to Arrow types is as follows:

<span id="eb2cf247"></span>
#### Random access

As a notable feature of columnar formats, Lance enables fast random access.

```Bash
访问第 2 行、第 101 行和第 501 行
data = ds.take([1, 100, 500], columns=["image", "label"])
```


The ability to quickly access individual rows plays a crucial role in facilitating various workflows, such as random sampling and shuffling during machine learning training. Additionally, it allows users to build secondary indexes, enabling fast query execution and improved performance.

<span id="11215a77"></span>
### Writing to Lance datasets

Similar to Apache Pyarrow, the simplest way to create a Lance dataset is to write a `pyarrow.Table` using `lance.write_dataset()`.

```Python
import lance
import pyarrow as pa
table = pa.Table.from_pylist([{"name": "Alice", "age": 20},{"name": "Bob", "age": 30}])
lance.write_dataset(table, "./alice_and_bob.lance")
```


If the dataset is too large to fit into memory at once, `lance.write_dataset()` also supports writing the dataset via an iterator of `pyarrow.RecordBatch`.

```Python
import lance
import pyarrow as pa

def producer():yield pa.RecordBatch.from_pylist([{"name": "Alice", "age": 20}])yield pa.RecordBatch.from_pylist([{"name": "Blob", "age": 30}])
schema = pa.schema([
    pa.field("name", pa.string()),
    pa.field("age", pa.int64()),])
lance.write_dataset(producer(), "./alice_and_bob.lance", schema)
```


`lance.write_dataset()` supports writing `pyarrow.Table`, `pandas.DataFrame`, `pyarrow.Dataset`, and `Iterator[pyarrow.RecordBatch]`. For more details, please refer to its documentation.

<span id="faea50f9"></span>
#### Deleting rows

Lance supports deleting rows from a dataset using SQL filters. For example, to delete the row for Bob from the dataset above, use the following code:

```Python
import lance
dataset = lance.dataset("./alice_and_bob.lance")
dataset.delete("name = 'Bob'")
```


`lance.LanceDataset.delete()` supports the same filters described in filter push\-down.

Rows are deleted by marking them as deleted in a separate deletion index. This is faster than rewriting files and does not invalidate indexes pointing to those files. Any subsequent queries will not return deleted rows.

<span id="e39fab15"></span>
#### Updating rows

Lance supports updating rows based on SQL expressions using the `lance.LanceDataset.update()` method. For example, if we find that Bob's name is sometimes written as `Blob` in the dataset, we can correct it as follows:

```Python
import lance
dataset = lance.dataset("./alice_and_bob.lance")
dataset.update({"name": "'Bob'"}, where="name = 'Blob'")
```


The updated value is an SQL expression, which is why `'Bob'` is enclosed in single quotation marks. This means that we can use complex expressions referencing existing columns as needed. For example, if two years have passed and we want to update Alice's and Bob's ages in the same example, we can do this as follows:

```Python
import lance
dataset = lance.dataset("./alice_and_bob.lance")
dataset.update({"age": "age + 2"})
```


To update a set of individual rows with new values, the merge insert operation described below is usually more efficient.

```Bash
import lance


new_table = pa.Table.from_pylist([{"name": "Alice", "age": 30},{"name": "Bob", "age": 20}])这种方法可以工作，但效率不高，下面有更好的方法
dataset = lance.dataset("./alice_and_bob.lance")for idx in range(new_table.num_rows):
    name = new_table[0][idx].as_py()
    new_age = new_table[1][idx].as_py()
    dataset.update({"age": new_age}, where=f"name='{name}'")
```


<span id="86ddfe1a"></span>
#### Batch update

Lance supports the merge insert operation. This can be used to add new data in batches, and can also (potentially) match existing data. This operation can be used for a variety of different use cases.

<span id="ae23728d"></span>
##### Batch update

The `lance.LanceDataset.update()` method is suitable for updating rows based on filters. However, to replace existing rows with new rows, the merge insert operation is more efficient:

```Bash
import lance

# Change the ages of Alice and Bob
new_table = pa.Table.from_pylist([{"name": "Alice", "age": 30},{"name": "Bob", "age": 20}])
dataset = lance.dataset("./alice_and_bob.lance")这将使用 name 作为匹配行的键。合并插入内部使用 JOIN，因此你通常希望这个列是某种唯一键或 ID。
dataset.merge_insert("name") \.when_matched_update_all() \.execute(new_table)
```


<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">Similar to update operations, the modified rows are first removed from their current positions and then reinserted into the table. After reinsertion, these rows will be at the end of the table. In addition, because a hash join operation is used internally, the relative order of these modified rows may change. In other words, the original relative positions in the table may no longer be maintained after this operation.</div>


Sometimes, we only want to insert data that has not been previously inserted. This may occur when we have a batch of data but do not know which rows have already been added, and want to avoid creating duplicate rows. We can use the merge insert operation to achieve this:

```Bash
import lance

# Bob is already in the table, but Carla is new
new_table = pa.Table.from_pylist([{"name": "Bob", "age": 30},{"name": "Carla", "age": 37}])
dataset = lance.dataset("./alice_and_bob.lance")这将插入 Carla 但保持 Bob 不变
dataset.merge_insert("name") \.when_not_matched_insert_all() \.execute(new_table)
```


<span id="839356b0"></span>
##### Update or insert (upsert)

Sometimes, we want to combine the two behaviors described above. If a row already exists, we want to update it; if the row does not exist, we want to add it. This operation is sometimes referred to as "upsert". We can also use the merge insert operation to achieve this:

```Bash
import lance

# Change Carla's age and insert David
new_table = pa.Table.from_pylist([{"name": "Carla", "age": 27},{"name": "David", "age": 42}])
dataset = lance.dataset("./alice_and_bob.lance")这将更新 Carla 并插入 David
dataset.merge_insert("name") \.when_matched_update_all() \.when_not_matched_insert_all() \.execute(new_table)
```


<span id="38e9af45"></span>
##### Replace partial data

A less common but still useful behavior is to replace the data in a region of existing rows (as defined by a filter) with new data. This is similar to performing both delete and insert in a single transaction. For example:

```Bash
import lance
new_table = pa.Table.from_pylist([{"name": "Edgar", "age": 46},{"name": "Francine", "age": 44}])
dataset = lance.dataset("./alice_and_bob.lance")这将移除任何年龄大于 40 的人，并插入我们的新数据
dataset.merge_insert("name") \.when_not_matched_insert_all() \.when_not_matched_by_source_delete("age >= 40") \.execute(new_table)
```


Complete example

```Python
# Update certain rows
dataset.update({"name": "'Blob'"}, where="name = 'Bob'")

# Delete certain rows
dataset.delete("name = 'Blob'")

# Write a new batch of data
table = pa.Table.from_pylist([{"name": "Alice", "age": 20},
                              {"name": "Bob", "age": 30}])
lance.write_dataset(table, "./alice_and_bob.lance", mode = "append")
```


<span id="b33fbc3d"></span>
#### Schema Change

Lance is a data lake that provides **multi\-version capability**, enables rapid data addition, deletion, querying, updating, and schema changes, and also offers time travel capability.

Lance supports schema changes: adding, deleting, and modifying columns in a dataset. Most of these operations can be performed without rewriting the data files in the dataset, making them highly efficient.

Typically, schema changes conflict with most other concurrent write operations. For example, if you change the dataset's schema while others are appending data to the dataset, either your schema change will fail or the append operation will fail, depending on the order of operations. Therefore, it is recommended to perform schema changes when there are no other write operations.

<span id="69019072"></span>
##### Rename columns

You can use the `lance.LanceDataset.alter_columns()` method to rename columns.

```Python
import lance
import pyarrow as pa
table = pa.table({"id": pa.array([1, 2, 3])})
dataset = lance.write_dataset(table, "ids")
dataset.alter_columns({"path": "id", "name": "new_id"})
dataset.to_table().to_pandas()
```


This applies to nested columns. To reference nested columns, use a dot (`.`) to separate the nested levels. For example:

```Python
data = [{"meta": {"id": 1, "name": "Alice"}},{"meta": {"id": 2, "name": "Bob"}},]
dataset = lance.write_dataset(data, "nested_rename")
dataset.alter_columns({"path": "meta.id", "name": "new_id"})
```


```Plain
  meta
0  {"new_id": 1, "name": "Alice"}
1  {"new_id": 2, "name": "Bob"}
```


<span id="aaa731a5"></span>
##### Change column data types

In addition to renaming columns, you can also use the `lance.LanceDataset.alter_columns()` method to change column data types. This requires rewriting new data files for the column, but does not require rewriting other columns.

**Important**

If a column has an index, changing the column type will cause the index to be discarded.

This method can be used to change the vector type of a column. For example, you can change a float32 embedding column to a float16 column to save disk space, but this will reduce precision:

```Python
import lance
import pyarrow as pa
import numpy as np
table = pa.table({"id": pa.array([1, 2, 3]),"embedding": pa.FixedShapeTensorArray.from_numpy_ndarray(
       np.random.rand(3, 128).astype("float32"))})
dataset = lance.write_dataset(table, "embeddings")
dataset.alter_columns({"path": "embedding","type": pa.list_(pa.float16(), 128)})
dataset.schema()
```


```Plain
id: int64
embedding: fixed_size_list<item: float16, 128>
```


<span id="59bd59c1"></span>
##### Add new columns

You can use the `lance.LanceDataset.add_columns()` method to add new columns and populate data in a single operation. There are two ways to specify how to populate new columns: first, provide a SQL expression for each new column; second, provide a function to generate new column data.

SQL expressions can be standalone expressions or reference existing columns. You can use SQL literal values to set a value for all existing rows.

```Python
import lance
import pyarrow as pa
table = pa.table({"name": pa.array(["Alice", "Bob", "Carla"])})
dataset = lance.write_dataset(table, "names")
dataset.add_columns({"hash": "sha256(name)","status": "'active'",})
dataset.to_table().to_pandas()
```


```Plain
    name         hash...   status
0  Alice  3bc51062973c...  active
1    Bob  cd9fb1e148cc...  active
2  Carla  ad8d83ffd82b...  active
```


You can also provide a Python function to generate new column data. This can be used to compute new embedding columns. This function should accept a PyArrow RecordBatch and return a PyArrow RecordBatch or Pandas DataFrame. The function will be called once for each batch in the dataset.

If the function is computationally expensive and may fail, it is recommended to set a checkpoint file in the UDF. This checkpoint file saves the state of the UDF after each invocation, so that if the UDF fails, it can be restarted from the last checkpoint. Caution: This file can become quite large because it needs to store unsaved results for up to the entire data file.

```Python
import lance
import pyarrow as pa
import numpy as np
table = pa.table({"id": pa.array([1, 2, 3])})
dataset = lance.write_dataset(table, "ids")

@lance.batch_udf(checkpoint_file="embedding_checkpoint.sqlite")
def add_random_vector(batch):
    embeddings = np.random.rand(batch.num_rows, 128).astype("float32")
    return pd.DataFrame({"embedding": embeddings})
dataset.add_columns(add_random_vector)
```


<span id="e87a8396"></span>
##### Add new columns using merge

If you have already precomputed one or more new columns, you can use the `lance.LanceDataset.merge()` method to add them to an existing dataset. This allows you to populate additional columns without needing to rewrite the entire dataset.

To use the `merge` method, provide a new dataset containing the columns to be added, as well as the column name used to join the new data with the existing dataset.

For example, suppose we have a dataset containing embeddings and IDs:

```Python
import lance
import pyarrow as pa
import numpy as np
table = pa.table({"id": pa.array([1, 2, 3]),"embedding": pa.array([np.array([1, 2, 3]), np.array([4, 5, 6]),
                          np.array([7, 8, 9])])})
dataset = lance.write_dataset(table, "embeddings")
```


Now, if you want to add a label column that has already been generated, you can do so by merging a new table:

```Python
new_data = pa.table({"id": pa.array([1, 2, 3]),"label": pa.array(["horse", "rabbit", "cat"])})
dataset.merge(new_data, "id")
dataset.to_table().to_pandas()
```


```Plain
   id  embedding   label
0   1  [1, 2, 3]   horse
1   2  [4, 5, 6]  rabbit
2   3  [7, 8, 9]     cat
```


<span id="e5c7faa5"></span>
##### Delete columns

Finally, you can use the `lance.LanceDataset.drop_columns()` method to delete columns from the dataset. This is a metadata\-only operation and does not delete data from disk. This makes it extremely fast.

```Python
import lance
import pyarrow as pa
table = pa.table({"id": pa.array([1, 2, 3]),"name": pa.array(["Alice", "Bob", "Carla"])})
dataset = lance.write_dataset(table, "names")
dataset.drop_columns(["name"])
dataset.schema()
```


To actually delete data from disk, you must rewrite the file to exclude the columns and then delete the old file. This can be accomplished by running `lance.dataset.DatasetOptimizer.compact_files()` followed by `lance.LanceDataset.cleanup_old_versions()`.

<span id="2dcd6a42"></span>
### Version management

Rows can be appended:

```Python
df = pd.DataFrame({"a": [10]})
tbl = pa.Table.from_pandas(df)
dataset = lance.write_dataset(tbl, "/tmp/test.lance", mode="append")
dataset.to_table().to_pandas()
```


Data can be overwritten to create a new version:

```Python
df = pd.DataFrame({"a": [50, 100]})
tbl = pa.Table.from_pandas(df)
dataset = lance.write_dataset(tbl, "/tmp/test.lance", mode="overwrite")
```


```Python
dataset.to_table().to_pandas()
```


Old versions still exist:

```Python
[{'version': 1,'timestamp': datetime.datetime(2024, 8, 15, 21, 22, 31, 453453),'metadata': {}},{'version': 2,'timestamp': datetime.datetime(2024, 8, 15, 21, 22, 35, 475152),'metadata': {}},{'version': 3,'timestamp': datetime.datetime(2024, 8, 15, 21, 22, 45, 32922),'metadata': {}}]
```


```Python
lance.dataset('/tmp/test.lance', version=1).to_table().to_pandas()
```


```Python
lance.dataset('/tmp/test.lance', version=2).to_table().to_pandas()
```


Labels can be created:

```Python
dataset.tags.create("stable", 2)
dataset.tags.create("nightly", 3)
dataset.tags.list()
```


```Python
{'nightly': {'version': 3, 'manifest_size': 628},'stable': {'version': 2, 'manifest_size': 684}}
```


Labels can be checked out:

```Python
lance.dataset('/tmp/test.lance', version="stable").to_table().to_pandas()
```


<span id="63a261e0"></span>
### Vector queries

<span id="fb922a4b"></span>
#### Prepare vector data

In this tutorial, we will use the Sift 1M dataset:


* Download `ANN_SIFT1M` from the following address: [http://corpus-texmex.irisa.fr/](http://corpus-texmex.irisa.fr/)

* The direct link should be: `ftp://ftp.irisa.fr/local/texmex/corpus/sift.tar.gz`

* Download and extract the tarball


```Python
rm -rf sift* vec_data.lance
wget ftp://ftp.irisa.fr/local/texmex/corpus/sift.tar.gz
tar -xzf sift.tar.gz
```


Convert it to Lance:

```Python
from lance.vector import vec_to_table
import lance
import numpy as np
import struct
uri = "vec_data.lance"
with open("sift/sift_base.fvecs", mode="rb") as fobj:
    buf = fobj.read()
    data = np.array(struct.unpack("<128000000f", buf[4 : 4 + 4 * 1000000 * 128])).reshape((1000000, 128))
    dd = dict(zip(range(1000000), data))
table = vec_to_table(dd)
lance.write_dataset(table, uri, max_rows_per_group=8192, max_rows_per_file=1024*1024)
```


Verify successful dataset write

<span id="ffa0047d"></span>
#### KNN query

Randomly sample 100 vectors as query vectors:

Invoke nearest neighbor (no ANN index here):

```Python
import time
start = time.time()
tbl = sift1m.to_table(columns=["id"], nearest={"column": "vector", "q": samples[0], "k": 10})
end = time.time()
```


<span id="92e354bf"></span>
### Compact optimization

Over time, certain operations can lead to suboptimal Lance dataset layouts. For example, multiple small batch appends can result in a large number of small fragments. Alternatively, deleting many rows can slow down queries because the deleted rows need to be filtered out.

To address these issues, Lance provides methods for optimizing dataset layout.

You can rewrite data files using the `lance.dataset.DatasetOptimizer.compact_files()` method to reduce the number of files. When the `target_rows_per_fragment` parameter is passed, Lance skips fragments that already exceed this number of rows and rewrites the others. Fragments are merged based on their fragment IDs, so the inherent order of the data is preserved.

**Caution**

Compaction creates a new version of the table. It does not delete the old versions of the table or the files they reference.

```Python
import lance
dataset = lance.dataset("./alice_and_bob.lance")
dataset.optimize.compact_files(target_rows_per_fragment=1024 * 1024)
```


During compaction, Lance can also remove deleted rows. Rewritten fragments will no longer have delete files. This can improve scan performance because soft\-deleted rows do not need to be skipped during scanning.

When files are rewritten, the original row addresses become invalid. This means the affected files no longer belong to any ANN index (if they did previously). Therefore, it is recommended to rewrite files before rebuilding the index.

<span id="afd2a357"></span>
### Object storage configuration

Lance supports object storage, such as AWS S3 (and compatible storage), Azure Blob Storage, and Google Cloud Storage. The object storage to use is determined by the URI scheme of the dataset path. For example, `s3://bucket/path` will use S3. For the S3 configuration of Volcano TOS, refer to [Access Lance data on TOS using the Lance Python SDK](https://docs.byteplus.com/docs/undefined/69a968df8a3fb00506e9dcb0).
