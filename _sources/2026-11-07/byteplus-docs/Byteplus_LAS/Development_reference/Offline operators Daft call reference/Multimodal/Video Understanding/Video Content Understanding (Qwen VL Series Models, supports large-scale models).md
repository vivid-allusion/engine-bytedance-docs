---
title: "Video Content Understanding (Qwen VL Series Models, supports large-scale models)"
product: "Lake AI Service"
product_code: "Byteplus_LAS"
source: "https://docs.byteplus.com/en/docs/Byteplus_LAS/Video-Understanding-qwen-vl"
---

<span id="operator-introduction"></span>
# Operator introduction

<span id="description"></span>
## Description

**Qwen2.5\-VL multimodal video understanding model supports temporal semantic parsing and natural language description generation, suitable for various video analysis scenarios.** 

<span id="key-features"></span>
## Key Features


* Multimodal temporal modeling: Supports three video input formats (URL, Base64 encoding, binary stream), flexibly adapting to different data sources.

* Spatiotemporal joint modeling: Automatically captures spatiotemporal features and semantic correlations of videos to achieve more accurate video content understanding.

* Conversational prompt support: Customize generation directions via the `prompt` parameter to meet diverse business needs.

* Efficient inference: Integrates the VLLM inference engine, supporting three precisions (`bfloat16`, `float16`, `float32`), making full use of GPU computing power.

* Recommended to use GPUs with 48G or more VRAM


<span id="applicable-scenarios"></span>
## Applicable Scenarios


* Video content understanding and summarization

* Intelligent monitoring and event analysis

* Multimodal dialogue and interaction

* Other AI applications requiring video semantic parsing


<span id="notes"></span>
## Notes


* Only supports GPU environments; it is recommended to set parameters reasonably based on VRAM and business needs.

* It is recommended to unify video size and frame rate before inference for optimal results.


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
|video_src_type |str |video_url |The format type of the input video. Supported types: \- "video_url": TOS/HTTP address \- "video_base64": Base64 encoding \- "video_binary": Binary stream Optional values: ["video_url", "video_base64", "video_binary"] Default value: "video_url" |
|model_path |str |/opt/las/models |The absolute path where local model files are stored. The default is the preset path inside the container; modify this path when using a custom model. Default value: "/opt/las/models" |
|model_name |str |Qwen/Qwen2.5\-VL\-7B\-Instruct |Supported vision\-language model version. Currently only supports Qwen2.5\-VL series models. Optional values: ["Qwen/Qwen2.5\-VL\-7B\-Instruct\-AWQ", "Qwen/Qwen2.5\-VL\-7B\-Instruct", "Qwen/Qwen2.5\-VL\-32B\-Instruct\-AWQ", "Qwen/Qwen2.5\-VL\-32B\-Instruct"] Default value: "Qwen/Qwen2.5\-VL\-7B\-Instruct" |
|prompt |str |请给出这段视频的详细描述。 |A prompt for the user to understand the video content; the model generates video descriptions based on this prompt. When set to empty, it is recommended to pass a specific prompt for each piece of data. Default value: "Please give a detailed description of this video." |
|batch_size |int |4 |The number of samples processed in a single inference. A larger batch_size can improve throughput but increases memory consumption; it is recommended to adjust based on GPU memory. Default value: 4 |
|dtype |str |bfloat16 |Model inference precision selection. \- "bfloat16": Balances precision and speed \- "float16": Faster inference speed \- "float32": Highest precision but maximum memory consumption Optional values: ["bfloat16", "float16", "float32"] Default value: "bfloat16" |
|max_model_len |int |128000 |The maximum supported input length of the model (in tokens), which affects the length of video descriptions that can be processed and cannot exceed 128000. Default value: 128000 |
|max_num_seqs |int |128 |Maximum number of sequences per batch, which affects concurrent inference capability. Default value: 128 |
|tensor_parallel_size |int |1 |Number of GPUs for tensor parallelism, which improves inference speed. Default value:1 |
|enable_prefix_caching |bool |True |Whether to enable prefix caching to accelerate multi\-turn inference. Default value: True |
|gpu_memory_utilization |float |0.9 |Upper limit of GPU memory utilization per card, ranging from 0 to1. Default value:0.9 |
|enforce_eager |bool |False |Whether to force the use of eager mode for inference, which is available for debugging or special scenarios. Default value: False |
|min_pixels |int or None | |Minimum number of pixels for the video. If not set, the original video pixels are used by default. Larger video pixels result in higher GPU memory usage. Default value: None |
|max_pixels |int or None | |Maximum number of pixels for the video. If not set, the original video pixels are used by default. Larger video pixels result in higher GPU memory usage. Default value: None |
|fps |float or None | |Video frame rate. If not set, the original video frame rate is used by default. Higher frame rates result in higher GPU memory usage. It is recommended to set a specific frame rate value. Default value: None |
|temperature |float |1.0 |Sampling temperature, which controls the diversity of generated content. Higher values lead to more random outputs. Default value: 1.0 |
|top_p |float |0.2 |Probability threshold for nucleus sampling, which controls the diversity of generated content. Smaller values lead to more conservative outputs. Default value:0.2 |
|repetition_penalty |float |1.05 |Repetition penalty coefficient to prevent duplicate content generation. Larger values result in fewer repeated contents. Default value: 1.05 |
|max_tokens |int |8192 |Maximum number of tokens generated in a single run, which affects the length of the description. Default value: 8192 |
|stop_token_ids |list |[] |Stop generation when these token IDs are encountered. Used to customize generation termination conditions. Default value: [] |
|seed |int |42 |Random seed to ensure reproducibility of inference results. Default value: 42 |


<span id="examples"></span>
## Examples

The following code shows how to use daft to run the operator to understand video content and generate descriptions according to instructions.

```python
from __future__ import annotations

import logging
import os

import ray

import daft
from daft import col
from daft.las.functions.multimodal.qwen_vl_video_understanding_vllm import QwenVLVideoUnderstandingVLLM
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
    default_prompt = None
    max_caption_length = 256
    min_pixels = 320 * 160
    max_pixels = 320 * 160
    fps = 1
    batch_size = 2
    seed = 42
    max_model_len = 12800
    max_num_seqs = 128
    tensor_parallel_size = 1
    enable_prefix_caching = True
    gpu_memory_utilization = 0.95
    enforce_eager = True

    ds = daft.from_pydict(samples)
    ds = ds.with_column(
        "caption",
        las_udf(
            QwenVLVideoUnderstandingVLLM,
            construct_args={
                "video_src_type": video_src_type,
                "model_path": model_path,
                "model_name": model_name,
                "dtype": dtype,
                "prompt": default_prompt,
                "max_caption_length": max_caption_length,
                "min_pixels": min_pixels,
                "max_pixels": max_pixels,
                "fps": fps,
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
        )(col("video_path"), col("prompt")),
    )

    ds.show()

    # ╭────────────────────────────────┬─────────────────────────┬─────────────────────────────────────────────────────────────╮
    # │ video_path                     ┆ prompt                  ┆ caption                                                     │
    # │ ---                            ┆ ---                     ┆ ---                                                         │
    # │ Utf8                           ┆ Utf8                    ┆ Utf8                                                        │
    # ╞════════════════════════════════╪═════════════════════════╪═════════════════════════════════════════════════════════════╡
    # │ https://las-cn-beijing-public… ┆ 请给出视频的详细描述。…    ┆ 这是一段动画片段，画面中出现了一个卡通角色，它被设计成一个…           │
    # ╰────────────────────────────────┴─────────────────────────┴─────────────────────────────────────────────────────────────╯
```
