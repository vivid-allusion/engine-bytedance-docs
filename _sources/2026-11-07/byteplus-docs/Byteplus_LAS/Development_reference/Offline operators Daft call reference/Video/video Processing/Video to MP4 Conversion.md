---
title: "Video to MP4 Conversion"
product: "Lake AI Service"
product_code: "Byteplus_LAS"
source: "https://docs.byteplus.com/en/docs/Byteplus_LAS/Video_to_MP4_Conversion"
---

<span id="operator-introduction"></span>
# Operator introduction

<span id="description"></span>
## Description

**Video Format Conversion Processor, converting various video formats to MP4**

<span id="core-features"></span>
## Core Features:


* Supports converting multiple video formats to MP4

* Intelligent audio track selection (All/Auto/First)

* Customizable video quality and encoding parameters

* Supports video height limitation and scaling

* Fine\-grained control over audio encoding parameters

* Supports local files, HTTP/HTTPS URLs, and TOS/S3 storage


<span id="format-support"></span>
## Format Support:


* Input: Mainstream video formats like AVI, MOV, MKV, FLV, WMV, 3GP, etc.

* Output: MP4 (.mp4)

* Video Codecs: H.264/H.265, etc.

* Audio Codecs: AAC, MP3, etc.


<span id="daft-call"></span>
# Daft call

<span id="operator-parameters"></span>
## Operator parameters

<span id="input"></span>
## Input


|Input column name |Note |
|---|---|
|input_col |An array containing input video paths (supports local paths, HTTP/HTTPS URLs, TOS/S3 URLs) |
|output_col |An array containing output MP4 file paths |


<span id="output"></span>
## Output

An array containing conversion result paths; returns the output path on success, None on failure

<span id="parameters"></span>
## Parameters

If a parameter does not have a default value, it is a required parameter.


|Parameter name |Type |Default value |Description |
|---|---|---|---|
|video_codec |str |libx264 |Video encoder; supports libx264, libx265, etc. Default value: "libx264" |
|crf |int |23 |Video quality control; value range is 0\-51, smaller values mean better quality Default value: 23 |
|preset |str |medium |Encoding speed preset; supports ultrafast, superfast, veryfast, faster, fast, medium, slow, slower, veryslow Default value: "medium" |
|max_height |int or None | |Maximum video height limit; automatically scales if exceeded; no limit when set to None Default value: None |
|audio_codec |str |aac |Audio encoder; supports aac, etc. Default value: "aac" |
|audio_bitrate |str |192k |Audio bitrate, e.g., "192k", "128k" Default value: "192k" |
|audio_sample_rate |int or None | |Audio sample rate, e.g.,44100,48000; keeps original sample rate when set to None Default value: None |
|select_audio |str |all |Audio track selection strategy: "all" (all tracks), "auto" (intelligently select default track), "first" (first track) Default value: "all" |
|extra_params |list or None | |Additional ffmpeg parameter list, e.g., ["\-movflags", "+faststart"] Default value: None |
|timeout |int or None | |Timeout for processing a single video (seconds); no limit when set to None Default value: None |


<span id="examples"></span>
## Examples

The following code shows how to use Daft (for distributed scenarios) to run the operator for converting videos to MP4 format.

```python
from __future__ import annotations

import os

import daft
from daft import col
from daft.las.functions.udf import las_udf
from daft.las.functions.video import VideoConvertToMp4

if __name__ == "__main__":
    # 转换后的视频会保存到指定的TOS路径下，因此，需要设置好环境变量以保证有权限写入TOS，包括：ACCESS_KEY,SECRET_KEY,TOS_ENDPOINT,TOS_REGION,TOS_TEST_DIR
    TOS_TEST_DIR_URL = os.getenv("TOS_TEST_DIR_URL", "las-cn-beijing-public-online.tos-cn-beijing.volces.com")
    TOS_TEST_DIR = os.getenv("TOS_TEST_DIR", "tos_bucket")

    if os.getenv("DAFT_RUNNER", "native") == "ray":
        import logging

        import ray

        def configure_logging():
            logging.basicConfig(
                level=logging.INFO,
                format="%(asctime)s - %(name)s - %(levelname)s - %(message)s",
                datefmt="%Y-%m-%d %H:%M:%S",
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

    samples = {
        "input_path": [f"https://{TOS_TEST_DIR_URL}/public/archive/video_convert_to_mp4/sample.mp4"],
        "output_path": [f"tos://{TOS_TEST_DIR}/video_convert_to_mp4/sample_converted.mp4"],
    }
    ds = daft.from_pydict(samples)

    # Using Daft to convert video to MP4 format
    constructor_kwargs = {
        "video_codec": "libx264",
        "crf": 23,
        "preset": "medium",
        "max_height": 240,
        "audio_codec": "aac",
        "audio_bitrate": "192k",
        "select_audio": "auto",
        "extra_params": ["-movflags", "+faststart"],
    }

    ds = ds.with_column(
        "convert_result",
        las_udf(
            VideoConvertToMp4,
            construct_args=constructor_kwargs,
            num_cpus=1,
            concurrency=1,
            batch_size=1,
        )(col("input_path"), col("output_path")),
    )

    ds.show()
    # ╭────────────────────────────────┬────────────────────────────────┬────────────────────────────────╮
    # │ input_path                     ┆ output_path                    ┆ convert_result                 │
    # │ ---                            ┆ ---                            ┆ ---                            │
    # │ String                         ┆ String                         ┆ String                         │
    # ╞════════════════════════════════╪════════════════════════════════╪════════════════════════════════╡
    # │ https://las-public-data-qa.to… ┆ tos://tos_bucket/video_conver… ┆ tos://tos_bucket/video_conver… │
    # ╰────────────────────────────────┴────────────────────────────────┴────────────────────────────────╯
```
