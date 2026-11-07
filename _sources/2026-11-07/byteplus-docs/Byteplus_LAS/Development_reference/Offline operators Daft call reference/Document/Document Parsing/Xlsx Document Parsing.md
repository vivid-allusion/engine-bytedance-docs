---
title: "Xlsx Document Parsing"
product: "Lake AI Service"
product_code: "Byteplus_LAS"
source: "https://docs.byteplus.com/en/docs/Byteplus_LAS/Xlsx_Document_Parsing"
---

<span id="operator-introduction"></span>
# Operator introduction

<span id="description"></span>
## Description

**Excel spreadsheet parsing processor that supports multi\-format output and structured data extraction**

<span id="core-features"></span>
## Core Features:


* Supports xlsx/xls format parsing

* Outputs markdown or html format

* Preserves table structure and data relationships

* Supports multi\-sheet processing

* Provides TOS storage option


<span id="format-support"></span>
## Format Support:


* Microsoft Excel (.xlsx, .xls)

* It is recommended to use xlsx format for optimal parsing results


<span id="daft-call"></span>
# Daft call

<span id="operator-parameters"></span>
## Operator parameters

<span id="input"></span>
## Input


|Input column name |Note |
|---|---|
|xlsx_col |Column containing paths to xlsx/xls files |


<span id="output"></span>
## Output

Array of structs, fields include


* data_item_uri: Original file path

* text: Merged markdown/html text

* text_by_table: List of markdown/html texts for each sheet


<span id="parameters"></span>
## Parameters

If a parameter does not have a default value, it is a required parameter.


|Parameter name |Type |Default value |Description |
|---|---|---|---|
|if_save_md_content |bool |True |Whether to save in markdown format, default True |
|if_save_html_content |bool |False |Whether to save in html format, default False If both are True, only markdown is saved |
|output_tos_path |str | |TOS directory to store parsed content; if empty, do not upload |


<span id="examples"></span>
## Examples

The following code shows how to use pandas (for standalone) and ray (for distributed) to run the operator to parse xlsx documents.

```python
from __future__ import annotations

import os

import daft
from daft import col
from daft.las.functions.doc import XlsxParse
from daft.las.functions.udf import las_udf

if __name__ == "__main__":

    # 更改完解析内容会保存到指定的TOS路径下，因此，需要设置好环境变量以保证有权限写入TOS，包括：ACCESS_KEY,SECRET_KEY,TOS_ENDPOINT,TOS_REGION,TOS_TEST_DIR
    TOS_DIR = os.getenv("TOS_TEST_DIR", "tos_bucket")
    output_tos_path = f"tos://{TOS_DIR}/doc/parse/xlsx_parse"
    
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

    # 使用绝对URL，去掉环境变量依赖
    tos_dir_url = os.getenv("TOS_DIR_URL", "las-cn-beijing-public-online.tos-cn-beijing.volces.com")
    samples = {
        "xlsx_path": [
            f"https://{tos_dir_url}/public/shared_doc_dataset/sample.xlsx"
        ],
    }
    df = daft.from_pydict(samples)

    constructor_kwargs = {
        "if_save_md_content": True,
        "if_save_html_content": False,
        "output_tos_path": output_tos_path,
    }

    # 使用 Daft 进行分布式处理
    df = df.with_column(
        "result",
        las_udf(XlsxParse, construct_args=constructor_kwargs, concurrency=1)(col("xlsx_path")),
    )
    df = df.with_column("data_item_uri", col("result")["data_item_uri"])
    df = df.with_column("text", col("result")["text"])
    df = df.with_column("text_by_table", col("result")["text_by_table"])

    df.show()
    # ╭────────────────────────────────┬────────────────────────────────────────────────────────────────────┬────────────────────────────────┬────────────────────────────────────────┬────────────────────────────────────────╮
    # │ xlsx_path                      ┆ result                                                             ┆ data_item_uri                  ┆ text                                   ┆ text_by_table                          │
    # │ ---                            ┆ ---                                                                ┆ ---                            ┆ ---                                    ┆ ---                                    │
    # │ Utf8                           ┆ Struct[data_item_uri: Utf8, text: Utf8, text_by_table: List[Utf8]] ┆ Utf8                           ┆ Utf8                                   ┆ List[Utf8]                             │
    # ╞════════════════════════════════╪════════════════════════════════════════════════════════════════════╪════════════════════════════════╪════════════════════════════════════════╪════════════════════════════════════════╡
    # │ https://las-cn-beijing-publi-… ┆ {data_item_uri: tos://tos_bucket/doc/parse/xlsx_parse/sample.md, … ┆ tos://tos_bucket/doc/parse/xls ┆ |   产品ID | 产品名称   |   价格 |   …    ┆ [|   产品ID | 产品名称   |   价格 |  …    │
    # ╰────────────────────────────────┴────────────────────────────────────────────────────────────────────┴────────────────────────────────┴────────────────────────────────────────┴────────────────────────────────────────╯
```
