---
title: "Helm deployment overview"
product: " Vital Kubernetes Engine"
product_code: "vke"
source: "https://docs.byteplus.com/en/docs/vke/Overview_of_AI_cloud-native_inference_suite"
---

This topic mainly describes the region information, model information, and documents related to the best practices of inference models for the AI cloud\-native inference suite. The inference models are deployed via **Application center** \> **Application template**.

<span id="wmjJKmoc"></span>
## Supported regions

The regions supported by the AI cloud\-native inference suite are as follows:


* China (Beijing): cn\-beijing

* China (Shanghai): cn\-shanghai

* Asia Pacific (Johor): ap\-southeast\-1


<span id="M6suDosP"></span>
## DeepSeek inference service practice


|Inference service template (Chart name) |Model name |Inference engine |Parallel policy |Quantization |Supported capability |Reference |
|---|---|---|---|---|---|---|
|deepseek\-r1\-sglang |DeepSeek\-R1\-671B |SGLang |Non\-PD disaggregation |\- |* GDKV<br><br>* EIC<br><br>* APMPlus<br><br>* VMP<br><br>* APIG |[Quickly deploying full-version DeepSeek-R1 on SGLang](https://docs.byteplus.com/en/docs/vke/Quickly_deploying_full-version_DeepSeek-R1_on_SGLang) |
|deepseek\-r1\-sglang\-pd |DeepSeek\-R1\-671B |SGLang |* PD disaggregation<br><br>* DP, TP, and EP |\- |* APMPlus<br><br>* VMP<br><br>* APIG |[Quickly deploy the full-version model DeepSeek-R1 based on SGLang (PD disaggregation)](https://docs.byteplus.com/en/docs/vke/Quickly_deploying_the_full-version_model_DeepSeek-R1_based_on_SGLang_PD_disaggregation) |
|deepseek\-v3\-xllm\-pd |DeepSeek\-V3\-671B |xLLM |* PD disaggregation<br><br>* DP, TP, and EP |\- |* VMP<br><br>* APIG |[Quickly deploy the full-version model DeepSeek-V3/R1 based on xLLM (PD disaggregation)](https://docs.byteplus.com/en/docs/vke/Quickly_deploying_the_full-version_model_DeepSeek-V3_R1_based_on_xLLM_PD_disaggregation) |
|deepseek\-r1\-xllm\-pd |DeepSeek\-R1\-671B |xLLM |* PD disaggregation<br><br>* DP, TP, and EP |\- |* VMP<br><br>* APIG |[Quickly deploy the full-version model DeepSeek-V3/R1 based on xLLM (PD disaggregation)](https://docs.byteplus.com/en/docs/vke/Quickly_deploying_the_full-version_model_DeepSeek-V3_R1_based_on_xLLM_PD_disaggregation) |
|deepseek\-r1\-w4afp8\-tensorrt\-llm |DeepSeek\-R1\-W4AFP8 |TensorRT\-LLM |TP and EP |W4A8 |APIG |[Quickly deploy the full-version model DeepSeek-R1 based on the TensorRT-LLM](https://docs.byteplus.com/en/docs/vke/Quickly_deploy_the_quantized_version_of_DeepSeek-R1_based_on_TensorRT-LLM) |
|deepseek\-r1\-0528\-sglang |DeepSeek\-R1\-0528 |SGLang |Non\-PD disaggregation |\- |* GDKV<br><br>* EIC<br><br>* APMPlus<br><br>* VMP<br><br>* APIG |[Quickly deploying the full-version model DeepSeek-R1-0528 based on SGLang](https://docs.byteplus.com/en/docs/vke/Quickly_deploying_the_full-version_model_DeepSeek-R1-0528_based_on_SGLang) |
|deepseek\-r1\-0528\-sglang\-pd |DeepSeek\-R1\-0528\-671B |SGLang |* PD disaggregation<br><br>* DP, TP, and EP |\- |* APMPlus<br><br>* VMP<br><br>* APIG |[Quickly deploying the SGLang-based DeepSeek-R1-0528/V3-0424 full version (with PD disaggregation)](https://docs.byteplus.com/en/docs/vke/Quickly_deploying_the_SGLang-based_DeepSeek-R1-0528_V3-0424_full_version_with_PD_disaggregation) |
|deepseek\-v3\-0324\-sglang\-pd |DeepSeek\-V3\-0324 |SGLang |* PD disaggregation<br><br>* DP, TP, and EP |\- |* APMPlus<br><br>* VMP<br><br>* APIG |[Quickly deploying the SGLang-based DeepSeek-R1-0528/V3-0424 full version (with PD disaggregation)](https://docs.byteplus.com/en/docs/vke/Quickly_deploying_the_SGLang-based_DeepSeek-R1-0528_V3-0424_full_version_with_PD_disaggregation) |
|deepseek\-r1\-w4afp8\-sglang |DeepSeek\-R1\-W4AFP8 |SGLang |TP and EP |\- |* APMPlus<br><br>* VMP<br><br>* APIG |[Quickly deploying SGLang-based DeepSeek-R1 quantitative version](https://docs.byteplus.com/en/docs/vke/Quickly_deploy_the_DeepSeek-R1_Quantitative_version_based_on_SGLang) |
|deepseek\-v3.1\-sglang |DeepSeek\-V3.1 |SGLang |Non\-PD disaggregation |\- |* VMP<br><br>* APIG |[Deploying DeepSeek-V3.1 based on SGLang](https://docs.byteplus.com/en/docs/vke/Quickly_deploying_DeepSeek-V3-1_based_on_SGLang) |


<span id="ojzmbHkt"></span>
## Qwen inference service practices


|Inference service template (Chart name) |Model name |Inference engine |Parallel policy |Quantization |Supported capability |Reference |
|---|---|---|---|---|---|---|
|qwen3\-dynamo\-vllm\-pd |Qwen3\-235B\-A22B |* Dynamo<br><br>* vLLM |PD disaggregation |\- |* GDKV<br><br>* EIC<br><br>* APMPlus<br><br>* VMP<br><br>* APIG |[Quickly deploy Qwen3-235B based on Dynamo and vLLM (PD disaggregation)](https://docs.byteplus.com/en/docs/vke/Quickly_deploying_Qwen3-235B_based_on_Dynamo_and_vLLM_PD_disaggregation) |
|qwen3\-32b\-fp8\-sglang |Qwen3\-32B\-FP8 |SGLang |TP |\- |* APMPlus<br><br>* VMP<br><br>* APIG |[Quickly deploying Qwen3-32B-FP8 based on SGLang](https://docs.byteplus.com/en/docs/vke/Quick_deployment_of_Qwen3-32B-FP8_based_on_SGlang) |
|qwen3\-235b\-a22b\-fp8\-sglang |Qwen3\-235B\-A22B\-FP8 |SGLang |TP |\- |* EIC<br><br>* APMPlus<br><br>* VMP<br><br>* APIG |[Quickly deploying Qwen3-235B-A22B-FP8 based on SGLang](https://docs.byteplus.com/en/docs/vke/Quickly_deploying_Qwen3-235B-A22B-FP8_based_on_SGLang) |
|qwen3\-30b\-a3b\-fp8\-sglang |Qwen3\-30B\-A3B\-FP8 |SGLang |TP |\- |* APMPlus<br><br>* VMP<br><br>* APIG |[Quick deployment of Qwen3-30B-A3B-FP8 based on SGlang](https://docs.byteplus.com/en/docs/vke/Quick_deployment_of_Qwen3-30B-A3B-FP8_based_on_SGlang) |


<span id="1O6DS7vR"></span>
## GPT inference service practices


|Inference service template (Chart name) |Model name |Inference engine |Parallel policy |Quantization |Supported capability |Reference |
|---|---|---|---|---|---|---|
|gpt\-oss\-120b\-vllm |gpt\-oss\-120b |vLLM (open source) |TP |\- |* VMP<br><br>* APIG |[Quickly deploying the gpt-oss-120b inference service based on vLLM](https://docs.byteplus.com/en/docs/vke/Deploying_the_gpt-oss-120b_inference_service) |


<span id="awh73z3l"></span>
## Seed inference service practices


|Inference service template (Chart name) |Model name |Inference engine |Parallel policy |Quantization |Supported capability |Reference |
|---|---|---|---|---|---|---|
|seed\-oss\-36b\-instruct\-vllm |Seed\-OSS\-36B\-Instruct |vLLM (open source) |TP |\- |* VMP<br><br>* APIG |[Deploying Seed-OSS-36B-Instruct based on vLLM](https://docs.byteplus.com/en/docs/vke/Quickly_deploying_Seed-OSS-36B-Instruct_based_on_vLLM) |
