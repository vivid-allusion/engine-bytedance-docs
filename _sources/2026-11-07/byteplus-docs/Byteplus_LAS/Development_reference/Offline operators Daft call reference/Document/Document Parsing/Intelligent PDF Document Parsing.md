---
title: "Intelligent PDF Document Parsing"
product: "Lake AI Service"
product_code: "Byteplus_LAS"
source: "https://docs.byteplus.com/en/docs/Byteplus_LAS/Intelligent_PDF_Document_Parsing"
---

# Operator introduction

## Description

**PDF Intelligent Document Parsing Processor, supporting multi\-dimensional content extraction and structured output**

## Core Features

* High\-precision PDF text extraction

* Output text in markdown format

* Preserve original document structure and format

* Support recognition of tables, images, etc.

* Provide detailed parsing results and TOS storage options

## Performance Notes

* Service QPS is low; it is recommended to set concurrency to 1

* Processing large documents may take a long time

# Daft call

## Operator parameters

## Input

|Input column name |Note |
|---|---|
|data_col |An array containing PDF file URLs or Base64 encoded content |
|file_name_col |An array containing file names for saving in TOS |

## Output

An array of structs containing parsing results.

* parsed_origin_text: Parsed original Markdown text.

* parsed_plain_text: Plain text with image links removed.

* parsed_detail: Detailed parsing information in JSON format.

* parsed_file_path: Storage path of parsing results on TOS.

* parsed_image_filenames: List of image filenames in parsing results.

## Parameters

If a parameter does not have a default value, it is a required parameter.

|Parameter name |Type |Default value |Description |
|---|---|---|---|
|input_type |str | |Input type, supports "url" (file link) or "base64" (Base64 encoded content). Optional values: ["url", "base64"] |
|output_tos_path |str | |TOS directory where parsed content is stored. Parsed content is saved in the txt folder under the specified TOS directory. Meanwhile, images from the PDF are saved in the images folder under the TOS directory, and the TOS paths of the images are used in the saved txt files. If this value is empty, parsed content does not need to be stored in TOS. Default value: "" |
|version |str |v3 |Parsing service version. Optional values: ["v3"] Default value: "v3" |
|file_type |str |pdf |File type. Optional values: ["pdf"] Default value: "pdf" |
|page_start |int |0 |Starting page number for parsing, starting from 0. Default value: 0 |
|page_parsed_num |int |\-1 |Number of pages to parse; \-1 means parse all pages. Default value: \-1 |
|page_batch |int |300 |Number of pages per batch for parsing. Default value: 300 |
|parse_mode |str |auto |Parsing mode. Optional values: ["auto", "fast", "accurate"] Default value: "auto" |
|table_mode |str |markdown |Table parsing mode. Optional values: ["markdown", "html", "excel"] Default value: "markdown" |
|filter_header |str |True |Whether to filter headers and footers. Optional values: ["true", "false"] Default value: "true" |
|timeout |int |120 |Timeout duration in seconds. Default value: 120 |
|qps |int |2 |Request QPS limit. Default value: 2 |
|max_retries |int |3 |Maximum number of retries. Default value: 3 |

## Examples

The following code shows how to use Daft (for distributed processing) to run the operator and parse PDF documents.

```python
# Copyright (c) Beijing Volcano Engine Technology Ltd.

from __future__ import annotations

import os

import daft
from daft import col
from daft.las.functions.doc import PDFParse
from daft.las.functions.udf import las_udf

if __name__ == "__main__":

    # 更改完解析内容会保存到指定的TOS路径下，因此，需要设置好环境变量以保证有权限写入TOS，包括：ACCESS_KEY,SECRET_KEY,TOS_ENDPOINT,TOS_REGION,TOS_TEST_DIR
    TOS_DIR = os.getenv("TOS_TEST_DIR", "tos_bucket")
    output_tos_path = f"tos://{TOS_DIR}/doc/parse/pdf_parse"
    
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

    # 使用环境变量构建URL
    tos_dir_url = os.getenv("TOS_DIR_URL", "las-cn-beijing-public-online.tos-cn-beijing.volces.com")
    samples = {
        "input_url": [
            f"https://{tos_dir_url}/public/shared_doc_dataset/sample.pdf"
        ],
        "filename": ["sample.pdf"],
    }
    df = daft.from_pydict(samples)

    constructor_kwargs = {"input_type": "url", "output_tos_path": output_tos_path, "qps": 1}

    # 使用 Daft 进行分布式处理
    df = df.with_column(
        "parsed_result",
        las_udf(PDFParse, construct_args=constructor_kwargs, concurrency=1)(col("input_url"), col("filename")),
    )
    df = df.with_column("parsed_text", col("parsed_result")["parsed_origin_text"])

    df.show()

    # ╭────────────────────────────────┬────────────┬────────────────────────────────────────────────────────────────────────────────────────────────────────┬────────────────────────────────╮
    # │ input_url                      ┆ filename   ┆ parsed_result                                                                                          ┆ parsed_text                    │
    # │ ---                            ┆ ---        ┆ ---                                                                                                    ┆ ---                            │
    # │ Utf8                           ┆ Utf8       ┆ Struct[parsed_origin_text: Utf8, parsed_plain_text: Utf8, parsed_detail: Utf8, parsed_file_path: Utf8, ┆ Utf8                           │
    # │                                ┆            ┆ parsed_image_filenames: List[Utf8]]                                                                    ┆                                │
    # ╞════════════════════════════════╪════════════╪════════════════════════════════════════════════════════════════════════════════════════════════════════╪════════════════════════════════╡
    # │  https://las-cn-beijing-publi-… ┆ sample.pdf ┆ {parsed_origin_text: ![fig_94…                                                                         ┆ ![fig_94052](https://pdf-buck… │
    # ╰────────────────────────────────┴────────────┴────────────────────────────────────────────────────────────────────────────────────────────────────────┴────────────────────────────────╯
```
