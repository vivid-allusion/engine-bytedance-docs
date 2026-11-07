---
title: "Audio Segment Segmentation (with Timestamps)"
product: "Lake AI Service"
product_code: "Byteplus_LAS"
source: "https://docs.byteplus.com/en/docs/Byteplus_LAS/Audio-Segment-Segmentation-Timestamps"
---

<span id="operator-introduction"></span>
# Operator introduction

<span id="description"></span>
## Description

**Audio timestamp segmentation processor, supporting precise segment extraction.** 

<span id="core-features"></span>
## Core Features


* Accurately split audio based on timestamps

* Supports multiple input formats:

* Local file path

* TOS storage path

* Binary data stream

* Supports binary output of segments or TOS storage


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
|timestamp_ranges |Required, column containing timestamp ranges for splitting. The input format is [[0.0, 5.0], [5.0, 10.0]], with the unit in seconds. |
|audio_paths |Optional, column containing audio file paths |
|audio_binaries |Optional, column containing audio binary data |
|audio_formats |Optional, column containing audio format strings; must be specified when audio_binaries is specified |
|output_basenames |Optional, column containing specified filenames |


<span id="output"></span>
## Output

A struct containing audio splitting results:


* segments: List of segment paths

* binaries: List of segment binary data (optional)


<span id="parameters"></span>
## Parameters

If a parameter does not have a default value, it is a required parameter.


|Parameter name |Type |Default value |Description |
|---|---|---|---|
|output_tos_dir |str | |Path where split audio segments are saved to TOS. |
|output_segments_binary |bool |False |Whether to return binary data of split audio segments. |
|output_format |str or None | |Globally specifies output audio format (e.g., "mp3", "wav"), with higher priority than input file extension and audio_format column. |


<span id="examples"></span>
## Examples

下面的代码展示了如何使用 Daft（适用于分布式）运行算子对音频按时间戳切分。

```python
from __future__ import annotations

import os

import daft
from daft import col
from daft.las.functions.audio import AudioSplitByTimestamps
from daft.las.functions.udf import las_udf

if __name__ == "__main__":

    # 更改完切分的音频会保存到指定的TOS路径下，因此，需要设置好环境变量以保证有权限写入TOS，包括：ACCESS_KEY,SECRET_KEY,TOS_ENDPOINT,TOS_REGION,TOS_TEST_DIR
    TOS_DIR = os.getenv("TOS_TEST_DIR", "tos_bucket")
    output_tos_dir = f"tos://{TOS_DIR}/audio/audio_split_by_timestamps"
    
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
        "timestamps": [[[0.0, 5.0], [5.0, 10.0], [10.0, 15.0]]],
    }
    ds = daft.from_pydict(samples)

    constructor_kwargs = {
        "output_tos_dir": output_tos_dir,
        "output_segments_binary": True,
        "output_audio_format": True,
    }

    # 使用 Daft 进行分布式处理
    ds = ds.with_column(
        "split_results",
        las_udf(AudioSplitByTimestamps, construct_args=constructor_kwargs)(col("timestamps"), col("audio_path")),
    )

    ds.show()
    # ╭────────────────────────────────┬─────────────────────────────┬───────────────────────────────────────────────────────────────────────────╮
    # │ audio_path                     ┆ timestamps                  ┆ split_results                                                             │
    # │ ---                            ┆ ---                         ┆ ---                                                                       │
    # │ Utf8                           ┆ List[List[Float64]]         ┆ Struct[segments: List[Utf8], binaries: List[Binary], formats: List[Utf8]] │
    # ╞════════════════════════════════╪═════════════════════════════╪═══════════════════════════════════════════════════════════════════════════╡
    # │ https://las-cn-beijing-publi-… ┆ [[0, 5], [5, 10], [10, 15]] ┆ {segments: ["tos://tos_bucket/audio/audio_split_by_timestamps/segment_1.… │
    # ╰────────────────────────────────┴─────────────────────────────┴───────────────────────────────────────────────────────────────────────────╯
```
