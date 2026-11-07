---
title: "Overview"
product: "Machine Learning Platform"
product_code: "mlp"
source: "https://docs.byteplus.com/en/docs/mlp/Overview"
---

mirrors encapsulate the software dependencies required for a program to run. Developing code, training, and deploying models on the Machine Learning Platform requires mirrors to provide a running environment. The [Container Registry] module provides users with the ability to manage mirrors, allowing users to version and manage mirrors, view mirror details, and build custom mirrors based on different types of mirrors.

<span id="支持的镜像类型"></span>
# Supported mirror types

Machine Learning Platform allows users to use multiple types of mirrors. Various workloads can be created on the console interface by simply selecting a preset/custom mirror, or by filling in the URL of the public mirror.


* Preset mirror: The platform provides users with a rich set of preset mirrors, including Python, CUDA, PyTorch, and other commonly used machine learning mirrors, which can be used out of the box.

* Public mirror: If the user's mirror is stored in a Container Registry that supports public \*\* network access, such as DockerHub, Azure ACR, AWS ECR, etc., the URL filled in the mirror can be directly pulled when creating the workload, without migrating to BytePlus.

   * When pulling the public network mirror directly, the pulling speed may be slow or the pulling failure may be caused by the instability of the public network.

   * For mirrors on the public network, support asking users to provide the username and key of the registry (it is recommended to provide temporary login keys as much as possible to avoid key leakage) to pull private mirrors.



&nbsp;

* 

*
