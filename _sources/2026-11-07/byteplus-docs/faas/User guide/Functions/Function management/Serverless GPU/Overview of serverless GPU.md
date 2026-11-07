---
title: "Overview of serverless GPU"
product: "Function Service"
product_code: "faas"
source: "https://docs.byteplus.com/en/docs/faas/Overview_of_serverless_GPU"
---

<span id="overview"></span>
## Overview

Cloud\-native combined with AI is accelerating the deployment of AI applications. The original AI computing tasks require the consumption of fixed GPU resources, which, due to imbalances among tasks, may lead to some GPUs being idle continuously, incurring high costs of unused resources. To address the above issue, veFaaS has launched the Serverless GPU feature that continues the principle of server\-transparent computing, supporting the deployment of AI applications efficiently and cost\-effectively.

veFaaS provides on\-demand allocated elastic GPU instances to effectively solve the issues of low resource utilization and high cost caused by persistent GPU instances. Users do not need to plan GPU resources in advance, nor worry about GPUs being idle for long periods due to uneven resource usage – they only pay for the actual GPU resources used.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">【<a href="https://docs.byteplus.com/en/docs/faas/How_do_I_apply_for_beta_features"><strong>Beta · apply for trial</strong></a>】 Serverless GPU is currently in beta, if you want to use it, contact your account manager.</div>


<span id="usage-scenarios"></span>
## Usage Scenarios

FaaS currently offers two kinds of instances: CPU and GPU instances. Traditional function uses CPU instances, supporting basic computing scenarios. GPU function uses GPU instances, excels in highly threaded parallel processing tasks (large\-scale computing tasks), suitable for AI model inference, AI model training, accelerating audio/video production, accelerating graphics and imaging scenarios.

<span id="usage-process"></span>
## Usage process

<span>![图片](https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/upload_90a254f7844b6d2af3d12369b05e4228.png) </span>


1. [Create a GPU function](https://docs.byteplus.com/en/docs/faas/GPU_function_management)

   Deploy the function via container images based on GPU instances.

2. [Release function](https://docs.byteplus.com/en/docs/faas/Release_function)

   Release the function and configurations online.

3. [Event triggering](https://docs.byteplus.com/en/docs/faas/Trigger_management)

   Supports configuring triggers to invoke functions via HTTP(S) calls or other event\-triggering methods.

4. [Monitoring and logs](https://docs.byteplus.com/en/docs/faas/Monitoring_and_logs)

   Provides a rich set of monitoring metrics and log observation capabilities to keep track of the function's operational status.


<span id="usage-limit"></span>
## Usage limit


* Each BytePlus account has a limited quota for GPU instances. For details refer to [Limits](https://docs.byteplus.com/en/docs/faas/Limits).

* We currently offer two types of cards: **NVIDIA A10** and **NVIDIA GPU**. The supported card types vary slightly by region, and the actual types are subject to the console.

* Each GPU instance only supports configuring one card.

* GPU instances and CPU instances are independent of each other, and cannot be switched after the function is created.

* The image size limit for GPU instances is 10 GiB.
