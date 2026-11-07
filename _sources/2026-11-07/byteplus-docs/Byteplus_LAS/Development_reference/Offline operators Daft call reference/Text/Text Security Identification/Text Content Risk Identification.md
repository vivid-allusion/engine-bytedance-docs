---
title: "Text Content Risk Identification"
product: "Lake AI Service"
product_code: "Byteplus_LAS"
source: "https://docs.byteplus.com/en/docs/Byteplus_LAS/Text_Content_Risk_Identification"
---

<span id="operator-introduction"></span>
# Operator introduction

<span id="description"></span>
## Description

**Text content risk identification processor, supporting multi\-dimensional security detection**

<span id="core-features"></span>
## Core Features:


* Multi\-risk type detection

* Three\-level risk judgment:

   * BLOCK: Unsafe sample

   * PASS: Safe sample

   * REVIEW: Recommend manual review

* Support custom business scenario configuration

* Provide detailed detection result output


<span id="performance-description"></span>
## Performance Description:


* Support batch processing; it is recommended to configure concurrency based on service QPS


<span id="daft-call"></span>
# Daft call

<span id="operator-parameters"></span>
## Operator parameters

<span id="input"></span>
## Input


|Input column name |Note |
|---|---|
|text_col |Input text column |
|account_id_col |(Optional) Column for the ID of the text sender |
|operate_time_col |(Optional) Column for the second\-level timestamp when the user sent the text |
|nick_name_col |(Optional) Column for the nickname of the text sender |
|signature_col |(Optional) Column for the user's personal signature |
|text_type_col |(Optional) Column for the type of text content (e.g., "prompt", "response") |
|session_id_col |(Optional) Column for the conversation round ID in AIGC dialogue scenarios |


<span id="output"></span>
## Output

An array of structs containing risk identification results


* FinalLabel: Final risk label

* Decision: Judgment result (PASS, BLOCK, REVIEW)

* Message: Server return message

* risk_result: Complete detection result in JSON format


<span id="parameters"></span>
## Parameters

If a parameter does not have a default value, it is a required parameter.


|Parameter name |Type |Default value |Description |
|---|---|---|---|
|app_id |int | |Application ID activated in the Business Risk Identification Product |
|biztype |str | |Scenario configured in the Business Risk Identification Product |
|timeout |int |120 |Timeout setting in seconds. Sets the timeout from sending the request to receiving the result. For offline tasks, you can increase this value appropriately to prevent data processing blockages. |


<span id="examples"></span>
## Examples

The code below demonstrates how to use Daft (suitable for distributed processing) to run the operator for text content risk identification.

```python
from __future__ import annotations

import os

import daft
from daft import col
from daft.las.functions.text import ContentRiskRec
from daft.las.functions.udf import las_udf

if __name__ == "__main__":

    """
    算子使用前置条件：开通业务风险识别产品-文本风险识别，产品链接见：https://www.volcengine.com/product/business-security
    app_id: 在业务风险识别产品中开通的应用ID
    biztype: 在业务风险识别产品中配置的场景
    本示例代码中使用模拟值
    """

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
        "id": [1, 2],
        "text": [
            "今天天气真好，我们一起去公园玩吧！",
            "出售枪支，联系电话123456789",
        ],
        "account_id": ["user1", "user2"],
        "nickname": ["用户1", "用户2"],
    }
    df = daft.from_pydict(samples)

    # 实际使用时需要替换为有效的app_id和biztype
    constructor_kwargs = {"app_id": 123456, "biztype": "test_biztype"}

    # 使用 Daft 进行分布式处理
    df = df.with_column(
        "parsed_result",
        las_udf(ContentRiskRec, construct_args=constructor_kwargs, concurrency=1)(
            col("text"), account_id_col=col("account_id"), nick_name_col=col("nickname")
        ),
    )
    df = df.with_column("FinalLabel", col("parsed_result")["FinalLabel"])
    df = df.with_column("Decision", col("parsed_result")["Decision"])

    df.select("text", "account_id", "nickname", "FinalLabel", "Decision").show()

    # ╭─────────────────────────────────────┬────────────┬──────────┬────────────┬──────────╮
    # │ text                                ┆ account_id ┆ nickname ┆ FinalLabel ┆ Decision │
    # │ ---                                 ┆ ---        ┆ ---      ┆ ---        ┆ ---      │
    # │ Utf8                                ┆ Utf8       ┆ Utf8     ┆ Utf8       ┆ Utf8     │
    # ╞═════════════════════════════════════╪════════════╪══════════╪════════════╪══════════╡
    # │ 今天天气真好，我们一起去公园玩吧！…       ┆ user1      ┆ 用户1    ┆            ┆ PASS     │
    # ├╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌╌┼╌╌╌╌╌╌╌╌╌╌╌╌┼╌╌╌╌╌╌╌╌╌╌┼╌╌╌╌╌╌╌╌╌╌╌╌┼╌╌╌╌╌╌╌╌╌╌┤
    # │ 出售枪支，联系电话123456789…           ┆ user2      ┆ 用户2     ┆ 106        ┆ BLOCK    │
    # ╰─────────────────────────────────────┴────────────┴──────────┴────────────┴──────────╯
```
