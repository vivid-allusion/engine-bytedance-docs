---
title: "Text Language Recognition"
product: "Lake AI Service"
product_code: "Byteplus_LAS"
source: "https://docs.byteplus.com/en/docs/Byteplus_LAS/Text_Language_Recognition"
---

<span id="operator-introduction"></span>
# Operator introduction

<span id="description"></span>
## Description

**Text Language Recognition Operator \- Provides multilingual recognition capabilities based on the FastText model**

<span id="core-features"></span>
## Core Features


* Supports recognition of 176 languages (based on fasttext/lid.176 series models)

* Batch inference optimization, suitable for processing large\-scale text data

* Supports simultaneous output of language labels and confidence scores

* Supports model files from local paths and TOS paths


<span id="application-scenarios"></span>
## Application Scenarios


* Multilingual text classification

* Language filtering and screening

* Multilingual dataset construction


<span id="recommendations"></span>
## Recommendations


* Input text length is recommended to be at least 10 characters to improve recognition accuracy

* Requires at least 4GB of memory for model batch inference


<span id="daft-call"></span>
# Daft call

<span id="operator-parameters"></span>
## Operator parameters

<span id="input"></span>
## Input


|Input column name |Note |
|---|---|
|texts |Original string column; elements must be of string type |


<span id="output"></span>
## Output

A struct column containing language labels and confidence scores\nEach element includes 'language' and 'confidence' fields

<span id="parameters"></span>
## Parameters

If a parameter does not have a default value, it is a required parameter.


|Parameter name |Type |Default value |Description |
|---|---|---|---|
|model_path |str |/opt/las/models |Path where the model files are located Default value: "/opt/las/models" |
|model_name |str |fasttext/lid.176.bin |Model file name; supports "fasttext/lid.176.bin" or "fasttext/lid.176.ftz" |
|batch_size |int |1000 |Batch processing size; a larger batch_size can improve throughput but increases memory consumption |


<span id="examples"></span>
## Examples

The following code shows how to use daft to run the operator for text language recognition.

```python
from __future__ import annotations

import os

import daft
from daft import col
from daft.las.functions.text.language_recognition import LanguageRecognitionOperator
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

    samples = {
        "text": [
            "这是一行测试内容。",
            "This is a test content.",
            "This is a test content.这是一行测试内容。",
            "こんにちは",
            "안녕하세요",
        ]
    }

    ds = daft.from_pydict(samples)
    ds = ds.with_column(
        "language_result",
        las_udf(
            LanguageRecognitionOperator,
            construct_args={
                "model_path": os.getenv("MODEL_PATH", "/opt/las/models"),
                "model_name": "fasttext/lid.176.bin",
                "batch_size": 1000,
            },
        )(col("text")),
    )

    ds.show()
    # ╭──────────────────────────────────────┬─────────────────────────────────────────────╮
    # │ text                                 ┆ language_result                             │
    # │ ---                                  ┆ ---                                         │
    # │ Utf8                                 ┆ Struct[language: Utf8, confidence: Float64] │
    # ╞══════════════════════════════════════╪═════════════════════════════════════════════╡
    # │ 这是一行测试内容。                   ┆ {language: zh, confidence: 1.000048279762268} │
    # │ This is a test content.              ┆ {language: en, confidence: 0.9209088683128357} │
    # │ This is a test content.这是一行测试… ┆ {language: zh, confidence: 0.6892356276512146} │
    # │ こんにちは                           ┆ {language: ja, confidence: 1.0000269412994385} │
    # │ 안녕하세요                           ┆ {language: ko, confidence: 0.9996028542518616} │
    # ╰──────────────────────────────────────┴─────────────────────────────────────────────╯
```
