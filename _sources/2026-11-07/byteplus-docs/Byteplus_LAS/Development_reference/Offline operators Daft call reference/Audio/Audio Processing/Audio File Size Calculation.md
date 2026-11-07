---
title: "Audio File Size Calculation"
product: "Lake AI Service"
product_code: "Byteplus_LAS"
source: "https://docs.byteplus.com/en/docs/Byteplus_LAS/Audio_File_Size_Calculation"
---

<span id="operator-introduction"></span>
# Operator introduction

<span id="description"></span>
## Description

**Audio file metadata analysis processor, accurately calculates file size**

<span id="core-features"></span>
## Core Features


* Accurately calculates audio file byte size

* Supports local files and TOS storage

* Lightweight and efficient, suitable for batch processing


<span id="format-support"></span>
## Format Support


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
|audio_paths |Column storing audio paths (tos or local path) |


<span id="output"></span>
## Output

Column storing audio file sizes

<span id="examples"></span>
## Examples

The following code shows how to use daft to run the operator to calculate audio file sizes.

```python
from __future__ import annotations

import os

import daft
from daft import col
from daft.las.functions.audio import AudioSize
from daft.las.functions.udf import las_udf

if __name__ == "__main__":

    # 音频文件从指定的 tos 路径读取，因此需要设置好环境变量以保证有权限读取 tos，包括：ACCESS_KEY,SECRET_KEY,TOS_ENDPOINT,TOS_REGION,TOS_TEST_DIR

    TOS_DIR = os.getenv("TOS_TEST_DIR", "tos_bucket")
    audio_tos_path = f"tos://{TOS_DIR}/audio_size/sample.mp3"
    
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

    samples = {
        "audio_path": [
            audio_tos_path
        ],
    }

    df = daft.from_pydict(samples)
    df = df.with_column("size_result", las_udf(AudioSize)(col("audio_path")))

    df.show()
    # ╭────────────────────────────────┬─────────────╮
    # │ audio_path                     ┆ size_result │
    # │ ---                            ┆ ---         │
    # │ Utf8                           ┆ Float32     │
    # ╞════════════════════════════════╪═════════════╡
    # │ tos://las-ai-cn-beijing/qa/op… ┆ 795426      │
    # ╰────────────────────────────────┴─────────────╯
```
