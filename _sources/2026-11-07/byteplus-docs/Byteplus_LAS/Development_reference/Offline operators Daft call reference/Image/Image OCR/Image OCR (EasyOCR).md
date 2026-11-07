---
title: "Image OCR (EasyOCR)"
product: "Lake AI Service"
product_code: "Byteplus_LAS"
source: "https://docs.byteplus.com/en/docs/Byteplus_LAS/Image-OCR-EasyOCR"
---

<span id="operator-introduction"></span>
# Operator introduction

<span id="description"></span>
## Description

**A multilingual OCR recognition component based on EasyOCR, supporting text detection and recognition in mixed Chinese and English scenarios.** 

<span id="core-features"></span>
## Core Features


* Supports recognition of over 100 languages (requires configuration of corresponding language models)

* Input format compatibility:

   * TOS URL

   * Base64 encoding

   * Binary stream

   * Numpy array

* Performance optimization:

   * GPU\-accelerated inference

   * Model quantization (enabled by default)

   * Batch processing optimization


<span id="multilingual-support"></span>
## Multilingual Support


* Simplified Chinese (ch_sim)

* English (en)

* Japanese (ja)

* Korean (ko)

* French (fr)

* German (de)


Refer to the official documentation for the complete list of languages: https://www.jaided.ai/easyocr/

<span id="daft-call"></span>
# Daft call

<span id="operator-parameters"></span>
## Operator parameters

<span id="input"></span>
## Input


|Input column name |Note |
|---|---|
|images |An array containing image data, supporting URL/base64/binary formats |


<span id="output"></span>
## Output

An array containing OCR recognition results, with elements of string type

<span id="parameters"></span>
## Parameters

If a parameter does not have a default value, it is a required parameter.


|Parameter name |Type |Default value |Description |
|---|---|---|---|
|image_src_type |str |image_url |The format type of the input image, supporting: \- tos/http address (image_url) \- base64 encoding (image_base64) \- binary stream (image_binary) Optional values: ["image_url", "image_base64", "image_binary"] Default value: "image_url" |
|model_path |str |/opt/las/models |Model storage path. Default value: "/opt/las/models" |
|model_name |str |EasyOCR |The name of the model used, currently only supporting "EasyOCR". Default value: "EasyOCR" |
|quantize |bool |True |Whether to enable model quantization to accelerate inference. Default value: True |
|lang_list |list |[en, ch_sim] |List of supported languages for recognition, see https://www.jaided.ai/easyocr/ for details. Default value: ["en", "ch_sim"] |
|batch_size |int |16 |Batch size for GPU inference (adjustable based on GPU memory). Default value: 16 |


<span id="examples"></span>
## Examples

The following code shows how to use daft to run the operator to recognize text in images.

```python
from __future__ import annotations

import os

import daft
from daft import col
from daft.las.functions.image.image_easyocr import ImageEasyOcr
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

    tos_dir_url = os.getenv("TOS_DIR_URL", "las-cn-beijing-public-online.tos-cn-beijing.volces.com")
    samples = {
        "image": [
            f"https://{tos_dir_url}/public/shared_image_dataset/通用场景图片.jpeg"
        ]
    }

    image_src_type = "image_url"
    model_path = os.getenv("MODEL_PATH", "/opt/las/models")
    model_name = "EasyOCR"
    quantize = True
    lang_list = ["en", "ch_sim"]
    batch_size = 16
    num_gpus = 1

    ds = daft.from_pydict(samples)
    ds = ds.with_column(
        "ocr_result",
        las_udf(
            ImageEasyOcr,
            construct_args={
                "image_src_type": image_src_type,
                "model_path": model_path,
                "model_name": model_name,
                "quantize": quantize,
                "lang_list": lang_list,
                "batch_size": batch_size,
            },
            num_gpus=num_gpus,
            batch_size=1,
        )(col("image")),
    )
    ds.show()
    df = ds.to_pandas()

    # ╭────────────────────────────────┬───────────────────╮
    # │ image                          ┆ ocr_result        │
    # │ ---                            ┆ ---               │
    # │ Utf8                           ┆ Utf8              │
    # ╞════════════════════════════════╪═══════════════════╡
    # │ tos://las-cn-beijing-public-o… ┆ 不论结局           │
    # │                                ┆ 我己经很感谢相遇…    │
    # ╰────────────────────────────────┴───────────────────╯
```
