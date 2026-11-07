---
title: "Video Keyframe Extraction"
product: "Lake AI Service"
product_code: "Byteplus_LAS"
source: "https://docs.byteplus.com/en/docs/Byteplus_LAS/Video_Keyframe_Extraction"
---

<span id="operator-introduction"></span>
# Operator introduction

<span id="description"></span>
## Description

**Video keyframe extraction processor that supports dynamic detection with multiple algorithms.** 

<span id="core-features"></span>
## Core Features:


* Multiple algorithm support:

   * Pixel difference method (difference)

   * Optical flow method (optical_flow)

   * Histogram method (histogram)

   * I\-frame keyframe identification (I_frame)

* Supports custom threshold and quantity control

* Provides timestamp positioning function

* Supports multiple output formats and storage options


<span id="format-support"></span>
## Format Support:


* Input: Common video formats such as MP4, AVI, MOV

* Output: JPG, PNG image formats


<span id="performance-advice"></span>
## Performance Advice:


* The I_frame method has the highest efficiency and is recommended for priority use


<span id="daft-call"></span>
# Daft call

<span id="operator-parameters"></span>
## Operator parameters

<span id="input"></span>
## Input


|Input column name |Note |
|---|---|
|video_paths |Input video path column, type is array. Default value: None |
|video_binaries |Input video binary data column, type is array. Default value: None |
|video_formats |Input video format column (e.g., 'mp4', 'avi', etc.), type is array. Default value: None |


<span id="output"></span>
## Output

Processed array, the struct fields include:


* keyframes: list[list[list[list[int]]]]，array format of keyframe images

* base64: list[str]，base64 encoding of keyframe images

* timestamps: list[float]，timestamps corresponding to keyframes (unit: seconds)

* tos_paths: list[str]，storage paths of keyframes on TOS


<span id="parameters"></span>
## Parameters

If a parameter does not have a default value, it is a required parameter.


|Parameter name |Type |Default value |Description |
|---|---|---|---|
|method |str |I_frame |Method for extracting keyframes, supports "difference" (pixel difference method), "optical_flow" (optical flow method), "histogram" (histogram method), "I_frame" (I\-type keyframe identifier). Optional values: ["difference", "optical_flow", "histogram", "I_frame"] Default value: "I_frame" |
|img_type |str |.jpg |Output keyframe image format, supports ".jpg", ".png". Optional values: [".jpg", ".png"] Default value: ".jpg" |
|threshold |float |0 |Threshold for determining keyframes. Recommended values: 2000000 for difference, 0.01 for histogram, and 2.0 for optical_flow. Default value: 0 |
|keyframes_cnt |int |10 |Specify the number of keyframes to extract, \-1 means no limit. Default value: 10 |
|seconds_per_frame |int |\-1 |Frame extraction interval in seconds, \-1 means no interval specified. Default value: \-1 |
|output_tos_dir |str | |Target path to save keyframe images to TOS; if empty string, no upload. Default value: "" |


<span id="examples"></span>
## Examples

The following code shows how to use Daft (suitable for distributed scenarios) to run the operator for video keyframe extraction.

```python
from __future__ import annotations

import os

import daft
from daft import col
from daft.las.functions.udf import las_udf
from daft.las.functions.video import VideoKeyframes

if __name__ == "__main__":

    # 更改完抽取的关键帧会保存到指定的TOS路径下，因此，需要设置好环境变量以保证有权限写入TOS，包括：ACCESS_KEY,SECRET_KEY,TOS_ENDPOINT,TOS_REGION,TOS_TEST_DIR
    TOS_DIR = os.getenv("TOS_TEST_DIR", "tos_bucket")
    output_tos_dir = f"tos://{TOS_DIR}/video/video_keyframes"
    
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

    extractor = las_udf(
        VideoKeyframes,
        construct_args={
            "method": "I_frame",
            "keyframes_cnt": 5,
            "output_tos_dir": output_tos_dir,
        },
    )

    # 使用 Daft 进行分布式处理
    ds = ds.with_column("results", extractor(col("video_path")))

    ds.show()
    # ╭────────────────────────────────┬────────────────────────────────────────────────────────────────────────────────────────────────────────────╮
    # │ video_path                     ┆ results                                                                                                    │
    # │ ---                            ┆ ---                                                                                                        │
    # │ Utf8                           ┆ Struct[keyframes: List[List[List[List[Int64]]]], base64: List[Utf8], timestamps: List[Float64], tos_paths: │
    # │                                ┆ List[Utf8]]                                                                                                │
    # ╞════════════════════════════════╪════════════════════════════════════════════════════════════════════════════════════════════════════════════╡
    # │ https://las-cn-beijing-publi-…  ┆ {keyframes: [[[[9, 17, 16], […                                                                             │
    # ╰────────────────────────────────┴────────────────────────────────────────────────────────────────────────────────────────────────────────────╯
```
