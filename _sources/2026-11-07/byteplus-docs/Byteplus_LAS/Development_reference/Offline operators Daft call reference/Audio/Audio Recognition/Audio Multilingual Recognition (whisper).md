---
title: "Audio Multilingual Recognition (whisper)"
product: "Lake AI Service"
product_code: "Byteplus_LAS"
source: "https://docs.byteplus.com/en/docs/Byteplus_LAS/Audio-Multilingual-Recognition-whisper"
---

<span id="operator-introduction"></span>
# Operator introduction

<span id="description"></span>
## Description

**AudioLidWhisper Audio Language Identification Processor**

<span id="core-features"></span>
## Core Features


* Audio decoding: Supports multiple audio formats → 16kHz waveform data

* Language detection: Identifies dozens of language codes based on the Whisper\-large model

* Full name mapping: Automatically converts language codes to full language names


<span id="technical-features"></span>
## Technical Features


* Loads models based on the ModelScope framework

* 16kHz sampling rate audio preprocessing pipeline


<span id="typical-application-scenarios"></span>
## Typical Application Scenarios


* ✅ Speech content analysis \- Multilingual audio classification

* ✅ Streaming media processing \- Real\-time language identification

* ✅ Speech datasets \- Automated language annotation


<span id="recommendations"></span>
## Recommendations


* It is recommended to first standardize upstream audio into wav format uniformly before performing language identification, which helps improve accuracy.


<span id="daft-call"></span>
# Daft call

<span id="operator-parameters"></span>
## Operator parameters

<span id="input"></span>
## Input


|Input column name |Note |
|---|---|
|audios |An array containing audio data Supported formats: \- Raw audio byte data \- Audio file path, e.g., TOS url, http url, local file path |


<span id="output"></span>
## Output

Structured array where each element contains:


* language_code: Language code

* language_code_full_name: Full English name of the language

    &nbsp;


<span id="parameters"></span>
## Parameters

If a parameter does not have a default value, it is a required parameter.


|Parameter name |Type |Default value |Description |
|---|---|---|---|
|model_path |str |/opt/las/models |Root path for model storage Default value: "/opt/las/models" |
|model_name |str |iic/speech_whisper\-large_lid_multilingual_pytorch |Pretrained model name Default value: "iic/speech_whisper\-large_lid_multilingual_pytorch" |
|model_version |str |v2.0.4 |Model version identifier Default value: "v2.0.4" |
|rank |int |0 |GPU device identifier Default value: 0 |


<span id="examples"></span>
## Examples

The following code shows how to use daft to run the operator for audio language identification.

```python
from __future__ import annotations

import logging
import os

import ray

import daft
from daft import col
from daft.las.functions.audio.audio_lid_whisper import AudioLidWhisper
from daft.las.functions.udf import las_udf

if __name__ == "__main__":
    if os.getenv("DAFT_RUNNER", "ray") == "ray":

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

        import ray

        ray.init(dashboard_host="0.0.0.0", runtime_env={"worker_process_setup_hook": configure_logging})
        daft.set_runner_ray()

    daft.set_execution_config(actor_udf_ready_timeout=600)
    daft.set_execution_config(min_cpu_per_task=0)

    tos_dir_url = os.getenv("TOS_DIR_URL", "las-cn-beijing-public-online.tos-cn-beijing.volces.com")
    samples = {
        "audio_path": [
            f"https://{tos_dir_url}/public/shared_audio_dataset/参观八达岭长城。.wav"
        ]
    }

    model_path = os.getenv("MODEL_PATH", "/opt/las/models")
    model_name = "iic/speech_whisper-large_lid_multilingual_pytorch"
    model_version = "v2.0.4"
    num_gpus = 1
    rank = 0

    df = daft.from_pydict(samples)
    df = df.with_column(
        "lid_result",
        las_udf(
            AudioLidWhisper,
            construct_args={
                "model_path": model_path,
                "model_name": model_name,
                "model_version": model_version,
                "rank": rank,
            },
            num_gpus=1,
            batch_size=1,
            concurrency=1,
        )(col("audio_path")),
    )
    df.show()

    # ╭────────────────────────────────┬────────────────────────────────────────────────────────────╮
    # │ audio_path                     ┆ lid_result                                                 │
    # │ ---                            ┆ ---                                                        │
    # │ Utf8                           ┆ Struct[language_code: Utf8, language_code_full_name: Utf8] │
    # ╞════════════════════════════════╪════════════════════════════════════════════════════════════╡
    # │ tos://las-cn-beijing-public-o… ┆ {language_code: zh,                                        │
    # │                                ┆ language_…                                                 │
    # ╰────────────────────────────────┴────────────────────────────────────────────────────────────╯
```
