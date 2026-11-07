---
title: "Special Character Proportion Calculator"
product: "Lake AI Service"
product_code: "Byteplus_LAS"
source: "https://docs.byteplus.com/en/docs/Byteplus_LAS/Special_Character_Proportion_Calculator"
---

<span id="operator-introduction"></span>
# Operator introduction

<span id="description"></span>
## Description

**Special Character Proportion Calculator \- Text Feature Extraction Based on Special Character Proportion**

<span id="core-features"></span>
## Core Features


* Special Character Proportion Calculation: Precisely count the proportion of special characters in text

* Multi\-granularity Support: Allows selection of different types of special characters for calculation

* Flexible Configuration: Supports calculating the proportion of all special characters or specific types


<span id="application-scenarios"></span>
## Application Scenarios


* Text Quality Evaluation

* Data Cleaning and Preprocessing

* Text Classification Feature Extraction

* Content Security Detection

* Multilingual Text Analysis


<span id="technical-features"></span>
## Technical Features


* Supports Multiple Character Types:

   * all: All special characters (default)

   * whitespace: Whitespace characters

   * punctuation: Punctuation marks

   * digits: Digit characters

   * emoji: Emoji symbols

* Supports multilingual Unicode character recognition


<span id="daft-call"></span>
# Daft call

<span id="operator-parameters"></span>
## Operator parameters

<span id="input"></span>
## Input


|Input column name |Note |
|---|---|
|texts |The text column to process, elements must be strings |


<span id="output"></span>
## Output

The ratio result column, elements are floats representing the proportion of special characters

<span id="parameters"></span>
## Parameters

If a parameter does not have a default value, it is a required parameter.


|Parameter name |Type |Default value |Description |
|---|---|---|---|
|character_type |str |all |Character type Description: Select the type of special characters to calculate Optional values: all, whitespace, punctuation, digits, emoji Default value: all |


<span id="examples"></span>
## Examples

The code below shows how to use daft to run the operator and calculate the proportion of special characters in text.

```python
from __future__ import annotations

import os

import daft
from daft import col
from daft.las.functions.text.special_characters_ratio_calculator import SpecialCharactersRatioCalculator
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
            "Hello world!",
            "1234567890",
            "     ",
            "这是中文文本",
            "你好 Hello 😊 123 !!!",
        ]
    }

    ds = daft.from_pydict(samples)
    ds = ds.with_column(
        "special_ratio",
        las_udf(
            SpecialCharactersRatioCalculator,
            construct_args={"character_type": "all"},
        )(col("text")),
    )

    ds.show()
    # ╭───────────────────────┬─────────────────────╮                                                                                               
    # │ text                  ┆ special_ratio       │
    # │ ---                   ┆ ---                 │
    # │ String                ┆ Float64             │
    # ╞═══════════════════════╪═════════════════════╡
    # │ Hello world!          ┆ 0.16666666666666666 │
    # ├╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌┼╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌┤
    # │ 1234567890            ┆ 1                   │
    # ├╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌┼╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌┤
    # │                       ┆ None                │
    # ├╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌┼╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌┤
    # │ 这是中文文本          ┆ 0                   │
    # ├╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌┼╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌┤
    # │ 你好 Hello 😊 123 !!! ┆ 0.6111111111111112  │
    # ╰───────────────────────┴─────────────────────╯
```
