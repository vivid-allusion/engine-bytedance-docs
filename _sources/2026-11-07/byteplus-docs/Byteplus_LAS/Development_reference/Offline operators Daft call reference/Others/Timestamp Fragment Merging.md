---
title: "Timestamp Fragment Merging"
product: "Lake AI Service"
product_code: "Byteplus_LAS"
source: "https://docs.byteplus.com/en/docs/Byteplus_LAS/Timestamp_Fragment_Merging"
---

<span id="operator-introduction"></span>
# Operator introduction

<span id="description"></span>
## Description

**Timestamp Merging Operator \- Normalization, Merging, and Splitting of Second\-level Intervals**

<span id="core-capabilities"></span>
## Core Capabilities


* Normalization and Sorting: Unify input format to (start, end) floating\-point seconds and validate legality.

* Pre\-merge Small Gaps: Merge overlapping or adjacent segments with gaps ≤ threshold (pre_merge_gap_seconds).

* Longest Silence First Splitting: Split at the longest silence first to ensure each segment's span does not exceed max_span_seconds.

* Forced Chunking (Optional): Split overlong segments into fixed windows to ensure each segment's length does not exceed the upper limit (enforce_chunking).


<span id="recommended-practices"></span>
## Recommended Practices


* When VAD output contains short silences and semantic continuity is desired, prioritize using "Longest Silence First Splitting" over simple sequential chunking.

* If the business requires strict segment length limits, enable enforce_chunking to get continuous window splitting results.

* Set pre_merge_gap_seconds to a value slightly larger than the typical duration of noise\-induced silences (e.g., 0.2–1.0 seconds).


<span id="output-format"></span>
## Output Format


* Each row returns List[List[float]], where elements are [start, end] (unit: seconds), sorted by start time in ascending order; the output column type is List[List[float32]].


<span id="processing-flow"></span>
## Processing Flow


1. Normalization: Add a unified offset start_time, sort, and validate legality.

2. Pre\-merging: Merge overlapping and small\-gap (≤ pre_merge_gap_seconds) segments.

3. Longest Silence First Splitting: Split at the longest silence to ensure each segment's span ≤ max_span_seconds; no requirement for a single segment's time range to be ≤ max_span_seconds.

4. (Optional) Forced Chunking: When enforce_chunking=True, split into continuous fixed windows to ensure the time length ≤ max_span_seconds.


<span id="daft-call"></span>
# Daft call

<span id="operator-parameters"></span>
## Operator parameters

<span id="input"></span>
## Input


|Input column name |Note |
|---|---|
|timestamps |Each element is a 2D list of floats (unit: seconds), formatted as [[start, end], ...]. |


<span id="output"></span>
## Output

Each element is a merged 2D list of floats (unit: seconds), type is List[List[float32]]; invalid rows return None.

<span id="parameters"></span>
## Parameters

If a parameter does not have a default value, it is a required parameter.


|Parameter name |Type |Default value |Description |
|---|---|---|---|
|start_time |float |0.0 |Start offset applied to each timestamp (seconds). Default value: 0 |
|pre_merge_gap_seconds |float |0.0 |Threshold for pre\-merging small gaps (seconds). When the interval between adjacent segments is less than or equal to this value, they are merged into a larger segment. Default value: 0 |
|max_span_seconds |float |20.0 |Maximum allowed span for merging segments (seconds). Default value: 20 |
|enforce_chunking |bool |False |Whether to enforce continuous chunking for overlong segments. When True, continuous chunking is performed according to max_span_seconds length. Default value: False |


<span id="examples"></span>
## Examples

The following code shows how to use daft to run the operator for normalization operations such as merging and splitting timestamp lists.

```python
from __future__ import annotations

import os

import daft
from daft import col
from daft.las.functions.other.timestamps_merge import TimestampsMerge
from daft.las.functions.udf import las_udf

if __name__ == "__main__":

    if os.getenv("DAFT_RUNNER", "native") == "ray":
        import logging

        import ray

        def configure_logging():
            logging.basicConfig(
                level=logging.INFO,
                format="%(asctime)s - %(name)s - %(levelname)s - %(message)s",
                datefmt="%Y-%m-%d %H:%M:%S.%s".format(),
            )
            logging.getLogger("tracing.span").setLevel(logging.WARNING)
            logging.getLogger("daft_io.stats").setLevel(logging.WARNING)
            logging.getLogger("DaftStatisticsManager").setLevel(logging.WARNING)
            logging.getLogger("DaftFlotillaScheduler").setLevel(logging.WARNING)
            logging.getLogger("DaftFlotillaDispatcher").setLevel(logging.WARNING)

        ray.init(dashboard_host="0.0.0.0", runtime_env={"worker_process_setup_hook": configure_logging})
        daft.set_runner_ray()
    daft.set_execution_config(actor_udf_ready_timeout=600)
    daft.set_execution_config(min_cpu_per_task=0)

    samples = {"timestamps": [[[0.0, 4.34], [5.50, 7.12], [8.10, 8.34], [8.50, 10.12]]]}
    ds = daft.from_pydict(samples)

    start_time = 0.0
    pre_merge_gap_seconds = 0.5
    max_span_seconds = 10.0
    enforce_chunking = True
    ds = ds.with_column(
        "timestamps_merged",
        las_udf(
            TimestampsMerge,
            construct_args={
                "start_time": start_time,
                "pre_merge_gap_seconds": pre_merge_gap_seconds,
                "max_span_seconds": max_span_seconds,
                "enforce_chunking": enforce_chunking,
            },
            num_cpus=1,
            batch_size=1,
            concurrency=1,
        )(col("timestamps")),
    )
    ds.show()

    # ╭────────────────────────────────┬───────────────────────────╮
    # │ timestamps                     ┆ timestamps_merged         │
    # │ ---                            ┆ ---                       │
    # │ List[List[Float64]]            ┆ List[List[Float32]]       │
    # ╞════════════════════════════════╪═══════════════════════════╡
    # │ [[0, 4.34], [5.5, 7.12], [8.1… ┆ [[0, 4.34], [5.5, 10.12]] │
    # ╰────────────────────────────────┴───────────────────────────╯
```
