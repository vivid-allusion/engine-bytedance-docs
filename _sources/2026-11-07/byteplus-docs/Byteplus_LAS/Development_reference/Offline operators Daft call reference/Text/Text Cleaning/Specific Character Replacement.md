---
title: "Specific Character Replacement"
product: "Lake AI Service"
product_code: "Byteplus_LAS"
source: "https://docs.byteplus.com/en/docs/Byteplus_LAS/Specific_Character_Replacement"
---

<span id="operator-introduction"></span>
# Operator introduction

<span id="description"></span>
## Description

**Regular Expression Batch Replacement Processor**

<span id="core-features"></span>
## Core Features


* Dual\-mode replacement mechanism:

   * Exact string match replacement

   * Regular expression pattern match replacement

* Batch processing capability:

   * Supports parallel processing of multiple `pattern-replacement` pairs

* Fault tolerance mechanism:

   * Skips abnormal modes and records detailed logs


<span id="daft-call"></span>
# Daft call

<span id="operator-parameters"></span>
## Operator parameters

<span id="input"></span>
## Input


|Input column name |Note |
|---|---|
|texts |An array containing original text content, with elements of string type |


<span id="output"></span>
## Output

An array of text content after replacement, with elements of string type

<span id="parameters"></span>
## Parameters

If a parameter does not have a default value, it is a required parameter.


|Parameter name |Type |Default value |Description |
|---|---|---|---|
|patterns |list | |A list of specific content to replace \* Supports regular expressions and specific strings \* Multi\-element lists will replace text content one by one \* Example: [r"\d+", "http://"] |
|replacements |list | |A list of content to replace with \* If there is only one element, use it to replace all content in patterns \* When there are multiple elements, replace one\-to\-one with patterns \* Example: ["NUM", "URL"] |


<span id="examples"></span>
## Examples

The following code shows how to use daft to run the operator to replace specific expressions.

```python
from __future__ import annotations

import os

import daft
from daft import col
from daft.las.functions.text.regex_replacement import RegexReplacer
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
            "<Query></Query><Title>提升党的领导力，推进国家治理体系和治理能力现代化</Title><Url>http://news.cnr.cn/native/gd/20191212/t20191212_524895559.shtml</Url>",
            None,
        ]
    }

    patterns = [r"<.*?>", "国家"]
    replacements = ["/replace_tag", "中国"]
    ds = daft.from_pydict(samples)
    ds = ds.with_column(
        "replaced_text",
        las_udf(
            RegexReplacer,
            construct_args={"patterns": patterns, "replacements": replacements},
        )(col("text")),
    )
    ds.show()

    # ╭───────────────────────────────────────┬────────────────────────────────╮
    # │ text                                  ┆ replaced_text                  │
    # │ ---                                   ┆ ---                            │
    # │ Utf8                                  ┆ Utf8                           │
    # ╞═══════════════════════════════════════╪════════════════════════════════╡
    # │ <Query></Query><Title>提升党的领导力…    ┆ /replace_tag/replace_tag/repl… │
    # ├╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌┼╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌┤
    # │ None                                  ┆ None                           │
    # ╰───────────────────────────────────────┴────────────────────────────────╯
```
