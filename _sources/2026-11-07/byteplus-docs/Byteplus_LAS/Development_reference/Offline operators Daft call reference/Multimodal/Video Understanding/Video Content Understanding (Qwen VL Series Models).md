---
title: "Video Content Understanding (Qwen VL Series Models)"
product: "Lake AI Service"
product_code: "Byteplus_LAS"
source: "https://docs.byteplus.com/en/docs/Byteplus_LAS/Vedio-Understanding-qwen"
---

<span id="operator-introduction"></span>
# Operator introduction

<span id="description"></span>
## Description

**Qwen2.5\-VL Multimodal Video Understanding Model \- Temporal Semantic Parsing and Natural Language Description Generation**

<span id="core-features"></span>
## Core Features


* Multimodal Temporal Modeling

   * Supports three video formats: `URL`/`Base64 encoding`/`binary stream`

* Spatio\-Temporal Joint Modeling

   * Captures spatio\-temporal features and semantic correlations of videos

* Conversational Prompt Support

   * Guides generation direction via the `prompt` parameter

* Resource Usage

   * Recommended to use a GPU with 48G or more VRAM


<span id="optimization-features"></span>
## Optimization Features


* Optimization for Chinese\-English mixed scenarios: specially enhanced for Chinese semantics

* Supports resizing videos to a consistent dimension first; it is recommended to set the dimension based on video and GPU conditions


<span id="daft-call"></span>
# Daft call

<span id="operator-parameters"></span>
## Operator parameters

<span id="input"></span>
## Input


|Input column name |Note |
|---|---|
|videos |An array containing video data, where elements are of type string or binary. |
|user_prompts | |


<span id="output"></span>
## Output

A processed array where each element is the visual understanding result of the corresponding video.

<span id="parameters"></span>
## Parameters

If a parameter does not have a default value, it is a required parameter.


|Parameter name |Type |Default value |Description |
|---|---|---|---|
|video_src_type |str |video_url |Format type of the input video, supporting: \- tos/http address (video_url) \- base64 encoding (video_base64) \- binary stream (video_binary) Optional values: ["video_url", "video_base64", "video_binary"] Default value: "video_url" |
|model_path |str |/opt/las/models |Absolute path for storing local model files; default is the preset path inside the container. Modify this path when using a custom model. Default value: "/opt/las/models" |
|model_name |str |Qwen/Qwen2.5\-VL\-7B\-Instruct |Supported vision\-language model version; currently only supports Qwen2.5\-VL series models. Optional values: ["Qwen/Qwen2.5\-VL\-7B\-Instruct"] Default value: "Qwen/Qwen2.5\-VL\-7B\-Instruct" |
|prompt |str |请给出这段视频的详细描述。 |Prompt for the user to understand the video content; the model generates the video description based on this prompt. Default value: "Please provide a detailed description of this video." |
|batch_size |int |4 |Number of samples processed per inference run. A larger batch_size can improve throughput but increases memory consumption; adjust based on GPU memory. Default value:4 |
|dtype |str |bfloat16 |Model inference precision option: \- bfloat16: Balances precision and speed \- float16: Faster inference speed \- float32: Highest precision but maximum memory consumption Optional values: ["bfloat16", "float16", "float32"] Default value: "bfloat16" |
|use_flash_attention_2 |bool |True |Whether to use Flash Attention 2 to optimize attention computation (takes effect only if CUDA\-compatible and dtype is 16\-bit float). Default value: True |
|max_caption_length |int |256 |Maximum number of tokens for the model\-generated description. Longer generations may include more details but increase computation time. Default value:256 |
|min_pixels |int or None | |Minimum number of pixels for the video; if not set, uses the original video pixels by default. Larger video pixels result in higher GPU memory usage. Default value: None |
|max_pixels |int or None | |Maximum number of pixels for the video; if not set, uses the original video pixels by default. Larger video pixels result in higher GPU memory usage. Default value: None |
|fps |float or None | |Frame rate of the video; if not set, uses the original video frame rate by default. Higher frame rates result in higher GPU memory usage. Default value: None |
|do_sample |bool |False |Whether to enable sampling for generation. When True, the model samples the next token probabilistically, leading to more diverse results; when False, uses greedy or beam search for more deterministic results. Default value: False |
|temperature |float |1.0 |Sampling temperature, controlling the randomness of generated content. Higher values lead to more diverse outputs; lower values lead to more conservative outputs. Default value:1.0 |
|top_k |int |50 |When sampling, select the next token only from the top k tokens with the highest probability. Smaller k improves relevance; larger k increases diversity. Default value:50 |
|top_p |float |1.0 |Cumulative probability threshold for nucleus sampling. Sample only from the set of tokens with cumulative probability greater than top_p to control diversity of generated content. Smaller values lead to more conservative outputs; larger values lead to more diverse outputs. Default value:1.0 |
|rank |int or None | |Specifies the GPU device ID to use (effective in multi\-card environments). For example:0 means the first GPU,1 means the second GPU. Default value: None |


<span id="examples"></span>
## Examples

The code below shows how to use daft to run the operator for video content understanding and generate descriptions according to instructions.

```python
from __future__ import annotations

import logging
import os

import ray

import daft
from daft import col
from daft.las.functions.multimodal.qwen_vl_video_understanding import QwenVLVideoUnderstanding
from daft.las.functions.udf import las_udf

if __name__ == "__main__":
    os.environ["DAFT_RUNNER"] = "ray"

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
        "video_path": [
            f"https://{tos_dir_url}/public/shared_video_dataset/eating_56.mp4"
        ],
        "prompt": ["请给出视频的详细描述。"]  
    }

    video_src_type = "video_url"
    model_path = os.getenv("MODEL_PATH", "/opt/las/models")
    model_name = os.getenv("MODEL_NAME", "Qwen/Qwen2.5-VL-7B-Instruct")
    dtype = "bfloat16"
    use_flash_attention_2 = True
    default_prompt = None
    max_caption_length = 256
    min_pixels = 320 * 160
    max_pixels = 320 * 160
    fps = 1
    batch_size = 2
    rank = 0

    ds = daft.from_pydict(samples)
    ds = ds.with_column(
        "caption",
        las_udf(
            QwenVLVideoUnderstanding,
            construct_args={
                "video_src_type": video_src_type,
                "model_path": model_path,
                "model_name": model_name,
                "dtype": dtype,
                "use_flash_attention_2": use_flash_attention_2,
                "prompt": default_prompt,
                "max_caption_length": max_caption_length,
                "min_pixels": min_pixels,
                "max_pixels": max_pixels,
                "batch_size": batch_size,
                "rank": rank,
            },
            num_gpus=1,
            batch_size=2,
            concurrency=1,
        )(col("video_path"), col("prompt")),
    )

    ds.show()

    # ╭────────────────────────────────┬─────────────────────────┬─────────────────────────────────────────────────────────────╮
    # │ video_path                     ┆ prompt                  ┆ caption                                                     │
    # │ ---                            ┆ ---                     ┆ ---                                                         │
    # │ Utf8                           ┆ Utf8                    ┆ Utf8                                                        │
    # ╞════════════════════════════════╪═════════════════════════╪═════════════════════════════════════════════════════════════╡
    # │ tos://las-cn-beijing-public-o… ┆ 请给出视频的详细描述。…     ┆ 这是一段动画片段，画面中出现了一个卡通角色，它看起来像是一…          │
    # ╰────────────────────────────────┴─────────────────────────┴─────────────────────────────────────────────────────────────╯
```
