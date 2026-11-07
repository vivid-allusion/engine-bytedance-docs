---
title: "Video Clip Segmentation (Keyframe)"
product: "Lake AI Service"
product_code: "Byteplus_LAS"
source: "https://docs.byteplus.com/en/docs/Byteplus_LAS/Video-Clip-Segmentation-Keyframe"
---

<span id="operator-introduction"></span>
# Operator introduction

<span id="description"></span>
## Description

**Video keyframe segmentation processor, supporting intelligent clip splitting.** 

<span id="core-features"></span>
## Core Features:


* Multi\-algorithm keyframe detection:

   * I_frame: Based on I\-frame detection (recommended)

   * difference: Pixel difference detection

   * histogram: Histogram difference detection

* Supports clip binary output or TOS storage

* Provides timestamp positioning function


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
|video_paths |Array containing input video paths Default value: None |
|video_binaries |Array containing video binary data Default value: None |
|video_formats |Array containing input video formats (e.g., 'mp4', 'avi', etc.), can provide format information when specifying video_binaries Default value: None |
|output_basenames |Optional, array of output subdirectory names (file names) |


<span id="output"></span>
## Output

The processed struct fields include:


* segments: list[str], list of paths for split video segments

* segments_binary: list[bytes], list of binary data for split video segments

* video_format: list[str], list of formats for split video segments


<span id="parameters"></span>
## Parameters

If a parameter does not have a default value, it is a required parameter.


|Parameter name |Type |Default value |Description |
|---|---|---|---|
|method |str |I_frame |Method for extracting keyframes, supports "difference" (pixel difference method), "histogram" (histogram method), "I_frame" (I\-type keyframe identification). Note: Non\-I\-frame methods may take longer to process videos. Optional values: ["difference", "histogram", "I_frame"] Default value: "I_frame" |
|threshold |float |0 |Threshold for determining keyframes. Recommended values: 2000000 for difference method, 0.01 for histogram method. Default value: 0 |
|keyframes_cnt |int |10 |Used to specify the number of keyframes to extract from the video. \-1 means use all detected keyframes; 0 means invalid parameter (no video splitting will occur); if the set number is greater than the actual number of keyframes, all keyframes are used; otherwise, the specified number of keyframes will be selected uniformly from all keyframes to avoid concentration in a certain time period. Default value:10 |
|seconds_per_frame |int |\-1 |Frame extraction interval in seconds, \-1 means no interval specified. Default value: \-1 |
|output_tos_dir |str | |TOS path to save video segments; if empty string, no upload. Default value: "" |
|output_segments_binary |bool |False |Whether to output binary data of video segments. Default value: False |
|output_video_format |str or None | |Globally specify output video format (e.g., "mp4", "avi", etc.), priority is higher than input file extension and video_format column. |


<span id="examples"></span>
## Examples

The following code shows how to use Daft (for distributed scenarios) to run the operator to split videos by keyframes.

```python
from __future__ import annotations

import os

import daft
from daft import col
from daft.las.functions.udf import las_udf
from daft.las.functions.video import VideoSplitByKeyframes

if __name__ == "__main__":

    # 更改完切分的视频会保存到指定的TOS路径下，因此，需要设置好环境变量以保证有权限写入TOS，包括：ACCESS_KEY,SECRET_KEY,TOS_ENDPOINT,TOS_REGION,TOS_TEST_DIR
    TOS_DIR = os.getenv("TOS_TEST_DIR", "tos_bucket")
    output_tos_dir = f"tos://{TOS_DIR}/video/video_split_by_keyframes"
    
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
        VideoSplitByKeyframes,
        construct_args={
            "method": "I_frame",
            "keyframes_cnt": 2,
            "output_tos_dir": output_tos_dir,
        },
    )

    # 使用 Daft 进行分布式处理
    ds = ds.with_column("results", splitter(col("video_path")))

    ds.show()
    # ╭──────────────────────────────────────────┬──────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────╮
    # │ video_path                               ┆ results                                                                                                                          │
    # │ ---                                      ┆ ---                                                                                                                              │
    # │ Utf8                                     ┆ Struct[segments: List[Utf8], segments_binary: List[Binary], video_format: List[Utf8]]                                            │
    # ╞══════════════════════════════════════════╪══════════════════════════════════════════════════════════════════════════════════════════════════════════════════════════════════╡
    # │ https://las-cn-beijing-publi-…           ┆ {segments: ["tos://tos_bucket/video/video_split_by_keyframes/sample/segment_1.mp4", "tos://tos_bucket/video/video_split_by_keyf… │
    # ╰──────────────────────────────────────────┴──────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────╯
```
