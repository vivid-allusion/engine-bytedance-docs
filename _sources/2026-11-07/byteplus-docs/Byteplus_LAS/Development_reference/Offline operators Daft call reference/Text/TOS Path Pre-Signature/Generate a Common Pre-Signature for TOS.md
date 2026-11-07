---
title: "Generate a Common Pre-Signature for TOS"
product: "Lake AI Service"
product_code: "Byteplus_LAS"
source: "https://docs.byteplus.com/en/docs/Byteplus_LAS/Generate_a_Common_Pre-Signature_for_TOS"
---

<span id="operator-introduction"></span>
# Operator introduction

<span id="description"></span>
## Description

<span id="core-features"></span>
## Core Features


* Signature Generation Mechanism: Generate time\-limited pre\-signed URLs based on the Volcengine TOS SDK.

* URL Schema Handling:

   * Natively supports signature conversion for paths using tos/s3 protocols.

   * Automatically skips paths containing http/https protocols.

* Security Controls:

   * Configurable signature validity period (default: 3600 seconds).


<span id="input-output-specifications"></span>
## Input/Output Specifications


* Input Format:

   * TOS Path: string type, supports the following formats:

* tos://{bucket}/

* s3://{bucket}/

* Output Format:

   * Valid Signed URL: https protocol string

   * Exception Cases: returns None


<span id="configuration-parameter-description"></span>
## Configuration Parameter Description


* expires: Controls the signature validity period (unit: seconds). Too short may cause service interruptions; too long poses security risks.


<span id="daft-call"></span>
# Daft call

<span id="operator-parameters"></span>
## Operator parameters

<span id="input"></span>
## Input


|Input column name |Note |
|---|---|
|urls |Input TOS file path |


<span id="output"></span>
## Output

Generated signed URL

<span id="parameters"></span>
## Parameters

If a parameter does not have a default value, it is a required parameter.


|Parameter name |Type |Default value |Description |
|---|---|---|---|
|expires |int |3600 |Expiration time of the signed URL in seconds. Default value is 3600 |


<span id="examples"></span>
## Examples

The following code shows how to use daft to run the operator and generate a normal pre\-signed URL for TOS.

```python
from __future__ import annotations

import os

import daft
from daft import col
from daft.las.functions.text.pre_sign_url_for_tos import PreSignUrlForTos
from daft.las.functions.udf import las_udf

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

if __name__ == "__main__":
    # 样例数据
    TOS_TEST_DIR = os.getenv("TOS_TEST_DIR", "tos_bucket")
    samples = {"url": [f"tos://{TOS_TEST_DIR}/sample.mp4"]}

    # 使用提供的算子生成签名URL
    ds = daft.from_pydict(samples)
    ds = ds.with_column(
        "signed_url",
        las_udf(
            PreSignUrlForTos,
            construct_args={
                "expires": 3600,
            },
        )(col("url")),
    )

    ds.show()
    # 输出内容，以实际情况为准
    # ╭─────────────────────────────┬────────────────────────────────╮
    # │ url                         ┆ signed_url                     │
    # │ ---                         ┆ ---                            │
    # │ Utf8                        ┆ Utf8                           │
    # ╞═════════════════════════════╪════════════════════════════════╡
    # │ tos://tos_bucket/sample.mp4 ┆ https://tos_bucket.tos-cn-bei… │
    # ╰─────────────────────────────┴────────────────────────────────╯
```
