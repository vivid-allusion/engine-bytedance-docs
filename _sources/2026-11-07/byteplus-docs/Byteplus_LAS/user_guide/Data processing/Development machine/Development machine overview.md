---
title: "Development machine overview"
product: "Lake AI Service"
product_code: "Byteplus_LAS"
source: "https://docs.byteplus.com/en/docs/Byteplus_LAS/Development_machine_overview"
---

The development machine is a professional development environment purpose\-built by the AI Data Lake service for algorithm developers. It features high efficiency and convenience, enabling developers to quickly start writing, debugging, and running data processing tasks.

In terms of resource support, the development machine offers flexible compute resource configurations, including both CPU and GPU, to meet the computational requirements of tasks with varying complexity. At the same time, it supports mounting storage systems such as TOS and vePFS, providing stable support for data storage and retrieval.

For the development environment, the development machine comes preloaded with a wide range of open\-source images, including Daft, Ray, and Spark, significantly reducing the time required to set up the environment. Additionally, it is equipped with persistent cloud disk storage services dedicated to storing data generated during development, ensuring data security and traceability.

This integrated design enables a truly "out\-of\-the\-box" development model, effectively improving development efficiency and allowing algorithm developers to focus more on core data processing and algorithm optimization tasks.

<span id="03146d1c"></span>
## Product overview

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/7eb77e8e384046259447a433d69179cf~tplv-goo7wpa0wc-image.image) </span>

<span id="054f3075"></span>
## Key features


|Function ||Description |
|---|---|---|
|Development machine creation and access |Create a development machine |When creating a development machine, you can select a resource queue as needed and build the development machine using built\-in images such as Daft, Ray, and Spark, as well as custom images. |
||Remote connection to the development machine |Supports remote connection to instances via SSH from a local terminal, allowing access to instances running in the cloud and debugging local code. |
|Instance configuration and management |Manage the development machine |Manage and modify the lifecycle and configuration of the development machine, for example: shutting down the development machine when idle to save costs. |
||Mount configuration |Supports mounting cloud disks on the development machine for data persistence during development, and also supports mounting TOS. |
||Network configuration |When resources need to be used within a VPC, you can configure the network parameters of the development machine. |
