---
title: "Multilingual text translation"
product: "Lake AI Service"
product_code: "Byteplus_LAS"
source: "https://docs.byteplus.com/en/docs/Byteplus_LAS/Multilingual_text_translation"
---

<span id="operator-introduction"></span>
# Operator introduction

<span id="description"></span>
## Description

**Seed\-X Multilingual Text Translation Model \- Core Features of Cross\-Language Text Translation**

<span id="core-features"></span>
## Core Features


* Multilingual Intelligent Translation

   * Supports text conversion between multiple languages; source and target languages can be customized via the source_language and target_language parameters

   * Based on the Seed\-X\-Instruct\-7B/Seed\-X\-PPO\-7B models, delivering high\-quality translation results

   * For supported languages, please refer to: https://huggingface.co/ByteDance\-Seed/Seed\-X\-Instruct\-7B

   * In general scenarios, it is recommended to use the Seed\-X\-PPO\-7B model, which has better translation quality

* Flexible Configuration and Optimization

   * Supports multiple computation precision options (e.g., bfloat16) to adapt to different performance requirements

   * Integrates tensor parallel processing and prefix caching technology to significantly improve inference efficiency

   * Supports automatic or manual device allocation, perfectly adapting to single\-GPU/multi\-GPU environments

* Resource Usage

   * It is recommended to use a GPU with more than 24GB of VRAM


<span id="scenario-optimization"></span>
## Scenario Optimization


* Widely applicable to scenarios such as cross\-language content conversion, multilingual document processing, and international application development

* Built\-in batch processing mechanism to efficiently support parallel translation of large\-scale text data

* Supports precise control over the maximum number of generated tokens to meet diverse business needs


<span id="daft-call"></span>
# Daft call

<span id="operator-parameters"></span>
## Operator parameters

<span id="input"></span>
## Input


|Input column name |Note |
|---|---|
|contents |An array containing texts to be translated, where each element is a string. |


<span id="output"></span>
## Output

A processed array where each element is the translation result of the corresponding text. For texts that fail to process, an empty string is returned.

<span id="parameters"></span>
## Parameters

If a parameter does not have a default value, it is a required parameter.


|Parameter name |Type |Default value |Description |
|---|---|---|---|
|model_path |str |/opt/las/models |Absolute path for storing local model files, default is the preset path inside the container. Modify this path when using a custom model. Default value: "/opt/las/models" |
|model_name |str |Seed\-X\-PPO\-7B |Supported multilingual model name. Currently supports Seed\-X\-Instruct\-7B/Seed\-X\-PPO\-7B series models. Optional values: ["Seed\-X\-Instruct\-7B", "Seed\-X\-PPO\-7B"] Default value: "Seed\-X\-PPO\-7B" |
|dtype |str |bfloat16 |Model inference precision selection Default value: "bfloat16" |
|max_model_len |int |32768 |Maximum sequence length supported by the model Default value:32768 |
|max_num_seqs |int |128 |Maximum number of sequences processed by the model simultaneously Default value:128 |
|tensor_parallel_size |int |1 |Number of devices for tensor parallel computing, used for multi\-GPU parallel inference Default value:1 |
|enable_prefix_caching |bool |True |Whether to enable prefix caching mechanism, which can improve inference efficiency for repeated prefixes Default value:True |
|gpu_memory_utilization |float |0.9 |GPU memory usage ratio, range from 0 to1 Default value:0.9 |
|use_cot |bool |False |Whether to use Chain\-of\-Thought (CoT) mode for translation Default value:False |
|source_language |str |Chinese |Source language name, refer to the model documentation for supported languages Default value:"Chinese" |
|target_language |str |English |Target language name, refer to the model documentation for supported languages Default value:"English" |
|max_tokens |int |1024 |Maximum number of tokens for the model to generate translation results Default value:1024 |
|batch_size |int |4 |Number of text samples processed per inference batch Default value:4 |
|seed |int |42 |Random seed for result reproducibility Default value:42 |


<span id="examples"></span>
## Examples

The following code shows how to use daft to run the operator for multilingual text translation based on the Doubao model.

```python
from __future__ import annotations

import logging
import os

import ray

import daft
from daft import col
from daft.las.functions.text.multilingual_text_translate import MultilingualTextTranslate
from daft.las.functions.udf import las_udf

if __name__ == "__main__":
    os.environ["DAFT_RUNNER"] = "ray"

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
            "这是一篇关于人工智能技术发展的高质量学术论文，内容详实且具有很强的参考价值。",
        ]
    }

    model_path = os.getenv("MODEL_PATH", "/opt/las/models")
    model_name = "Seed-X-PPO-7B"
    max_model_len = 32768
    max_num_seqs = 128
    tensor_parallel_size = 1
    dtype = "bfloat16"
    enable_prefix_caching = True
    gpu_memory_utilization = 0.9
    use_cot = False
    source_language = "Chinese"
    target_language = "English"
    max_tokens = 1024
    batch_size = 4
    seed = 42

    ds = daft.from_pydict(samples)
    ds = ds.with_column(
        "translate_text",
        las_udf(
            MultilingualTextTranslate,
            construct_args={
                "model_path": model_path,
                "model_name": model_name,
                "dtype": dtype,
                "max_model_len": max_model_len,
                "max_num_seqs": max_num_seqs,
                "tensor_parallel_size": tensor_parallel_size,
                "enable_prefix_caching": enable_prefix_caching,
                "gpu_memory_utilization": gpu_memory_utilization,
                "use_cot": use_cot,
                "source_language": source_language,
                "target_language": target_language,
                "max_tokens": max_tokens,
                "batch_size": batch_size,
                "seed": seed,
            },
            num_gpus=1,
            batch_size=1,
            concurrency=1,
        )(col("text")),
    )

    ds.show()

    # ╭─────────────────────────────────────────────────────────────┬────────────────────────────────╮
    # │ text                                                        ┆ translate_text                 │
    # │ ---                                                         ┆ ---                            │
    # │ Utf8                                                        ┆ Utf8                           │
    # ╞═════════════════════════════════════════════════════════════╪════════════════════════════════╡
    # │ 这是一篇关于人工智能技术发展的高质量学术论文，内容详实且具…           ┆ This is a high-quality academ… │
    # ╰─────────────────────────────────────────────────────────────┴────────────────────────────────╯
```
