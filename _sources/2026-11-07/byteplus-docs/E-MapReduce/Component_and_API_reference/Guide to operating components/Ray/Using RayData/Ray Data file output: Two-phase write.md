---
title: "Ray Data file output: Two-phase write"
product: "BytePlus EMR"
product_code: "E-MapReduce"
source: "https://docs.byteplus.com/en/docs/E-MapReduce/ray_data_file_output_two-phase_write"
---

EMR Ray has added a **two\-phase write (Two\-phase write)**  option to the Ray Data file output capability. When enabled, Ray Data first writes data to a temporary directory under the target path. After all data is written, the files are moved to the final directory, thereby improving the reliability of file output. This article provides the functional logic and usage examples of the **two\-phase write** feature.

<span id="3b6a247e"></span>
# Context

When using Ray Data for offline data processing, a common output method is to write results to object storage or distributed file systems (such as S3/TOS, HDFS, parallel file systems, and so on) as input for subsequent computation or training.

In production environments, the output pipeline often faces the following issues:


* During job execution, failures, retries, or interruptions (such as node failures, resource reclamation, network jitter, and so on) may occur, resulting in **incomplete files** or **partially written files** in the target directory, which may be misread by downstream tasks.

* When using overwrite mode (`mode=SaveMode.OVERWRITE`), the traditional logic is often "delete old data first, then write new data." If the write process fails or takes a long time, there will be a window during which the target path has **no available data** or **incomplete data**.


<span id="1a5dbf56"></span>
# Feature description

EMR Ray has added a **two\-phase write (Two\-phase write)**  option to the Ray Data file output capability. When enabled, Ray Data first writes data to a temporary directory under the target path. After all data is written, the files are moved to the final directory, thereby improving the reliability of file output.

This capability is provided as the Python API parameter `two_phase_write`, and applies to Ray Data file output interfaces such as `Dataset.write_parquet`, `Dataset.write_csv`, `Dataset.write_json`, `Dataset.write_images`, and more.

<span id="79632b0f"></span>
### Output process

After enabling `two_phase_write=True`, the Ray Data output process is as follows:


* **Phase 1: Write to temporary directory**. A temporary staging directory (such as `.tmp_staging_dir_<uuid>`) is created under the target directory, and all output files are first written to this temporary directory.

* **Phase 2: Commit to final directory**. After the write operation is completed, move the files in the temporary directory to the final target path one by one, and clean up the temporary directory.


In the overwrite write (`mode=SaveMode.OVERWRITE`) scenario, the two\-phase write protocol postpones the "delete old data" action to the commit phase, avoiding the data gap caused by "delete first, then write", thereby reducing the impact of the overwrite process on downstream reads.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip"><code>two_phase_write</code> provides <strong>file\-level</strong> write atomicity: each file will not appear in the target location until it is moved to the final directory. The commit phase uses a file\-by\-file move approach. If an exception occurs during the commit process, the target directory may be in a state where "some files are committed, some are not".</div>


<span id="1db1e867"></span>
### Parameter note


|Parameter |Note |Default value |
|---|---|---|
|`two_phase_write` |Whether to enable the two\-phase write protocol. Once enabled, data is first written to the temporary directory and then moved to the final directory, improving the reliability of the write process and, to some extent, enhancing the availability of overwrite scenarios. |`False` |


<span id="50ade75d"></span>
# important notes


* `two_phase_write` is disabled by default and must be explicitly enabled in the write interface.

* Once enabled, a temporary directory (`.tmp_staging_dir_<uuid>`) will be created under the target path. It will be automatically cleaned up upon normal completion; if the job is interrupted abnormally, the temporary directory may remain. After confirming that no tasks are using it, you can manually clean it up.

* For some remote file systems, the `move` operation may be implemented as "copy + delete", which introduces additional I/O overhead and may increase the overall write time. It is recommended to enable this feature after evaluation in critical workflows (overwrite write, downstream strong dependency on write consistency).


<span id="f21ff616"></span>
# Usage examples

<span id="f39c3455"></span>
## Example 1: Overwrite write usage example

```Python
#!/usr/bin/env python3
"""Ray Data Two-Phase Write to TOS Example

Use Ray Data with tosfs to write data to TOS (Tinder Object Storage)
with two-phase write for atomicity.
"""

import ray
import ray.data as rd
from ray.data import SaveMode
from tosfs.core import TosFileSystem

# Initialize TOS filesystem
fs = TosFileSystem(
    endpoint_url="https://tos-cn-beijing.ivolces.com",
    key='your-access-key',        # Replace with your access key
    secret='your-secret-key',     # Replace with your secret key
    region="cn-beijing"
)

# Initialize Ray
ray.init()

# Create sample data
data = [
    {"id": 1, "name": "Alice", "score": 95.5},
    {"id": 2, "name": "Bob", "score": 87.0},
    {"id": 3, "name": "Charlie", "score": 92.5},
]
ds = rd.from_items(data)

# Write to TOS with two-phase write
tos_path = "tos://your-bucket/output/data"

# Write to CSV
ds.write_csv(tos_path, filesystem=fs, mode=SaveMode.OVERWRITE, two_phase_write=True)

# Write to Parquet
# ds.write_parquet(tos_path, filesystem=fs, two_phase_write=True)

# Read back and verify
read_ds = rd.read_csv(tos_path, filesystem=fs)
print(f"Total rows written to TOS: {read_ds.count()}")

ray.shutdown()
```


<span id="4e15951b"></span>
## Example 2: Append write usage example

```Python
#!/usr/bin/env python3
"""Ray Data Two-Phase Write Example

Use two-phase write to ensure atomic data writing.
Data is first written to a temporary directory and then moved to the final location.
"""

import ray
import ray.data as rd

ray.init()

data = [
    {"id": 1, "name": "Alice", "score": 95.5},
    {"id": 2, "name": "Bob", "score": 87.0},
    {"id": 3, "name": "Charlie", "score": 92.5},
]
ds = rd.from_items(data)

ds.write_csv("/tmp/output/csv", two_phase_write=True)
ds.write_json("/tmp/output/json", two_phase_write=True)
ds.write_parquet("/tmp/output/parquet", two_phase_write=True)

print(f"CSV rows: {rd.read_csv('/tmp/output/csv').count()}")
print(f"JSON rows: {rd.read_json('/tmp/output/json').count()}")
print(f"Parquet rows: {rd.read_parquet('/tmp/output/parquet').count()}")

ray.shutdown()
```
