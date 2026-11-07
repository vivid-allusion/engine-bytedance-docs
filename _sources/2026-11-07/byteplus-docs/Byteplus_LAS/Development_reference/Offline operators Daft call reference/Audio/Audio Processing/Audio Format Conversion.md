---
title: "Audio Format Conversion"
product: "Lake AI Service"
product_code: "Byteplus_LAS"
source: "https://docs.byteplus.com/en/docs/Byteplus_LAS/Audio_Format_Conversion"
---

<span id="operator-introduction"></span>
# Operator introduction

<span id="description"></span>
## Description

**Universal audio format conversion processor that supports conversion to any audio format**

<span id="core-features"></span>
## Core Features:


* Supports conversion to multiple audio formats (MP3, WAV, FLAC, AAC, OGG, etc.)

* Customizable audio sample rate

* Intelligent audio track selection (all/auto/first)

* Supports format\-specific parameters via extra_params

* Supports local files, HTTP/HTTPS URLs, and TOS/S3 storage


<span id="format-support"></span>
## Format Support:


* Input: Mainstream audio formats like WAV, FLAC, MP3, AAC, M4A, OGG, WMA, APE, etc.

* Output: Specified by the output_format parameter (mp3, wav, flac, aac, ogg, m4a, etc.)

* Sample rate: 8kHz\-192kHz


<span id="daft-call"></span>
# Daft call

<span id="operator-parameters"></span>
## Operator parameters

<span id="input"></span>
## Input


|Input column name |Note |
|---|---|
|input_col |An array containing input audio paths (supports local paths, HTTP/HTTPS URLs, TOS/S3 URLs) |
|output_col |An array containing output audio file paths |


<span id="output"></span>
## Output

An array containing the paths of conversion results; returns the output path if successful, None if failed

<span id="parameters"></span>
## Parameters

If a parameter does not have a default value, it is a required parameter.


|Parameter name |Type |Default value |Description |
|---|---|---|---|
|output_format |str | |Output audio format, such as "mp3", "wav", "flac", "aac", "ogg", etc. This parameter determines the output file extension and default encoder |
|sample_rate |int or None | |Audio sample rate, e.g., 22050, 44100, 48000, 96000, 192000; keeps the original sample rate if None Default value: None |
|audio_map |str |all |Audio track selection strategy: \- "all": Select all tracks (default) \- "auto": Intelligently select the default track (automatically detect the default flag) \- "first": Select only the first track Default value: "all" |
|extra_params |list or None | |Additional ffmpeg parameter list for specifying format\-specific encoders and parameters Examples: \- MP3: ["\-c:a", "libmp3lame", "\-b:a", "192k", "\-q:a", "2"] \- WAV: ["\-c:a", "pcm_s24le"] \- FLAC: ["\-c:a", "flac", "\-compression_level", "8"] \- AAC: ["\-c:a", "aac", "\-b:a", "128k"] Default value: None (uses the default encoder automatically selected by ffmpeg) |
|timeout |int or None | |Timeout for processing a single audio file (in seconds); no limit if None Default value: None |


<span id="examples"></span>
## Examples

The following code shows how to use Daft (for distributed processing) to run the operator for audio format conversion. Supports conversion to multiple formats such as MP3, WAV, FLAC, AAC, OGG, etc.

```python
from __future__ import annotations

import os

import daft
from daft import col
from daft.las.functions.audio import AudioConvert
from daft.las.functions.udf import las_udf

if __name__ == "__main__":
    # 转换后的音频会保存到指定的TOS路径下，因此，需要设置好环境变量以保证有权限写入TOS，包括：ACCESS_KEY,SECRET_KEY,TOS_ENDPOINT,TOS_REGION,TOS_TEST_DIR
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
        "input_path": [f"https://{TOS_TEST_DIR_URL}/public/archive/audio_convert/sample.wav"],
        "output_path": [f"tos://{TOS_TEST_DIR}/audio_convert/sample_converted.mp3"],
    }
    ds = daft.from_pydict(samples)

    # Using Daft to convert audio to MP3 format (as an example)
    # AudioConvert supports multiple formats: mp3, wav, flac, aac, ogg, etc.
    constructor_kwargs = {
        "output_format": "mp3",
        "sample_rate": 44100,
        "audio_map": "auto",
        "extra_params": ["-c:a", "libmp3lame", "-b:a", "192k", "-q:a", "2"],
    }

    ds = ds.with_column(
        "convert_result",
        las_udf(
            AudioConvert,
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
    # │ https://las-public-data-qa.to… ┆ tos://tos_bucket/audio_conver… ┆ tos://tos_bucket/audio_conver… │
    # ╰────────────────────────────────┴────────────────────────────────┴────────────────────────────────╯
```
