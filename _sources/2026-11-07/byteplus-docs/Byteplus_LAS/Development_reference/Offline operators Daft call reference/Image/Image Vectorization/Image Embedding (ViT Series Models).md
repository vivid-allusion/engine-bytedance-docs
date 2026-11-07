---
title: "Image Embedding (ViT Series Models)"
product: "Lake AI Service"
product_code: "Byteplus_LAS"
source: "https://docs.byteplus.com/en/docs/Byteplus_LAS/Image-Embedding-ViT"
---

<span id="operator-introduction"></span>
# Operator introduction

<span id="description"></span>
## Description

**ViT Image Semantic Embedding Processor, suitable for scenarios like image similarity search and content retrieval.** 

<span id="core-features"></span>
## Core Features


* Multi\-model support:

   * Google official ViT models

   * Meta DINOv2 visual models

* Feature extraction modes:

   * CLS Token embedding vector

   * Global average pooling

* Input format compatibility:

   * URL

   * Base64 encoding

   * Binary stream

* Performance optimizations:

   * FP16 inference acceleration

   * Multi\-GPU parallel computing


<span id="fault-tolerance-mechanism"></span>
## Fault Tolerance Mechanism


* Returns an all\-zero vector when extraction fails


<span id="recommended-models"></span>
## Recommended Models


* `google/vit-base-patch16-224-in21k` (768 dimensions)

* `google/vit-large-patch16-224-in21k` (1024 dimensions)

* `facebook/dinov2-base` (768 dimensions)

* `facebook/dinov2-large` (1024 dimensions)


<span id="daft-call"></span>
# Daft call

<span id="operator-parameters"></span>
## Operator parameters

<span id="input"></span>
## Input


|Input column name |Note |
|---|---|
|images |An array containing image data, where elements can be image URLs, Base64 encoded strings, or binary data |


<span id="output"></span>
## Output

An array containing feature vectors, where each element is a nested array of float type, and the array dimension is determined by the model output

<span id="parameters"></span>
## Parameters

If a parameter does not have a default value, it is a required parameter.


|Parameter name |Type |Default value |Description |
|---|---|---|---|
|image_src_type |str |image_url |Input image format type, supports: \- tos/http address (image_url) \- base64 encoding (image_base64) \- binary stream (image_binary) Optional values: ["image_url", "image_base64", "image_binary"] Default value: "image_url" |
|dtype |str |float32 |Model inference precision option: \- bfloat16: Balances precision and speed (faster on TPU) \- float16: Faster inference speed \- float32: Highest precision but largest memory consumption Optional values: ["bfloat16", "float16", "float32"] Default value: "float16" |
|batch_size |int |32 |Batch size Default value:32 |
|model_path |str |/opt/las/models |Model file storage path Default value: "/opt/las/models" |
|model_name |str |facebook/dinov2\-large |Name of the image vector model to use Optional values: [ "google/vit\-base\-patch16\-224\-in21k", "google/vit\-large\-patch16\-224\-in21k", "facebook/dinov2\-base", "facebook/dinov2\-large" ] Default value: "facebook/dinov2\-large" |
|use_cls_token_embedding |bool |True |Whether to use CLS Token features Default value: True |
|rank |int |0 |Specifies the GPU device ID to use (valid in multi\-card environments). For example:0 means the first GPU, and1 means the second GPU Default value:0 |


<span id="examples"></span>
## Examples

The following code shows how to use daft to run the operator to compute image embeddings.

```python
from __future__ import annotations

import logging
import os

import ray

import daft
from daft import col
from daft.las.functions.image.embedding.image_vit_embedding import ImageViTEmbedding
from daft.las.functions.udf import las_udf

if __name__ == "__main__":

    if os.getenv("DAFT_RUNNER", "ray") == "ray":

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

        import ray

        ray.init(dashboard_host="0.0.0.0", runtime_env={"worker_process_setup_hook": configure_logging})
        daft.set_runner_ray()

    daft.set_execution_config(actor_udf_ready_timeout=600)
    daft.set_execution_config(min_cpu_per_task=0)

    tos_dir_url = os.getenv("TOS_DIR_URL", "las-cn-beijing-public-online.tos-cn-beijing.volces.com")
    samples = {
        "image": [
            f"https://{tos_dir_url}/public/shared_image_dataset/cat_ip_adapter.jpeg"
        ]
    }

    image_src_type = "image_url"
    batch_size = 64
    model_path = os.getenv("MODEL_PATH", "/opt/las/models")
    model_name = "google/vit-base-patch16-224-in21k"
    dtype = "float32"
    use_cls_token_embedding = True
    rank = 0
    num_gpus = 1

    ds = daft.from_pydict(samples)
    ds = ds.with_column(
        "embedding",
        las_udf(
            ImageViTEmbedding,
            construct_args={
                "image_src_type": image_src_type,
                "batch_size": batch_size,
                "model_path": model_path,
                "model_name": model_name,
                "dtype": dtype,
                "use_cls_token_embedding": use_cls_token_embedding,
                "rank": rank,
            },
            num_gpus=num_gpus,
            batch_size=1,
        )(col("image")),
    )

    ds.show()

    # ╭────────────────────────────────┬────────────────────────────────╮
    # │ image                          ┆ embedding                      │
    # │ ---                            ┆ ---                            │
    # │ Utf8                           ┆ List[Float32]                  │
    # ╞════════════════════════════════╪════════════════════════════════╡
    # │ tos://las-cn-beijing-public-o… ┆[-0.011575016, -0.019808339, …  │
    # ╰────────────────────────────────┴────────────────────────────────╯
```
