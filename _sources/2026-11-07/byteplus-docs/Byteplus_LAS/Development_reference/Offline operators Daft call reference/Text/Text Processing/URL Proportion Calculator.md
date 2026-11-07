---
title: "URL Proportion Calculator"
product: "Lake AI Service"
product_code: "Byteplus_LAS"
source: "https://docs.byteplus.com/en/docs/Byteplus_LAS/URL_Proportion_Calculator"
---

<span id="operator-introduction"></span>
# Operator introduction

<span id="description"></span>
## Description

**URL Proportion Calculator \- Text Feature Extraction Based on URL Character Proportion**

<span id="core-features"></span>
## Core Features


* URL Proportion Calculation: Precisely count the proportion of URL characters in the text

* Multi\-protocol Support: Supports multiple URL protocols including HTTP, HTTPS

* Intelligent Recognition: Accurately identify URL formats using regular expressions


<span id="application-scenarios"></span>
## Application Scenarios


* Text Quality Assessment

* Data Cleaning and Preprocessing

* Text Classification Feature Extraction

* Content Security Detection

* Web Content Analysis


<span id="technical-features"></span>
## Technical Features


* URL Character Proportion: The ratio of URL characters to the total number of characters

* Supports multiple URL formats, including but not limited to:

   * HTTP/HTTPS links

   * URLs with query parameters

   * URLs with anchors

   * URLs with ports


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

A column of ratio results, elements are floating\-point numbers representing the proportion of URL characters

<span id="examples"></span>
## Examples

The following code shows how to use daft to run the operator and calculate the proportion of URL characters in text.

```python
from __future__ import annotations

import os

import daft
from daft import col
from daft.las.functions.text.url_ratio_calculator import UrlRatioCalculator
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
            "Hello world",
            "Check out https://example.com for more info",
            "Visit http://test.com and https://demo.org",
            "No URLs here, just text",
            "Mixed content: https://short.com and some text",
        ]
    }

    ds = daft.from_pydict(samples)
    ds = ds.with_column(
        "url_ratio",
        las_udf(
            UrlRatioCalculator,
            construct_args={},
        )(col("text")),
    )

    ds.show()
    # ╭────────────────────────────────┬────────────────────╮
    # │ text                           ┆ url_ratio          │
    # │ ---                            ┆ ---                │
    # │ String                         ┆ Float64            │
    # ╞════════════════════════════════╪════════════════════╡
    # │ Hello world                    ┆ 0                  │
    # ├╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌┼╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌┤
    # │ Check out https://example.com… ┆ 0.4418604651162791 │
    # ├╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌┼╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌┤
    # │ Visit http://test.com and htt… ┆ 0.7380952380952381 │
    # ├╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌┼╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌┤
    # │ No URLs here, just text        ┆ 0                  │
    # ├╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌┼╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌┤
    # │ Mixed content: https://short.… ┆ 0.3695652173913043 │
    # ╰────────────────────────────────┴────────────────────╯
```
