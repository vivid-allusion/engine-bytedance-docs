---
title: "Audio Content Understanding (Qwen Omni Model)"
product: "Lake AI Service"
product_code: "Byteplus_LAS"
source: "https://docs.byteplus.com/en/docs/Byteplus_LAS/Audio-Understanding-qwen"
---

<span id="operator-introduction"></span>
# Operator introduction

<span id="description"></span>
## Description

**Qwen2.5\-Omni Multimodal Audio Understanding Model \- Core Functions for Audio Content Parsing and Natural Language Description Generation**

<span id="core-functions"></span>
## Core Functions


* Intelligent Content Understanding and Description Generation

   * Automatically generate detailed and accurate natural language descriptions based on audio signals, supporting custom prompts via the prompt parameter

   * Supports audio formats such as mp3, acc, m4a, etc.

* Efficient Model Loading and Inference Optimization

   * Supports multiple computation precision options (bfloat16, float16, float32) to adapt to different performance requirements

   * Integrates FlashAttention2 acceleration technology to significantly improve inference efficiency

   * Supports automatic or manual device allocation, perfectly adapting to single\-card/multi\-card environments

* Resource Usage

   * Recommended to use GPUs with 48G or more VRAM


<span id="scenario-optimization"></span>
## Scenario Optimization


* Widely applicable to application scenarios such as audio content analysis, intelligent audio description, multimedia content understanding, etc.

* Built\-in batch processing mechanism to efficiently support parallel inference of large\-scale audio data

* Flexible configuration of audio data return options to meet diverse business needs


<span id="daft-call"></span>
# Daft call

<span id="operator-parameters"></span>
## Operator parameters

<span id="input"></span>
## Input


|Input column name |Note |
|---|---|
|contents |An array containing audio data, where elements are strings (file paths or URLs). |
|user_prompts | |


<span id="output"></span>
## Output

A processed array where elements are the text results of understanding each audio. For audio that fails to process, an empty string is returned.

<span id="parameters"></span>
## Parameters

If a parameter does not have a default value, it is a required parameter.


|Parameter name |Type |Default value |Description |
|---|---|---|---|
|model_path |str |/opt/las/models |Absolute path for storing local model files, default is the preset path inside the container. Modify this path when using a custom model. Default value: "/opt/las/models" |
|model_name |str |Qwen/Qwen2.5\-Omni\-7B |Supported multimodal model version; currently supports Qwen2.5\-Omni series models. Optional values: ["Qwen/Qwen2.5\-Omni\-7B"] Default value: "Qwen/Qwen2.5\-Omni\-7B" |
|prompt |str |请给出这个音频的详细描述。 |Prompt for the user to understand the audio content; the model generates the audio description based on this prompt. Default value: "Please provide a detailed description of this audio." |
|batch_size |int |4 |Number of samples processed in a single inference. A larger batch_size can improve throughput but increases memory consumption; adjust according to GPU memory. Default value:4 |
|dtype |str |bfloat16 |Model inference precision option: \- bfloat16: Balances precision and speed \- float16: Faster inference speed \- float32: Highest precision but maximum memory consumption Optional values: ["bfloat16", "float16", "float32"] Default value: "bfloat16" |
|use_flash_attention_2 |bool |True |Whether to use Flash Attention 2 to optimize attention computation (takes effect when CUDA\-compatible and dtype is 16\-bit float). Default value: True |
|max_caption_length |int |256 |Maximum number of tokens for the model\-generated description. Longer generation may include more details but increases computation time. Default value:256 |
|rank |int or None | |Specify the GPU device ID to use (valid in multi\-card environments). For example:0 means the first GPU,1 means the second GPU. Default value: None |


<span id="examples"></span>
## Examples

The following code shows how to use daft to run the operator to understand audio content and generate descriptions according to instructions.

```python
from __future__ import annotations

import os

import daft
from daft import col
from daft.las.functions.multimodal.qwen_omni_audio_understanding import QwenOmniAudioUnderstanding
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

    tos_dir_url = os.getenv("TOS_DIR_URL", "las-cn-beijing-public-online.tos-cn-beijing.volces.com")
    samples = {
        "audio_path": [
            f"https://{tos_dir_url}/public/shared_audio_dataset/黑神话悟空对话.mp3"
        ],
        "prompt": ["请直接将这个音频转换成文字，不要做任何解释。"],

    }

    model_path = os.getenv("MODEL_PATH", "/opt/las/models")
    model_name = "Qwen/Qwen2.5-Omni-7B"
    dtype = "bfloat16"
    use_flash_attention_2 = True
    default_prompt = None
    max_caption_length = 256
    batch_size = 1
    rank = 0
    num_gpus = int(os.getenv("NUM_GPUS", 1))
    num_gpus = 1

    ds = daft.from_pydict(samples)
    ds = ds.with_column(
        "caption",
        las_udf(
            QwenOmniAudioUnderstanding,
            construct_args={
                "model_path": model_path,
                "model_name": model_name,
                "dtype": dtype,
                "use_flash_attention_2": use_flash_attention_2,
                "prompt": default_prompt,
                "max_caption_length": max_caption_length,
                "batch_size": batch_size,
                "rank": rank,
            },
            num_gpus=num_gpus,
            batch_size=1,
            concurrency=1,
        )(col("audio_path"), col("prompt")),
    )
    print(ds.to_pandas()["caption"][0])

    ds.show()

    # ╭────────────────────────────────┬───────────────────────────────────────────────┬─────────────────────────────────────────────────────────────╮
    # │ audio_path                     ┆ prompt                                        ┆ caption                                                     │
    # │ ---                            ┆ ---                                           ┆ ---                                                         │
    # │ Utf8                           ┆ Utf8                                          ┆ Utf8                                                        │
    # ╞════════════════════════════════╪═══════════════════════════════════════════════╪═════════════════════════════════════════════════════════════╡
    # │ tos://las-cn-beijing-public-o… ┆ 请直接将这个音频转换成文字，不要做任何解释。…        ┆ 人我保住了，经我取到了。俺老孙啥功名不要，只求回到这花果山…           │
    # ╰────────────────────────────────┴───────────────────────────────────────────────┴─────────────────────────────────────────────────────────────╯
```
