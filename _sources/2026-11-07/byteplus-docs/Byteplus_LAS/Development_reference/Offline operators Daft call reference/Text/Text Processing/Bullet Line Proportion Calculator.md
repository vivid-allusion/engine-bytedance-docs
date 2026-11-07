---
title: "Bullet Line Proportion Calculator"
product: "Lake AI Service"
product_code: "Byteplus_LAS"
source: "https://docs.byteplus.com/en/docs/Byteplus_LAS/Bullet_Line_Proportion_Calculator"
---

<span id="operator-introduction"></span>
# Operator introduction

<span id="description"></span>
## Description

**Bullet Line Proportion Calculator \- Calculate the proportion of bullet lines in text**

<span id="core-features"></span>
## Core Features


* Bullet detection: Automatically identify lines starting with bullet points in text

* Proportion calculation: Calculate the ratio of the number of bullet lines to the total number of lines


<span id="application-scenarios"></span>
## Application Scenarios


* Text quality assessment

* Data cleaning and preprocessing


<span id="technical-features"></span>
## Technical Features


* Supports multiple bullet points: •, \-, ·, ●, ▪, —, \*, etc.

* Accurate identification: Only count lines starting with bullet points

* Result range: 0\-1; the closer to 1, the more bullet lines there are

* Intelligent filtering: Automatically filter blank lines without affecting calculation


<span id="daft-call"></span>
# Daft call

<span id="operator-parameters"></span>
## Operator parameters

<span id="input"></span>
## Input


|Input column name |Note |
|---|---|
|texts |The text column to process, requiring elements to be of string type |


<span id="output"></span>
## Output

A column of bullet line ratios, elements are floats representing the ratio of bullet lines

<span id="examples"></span>
## Examples

The code below shows how to use daft to run the operator and calculate the proportion of bullet lines in text.

```python
from __future__ import annotations

import os

import daft
from daft import col
from daft.las.functions.text.bullet_line_ratio_calculator import BulletLineRatioCalculator
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
            "第一行内容\n• 项目符号行1\n- 项目符号行2\n第三行内容\n* 项目符号行3",
            "这是普通文本\n没有任何项目符号\n都是正常的内容",
            "• 只有项目符号\n- 全是项目符号\n* 没有普通文本",
        ]
    }

    ds = daft.from_pydict(samples)
    ds = ds.with_column(
        "bullet_ratio",
        las_udf(BulletLineRatioCalculator)(col("text")),
    )

    ds.show()
    # ╭──────────────────────────────────────────────┬──────────────────────────────────────────────╮
    # │ text                                         ┆ bullet_ratio                                │
    # │ ---                                          ┆ ---                                          │
    # │ Utf8                                         ┆ Float64                                      │
    # ╞══════════════════════════════════════════════╪══════════════════════════════════════════════╡
    # │ 第一行内容\n• 项目符号行1\n- 项目符号行2\n第三行内容  ┆ 0.6                                         │
    # │ \* 项目符号行3                               ┆                                              │
    # ├╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌┼╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌┤
    # │ 这是普通文本\n没有任何项目符号\n都是正常的内容    ┆ 0.0                                         │
    # ├╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌┼╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌┤
    # │ • 只有项目符号\n- 全是项目符号\n* 没有普通文本    ┆ 1.0                                         │
    # ╰──────────────────────────────────────────────┴──────────────────────────────────────────────╯
```
