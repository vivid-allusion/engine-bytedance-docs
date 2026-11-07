---
title: "Audio to MP3"
product: "Lake AI Service"
product_code: "Byteplus_LAS"
source: "https://docs.byteplus.com/en/docs/Byteplus_LAS/Audio_to_MP3"
---

# Operator introduction

## Description

**Audio format conversion processor that converts various audio formats to MP3**

## Core Features:

* Supports converting multiple audio formats to MP3

* Customizable audio quality and encoding parameters

* Supports fine control of audio sample rate and bit rate

* Intelligent audio track selection (All/Auto/First)

* Supports local files, HTTP/HTTPS URLs, and TOS/S3 storage

## Format Support:

* Input: Mainstream audio formats like WAV, FLAC, AAC, M4A, OGG, WMA, APE, etc.

* Output: MP3 (.mp3)

* Audio codec: LAME MP3 encoder

* Sample rate: 8kHz\-96kHz

* Bit rate: 32kbps\-320kbps

# Daft call

## Operator parameters

## Input

|Input column name |Note |
|---|---|
|input_col |An array containing input audio paths (supports local paths, HTTP/HTTPS URLs, TOS/S3 URLs) |
|output_col |An array containing output MP3 file paths |

## Output

An array containing conversion result paths; returns the output path on success, None on failure

## Parameters

If a parameter does not have a default value, it is a required parameter.

|Parameter name |Type |Default value |Description |
|---|---|---|---|
|bitrate |str |192k |Audio bitrate, e.g., "128k", "192k", "256k", "320k" Default value: "192k" |
|sample_rate |int or None | |Audio sample rate, e.g., 22050, 44100,48000; keeps original sample rate if None Default value: None |
|audio_map |str |all |Audio track selection strategy: \- "all": Select all tracks (default) \- "auto": Intelligently select default track (automatically detect default flag) \- "first": Select only the first track Default value: "all" |
|quality |int |2 |MP3 encoding quality; range from 0\-9, where 0 is highest quality (slowest), and9 is lowest quality (fastest) Default value:2 |
|extra_params |list or None | |Extra ffmpeg parameter list, e.g., ["\-ac", "1"] Default value: None |
|timeout |int or None | |Timeout for processing a single audio (seconds); no limit if None Default value: None |

## Examples

The following code shows how to use Daft (for distributed scenarios) to run the operator for audio MP3 format conversion.

```python
from __future__ import annotations

import os

import daft
from daft import col
from daft.las.functions.audio import AudioConvertToMp3
from daft.las.functions.udf import las_udf

if __name__ == "__main__":
    # The converted audio is saved to the specified TOS path. Configure
    # ACCESS_KEY, SECRET_KEY, TOS_ENDPOINT, TOS_REGION, and TOS_TEST_DIR,
    # and provide an input audio URL that is reachable from BytePlus.
    INPUT_AUDIO_URL = os.environ["INPUT_AUDIO_URL"]
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
        "input_path": [INPUT_AUDIO_URL],
        "output_path": [f"tos://{TOS_TEST_DIR}/audio_convert_to_mp3/sample_converted.mp3"],
    }
    ds = daft.from_pydict(samples)

    # Using Daft to convert audio to MP3 format
    constructor_kwargs = {
        "bitrate": "192k",
        "sample_rate": 44100,
        "audio_map": "auto",
        "quality": 2,
        "extra_params": [],
    }

    ds = ds.with_column(
        "convert_result",
        las_udf(
            AudioConvertToMp3,
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
