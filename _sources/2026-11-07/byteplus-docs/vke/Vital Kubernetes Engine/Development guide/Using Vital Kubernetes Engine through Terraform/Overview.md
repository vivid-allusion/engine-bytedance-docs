---
title: "Overview"
product: " Vital Kubernetes Engine"
product_code: "vke"
source: "https://docs.byteplus.com/en/docs/vke/Overview-of-using-VKE-through-Terraform"
---

This topic describes how to utilize VKE features by using Terraform.

<span id=".dGVycmFmb3JtLeS7i-e7jQ=="></span>
## Introduction to Terraform

Terraform is an open\-source infrastructure automation and orchestration tool designed to efficiently configure and manage cloud infrastructure resources. BytePlus provides developer tools based on open\-source Terraform that you can use to securely and efficiently preview, configure, and manage cloud infrastructure and resources. For more information, see [Terraform](https://www.volcengine.com/docs/6706/101976).

<span id=".dGVycmFmb3JtLeS8mOWKvw=="></span>
## Terraform advantages


* Infrastructure as code

   By using advanced configuration syntax for resource description, infrastructure can be codified. By controlling the resource versions defined in Terraform, cloud resources are controllable, manageable, and traceable.

* Automated infrastructure management

   Terraform configuration templates support configuration planning and automatic execution, while maintaining the state of infrastructure resources. This eliminates the tediousness and errors of manual operations.

* Lower handover costs

   Using Terraform facilitates the handoff of operation and maintenance (O&M) tasks, reducing issues such as information gaps and cloud resource waste caused by inefficient handovers.


<span id=".6YCa6L-HLXRlcnJhZm9ybS3nrqHnkIblrrnlmajmnI3liqHotYTmupA="></span>
## Managing VKE resources with Terraform

VKE supports managing the following resources and data sources through Terraform.


* Resources:

   
   |Item |Description |
   |---|---|
   |[byteplus_vke_cluster](https://registry.terraform.io/providers/byteplus-sdk/byteplus/latest/docs/resources/vke_cluster) |Manage clusters. |
   |[byteplus_vke_node_pool](https://registry.terraform.io/providers/byteplus-sdk/byteplus/latest/docs/resources/vke_node_pool) |Manage custom node pools. |
   |[byteplus_vke_default_node_pool](https://registry.terraform.io/providers/byteplus-sdk/byteplus/latest/docs/resources/vke_default_node_pool) |Manage the default node pool (vke\-default\-nodepool). |
   |[byteplus_vke_node](https://registry.terraform.io/providers/byteplus-sdk/byteplus/latest/docs/resources/vke_node) |Manage nodes. |
   |[byteplus_vke_addon](https://registry.terraform.io/providers/byteplus-sdk/byteplus/latest/docs/resources/vke_addon) |Manage add\-ons. |
   

* Data Sources:

   
   |Item |Description |
   |---|---|
   |[byteplus_vke_clusters](https://registry.terraform.io/providers/byteplus-sdk/byteplus/latest/docs/data-sources/vke_clusters) |Query details about clusters. |
   |[byteplus_vke_node_pools](https://registry.terraform.io/providers/byteplus-sdk/byteplus/latest/docs/data-sources/vke_node_pools) |Query detailed information about node pools. |
   |[byteplus_vke_nodes](https://registry.terraform.io/providers/byteplus-sdk/byteplus/latest/docs/data-sources/vke_nodes) |Query detailed information about nodes. |
   |[byteplus_vke_support_addons](https://registry.terraform.io/providers/byteplus-sdk/byteplus/latest/docs/data-sources/vke_support_addons) |Query add\-ons supported by VKE. |
   |[byteplus_vke_addons](https://registry.terraform.io/providers/byteplus-sdk/byteplus/latest/docs/data-sources/vke_addons) |Query detailed information about add\-ons. |
   


For more information, see [Terraform Registry](https://registry.terraform.io/providers/byteplus-sdk/byteplus/latest/docs).
