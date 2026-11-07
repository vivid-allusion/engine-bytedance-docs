---
title: "Maximum English Word Length Calculator"
product: "Lake AI Service"
product_code: "Byteplus_LAS"
source: "https://docs.byteplus.com/en/docs/Byteplus_LAS/Maximum_English_Word_Length_Calculator"
---

<span id="operator-introduction"></span>
# Operator introduction

<span id="description"></span>
## Description

**Maximum English Word Length Calculator \- Calculate the maximum length of English words in text**

<span id="core-features"></span>
## Core Features


* English word recognition: Use regular expressions to identify English words in text

* Maximum length calculation: Calculate the maximum length among all English words

* Batch processing: Support maximum English word length calculation for batch texts


<span id="application-scenarios"></span>
## Application Scenarios


* Text quality check

* Data preprocessing and filtering


<span id="technical-features"></span>
## Technical Features


* Recognize only English words: Use the regular expression `[A-Za-z]+` to match English words

* Intelligent processing: Automatically ignore non\-English words and only calculate the length of English words


<span id="daft-call"></span>
# Daft call

<span id="operator-parameters"></span>
## Operator parameters

<span id="input"></span>
## Input


|Input column name |Note |
|---|---|
|texts |The text column to process; elements must be of string type |


<span id="output"></span>
## Output

Column of maximum word lengths, element type is integer

<span id="examples"></span>
## Examples

The following code demonstrates how to use daft to run the operator and calculate the maximum length of English words in text.

```python
from __future__ import annotations

import os

import daft
from daft import col
from daft.las.functions.text.maximum_word_length_calculator import MaximumWordLengthCalculator
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
            "Hello world 你好世界",
            "Python编程 is fun",
            "这是一个中文句子",
            "The quick brown fox jumps over the lazy dog",
            "supercalifragilisticexpialidocious is a very long word",
            None,
        ]
    }

    ds = daft.from_pydict(samples)
    ds = ds.with_column(
        "max_word_length",
        las_udf(
            MaximumWordLengthCalculator,
            construct_args={},
        )(col("text")),
    )

    ds.show()
    # ╭────────────────────────────────┬─────────────────╮
    # │ text                           ┆ max_word_length │
    # │ ---                            ┆ ---             │
    # │ String                         ┆ Int64           │
    # ╞════════════════════════════════╪═════════════════╡
    # │ Hello world 你好世界           ┆ 5               │
    # ├╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌┼╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌┤
    # │ Python编程 is fun              ┆ 6               │
    # ├╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌┼╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌┤
    # │ 这是一个中文句子               ┆ 0               │
    # ├╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌┼╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌┤
    # │ The quick brown fox jumps ove… ┆ 5               │
    # ├╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌┼╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌┤
    # │ supercalifragilisticexpialido… ┆ 34              │
    # ├╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌┼╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌┤
    # │ None                           ┆ None            │
    # ╰────────────────────────────────┴─────────────────╯
```
