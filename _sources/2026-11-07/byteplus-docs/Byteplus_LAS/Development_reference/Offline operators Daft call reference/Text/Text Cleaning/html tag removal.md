---
title: "html tag removal"
product: "Lake AI Service"
product_code: "Byteplus_LAS"
source: "https://docs.byteplus.com/en/docs/Byteplus_LAS/html_tag_removal"
---

<span id="operator-introduction"></span>
# Operator introduction

<span id="description"></span>
## Description

**HTML Document Purification Processor \- Multi\-structure Parsing and Intelligent Cleaning Solution**

<span id="core-features"></span>
## Core Features


* **Multi\-structure Parsing**

   * Title Extraction: Automatically recognize `<h1>`\-`<h6>` tags

   * Main Text Extraction: Intelligently identify the main content of the article

   * Redundancy Filtering: Remove non\-text tags such as `<script>`/`<style>`

* **Intelligent Processing**

   * Fault Tolerance Mechanism: Support parsing of incomplete HTML fragments

   * Format Preservation: Maintain text paragraph structure and line break logic


<span id="technical-implementation"></span>
## Technical Implementation


* Basic Library: `BeautifulSoup4` (html.parser)


<span id="daft-call"></span>
# Daft call

<span id="operator-parameters"></span>
## Operator parameters

<span id="input"></span>
## Input


|Input column name |Note |
|---|---|
|texts |An array of texts containing HTML content, with elements of type string |


<span id="output"></span>
## Output

An array of cleaned texts, with elements of type string

<span id="parameters"></span>
## Parameters

If a parameter does not have a default value, it is a required parameter.


|Parameter name |Type |Default value |Description |
|---|---|---|---|
|separator |str | | |
|strip |bool |True | |


<span id="examples"></span>
## Examples

The following code shows how to use daft to run the operator to remove HTML tags.

```python
from __future__ import annotations

import os

import daft
from daft import col
from daft.las.functions.text.clean_html_tag import CleanHtmlTag
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
            """<!-- 这是 HTML 注释，不会在浏览器中显示 -->
    <!DOCTYPE html>
    <html>
    <head>
        <!-- 引入外部 CSS -->
        <link rel="stylesheet" href="styles.css">
    </head>
    <body>
        <!--
            多行注释示例：
            保持代码缩进一致（如 2/4 空格）。
            标签属性使用双引号。
        -->
        <div class="content" id="main-content">
            <p class="text">Hello World!</p>
        </div>
    </body>
    </html>""",
            None,
        ]
    }

    separator = "\n"
    strip = True
    ds = daft.from_pydict(samples)

    ds = ds.with_column(
        "cleaned_text",
        las_udf(
            CleanHtmlTag,
            construct_args={"separator": separator, "strip": strip},
        )(col("text")),
    )
    ds.show()

    # ╭──────────────────────────────────────────────┬──────────────╮
    # │ text                                         ┆ cleaned_text │
    # │ ---                                          ┆ ---          │
    # │ Utf8                                         ┆ Utf8         │
    # ╞══════════════════════════════════════════════╪══════════════╡
    # │ <!-- 这是 HTML 注释，不会在浏览器中显示 -->…      ┆ Hello World! │
    # ├╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌┼╌╌╌╌╌╌╌╌╌╌╌╌╌╌┤
    # │ None                                         ┆ None         │
    # ╰──────────────────────────────────────────────┴──────────────╯
```
