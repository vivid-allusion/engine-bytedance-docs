---
title: "Perplexity Calculator"
product: "Lake AI Service"
product_code: "Byteplus_LAS"
source: "https://docs.byteplus.com/en/docs/Byteplus_LAS/Perplexity_Calculator"
---

<span id="operator-introduction"></span>
# Operator introduction

<span id="description"></span>
## Description

**Perplexity Calculation Operator \- Text Quality Evaluation Solution Based on Language Model**

<span id="core-features"></span>
## Core Features


* **Language Model Evaluation**

   * Calculate text perplexity based on KenLM language model

   * Support Chinese and English text quality evaluation

   * Provide text readability indicators

* **Quality Evaluation**

   * The lower the perplexity, the higher the text quality

   * Suitable for text quality screening and evaluation


<span id="technical-implementation"></span>
## Technical Implementation


* **Model Core**

   * KenLM: Efficient language model inference

   * SentencePiece: Chinese and English tokenization processing

* **Computation Optimization**

   * Batch processing to improve efficiency

   * Memory\-friendly model loading


<span id="daft-call"></span>
# Daft call

<span id="operator-parameters"></span>
## Operator parameters

<span id="input"></span>
## Input


|Input column name |Note |
|---|---|
|texts |The text column to process, elements must be strings. |


<span id="output"></span>
## Output

A column of perplexity values, elements are floating\-point numbers.

<span id="parameters"></span>
## Parameters

If a parameter does not have a default value, it is a required parameter.


|Parameter name |Type |Default value |Description |
|---|---|---|---|
|lang |str |zh |Language Description: The language of the text to calculate Optional values: ["en", "zh"] Default value: "zh" |
|model_path |str |/opt/las/models |Path to the model files Default value: "/opt/las/models" |
|model_name |str |kenlm/wikipedia |Model name Default value: "kenlm/wikipedia" |
|rank |int |0 |GPU ID Description: GPU ID used for model loading Default value: 0 |


<span id="examples"></span>
## Examples

The following code demonstrates how to use daft to run the operator and calculate text perplexity for evaluating text quality.

```python
from __future__ import annotations

import os

import daft
from daft import col
from daft.las.functions.text.perplexity_calculator import PerplexityCalculator
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
            "人工智能技术正在快速发展，人工智能技术已经广泛应用于各个领域。",
            "这是一个正常的句子。",
            "乱码文本 12345 !@#$%",
        ]
    }
    lang = "zh"

    ds = daft.from_pydict(samples)
    ds = ds.with_column(
        "perplexity",
        las_udf(
            PerplexityCalculator,
            construct_args={
                "lang": lang,
                "model_path": os.getenv("MODEL_PATH", "/opt/las/models"),
                "model_name": "kenlm/wikipedia",
            },
            num_gpus=0,
            batch_size=1,
            concurrency=1,
        )(col("text")),
    )

    ds.show()
    # ╭──────────────────────────────────────────────┬──────────────────────────────────────────────╮
    # │ text                                         ┆ perplexity                                  │
    # │ ---                                          ┆ ---                                          │
    # │ Utf8                                         ┆ Float64                                      │
    # ╞══════════════════════════════════════════════╪══════════════════════════════════════════════╡
    # │ 人工智能技术正在快速发展，人工智能技术已经广泛应        ┆ 335.9                                        │
    # │ 用于各个领域。                                ┆                                             │
    # ├╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌┼╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌┤
    # │ 这是一个正常的句子。                           ┆ 530.3                                        │
    # ├╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌┼╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌┤
    # │ 乱码文本 12345 !@#$%                           ┆ 9081.4                                       │
    # ╰──────────────────────────────────────────────┴──────────────────────────────────────────────╯
```
