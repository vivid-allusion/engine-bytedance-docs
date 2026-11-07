---
title: "Word Repetition Ratio Calculator"
product: "Lake AI Service"
product_code: "Byteplus_LAS"
source: "https://docs.byteplus.com/en/docs/Byteplus_LAS/Word_Repetition_Ratio_Calculator"
---

<span id="operator-introduction"></span>
# Operator introduction

<span id="description"></span>
## Description

**Word Repetition Ratio Calculator \- Text Feature Extraction Based on N\-gram Phrase Repetition Ratio**

<span id="core-features"></span>
## Core Features


* Word repetition ratio calculation: accurately count the proportion of repeated phrases in text

* Bilingual support: supports word segmentation for Chinese and English

* Flexible configuration: supports calculation of N\-gram phrases of different lengths


<span id="application-scenarios"></span>
## Application Scenarios


* Text quality assessment

* Data cleaning and preprocessing

* Content duplication detection


<span id="technical-features"></span>
## Technical Features


* Supports two word segmentation modes:

   * Space\-based segmentation: suitable for space\-separated languages like English

   * Model\-based segmentation: uses the sentencepiece model; Chinese must use this mode

* Configurable N\-gram length: supports combinations of 1\-N words

* Intelligent filtering: automatically filters special characters to improve calculation accuracy


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

A column of word repetition ratios, elements are floating\-point numbers representing the proportion of repeated phrases

<span id="parameters"></span>
## Parameters

If a parameter does not have a default value, it is a required parameter.


|Parameter name |Type |Default value |Description |
|---|---|---|---|
|repetition |int |5 |Phrase length Description: Number of words used to form a phrase Default value:5 |
|lang |str |zh |Language Description: Language of the text, supports zh (Chinese) and en (English) Default value:"zh" |
|tokenization |bool |True |Whether to use tokenizer Description: Whether to use the sentencepiece model for tokenization; must be enabled for Chinese Default value:True |
|model_path |str |/opt/las/models |Path where model files are located Default value:"/opt/las/models" |
|model_name |str |kenlm/wikipedia |Model name Default value:"kenlm/wikipedia" |


<span id="examples"></span>
## Examples

The following code shows how to use daft to run the operator to calculate the proportion of repeated phrases based on N\-grams in text.

```python
from __future__ import annotations

import os

import daft
from daft import col
from daft.las.functions.text.word_repetition_calculator import WordRepetitionCalculator
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
            "人工智能技术正在快速发展，人工智能技术在各领域的应用越来越广泛。人工智能技术可以帮助我们解决复杂问题，人工智能技术的未来充满无限可能。",
            "这是一个没有重复词汇的文本示例，每个词语都只出现一次。",
            None,
        ]
    }
    repetition = 2
    lang = "zh"
    tokenization = True

    ds = daft.from_pydict(samples)
    ds = ds.with_column(
        "repetition_ratio",
        las_udf(
            WordRepetitionCalculator,
            construct_args={
                "repetition": repetition,
                "lang": lang,
                "tokenization": tokenization,
                "model_path": os.getenv("MODEL_PATH", "/opt/las/models"),
                "model_name": "kenlm/wikipedia",
            },
        )(col("text")),
    )

    ds.show()
    # ╭─────────────────────────────────────────────────────────────┬─────────────────────╮
    # │ text                                                        ┆ repetition_ratio    │
    # │ ---                                                         ┆ ---                 │
    # │ String                                                      ┆ Float64             │
    # ╞═════════════════════════════════════════════════════════════╪═════════════════════╡
    # │ 人工智能技术正在快速发展，人工智能技术在各领域的应用越来越… ┆ 0.14285714285714285 │
    # ├╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌┼╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌┤
    # │ 这是一个没有重复词汇的文本示例，每个词语都只出现一次。      ┆ 0                   │
    # ├╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌┼╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌┤
    # │ None                                                        ┆ None                │
    # ╰─────────────────────────────────────────────────────────────┴─────────────────────╯
```
