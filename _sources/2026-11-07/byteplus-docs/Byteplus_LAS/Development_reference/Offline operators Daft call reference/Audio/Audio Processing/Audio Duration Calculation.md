---
title: "Audio Duration Calculation"
product: "Lake AI Service"
product_code: "Byteplus_LAS"
source: "https://docs.byteplus.com/en/docs/Byteplus_LAS/Audio_Duration_Calculation"
---

<span id="operator-introduction"></span>
# Operator introduction

<span id="description"></span>
## Description

**Audio Duration Analysis Processor: accurately calculates audio content duration**

<span id="core-features"></span>
## Core Features


* Accurately calculates audio duration (second\-level precision)

* Supports local files, TOS storage, and binary data

* Based on the librosa professional audio processing library


<span id="supported-formats"></span>
## Supported Formats


* MP3 (.mp3)

* WAV (.wav)

* FLAC (.flac)

* OGG (.ogg)

* AAC (.aac)

* M4A (.m4a)


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

Column storing audio duration

<span id="examples"></span>
## Examples

The following code shows how to use daft to run the operator to calculate the duration of audio files.

```python
from __future__ import annotations

import os

import daft
from daft import col
from daft.las.functions.audio import AudioDuration
from daft.las.functions.udf import las_udf

if __name__ == "__main__":
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
        ],
    }
    df = daft.from_pydict(samples)

    # 使用 Daft 进行分布式处理
    df = df.with_column("duration_result", las_udf(AudioDuration)(col("audio_path")))

    df.show()
    # ╭────────────────────────────────┬─────────────────╮
    # │ audio_path                     ┆ duration_result │
    # │ ---                            ┆ ---             │
    # │ Utf8                           ┆ Float32         │
    # ╞════════════════════════════════╪═════════════════╡
    # │ https://las-cn-beijing-publ-…  ┆ 49.711          │
    # ╰────────────────────────────────┴─────────────────╯
```
