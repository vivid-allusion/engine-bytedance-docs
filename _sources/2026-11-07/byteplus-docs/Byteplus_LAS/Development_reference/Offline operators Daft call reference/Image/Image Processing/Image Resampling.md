---
title: "Image Resampling"
product: "Lake AI Service"
product_code: "Byteplus_LAS"
source: "https://docs.byteplus.com/en/docs/Byteplus_LAS/Image_Resampling"
---

<span id="operator-introduction"></span>
# Operator introduction

<span id="description"></span>
## Description

**Image resampling processor, supporting multiple interpolation algorithms and output formats.** 

<span id="core-features"></span>
## Core Features


* Offers 4 professional\-grade interpolation algorithms:

   * Nearest\-neighbor interpolation (nearest) \- Fastest speed, suitable for pixel art

   * Bilinear interpolation (bilinear) \- Balances speed and quality

   * Bicubic interpolation (bicubic) \- High\-precision smooth processing

   * Lanczos interpolation (lanczos) \- Best anti\-aliasing, suitable for photos

* Multi\-format input support:

   * URL address (image_url)

   * Base64 encoding (image_base64)

   * Binary stream (image_binary)

* Dual output modes:

   * Direct Base64 encoding output

   * TOS persistent storage


<span id="daft-call"></span>
# Daft call

<span id="operator-parameters"></span>
## Operator parameters

<span id="input"></span>
## Input


|Input column name |Note |
|---|---|
|images |An array containing input images, supporting URL/base64/binary formats |
|images_name |Optional parameter, an array containing image identifiers, used to generate output filenames. It is recommended to pass this to ensure filename uniqueness, and do not include a suffix; if not passed, a random name will be generated for images whose names cannot be parsed. |


<span id="output"></span>
## Output

An array of dictionaries containing processing results, each element includes:


* base64: base64 encoding of the resampled image;

* image_path: local/TOS storage path (valid when output directory is configured)


<span id="parameters"></span>
## Parameters

If a parameter does not have a default value, it is a required parameter.


|Parameter name |Type |Default value |Description |
|---|---|---|---|
|image_suffix |str |.jpg |Image format saved to TOS. Description: Image format saved to TOS, default is '.jpg' Optional values: [".jpg", ".png"] Default value: ".jpg" |
|tos_dir |str | |TOS folder path to save images. Description: TOS path where resampled images are saved; if not set, resampled images will not be saved to TOS. Default value: "" |
|local_dir |str | |Local folder path to save images. Description: Local storage directory for adjusted images; if empty, adjusted images will not be saved locally. Default value: "" |
|image_src_type |str |image_url |Format type of input images, supports: \- url address (image_url) \- base64 encoding (image_base64) \- binary stream (image_binary) Description: Format type of input images. Optional values: ["image_url", "image_base64", "image_binary"] Default value: "image_url" |
|target_size |list |[200, 200] |Size of the resampled image. Description: Size of the resampled image, format is [width, height], default is [200, 200]. Default value: [200, 200] |
|target_dpi |list |[72, 72] |Image DPI. Description: Image DPI, format is [width, height], default is [72, 72]. Default value: [72, 72] |
|method |str |lanczos |Resampling method. Description: Resampling method, supports nearest (nearest neighbor interpolation), bilinear (bilinear interpolation), bicubic (bicubic interpolation), lanczos (Lanczos interpolation), default is lanczos. Optional values: ["nearest", "bilinear", "bicubic", "lanczos"] Default value: "lanczos" |


<span id="examples"></span>
## Examples

The following code shows how to use daft to run the operator for image resampling.

```python
from __future__ import annotations

import os

import daft
from daft import col
from daft.las.functions.image.image_resample import ImageResample
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
            f"https://{tos_dir_url}/public/shared_image_dataset/cat_ip_adapter.jpeg"
        ],
        "image_name": ["cat_ip_adapter"],
    }

    image_suffix = ".jpg"
    image_src_type = "image_url"
    target_size = (200, 200)
    target_dpi = (72, 72)
    method = "lanczos"
    local_dir = ""
    tos_dir = ""
    num_gpus = 0

    ds = daft.from_pydict(samples)
    ds = ds.with_column(
        "image_resample",
        las_udf(
            ImageResample,
            construct_args={
                "image_suffix": image_suffix,
                "tos_dir": tos_dir,
                "local_dir": local_dir,
                "image_src_type": image_src_type,
                "target_size": target_size,
                "target_dpi": target_dpi,
                "method": method,
            },
            num_gpus=num_gpus,
            batch_size=1,
        )(col("image"), col("image_name")),
    )

    ds.show()

    # ╭────────────────────────────────┬────────────────┬────────────────────────────────────────╮
    # │ image                          ┆ image_name     ┆ image_resample                         │
    # │ ---                            ┆ ---            ┆ ---                                    │
    # │ Utf8                           ┆ Utf8           ┆ Struct[base64: Utf8, image_path: Utf8] │
    # ╞════════════════════════════════╪════════════════╪════════════════════════════════════════╡
    # │ https://las-cn-beijing-public… ┆ cat_ip_adapter ┆ {base64: iVBORw0KGgoAAAANSUhE…         │
    # ╰────────────────────────────────┴────────────────┴────────────────────────────────────────╯
```
