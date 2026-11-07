---
title: "Adaptive Video Compression"
product: "Lake AI Service"
product_code: "Byteplus_LAS"
source: "https://docs.byteplus.com/en/docs/Byteplus_LAS/Adaptive_Video_Compression"
---

<span id="operator-introduction"></span>
# Operator introduction

<span id="description"></span>
## Description

**Video Adaptive Compression**

<span id="core-features"></span>
## Core Features:


* Adaptively compress video according to target file size

* Multi\-level compression strategy: Frame rate adjustment → Resolution adjustment → Bitrate control

* Compress file size as much as possible while maintaining video quality

* Support CPU and GPU encoding

* Support path input, binary input, and TOS output


<span id="compression-strategy"></span>
## Compression Strategy:


1. Check original file size; if smaller than target size, return directly

2. Adjust frame rate to target_fps (default 5fps), check if size meets requirements (skip if original fps is less than or within 2fps of target fps)

3. Adjust resolution proportionally to minimum resolution (default 360p), check if size meets requirements (skip if original resolution is less than or within 1.2x of target resolution)

4. Use two\-pass bitrate control to force compression to target size


<span id="supported-formats"></span>
## Supported Formats:


* MP4 (.mp4)

* AVI (.avi)

* MOV (.mov)

* MKV (.mkv)

* Other common video formats


<span id="encoding-modes"></span>
## Encoding Modes:


* **CPU Encoding (libx264):**  Quality priority, high compression efficiency, slow speed, low cost

* **GPU Encoding (h264_nvenc):**  Fast speed, relatively high cost


<span id="daft-call"></span>
# Daft call

<span id="operator-parameters"></span>
## Operator parameters

<span id="input"></span>
## Input


|Input column name |Note |
|---|---|
|video_paths |Column of video file paths (local, TOS, HTTP, etc.); choose either this or video_binaries |
|video_binaries |Column of video binary data; choose either this or video_paths |
|video_formats |Column of video format strings; used with video_binaries |
|output_basenames |Column of output file base names (without extension) |


<span id="output"></span>
## Output

Column of compressed video paths

<span id="parameters"></span>
## Parameters

If a parameter does not have a default value, it is a required parameter.


|Parameter name |Type |Default value |Description |
|---|---|---|---|
|output_tos_dir |str | |Save compressed videos to this TOS directory; if empty, do not save. Format: "tos://bucket/path/" Default value: "" |
|max_output_size_mb |float |50.0 |Maximum output file size (MB). Default value:50.0 |
|target_fps |float |5.0 |Target value for frame rate adjustment. Default value:5.0 |
|min_resolution_height |int |360 |Minimum resolution height (pixels), maintaining aspect ratio. Default value:360 |
|allowed_formats |list |[mp4, avi, mov] |List of video formats allowed to output directly if the video size meets requirements. Default value: ["mp4", "avi", "mov"] |
|rank |int or None | |Specify the GPU device ID to use (valid in multi\-card environments). Default value: None |


<span id="examples"></span>
## Examples

The following code demonstrates how to use Daft (suitable for distributed environments) to run the operator for adaptive video compression with intelligent file size control.

```python
from __future__ import annotations

import os

import daft
from daft import col
from daft.las.functions.udf import las_udf
from daft.las.functions.video import VideoAdaptiveCompress

if __name__ == "__main__":
    # 更改完的视频会保存到指定的TOS路径下，因此，需要设置好环境变量以保证有权限写入TOS，包括：ACCESS_KEY,SECRET_KEY,TOS_ENDPOINT,TOS_REGION,TOS_TEST_DIR
    TOS_DIR = os.getenv("TOS_DIR", "tos_bucket")
    output_tos_dir = f"tos://{TOS_DIR}/video/video_adaptive_compress"

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

    tos_dir_url = os.getenv("TOS_DIR_URL", "las-cn-beijing-public-online.tos-cn-beijing.volces.com")
    samples = {"video_path": [f"https://{tos_dir_url}/public/shared_video_dataset/A_Quiet_Place_movie_clip.mp4"]}
    ds = daft.from_pydict(samples)

    constructor_kwargs = {
        "output_tos_dir": output_tos_dir,
        "max_output_size_mb": 30.0,
        "target_fps": 20.0,
        "min_resolution_height": 360,
        "rank": None,
    }

    ds = ds.with_column(
        "compressed_video_path",
        las_udf(VideoAdaptiveCompress, construct_args=constructor_kwargs, num_gpus=1, batch_size=1, concurrency=1)(
            col("video_path")
        ),
    )

    ds.show()
    
    # ╭────────────────────────────────┬────────────────────────────────╮
    # │ video_path                     ┆ compressed_video_path          │
    # │ ---                            ┆ ---                            │
    # │ String                         ┆ String                         │
    # ╞════════════════════════════════╪════════════════════════════════╡
    # │ https://las-cn-beijing-public… ┆ tos://tos_bucket/video/video_… │
    # ╰────────────────────────────────┴────────────────────────────────╯
```
