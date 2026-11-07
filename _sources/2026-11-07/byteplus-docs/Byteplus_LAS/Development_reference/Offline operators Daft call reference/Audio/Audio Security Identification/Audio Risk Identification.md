---
title: "Audio Risk Identification"
product: "Lake AI Service"
product_code: "Byteplus_LAS"
source: "https://docs.byteplus.com/en/docs/Byteplus_LAS/Audio_Risk_Identification"
---

<span id="operator-introduction"></span>
# Operator introduction

<span id="description"></span>
## Description

**Audio content risk identification processor, supporting multi\-format audio security detection**

<span id="core-features"></span>
## Core Features:


* Supports multiple audio formats (mp3, m4a, wav, wma, amr, aac, ogg)

* Supports large files (duration ≤5 hours, ≤512MB)

* Three\-level risk determination:

   * BLOCK: Unsafe sample

   * PASS: Safe sample

   * REVIEW: Manual review recommended

* Supports custom business scenario configuration

* Provides detailed detection result output


<span id="performance-description"></span>
## Performance Description:


* Supports batch processing; it is recommended to configure concurrency based on service QPS

* Asynchronous interface; automatically polls to get detection results


<span id="daft-call"></span>
# Daft call

<span id="operator-parameters"></span>
## Operator parameters

<span id="input"></span>
## Input


|Input column name |Note |
|---|---|
|audio_id_col |Input column for unique audio identifier |
|audio_url_col |Column containing audio content, supports directly accessible URLs |
|audio_title_col |(Optional) Audio title column |
|account_id_col |(Optional) Column for the ID of the audio sender |
|operate_time_col |(Optional) Column for the second\-level timestamp when the user sent the audio |


<span id="output"></span>
## Output

A struct containing risk identification results


* Decision: Judgment result (PASS, BLOCK, REVIEW)

* Message: Server return message

* risk_result: Complete JSON format detection result


<span id="parameters"></span>
## Parameters

If a parameter does not have a default value, it is a required parameter.


|Parameter name |Type |Default value |Description |
|---|---|---|---|
|app_id |int | |Application ID activated in the business risk identification product |
|biztype |str | |Audio risk identification scenario configured in the business risk identification product |
|result_type |int |0 |Slice content type 0 means only return non\-compliant audio slices 1 means return all slice detection results Optional values: [0, 1] |
|timeout |int |120 |Timeout setting in seconds Sets the timeout from sending the request to receiving the result. For offline tasks, increase appropriately to prevent data processing blocking |
|poll_interval |int |10 |Polling interval in seconds Interval for calling the active query interface; set based on QPS and performance requirements of the active query interface |
|num_coroutines |int |5 | |


<span id="examples"></span>
## Examples

The following code shows how to use Daft (suitable for distributed environments) to run the operator for audio content risk identification.

```python
from __future__ import annotations

import os

import daft
from daft import col
from daft.las.functions.audio import AudioRiskRec
from daft.las.functions.udf import las_udf

if __name__ == "__main__":

    """
    算子使用前置条件：开通业务风险识别产品-音频风险识别-音频点播服务，产品链接见：https://www.volcengine.com/product/business-security
    app_id: 在业务风险识别产品中开通的应用ID
    biztype: 在业务风险识别产品中配置的音频风险识别场景
    本示例代码中使用模拟值
    """
    
    # 注意：AudioRiskRec需要app_id和biztype参数，这里使用示例值
    
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
        "audio_id": ["1"],
        "audio_path": [
            f"https://{tos_dir_url}/public/shared_audio_dataset/sample.mp3"
        ],
    }
    df = daft.from_pydict(samples)

    # 实际使用时需要替换为有效的app_id和biztype
    constructor_kwargs = {"app_id": 123456, "biztype": "test_biztype"}

    # 使用 Daft 进行分布式处理
    df = df.with_column(
        "parsed_result",
        las_udf(AudioRiskRec, construct_args=constructor_kwargs, concurrency=1)(col("audio_id"), col("audio_path")),
    )
    df = df.with_column("Decision", col("parsed_result")["Decision"])
    df = df.with_column("Message", col("parsed_result")["Message"])
    df = df.with_column("risk_result", col("parsed_result")["risk_result"])

    df.select("audio_id", "audio_path", "Decision", "Message").show()
    # ╭──────────┬────────────────────────────────┬──────────┬─────────╮
    # │ audio_id ┆ audio_path                     ┆ Decision ┆ Message │
    # │ ---      ┆ ---                            ┆ ---      ┆ ---     │
    # │ Utf8     ┆ Utf8                           ┆ Utf8     ┆ Utf8    │
    # ╞══════════╪════════════════════════════════╪══════════╪═════════╡
    # │ 1        ┆ https://las-cn-beijing-publi-… ┆ PASS     ┆ success │
    # ╰──────────┴────────────────────────────────┴──────────┴─────────╯
```
