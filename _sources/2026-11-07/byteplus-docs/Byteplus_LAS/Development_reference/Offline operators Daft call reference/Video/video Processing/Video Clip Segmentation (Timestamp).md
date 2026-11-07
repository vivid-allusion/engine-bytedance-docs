---
title: "Video Clip Segmentation (Timestamp)"
product: "Lake AI Service"
product_code: "Byteplus_LAS"
source: "https://docs.byteplus.com/en/docs/Byteplus_LAS/Video-Clip-Segmentation-Timestamp"
---

<span id="operator-introduction"></span>
# Operator introduction

<span id="description"></span>
## Description

**Video Timestamp Splitting Processor, supports splitting by specified time ranges**

<span id="core-features"></span>
## Core Features:


* Split video by given timestamp intervals

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
|timestamp_ranges |A list of timestamp ranges corresponding to each row, supporting formats: \- [(start,end), (start,end)] or [[start,end], [start,end]] \- Single (start,end) or [start,end] |
|output_basenames |Optional, array of output subdirectory names (file names) |


<span id="output"></span>
## Output

The processed struct fields include:


* segments: list[str], list of paths of split video segments

* segments_binary: list[bytes], list of binary data of split video segments


<span id="parameters"></span>
## Parameters

If a parameter does not have a default value, it is a required parameter.


|Parameter name |Type |Default value |Description |
|---|---|---|---|
|output_tos_dir |str | |TOS path to save video segments; if empty string, no upload Default value: "" |
|output_segments_binary |bool |False |Whether to output binary data of video segments Default value: False |
|output_video_format |str or None | |Globally specify the output video format (e.g., "mp4", "avi", etc.), which has higher priority than input file suffix and video_format column |


<span id="examples"></span>
## Examples

The following code demonstrates how to use Daft (for distributed scenarios) to run the operator to split videos by timestamps.

```python
from __future__ import annotations

import os

import daft
from daft import col
from daft.las.functions.udf import las_udf
from daft.las.functions.video import VideoSplitByTimestamps

if __name__ == "__main__":

    # 更改完切分的视频会保存到指定的TOS路径下，因此，需要设置好环境变量以保证有权限写入TOS，包括：ACCESS_KEY,SECRET_KEY,TOS_ENDPOINT,TOS_REGION,TOS_TEST_DIR
    TOS_DIR = os.getenv("TOS_TEST_DIR", "tos_bucket")
    output_tos_dir = f"tos://{TOS_DIR}/video/video_split_by_timestamps"
    
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
        ],
        "timestamp_ranges": [[(0.0, 2.0), (2.0, 4.0)]],
    }

    ds = daft.from_pydict(samples)

    splitter = las_udf(
        VideoSplitByTimestamps,
        construct_args={
            "output_tos_dir": output_tos_dir,
            "output_segments_binary": False,
            "output_video_format": "mp4",
        },
    )

    # 使用 Daft 进行分布式处理
    ds = ds.with_column("results", splitter(col("video_path"), None, None, col("timestamp_ranges")))

    ds.show()
    # ╭────────────────────────────────┬────────────────────────────────────────┬─────────────────────────────────────────────────────────────╮
    # │ video_path                     ┆ timestamp_ranges                       ┆ results                                                     │
    # │ ---                            ┆ ---                                    ┆ ---                                                         │
    # │ Utf8                           ┆ List[Struct[_0: Float64, _1: Float64]] ┆ Struct[segments: List[Utf8], segments_binary: List[Binary]] │
    # ╞════════════════════════════════╪════════════════════════════════════════╪═════════════════════════════════════════════════════════════╡
    # │ https://las-cn-beijing-publi-… ┆ [{_0: 0,                               ┆ {segments: ["tos://tos_bucket/video/video_split_b…          │
    # │                                ┆ }, {_0: 2,                             ┆                                                             │
    # │                                ┆ _1…                                    ┆                                                             │
    # ╰────────────────────────────────┴────────────────────────────────────────┴─────────────────────────────────────────────────────────────╯
```
