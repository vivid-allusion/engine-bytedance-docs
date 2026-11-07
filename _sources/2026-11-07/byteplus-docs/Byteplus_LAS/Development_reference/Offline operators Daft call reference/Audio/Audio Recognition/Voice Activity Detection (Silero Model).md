---
title: "Voice Activity Detection (Silero Model)"
product: "Lake AI Service"
product_code: "Byteplus_LAS"
source: "https://docs.byteplus.com/en/docs/Byteplus_LAS/Voice-Activity-Detection"
---

<span id="operator-introduction"></span>
# Operator introduction

<span id="description"></span>
## Description

**Core Features**


* Speech endpoint detection: Automatically identify the start and end times of speech segments in audio, enabling accurate segmentation between speech and silence.

* Batch processing: Support efficient endpoint detection for large volumes of audio data.

* Multi\-format input: Compatible with various audio input methods such as raw binary, Base64 encoding, TOS/HTTP links.

* GPU acceleration: Supports high\-performance inference in GPU environments.

* Strong versatility: Performs excellently when processing audio from different domains with various background noises and quality levels.


<span id="recommended-practices"></span>
## Recommended Practices


* It is recommended to input WAV format audio with 8k/16k sampling rate and mono channel to improve detection accuracy.

* GPU speedup is not significant; in scenarios where extreme performance is not required, you can use CPU to infer the ONNX model.

* Suitable for scenarios such as speech activity detection and speech segmentation.


<span id="supported-models"></span>
## Supported Models


* silero_vad.onnx (corresponds to onnx_model_revision=16)

* silero_vad_16k_op15.onnx (corresponds to onnx_model_revision=15)

* silero_vad.jit


<span id="output-description"></span>
## Output Description


* Each audio outputs a 2D list of floating\-point numbers, representing the start and end timestamps (unit: seconds) of all speech segments, e.g., [[0.0, 4.34], [5.50, 7.12]].

* Returns None when processing fails.


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

Column containing voice activity detection timestamps. Each element is a 2D list of floats, representing the start and end timestamps (in seconds) of each speech segment in the audio, e.g., [[0.0, 4.34], [5.50, 7.12]]. If processing fails, it is None.

<span id="parameters"></span>
## Parameters

If a parameter does not have a default value, it is a required parameter.


|Parameter name |Type |Default value |Description |
|---|---|---|---|
|audio_src_type |str | |Audio format type Supported audio format types include: \- tos/http address (audio_url) \- base64 encoding (audio_base64) \- binary stream (audio_binary) Optional values: ["audio_binary", "audio_url", "audio_base64"] |
|model_path |str |/opt/las/models |Model path Local model storage path. Default value: "/opt/las/models" |
|model_name |str |silero\-vad |Model name Name of the model used, including: \- silero\-vad Optional values: ["silero\-vad"] Default value: "silero\-vad" |
|use_onnx_model |bool |True |Whether to use ONNX model Default value: True |
|onnx_model_revision |int |16 |ONNX model revision Optional values: [16, 15] Default value: 16 |


<span id="examples"></span>
## Examples

The following code shows how to use daft to run the operator to detect voice activity endpoints in speech.

```python
from __future__ import annotations

import logging
import os

import ray

import daft
from daft import col
from daft.las.functions.audio.audio_vad_silero import AudioVadSilero
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
    model_name = "silero-vad"
    audio_src_type = "audio_url"
    use_onnx_model = True
    onnx_model_revision = 16

    df = daft.from_pydict(samples)
    df = df.with_column(
        "audio_vad_result",
        las_udf(
            AudioVadSilero,
            construct_args={
                "audio_src_type": audio_src_type,
                "model_path": model_path,
                "model_name": model_name,
                "use_onnx_model": use_onnx_model,
                "onnx_model_revision": onnx_model_revision,
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
    # │tos://las-cn-beijing-public-on… ┆ [[0.8, 2.4]]        │
    # ╰────────────────────────────────┴─────────────────────╯
```
