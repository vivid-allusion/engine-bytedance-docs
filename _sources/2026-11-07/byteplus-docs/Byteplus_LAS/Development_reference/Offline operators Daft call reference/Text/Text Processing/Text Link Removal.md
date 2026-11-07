---
title: "Text Link Removal"
product: "Lake AI Service"
product_code: "Byteplus_LAS"
source: "https://docs.byteplus.com/en/docs/Byteplus_LAS/Text_Link_Removal"
---

<span id="operator-introduction"></span>
# Operator introduction

<span id="description"></span>
## Description

**Hyperlink Removal Operator \- Text Link Regex Replacement**

<span id="core-features"></span>
## Core Features


* Identify common forms of hyperlinks such as protocol links, www links, domain names + paths, etc.

* Replace matched hyperlinks with a specified string (`repl`), defaulting to ""

* Process strings in batches, return None for abnormal items


<span id="technical-implementation"></span>
## Technical Implementation


* Regex matching: The default built\-in expression is semantically equivalent to the LAS version

* Compatible with the r'...'/r"..." wrapping format of incoming strings (remove the prefix r and quotes)

* Precompile regex and enable DOTALL semantics to cover multi\-line text

* Logging: Output default/custom regex and processing statistics for easy troubleshooting


<span id="daft-call"></span>
# Daft call

<span id="operator-parameters"></span>
## Operator parameters

<span id="input"></span>
## Input


|Input column name |Note |
|---|---|
|texts |Array of strings, each element is text content |


<span id="output"></span>
## Output

Processed array of strings; returns `None` for abnormal items

<span id="parameters"></span>
## Parameters

If a parameter does not have a default value, it is a required parameter.


|Parameter name |Type |Default value |Description |
|---|---|---|---|
|pattern |str | |Regular expression for hyperlink positioning. If empty, uses the operator's built\-in expression; compatible with wrapping forms like `r'...'` or `r"..."` |
|repl |str | |String to replace matched hyperlinks; defaults to empty string |


<span id="examples"></span>
## Examples

The following code shows how to use daft to run the operator to remove links from text.

```python
from __future__ import annotations

import logging
import os

import ray

import daft
from daft import col
from daft.las.functions.text.remove_links import RemoveLinks
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
            "prefix https://example.com/path suffix",
            None,
        ]
    }

    pattern = ""
    repl = "[LINK]"

    ds = daft.from_pydict(samples)

    ds = ds.with_column(
        "cleaned_text",
        las_udf(
            RemoveLinks,
            construct_args={"pattern": pattern, "repl": repl},
        )(col("text")),
    )
    ds.show()

    # ╭────────────────────────────────┬──────────────────────╮
    # │ text                           ┆ cleaned_text         │
    # │ ---                            ┆ ---                  │
    # │ Utf8                           ┆ Utf8                 │
    # ╞════════════════════════════════╪══════════════════════╡
    # │ prefix https://example.com/pa… ┆ prefix [LINK] suffix │
    # ├╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌┼╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌┤
    # │ None                           ┆ None                 │
    # ╰────────────────────────────────┴──────────────────────╯
```
