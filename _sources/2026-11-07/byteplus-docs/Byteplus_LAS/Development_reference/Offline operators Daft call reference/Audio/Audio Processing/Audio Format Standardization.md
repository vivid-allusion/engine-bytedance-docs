---
title: "Audio Format Standardization"
product: "Lake AI Service"
product_code: "Byteplus_LAS"
source: "https://docs.byteplus.com/en/docs/Byteplus_LAS/Audio_Format_Standardization"
---

<span id="operator-introduction"></span>
# Operator introduction

<span id="description"></span>
## Description

**Audio Standardization Module \- Unify audio to specified formats (sampling rate, channel, loudness, etc.)** 

<span id="core-features"></span>
## Core Features


* Supports sampling rate resampling

* Supports channel unification (e.g., convert to mono)

* Supports loudness normalization (target dBFS with limited gain range)

* Default input/output audio is in bytes format


<span id="usage-scenarios"></span>
## Usage Scenarios


* Unified processing of multi\-source audio data

* Preprocessing for downstream models like ASR/TTS

* Audio standardization step in multi\-modal content processing


<span id="daft-call"></span>
# Daft call

<span id="operator-parameters"></span>
## Operator parameters

<span id="input"></span>
## Input


|Input column name |Note |
|---|---|
|audio_col |PyArrow byte array of the input audio |


<span id="output"></span>
## Output

Processed audio result; returns None if failed.

<span id="parameters"></span>
## Parameters

If a parameter does not have a default value, it is a required parameter.


|Parameter name |Type |Default value |Description |
|---|---|---|---|
|target_sr |int or None | |Target sampling rate (unit: Hz), e.g., 16000 |
|target_channels |int or None | |Target number of channels, e.g., 1 for mono |
|target_dbfs |float or None | |Target loudness (unit: dBFS) |
|target_gain_range |list |[\-3, 3] |Allowed gain range during normalization, e.g., [\-3, 3] |
|num_coroutines |int |1 |Limit on the number of concurrent processes |


<span id="examples"></span>
## Examples

The following code shows how to use the Daft operator `AudioStandardization` to standardize audio data into a unified format, including sampling rate, channels, loudness, etc.

```python
# Copyright (c) Beijing Volcano Engine Technology Ltd.

from __future__ import annotations

import os

import daft
from daft import col
from daft.las.functions.audio.audio_standardization import AudioStandardization
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

    # 示例输入数据
    samples = {"audio_path": [f"https://{TOS_TEST_DIR_URL}/public/archive/audio_standardization/耙耙柑大叔.aac"]}

    # 构建 Daft DataFrame
    df = daft.from_pydict(samples)

    # 应用 AudioStandardization 算子
    df = df.with_column(
        "standardized_audio",
        las_udf(
            AudioStandardization,
            construct_args={
                "target_sr": 16000,
                "target_channels": 1,
                "target_dbfs": -20.0,
                "target_gain_range": [-3.0, 3.0],
            },
            num_cpus=1,
            batch_size=1,
            concurrency=2,
        )(col("audio_path")),
    )

    df.show()
    # ╭────────────────────────────────┬────────────────────────────────╮
    # │ audio_path                     ┆ standardized_audio             │
    # │ ---                            ┆ ---                            │
    # │ String                         ┆ Binary                         │
    # ╞════════════════════════════════╪════════════════════════════════╡
    # │ https://las-public-data-qa.to… ┆ b"RIFF\xd0\x9a\x08\x00WAVEfmt… │
    # ╰────────────────────────────────┴────────────────────────────────╯
```
