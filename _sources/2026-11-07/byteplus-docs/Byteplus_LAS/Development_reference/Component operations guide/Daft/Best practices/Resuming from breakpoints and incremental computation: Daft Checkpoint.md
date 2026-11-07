---
title: "Resuming from breakpoints and incremental computation: Daft Checkpoint"
product: "Lake AI Service"
product_code: "Byteplus_LAS"
source: "https://docs.byteplus.com/en/docs/Byteplus_LAS/Daft_Checkpoint"
---

The Daft engine of BytePlus LAS AI provides the Checkpoint feature, enabling 'resuming from breakpoints' and 'incremental computation' in production environments for batch data processing. It leverages previously written results for deduplication, filtering out unnecessary computations. This article introduces the details and practical usage of the Checkpoint feature based on the Daft engine.

<span id="4443ac2f"></span>
# Background information

When using distributed frameworks to preprocess multimodal data (such as images, text, audio, video, and more), the workflow often fails and terminates due to various reasons, including limited resources, unstable environments, or unreliable code. If a failure occurs during the intermediate process, restarting typically means the entire workflow runs from the beginning, causing **processed** data from the previous run to be executed again. This repeated computation results in significant waste of resources and time.

Therefore, based on the Daft engine, BytePlus LAS AI offers the Checkpoint feature: enabling 'resuming from breakpoints' and 'incremental computation' in production environments for batch data writing. For example, if the first run only processes and writes part of the data before failing and terminating, subsequent runs will only process the remaining portion, avoiding duplication, ensuring idempotency, and saving both cost and time.

<span id="9246546e"></span>
## Caution and limitations


|Breakdown |Notes |
|---|---|
|Data source requirements |* Currently, only the Checkpoint feature for a **single source** dataframe is supported.<br><br>* For dataframes with multiple data sources (typically resulting from `join`, `union`, `intersect`, or `concat` operations), you can first run `df.collect()` to materialize the data and cache it in memory. The newly materialized dataframe will have only one data source (single source), enabling support for Checkpoint. |
|Runtime requirements |Currently, the Checkpoint feature is only supported in the distributed mode of Daft on Ray and is not yet available for Daft standalone mode. |
|Data format requirements |Consistent Checkpoint functionality is provided for writing to CSV, Parquet, and JSON formats. |


<span id="72deeb09"></span>
# Instructions for use

<span id="e4fe820a"></span>
## Usage

```Python
df = daft.read_parquet(source_dir)

# Intermediate processing flow
df = df.with_column(...)
df = df.with_column(...)

# Configure checkpoint parameters
checkpoint_config = {
    "key_column": "object_key",
}

# Write
df.write_parquet(dest_dir, checkpoint_config=checkpoint_config)
```


<span id="bc3ec8d6"></span>
## Configure checkpoint


|Parameters |Logic description |
|---|---|
|checkpoint_config |When using the checkpoint feature, you must first configure checkpoint_config (see the [Checkpoint parameter description](https://docs.byteplus.com/docs/Byteplus_LAS/92530#20360275)section below for specific configuration parameters).<br><br><br>* If the checkpoint configuration is enabled when writing files (such as `df.write_parquet`), when the daft task runs again, only **data not previously written** (that is, data not yet processed) will be appended, while data already written to the target location (that is, already processed) will be skipped, avoiding duplicate processing.<br><br>* Checkpoint must be set in the dataframe's write_api (such as `write_parquet`). |


<span id="20360275"></span>
## Checkpoint parameter description


|Parameters |Required |Description |
|---|---|---|
|key_column |Yes |* The column specified by the `key_column` parameter is used as the deduplication primary key, which must remain unique across the entire dataset.<br><br>* The recommended data types for the unique key are simple primitive types, such as `string` or `int`. |
|num_buckets |No |* Set the number of load balancing buckets for checkpoint processing to control memory pressure on a single machine. The larger the `num_buckets`, the lower the memory pressure on a single machine.<br><br>* Default value: 4. It is recommended to keep the default value. If there are billions or even tens of billions of records, you can increase `num_buckets` as needed to reduce memory pressure on a single machine. |
|num_cpus |No |* Set the number of CPUs for each checkpoint load balancing bucket.<br><br>* Default value is 1.0; it is recommended to keep the default value. |


<span id="1cb04184"></span>
# Practical demo

<span id="38f607c1"></span>
## Demo 1: Resuming from breakpoints using the primary key column id (using Parquet as an example)

The following demonstrates how Daft's `checkpoint` feature automatically skips processed records and only processes remaining records when retrying a failed Daft task.


* Applicable scenario: A dataset with a primary key (unique ID).

* Requirement for resuming from breakpoints: When data processing fails, subsequent runs only process the remaining **data**, avoiding duplication.

* Core configuration: Use `checkpoint_config={"key_column": "id"}`.


The complete code example is as follows.

```Python
from __future__ import annotations

import shutil
from pathlib import Path

import daft
from daft import col, set_runner_ray


def init_runner() -> None:
    try:
        set_runner_ray(noop_if_initialized=True)
        print("[info] Ray runner initialized")
    except Exception as e:
        print(f"[warn] Fallback to default runner: {e}")


def example_checkpoint_with_id() -> None:
    """
    Demonstrate Daft's checkpoint incremental write function:
    - Use the'id 'column as the unique key to avoid duplicate writes.
    - first write id=0..50(simulated historical data)
    - second write id=0..99(Simulate full pull)
    - Verify that the final result is 100 unique records.
    Note: The checkpoint function relies on the Ray executor.
    """
    # Construct test data
    df_all = daft.from_pydict({"id": list(range(100)), "val": [f"v{i}" for i in range(100)]})
    df_seed = df_all.where(col("id") <= 50)

    # Set the output path (clean before each run)
    dest = Path("/tmp/ckpt_demo_parquet_id")
    if dest.exists():
        shutil.rmtree(dest)
    dest.mkdir(parents=True, exist_ok=True)

    # Configure checkpoint: use 'id' as the unique key
    ck = {"key_column": "id"}

    # First write: seed data (id <= 50)
    df_seed.write_parquet(str(dest), write_mode="append", checkpoint_config=ck)

    # Second write: full data (id 0~99), checkpoint automatically deduplicates
    df_all.write_parquet(str(dest), write_mode="append", checkpoint_config=ck)

    # Verify results
    out_df = daft.read_parquet(str(dest))
    ids = out_df.select("id").to_pydict()["id"]
    print("[result] rows:", len(ids), "unique_ids:", len(set(ids)))
    print("[result] has_all_ids_0_to_99:", set(ids) == set(range(100)))


if __name__ == "__main__":
    init_runner()
    example_checkpoint_with_id()
```


<span id="3805a101"></span>
## Demo 2: Incremental computation based on file path

The following demonstrates how Daft's `checkpoint` feature avoids repeated processing in incremental computation scenarios, only processing new files and skipping files that have already been processed.


* Applicable scenarios: A continuously growing file directory (such as logs, images, or audio), where only newly added files are processed each time.

* Incremental requirement: Avoid processing files that have already been handled.

* Core configuration: Use `checkpoint_config={"key_column": "path"}`, with the file path as the unique identifier.


The complete code example is as follows.

```Python
from __future__ import annotations

import shutil
from pathlib import Path

import daft
from daft import set_runner_ray


def init_runner() -> None:
    try:
        set_runner_ray(noop_if_initialized=True)
        print("[info] Ray runner initialized")
    except Exception as e:
        print(f"[warn] Fallback to default runner: {e}")


def example_checkpoint_with_path() -> None:
    """
    Demonstrates incremental writing of checkpoints based on file paths:
    1. Create 10 initial files(file_0.txt ~ file_9.txt)
    2. Add 5 new files (file_10.txt ~ file_14.txt)；
    3. Rescan all files, automatically skip existing paths through checkpoints
    4. Validation ultimately consists of 15 unique paths with no duplicates.
    Note: The checkpoint function relies on the Ray executor.
    """
    src_dir = Path("/tmp/glob_src")
    dest = Path("/tmp/ckpt_demo_parquet_path")

    # Clean old data to ensure repeatable runs
    if src_dir.exists():
        shutil.rmtree(src_dir)
    if dest.exists():
        shutil.rmtree(dest)
    src_dir.mkdir(parents=True)
    dest.mkdir(parents=True)

    # Step 1: Generate initial files (0-9)
    for i in range(10):
        (src_dir / f"file_{i}.txt").write_text("x" * i)

    df_initial = daft.from_glob_path(str(src_dir / "*.txt"))
    ck = {"key_column": "path"}
    df_initial.write_parquet(str(dest), write_mode="append", checkpoint_config=ck)

    # Step 2: Add files (10-14)
    for i in range(10, 15):
        (src_dir / f"file_{i}.txt").write_text("x" * i)

    # Step 3: Rescan all files, checkpoint automatically deduplicates
    df_full = daft.from_glob_path(str(src_dir / "*.txt"))
    df_full.write_parquet(str(dest), write_mode="append", checkpoint_config=ck)

    # Step 4: Verify results
    out_df = daft.read_parquet(str(dest))
    paths = out_df.select("path").to_pydict()["path"]
    print("[result] total rows:", len(paths), "unique paths:", len(set(paths)))

    expected_paths = {str(src_dir / f"file_{i}.txt") for i in range(15)}
    print("[result] has_all_expected_paths:", set(paths) == expected_paths)


if __name__ == "__main__":
    init_runner()
    example_checkpoint_with_path()
```
