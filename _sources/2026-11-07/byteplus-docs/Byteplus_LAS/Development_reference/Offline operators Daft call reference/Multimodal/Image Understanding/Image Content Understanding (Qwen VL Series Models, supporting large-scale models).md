---
title: "Image Content Understanding (Qwen VL Series Models, supporting large-scale models)"
product: "Lake AI Service"
product_code: "Byteplus_LAS"
source: "https://docs.byteplus.com/en/docs/Byteplus_LAS/Image-Understanding-qwen-vl"
---

<span id="operator-introduction"></span>
# Operator introduction

<span id="description"></span>
## Description

**Qwen2.5\-VL multimodal image understanding model supports visual semantic parsing and natural language description generation, suitable for various image analysis scenarios.** 

<span id="key-features"></span>
## Key Features


* Multimodal temporal modeling: Supports three image input formats (URL, Base64 encoding, binary stream), flexibly adapting to different data sources.

* Conversational prompt support: Customize generation direction via the `prompt` parameter to meet diverse business needs.

* Efficient inference: Integrates VLLM inference engine, supports three precisions (`bfloat16`, `float16`, `float32`), making full use of GPU computing power.

* Recommend using GPUs with 48G or more VRAM


<span id="applicable-scenarios"></span>
## Applicable Scenarios


* Image content understanding and summarization

* Intelligent monitoring and event analysis

* Multimodal dialogue and interaction

* Other AI applications requiring image semantic parsing


<span id="notes"></span>
## Notes


* Only supports GPU environments; it is recommended to set parameters reasonably according to VRAM and business needs.

* It is recommended to unify images before inference to achieve the best results.


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

A processed array where each element is the understanding result of the corresponding image.

<span id="parameters"></span>
## Parameters

If a parameter does not have a default value, it is a required parameter.


|Parameter name |Type |Default value |Description |
|---|---|---|---|
|image_src_type |str |image_url |The format type of the input image. Supported types: \- "image_url": TOS/HTTP address \- "image_base64": Base64 encoded string \- "image_binary": Binary stream Optional values: ["image_url", "image_base64", "image_binary"] Default value: "image_url" |
|model_path |str |/opt/las/models |Absolute path for storing local model files. Defaults to the preset path inside the container; modify this path when using a custom model. Default value: "/opt/las/models" |
|model_name |str |Qwen/Qwen2.5\-VL\-7B\-Instruct |Supported vision\-language model version. Currently only supports Qwen2.5\-VL series models. Optional values: ["Qwen/Qwen2.5\-VL\-7B\-Instruct\-AWQ", "Qwen/Qwen2.5\-VL\-7B\-Instruct", "Qwen/Qwen2.5\-VL\-32B\-Instruct\-AWQ", "Qwen/Qwen2.5\-VL\-32B\-Instruct"] Default value: "Qwen/Qwen2.5\-VL\-7B\-Instruct" |
|prompt |str |请给出这张图片的详细描述。 |Prompt for users to understand video content; the model generates video descriptions based on this prompt. When set to empty, it is recommended to pass a specific prompt for each data entry. Default value: "Please provide a detailed description of this video." |
|batch_size |int |4 |Number of samples processed in a single inference. A larger batch_size increases throughput but consumes more GPU memory; adjust based on available GPU memory. Default value:4 |
|dtype |str |bfloat16 |Model inference precision option. \- "bfloat16": Balances precision and speed \- "float16": Faster inference speed \- "float32": Highest precision but maximum memory consumption Optional values: ["bfloat16", "float16", "float32"] Default value: "bfloat16" |
|max_model_len |int |128000 |Maximum supported input length (in tokens) for the model; affects the length of video descriptions that can be processed, cannot exceed 128000. Default value:128000 |
|max_num_seqs |int |128 |Maximum number of sequences per batch; affects concurrent inference capability. Default value:128 |
|tensor_parallel_size |int |1 |Number of GPUs for tensor parallelism; improves inference speed. Default value:1 |
|enable_prefix_caching |bool |True |Whether to enable prefix caching to accelerate multi\-turn inference. Default value:True |
|gpu_memory_utilization |float |0.9 |Maximum GPU memory utilization per card; range from 0 to1. Default value:0.9 |
|enforce_eager |bool |False |Whether to force eager mode for inference; useful for debugging or special scenarios. Default value:False |
|resized_height |int or None | |Image height. If not set, uses the original image height by default. Larger height increases GPU memory consumption. Default value:None |
|resized_width |int or None | |Image width. If not set, uses the original image width by default. Larger width increases GPU memory consumption. Default value:None |
|temperature |float |1.0 |Sampling temperature; controls the diversity of generated content. Higher values lead to more random outputs. Default value:1.0 |
|top_p |float |0.2 |Probability threshold for nucleus sampling; controls diversity of generated content. Smaller values lead to more conservative outputs. Default value:0.2 |
|repetition_penalty |float |1.05 |Repetition penalty coefficient; prevents repetitive content. Larger values reduce repetition. Default value:1.05 |
|max_tokens |int |8192 |Maximum number of tokens generated in a single output; affects description length. Default value:8192 |
|stop_token_ids |list |[] |Stop generation when these token IDs are encountered; used for custom termination conditions. Default value:[] |
|seed |int |42 |Random seed; ensures reproducibility of inference results. Default value:42 |


<span id="examples"></span>
## Examples

The following code shows how to use daft to run the operator to understand image content and generate descriptions according to instructions.

```python
from __future__ import annotations

import logging
import os

import ray

import daft
from daft import col
from daft.las.functions.multimodal.qwen_vl_image_understanding_vllm import QwenVLImageUnderstandingVLLM
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
        "image_path": [
            f"https://{tos_dir_url}/public/shared_image_dataset/cat_ip_adapter.jpeg"
        ],
        "prompt": ["请给出图片的详细描述。"],
    }

    image_src_type = "image_url"
    model_path = os.getenv("MODEL_PATH", "/opt/las/models")
    model_name = os.getenv("MODEL_NAME", "Qwen/Qwen2.5-VL-7B-Instruct")
    dtype = "bfloat16"
    default_prompt = None
    max_caption_length = 256
    resized_height = 256
    resized_width = 256
    batch_size = 2
    seed = 42
    max_model_len = 12800
    max_num_seqs = 128
    tensor_parallel_size = 1
    enable_prefix_caching = False
    gpu_memory_utilization = 0.95
    enforce_eager = True

    ds = daft.from_pydict(samples)
    ds = ds.with_column(
        "caption",
        las_udf(
            QwenVLImageUnderstandingVLLM,
            construct_args={
                "image_src_type": image_src_type,
                "model_path": model_path,
                "model_name": model_name,
                "dtype": dtype,
                "prompt": default_prompt,
                "max_caption_length": max_caption_length,
                "resized_height": resized_height,
                "resized_width": resized_width,
                "batch_size": batch_size,
                "seed": seed,
                "max_model_len": max_model_len,
                "max_num_seqs": max_num_seqs,
                "tensor_parallel_size": tensor_parallel_size,
                "enable_prefix_caching": enable_prefix_caching,
                "gpu_memory_utilization": gpu_memory_utilization,
                "enforce_eager": enforce_eager,
            },
            num_gpus=tensor_parallel_size,
            batch_size=batch_size,
            concurrency=1,
        )(col("image_path"), col("prompt")),
    )

    ds.show()

    # ╭────────────────────────────────┬─────────────────────────┬─────────────────────────────────────────────────────────────╮
    # │ image_path                     ┆ prompt                  ┆ caption                                                     │
    # │ ---                            ┆ ---                     ┆ ---                                                         │
    # │ Utf8                           ┆ Utf8                    ┆ Utf8                                                        │
    # ╞════════════════════════════════╪═════════════════════════╪═════════════════════════════════════════════════════════════╡
    # │ https://las-cn-beijing-public… ┆ 请给出图片的详细描述。…     ┆ 这张图片展示了一只拟人化的猫，它穿着一套复古风格的服装，，包括一件蓝色… │
    # ╰────────────────────────────────┴─────────────────────────┴─────────────────────────────────────────────────────────────╯
```
