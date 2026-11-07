---
title: "Duplicate Line Calculator"
product: "Lake AI Service"
product_code: "Byteplus_LAS"
source: "https://docs.byteplus.com/en/docs/Byteplus_LAS/Duplicate_Line_Calculator"
---

<span id="operator-introduction"></span>
# Operator introduction

<span id="description"></span>
## Description

**Duplicate Line Calculator \- Calculate the Proportion of Duplicate Lines in Text**

<span id="core-features"></span>
## Core Features


* Duplicate line detection: Automatically identify duplicate line content in text

* Proportion calculation: Calculate the ratio of duplicate lines to original lines

* Quality assessment: Evaluate the repetition degree and quality of the text


<span id="application-scenarios"></span>
## Application Scenarios


* Text quality assessment

* Data cleaning and preprocessing

* Content duplication detection

* Document quality inspection


<span id="technical-features"></span>
## Technical Features


* Exact matching: Only identical content is considered duplicate

* Empty line filtering: Automatically filter blank lines without affecting calculations

* Result range: 0\-1, closer to 1 means more duplicates


<span id="daft-call"></span>
# Daft call

<span id="operator-parameters"></span>
## Operator parameters

<span id="input"></span>
## Input


|Input column name |Note |
|---|---|
|texts |The text column to process, requires elements to be of string type |


<span id="output"></span>
## Output

A column of repeated line ratios, elements are floating\-point numbers representing the ratio of repeated lines

<span id="examples"></span>
## Examples

The following code shows how to use daft to run the operator to calculate the ratio of repeated lines in text.

```python
from __future__ import annotations

import os

import daft
from daft import col
from daft.las.functions.text.repeated_lines_calculator import RepeatedLinesCalculator
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
            "第一行内容\n第二行内容\n第一行内容\n第三行内容",
            "第一行内容\n第一行内容\n第一行内容",
            "第一行内容\n\n第二行内容\n   \n第三行内容",
        ]
    }

    ds = daft.from_pydict(samples)
    ds = ds.with_column(
        "repeated_ratio",
        las_udf(
            RepeatedLinesCalculator,
            construct_args={},
        )(col("text")),
    )

    ds.show()
    
    # ╭────────────┬────────────────────╮
    # │ text       ┆ repeated_ratio     │
    # │ ---        ┆ ---                │
    # │ String     ┆ Float64            │
    # ╞════════════╪════════════════════╡
    # │ 第一行内容 ┆ 0.25               │
    # │ 第二行内容 ┆                    │
    # │ 第一行内容 ┆                    │
    # │ 第三行内容 ┆                    │
    # ├╌╌╌╌╌╌╌╌╌╌╌╌┼╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌┤
    # │ 第一行内容 ┆ 0.6666666666666666 │
    # │ 第一行内容 ┆                    │
    # │ 第一行内容 ┆                    │
    # ├╌╌╌╌╌╌╌╌╌╌╌╌┼╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌┤
    # │ 第一行内容 ┆ 0                  │
    # │            ┆                    │
    # │ 第二行内容 ┆                    │
    # │            ┆                    │
    # │ 第三行内容 ┆                    │
    # ╰────────────┴────────────────────╯
```
