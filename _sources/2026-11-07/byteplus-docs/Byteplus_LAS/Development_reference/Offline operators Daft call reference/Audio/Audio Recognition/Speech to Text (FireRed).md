---
title: "Speech to Text (FireRed)"
product: "Lake AI Service"
product_code: "Byteplus_LAS"
source: "https://docs.byteplus.com/en/docs/Byteplus_LAS/Speech-to-Text-FireRed"
---

<span id="operator-introduction"></span>
# Operator introduction

<span id="description"></span>
## Description

**Speech Recognition Module \- A Multilingual Speech\-to\-Text Solution Based on FireRed ASR Models**

<span id="core-features"></span>
## Core Features


* Multilingual Recognition: Supports Chinese, English, and Chinese dialects

* Multiple Model Options: Supports various models including AED and LLM models

* Audio Type: Supports mono\-channel WAV audio files with 16K sampling rate


<span id="recommended-practices"></span>
## Recommended Practices


* To ensure recognition accuracy, for AED models, it is recommended that the audio length does not exceed 60 seconds; for LLM models, the audio length should not exceed 30 seconds

* When performing batch inference with LLM models, it is recommended to ensure that the audio lengths are not significantly different. If the differences are large, set batch_size=1

* It is recommended to standardize the audio before use to convert it into the format supported by this operator


<span id="supported-models"></span>
## Supported Models


* `FireRedASR-AED-L`

* `FireRedASR-LLM-L`


<span id="daft-call"></span>
# Daft call

<span id="operator-parameters"></span>
## Operator parameters

<span id="input"></span>
## Input


|Input column name |Note |
|---|---|
|contents |An array containing audio data, with elements of string type (file paths or URLs). Supports local file paths and remote file links starting with tos://, s3://, http://, or https:// |
|contents_ids |An array containing audio data, with elements of string type, used to uniquely identify audio. Default value: None |


<span id="output"></span>
## Output

A processed array where each element is the understanding result text of the corresponding audio. For audio that fails to process, an empty string is returned.

<span id="parameters"></span>
## Parameters

If a parameter does not have a default value, it is a required parameter.


|Parameter name |Type |Default value |Description |
|---|---|---|---|
|audio_src_type |str | |Audio format type Supported audio format types include: \- tos/http address (audio_url) \- base64 encoding (audio_base64) \- binary stream (audio_binary) Optional values: ["audio_binary", "audio_url", "audio_base64"] |
|model_path |str |/opt/las/models |Model storage path Default value: "/opt/las/models" |
|model_name |str |FireRedAsr/FireRedASR\-AED\-L |Model name Supported FireRed series models: \- FireRedAsr/FireRedASR\-AED\-L: Small model \- FireRedAsr/FireRedASR\-LLM\-L: Large model Optional values: [ "FireRedAsr/FireRedASR\-AED\-L", "FireRedAsr/FireRedASR\-LLM\-L" ] Default value: "FireRedAsr/FireRedASR\-AED\-L" |
|batch_size |int |1 |Number of audio samples processed per batch Default value: 1 |
|beam_size |int |3 |Beam width during decoding Controls the size of the search space during decoding; a larger value may improve recognition accuracy but reduce speed Default value:3 |
|decode_min_len |int |0 |Minimum decoding length Limits the minimum length of the output text; 0 means no limit Default value:0 |
|decode_max_len |int |0 |Maximum decoding length Limits the maximum length of the output text;0 means no limit Default value:0 |
|nbest |int |1 |Number of candidate outputs for the AED model Controls the number of candidate texts output; only valid for the AED model Default value:1 |
|softmax_smoothing |float |1.25 |Softmax smoothing coefficient for the AED model Adjusts the smoothness of the softmax distribution; only valid for the AED model Default value:1.25 |
|aed_length_penalty |float |0.6 |Length penalty for the AED model Controls the penalty coefficient for the length of the output text; only valid for the AED model Default value:0.6 |
|eos_penalty |float |1.0 |EOS penalty for the AED model Controls the penalty coefficient for the end\-of\-sequence token; only valid for the AED model Default value:1.0 |
|repetition_penalty |float |3.0 |Repetition penalty for the LLM model Controls the penalty coefficient for repeated content when generating text; only valid for the LLM model Default value:3.0 |
|llm_length_penalty |float |1.0 |Length penalty for the LLM model Controls the penalty coefficient for the length of the generated text; only valid for the LLM model Default value:1.0 |
|temperature |float |1.0 |Temperature coefficient Controls the randomness of generated text (range:0.0\-1.0). Higher values are suitable for creative scenarios, while lower values are suitable for deterministic scenarios Default value:1.0 |
|use_fp16 |bool |False |Whether to use FP16 inference Whether to enable half\-precision floating\-point acceleration for inference to save video memory Default value: False |


<span id="examples"></span>
## Examples

The following code shows how to use daft to run the operator to convert speech to text.

```python
from __future__ import annotations

import logging
import os

import daft
from daft import col
from daft.las.functions.audio.audio_asr_firered import AudioAsrFireRed
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
            f"https://{tos_dir_url}/public/shared_audio_dataset/sample_normal.wav"
        ]
    }

    model_path = os.getenv("MODEL_PATH", "/opt/las/models")
    audio_src_type = "audio_url"
    beam_size = 3
    decode_min_len = 0
    decode_max_len = 100
    nbest = 1
    softmax_smoothing = 1.25
    aed_length_penalty = 0.6
    eos_penalty = 1.0
    repetition_penalty = 3.0
    llm_length_penalty = 1.0
    temperature = 1.0
    use_fp16 = True
    batch_size = 1
    num_gpus = 1

    df = daft.from_pydict(samples)

    # 每个UDF都需要1个GPU，如果只有一个GPU，请注释掉一个UDF的代码只运行另一个
    df = df.with_column(
        "asr_result_aed",
        las_udf(
            AudioAsrFireRed,
            construct_args={
                "audio_src_type": audio_src_type,
                "model_path": model_path,
                "model_name": "FireRedAsr/FireRedASR-AED-L",
                "batch_size": batch_size,
                "beam_size": beam_size,
                "decode_min_len": decode_min_len,
                "decode_max_len": decode_max_len,
                "nbest": nbest,
                "softmax_smoothing": softmax_smoothing,
                "aed_length_penalty": aed_length_penalty,
                "eos_penalty": eos_penalty,
            },
            num_gpus=num_gpus,
            batch_size=1,
            concurrency=1,
        )(col("audio_path")),
    )

    df = df.with_column(
        "asr_result_llm",
        las_udf(
            AudioAsrFireRed,
            construct_args={
                "audio_src_type": audio_src_type,
                "model_path": model_path,
                "model_name": "FireRedAsr/FireRedASR-LLM-L",
                "batch_size": batch_size,
                "beam_size": beam_size,
                "decode_min_len": decode_min_len,
                "decode_max_len": decode_max_len,
                "repetition_penalty": repetition_penalty,
                "llm_length_penalty": llm_length_penalty,
                "use_fp16": use_fp16,
                "temperature": temperature,
            },
            num_gpus=num_gpus,
            batch_size=1,
            concurrency=1,
        )(col("audio_path")),
    )
    df.show()

    # ╭────────────────────────────────┬────────────────────────────────────────────┬───────────────────────────────────────────╮
    # │ audio_path                     ┆ asr_result_aed                             ┆ asr_result_llm                            │
    # │ ---                            ┆ ---                                        ┆ ---                                       │
    # │ Utf8                           ┆ Utf8                                       ┆ Utf8                                      │
    # ╞════════════════════════════════╪════════════════════════════════════════════╪═══════════════════════════════════════════╡
    # │ https://las-cn-beijing-publ…   ┆ 人我保住了金我取到了俺老孙啥功名不要只求回        ┆ 人我保住了金我取到了俺老孙啥功名不要只求         │
    # │                                ┆ 到这花果山终老过…                             ┆ 回到这花果山中了过…                          │
    # ╰────────────────────────────────┴────────────────────────────────────────────┴───────────────────────────────────────────╯
```
