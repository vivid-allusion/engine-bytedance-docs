---
title: "Whitespace Normalizer"
product: "Lake AI Service"
product_code: "Byteplus_LAS"
source: "https://docs.byteplus.com/en/docs/Byteplus_LAS/Whitespace_Normalizer"
---

<span id="operator-introduction"></span>
# Operator introduction

<span id="description"></span>
## Description

**Whitespace Normalizer \- Replace various whitespace characters in text with standard spaces**

<span id="core-features"></span>
## Core Features


* Whitespace Recognition: Automatically recognize various Unicode whitespace characters

* Normalization Processing: Replace all whitespace characters with standard spaces


<span id="application-scenarios"></span>
## Application Scenarios


* Text preprocessing

* Data cleaning and standardization

* Format unification

* Text normalization


<span id="technical-features"></span>
## Technical Features


* Supports multiple whitespace characters: spaces, tabs, line breaks, full\-width spaces, etc.

* Intelligent processing: Preserve text content, only replace whitespace characters

* Leading/trailing cleanup: Automatically remove leading and trailing whitespace characters from text

* Preserve structure: Does not change the basic structure and content of the text


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

The normalized text column

<span id="examples"></span>
## Examples

The following code shows how to use daft to run the operator to normalize whitespace characters in text.

```python
from __future__ import annotations

import os

import daft
from daft import col
from daft.las.functions.text.whitespace_normalizer import WhitespaceNormalizer
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
            "Hello\u2000World\u2001Test",
            "中文\u2002文本\u2003测试",
            "English\u2004中文\u2005Mixed",
            "Multiple\u2006\u2007\u2008Spaces",
        ]
    }

    ds = daft.from_pydict(samples)
    ds = ds.with_column(
        "normalized_text",
        las_udf(WhitespaceNormalizer)(col("text")),
    )

    ds.show()
    # ╭──────────────────────────────────────────────┬──────────────────────────────────────────────╮
    # │ text                                         ┆ normalized_text                             │
    # │ ---                                          ┆ ---                                          │
    # │ Utf8                                         ┆ Utf8                                         │
    # ╞══════════════════════════════════════════════╪══════════════════════════════════════════════╡
    # │ Hello World Test                             ┆ Hello World Test                             │
    # ├╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌┼╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌┤
    # │ 中文 文本 测试                                ┆ 中文 文本 测试                               │
    # ├╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌┼╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌┤
    # │ English 中文 Mixed                            ┆ English 中文 Mixed                            │
    # ├╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌┼╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌┤
    # │ Multiple   Spaces                            ┆ Multiple Spaces                              │
    # ╰──────────────────────────────────────────────┴──────────────────────────────────────────────╯
```
