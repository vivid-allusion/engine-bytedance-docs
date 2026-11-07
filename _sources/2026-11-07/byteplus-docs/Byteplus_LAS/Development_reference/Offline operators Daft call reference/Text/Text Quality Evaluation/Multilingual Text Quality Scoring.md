---
title: "Multilingual Text Quality Scoring"
product: "Lake AI Service"
product_code: "Byteplus_LAS"
source: "https://docs.byteplus.com/en/docs/Byteplus_LAS/Multilingual_Text_Quality_Scoring"
---

<span id="operator-introduction"></span>
# Operator introduction

<span id="description"></span>
## Description

**Multilingual Text Quality Scoring Operator \- Multilingual Text Quality Evaluation Based on E5 Model**

<span id="core-features"></span>
## Core Features


* **Multilingual Support**: Uses the multilingual\-e5 model to support text quality scoring in multiple languages

* **Deep Learning Evaluation**: Performs quality evaluation using the Transformer\-based E5 model

* **GPU Acceleration**: Supports GPU inference acceleration to improve processing efficiency

* **Batch Processing**: Supports batch text processing to optimize inference performance


<span id="scoring-criteria"></span>
## Scoring Criteria


* Output Range: Floating\-point number between 0 and 1

* Higher Score Indicates Better Quality: A higher score means better text quality

* Generally Speaking: A score exceeding 0.5 indicates good text quality


<span id="supported-languages"></span>
## Supported Languages


* English, Chinese, Japanese, Korean, French, German, Spanish, and other languages

* Based on the multilingual\-e5\-small\-aligned\-quality model


<span id="daft-call"></span>
# Daft call

<span id="operator-parameters"></span>
## Operator parameters

<span id="input"></span>
## Input


|Input column name |Note |
|---|---|
|texts |Column containing text to process, element type is string |


<span id="output"></span>
## Output

Column containing text quality scores, element type is float32

<span id="parameters"></span>
## Parameters

If a parameter does not have a default value, it is a required parameter.


|Parameter name |Type |Default value |Description |
|---|---|---|---|
|model_path |str |/opt/las/models |Base path where the model files are located Default value: "/opt/las/models" |
|model_name |str |multilingual\-e5\-small\-aligned\-quality |Model name Default value: "multilingual\-e5\-small\-aligned\-quality" |
|dtype |str |float32 |Model precision, supports bfloat16, float16, and float32 Default value: "float32" |
|batch_size |int |100 |Batch size Description: Batch size for model inference Default value: 100 |
|rank |int |0 |GPU ID Description: Specify the GPU device ID to use Default value: 0 |


<span id="examples"></span>
## Examples

The following code shows how to use daft to run the operator for scoring multilingual text quality based on the E5 model.

```python
from __future__ import annotations

import os

import daft
from daft import col
from daft.las.functions.text.multilingual_text_quality_scorer import MultilingualTextQualityScorer
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
            "这是一篇关于人工智能技术发展的高质量学术论文，内容详实且具有很强的参考价值。",
            "これは量子物理学とその現代技術への応用に関するよく書かれた科学論文です。",
            "이것은 양자물리학과 현대 기술에의 응용에 관한 잘 쓰여진 과학 논문입니다.",
            None,
        ]
    }

    model_path = os.getenv("MODEL_PATH", "/opt/las/models")
    model_name = "multilingual-e5-small-aligned-quality"
    dtype = "float32"
    batch_size = 100

    ds = daft.from_pydict(samples)
    ds = ds.with_column(
        "quality_score",
        las_udf(
            MultilingualTextQualityScorer,
            construct_args={
                "model_path": model_path,
                "model_name": model_name,
                "dtype": dtype,
                "batch_size": batch_size,
                "rank": 0,
            },
            num_gpus=1,
            batch_size=1,
            concurrency=1,
        )(col("text")),
    )

    ds.show()
    # ╭──────────────────────────────────────────────────────────────────────────┬─────────────────────╮
    # │ text                                                                     ┆ quality_score       │
    # │ ---                                                                      ┆ ---                 │
    # │ Utf8                                                                     ┆ Float32             │
    # ╞══════════════════════════════════════════════════════════════════════════╪═════════════════════╡
    # │ 这是一篇关于人工智能技术发展的高质量学术论文，内容详实且具有很强的参考价值。          ┆ 0.6294931           │
    # ├╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌┼╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌┤
    # │ これは量子物理学とその現代技術への応用に関するよく書かれた科学論文です。             ┆ 0.73835784          │
    # ├╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌┼╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌┤
    # │ 이것은 양자물리학과 현대 기술에의 응용에 관한 잘 쓰여진 과학 논문입니다。                  ┆ 0.7729334           │
    # ├╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌┼╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌┤
    # │ None                                                                     ┆ None                │
    # ╰──────────────────────────────────────────────────────────────────────────┴─────────────────────╯
```
