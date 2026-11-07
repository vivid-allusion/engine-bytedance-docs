---
title: "Text sparse & dense embedding (BGE model)"
product: "Lake AI Service"
product_code: "Byteplus_LAS"
source: "https://docs.byteplus.com/en/docs/Byteplus_LAS/Text-sparse-dense-embedding"
---

<span id="operator-introduction"></span>
# Operator introduction

<span id="description"></span>
## Description

**Text embedding model based on BGE\-M3, supporting sparse/dense/token three\-level vector generation**

<span id="core-features"></span>
## Core Features


* **Multi\-granularity Embedding Output:** 

   * Sparse Vector: Term weight representation, suitable for keyword retrieval

   * Dense Vector: 1024\-dimensional semantic representation, suitable for semantic similarity calculation

   * Token Vector: Fine\-grained context representation

* **Hardware Acceleration**: Supports `FP16` quantization and GPU parallel computing


<span id="daft-call"></span>
# Daft call

<span id="operator-parameters"></span>
## Operator parameters

<span id="input"></span>
## Input


|Input column name |Note |
|---|---|
|texts |An array containing the text to process, element type is str. |


<span id="output"></span>
## Output

The processed array contains the following fields:


* dense_embedding: Dense embedding vector

* sparse_embedding: Sparse embedding vector

* token_embedding: Optional token\-level embedding vector


<span id="parameters"></span>
## Parameters

If a parameter does not have a default value, it is a required parameter.


|Parameter name |Type |Default value |Description |
|---|---|---|---|
|is_output_token_vec |bool |False |Whether to output token vectors Default value: False |
|dtype |str |float32 |Model precision, supports float32 and float16 Optional values: ["float32", "float16"] Default value: "float32" |
|batch_size |int |512 |Batch size for model inference Default value: 512 |
|model_path |str |/opt/las/models |Path where the model files are located Default value: "/opt/las/models" |
|model_name |str |BAAI/bge\-m3 |Model name Optional values: ["BAAI/bge\-m3"] Default value: "BAAI/bge\-m3" |
|rank |int or None | |GPU ID Default value: None |


<span id="examples"></span>
## Examples

The following code shows how to use daft to run the operator to compute text dense embedding, sparse embedding, and token embedding based on the bge\-m3 model.

```python
from __future__ import annotations

import os

import daft
from daft import col
from daft.las.functions.text.embedding.bge_sparse_dense_embedding import BgeSparseDenseEmbedding
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

    samples = {"text": ["Hello World!", None]}
    is_output_token_vec = True
    dtype = "float16"
    batch_size = 512
    model_path = os.getenv("MODEL_PATH", "/opt/las/models")
    model_name = "BAAI/bge-m3"
    rank = 0

    ds = daft.from_pydict(samples)
    ds = ds.with_column(
        "embeddings",
        las_udf(
            BgeSparseDenseEmbedding,
            construct_args={
                "is_output_token_vec": is_output_token_vec,
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

    ds.show()
    # ╭──────────────┬───────────────────────────────────────────────────────────────────────────────────────────────╮
    # │ text         ┆ embeddings                                                                                    │
    # │ ---          ┆ ---                                                                                           │
    # │ Utf8         ┆ Struct[dense_embedding: List[Float32], sparse_embedding: Map[Utf8: Float32], token_embedding: │
    # │              ┆ List[List[Float32]]]                                                                          │
    # ╞══════════════╪═══════════════════════════════════════════════════════════════════════════════════════════════╡
    # │ Hello World! ┆ {dense_embedding: [-0.0420532…                                                                │
    # ├╌╌╌╌╌╌╌╌╌╌╌╌╌╌┼╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌┤
    # │ None         ┆ {dense_embedding: None,                                                                       │
    # │              ┆ spars…                                                                                        │
    # ╰──────────────┴───────────────────────────────────────────────────────────────────────────────────────────────╯
```
