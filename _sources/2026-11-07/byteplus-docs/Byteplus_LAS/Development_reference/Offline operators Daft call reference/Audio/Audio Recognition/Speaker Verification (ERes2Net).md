---
title: "Speaker Verification (ERes2Net)"
product: "Lake AI Service"
product_code: "Byteplus_LAS"
source: "https://docs.byteplus.com/en/docs/Byteplus_LAS/Speaker-Verification-ERes2Net"
---

<span id="operator-introduction"></span>
# Operator introduction

<span id="description"></span>
## Description

**AudioSpeakerVerificationEres2net Audio Speaker Verification Processor**

<span id="core-features"></span>
## Core Features


* Speaker verification: Determine if two audio clips belong to the same speaker and output a similarity score

* Multi\-source audio support: Supports multiple audio input types including local files, URLs, object storage, base64, and binary

* Batch processing: Supports efficient verification and exception handling for batch audio pairs


<span id="technical-features"></span>
## Technical Features


* Loads the ERes2Net speaker verification model based on the ModelScope framework

* Supports multi\-GPU inference, with automatic device selection or manual specification

* 16kHz sampling rate audio preprocessing, compatible with various audio formats


<span id="typical-application-scenarios"></span>
## Typical Application Scenarios


* ✅ Voice identity authentication \- Speaker consistency verification

* ✅ Intelligent customer service \- Multi\-channel voice normalization and verification

* ✅ Voice data cleaning \- Automated speaker deduplication


<span id="recommendations"></span>
## Recommendations


* It is recommended to unify the input audio sampling rate to 16kHz to improve verification accuracy

* In multi\-card environments, you can flexibly specify GPU devices via the rank parameter


<span id="daft-call"></span>
# Daft call

<span id="operator-parameters"></span>
## Operator parameters

<span id="input"></span>
## Input


|Input column name |Note |
|---|---|
|speaker_a_audios |Speaker A's audio Supported formats: \- Audio file path (e.g., TOS URL, S3 URL, http(s) URL, local path) \- Audio binary data \- Audio base64 encoding |
|speaker_b_audios |Speaker B's audio Supported formats are the same as above |


<span id="output"></span>
## Output

Speaker similarity score (float) for each pair of audios; None for abnormal samples

<span id="parameters"></span>
## Parameters

If a parameter does not have a default value, it is a required parameter.


|Parameter name |Type |Default value |Description |
|---|---|---|---|
|audio_src_type |str | |Audio format type Supported audio format types include: \- tos/http address (audio_url) \- base64 encoding (audio_base64) \- binary stream (audio_binary) Optional values: ["audio_binary", "audio_url", "audio_base64"] |
|model_path |str |/opt/las/models |Model storage path Default value: "/opt/las/models" |
|model_name |str |iic/speech_eres2net_sv_zh\-cn_16k\-common |Model name Default value: "iic/speech_eres2net_sv_zh\-cn_16k\-common" |
|rank |int or None | |Specify the GPU device ID to use (valid in multi\-card environments) Example: 0 means the first GPU, 1 means the second GPU. Default value: None (automatically select available devices) Default value: None |


<span id="examples"></span>
## Examples

The following code shows how to use daft to run the operator to confirm whether the speakers in two audios are the same person.

```python
from __future__ import annotations

import logging
import os

import ray

import daft
from daft import col
from daft.las.functions.audio.audio_speaker_verification_eres2net import AudioSpeakerVerificationEres2net
from daft.las.functions.udf import las_udf

if __name__ == "__main__":
    if os.getenv("DAFT_RUNNER", "ray") == "ray":

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

        import ray

        ray.init(dashboard_host="0.0.0.0", runtime_env={"worker_process_setup_hook": configure_logging})
        daft.set_runner_ray()

    daft.set_execution_config(actor_udf_ready_timeout=600)
    daft.set_execution_config(min_cpu_per_task=0)

    tos_dir_url = os.getenv("TOS_DIR_URL", "las-cn-beijing-public-online.tos-cn-beijing.volces.com")
    samples = {
        "speaker_a": [f"https://{tos_dir_url}/public/shared_audio_dataset/参观八达岭长城。.wav"],
        "speaker_b": [f"https://{tos_dir_url}/public/shared_audio_dataset/参观八达岭长城。.wav"],
    }

    model_path = os.getenv("MODEL_PATH", "/opt/las/models")
    model_name = "iic/speech_eres2net_sv_zh-cn_16k-common"
    audio_src_type = "audio_url"
    rank = 0

    df = daft.from_pydict(samples)
    df = df.with_column(
        "speaker_verification_result",
        las_udf(
            AudioSpeakerVerificationEres2net,
            construct_args={
                "audio_src_type": audio_src_type,
                "model_path": model_path,
                "model_name": model_name,
                "rank": rank,
            },
            num_gpus=1,
            batch_size=1,
            concurrency=1,
        )(col("speaker_a"), col("speaker_b")),
    )

    df.show()

    # ╭────────────────────────────────┬────────────────────────────────┬─────────────────────────────╮
    # │ speaker_a                      ┆ speaker_b                      ┆ speaker_verification_result │
    # │ ---                            ┆ ---                            ┆ ---                         │
    # │ Utf8                           ┆ Utf8                           ┆ Float32                     │
    # ╞════════════════════════════════╪════════════════════════════════╪═════════════════════════════╡
    # │ tos://las-cn-beijing-public-o… ┆ tos://las-cn-beijing-public-o… ┆ 1                           │
    # ╰────────────────────────────────┴────────────────────────────────┴─────────────────────────────╯
```
