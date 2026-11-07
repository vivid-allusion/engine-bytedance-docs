---
title: "Audio Signal-to-Noise Ratio Calculation"
product: "Lake AI Service"
product_code: "Byteplus_LAS"
source: "https://docs.byteplus.com/en/docs/Byteplus_LAS/Audio_Signal-to-Noise_Ratio_Calculation"
---

# Operator introduction

## Description

Audio Signal\-to\-Noise Ratio (SNR) Calculator, which performs signal\-noise separation based on Non\-negative Matrix Factorization (NMF).

## Core Features:

* Perform STFT spectrum analysis on audio;

* Use NMF to decompose the spectrum into signal and noise components;

* Calculate SNR (in dB) based on the energy ratio between the reconstructed time\-domain signal and the estimated noise.

## Format Support:

* Common audio formats: mp3, wav, flac, ogg, aac, m4a

* Supports local paths and object storage paths (tos:// or s3://)

# Daft call

## Operator parameters

## Input

|Input column name |Note |
|---|---|
|audio_paths |Array of audio paths (supports local and object storage paths) \- Local path: absolute or relative path \- Object storage: paths starting with "tos://" or "s3://" |

## Output

Float array (float64), each row is the SNR value (in dB) of the corresponding audio.

## Parameters

If a parameter does not have a default value, it is a required parameter.

|Parameter name |Type |Default value |Description |
|---|---|---|---|
|n_components |int |2 |Number of components for NMF decomposition Default value: 2 (usually the first component is signal, others are noise) |
|max_iter |int |200 |Maximum number of iterations for NMF Default value: 200 |

## Examples

The example code shows how to use Daft to run the operator to calculate the Signal\-to\-Noise Ratio (SNR, in dB) of audio.

```python
from __future__ import annotations

import os

import daft
from daft import col
from daft.las.functions.audio import AudioSNR
from daft.las.functions.udf import las_udf

if __name__ == "__main__":
    if os.getenv("DAFT_RUNNER", "native") == "ray":
        import logging

        import ray

        def configure_logging():
            logging.basicConfig(
                level=logging.INFO,
                format="%(asctime)s - %(name)s - %(levelname)s - %(message)s",
                datefmt="%Y-%m-d %H:%M:%S.%s".format(),
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

    # Provide an audio URL that is reachable from your BytePlus environment.
    audio_url = os.environ["AUDIO_URL"]
    samples = {
        "audio_path": [
            audio_url
        ],
    }

    ds = daft.from_pydict(samples)

    # Use Daft for distributed processing.
    snr_udf = las_udf(
        AudioSNR,
        construct_args={
            "n_components": 2,
            "max_iter": 200,
        },
    )

    ds = ds.with_column("snr_db", snr_udf(col("audio_path")))
    ds.show()
    # ╭──────────────────────────────────────────┬──────────╮
    # │ audio_path                               ┆ snr_db   │
    # │ ---                                      ┆ ---      │
    # │ Utf8                                     ┆ Float64  │
    # ╞══════════════════════════════════════════╪══════════╡
    # │ https://example-audio-url/…               ┆ 12.34    │
    # ╰──────────────────────────────────────────┴──────────╯
```
