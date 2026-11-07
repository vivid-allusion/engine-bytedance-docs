---
title: "Audio Silence Detection"
product: "Lake AI Service"
product_code: "Byteplus_LAS"
source: "https://docs.byteplus.com/en/docs/Byteplus_LAS/Audio_Silence_Detection"
---

<span id="operator-introduction"></span>
# Operator introduction

<span id="description"></span>
## Description

**Audio Silence Detection Processor, intelligently identifies whether audio is completely silent**

<span id="core-features"></span>
## Core Features:


* Silence Detection: Analyzes the entire audio file to determine if it is silent

* Configurable Threshold: Supports custom sensitivity thresholds (dB) for silence detection

* Efficient Processing: Optimized volume analysis algorithm for fast processing speed

* Accurate Analysis: Determines silence status using professional volume detection technology

* Supports Local Files, HTTP/HTTPS URLs, and TOS/S3 Storage


<span id="format-support"></span>
## Format Support:


* Input: Mainstream audio formats such as MP3, WAV, FLAC, AAC, M4A, OGG, etc.

* Detection Algorithm: Based on professional volume analysis technology

* Sampling Rate: Automatically adapts to various sampling rates

* Channels: Supports mono and multi\-channel audio


<span id="detection-principle"></span>
## Detection Principle:


* Volume Threshold Detection: Analyzes the maximum and average volume of the audio

* Silence Judgment: When the maximum volume is below the set threshold, the audio is considered silent

* Lossless Analysis: Uses professional audio processing technology to ensure analysis accuracy


<span id="daft-call"></span>
# Daft call

<span id="operator-parameters"></span>
## Operator parameters

<span id="input"></span>
## Input


|Input column name |Note |
|---|---|
|audio_inputs |Column storing audio paths or binary data |


<span id="output"></span>
## Output

Boolean column storing silence detection results, where True indicates silence and False indicates non\-silence

<span id="parameters"></span>
## Parameters

If a parameter does not have a default value, it is a required parameter.


|Parameter name |Type |Default value |Description |
|---|---|---|---|
|silence_threshold_db |float |\-60.0 |Silence volume threshold (dB). Audio is considered silent if its maximum volume is below this value. Default: \-60.0 (dB) |
|timeout |int or None | |Timeout for processing a single audio file (seconds). No limit if set to None. Default: None |


<span id="examples"></span>
## Examples

The following code shows how to use Daft (suitable for distributed processing) to run the operator for audio silence detection.

```python
from __future__ import annotations

import os

import daft
from daft import col
from daft.las.functions.audio import AudioSilenceDetection
from daft.las.functions.udf import las_udf

if __name__ == "__main__":
    TOS_TEST_DIR_URL = os.getenv("TOS_TEST_DIR_URL", "las-cn-beijing-public-online.tos-cn-beijing.volces.com")

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
        "input_path": [
            f"https://{TOS_TEST_DIR_URL}/public/archive/audio_silence_detection/sample_silence.wav",
            f"https://{TOS_TEST_DIR_URL}/public/archive/audio_silence_detection/sample_speech.wav",
        ],
    }
    ds = daft.from_pydict(samples)

    # Using Daft to detect silence in audio files
    constructor_kwargs = {
        "silence_threshold_db": -60.0,
        "timeout": 30,
    }

    ds = ds.with_column(
        "is_silence",
        las_udf(
            AudioSilenceDetection,
            construct_args=constructor_kwargs,
            num_cpus=1,
            concurrency=1,
            batch_size=1,
        )(col("input_path")),
    )

    ds.show()
    # ╭────────────────────────────────┬────────────╮
    # │ input_path                     ┆ is_silence │
    # │ ---                            ┆ ---        │
    # │ String                         ┆ Bool       │
    # ╞════════════════════════════════╪════════════╡
    # │ https://las-public-data-qa.to… ┆ true       │
    # ├╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌┼╌╌╌╌╌╌╌╌╌╌╌╌┤
    # │ https://las-public-data-qa.to… ┆ false      │
    # ╰────────────────────────────────┴────────────╯
```
