---
title: "Video Audio Extraction"
product: "Lake AI Service"
product_code: "Byteplus_LAS"
source: "https://docs.byteplus.com/en/docs/Byteplus_LAS/Video_Audio_Extraction"
---

<span id="operator-introduction"></span>
# Operator introduction

<span id="description"></span>
## Description

**Video Audio Extraction Processor, supporting multi\-stream separation**

<span id="core-features"></span>
## Core Features:


* Supports extracting audio streams from videos with multiple input sources including local files, TOS, HTTP paths, or binary input

* Supports multi\-audio stream selection: take only the first stream or all streams

* Supports outputting audio to TOS, returning binary data, setting sample rates, etc.

* Supports extracting specified time intervals (start_second, end_second)

* **All output audio is in MP3 format**


<span id="daft-call"></span>
# Daft call

<span id="operator-parameters"></span>
## Operator parameters

<span id="input"></span>
## Input


|Input column name |Note |
|---|---|
|video_paths |Array of video file paths (local, TOS, HTTP, etc.) |
|video_binaries |Array of video binary data (optional) |
|video_formats |Array of video format strings (optional) |
|output_basenames |Optional; array of output subdirectory names (file names) |


<span id="output"></span>
## Output

An array of structs, including:


* audio_paths: Column containing TOS paths of audio

* audio_arrays: Column containing audio array data (optional)

* binaries: Column containing audio binary data (optional)

* original_audio_sampling_rates: Always returned; contains the original sampling rate of each audio stream, one\-to\-one corresponding to audio_paths/binaries


<span id="parameters"></span>
## Parameters

If a parameter does not have a default value, it is a required parameter.


|Parameter name |Type |Default value |Description |
|---|---|---|---|
|output_tos_dir |str | |Save the audio extracted from the video to this TOS directory; if empty, do not save the audio |
|output_audio_binary |bool |False |Whether to return the binary content of the audio; default is False |
|output_audio_array |bool |False |Whether to return the audio in numpy array format; default is False |
|stream_indexes |list or None | |Specify which audio streams to extract; default is all. Indexes out of range are automatically ignored |
|return_first_stream |bool |True |If True, only return the first audio stream; otherwise, return a list of all streams; default is True |
|start_second |float or None | |Start extracting audio from which second of the video; None means start from the beginning; unit is seconds |
|end_second |float or None | |End extracting audio at which second of the video; None means end at the end; unit is seconds |
|output_format |str |mp3 |Output audio format; default is "mp3" |
|output_sample_rate |int |48000 |Output audio sampling rate; default is 48000 |


<span id="examples"></span>
## Examples

The following code shows how to use Daft (for distributed scenarios) to run the operator to extract audio from videos.

```python
from __future__ import annotations
import os
import daft
from daft import col
from daft.las.functions.udf import las_udf
from daft.las.functions.video import VideoExtractAudio
if __name__ == "__main__":
    # 更改完抽取的音频会保存到指定的TOS路径下，因此，需要设置好环境变量以保证有权限写入TOS，包括：ACCESS_KEY,SECRET_KEY,TOS_ENDPOINT,TOS_REGION,TOS_TEST_DIR
    TOS_DIR = os.getenv("TOS_TEST_DIR", "tos_bucket")
    output_tos_dir = f"tos://{TOS_DIR}/video/video_extract_audio"
    
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
    }
    ds = daft.from_pydict(samples)
    constructor_kwargs = {
        "output_tos_dir": output_tos_dir,
        "output_audio_binary": True,
        "output_sampling_rate": 16000,
        "output_audio_format": "mp3",
    }
    # 使用 Daft 进行分布式处理
    ds = ds.with_column(
        "extract_results",
        las_udf(VideoExtractAudio, construct_args=constructor_kwargs)(col("video_path")),
    )
    ds.show()
    # ╭────────────────────────────────┬──────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────╮
    # │ video_path                     ┆ extract_results                                                                                                                          │
    # │ ---                            ┆ ---                                                                                                                                      │
    # │ Utf8                           ┆ Struct[audio_paths: List[Utf8], audio_arrays: List[List[Float32]], binaries: List[Binary], original_audio_sampling_rates: List[Float64]] │
    # ╞════════════════════════════════╪══════════════════════════════════════════════════════════════════════════════════════════════════════════════════════════════════════════╡
    # │ https://las-cn-beijing-publi-… ┆ {audio_paths: [tos://tos_bucket/video/video_extract_audio/sample.mp3], …                                                                 │
    # ╰────────────────────────────────┴──────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────╯
```
