---
title: "Audio Understanding (Kimi-Audio Series Models)"
product: "Lake AI Service"
product_code: "Byteplus_LAS"
source: "https://docs.byteplus.com/en/docs/Byteplus_LAS/Audio-Understanding-kimi"
---

<span id="operator-introduction"></span>
# Operator introduction

<span id="description"></span>
## Description

**Kimi\-Audio Multimodal Audio Understanding Model \- Audio Semantic Parsing and Natural Language Description Generation**

<span id="core-features"></span>
## Core Features


* Multimodal Audio Processing

   * Supports three audio formats: `URL`/`Base64 encoding`/`binary stream`

* Audio\-Language Joint Modeling

   * Achieves accurate mapping of audio content to the semantic space

* Conversational Prompt Support

   * Guides generation direction via the `prompt` parameter

* Resource Usage

   * Recommended to use GPUs with 48G or higher VRAM


<span id="scenario-optimization"></span>
## Scenario Optimization


* Chinese\-English mixed scenario optimization: Special enhancement for Chinese semantics

* Supports multiple audio understanding tasks: ASR, audio description, emotion recognition, content analysis


<span id="daft-call"></span>
# Daft call

<span id="operator-parameters"></span>
## Operator parameters

<span id="input"></span>
## Input


|Input column name |Note |
|---|---|
|audios |A column containing audio data, where elements are of string or binary type. |


<span id="output"></span>
## Output

The processed column, where elements are the understanding results of each audio.

<span id="parameters"></span>
## Parameters

If a parameter does not have a default value, it is a required parameter.


|Parameter name |Type |Default value |Description |
|---|---|---|---|
|audio_src_type |str |audio_url |Audio data source type, supports three formats Optional values: ["audio_url", "audio_base64", "audio_binary"] Default value: "audio_url" |
|model_path |str |/opt/las/models |Absolute path for storing local model files, default is the preset path inside the container. Modify this path when using a custom model Default value: "/opt/las/models" |
|model_name |str |moonshotai/Kimi\-Audio\-7B\-Instruct |Supported audio language model version; currently only supports Kimi\-Audio series models Optional values: ["moonshotai/Kimi\-Audio\-7B\-Instruct"] Default value: "moonshotai/Kimi\-Audio\-7B\-Instruct" |
|prompt |str |Please analyze the content of this audio. |Prompt word for users to understand audio content; the model generates audio analysis results based on this prompt. Default value: "Please analyze the content of this audio." |
|batch_size |int |4 |Number of audios processed per batch. Larger values may increase GPU memory consumption. Default value: 4 |
|text_temperature |float |0.0 |Temperature parameter for text generation, controlling the randomness of generated text. 0.0 means deterministic generation Default value: 0.0 |
|text_top_k |int |5 |Number of top\-k candidate words considered during text generation Default value:5 |
|text_repetition_penalty |float |1.0 |Penalty coefficient for text repetition to avoid generating duplicate content Default value:1.0 |
|text_repetition_window_size |int |16 |Window size for text repetition detection Default value:16 |
|rank |int or None | |Specifies the GPU device ID to use (effective in multi\-GPU environments). For example: 0 means the first GPU, 1 means the second GPU Default value: None |


<span id="examples"></span>
## Examples

The following code shows how to use daft to run the operator for audio understanding and content analysis.

```python
from __future__ import annotations

import os

import daft
from daft import col
from daft.las.functions.multimodal.kimi_audio_understanding import KimiAudioUnderstanding
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
        ]
    }

    audio_src_type = "audio_url"
    model_path = os.getenv("MODEL_PATH", "/opt/las/models")
    model_name = "moonshotai/Kimi-Audio-7B-Instruct"
    prompt = """
    你是一名专业的音频分析助手。请全面理解输入音频，并按以下维度进行有条理的说明：
    内容概括：简要描述音频的主要内容、主题或事件。
    说话人信息：识别有多少个说话人，并简要描述他们的说话风格、性别或情绪。
    情绪与语气：总结音频中情绪状态及其变化（如平静、激动、紧张、愉快）。
    关键信息提取：提取音频中的核心信息点或指令，按时间顺序简要列出。
    背景环境：分析是否存在背景音乐、噪音或特殊声效，并描述其特征。
    请使用结构化自然语言输出，既简洁又完整，避免遗漏重要信息。
    """
    text_temperature = 0.0
    text_top_k = 5
    text_repetition_penalty = 1.0
    text_repetition_window_size = 16
    batch_size = 1
    rank = None

    df = daft.from_pydict(samples)
    df = df.with_column(
        "audio_analysis",
        las_udf(
            KimiAudioUnderstanding,
            construct_args={
                "audio_src_type": audio_src_type,
                "model_path": model_path,
                "model_name": model_name,
                "prompt": prompt,
                "text_temperature": text_temperature,
                "text_top_k": text_top_k,
                "text_repetition_penalty": text_repetition_penalty,
                "text_repetition_window_size": text_repetition_window_size,
                "batch_size": batch_size,
                "rank": rank,
            },
            num_gpus=1,
            batch_size=1,
            concurrency=1,
        )(col("audio_path")),
    )
    df.show()

    # ╭────────────────────────────────┬─────────────────────────────────────────────────────────────╮
    # │ audio_path                     ┆ audio_analysis                                              │
    # │ ---                            ┆ ---                                                         │
    # │ Utf8                           ┆ Utf8                                                        │
    # ╞════════════════════════════════╪═════════════════════════════════════════════════════════════╡
    # │ tos://las-cn-beijing-public-o… ┆ 内容概括：这段音频是一位老人在讲述自己的经历和感受，内容涉及…         │
    # ╰────────────────────────────────┴─────────────────────────────────────────────────────────────╯
```
