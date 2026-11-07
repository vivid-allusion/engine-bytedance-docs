---
title: "Audio Filter Processing"
product: "Lake AI Service"
product_code: "Byteplus_LAS"
source: "https://docs.byteplus.com/en/docs/Byteplus_LAS/Audio_Filter_Processing"
---

<span id="operator-introduction"></span>
# Operator introduction

<span id="description"></span>
## Description

**Audio filter processor, a flexible audio effect application based on FFmpeg.** 

<span id="core-features"></span>
## Core Features:


* Apply common audio filters (volume, highpass, lowpass, bass, treble, aecho, etc.) via FFmpeg

* Supports automatic download and processing of local paths and TOS/S3 remote paths

* Supports uploading processing results to TOS or returning binary results


<span id="format-support"></span>
## Format Support:


* MP3 (.mp3)

* WAV (.wav)

* FLAC (.flac)

* OGG (.ogg)

* AAC (.aac)

* M4A (.m4a)


Reference Document: https://ffmpeg.org/ffmpeg\-filters.html#Audio\-Filters

<span id="daft-call"></span>
# Daft call

<span id="operator-parameters"></span>
## Operator parameters

<span id="input"></span>
## Input


|Input column name |Note |
|---|---|
|audio_paths |An array containing input audio paths Default value: None |
|audio_binaries |An array containing audio binary data Default value: None |
|audio_formats |An array containing input audio formats (e.g., 'mp3', 'wav', etc.), which can provide format information when specifying audio_binaries Default value: None |
|output_basenames |Optional, an array of base names for output files (without extension), used to customize output file names Default value: None |


<span id="output"></span>
## Output

The processed structure fields include:


* processed_audio_path: str, path of the processed audio (local or TOS)

* processed_audio_binary: bytes, binary content of the processed audio (when output_audio_binary=True)


<span id="parameters"></span>
## Parameters

If a parameter does not have a default value, it is a required parameter.


|Parameter name |Type |Default value |Description |
|---|---|---|---|
|filter_name |str | |FFmpeg audio filter name. Common filters: \- volume: volume adjustment \- highpass: high\-pass filter (removes low\-frequency noise) \- lowpass: low\-pass filter (removes high\-frequency noise) \- bass/lowshelf: bass enhancement \- treble/highshelf: treble enhancement \- aecho: echo effect For more filters, refer to the official documentation. |
|filter_kwargs |dict or None | |Filter parameter dictionary (varies by filter). Examples: \- volume: {"volume": 1.5} \- highpass: {"f": 300, "width_type": "h", "width": 0.5} \- lowpass: |
|global_args |list or None | |FFmpeg global parameter list. Common combinations: \- Silent mode (errors only): ["\-loglevel", "error", "\-hide_banner"] \- Debug mode: ["\-loglevel", "debug", "\-stats"] \- Force overwrite output: ["\-y"] \- Performance optimization: ["\-threads", "4"] |
|output_tos_dir |str | |TOS directory for output results (no upload if empty). |
|output_audio_binary |bool |False |Whether to return the processed audio binary. Default value: False |
|output_audio_format |str or None | |Specify output audio format (e.g., "mp3", "wav", etc.). If empty, uses the input file extension; defaults to "wav" for binary input. |


<span id="examples"></span>
## Examples

The following code demonstrates how to use Daft (suitable for distributed execution) to run the operator and apply FFmpeg filters to audio.

```python
from __future__ import annotations

import os

import daft
from daft import col
from daft.las.functions.audio.audio_ffmpeg_wrapped import AudioFFMPEGWrapped
from daft.las.functions.udf import las_udf

if __name__ == "__main__":

    # 更改完处理的音频会保存到指定的TOS路径下，因此，需要设置好环境变量以保证有权限写入TOS，包括：ACCESS_KEY,SECRET_KEY,TOS_ENDPOINT,TOS_REGION,TOS_TEST_DIR
    TOS_DIR = os.getenv("TOS_TEST_DIR", "tos_bucket")
    output_tos_dir = f"tos://{TOS_DIR}/audio/audio_ffmpeg_wrapped"

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
        "audio_path": [
            f"https://{tos_dir_url}/public/shared_audio_dataset/sample.mp3"
        ]
    }

    ds = daft.from_pydict(samples)

    splitter = las_udf(
        AudioFFMPEGWrapped,
        construct_args={
            "filter_name": "volume",
            "filter_kwargs": {"volume": 1.5},
            "global_args": ["-loglevel", "error", "-hide_banner", "-y"],
            "output_tos_dir": output_tos_dir,
            "output_audio_binary": False,
            "output_audio_format": "wav",
        },
    )

    ds = ds.with_column("results", splitter(col("audio_path")))

    ds.show()
    # ╭─────────────────────────────────────────┬────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────╮
    # │ audio_path                              ┆ results                                                                                                                            │
    # │ ---                                     ┆ ---                                                                                                                                │
    # │ Utf8                                    ┆ Struct[processed_audio_path: Utf8, processed_audio_binary: Binary]                                                                 │
    # ╞═════════════════════════════════════════╪════════════════════════════════════════════════════════════════════════════════════════════════════════════════════════════════════╡
    # │ https://las-cn-beijing-publi-…          ┆ {processed_audio_path: "tos://tos_bucket/audio/audio_ffmpeg_wrapped/sample_processed.wav", processed_audio_binary: null}           │
    # ╰─────────────────────────────────────────┴────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────╯
```
