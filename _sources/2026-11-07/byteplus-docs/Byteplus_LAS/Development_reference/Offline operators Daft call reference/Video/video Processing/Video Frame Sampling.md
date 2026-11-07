---
title: "Video Frame Sampling"
product: "Lake AI Service"
product_code: "Byteplus_LAS"
source: "https://docs.byteplus.com/en/docs/Byteplus_LAS/Video_Frame_Sampling"
---

<span id="operator-introduction"></span>
# Operator introduction

<span id="description"></span>
## Description

An image frame sampler from video, supporting multiple sampling modes and time range control.

Core features:


* Multiple sampling methods:

   * by_count_uniform: Uniformly sample K frames within the time range

   * by_interval_time: Sample at time interval Δt seconds

   * by_interval_frames: Sample at decoded frame interval N

   * by_fps: Sample at target fps

   * by_timestamps: Sample according to the given timestamp list

* Support start and end time range restrictions and whether to include the last frame

* Output original frames (array), base64 encoding, timestamps, frame indices, and optional TOS storage paths

* Two input sources: path input or binary input, compatible with remote URIs (via run_on_local_path)


<span id="daft-call"></span>
# Daft call

<span id="operator-parameters"></span>
## Operator parameters

<span id="input"></span>
## Input


|Input column name |Note |
|---|---|
|video_paths |Input video path column (local or remote URI), type string, default None |
|video_binaries |Input video binary column, type binary, default None |
|video_formats |Format corresponding to binary input (e.g., "mp4", "mov"), type string, default None |
|video_durations |Video duration column (seconds), type float, default None |


<span id="output"></span>
## Output

Struct array with fields including:


* frames: Array of sampled frame images (H x W x C), output configurable

* base64: Base64 encoding of sampled frames (format specified by img_type), output configurable

* timestamps: Timestamps of sampled frames (seconds)

* frame_indices: Frame indices of sampled frames in the decoded sequence

* tos_paths: Storage paths of sampled frames on TOS (if output_tos_dir is configured)


<span id="parameters"></span>
## Parameters

If a parameter does not have a default value, it is a required parameter.


|Parameter name |Type |Default value |Description |
|---|---|---|---|
|sample_mode |str |by_count_uniform |Sampling mode Optional values: ["by_count_uniform", "by_interval_time", "by_interval_frames", "by_fps", "by_timestamps"] |
|start_time_sec |float |0.0 |Start time (seconds) |
|end_time_sec |float or None | |End time (seconds), None means end of video |
|count_k |int or None | |Number of frames for uniform/random sampling (used by by_count_uniform) |
|interval_sec |float or None | |Time interval Δt (seconds, used by by_interval_time) |
|interval_frames |int or None | |Decoded frame interval N (used by by_interval_frames) |
|target_fps |float or None | |Target FPS (used by by_fps) |
|timestamps_sec |list or None | |Target timestamp list (seconds, used by by_timestamps) |
|img_type |str |.jpg |Output image format (for base64 and optional TOS storage), optional values: [".jpg", ".png", ".webp"], default ".jpg" |
|output_tos_dir |str | |If non\-empty, save sampled frames locally and upload to the target directory on TOS (each video has a separate subdirectory under the directory) |
|max_frames |int or None | |Maximum number of frames to return (defensive limit), None means no limit |
|seed |int |42 |When the total video duration is unknown in advance, the operator uses the reservoir sampling algorithm to uniformly randomly sample a specified number of frames from the video stream. This parameter sets the random seed to ensure reproducible sampling results, default value is 42. |
|output_frames |bool |True |Whether to output the original frame array (large size, default True). Note: Even if set to False, the returned result still contains the frames field, but the content is an empty list. |
|output_base64 |bool |True |Whether to output base64 encoding (large size, default True). Note: Even if set to False, the returned result still contains the base64 field, but the content is an empty list. |


<span id="examples"></span>
## Examples

The following code shows how to use Daft (suitable for distributed scenarios) to sample several image frames from a video at frame intervals. This example sets interval_frames=100 and actually produces 6 images.

```python
from __future__ import annotations

import os

import daft
from daft import col
from daft.las.functions.udf import las_udf
from daft.las.functions.video.video_frame_sampler import VideoFrameSampler

if __name__ == "__main__":

    # 更改完采样的帧会保存到指定的TOS路径下，因此，需要设置好环境变量以保证有权限写入TOS，包括：ACCESS_KEY,SECRET_KEY,TOS_ENDPOINT,TOS_REGION,TOS_TEST_DIR
    TOS_DIR = os.getenv("TOS_TEST_DIR", "tos_bucket")
    output_tos_dir = f"tos://{TOS_DIR}/video/video_frame_sampler"
    
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

    sampler = las_udf(
        VideoFrameSampler,
        construct_args={
            "sample_mode": "by_interval_frames",
            "interval_frames": 100,
            "output_tos_dir": output_tos_dir,
            "img_type": ".jpg",
        },
    )

    # 使用 Daft 进行分布式处理
    ds = ds.with_column("results", sampler(col("video_path")))

    ds = ds.select(
        "video_path",
        col("results")["frames"].alias("frames"),
        col("results")["base64"].alias("base64"),
        col("results")["timestamps"].alias("timestamps"),
        col("results")["frame_indices"].alias("frame_indices"),
        col("results")["tos_paths"].alias("tos_paths"),
    )

    ds.show()
    # ╭────────────────────────────────┬──────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────╮
    # │ video_path                     ┆ results                                                                                                                          │
    # │ ---                            ┆ ---                                                                                                                                      │
    # │ Utf8                           ┆ Struct[frames: List[Binary], base64: List[Utf8], timestamps: List[Float64], frame_indices: List[Int64], tos_paths: List[Utf8]] │
    # ╞════════════════════════════════╪══════════════════════════════════════════════════════════════════════════════════════════════════════════════════════════════════════════╡
    # │ https://las-cn-beijing-publi-… ┆ {frames: […], base64: […], timestamps: […], frame_indices: […], tos_paths: ["tos://tos_bucket/video/video_frame_sampler/frame_0.jpg", …]} │
    # ╰────────────────────────────────┴──────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────╯
```
