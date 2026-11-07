---
title: "Copyright Notice Removal"
product: "Lake AI Service"
product_code: "Byteplus_LAS"
source: "https://docs.byteplus.com/en/docs/Byteplus_LAS/Copyright_Notice_Removal"
---

<span id="operator-introduction"></span>
# Operator introduction

<span id="description"></span>
## Description

**Copyright Notice Remover \- Remove text related to copyright notices from content**

<span id="core-features"></span>
## Core Features


* Copyright Notice Detection: Automatically identify copyright notice comments in code

* Intelligent Cleaning: Precisely remove content based on copyright notice characteristics

* Multi\-format Support: Supports block comment and line comment formats


<span id="application-scenarios"></span>
## Application Scenarios


* Code copyright notice cleaning

* Text preprocessing and standardization

* Code quality inspection and optimization


<span id="technical-features"></span>
## Technical Features


* Supports two copyright notice formats:

   * Block comment format: Comment blocks enclosed in /\* ... \*/ that contain the keyword "copyright"

   * Line comment format: Line comments starting with //, #, or \-\-


<span id="daft-call"></span>
# Daft call

<span id="operator-parameters"></span>
## Operator parameters

<span id="input"></span>
## Input


|Input column name |Note |
|---|---|
|texts |The text column to process, requiring elements of string type |


<span id="output"></span>
## Output

The cleaned text column with copyright statement\-related content removed

<span id="examples"></span>
## Examples

The following code shows how to use daft to run the operator to remove copyright statement content from text.

```python
from __future__ import annotations

import os

import daft
from daft import col
from daft.las.functions.text.copyright_cleaner import CopyrightCleaner
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
            "/* \n * Copyright (c) 2023 Jane Smith\n * 本代码依据 Apache License 2.0 授权，详见随附的 LICENSE 文件。\n */ 你好",
            "# 版权 (c) 2023 Jane Smith\n# 本代码依据 Apache License 2.0 授权，详见随附的 LICENSE 文件。\n 你好",
        ]
    }

    ds = daft.from_pydict(samples)
    ds = ds.with_column(
        "cleaned_text",
        las_udf(
            CopyrightCleaner,
            construct_args={},
        )(col("text")),
    )

    ds.show()
    # ╭──────────────────────────────────────────────┬──────────────────────────────────────────────╮
    # │ text                                         ┆ cleaned_text                                │
    # │ ---                                          ┆ ---                                          │
    # │ Utf8                                         ┆ Utf8                                         │
    # ╞══════════════════════════════════════════════╪══════════════════════════════════════════════╡
    # │ /* \n * Copyright (c) 2023 Jane Smith\n * 本    ┆  你好                                        │
    # │ 代码依据 Apache License 2.0 授权，详见随附的     ┆                                             │
    # │ LICENSE 文件。\n */ 你好                        ┆                                             │
    # ├╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌┼╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌┤
    # │ # 版权 (c) 2023 Jane Smith\n# 本代码依据 Apache    ┆  你好                                        │
    # │ License 2.0 授权，详见随附的 LICENSE 文件。\n     ┆                                             │
    # │ 你好                                          ┆                                             │
    # ╰──────────────────────────────────────────────┴──────────────────────────────────────────────╯
```
