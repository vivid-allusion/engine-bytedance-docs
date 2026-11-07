---
title: "Text-to-Speech (Doubao Speech Large Model)"
product: "Lake AI Service"
product_code: "Byteplus_LAS"
source: "https://docs.byteplus.com/en/docs/Byteplus_LAS/Text-to-Speech-doubao"
---

<span id="operator-introduction"></span>
# Operator introduction

<span id="description"></span>
## Description

**Speech Synthesis Module \- Text\-to\-Audio Solution Based on Doubao Speech Large Model**

<span id="core-features"></span>
## Core Features


* Integrate with the speech synthesis interface of Volcano Engine's large model (`volc.tts`)

* Support multiple parameter configurations such as voice type, emotion, encoding format, speech rate, sampling rate, etc.

* Process multiple text inputs concurrently, output Base64\-encoded audio and original responses

* Suitable for scenarios like voice broadcasting, virtual human voice generation, listening content production, etc.


<span id="application-scenarios"></span>
## Application Scenarios


* Intelligent customer service, voice assistant content generation

* Multilingual text broadcasting system

* Content platforms, short video dubbing

* Virtual human voice driving


<span id="enterprise-access-instructions"></span>
## Enterprise Access Instructions

Currently, this capability is only open to users who have completed enterprise authentication. If you need to test or officially access it, please first complete the Volcano Engine enterprise authentication process.

<span id="daft-call"></span>
# Daft call

<span id="operator-parameters"></span>
## Operator parameters

<span id="input"></span>
## Input


|Input column name |Note |
|---|---|
|texts |PyArrow array of input texts, each element is a string type |


<span id="output"></span>
## Output

PyArrow string array, audio results generated from text; if recognition fails or input is an empty string, the corresponding element is None.

<span id="parameters"></span>
## Parameters

If a parameter does not have a default value, it is a required parameter.


|Parameter name |Type |Default value |Description |
|---|---|---|---|
|appid |str | | |
|token |str | | |
|uid |str | | |
|cluster |str |volcano_tts | |
|voice_type |str |zh_female_wanqudashu_moon_bigtts | |
|encoding |str |mp3 | |
|speed_ratio |float |1.0 | |
|rate |int |24000 | |
|bitrate |int |160 | |
|enable_emotion |bool |False | |
|emotion |str |happy | |
|emotion_scale |int |4 | |
|extra_audio_params |dict or None | | |
|extra_request_params |dict or None | | |
|timeout |int |60 | |
|num_coroutines |int |1 | |


<span id="examples"></span>
## Examples

The following code demonstrates how to use daft to run the operator for text\-to\-speech conversion.

```python
from __future__ import annotations

import os

import daft
from daft import col
from daft.las.functions.audio.audio_tts_doubao import AudioTtsDoubao
from daft.las.functions.udf import las_udf

if __name__ == "__main__":
    # 从环境变量中读取豆包语音服务的鉴权信息：
    # - OPENSPEECH_APPID：应用 ID，用于标识调用方
    # - OPENSPEECH_TOKEN：访问令牌，用于接口鉴权
    appid = os.getenv("OPENSPEECH_APPID")
    token = os.getenv("OPENSPEECH_TOKEN")

    if os.getenv("DAFT_RUNNER", "native") == "ray":
        import logging

        import ray

        def configure_logging():
            logging.basicConfig(
                level=logging.INFO,
                format="%(asctime)s - %(name)s - %(levelname)s - %(message)s",
                datefmt="%Y-%m-%d %H:%M:%S",
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

    samples = {
        "text_input": [
            "今天天气真好，适合出去走走。",
        ]
    }

    df = daft.from_pydict(samples)
    df = df.with_column(
        "tts_audio",
        las_udf(
            AudioTtsDoubao,
            construct_args={
                "appid": appid,
                "token": token,
                "uid": "test",
                "concurrency": 1,
                "timeout": 60,
            },
            num_cpus=1,
            batch_size=1,
            concurrency=1,
        )(col("text_input")),
    )

    df.show()
    # ╭─────────────────────────────────────────────┬────────────────────────────────╮
    # │ text_input                                  ┆ tts_audio                      │
    # │ ---                                         ┆ ---                            │
    # │ Utf8                                        ┆ Binary                         │
    # ╞═════════════════════════════════════════════╪════════════════════════════════╡
    # │ 欢迎使用豆包语音大模型，这是一个演示示例。…        ┆ b"\xff\xf3\xe4\xc4\x00\x00\x0… │
    # ╰─────────────────────────────────────────────┴────────────────────────────────╯
```
