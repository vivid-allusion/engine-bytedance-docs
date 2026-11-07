---
title: "Image Content Understanding (LLaVA Series Models)"
product: "Lake AI Service"
product_code: "Byteplus_LAS"
source: "https://docs.byteplus.com/en/docs/Byteplus_LAS/Image-Understanding-LLaVA"
---

<span id="operator-introduction"></span>
# Operator introduction

<span id="description"></span>
## Description

**LLaVA Multimodal Image Understanding Model \- Visual Semantic Parsing and Natural Language Description Generation**

<span id="core-features"></span>
## Core Features


* Multimodal Input Processing

   * Supports three image formats: `URL`, `Base64 encoding`, and `binary stream`

* Vision\-Language Joint Modeling

   * Achieves accurate mapping of image content to the semantic space

* Conversational Prompt Support

   * Guides generation direction via the `prompt` parameter

* Resource Usage

   * Recommended to use a GPU with 48G or more VRAM


<span id="scenario-optimization"></span>
## Scenario Optimization


* Chinese\-English Mixed Scenario Optimization: Special enhancement for Chinese semantics

* Supports resizing images to a consistent size first; it is recommended to set the image size according to the image and GPU conditions


<span id="daft-call"></span>
# Daft call

<span id="operator-parameters"></span>
## Operator parameters

<span id="input"></span>
## Input


|Input column name |Note |
|---|---|
|images |An array containing image data, elements are of type string or binary. |
|user_prompts | |


<span id="output"></span>
## Output

Processed array where each element is the visual understanding result of each image.

<span id="parameters"></span>
## Parameters

If a parameter does not have a default value, it is a required parameter.


|Parameter name |Type |Default value |Description |
|---|---|---|---|
|image_src_type |str |image_url |Format type of input images, supports: \- tos/http address (image_url) \- base64 encoding (image_base64) \- binary stream (image_binary) Optional values: ["image_url", "image_base64", "image_binary"] Default value: "image_url" |
|model_path |str |/opt/las/models |Absolute path for local model file storage, default is the preset path inside the container. Modify this path when using a custom model. Default value: "/opt/las/models" |
|model_name |str |LLaVA\-OneVision\-1.5\-8B\-Instruct |Supported vision\-language model versions; currently only supports LLaVA one vision series models. Optional values: ["LLaVA\-OneVision\-1.5\-8B\-Instruct", "LLaVA\-OneVision\-1.5\-4B\-Instruct"] Default value: "LLaVA\-OneVision\-1.5\-8B\-Instruct" |
|prompt |str |请给出这张图片的详细描述。 |Prompt for the user to understand the image content; the model generates the image description based on this prompt. Default value: "Please provide a detailed description of this image." |
|batch_size |int |4 |Number of samples processed in a single inference. Larger batch_size increases throughput but consumes more memory; adjust based on GPU memory. Default value: 4 |
|dtype |str |bfloat16 |Model inference precision selection: \- bfloat16: Balances precision and speed \- float16: Faster inference speed \- float32: Highest precision but maximum memory consumption Optional values: ["bfloat16", "float16", "float32"] Default value: "bfloat16" |
|use_flash_attention_2 |bool |True |Whether to use Flash Attention 2 to optimize attention computation (takes effect when CUDA\-compatible and dtype is 16\-bit float) Default value: True |
|max_caption_length |int |256 |Maximum number of tokens for the model\-generated description. Longer generation may include more details but increases computation time. Default value: 256 |
|resized_height |int or None | |Unified height (in pixels) to resize images during preprocessing; None retains original size. Increasing size preserves details but significantly increases memory usage. Default value: None |
|resized_width |int or None | |Unified width (in pixels) to resize images during preprocessing; None retains original size. Recommended to use with resized_height. Default value: None |
|do_sample |bool |False |Whether to enable sampling generation. When True, the model samples the next token probabilistically, leading to more diverse results; when False, greedy or beam search is used, leading to more deterministic results. Default value: False |
|temperature |float |1.0 |Sampling temperature, controls randomness of generated content. Higher values lead to more diverse generation; lower values lead to more conservative generation. Default value: 1.0 |
|top_k |int |50 |When sampling, select the next token only from the top k tokens with highest probability. Smaller k improves relevance of generation; larger k increases diversity. Default value:50 |
|top_p |float |1.0 |Cumulative probability threshold for nucleus sampling. Sample only from the set of tokens with cumulative probability greater than top_p, controlling diversity of generated content. Smaller values lead to more conservative generation; larger values lead to more diverse generation. Default value:1.0 |
|rank |int or None | |Specify the GPU device number to use (effective in multi\-card environment). For example: 0 means first GPU, 1 means second GPU Default value: None |


<span id="examples"></span>
## Examples

下面的代码展示了如何使用 daft 运行算子理解图像内容，并按照指令生成描述。

```python
from __future__ import annotations

import os

import daft
from daft import col
from daft.las.functions.multimodal.llava_one_vision_image_understanding import LlavaOneVisionImageUnderstanding
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
        "prompt": ["请给出图片的类型。"]  
    }

    image_src_type = "image_url"
    model_path = os.getenv("MODEL_PATH", "/opt/las/models")
    model_name = os.getenv("MODEL_NAME", "LLaVA-OneVision-1.5-8B-Instruct")
    dtype = "bfloat16"
    use_flash_attention_2 = True
    prompt = None
    max_caption_length = 256
    resized_height = None
    resized_width = None
    batch_size = 2
    rank = 0

    ds = daft.from_pydict(samples)
    ds = ds.with_column(
        "caption",
        las_udf(
            LlavaOneVisionImageUnderstanding,
            construct_args={
                "image_src_type": image_src_type,
                "model_path": model_path,
                "model_name": model_name,
                "dtype": dtype,
                "use_flash_attention_2": use_flash_attention_2,
                "prompt": prompt,
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

    # ╭────────────────────────────────┬────────────────────┬──────────────────────────────────────────────────────────╮
    # │ image_path                     ┆ prompt             ┆ caption                                                  │
    # │ ---                            ┆ ---                ┆ ---                                                      │
    # │ Utf8                           ┆ Utf8               ┆ Utf8                                                     │
    # ╞════════════════════════════════╪════════════════════╪══════════════════════════════════════════════════════════╡
    # │ tos://las-cn-beijing-public-o… ┆ 请给出图片的类型。    ┆ 这幅图片属于动画类型，具体来说是CGI（计算机生成图像）动…          │
    # ╰────────────────────────────────┴────────────────────┴──────────────────────────────────────────────────────────╯
```
