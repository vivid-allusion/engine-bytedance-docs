---
title: "Text embedding (BGE model)"
product: "Lake AI Service"
product_code: "Byteplus_LAS"
source: "https://docs.byteplus.com/en/docs/Byteplus_LAS/Text-embedding-BGE"
---

<span id="operator-introduction"></span>
# Operator introduction

<span id="description"></span>
## Description

**Based on the BGE series of text embedding models, supports dense vector generation**

<span id="core-features"></span>
## Core Features


* **Multi\-model Support:** 

   * Supports models such as BGE\-M3, BGE\-Large\-zh\-v1.5, BGE\-Large\-en\-v1.5, BGE\-Multilingual\-Gemma2

   * Each model has different input prompts; users can choose different models according to their needs

* **Hardware Acceleration**: Supports `FP16` quantization and GPU parallel computing


<span id="daft-call"></span>
# Daft call

<span id="operator-parameters"></span>
## Operator parameters

<span id="input"></span>
## Input


|Input column name |Note |
|---|---|
|texts |An array containing texts to process, with element type str. |


<span id="output"></span>
## Output

A processed array containing dense embedding vectors corresponding to each text.

<span id="parameters"></span>
## Parameters

If a parameter does not have a default value, it is a required parameter.


|Parameter name |Type |Default value |Description |
|---|---|---|---|
|dtype |str |float32 |Model precision, supports float32 and float16 Optional values: ["float32", "float16"] Default value: "float32" |
|batch_size |int |512 |Batch size for model inference Default value:512 |
|model_path |str |/opt/las/models |Path to the model files Default value: "/opt/las/models" |
|model_name |str |BAAI/bge\-m3 |Model name Optional values: ["BAAI/bge\-m3", "BAAI/bge\-large\-zh\-v1.5", "BAAI/bge\-large\-en\-v1.5", "BAAI/bge\-multilingual\-gemma2"] Default value: "BAAI/bge\-m3" |
|rank |int or None | |GPU ID Default value: None |


<span id="examples"></span>
## Examples

The following code demonstrates how to use daft to run the operator to compute text embeddings using the bge\-m3 model.

```python
from __future__ import annotations

import logging
import os

import ray

import daft
from daft import col
from daft.las.functions.text.embedding.bge_embedding import BgeEmbedding
from daft.las.functions.udf import las_udf

if __name__ == "__main__":

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

    samples = {"text": ["Hello World!", None]}
    dtype = "float16"
    batch_size = 512
    model_path = os.getenv("MODEL_PATH", "/opt/las/models")
    model_name = "BAAI/bge-m3"
    rank = 0

    ds = daft.from_pydict(samples)
    ds = ds.with_column(
        "embeddings",
        las_udf(
            BgeEmbedding,
            construct_args={
                "dtype": dtype,
                "batch_size": batch_size,
                "model_path": model_path,
                "model_name": model_name,
                "rank": rank,
            },
            num_gpus=1,
            batch_size=1,
            concurrency=1,
        )(col("text")),
    )

    df = ds.to_pandas()
    ds.show()

    # ╭──────────────┬────────────────────────────────╮
    # │ text         ┆ embeddings                     │
    # │ ---          ┆ ---                            │
    # │ Utf8         ┆ List[Float32]                  │
    # ╞══════════════╪════════════════════════════════╡
    # │ Hello World! ┆ [-0.042053223, 0.02178955, -0… │
    # ├╌╌╌╌╌╌╌╌╌╌╌╌╌╌┼╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌┤
    # │ None         ┆ None                           │
    # ╰──────────────┴────────────────────────────────╯
```
