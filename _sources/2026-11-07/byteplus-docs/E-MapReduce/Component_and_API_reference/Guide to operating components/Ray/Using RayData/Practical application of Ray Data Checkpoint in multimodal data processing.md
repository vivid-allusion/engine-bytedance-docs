---
title: "Practical application of Ray Data Checkpoint in multimodal data processing"
product: "BytePlus EMR"
product_code: "E-MapReduce"
source: "https://docs.byteplus.com/en/docs/E-MapReduce/Practical_application_of_Ray_Data_Checkpoint_in_multimodal_data_processing"
---

<span id="6c760062"></span>
## Background

In the preprocessing workflow for multimodal data (such as images, text, audio, video, and more), GPU\-based data processing and inference are typically involved. However, such processing workflows usually have the following characteristics:


* Ultra\-large\-scale datasets: When a dataset contains millions or even billions of samples (files), the processing time becomes extremely long, the probability of failure increases, and the cost of repeated processing becomes prohibitively high.

* Time\-consuming preprocessing tasks: Even if the dataset is not particularly large, the preprocessing of a single sample can be extremely complex and time\-consuming (for example, high\-quality video frame extraction, complex speech feature transformation, or high\-precision transformation of large images), resulting in an overall workflow that can take several hours or more.

* Resource constraints or unstable environments:

   * Shared GPU clusters (with the possibility of preemption).

   * Using Spot instances (low cost but may be terminated at any time).

   * Local development environments (where processing may be interrupted due to debugging, system updates, and other factors).

* Complex and variable preprocessing workflows: The workflow itself may not be robust enough, making it prone to edge cases or unknown errors.

* Automated pipelines: In unattended automated data processing pipelines, the workflow is required to have the ability to automatically recover from errors.

* Heterogeneous multimodal processing: Processing workflows for different types of data (such as image + text + audio) may involve multiple steps and toolchains, increasing the potential points of failure.


Once the above processing workflows fail at an intermediate stage, restarting often requires the entire workflow to run from the beginning, which inevitably results in previously successfully processed data being re\-executed. This repeated processing not only represents a tremendous waste of computing resources—consuming valuable GPU/CPU computation time and increasing unnecessary resource overhead—but also means that valuable time is occupied ineffectively. More importantly, it significantly slows down the progress of downstream tasks (such as critical model training or data evaluation stages), resulting in a snowball effect that greatly reduces the efficiency of the entire data processing chain. The issues of resource waste and time delays urgently need to be addressed.

<span id="0a345780"></span>
## Note

To address the above issues, EMR has developed the Checkpoint feature in the multimodal data preprocessing pipeline. The Checkpoint feature is a mechanism that can record data processing progress and save the status of completed tasks. This mechanism achieves its core capability—skipping completed work and processing only unfinished parts during recovery after failure—by persistently storing 'successfully processed data'. This is especially important in scenarios that rely on GPUs for high\-cost multimodal data processing, such as image enhancement, video frame extraction, cross\-modal feature alignment, and so on. Its core value lies in significantly saving computing resources and time costs, enhancing the reliability and robustness of the processing workflow, and improving development and research efficiency.

<span id="a05fa756"></span>
### Note

When configuring checkpoint\-related settings during Ray Data output, processed data will be automatically recorded at the specified checkpoint location during data processing. When a task fails and restarts, the Read phase will automatically filter out processed data, and only unprocessed data will enter subsequent processing workflows.

```Python

checkpoint_config = {
    "enabled": True,
    "num_buckets": 2,
    "key_columns": "id",
    "storage": {
        "type":"fs",
        "check_ready_timeout": 300,
        "fs_options": {
            "path": "tos://bucket_name/checkpointdata/",
            "key": "xxx",
            "secret": "yyy==",
            "endpoint_url": 'http://tos-cn-beijing.ivolces.com',
            "region": 'cn-beijing',
            "max_items_per_file": 10000,
        },
        "remote_args": {
            "num_cpus":1,
        },
    }
  }
ds.write_parquet(dest_path, checkpoint_config=checkpoint_config)
```


Supported data sources: Any data source. This can include files such as images, data files such as JSON, or relational databases such as SQL.

Supported output formats: Supports file output formats such as CSV, JSON, and Parquet.

<span id="78acac3d"></span>
### Note


|Parameters |Note |Default value |
|---|---|---|
|enabled |Whether to enable the checkpoint feature |False |
|num_buckets |The number of Actors that handle checkpoints. Data will be bucketed according to the number of buckets (num_buckets), and each bucket will only process a portion of the data corresponding to it. When processing large\-scale data, each Actor will handle a portion of the data. |1 |
|key_columns |The column name of the unique key in the data |None |
|storage.type |Currently fixed as fs, representing the fileSystem storage backend |fs |
|storage.check_ready_timeout |When the task restarts, the timeout for loading checkpoint information, in seconds, of type float, and set according to the amount of data processed. Loading 5 million long\-type data takes about 1 minute, |500 |
|storage.fs_options.path |The file path for storing checkpoint information, which can be a local path or an object storage service (TOS) path. When using a local path, ensure that all nodes can access the same path, such as when mounting the Volcano Engine Parallel File System (vePFS). |None |
|storage.fs_options.max_items_per_file |The maximum number of data entries saved in a single checkpoint file |100000 |
|Other configurations under storage.fs_options |Other configurations under storage.fs_options can be used to configure TosFileSystem\-related settings, supporting key, secret, endpoint_url, region, and more |None |
|storage.remote_args.x |The resources used by the Actor that handles checkpoints. Parameter settings must follow Ray's Actor resource configuration pattern. x can be num_cpus and so on. | |


<span id="dc3ca845"></span>
### Optimal parameter configuration


|Data scale (amount of data in key_column) |Recommended parameter configuration |Note |
|---|---|---|
|512M |num_buckets = 4 |When the unique key is of type long, the number of supported data entries is about 170 million. For other types, calculate based on the size of a single data entry. |
|1G |num_buckets = 8 |The calculation formula for the number of supported data entries is the same as above |
|Above 1G |Configure proportionally | |


<span id="b462c152"></span>
## Usage examples

<span id="b52a075d"></span>
### Record\-level usage example

When processing multimodal data at the row level, the unique key in the data (such as id) will be recorded in the checkpoint. When the task fails and is executed again, ids that have already been processed will be skipped.

```Python
import ray
import pandas as pd

ray.init()

from tosfs.core import TosFileSystem
fs = TosFileSystem(
    endpoint_url="https://tos-cn-beijing.ivolces.com",
    key='xxx',
    secret='yyy==',
    region="cn-beijing"
)

ds = ray.data.read_parquet("tos://bucket_name/source_data/", filesystem=fs)

dest_path = "tos://bucket_name/dest_data/"

checkpoint_config = {
    "enabled": True,
    "num_buckets": 2,
    "key_columns": "id",
    "storage": {
        "type":"fs",
        "check_ready_timeout": 300,
        "fs_options": {
            "path": "tos://bucket_name/checkpointdata/",
            "key": "xxx",
            "secret": "yyy==",
            "endpoint_url": 'http://tos-cn-beijing.ivolces.com',
            "region": 'cn-beijing',
            "max_items_per_file": 10000,
        },
        "remote_args": {
            "num_cpus":1,
        },
    }
  }
# Write 1,234,567 rows of data
ds.limit(1234567).write_parquet(dest_path, checkpoint_config=checkpoint_config, filesystem=fs)
# Write the remaining data
ds.write_parquet(dest_path, checkpoint_config=checkpoint_config, filesystem=fs)
# No task data will be written, as all data has already been processed
ds.write_parquet(dest_path, checkpoint_config=checkpoint_config, filesystem=fs)
```


<span id="83f27847"></span>
### File\-level usage example

When processing multimodal data at the file level, the file path is used as the unique key, and the processing results are recorded. If the task fails and is re\-executed, files that have already been processed will be skipped.

```Python
import ray
import pandas as pd

ray.init()

from tosfs.core import TosFileSystem
fs = TosFileSystem(
    endpoint_url="https://tos-cn-beijing.ivolces.com",
    key='xxx',
    secret='yyy==',
    region="cn-beijing"
)

ds = ray.data.read_images("tos://bucket_name/image_data/", include_paths=True, filesystem=fs)

dest_path = "tos://bucket_name/dest_data/"

checkpoint_config = {
    "enabled": True,
    "num_buckets": 2,
    "key_columns": "path",
    "storage": {
        "type":"fs",
        "check_ready_timeout": 300,
        "fs_options": {
            "path": "tos://bucket_name/checkpointdata/",
            "key": "xxx",
            "secret": "yyy==",
            "endpoint_url": 'http://tos-cn-beijing.ivolces.com',
            "region": 'cn-beijing',
            "max_items_per_file": 10000,
        },
        "remote_args": {
            "num_cpus":1,
        },
    }
  }
# Write 1,234,567 rows of data
ds.limit(1234567).write_parquet(dest_path, checkpoint_config=checkpoint_config, filesystem=fs)
# Write the remaining data
ds.write_parquet(dest_path, checkpoint_config=checkpoint_config, filesystem=fs)
# No task data will be written, as all data has already been processed
ds.write_parquet(dest_path, checkpoint_config=checkpoint_config, filesystem=fs)
```
