---
title: "Image Content Understanding (Qwen VL Series Models)"
product: "Lake AI Service"
product_code: "Byteplus_LAS"
source: "https://docs.byteplus.com/en/docs/Byteplus_LAS/Image-Understanding-qwen"
---

<span id="operator-introduction"></span>
# Operator introduction

<span id="description"></span>
## Description

**Qwen2.5\-VL Multimodal Image Understanding Model \- Visual Semantic Parsing and Natural Language Description Generation**

<span id="core-features"></span>
## Core Features


* Multimodal Input Processing

   * Supports three image formats: `URL`, `Base64 encoding`, and `binary stream`

* Visual\-Language Joint Modeling

   * Achieves accurate mapping of image content to semantic space

* Conversational Prompt Support

   * Guides generation direction via the `prompt` parameter

* Resource Usage

   * Recommended to use a GPU with 48G or more VRAM


<span id="scene-optimization"></span>
## Scene Optimization


* Optimization for mixed Chinese\-English scenes: Special enhancement for Chinese semantics

* Supports resizing images to a consistent size first; it is recommended to set the image size according to the image and GPU conditions


<span id="daft-call"></span>
# Daft call

<span id="operator-parameters"></span>
## Operator parameters

<span id="input"></span>
## Input


|Input column name |Note |
|---|---|
|images |An array containing image data, where elements are of type string or binary. |
|user_prompts | |


<span id="output"></span>
## Output

A processed array where each element is the visual understanding result of the corresponding image.

<span id="parameters"></span>
## Parameters

If a parameter does not have a default value, it is a required parameter.


|Parameter name |Type |Default value |Description |
|---|---|---|---|
|image_src_type |str |image_url |The format type of the input image, supporting: \- tos/http address (image_url) \- base64 encoding (image_base64) \- binary stream (image_binary) Optional values: ["image_url", "image_base64", "image_binary"] Default value: "image_url" |
|model_path |str |/opt/las/models |The absolute path for storing local model files, defaulting to the preset path inside the container. Modify this path when using a custom model. Default value: "/opt/las/models" |
|model_name |str |Qwen/Qwen2.5\-VL\-7B\-Instruct |Supported vision\-language model version; currently only Qwen2.5\-VL series models are supported. Optional values: ["Qwen/Qwen2.5\-VL\-7B\-Instruct"] Default value: "Qwen/Qwen2.5\-VL\-7B\-Instruct" |
|prompt |str |请给出这张图片的详细描述。 |The prompt for the model to generate image descriptions based on user intent. Default value: "Please provide a detailed description of this image." |
|batch_size |int |4 |Number of samples processed in a single inference. A larger batch_size improves throughput but increases GPU memory consumption; adjust based on GPU memory. Default value:4 |
|dtype |str |bfloat16 |Model inference precision selection: \- bfloat16: Balances precision and speed \- float16: Faster inference speed \- float32: Highest precision but maximum GPU memory consumption Optional values: ["bfloat16", "float16", "float32"] Default value: "bfloat16" |
|use_flash_attention_2 |bool |True |Whether to use Flash Attention 2 to optimize attention computation (takes effect when CUDA\-compatible and dtype is 16\-bit floating point). Default value: True |
|max_caption_length |int |256 |Maximum number of tokens for the generated description. Longer lengths may include more details but increase computation time. Default value:256 |
|resized_height |int or None | |Height (in pixels) to uniformly resize the image during preprocessing; null retains original size. Increasing size preserves details but significantly increases GPU memory usage. Default value: None |
|resized_width |int or None | |Width (in pixels) to uniformly resize the image during preprocessing; null retains original size. Recommended to use with resized_height. Default value: None |
|do_sample |bool |False |Whether to enable sampling generation. When True, the model samples the next token probabilistically for diverse results; when False, greedy or beam search is used for deterministic results. Default value: False |
|temperature |float |1.0 |Sampling temperature that controls randomness. Higher values lead to more diverse outputs; lower values lead to more conservative outputs. Default value:1.0 |
|top_k |int |50 |Select the next token only from the top k tokens with highest probability during sampling. Smaller k improves relevance; larger k increases diversity. Default value:50 |
|top_p |float |1.0 |Cumulative probability threshold for nucleus sampling. Sample only from tokens with cumulative probability \> top_p to control diversity. Smaller values are more conservative; larger values are more diverse. Default value:1.0 |
|rank |int or None | |Specify the GPU device ID to use (valid in multi\-card environments). E.g., 0 for first GPU,1 for second GPU. Default value: None |


<span id="examples"></span>
## Examples

The following code demonstrates how to use daft to run the operator for image content understanding and generate descriptions as instructed.

```python
from __future__ import annotations

import os

import daft
from daft import col
from daft.las.functions.multimodal.qwen_vl_image_understanding import QwenVLImageUnderstanding
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
        "image_path": [
            f"https://{tos_dir_url}/public/shared_image_dataset/cat_ip_adapter.jpeg"
        ],
        "prompt": ["请给出图片的详细描述。"],
    }
    
    image_src_type = "image_url"
    model_path = os.getenv("MODEL_PATH", "/opt/las/models")
    model_name = os.getenv("MODEL_NAME", "Qwen/Qwen2.5-VL-7B-Instruct")
    dtype = "bfloat16"
    use_flash_attention_2 = True
    default_prompt = None
    max_caption_length = 256
    resized_height = None
    resized_width = None
    batch_size = 2
    rank = 0

    ds = daft.from_pydict(samples)
    ds = ds.with_column(
        "caption",
        las_udf(
            QwenVLImageUnderstanding,
            construct_args={
                "image_src_type": image_src_type,
                "model_path": model_path,
                "model_name": model_name,
                "dtype": dtype,
                "use_flash_attention_2": use_flash_attention_2,
                "prompt": default_prompt,
                "max_caption_length": max_caption_length,
                "resized_height": resized_height,
                "resized_width": resized_width,
                "batch_size": batch_size,
                "rank": rank,
            },
            num_gpus=1,
            batch_size=2,
            concurrency=1,
        )(col("image_path"), col("prompt")),
    )

    ds.show()

    # ╭────────────────────────────────┬────────────────────┬─────────────────────────────────────────────────────────────╮
    # │ image_path                     ┆ prompt             ┆ caption                                                     │
    # │ ---                            ┆ ---                ┆ ---                                                         │
    # │ Utf8                           ┆ Utf8               ┆ Utf8                                                        │
    # ╞════════════════════════════════╪════════════════════╪═════════════════════════════════════════════════════════════╡
    # │ tos://las-cn-beijing-public-o… ┆ 请给出图片的详细描述。 ┆ 这张图片展示了一只拟人化的猫，它穿着一套复古风格的服装， …           │
    # ╰────────────────────────────────┴────────────────────┴─────────────────────────────────────────────────────────────╯
```
