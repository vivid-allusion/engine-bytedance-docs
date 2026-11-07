---
title: "Audio Quality Score (DNSMOS)"
product: "Lake AI Service"
product_code: "Byteplus_LAS"
source: "https://docs.byteplus.com/en/docs/Byteplus_LAS/AudioQualityScore-DNSMOS"
---

<span id="operator-introduction"></span>
# Operator introduction

<span id="description"></span>
## Description

**Audio Quality Scoring Module \- Evaluate Audio Quality Using DNSMOS Model**

<span id="core-features"></span>
## Core Features


* Evaluate audio quality using the DNSMOS (Deep Noise Suppression Mean Opinion Score) model

* Provide scores in three dimensions: Overall Quality (OVRL), Signal Quality (SIG), and Background Noise (BAK)

* Scores range from 1 to 5, with higher scores indicating better audio quality

* Support automatic sample rate conversion and audio preprocessing

* Applicable to scenarios such as speech quality evaluation, audio filtering, and quality control


<span id="score-dimension-explanations"></span>
## Score Dimension Explanations


* OVRL (Overall): Overall audio quality score, comprehensively evaluating the listenability of the audio

* SIG (Signal): Signal quality score, evaluating the clarity and naturalness of the speech signal

* BAK (Background): Background noise score, evaluating the degree of interference from background noise


<span id="daft-call"></span>
# Daft call

<span id="operator-parameters"></span>
## Operator parameters

<span id="input"></span>
## Input


|Input column name |Note |
|---|---|
|audio_col |An array containing audio binary data (pa.binary type), each element should be a complete audio segment. |


<span id="output"></span>
## Output

A structured result array where each element contains the following fields:


* ovrl (float): Overall audio quality score, comprehensively evaluating the audibility of the audio, ranging from 1.0 to 5.0.

* sig (float): Signal quality score, evaluating the clarity and naturalness of the speech signal, ranging from 1.0 to 5.0.

* bak (float): Background noise score, evaluating the interference level of background noise, ranging from 1.0 to 5.0.


Audio that fails to process returns a structure containing null values.

<span id="parameters"></span>
## Parameters

If a parameter does not have a default value, it is a required parameter.


|Parameter name |Type |Default value |Description |
|---|---|---|---|
|model_path |str |/opt/las/models | |
|device |str |cpu | |
|is_personalized_mos |bool |False | |


<span id="examples"></span>
## Examples

The following code shows how to use daft to run the operator for audio quality scoring.

```python
from __future__ import annotations

import os

import daft
from daft import col
from daft.las.functions.audio import AudioQualityScore
from daft.las.functions.udf import las_udf

if __name__ == "__main__":
    TOS_TEST_DIR_URL = os.getenv("TOS_TEST_DIR_URL", "las-cn-beijing-public-online.tos-cn-beijing.volces.com")
    model_path = os.getenv("MODEL_PATH", "/opt/las/models")

    if os.getenv("DAFT_RUNNER", "native") == "ray":
        import logging

        import ray

        def configure_logging():
            logging.basicConfig(
                level=logging.INFO,
                format="%(asctime)s - %(name)s - %(levelname)s - %(message)s",
                datefmt="%Y-%m-%d %H:%M:%S",
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

    samples = {"audio_path": [f"https://{TOS_TEST_DIR_URL}/public/archive/audio_quality_score/test_audio.wav"]}
    df = daft.from_pydict(samples)
    df = df.with_column(
        "audio_quality_score",
        las_udf(
            AudioQualityScore,
            construct_args={"model_path": model_path, "device": "cuda"},
            num_gpus=1,
            batch_size=8,
            concurrency=1,
        )(col("audio_path")),
    )

    df.show()
    # ╭────────────────────────────────┬───────────────────────────────────────────────────╮
    # │ audio_path                     ┆ audio_quality_score                               │
    # │ ---                            ┆ ---                                               │
    # │ String                         ┆ Struct[ovrl: Float64, sig: Float64, bak: Float64] │
    # ╞════════════════════════════════╪═══════════════════════════════════════════════════╡
    # │ https://las-public-data-qa.to… ┆ {ovrl: 1.7469981067293439,                        │
    # │                                ┆ si…                                               │
    # ╰────────────────────────────────┴───────────────────────────────────────────────────╯
```
