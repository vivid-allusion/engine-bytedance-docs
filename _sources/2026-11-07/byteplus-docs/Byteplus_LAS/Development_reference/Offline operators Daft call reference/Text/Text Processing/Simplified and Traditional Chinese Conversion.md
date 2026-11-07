---
title: "Simplified and Traditional Chinese Conversion"
product: "Lake AI Service"
product_code: "Byteplus_LAS"
source: "https://docs.byteplus.com/en/docs/Byteplus_LAS/Simplified_and_Traditional_Chinese_Conversion"
---

<span id="operator-introduction"></span>
# Operator introduction

<span id="description"></span>
## Description

**OpenCC\-based Chinese Simplified\-Traditional Conversion Operator**

<span id="core-features"></span>
## Core Features


* **Multi\-directional Conversion**: Supports multiple conversion directions such as Simplified\-Traditional Chinese, Taiwan Traditional, Hong Kong Traditional, etc.

* **Mixed Text Processing**: Correctly handles content mixed with Chinese and English, converting only the Chinese part.

* **Efficient Batch Processing**: Supports fast conversion processing of large batches of text.


<span id="technical-implementation"></span>
## Technical Implementation


* **Conversion Engine**: Uses OpenCC for conversion.


<span id="daft-call"></span>
# Daft call

<span id="operator-parameters"></span>
## Operator parameters

<span id="input"></span>
## Input


|Input column name |Note |
|---|---|
|texts |A column containing text to be converted, with elements of string type. |


<span id="output"></span>
## Output

The converted text column, with elements of string type.

<span id="parameters"></span>
## Parameters

If a parameter does not have a default value, it is a required parameter.


|Parameter name |Type |Default value |Description |
|---|---|---|---|
|direction |str |t2s |Conversion direction Optional values: ["t2s", "s2t", "t2tw", "s2tw", "t2hk", "s2hk", "tw2s", "hk2s"] Default value: "t2s" (Traditional Chinese to Simplified Chinese) |


<span id="examples"></span>
## Examples

The code below shows how to use daft to run the operator for Chinese Simplified and Traditional conversion.

```python
from __future__ import annotations

import os

import pandas as pd

import daft
from daft import col
from daft.las.functions.text.chinese_text_converter import ChineseTextConverter
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
            "這是一個繁體中文的測試文本，包含了一些專業術語和技術名詞。",
            "Hello 世界！這裡有中英文混雜的內容，測試OpenCC是否能正確處理。",
            "Mixed content: 繁體字轉換測試 with English words and numbers 123。",
            None,
        ]
    }

    df = pd.DataFrame(samples)
    ds = daft.from_pandas(df)

    ds = ds.with_column(
        "converted_text",
        las_udf(
            ChineseTextConverter,
            construct_args={
                "direction": "t2s",
            },
            num_gpus=0,
            batch_size=1,
            concurrency=1,
        )(col("text")),
    )

    ds.show()
    # ╭─────────────────────────────────────────────────────────────────────────────────┬─────────────────────────────────────────────────────────────────────────────────╮
    # │ text                                                                            ┆ converted_text                                                                  │
    # │ ---                                                                             ┆ ---                                                                             │
    # │ Utf8                                                                            ┆ Utf8                                                                            │
    # ╞═════════════════════════════════════════════════════════════════════════════════╪═════════════════════════════════════════════════════════════════════════════════╡
    # │ 這是一個繁體中文的測試文本，包含了一些專業術語和技術名詞。                                ┆ 这是一个繁体中文的测试文本，包含了一些专业术语和技术名词。                                │
    # ├╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌┼╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌┤
    # │ Hello 世界！這裡有中英文混雜的內容，測試OpenCC是否能正確處理。                           ┆ Hello 世界！这里有中英文混杂的内容，测试OpenCC是否能正确处理。                          │
    # ├╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌┼╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌┤
    # │ Mixed content: 繁體字轉換測試 with English words and numbers 123。                 ┆ Mixed content: 繁体字转换测试 with English words and numbers 123。                │
    # ├╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌┼╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌┤
    # │ None                                                                            ┆ None                                                                            │
    # ╰─────────────────────────────────────────────────────────────────────────────────┴─────────────────────────────────────────────────────────────────────────────────╯
```
