---
title: "Character Proportion Calculator"
product: "Lake AI Service"
product_code: "Byteplus_LAS"
source: "https://docs.byteplus.com/en/docs/Byteplus_LAS/Character_Proportion_Calculator"
---

<span id="operator-introduction"></span>
# Operator introduction

<span id="description"></span>
## Description

**Character Proportion Calculator \- Text Feature Extraction Based on Letter and Digit Character Proportions**

<span id="core-features"></span>
## Core Features


* Character proportion calculation: Accurately count the proportion of letter and digit characters in the text

* Word segmentation mode support: Option to calculate proportions based on word segmentation or character level

* Multilingual support: Supports character recognition for multiple languages including English, Chinese, Japanese, Korean, etc.


<span id="application-scenarios"></span>
## Application Scenarios


* Multilingual text quality assessment

* Data cleaning and preprocessing

* Text classification feature extraction

* Content security detection

* Multilingual text analysis


<span id="technical-features"></span>
## Technical Features


* Supports two calculation modes:

   * Character mode: Proportion of letter and digit characters to total characters

   * Word segmentation mode: Proportion of letter characters to total number of segmented words

* Supports multilingual Unicode character recognition, including but not limited to:

   * English letters (a\-z, A\-Z)

   * Chinese characters (Hanzi)

   * Japanese characters (Hiragana, Katakana, Kanji)

   * Korean characters (Hangul)

   * Digit characters (0\-9)


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

A column of ratio results, elements are floats representing the proportion of alphanumeric characters.

<span id="parameters"></span>
## Parameters

If a parameter does not have a default value, it is a required parameter.


|Parameter name |Type |Default value |Description |
|---|---|---|---|
|tokenization |bool |False |Whether to tokenize Description: Whether to calculate the ratio using tokenization mode Default value: False |
|model_path |str |/opt/las/models |Path where the model files are located Default value: "/opt/las/models" |
|model_name |str |pythia\-6.9b\-deduped |Model name Default value: "pythia\-6.9b\-deduped" |


<span id="examples"></span>
## Examples

The following code shows how to use daft to run the operator and calculate the proportion of alphanumeric characters in text.

```python
from __future__ import annotations

import os

import daft
from daft import col
from daft.las.functions.text.alphanumeric_ratio_calculator import AlphanumericRatioCalculator
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
            "HelloWorld123",
            "Hello, world!",
            "!!!@@@###$$$",
            "Test 123! Is it working?",
            "你好Hello123",
        ]
    }

    ds = daft.from_pydict(samples)
    ds = ds.with_column(
        "alphanumeric_ratio",
        las_udf(
            AlphanumericRatioCalculator,
            construct_args={"tokenization": False},
        )(col("text")),
    )

    ds.show()
    # ╭─────────────────────────┬─────────────────────╮
    # │ text                    ┆ alphanumeric_ratio  │
    # │ ---                     ┆ ---                 │
    # │ Utf8                    ┆ Float64             │
    # ╞═════════════════════════╪═════════════════════╡
    # │ HelloWorld123           ┆ 1.0                 │
    # │ Hello, world!           ┆ 0.7692307692307693  │
    # │ !!!@@@###$$$            ┆ 0.0                 │
    # │ Test 123! Is it work…   ┆ 0.75                │
    # │ 你好Hello123             ┆ 1.0                 │
    # ╰─────────────────────────┴─────────────────────╯
```
