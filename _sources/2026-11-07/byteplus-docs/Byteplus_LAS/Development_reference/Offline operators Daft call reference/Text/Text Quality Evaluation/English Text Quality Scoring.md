---
title: "English Text Quality Scoring"
product: "Lake AI Service"
product_code: "Byteplus_LAS"
source: "https://docs.byteplus.com/en/docs/Byteplus_LAS/English_Text_Quality_Scoring"
---

<span id="operator-introduction"></span>
# Operator introduction

<span id="description"></span>
## Description

**English Text Quality Scoring Operator \- Text Quality Evaluation Based on FastText**

<span id="core-features"></span>
## Core Features


* **Quality Scoring**: Use the FastText model to score the quality of English text, with a preference for scientific knowledge, and only supports CPU environment.

* **Batch Processing**: Support batch processing of text to improve processing efficiency


<span id="scoring-criteria"></span>
## Scoring Criteria


* 0: Low Quality (Low)

* 1: Mid Quality (Mid)

* 2: High Quality (High)

* The final score is a floating\-point number between 0 and 2, with higher scores indicating better quality.

* Generally speaking, a score above 0.5 indicates good text quality.


<span id="daft-call"></span>
# Daft call

<span id="operator-parameters"></span>
## Operator parameters

<span id="input"></span>
## Input


|Input column name |Note |
|---|---|
|texts |A column containing text to process, with elements of string type. |


<span id="output"></span>
## Output

A column containing text quality scores, with elements of float64 type.

<span id="parameters"></span>
## Parameters

If a parameter does not have a default value, it is a required parameter.


|Parameter name |Type |Default value |Description |
|---|---|---|---|
|model_path |str |/opt/las/models |Base path where the model file is located. Default value: "/opt/las/models" |
|model_name |str |llm\-data\-textbook\-quality\-fasttext\-classifier\-v2/model_quantized.bin |Model file name. Default value: "llm\-data\-textbook\-quality\-fasttext\-classifier\-v2/model_quantized.bin" |


<span id="examples"></span>
## Examples

The following code demonstrates how to use daft to run the operator for scoring English text quality based on the FastText model.

```python
from __future__ import annotations

import os

import daft
from daft import col
from daft.las.functions.text.en_text_quality_scorer import EnTextQualityScorer
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

    samples = {"text": ["This is a well-written scientific article about quantum physics.", None]}
    batch_size = 4
    model_path = os.getenv("MODEL_PATH", "/opt/las/models")
    model_name = "llm-data-textbook-quality-fasttext-classifier-v2/model_quantized.bin"

    ds = daft.from_pydict(samples)
    ds = ds.with_column(
        "quality_score",
        las_udf(
            EnTextQualityScorer,
            construct_args={
                "batch_size": batch_size,
                "model_path": model_path,
                "model_name": model_name,
            },
            num_gpus=0,
            batch_size=1,
            concurrency=1,
        )(col("text")),
    )

    ds.show()
    # ╭──────────────────────────────────────────────────────────────────────────┬─────────────────────╮
    # │ text                                                                     ┆ quality_score       │
    # │ ---                                                                      ┆ ---                 │
    # │ Utf8                                                                     ┆ Float64             │
    # ╞══════════════════════════════════════════════════════════════════════════╪═════════════════════╡
    # │ This is a well-written scientific article about quantum physics.         ┆ 0.6918241381645203  │
    # ├╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌┼╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌┤
    # │ None                                                                     ┆ None                │
    # ╰──────────────────────────────────────────────────────────────────────────┴─────────────────────╯
```
