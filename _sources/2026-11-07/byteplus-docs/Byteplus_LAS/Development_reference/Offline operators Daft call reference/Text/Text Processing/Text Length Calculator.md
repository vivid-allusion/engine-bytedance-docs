---
title: "Text Length Calculator"
product: "Lake AI Service"
product_code: "Byteplus_LAS"
source: "https://docs.byteplus.com/en/docs/Byteplus_LAS/Text_Length_Calculator"
---

<span id="operator-introduction"></span>
# Operator introduction

<span id="description"></span>
## Description

**Text Length Calculator \- Calculate the character length of text**

<span id="core-features"></span>
## Core Features


* Text length calculation: Calculate the number of characters in the input text

* Batch processing: Support batch text length calculation

* Numeric output: Return the length value as an integer type


<span id="application-scenarios"></span>
## Application Scenarios


* Text length statistical analysis

* Data quality inspection

* Text preprocessing and filtering


<span id="technical-features"></span>
## Technical Features


* Precise calculation: Use Python's built\-in len() function to count characters

* Type safety: Ensure input is of string type


<span id="daft-call"></span>
# Daft call

<span id="operator-parameters"></span>
## Operator parameters

<span id="input"></span>
## Input


|Input column name |Note |
|---|---|
|texts |The text column to be processed; elements must be of string type. |


<span id="output"></span>
## Output

A column of text lengths; elements are of integer type.

<span id="examples"></span>
## Examples

The following code demonstrates how to use daft to run the operator and calculate the character lengths of text.

```python
from __future__ import annotations

import os

import daft
from daft import col
from daft.las.functions.text.text_length_calculator import TextLengthCalculator
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
            "Hello World",
            "你好世界",
            "Python编程 is fun",
            None,
        ]
    }

    ds = daft.from_pydict(samples)
    ds = ds.with_column(
        "length",
        las_udf(
            TextLengthCalculator,
            construct_args={},
        )(col("text")),
    )

    ds.show()
    # ╭───────────────────┬────────╮
    # │ text              ┆ length │
    # │ ---               ┆ ---    │
    # │ String            ┆ Int64  │
    # ╞═══════════════════╪════════╡
    # │ Hello World       ┆ 11     │
    # ├╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌┼╌╌╌╌╌╌╌╌┤
    # │ 你好世界          ┆ 4      │
    # ├╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌┼╌╌╌╌╌╌╌╌┤
    # │ Python编程 is fun ┆ 15     │
    # ├╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌┼╌╌╌╌╌╌╌╌┤
    # │ None              ┆ None   │
    # ╰───────────────────┴────────╯
```
