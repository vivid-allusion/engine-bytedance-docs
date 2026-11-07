---
title: "Speech-to-Text (Whisper Series Models)"
product: "Lake AI Service"
product_code: "Byteplus_LAS"
source: "https://docs.byteplus.com/en/docs/Byteplus_LAS/Speech-to-Text-Whisper"
---

<span id="operator-introduction"></span>
# Operator introduction

<span id="description"></span>
## Description

**Speech Recognition Module \- A Multilingual Speech\-to\-Text Solution Based on the Whisper Model**

<span id="core-features"></span>
## Core Features


* Multilingual Recognition: Supports mainstream languages such as Chinese and English

* Speech Translation: Can translate recognition results into English


<span id="recommended-practices"></span>
## Recommended Practices


* Prioritize processing audio clips within 30 seconds

* Highest recognition accuracy in English scenarios


<span id="supported-models"></span>
## Supported Models


* `openai/whisper-large-v3-turbo`

* `openai/whisper-large-v3`

* `openai/whisper-medium` (Chinese support is average)

* `openai/whisper-small` (Outputs traditional Chinese for Chinese content)


<span id="language-support"></span>
## Language Support

For the complete list of supported languages, please refer to:

https://github.com/ggml\-org/whisper.cpp/blob/d682e150908e10caa4c15883c633d7902d385237/src/whisper.cpp#L248

<span id="daft-call"></span>
# Daft call

<span id="operator-parameters"></span>
## Operator parameters

<span id="input"></span>
## Input


|Input column name |Note |
|---|---|
|audios |An array containing audio data, supporting the following formats: \- audio_base64: Base64 encoded audio string; \- audio_url: Audio file URL path; \- audio_binary: Raw audio byte data |


<span id="output"></span>
## Output

A processed structured array where each element contains the following fields:


* asr_result: Speech recognition text result;

* timestamps: List of time stamp pairs (start/end time);

* segments: List of segmented text results

    &nbsp;


<span id="parameters"></span>
## Parameters

If a parameter does not have a default value, it is a required parameter.


|Parameter name |Type |Default value |Description |
|---|---|---|---|
|audio_src_type |str | |Audio format type Supported audio format types include: \- tos/http address (audio_url) \- base64 encoding (audio_base64) \- binary stream (audio_binary) Optional values: ["audio_binary", "audio_url", "audio_base64"] |
|model_path |str |/opt/las/models |Model storage path Default value: "/opt/las/models" |
|model_name |str |openai/whisper\-large\-v3 |Model name Supported Whisper series models: \- whisper\-small: Small model \- whisper\-medium: Medium model \- whisper\-large\-v3: Latest large model \- whisper\-large\-v3\-turbo: Optimized large model Optional values: [ "openai/whisper\-small", "openai/whisper\-medium", "openai/whisper\-large\-v3\-turbo", "openai/whisper\-large\-v3" ] Default value: "openai/whisper\-large\-v3" |
|batch_size |int |10 |Number of audio samples processed per batch Default value: 10 |
|source_language |str |chinese |Source language of the audio Supported: chinese/english/japanese/korean, etc. Default value: "chinese" |
|translate_to_english |bool |False |English translation mode Whether to translate the recognition result into English When enabled, the output text will be the English translation result Default value: False |
|condition_on_prev_tokens |bool |True |History dependency mode Whether to predict based on historical tokens Disabling it reduces result coherence but improves processing speed Default value: True |
|compression_ratio_threshold |float |1.35 |Text compression threshold Controls the compression level of generated text (suggested range 1.2\-2.0) A larger value retains more duplicate content Default value: 1.35 |
|temperature |float |0.5 |Temperature coefficient Controls the randomness of generated text (0.0\-1.0) Higher values are suitable for creative scenarios, lower values for deterministic scenarios Default value: 0.5 |
|logprob_threshold |float |\-1.0 |Log probability threshold Log probability threshold to filter words with too low confidence. If a word's log probability is lower than this value, it may be rejected. Default is \-1.0, which disables filtering and retains all words. |
|dtype |str |bfloat16 |Computation precision type Numerical precision used for model inference: \- bfloat16: Balanced precision and speed (default) \- float16: Faster inference speed \- float32: Highest precision Optional values: ["bfloat16", "float16", "float32"] Default value: "bfloat16" |
|rank |int |0 |GPU device number Specifies the GPU device ID to use (effective in multi\-card environment) Defaults to the first graphics card (ID=0) |


<span id="examples"></span>
## Examples

The following code shows how to use daft to run the operator to convert speech to text.

```python
from __future__ import annotations

import logging
import os

import ray

import daft
from daft import col
from daft.las.functions.audio.audio_asr_whisper import AudioAsrWhisper
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
    model_name = "openai/whisper-large-v3"
    audio_src_type = "audio_url"
    dtype = "bfloat16"
    source_language = "chinese"
    translate_to_english = False
    condition_on_prev_tokens = True
    compression_ratio_threshold = 1.35
    temperature = 0.5
    logprob_threshold = -1.0
    batch_size = 1
    rank = 0

    df = daft.from_pydict(samples)
    df = df.with_column(
        "asr_result_detail",
        las_udf(
            AudioAsrWhisper,
            construct_args={
                "audio_src_type": audio_src_type,
                "model_path": model_path,
                "model_name": model_name,
                "dtype": dtype,
                "source_language": source_language,
                "translate_to_english": translate_to_english,
                "condition_on_prev_tokens": condition_on_prev_tokens,
                "compression_ratio_threshold": compression_ratio_threshold,
                "temperature": temperature,
                "logprob_threshold": logprob_threshold,
                "batch_size": batch_size,
                "rank": rank,
            },
            num_gpus=1,
            batch_size=1,
            concurrency=1,
        )(col("audio_path")),
    )
    df.show()

    # ╭────────────────────────────────┬─────────────────────────────────────────────────────────────╮
    # │ audio_path                     ┆ asr_result_detail                                           │
    # │ ---                            ┆ ---                                                         │
    # │ Utf8                           ┆ Struct[asr_result: Utf8, timestamps: List[List[Float32]],   │
    # │                                ┆ segments: List[Utf8]]                                       │
    # ╞════════════════════════════════╪═════════════════════════════════════════════════════════════╡
    # │ tos://las-cn-beijing-publi-…   ┆ {asr_result: 参观八道岭长城,                                  │
    # │                                ┆ timesta…                                                    │
    # ╰────────────────────────────────┴─────────────────────────────────────────────────────────────╯
```
