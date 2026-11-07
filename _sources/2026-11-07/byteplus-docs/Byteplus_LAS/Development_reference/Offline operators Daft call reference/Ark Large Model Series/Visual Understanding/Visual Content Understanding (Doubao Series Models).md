---
title: "Visual Content Understanding (Doubao Series Models)"
product: "Lake AI Service"
product_code: "Byteplus_LAS"
source: "https://docs.byteplus.com/en/docs/Byteplus_LAS/Visual-Content-Doubao-Models"
---

<span id="operator-introduction"></span>
# Operator introduction

<span id="description"></span>
## Description

**Large Model Multimodal Video Understanding Processor**

<span id="core-features"></span>
## Core Features:


* Multimodal Scene Support: Supports image/video understanding tasks and automatically constructs message structures compliant with multimodal model specifications

* Simplified Input Mechanism: Configure input formats such as base64 encoding or URLs for images/videos to enable visual understanding functionality


<span id="input-and-output-specifications"></span>
## Input and Output Specifications:


* Input Format:

   * Image/Video Data: string type, supports base64 encoding/URL address

   * (Optional Configuration) User Prompt: string type. Pass a user prompt if you need to specify different prompts for each data entry; if not provided, the unified prompt configured in the prompt field will be used

* Output Format:

   * Default Mode: Generated result of str type

   * Diagnostic Mode: Set the environment variable LAS_LLM_FINISH_REASON_CHECK=true to return the complete generated result and the finish reason of the model output:

* llm_result: str type, generated result

* finish_reason: str type, finish reason of the model output, possible values: stop, length, content_filter


<span id="daft-call"></span>
# Daft call

<span id="operator-parameters"></span>
## Operator parameters

<span id="input"></span>
## Input


|Input column name |Note |
|---|---|
|media_datas |Pass in the image or video data to be processed. Supports passing base64 encoding or URL of images or videos |
|user_prompts |Pass in user prompts. When passing image or video data, if different prompts are used for different images/videos, specify them via this field. If the prompts are the same, specify via the prompt parameter |


<span id="output"></span>
## Output

(By default) When the environment variable LAS_LLM_FINISH_REASON_CHECK=false, the return field type is str.

When the environment variable LAS_LLM_FINISH_REASON_CHECK=true, the return field type is struct, containing the following fields:


* llm_result: Model output result

* finish_reason: Reason for model output termination


<span id="parameters"></span>
## Parameters

If a parameter does not have a default value, it is a required parameter.


|Parameter name |Type |Default value |Description |
|---|---|---|---|
|model |str | |Model name Supported models: Doubao models and DeepSeek models. Example: doubao\-1.5\-lite\-32k |
|version |str or None | |Model version Enter the version information corresponding to the model. Example: 250115 |
|inference_type |str |batch |Inference type, supports online inference and batch inference. Default value is batch (batch inference) \- online: Use the online inference module provided by the Ark platform \- batch: Use the batch inference module provided by the Ark platform |
|system_text |str or None | |System prompt content System prompt content, input to the model as the "system" role |
|system_image_url |str or None | |System image URL In text\-image mixed scenarios, input the system image URL to guide the model's behavior |
|system_video_url |str or None | |System video URL In text\-image mixed scenarios, input the system video URL to guide the model's behavior |
|prompt |str or None | |User prompt User prompt used to guide the model's behavior. When configured, it will be concatenated with the input text and sent to the model as the "user" role. Additionally, this field can be set to {query}, in which case the input text will replace this field |
|multimodal_type |str |image |Multimodal content type Specifies whether to process images, videos, or text. Default is image. Optional values: \- image: Image \- video: Video \- text: Text |
|image_format |str |jpeg |Image encoding format Only effective when multimodal_type=image. Default is jpeg. Supported formats: JPEG, PNG, WEBP, GIF, BMP, TIFF and other common formats. For detailed formats, refer to https://www.volcengine.com/docs/82379/1362931#%E5%9B%BE%E7%89%87%E6%A0%BC%E5%BC%8F%E8%AF%B4%E6%98%8E |
|image_url_detail |str or None | |Image quality Supports manual setting of image quality with values: high, low, auto. \- high: High\-detail mode, suitable for scenarios requiring understanding of image details (e.g., extracting multiple local information/features or understanding complex/richly detailed images) \- low: Low\-detail mode, suitable for simple image classification/recognition or overall content understanding (faster) \- auto: Default mode; varies slightly by model. For details, refer to https://www.volcengine.com/docs/82379/1362931#bf4d9224 |
|video_format |str |mp4 |Video encoding format Configures the video format; default is mp4. Supported formats: MP4, AVI, MOV. Single video file size must be within 50MB |
|video_fps |float or None | |Video frame rate Range: [0.2,5]. Default:1 Extracts the specified number of frames per second from the video. Higher values lead to more precise understanding of frame changes; lower values reduce sensitivity but use fewer tokens and are faster. Refer to https://www.volcengine.com/docs/82379/1362931#%E7%94%A8%E9%87%8F%E8%AF%B4%E6%98%8E |
|source_type |str |url |Data source type Specifies the source format of media data; default is url. Optional values: \- binary: Raw binary data \- base64: Base64 encoded data \- url: Network resource address (supports http/https/tos) |
|max_tokens |int or None | |Maximum length of model response (in tokens). Total input/output length is limited by the model's context window |
|max_completion_tokens |int or None | |Maximum number of tokens generated by the model (includes chain\-of\-thought and answer content, excludes incoming messages). If exceeded, the model stops outputting and returns finish_reason=length |
|stop |list or None | |When the model encounters the specified strings, it stops generating (strings are not output). Supports up to4 strings. Example: ["你好","天气"] |
|frequency_penalty |float |0 |Frequency penalty coefficient If positive, penalizes tokens based on their frequency to reduce verbatim repetition. Range: [\-2.0,2.0] |
|presence_penalty |float |0 |Presence penalty coefficient If positive, penalizes tokens based on their presence to encourage new topics. Range: [\-2.0,2.0] |
|temperature |float |1 |Sampling temperature Controls the randomness of output. 0 means deterministic (only highest probability token); higher values (e.g.,0.8) make output more random, lower values (e.g.,0.2) more focused. Adjust either temperature or top_p, not both. Range: [0,2] |
|top_p |float |0.7 |Nucleus sampling threshold Considers tokens with cumulative probability ≤ top_p. 0 means deterministic; higher values increase randomness. Adjust either temperature or top_p, not both. Default:0.7 |
|logit_bias |dict or None | |Adjusts token probabilities to align with preferences. Map of token IDs to biases (range: [\-100,100]). \-1 reduces selection likelihood;1 increases it;\-100 prohibits selection;100 forces selection. Effect varies by model |
|tools |list or None | |List of tools to call. Configure this if you want the model to return tools to invoke |
|llm_config |dict or None | |Custom LLM configuration Other parameters are passed through to the model. The above parameters override values in llm_config |
|request_timeout |int |1200 |Request timeout Timeout for a single request (seconds) |
|max_concurrency |int |100 |Maximum concurrency Max concurrent requests per process |


<span id="examples"></span>
## Examples

The following code shows how to use daft to access the Volcano Ark Visual Understanding model for batch inference. Note that the results may vary each time.

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
        "videos": [
            f"https://{tos_dir_url}/public/shared_video_dataset/eating_56.mp4",
        ],
        "prompts": ["视频里有什么？"],
    }
    
    df = daft.from_pydict(samples)
    df = df.with_column(
        "llm_result",
        las_udf(
            ArkLLMVisionUnderstanding,
            construct_args={
                "model": "doubao-1.5-vision-pro",
                "system_text": "你是一个专业的视频理解助手，能够分析视频中的内容并提供详细的描述。",
                "inference_type": "online",
            },
        )(videos=col("videos"), texts=col("prompts")),
    )
    df.show()

    # 输出 (每次大模型推理结果可能不同)
    # ╭────────────────────────────────┬────────────────┬─────────────────────────────────────────────────────────────╮
    # │ videos                         ┆ prompts        ┆ llm_result                                                  │
    # │ ---                            ┆ ---            ┆ ---                                                         │
    # │ String                         ┆ String         ┆ String                                                      │
    # ╞════════════════════════════════╪════════════════╪═════════════════════════════════════════════════════════════╡
    # │ https://las-public-data-qa.to… ┆ 视频里有什么？ ┆ 视频里展示了一个卡通风格的场景，主要元素是一个两层的红色蛋… │
    # ╰────────────────────────────────┴────────────────┴─────────────────────────────────────────────────────────────╯
```
