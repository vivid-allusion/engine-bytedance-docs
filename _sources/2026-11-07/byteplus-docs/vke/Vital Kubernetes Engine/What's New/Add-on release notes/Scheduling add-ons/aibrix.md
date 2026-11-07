---
title: "aibrix"
product: " Vital Kubernetes Engine"
product_code: "vke"
source: "https://docs.byteplus.com/en/docs/vke/aibrix"
---

As a part of a solution suite for generative artificial intelligence (GenAI) inference infrastructure, the aibrix add\-on provides the GPU workload autoscaling capability. This topic describes the change history of the aibrix add\-on.

For more information about the add\-on and how to use it, see [aibrix](https://docs.byteplus.com/en/docs/vke/aibrix-add-on?lang=en).

## September 2026

|Version |Kubernetes version compatibility |Version status |Description |Impact |
|---|---|---|---|---|
|v0.5.0\-vke.3 |Cluster version ≥ v1.26 |Being maintained |PodGroup\-level re\-creation policies are supported. |None |

## April 2026

|Version |Kubernetes version compatibility |Version status |Description |Impact |
|---|---|---|---|---|
|v0.5.0\-vke.2 |All versions |Being maintained |Supported autoscaling based on the metrics of the inference engine. |None |

## December 2025

|Version |Kubernetes version compatibility |Version status |Description |Impact |
|---|---|---|---|---|
|v0.5.0\-vke.1 |All versions |Being maintained |Upgraded to community AIBrix v0.5.0 and supported independent scaling of Prefill and Decode roles. |None |

## September 2025

|Version |Kubernetes version compatibility |Version status |Description |Impact |
|---|---|---|---|---|
|v0.4.1\-vke.2 |All versions |Being maintained |Fixed the issue that StormService couldn't automatically recreate the pods it created after they were manually deleted. |None |
|v0.4.1\-vke.1 |All versions |Being maintained |The aibrix add\-on is officially released for the first time. |None |
