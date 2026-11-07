---
title: "Multimodal Deep Thinking (Doubao-Seed-1.6)"
product: "Lake AI Service"
product_code: "Byteplus_LAS"
source: "https://docs.byteplus.com/en/docs/Byteplus_LAS/Multimodal-Deep-Thinking-Doubao-Seed-1-6"
---

<span id="operator-introduction"></span>
# Operator introduction

<span id="description"></span>
## Description

**Provide deep thinking capabilities for large models in multimodal scenarios**

Use models with deep thinking capabilities to analyze and understand images, videos, or text, and return text output.

<span id="core-features"></span>
## Core Features:


* Deep thinking mechanism: The model automatically decomposes problems and performs logical reasoning before answering, generating a chain of thought (reasoning_content)

* Multimodal scenario support: Supports image/video understanding tasks and automatically constructs message structures that comply with multimodal model specifications

* Input simplification mechanism: Configure input formats such as base64 encoding or URLs for images/videos to enable visual understanding functions


<span id="input-and-output-specifications"></span>
## Input and Output Specifications:


* Input Format:

   * Image/video data/text data: string type, supports base64 encoding/URL address

   * (Optional) User prompt: string type, passed when different prompts need to be specified for each piece of data; if not passed, the prompt from the class initialization parameters is used

* Output Format:

   * Default mode: struct type includes llm_result (generated result), reasoning_content (chain of thought content) and finish_reason (reason for model result termination)

   * Diagnostic mode: Set the environment variable LAS_LLM_FINISH_REASON_CHECK=true to return an additional finish_reason field:

* finish_reason: Reason for model result termination, possible values: stop (normal termination), length (token limit exceeded), content_filter (content filtering)


<span id="model-capability-enhancements"></span>
## Model Capability Enhancements:


* Chain of thought visualization: Output the model's reasoning process through the reasoning_content field

* Result reliability control: Identify abnormal termination cases through the finish_reason field

* Multimodal understanding: Supports parsing of mixed inputs of images/videos/text


<span id="daft-call"></span>
# Daft call

<span id="operator-parameters"></span>
## Operator parameters

<span id="input"></span>
## Input


|Input column name |Note |
|---|---|
|media_datas |Pass in the image or video data to be processed. Supports passing base64 encoding or URL of images or videos |
|user_prompts |Pass in user prompts. When passing image or video data, if the prompts used for different images or videos are different, you can specify them via this field. If they are the same, you can specify via the prompt parameter. |


<span id="output"></span>
## Output

When the environment variable LAS_LLM_FINISH_REASON_CHECK=true, the returned field type is struct, containing the following fields:


* llm_result: Model output result

* finish_reason: Model output end reason

* reasoning_content: Model output thinking content


When the environment variable LAS_LLM_FINISH_REASON_CHECK=false, the returned field type is struct, containing the following fields:


* llm_result: Model output result

* reasoning_content: Model output thinking content


<span id="parameters"></span>
## Parameters

If a parameter does not have a default value, it is a required parameter.


|Parameter name |Type |Default value |Description |
|---|---|---|---|
|model |str | |Model name Supported models: Doubao model and DeepSeek model. Example: doubao\-seed\-1.6 |
|version |str or None | |Model version Enter the version information corresponding to the model. Example: 250115 |
|thinking_type |str or None | |Thinking mode Controls whether the model enables deep thinking mode. If not configured, deep thinking mode is used and can be manually turned off. Optional values: \- enabled: Enable thinking mode; the model will always think before answering. \- disabled: Disable thinking mode; the model will answer directly without thinking. \- auto: Auto thinking mode; the model independently judges whether to think based on the question and answers simple questions directly. |
|multimodal_type |str |image |Multimedia content type Specifies whether to process images or videos; the default is image. Optional values: \- image: Image \- video: Video \- text: Text |


<span id="examples"></span>
## Examples

The following code shows how to use daft to access the Volcano Ark multimodal deep thinking model (Doubao series) for batch inference. Please note that the results of each large model inference may vary.

```python
from __future__ import annotations

import os

import daft
from daft import col
from daft.las.functions.ark_llm.ark_llm_thinking_vision import ArkLLMThinkingVision
from daft.las.functions.udf import las_udf

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

daft.set_execution_config(min_cpu_per_task=0)

if __name__ == "__main__":
    # 需配置环境变量 LAS_API_KEY ： LAS_API_KEY 通过在 LAS 服务页面上创建获取
    tos_dir_url = os.getenv("TOS_DIR_URL", "las-cn-beijing-public-online.tos-cn-beijing.volces.com")
    samples = {
        "videos": [
            f"https://{tos_dir_url}/public/shared_video_dataset/eating_56.mp4",
        ]
    }

    df = daft.from_pydict(samples)
    df = df.with_column(
        "llm_result",
        las_udf(
            ArkLLMThinkingVision,
            construct_args={
                "model": "doubao-seed-1.6",
                "system_text": "你是一个专业的视频理解助手，能够分析视频中的内容并提供详细的描述。",
                "inference_type": "online",
            },
        )(videos=col("videos"), texts="请用简短的语言描述视频里的内容，返回格式为json。"),
    )

    df = df.with_column("reasoning_content", col("llm_result")["reasoning_content"])
    df = df.with_column("llm_result", col("llm_result")["llm_result"])
    df.show()

    #  输出(每次大模型推理结果可能不同)
    # ╭────────────────────────────────┬────────────────────────────────────────────────┬───────────────────────────────────────────────────────────╮
    # │ videos                         ┆ llm_result                                     ┆ reasoning_content                                         │
    # │ ---                            ┆ ---                                            ┆ ---                                                       │
    # │ String                         ┆ String                                         ┆ String                                                    │
    # ╞════════════════════════════════╪════════════════════════════════════════════════╪═══════════════════════════════════════════════════════════╡
    # │ https://las-public-data-qa.to… ┆ {"content": "一个两层蛋糕上，绿色角色从顶部奶… ┆                                                           │
    # │                                ┆                                                ┆ 我现在需要处理用户的请求，用简短的语言描述视频内容并返回… │
    # ╰────────────────────────────────┴────────────────────────────────────────────────┴───────────────────────────────────────────────────────────╯
```
