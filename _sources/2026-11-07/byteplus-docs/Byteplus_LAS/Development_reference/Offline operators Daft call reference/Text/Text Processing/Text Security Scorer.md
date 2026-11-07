---
title: "Text Security Scorer"
product: "Lake AI Service"
product_code: "Byteplus_LAS"
source: "https://docs.byteplus.com/en/docs/Byteplus_LAS/Text_Security_Scorer"
---

<span id="operator-introduction"></span>
# Operator introduction

<span id="description"></span>
## Description

**Text Security Scorer \- Security Assessment Based on ShieldLM\-6B\-chatglm3**

<span id="core-features"></span>
## Core Features


* **Multilingual Support**: Supports Chinese and English text security assessment

* **Three\-Category Evaluation**: Outputs probabilities for three categories: safe, unsafe, controversial

* **Batch Processing**: Supports batch text security assessment to improve processing efficiency


<span id="technical-implementation"></span>
## Technical Implementation


* **Model Core**: Based on ShieldLM\-6B\-chatglm3

* **Inference Optimization**: Supports GPU acceleration and batch inference


<span id="application-scenarios"></span>
## Application Scenarios


* Content security review

* Text risk assessment

* Multilingual security filtering


<span id="daft-call"></span>
# Daft call

<span id="operator-parameters"></span>
## Operator parameters

<span id="input"></span>
## Input


|Input column name |Note |
|---|---|
|texts |pyarrow.Array, element type is str |


<span id="output"></span>
## Output

Each element is a struct or None:


* If the corresponding input is None, the output is None;

* Otherwise, output a Struct including the following fields:

* safe: Float64, the probability that the model predicts the text as "safe"

* unsafe: Float64, the probability that the model predicts the text as "unsafe"

* controversial: Float64, the probability that the model predicts the text as "controversial"


<span id="parameters"></span>
## Parameters

If a parameter does not have a default value, it is a required parameter.


|Parameter name |Type |Default value |Description |
|---|---|---|---|
|lang |str |zh |Language Description: The language of the text to be evaluated Optional values: ["en", "zh"] Default value: "zh" |
|model_path |str |/opt/las/models |Base path where the model files are located Default value: "/opt/las/models" |
|model_name |str |thu\-coai/ShieldLM\-6B\-chatglm3 |Model name Default value: "thu\-coai/ShieldLM\-6B\-chatglm3" |
|batch_size |int |1 |Batch size Description: Controls the batch size during model inference Impact: A larger batch_size can improve GPU utilization and throughput but increases memory usage Recommendation: The ShieldLM\-6B model has high memory usage, so the default is set to 1 to ensure stability and compatibility Tuning: In environments with sufficient memory, it can be appropriately increased to 2\-4 to improve processing efficiency Default value: 1 |
|rank |int or None | |GPU ID Description: Specifies the GPU ID to use; None means automatic selection Default value: None |


<span id="examples"></span>
## Examples

The following code shows how to use daft to run the operator to evaluate text safety, outputting the three\-class probabilities of safe, unsafe, and controversial.

```python
from __future__ import annotations

import os

import daft
from daft import col
from daft.las.functions.text.text_safety_scorer import TextSafetyScorer
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
            "爱与和平是世界的主旋律。",
            "我讨厌所有人，最好都去死。",
            None,
        ]
    }

    model_path = os.getenv("MODEL_PATH", "/opt/las/models")
    model_name = "thu-coai/ShieldLM-6B-chatglm3"
    lang = "zh"
    batch_size = 3
    rank = 0

    ds = daft.from_pydict(samples)
    ds = ds.with_column(
        "safety_scores",
        las_udf(
            TextSafetyScorer,
            construct_args={
                "lang": lang,
                "model_path": model_path,
                "model_name": model_name,
                "batch_size": batch_size,
                "rank": rank,
            },
            num_gpus=1,
            batch_size=3,
            concurrency=1,
        )(col("text")),
    )

    ds.show()
    # ╭─────────────────────────────┬────────────────────────────────────────────────────────────────╮
    # │ text                        ┆ safety_scores                                                  │
    # │ ---                         ┆ ---                                                            │
    # │ Utf8                        ┆ Struct[safe: Float64, unsafe: Float64, controversial: Float64] │
    # ╞═════════════════════════════╪════════════════════════════════════════════════════════════════╡
    # │ 爱与和平是世界的主旋律。        ┆ {safe: 0.8632398843765259,                                     │
    # │                             ┆ unsafe: 0.04434245824813843,                                   │
    # │                             ┆ controversial: 0.09241761267185211}                            │
    # ├╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌┼╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌┤
    # │ 我讨厌所有人，最好都去死。      ┆ {safe: 0.0004654618678614497,                                  │
    # │                             ┆ unsafe: 0.9993947744369507,                                    │
    # │                             ┆ controversial: 0.00013975700130686164}                         │
    # ├╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌┼╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌┤
    # │ None                        ┆ None                                                           │
    # ╰─────────────────────────────┴────────────────────────────────────────────────────────────────╯
```
