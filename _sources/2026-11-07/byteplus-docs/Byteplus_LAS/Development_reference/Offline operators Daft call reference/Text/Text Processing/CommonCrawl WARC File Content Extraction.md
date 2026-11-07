---
title: "CommonCrawl WARC File Content Extraction"
product: "Lake AI Service"
product_code: "Byteplus_LAS"
source: "https://docs.byteplus.com/en/docs/Byteplus_LAS/CommonCrawl_WARC_File_Content_Extraction"
---

<span id="operator-introduction"></span>
# Operator introduction

<span id="description"></span>
## Description

**CommonCrawl Web Content Extractor, supporting multiple parsing strategies**

<span id="core-features"></span>
## Core Features:


* Multi\-parser support: trafilatura/justext/goose3

* Supports local and remote WARC files

* Supports binary data and base64 encoding

* Batch processing of WARC files to extract web page content

* Intelligent content extraction, filtering ads and navigation elements


<span id="parser-comparison"></span>
## Parser Comparison:


* **justext**: Fastest speed, low resource usage, relatively strict filtering

* **trafilatura**: Moderate speed, built\-in rules + lightweight NLP model, high extraction quality

* **goose3**: Slower speed, enables multi\-layer logical extraction, mainly for English news


<span id="daft-call"></span>
# Daft call

<span id="operator-parameters"></span>
## Operator parameters

<span id="input"></span>
## Input


|Input column name |Note |
|---|---|
|warc_files |Column containing WARC data, supporting the following formats: \- warc_base64: Base64\-encoded WARC string \- warc_url: WARC file path or TOS link \- warc_binary: Raw WARC binary data |


<span id="output"></span>
## Output

List of extraction results, each element contains the following fields:


* url: Webpage URL

* content: Extracted main content

* warc_file: Source WARC file identifier

* extractor: Name of the extractor used


<span id="parameters"></span>
## Parameters

If a parameter does not have a default value, it is a required parameter.


|Parameter name |Type |Default value |Description |
|---|---|---|---|
|warc_src_type |str | |WARC data source type Supported WARC format types include: \- warc_binary: Raw binary data \- warc_base64: Base64\-encoded data \- warc_url: File path or TOS storage link Optional values: ["warc_binary", "warc_url", "warc_base64"] |
|extractor_type |str |trafilatura |Type of webpage content extractor to use Optional values: ["trafilatura", "justext", "goose3"] Default value: "trafilatura" |
|max_records |int or None | |Limit the number of WARC records to process Default value: None (unlimited) |


<span id="examples"></span>
## Examples

The following code shows how to use daft to run the operator to extract webpage main content from CommonCrawl WARC files, supporting multiple input formats such as file paths, binary data, and base64 encoding.

```python
from __future__ import annotations

import os

import daft
from daft import col
from daft.las.functions.text.commoncrawl_content_extractor import CommonCrawlContentExtractor
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

    tos_dir_url = os.getenv("TOS_DIR_URL", "las-cn-beijing-public-online.tos-cn-beijing.volces.com")
    samples = {"warc_data": [f"https://{tos_dir_url}/public/shared_file_dataset/small-sample.warc.gz"]}

    extractor_type = "trafilatura"
    max_records = 5
    df = daft.from_pydict(samples)
    df = df.with_column(
        "extracted_content",
        las_udf(
            CommonCrawlContentExtractor,
            construct_args={
                "warc_src_type": "warc_url",
                "extractor_type": extractor_type,
                "max_records": max_records,
            },
            num_gpus=0,
            batch_size=1,
            concurrency=1,
        )(col("warc_data")),
    )
    df.show()

    # ╭──────────────────────────────────────────────┬─────────────────────────────────────────────────────────────╮
    # │ warc_files                                   ┆ extracted_content                                           │
    # │ ---                                          ┆ ---                                                         │
    # │ Utf8                                         ┆ List[Struct[url: Utf8, content: Utf8, warc_file: Utf8,      │
    # │                                              ┆ extractor: Utf8]]                                           │
    # ╞══════════════════════════════════════════════╪═════════════════════════════════════════════════════════════╡
    # │ https://las-public-data-qa.tos…              ┆ [{url: http://00852imports.com/detail/5389084.html,         │
    # │                                              ┆ content: 随着互联网的发展，人们对网络速度的要求也越来越高…,         │
    # │                                              ┆ warc_file: sample.warc.gz, extractor: trafilatura},         │
    # │                                              ┆ {url: http://02y3tcpv.gd9.cc/?penglaibexdkcl224396.html,    │
    # │                                              ┆ content: 查看更多相关内容\n\n取消关注在如今的数字时代…,            │
    # │                                              ┆ warc_file: sample.warc.gz, extractor: trafilatura}]         │
    # ╰──────────────────────────────────────────────┴─────────────────────────────────────────────────────────────╯
```
