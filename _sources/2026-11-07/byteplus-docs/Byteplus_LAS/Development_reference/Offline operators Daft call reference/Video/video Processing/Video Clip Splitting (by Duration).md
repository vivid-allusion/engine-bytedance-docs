---
title: "Video Clip Splitting (by Duration)"
product: "Lake AI Service"
product_code: "Byteplus_LAS"
source: "https://docs.byteplus.com/en/docs/Byteplus_LAS/Video-Clip-Splitting-Duration"
---

<span id="operator-introduction"></span>
# Operator introduction

<span id="description"></span>
## Description

**Video Segment Splitting Processor, Intelligent Division by Fixed Duration**

<span id="core-features"></span>
## Core Features:


* Split video by fixed second duration

* Support minimum duration filtering for remaining segments

* Support segment binary output or TOS storage

* Provide automatic format inference and customization


<span id="supported-formats"></span>
## Supported Formats:


* MP4 (.mp4)

* AVI (.avi)

* MOV (.mov)

* MKV (.mkv)

* Other common video formats


<span id="daft-call"></span>
# Daft call

<span id="operator-parameters"></span>
## Operator parameters

<span id="input"></span>
## Input


|Input column name |Note |
|---|---|
|video_paths |An array containing input video paths Default value: None |
|video_binaries |An array containing video binary data Default value: None |
|video_formats |An array containing input video formats (e.g., 'mp4', 'avi', etc.), which can provide format information when specifying video_binaries Default value: None |
|output_basenames |Optional; an array of output subdirectory names (file names) |


<span id="output"></span>
## Output

The processed struct fields include:


* segments: List of paths to the split video segments

* segments_binary: List of binary data of the split video segments

* video_format: List of formats of the split video segments


<span id="parameters"></span>
## Parameters

If a parameter does not have a default value, it is a required parameter.


|Parameter name |Type |Default value |Description |
|---|---|---|---|
|segment_duration |float |5.0 |Duration of each segment (in seconds), must be \>0 Default value:5.0 |
|min_segment_duration |float |0.0 |Remaining segments shorter than this value will be discarded (in seconds) Default value:0.0 |
|output_tos_dir |str | |TOS path to save video segments; if empty string, no upload will be performed Default value: "" |
|output_segments_binary |bool |False |Whether to output binary data of video segments Default value: False |
|output_video_format |str or None | |Globally specify the output video format (e.g., "mp4", "avi", etc.), which has higher priority than input file extension and video_format column |


<span id="examples"></span>
## Examples

The following code shows how to use Daft (suitable for distributed scenarios) to run the operator to split videos by duration.

```python
from __future__ import annotations

import os

import daft
from daft import col
from daft.las.functions.udf import las_udf
from daft.las.functions.video import VideoSplitByDuration

if __name__ == "__main__":

    # 更改完切分的视频会保存到指定的TOS路径下，因此，需要设置好环境变量以保证有权限写入TOS，包括：ACCESS_KEY,SECRET_KEY,TOS_ENDPOINT,TOS_REGION,TOS_TEST_DIR
    TOS_DIR = os.getenv("TOS_TEST_DIR", "tos_bucket")
    output_tos_dir = f"tos://{TOS_DIR}/video/video_split_by_duration"
    
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

    # 使用环境变量构建URL
    tos_dir_url = os.getenv("TOS_DIR_URL", "las-cn-beijing-public-online.tos-cn-beijing.volces.com")
    samples = {
        "video_path": [
            f"https://{tos_dir_url}/public/shared_video_dataset/sample.mp4"
        ]
    }

    ds = daft.from_pydict(samples)

    splitter = las_udf(
        VideoSplitByDuration,
        construct_args={
            "segment_duration": 60.0,
            "min_segment_duration": 1.0,
            "output_tos_dir": output_tos_dir,
        },
    )

    ds = ds.with_column("results", splitter(col("video_path")))

    ds.show()

    # ╭─────────────────────────────────────────┬──────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────╮
    # │ video_path                              ┆ results                                                                                                                          │
    # │ ---                                     ┆ ---                                                                                                                              │
    # │ Utf8                                    ┆ Struct[segments: List[Utf8], segments_binary: List[Binary]]                                            │
    # ╞═════════════════════════════════════════╪══════════════════════════════════════════════════════════════════════════════════════════════════════════════════════════════════╡
    # │ https://las-cn-beijing-publi-…          ┆ {segments: ["tos://tos_bucket/video/video_split_by_duration/sample/segment_1.mp4", "tos://tos_bucket/video/video_split_by_durat… │
    # ╰─────────────────────────────────────────┴──────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────╯
```
