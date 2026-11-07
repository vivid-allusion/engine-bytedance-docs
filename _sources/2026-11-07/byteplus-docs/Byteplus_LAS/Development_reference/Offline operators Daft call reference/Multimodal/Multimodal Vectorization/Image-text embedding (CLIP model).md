---
title: "Image-text embedding (CLIP model)"
product: "Lake AI Service"
product_code: "Byteplus_LAS"
source: "https://docs.byteplus.com/en/docs/Byteplus_LAS/Image-text-embedding-CLIP"
---

<span id="operator-introduction"></span>
# Operator introduction

<span id="description"></span>
## Description

**CLIP (Contrastive Language\-Image Pretraining) cross\-modal embedding generator, which implements text\-image joint embedding space mapping based on the CLIP model**

<span id="core-features"></span>
## Core Features


* **Unified Multimodal Encoding**

   * Text Encoding: Chinese text → 512/768/1024\-dimensional semantic vector

   * Image Encoding: Image → 512/768/1024\-dimensional visual feature vector

* **Cross\-modal Similarity Calculation**

   * Supports cosine similarity/dot product calculation of the correlation between text and image embedding vectors


<span id="typical-application-scenarios"></span>
## Typical Application Scenarios


* ✅ E\-commerce Scenario \- Product Text\-Image Mutual Search

* ✅ Content Moderation \- Text\-Image Consistency Check

* ✅ Recommendation System \- Multimodal Feature Fusion


<span id="daft-call"></span>
# Daft call

<span id="operator-parameters"></span>
## Operator parameters

<span id="input"></span>
## Input


|Input column name |Note |
|---|---|
|content |An array containing input data, supporting the following element types: \- Text mode: UTF\-8 string \- Image mode: Base64 string/binary data/image URL |


<span id="output"></span>
## Output

An array containing floating\-point embedding vectors, where each element is a List[float].

<span id="parameters"></span>
## Parameters

If a parameter does not have a default value, it is a required parameter.


|Parameter name |Type |Default value |Description |
|---|---|---|---|
|content_type |str | |Input content format type, supporting: \- Text (text) \- tos/http address (image_url) \- base64 encoding (image_base64) \- Binary stream (image_binary) Optional values: ["text", "image_url", "image_base64", "image_binary"] Default value: "image_url" |
|batch_size |int |16 |Batch size for computation, default:16 |
|model_path |str |/opt/las/models |Model storage path, default: '/opt/las/models' (internal parameter) |
|model_name |str |iic/multi\-modal_clip\-vit\-base\-patch16_zh |Model name, optional values: \- 'iic/multi\-modal_clip\-vit\-base\-patch16_zh' \- 'iic/multi\-modal_clip\-vit\-huge\-patch14_zh' \- 'iic/multi\-modal_clip\-vit\-large\-patch14_zh' \- 'iic/multi\-modal_clip\-vit\-large\-patch14_336_zh' Default value: 'iic/multi\-modal_clip\-vit\-base\-patch16_zh' |
|model_version |str |v1.0.1 |Model version, currently only 'v1.0.1' is supported |
|rank |int |0 |Specifies the GPU device ID (valid in multi\-card environments), default:0 (internal parameter) |


<span id="examples"></span>
## Examples

The code below shows how to use daft to run the image\-text embedding operator and generate image\-text embeddings.

```python
from __future__ import annotations

import os

import daft
from daft import col
from daft.las.functions.multimodal.embedding.clip_embedding import ClipEmbedding
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

    samples = {"text": ["皮卡丘", "小狗", "小猫", None]}
    content_type = "text"
    model_path = os.getenv("MODEL_PATH", "/opt/las/models")
    model_name = "iic/multi-modal_clip-vit-base-patch16_zh"
    model_version = "v1.0.1"
    embedding_col_name = "embedding"
    batch_size = 2
    rank = 0
    num_gpus = 1

    ds = daft.from_pydict(samples)
    ds = ds.with_column(
        "embedding",
        las_udf(
            ClipEmbedding,
            construct_args={
                "content_type": content_type,
                "model_path": model_path,
                "model_name": model_name,
                "model_version": model_version,
                "batch_size": batch_size,
                "rank": rank,
            },
            num_gpus=num_gpus,
            batch_size=1,
            concurrency=1,
        )(col("text")),
    )

    ds.show()

    # ╭────────┬────────────────────────────────╮
    # │ text   ┆ embedding                      │
    # │ ---    ┆ ---                            │
    # │ Utf8   ┆ List[Float32]                  │
    # ╞════════╪════════════════════════════════╡
    # │ 皮卡丘  ┆ [0.12005615, -0.009140015, -0… │
    # ├╌╌╌╌╌╌╌╌┼╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌┤
    # │ 小狗    ┆ [0.12963867, 0.00039935112, 0… │
    # ├╌╌╌╌╌╌╌╌┼╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌┤
    # │ 小猫    ┆ [0.12670898, 0.015533447, 0.0… │
    # ├╌╌╌╌╌╌╌╌┼╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌┤
    # │ None   ┆ None                           │
    # ╰────────┴────────────────────────────────╯

    tos_dir_url = os.getenv("TOS_DIR_URL", "las-cn-beijing-public-online.tos-cn-beijing.volces.com")
    samples = {
        "image_path": [
            f"https://{tos_dir_url}/public/shared_image_dataset/cat_ip_adapter.jpeg"
        ]
    }
    ds = daft.from_pydict(samples)
    ds = ds.with_column(
        "embedding",
        las_udf(
            ClipEmbedding,
            construct_args={
                "content_type": "image_url",
                "model_path": model_path,
                "model_name": model_name,
                "model_version": model_version,
                "batch_size": batch_size,
                "rank": rank,
            },
            num_gpus=num_gpus,
            batch_size=1,
        )(col("image_path")),
    )

    ds.show()

    # ╭────────────────────────────────┬────────────────────────────────╮
    # │ image_path                     ┆ embedding                      │
    # │ ---                            ┆ ---                            │
    # │ Utf8                           ┆ List[Float32]                  │
    # ╞════════════════════════════════╪════════════════════════════════╡
    # │ tos://las-cn-beijing-public-o… ┆ [0.04598999, -0.090148926, -0… │
    # ╰────────────────────────────────┴────────────────────────────────╯
```
