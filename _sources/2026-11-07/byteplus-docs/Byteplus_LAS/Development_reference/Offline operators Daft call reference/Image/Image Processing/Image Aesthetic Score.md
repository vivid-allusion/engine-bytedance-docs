---
title: "Image Aesthetic Score"
product: "Lake AI Service"
product_code: "Byteplus_LAS"
source: "https://docs.byteplus.com/en/docs/Byteplus_LAS/Image_Aesthetic_Score"
---

<span id="operator-introduction"></span>
# Operator introduction

<span id="description"></span>
## Description

**Image Aesthetic Score Processor, intelligently evaluates the aesthetic quality and composition effect of images**

<span id="core-features"></span>
## Core Features:


* Aesthetic Scoring: Professionally evaluates the aesthetic quality of input images

* Composition Analysis: Analyzes image composition based on visual perception theory

* Standardized Output: Scores are normalized to the range of 0\-1 for easy subsequent processing

* Batch Processing: Supports efficient batch image scoring

* Multi\-format Support: Compatible with multiple image input formats


<span id="format-support"></span>
## Format Support:


* Input: Supports multiple formats such as image URLs, TOS addresses, binary streams, etc.

* Output: Floating\-point aesthetic score (0.0\-1.0), higher values indicate better aesthetic quality

* Image Formats: Mainstream image formats like JPG, PNG, WebP, etc.

* Resolution: Automatically adapts to image inputs of different resolutions


<span id="scoring-principles"></span>
## Scoring Principles:


* Visual Feature Extraction: Uses advanced visual models to extract image features

* Aesthetic Modeling: Scoring model trained on large\-scale aesthetic datasets

* Multi\-dimensional Evaluation: Comprehensively considers multiple aesthetic elements such as color, composition, contrast, etc.

* Perception Alignment: Scoring results are highly consistent with human aesthetic perception


<span id="daft-call"></span>
# Daft call

<span id="operator-parameters"></span>
## Operator parameters

<span id="input"></span>
## Input


|Input column name |Note |
|---|---|
|image_inputs |An array containing input images |


<span id="output"></span>
## Output

A float array containing aesthetic scores, with values ranging from 0.0 to 1.0.

Images that cannot be decoded or fail to process return null values.

<span id="parameters"></span>
## Parameters

If a parameter does not have a default value, it is a required parameter.


|Parameter name |Type |Default value |Description |
|---|---|---|---|
|batch_size |int |32 |Batch processing size, controlling the number of images processed in a single inference Default value: 32 |
|model_path |str |/data00/tiger/las/models |Model file storage path Default value: '/data00/tiger/las/models' |
|clip_model_name |str |openai/clip\-vit\-large\-patch14 |CLIP visual model name Default value: 'openai/clip\-vit\-large\-patch14' |
|mlp_model_name |str |laion_aesthetic_v2/sac+logos+ava1\-l14\-linearMSE.pth |MLP scoring model name Default value: 'laion_aesthetic_v2/sac+logos+ava1\-l14\-linearMSE.pth' |
|device |str |cpu |Device type, supporting CPU and GPU devices Default value: "cpu" Optional values: "cpu", "cuda", "cuda:0", "cuda:1", etc. |


<span id="examples"></span>
## Examples

The following code demonstrates how to use Daft (suitable for distributed environments) to run the operator for aesthetic quality scoring of images.

```python
from __future__ import annotations

import os

import daft
from daft import col
from daft.las.functions.image import ImageAestheticScore
from daft.las.functions.udf import las_udf

if __name__ == "__main__":
    TOS_TEST_DIR_URL = os.getenv("TOS_TEST_DIR_URL", "las-cn-beijing-public-online.tos-cn-beijing.volces.com")
    model_path = os.getenv("MODEL_PATH", "/opt/las/models")

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
        "input_path": [f"https://{TOS_TEST_DIR_URL}/public/archive/image_aesthetic_score/forest.jpg"],
    }
    ds = daft.from_pydict(samples)

    # Using Daft to calculate aesthetic scores for images
    constructor_kwargs = {
        "model_path": model_path,
        "image_src_type": "image_url",
        "batch_size": 1,
    }

    ds = ds.with_column(
        "aesthetic_score",
        las_udf(
            ImageAestheticScore,
            construct_args=constructor_kwargs,
            num_cpus=1,
            concurrency=1,
            batch_size=1,
        )(col("input_path")),
    )

    ds.show()
    # ╭────────────────────────────────┬────────────────────╮
    # │ input_path                     ┆ aesthetic_score    │
    # │ ---                            ┆ ---                │
    # │ Utf8                           ┆ Float64            │
    # ╞════════════════════════════════╪════════════════════╡
    # │ https://las-public-data-qa.to… ┆ 0.5603389739990234 │
    # ╰────────────────────────────────┴────────────────────╯
```
