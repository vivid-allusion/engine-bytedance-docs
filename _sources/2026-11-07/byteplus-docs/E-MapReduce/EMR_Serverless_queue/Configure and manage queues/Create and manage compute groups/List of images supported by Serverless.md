---
title: "List of images supported by Serverless"
product: "BytePlus EMR"
product_code: "E-MapReduce"
source: "https://docs.byteplus.com/en/docs/E-MapReduce/List_of_images_supported_by_Serverless"
---

When creating an EMR Serverless compute group, you can directly select the official base images provided by EMR Serverless to quickly obtain a ready\-to\-use runtime environment. This document summarizes the currently available base image types and their version information for creating compute groups, making it easier for you to choose according to your business scenarios.

<span id="751fe02f"></span>
# Important notes


* Images marked with `cu` are GPU versions and support CUDA; those without the `cu` mark are CPU versions.

* The image version number usually follows this format: `{Ray version}-[cu{CUDA version}]-py{Python version}-ubuntu{Ubuntu version}-{internal version}-{EMR version}`.


<span id="80e896cf"></span>
# List of base images

<span id="d08cc9e4"></span>
## ray\-llm: Large model inference scenarios

**Image description:**  A customized Ray Runtime released by the Volcano Engine EMR team, with Ray and its required dependencies built in, and pre\-installed components related to large model inference (such as common deep learning frameworks and dependencies). The image also integrates Conda, Java 8, and Hadoop services, suitable for quickly deploying inference services and online/offline inference tasks on EMR Serverless.


|Image version |Image address |Size |Detailed specifications |
|---|---|---|---|
|`2.54.0.0-cu12.9.1-py3.11-ubuntu24.04-958-3.21.0` |`emr-vke-public-cn-beijing.cr.volces.com/emr/ray-llm:2.54.0.0-cu12.9.1-py3.11-ubuntu24.04-958-3.21.0` |21.17 GiB |CUDA 12.9.1, Python 3.11 |


<span id="50398305"></span>
## daft: Data processing and machine learning scenarios

**Image description:**  A distributed computing engine Runtime released by the Volcano Engine EMR team, with Daft and its required dependencies built in, and pre\-installed Conda, Python, and common data processing libraries, suitable for data cleaning, ETL, feature engineering, and machine learning training tasks.


|Image version |Image address |Size |Detailed specifications |
|---|---|---|---|
|`0.7.2.post6-py3.11-ubuntu24.04` |`las-ai-online-cn-beijing.cr.volces.com/las/ve-daft:0.7.2.post6-py3.11-ubuntu24.04` |6.69 GiB |Python 3.11 (CPU) |
|`0.7.2.post6-cu12.9.1-py3.11-ubuntu24.04` |`las-ai-online-cn-beijing.cr.volces.com/las/ve-daft:0.7.2.post6-cu12.9.1-py3.11-ubuntu24.04` |12.75 GiB |CUDA 12.9.1, Python 3.11 |


<span id="6d41626f"></span>
## ray\-ml: Machine learning scenarios

**Image description:**  A customized Ray Runtime released by the Volcano Engine EMR team, with Ray and its required dependencies built in, and integrated with machine learning components such as Spark, RayDP, PyTorch, TensorFlow, and their dependencies. The image also comes with Conda, Java 8, and Hadoop services pre\-installed, suitable for distributed training, feature engineering, and hybrid computing scenarios with Ray + Spark on EMR Serverless.


|Image version |Image address |Size |Detailed specifications |
|---|---|---|---|
|`2.54.0.0-py3.12-ubuntu24.04-961-3.21.0` |`emr-vke-public-cn-beijing.cr.volces.com/emr/ray-ml:2.54.0.0-py3.12-ubuntu24.04-961-3.21.0` |9.22 GiB |Python 3.12 (CPU) |
|`2.54.0.0-cu12.9.1-py3.12-ubuntu24.04-961-3.21.0` |`emr-vke-public-cn-beijing.cr.volces.com/emr/ray-ml:2.54.0.0-cu12.9.1-py3.12-ubuntu24.04-961-3.21.0` |15.20 GiB |CUDA 12.9.1, Python 3.12 |
|`2.54.0.0-py3.10-ubuntu24.04-959-3.21.0` |`emr-vke-public-cn-beijing.cr.volces.com/emr/ray-ml:2.54.0.0-py3.10-ubuntu24.04-959-3.21.0` |9.84 GiB |Python 3.10 (CPU) |
|`2.54.0.0-cu12.9.1-py3.10-ubuntu24.04-959-3.21.0` |`emr-vke-public-cn-beijing.cr.volces.com/emr/ray-ml:2.54.0.0-cu12.9.1-py3.10-ubuntu24.04-959-3.21.0` |15.82 GiB |CUDA 12.9.1, Python 3.10 |
|`2.54.0.0-cu12.9.1-py3.11-ubuntu24.04-958-3.21.0` |`emr-vke-public-cn-beijing.cr.volces.com/emr/ray-ml:2.54.0.0-cu12.9.1-py3.11-ubuntu24.04-958-3.21.0` |16.40 GiB |CUDA 12.9.1, Python 3.11 |
|`2.54.0.0-py3.11-ubuntu24.04-958-3.21.0` |`emr-vke-public-cn-beijing.cr.volces.com/emr/ray-ml:2.54.0.0-py3.11-ubuntu24.04-958-3.21.0` |10.42 GiB |Python 3.11 (CPU) |
|`2.50.1.0-cu12.9.1-py3.11-ubuntu22.04-845-3.19.0` |`emr-vke-public-cn-beijing.cr.volces.com/emr/ray-ml:2.50.1.0-cu12.9.1-py3.11-ubuntu22.04-845-3.19.0` |13.36 GiB |CUDA 12.9.1, Python 3.11 |


<span id="d7aa38e0"></span>
## ray: Basic Ray scenarios

**Image description:**  A customized Ray Runtime released by the Volcano Engine EMR team, with Ray and its required dependencies built in, and pre\-installed Conda, Java 8, and Hadoop services. This image is suitable for general Ray distributed computing scenarios (such as task scheduling, distributed data processing, Ray Serve, and more), making it easy to quickly build a Ray runtime environment on EMR Serverless.


|Image version |Image address |Size |Detailed specifications |
|---|---|---|---|
|`2.54.0.0-py3.12-ubuntu24.04-961-3.21.0` |`emr-vke-public-cn-beijing.cr.volces.com/emr/ray:2.54.0.0-py3.12-ubuntu24.04-961-3.21.0` |3.52 GiB |Python 3.12 (CPU) |
|`2.54.0.0-cu12.9.1-py3.12-ubuntu24.04-961-3.21.0` |`emr-vke-public-cn-beijing.cr.volces.com/emr/ray:2.54.0.0-cu12.9.1-py3.12-ubuntu24.04-961-3.21.0` |9.58 GiB |CUDA 12.9.1, Python 3.12 |
|`2.54.0.0-py3.10-ubuntu24.04-959-3.21.0` |`emr-vke-public-cn-beijing.cr.volces.com/emr/ray:2.54.0.0-py3.10-ubuntu24.04-959-3.21.0` |3.51 GiB |Python 3.10 (CPU) |
|`2.54.0.0-cu12.9.1-py3.10-ubuntu24.04-959-3.21.0` |`emr-vke-public-cn-beijing.cr.volces.com/emr/ray:2.54.0.0-cu12.9.1-py3.10-ubuntu24.04-959-3.21.0` |9.57 GiB |CUDA 12.9.1, Python 3.10 |
|`2.54.0.0-cu12.9.1-py3.11-ubuntu24.04-958-3.21.0` |`emr-vke-public-cn-beijing.cr.volces.com/emr/ray:2.54.0.0-cu12.9.1-py3.11-ubuntu24.04-958-3.21.0` |9.60 GiB |CUDA 12.9.1, Python 3.11 |
|`2.54.0.0-py3.11-ubuntu24.04-958-3.21.0` |`emr-vke-public-cn-beijing.cr.volces.com/emr/ray:2.54.0.0-py3.11-ubuntu24.04-958-3.21.0` |3.53 GiB |Python 3.11 (CPU) |
|`2.50.1.0-cu12.9.1-py3.11-ubuntu22.04-845-3.19.0` |`emr-vke-public-cn-beijing.cr.volces.com/emr/ray:2.50.1.0-cu12.9.1-py3.11-ubuntu22.04-845-3.19.0` |8.10 GiB |CUDA 12.9.1, Python 3.11 |
|`2.50.1.0-py3.11-ubuntu22.04-845-3.19.0` |`emr-vke-public-cn-beijing.cr.volces.com/emr/ray:2.50.1.0-py3.11-ubuntu22.04-845-3.19.0` |2.52 GiB |Python 3.11 (CPU) |
