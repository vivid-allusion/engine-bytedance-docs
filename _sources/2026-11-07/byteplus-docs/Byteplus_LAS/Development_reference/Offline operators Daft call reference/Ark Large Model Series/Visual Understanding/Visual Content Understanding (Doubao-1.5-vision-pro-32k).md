---
title: "Visual Content Understanding (Doubao-1.5-vision-pro-32k)"
product: "Lake AI Service"
product_code: "Byteplus_LAS"
source: "https://docs.byteplus.com/en/docs/Byteplus_LAS/Visual-Content-Doubao-1-5"
---

<span id="operator-introduction"></span>
# Operator introduction

<span id="description"></span>
## Description

**Large Model Multimodal Video Understanding Processor**

<span id="core-features"></span>
## Core Features:


* Multimodal Scene Support: Supports image/video understanding tasks and automatically constructs message structures compliant with multimodal model specifications

* Simplified Input Mechanism: Configure input formats such as base64 encoding or URLs for images/videos to enable visual understanding functions


<span id="input-output-specifications"></span>
## Input/Output Specifications:


* Input Format:

   * Image/Video Data: string type, supports base64 encoding or URL addresses

   * (Optional Configuration) User Prompt: string type. When users need to specify different prompts for each data entry, pass the user prompt. If not passed, the unified prompt configured in the prompt field will be used

* Output Format:

   * Default Mode: str type generated result

   * Diagnostic Mode: Set the environment variable LAS_LLM_FINISH_REASON_CHECK=true to return the complete generated result and the model's finish reason:

* llm_result: str type, generated result

* finish_reason: str type, model result finish reason, possible values: stop, length, content_filter


<span id="daft-call"></span>
# Daft call

<span id="operator-parameters"></span>
## Operator parameters

<span id="input"></span>
## Input


|Input column name |Note |
|---|---|
|media_datas |Pass in the image or video data to be processed. Supports passing base64 encoding or URL of images or videos |
|user_prompts |Pass in user prompts. When passing image or video data, if prompts for different images/videos are different, specify via this field; if the same, specify via the prompt parameter |


<span id="output"></span>
## Output

(By default) When the environment variable LAS_LLM_FINISH_REASON_CHECK=false, the return field type is str.

When LAS_LLM_FINISH_REASON_CHECK=true, the return field type is struct, containing the following fields:


* llm_result: Model output result

* finish_reason: Reason for the end of model output


<span id="parameters"></span>
## Parameters

If a parameter does not have a default value, it is a required parameter.


|Parameter name |Type |Default value |Description |
|---|---|---|---|
|model |str | |Model name Supported models: Doubao models and DeepSeek models. Example: doubao\-1.5\-lite\-32k |
|version |str or None | |Model version Enter the version information corresponding to the model. Example: 250115 |
|inference_type |str |batch |Inference type, supports online and batch inference. Default: batch \- online: Use the online inference module provided by the Ark platform \- batch: Use the batch inference module provided by the Ark platform |
|system_text |str or None | |System prompt content System prompt content, input to the model as the system role |
|system_image_url |str or None | |System image URL In mixed text\-image scenarios, input the system image URL to guide the model's behavior |
|system_video_url |str or None | |System video URL In mixed text\-video scenarios, input the system video URL to guide the model's behavior |
|prompt |str or None | |User prompt Used to guide the model's behavior. When configured, it will be concatenated with input text and sent as the user role. Can also be set to {query}, where input text replaces this field |
|multimodal_type |str |image |Media content type Specifies the type of content to process. Default: image \- image: Image \- video: Video \- text: Text |
|image_format |str |jpeg |Image encoding format Valid only when multimodal_type=image, default: jpeg. Supported formats: JPEG, PNG, WEBP, GIF, BMP, TIFF and other common formats. For details, refer to https://www.volcengine.com/docs/82379/1362931#%E5%9B%BE%E7%89%87%E6%A0%BC%E5%BC%8F%E8%AF%B4%E6%98%8E |
|image_url_detail |str or None | |Image quality Supports manual setting with values: high, low, auto \- high: High\-detail mode, suitable for scenarios requiring detailed image understanding (e.g., local feature extraction, complex detail analysis) \- low: Low\-detail mode, suitable for simple tasks (e.g., classification, overall description) for faster processing \- auto: Default mode; varies by model. For details, refer to https://www.volcengine.com/docs/82379/1362931#bf4d9224 |
|video_format |str |mp4 |Video encoding format Default: mp4. Supported formats: MP4, AVI, MOV. Single file size ≤50MB |
|video_fps |float or None |1 |Video frame rate Range: [0.2,5]. Default:1 Extracts specified frames per second. Higher values improve detail but increase token usage; lower values reduce usage and speed up processing. Refer to https://www.volcengine.com/docs/82379/1362931#%E7%94%A8%E9%87%8F%E8%AF%B4%E6%98%8E |
|source_type |str |url |Data source type Specifies the source format of media data. Default: url \- binary: Raw binary data \- base64: Base64 encoded data \- url: Network resource address (supports http/https/tos) |
|max_tokens |int or None | |Maximum response length (tokens). Total input/output length is limited by model context |
|max_completion_tokens |int or None | |Maximum tokens generated by the model, including reasoning_content and content (excluding messages). When exceeded, stops generation and returns finish_reason=length |
|stop |list or None | |Stops generation when the model encounters specified strings (strings not output). Supports up to4 strings. E.g., ["Hello", "Weather"] |
|frequency_penalty |float |0 |Frequency penalty Positive values reduce verbatim repetition by penalizing frequent tokens. Range: [\-2.0,2.0] |
|presence_penalty |float |0 |Presence penalty Positive values encourage new topics by penalizing existing tokens. Range: [\-2.0,2.0] |
|temperature |float |1 |Sampling temperature Controls randomness. 0 means deterministic (highest probability token); higher values (e.g.,0.8) increase randomness, lower values (e.g.,0.2) increase focus. Adjust either temperature or top_p, not both. Range: [0,2] |
|top_p |float |0.7 |Nucleus sampling threshold Considers tokens with cumulative probability ≤top_p. 0 means deterministic; higher values increase randomness. Adjust either temperature or top_p, not both |
|logit_bias |dict or None | |Adjust token probability to align with preferences. Accepts a map of token IDs to biases (\-100 to100). \-100 prohibits,100 forces selection |
|tools |list or None | |List of tools to call. Configure if you want the model to return tools for invocation |
|llm_config |dict or None | |Custom LLM configuration Other parameters are passed to the model. Overrides values in llm_config |
|request_timeout |int |1200 |Request timeout Timeout for a single request (seconds) |
|max_concurrency |int |100 |Max concurrency Maximum concurrent requests per process |


<span id="examples"></span>
## Examples

The following code shows how to use Daft to access the Volcano Ark Visual Understanding model for batch inference. Note that results may vary each time.

```python
from __future__ import annotations
import os
import daft
from daft import col
from daft.las.functions.ark_llm.ark_llm_vision_understanding import ArkLLMVisionUnderstanding
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
        "image_urls": [
            f"https://{tos_dir_url}/public/shared_image_dataset/cat_ip_adapter.jpeg"
        ],
        "prompts": ["图片里有什么？"],
    }

    df = daft.from_pydict(samples)
    df = df.with_column(
        "llm_result",
        las_udf(
            ArkLLMVisionUnderstanding,
            construct_args={
                "model": "doubao-1.5-vision-pro-32k",
                "system_text": "你是一个专业的图片理解助手，能够分析图片中的内容并提供详细的描述。",
                "inference_type": "online", # 该模型仅支持在线推理
            },
        )(images=col("image_urls"), texts=col("prompts")),
    )
    df.show()

    # 输出 (每次大模型推理结果可能不同)
    # ╭────────────────────────────────┬────────────────┬─────────────────────────────────────────────────────────────╮
    # │ image_urls                     ┆ prompts        ┆ llm_result                                                  │
    # │ ---                            ┆ ---            ┆ ---                                                         │
    # │ String                         ┆ String         ┆ String                                                      │
    # ╞════════════════════════════════╪════════════════╪═════════════════════════════════════════════════════════════╡
    # │ https://las-public-data-qa.to… ┆ 图片里有什么？ ┆ 画面中是一只拟人化的猫，毛色为米白色与浅棕色相间，拥有一双… │
    # ╰────────────────────────────────┴────────────────┴─────────────────────────────────────────────────────────────╯
```
