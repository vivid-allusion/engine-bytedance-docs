---
title: "Voice Activity Detection (FSMN Model)"
product: "Lake AI Service"
product_code: "Byteplus_LAS"
source: "https://docs.byteplus.com/en/docs/Byteplus_LAS/Voice-Activity-Detection-FSMN"
---

<span id="operator-introduction"></span>
# Operator introduction

<span id="description"></span>
## Description

**Voice Activity Detection Module \- Efficient Audio Segmentation Solution Based on FSMN VAD**

<span id="core-features"></span>
## Core Features


* Voice Activity Detection: Automatically identifies the start and end times of speech segments in audio, enabling precise segmentation between speech and silence.

* Batch Processing: Supports efficient endpoint detection for large volumes of audio data.

* Multi\-format Input: Compatible with multiple audio input methods including raw binary, Base64 encoding, TOS/HTTP links, etc.

* GPU Acceleration: Supports high\-performance inference in GPU environments.


<span id="recommended-practices"></span>
## Recommended Practices


* It is recommended to input WAV format audio with 16k sampling rate and mono channel to improve detection accuracy.

* For long audio, it is suggested to process in segments; the duration of a single processing should not exceed 1 hour.

* Suitable for scenarios such as voice activity detection and speech segmentation.


<span id="supported-models"></span>
## Supported Models


* `iic/speech_fsmn_vad_zh-cn-16k-common-pytorch` (Chinese General FSMN VAD)


<span id="output-description"></span>
## Output Description


* Each audio outputs a 2D list of floating\-point numbers representing the start and end timestamps (unit: seconds) of all speech segments, e.g.: [[0.0, 4.34], [5.50, 7.12]]

* Returns None if processing fails.


<span id="daft-call"></span>
# Daft call

<span id="operator-parameters"></span>
## Operator parameters

<span id="input"></span>
## Input


|Input column name |Note |
|---|---|
|videos |Column containing audio data, supporting the following formats: \- audio_base64: base64 encoded audio string \- audio_url: URL path of the audio file \- audio_binary: raw audio byte data |


<span id="output"></span>
## Output

Column containing speech endpoint timestamps. Each element is a 2D float list representing the start and end timestamps (in seconds) of each speech segment in the audio, e.g., [[0.0, 4.34], [5.50, 7.12]]. If processing fails, it is None.

<span id="parameters"></span>
## Parameters

If a parameter does not have a default value, it is a required parameter.


|Parameter name |Type |Default value |Description |
|---|---|---|---|
|audio_src_type |str | |Audio format type Supported audio format types include: \- tos/http address (audio_url) \- base64 encoded (audio_base64) \- binary stream (audio_binary) Optional values: ["audio_binary", "audio_url", "audio_base64"] |
|batch_size_s |int |3600 |Batch processing duration in seconds Audio duration processed per batch (in seconds), only effective when using GPU. Default value: 3600 |
|model_path |str |/opt/las/models |Model path Local model storage path. Default value: "/opt/las/models" |
|model_name |str |iic/speech_fsmn_vad_zh\-cn\-16k\-common\-pytorch |Model name Model name used, including: \- iic/speech_fsmn_vad_zh\-cn\-16k\-common\-pytorch Optional values: ["iic/speech_fsmn_vad_zh\-cn\-16k\-common\-pytorch"] Default value: "iic/speech_fsmn_vad_zh\-cn\-16k\-common\-pytorch" |
|model_revision |str |v2.0.4 |Model revision Specified model version number, including: \- v2.0.4 Optional values: ["v2.0.4"] Default value: "v2.0.4" |
|rank |int |0 |Specifies the GPU device ID to use (effective in multi\-card environment). For example: 0 means the first GPU, 1 means the second GPU Default value: None |


<span id="examples"></span>
## Examples

<span id="the-following-code-shows-how-to-use-daft-to-run-the-operator-to-identify-speech-endpoints-in-audio"></span>
# The following code shows how to use daft to run the operator to identify speech endpoints in audio.

```python
from __future__ import annotations

import logging
import os

import ray

import daft
from daft import col
from daft.las.functions.audio.audio_vad_fsmn import AudioVadFsmn
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
    model_name = "iic/speech_fsmn_vad_zh-cn-16k-common-pytorch"
    audio_src_type = "audio_url"
    batch_size_s = 3600
    model_revision = "v2.0.4"
    rank = 0

    df = daft.from_pydict(samples)
    df = df.with_column(
        "audio_vad_result",
        las_udf(
            AudioVadFsmn,
            construct_args={
                "audio_src_type": audio_src_type,
                "model_path": model_path,
                "model_name": model_name,
                "model_revision": model_revision,
                "batch_size_s": batch_size_s,
                "rank": rank,
            },
            num_gpus=1,
            batch_size=1,
            concurrency=1,
        )(col("audio_path")),
    )
    df.show()

    # ╭────────────────────────────────┬─────────────────────╮
    # │ audio_path                     ┆ audio_vad_result    │
    # │ ---                            ┆ ---                 │
    # │ Utf8                           ┆ List[List[Float32]] │
    # ╞════════════════════════════════╪═════════════════════╡
    # │ tos://las-cn-beijing-public-o… ┆ [[0.51, 2.8]]       │
    # ╰────────────────────────────────┴─────────────────────╯
```
