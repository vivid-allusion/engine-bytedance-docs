---
title: "Audio segment splitting (by duration)"
product: "Lake AI Service"
product_code: "Byteplus_LAS"
source: "https://docs.byteplus.com/en/docs/Byteplus_LAS/Audio-segment-splitting-duration"
---

<span id="operator-introduction"></span>
# Operator introduction

<span id="description"></span>
## Description

**Split audio by duration, supporting splitting audio clips into fixed\-length segments**

<span id="core-features"></span>
## Core Features


* Split audio into multiple segments according to the specified duration

* Support multiple input formats:

* Local file path

* TOS/S3 storage path

* Binary data stream

* Support binary output of segments or storage to TOS

* Support filtering segments by minimum duration


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
|audio_paths |Optional, column containing audio file paths |
|audio_binaries |Optional, column containing audio binary data |
|audio_formats |Optional, column containing audio format strings, must be specified when audio_binaries is provided |
|output_basenames |Optional, column containing specified file names |


<span id="output"></span>
## Output

A struct array containing audio segmentation results:


* segments: List of segment paths

* binaries: List of segment binary data (optional)


<span id="parameters"></span>
## Parameters

If a parameter does not have a default value, it is a required parameter.


|Parameter name |Type |Default value |Description |
|---|---|---|---|
|output_tos_dir |str | |Path where the split audio segments are saved to TOS |
|output_segments_binary |bool |False |Whether to return the binary data of the split audio segments |
|segment_duration |float |5.0 |Duration of each segment (unit: seconds) |
|min_segment_duration |float |0.0 |Minimum segment duration (unit: seconds) |
|output_format |str or None | |Globally specify the output audio format (e.g., "mp3", "wav", etc.), priority is higher than input file suffix and audio_format column |


<span id="examples"></span>
## Examples

The following code shows how to use Daft (for distributed processing) to run the operator to split audio by duration.

```python
from __future__ import annotations

import os

import daft
from daft import col
from daft.las.functions.audio import AudioSplitByDuration
from daft.las.functions.udf import las_udf

if __name__ == "__main__":

    # 更改完切分的音频会保存到指定的TOS路径下，因此，需要设置好环境变量以保证有权限写入TOS，包括：ACCESS_KEY,SECRET_KEY,TOS_ENDPOINT,TOS_REGION,TOS_TEST_DIR
    TOS_DIR = os.getenv("TOS_TEST_DIR", "tos_bucket")
    output_tos_dir = f"tos://{TOS_DIR}/audio/audio_split_by_duration"

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

    tos_dir_url = os.getenv("TOS_DIR_URL", "las-cn-beijing-public-online.tos-cn-beijing.volces.com")
    samples = {
        "audio_path": [f"https://{tos_dir_url}/public/shared_audio_dataset/sample.mp3"],
    }
    ds = daft.from_pydict(samples)

    constructor_kwargs = {
        "output_tos_dir": output_tos_dir,
        "output_segments_binary": True,
        "segment_duration": 10.0,
        "min_segment_duration": 1.0,
    }

    ds = ds.with_column(
        "split_results",
        las_udf(AudioSplitByDuration, construct_args=constructor_kwargs)(col("audio_path")),
    )

    ds.show()
    # ╭────────────────────────────────┬────────────────────────────────────────────────────────────╮
    # │ audio_path                     ┆ split_results                                             │
    # │ ---                            ┆ ---                                                       │
    # │ Utf8                           ┆ Struct[segments: List[Utf8], binaries: List[Binary]]      │
    # ╞════════════════════════════════╪════════════════════════════════════════════════════════════╡
    # │ https://las-cn-beijing-publi-… ┆ {segments: [tos://tos_bucket/audio/audio_split_by_duration… │
    # ╰────────────────────────────────┴────────────────────────────────────────────────────────────╯
```
