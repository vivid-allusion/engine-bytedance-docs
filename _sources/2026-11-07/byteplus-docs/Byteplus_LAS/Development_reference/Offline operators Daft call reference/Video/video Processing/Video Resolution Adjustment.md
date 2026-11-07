---
title: "Video Resolution Adjustment"
product: "Lake AI Service"
product_code: "Byteplus_LAS"
source: "https://docs.byteplus.com/en/docs/Byteplus_LAS/Video_Resolution_Adjustment"
---

<span id="operator-introduction"></span>
# Operator introduction

<span id="description"></span>
## Description

**Video Resolution Adjustment**

<span id="core-features"></span>
## Core Features:


* Intelligently adjust resolution to a specified range

* Support multiple aspect ratio preservation strategies

* Control video quality and encoding parameters

* Keep audio streams unaffected

* Support path input, binary input, and TOS output


<span id="supported-formats"></span>
## Supported Formats:


* MP4 (.mp4)

* AVI (.avi)

* MOV (.mov)

* MKV (.mkv)

* Other common video formats


<span id="encoding-modes"></span>
## Encoding Modes:


* **CPU Encoding (libx264):**  Quality\-first, high compression efficiency, slower speed

* **GPU Encoding (h264_nvenc):**  Fast speed, suitable for batch processing, slightly lower quality than libx264 (at the same bitrate), slightly worse compression efficiency, files may be larger


<span id="daft-call"></span>
# Daft call

<span id="operator-parameters"></span>
## Operator parameters

<span id="input"></span>
## Input


|Input column name |Note |
|---|---|
|video_paths |Column of video file paths (local, TOS, HTTP, etc.), choose either this or video_binaries |
|video_binaries |Column of video binary data, choose either this or video_paths |
|video_formats |Column of video format strings, used with video_binaries |
|output_basenames |Column of output file base names (without extension) |


<span id="output"></span>
## Output

Column of resized video paths

<span id="parameters"></span>
## Parameters

If a parameter does not have a default value, it is a required parameter.


|Parameter name |Type |Default value |Description |
|---|---|---|---|
|output_tos_dir |str | |Save the resized video to this TOS directory. If empty, do not save. Format: "tos://bucket/path/" Default value: "" |
|min_width |int |1280 |Minimum video width; adjust if the video width is smaller than this value. Unit: pixels Default value: 1280 |
|max_width |int |2560 |Maximum video width; adjust if the video width is larger than this value. Unit: pixels Default value: 2560 |
|min_height |int |1280 |Minimum video height; adjust if the video height is smaller than this value. Unit: pixels Default value: 1280 |
|max_height |int |2560 |Maximum video height; adjust if the video height is larger than this value. Unit: pixels Default value: 2560 |
|force_original_aspect_ratio_type |str |disable |Aspect ratio preservation strategy. disable: Do not force preserve original aspect ratio; may stretch or distort. increase: Preserve aspect ratio, adjust to be greater than or equal to target size. decrease: Preserve aspect ratio, adjust to be less than or equal to target size. Optional values: ["disable", "increase", "decrease"] Default value: "disable" |
|force_divisible_by |int |2 |Pixel alignment step; ensure width and height are divisible by this value. Default value: 2 |
|crf |float |23.0 |Constant quality factor for libx264 encoder. Applicable: Only used for CPU encoding (libx264). Range: 0.0\-51.0; smaller values mean higher quality and larger file size. Recommendations: 18 (high quality), 23 (balanced), 28 (compression priority). Default value: 23.0 |
|preset |str |medium |Encoding speed preset for libx264 encoder. Applicable: Only used for CPU encoding (libx264). Trade\-off: Speed ↔ compression efficiency. Optional values: ["ultrafast", "superfast", "veryfast", "faster", "fast", "medium", "slow", "slower", "veryslow"] Recommendations: "medium" (balanced), "fast" (speed priority), "slow" (quality priority). Default value: "medium" |
|cq |float |0 |Quality control parameter for NVENC encoder. Applicable: Only used for GPU encoding (h264_nvenc). Range: 0\-51; 0 means automatic quality control. Recommendations: 0 (automatic) or 18\-28 (manual control). Default value: 0 |
|rc |str |vbr |Bitrate control mode for NVENC encoder. Applicable: Only used for GPU encoding (h264_nvenc). constqp: Constant quantization parameter; stable quality. vbr: Variable bitrate; balances quality and file size. cbr: Constant bitrate; suitable for streaming. Recommendations: "vbr" (general use), "cbr" (live streaming). Default value: "vbr" |
|rank |int or None | |Specify the GPU device index to use (effective in multi\-GPU environments). Note: 0 means the first GPU, 1 means the second GPU, None means automatic selection. Applicable: Only effective for GPU encoding. Default value: None |


<span id="examples"></span>
## Examples

The following code shows how to use Daft (suitable for distributed environments) to run the operator for intelligent video resolution adjustment.

```python
from __future__ import annotations

import os

import daft
from daft import col
from daft.las.functions.udf import las_udf
from daft.las.functions.video import VideoResizeResolution

if __name__ == "__main__":

    # 更改完分辨率的视频会保存到指定的TOS路径下，因此，需要设置好环境变量以保证有权限写入TOS，包括：ACCESS_KEY,SECRET_KEY,TOS_ENDPOINT,TOS_REGION,TOS_TEST_DIR
    TOS_DIR = os.getenv("TOS_TEST_DIR", "tos_bucket")
    output_tos_dir = f"tos://{TOS_DIR}/video/video_resize_resolution"

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
    samples = {
        "video_path": [
            f"https://{tos_dir_url}/public/shared_video_dataset/eating_56.mp4"
        ]
    }
    ds = daft.from_pydict(samples)

    constructor_kwargs = {
        "output_tos_dir": output_tos_dir,
        "min_width": 1280,
        "max_width": 2560,
        "min_height": 720,
        "max_height": 1440,
        "force_original_aspect_ratio_type": "decrease",
        "rank": None,
    }

    ds = ds.with_column(
        "resized_video_path",
        las_udf(VideoResizeResolution, construct_args=constructor_kwargs, num_gpus=1, batch_size=1, concurrency=1)(
            col("video_path")
        ),
    )

    ds.show()
    # ╭────────────────────────────────┬──────────────────────────────────╮
    # │ video_path                     ┆ resized_video_path               │
    # │ ---                            ┆ ---                              │
    # │ Utf8                           ┆ Utf8                             │
    # ╞════════════════════════════════╪══════════════════════════════════╡
    # │ https://las-cn-beijing-publi-… ┆ tos://tos_bucket/video_resize…   │
    # ╰────────────────────────────────┴──────────────────────────────────╯
```
