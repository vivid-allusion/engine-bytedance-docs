---
title: "ServingKit overview"
product: " Vital Kubernetes Engine"
product_code: "vke"
source: "https://docs.byteplus.com/en/docs/vke/Servingkit_overview"
---

The AI cloud\-native inference suite (ServingKit), built on ByteDance's large\-scale AI practices, enables enterprises to run mainstream inference models efficiently, stably, and cost\-effectively on large\-scale GPU clusters.

<span id="Ood23q5v"></span>
## Introduction

ServingKit integrates large\-scale ByteDance AI practices with the extensive operational experience of Volcano Ark and provides four core capabilities: container orchestration, AI gateways, end\-to\-end observability, and distributed caching. It empowers enterprises to achieve efficient, stable, and cost\-effective operation of mainstream inference models on large\-scale GPU clusters, covering diverse inference scenarios such as text\-to\-text, text\-to\-image, and image\-to\-video generation.

<span id="joPPSeny"></span>
## Advantages


* **Compatibility with abundant inference frameworks:**  ServingKit is deeply adapted for mainstream inference engines and frameworks such as vLLM, SGLang, and Dynamo. It supports the prefill\-decode (PD) disaggregation architecture to boost inference efficiency. It addresses the issues of insufficient computing power, high costs, and low utilization for user\-managed ComfyUI, helping users use computing power at low costs.

* **Rapid model startup:**  Leveraging the P2P technology and model loading tools, ServingKit achieves the deployment of the full DeepSeek\-R1\-671B model on 100 GPUs within minutes, which considerably reduces the model deployment duration.

* **Higher inference performance:**  ServingKit provides performance optimization methods such as the operator\-level optimization method for mainstream inference engines and GPUs. It increases the inference throughput of the DeepSeek\-R1 model to 100 to 300% of its original level in text generation scenarios, and reduces end\-to\-end latency by 99% in video generation scenarios.

* **Full\-chain observability for inference:**  ServingKit provides end\-to\-end transparent instrumentation for inference, which covers the full metrics of AI inference engines, and achieves accurate troubleshooting during inference within minutes.


<span id="gbZqhB2i"></span>
## Terms

<span id="FRfrxPHf"></span>
### PD disaggregation and PD co\-location


* **PD disaggregation:**  The PD disaggregation architecture divides the inference process into the following two phases, which are deployed in different hardware resources to improve resource utilization and inference performance.

   * Prefill: compute\-intensive phase

   * Decode: video memory\-intensive phase

* **PD co\-location:**  This is the non\-PD disaggregation architecture, where the prefill and decode phases are deployed on the same group of GPUs, with the prefill and decode service clusters not being distinguished.


<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_b07e15f2bf67b2ea0de3a2b5f309ec26.png) </span>

<span id="ZD4RdmCG"></span>
### Oniond model loading acceleration

Oniond is a model downloader that enables rapid model distribution without requiring an API access key (AK and SK).

<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_69bd6ed91a95fdaa80e694fd3532e4d4.png) </span>

<span id="7H7gF9CV"></span>
### BytePlus Enhanced Edition of the ComfyUI add\-on

As a mainstream open source tool in the Artificial Intelligence Generative Component (AIGC) field, ComfyUI integrates with the ServingKit add\-on to provide inference acceleration capabilities, such as parallel inference, quantization, and caching, for mainstream models such as FLUX.1, FLUX\-kontext, and Wan2.2. These capabilities are delivered without affecting the native use of the tool, which reduces the image generation time by over 50% and the total video generation time by 99%.

<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_661c4374344df8749e8ce8446ab87881.png) </span>

<span id="obHV9sLB"></span>
### Openvefuser add\-on

Developed by BytePlus, the Openvefuser add\-on is seamlessly integrated with the ComfyUI service. It provides optimization technologies for large models, including compilation, operators, caching, quantization, parallelism, offloading, and distillation.

<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_eec542d552e7bc15ac3a29eeb830dfe8.png) </span>

<span id="xWiAPVOt"></span>
### KV Cache

KV Cache is a caching mechanism for storing and quickly retrieving key\-value pair data, which is commonly used in large language model (LLM) inference scenarios. ServingKit provides a high\-performance distributed KV Cache service for AI inference applications by using Elastic Instant Cache (EIC).
