---
title: "Ray image list"
product: "BytePlus EMR"
product_code: "E-MapReduce"
source: "https://docs.byteplus.com/en/docs/E-MapReduce/Ray_image_list"
---

The EMR on VKE service provides a list of container images used by external Ray services, enabling users to perform secondary development based on these images.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



1. <div data-tips="true" data-tips-type="tip">The external image list provided by the EMR service is configured with a username and password. You can contact the EMR service engineer to obtain them.</div>



<div data-tips="true" data-tips-type="tip">(Currently, the <code>emr-vke-public-{region}.cr.volces.com/emr/ ray</code> image does not require a username and password; <code>emr-vke-public-{region}.cr.volces.com/emr/ ray-ds</code> and <code>emr-vke-public-{region}.cr.volces.com/emr/ray- ml</code> require a username and password for access.)</div>



2. <div data-tips="true" data-tips-type="tip">The image list provided by EMR, due to network restrictions, is by default only accessible from Volcano Engine ECS machines, including Pod services or other services deployed on ECS machines.</div>



<span id="_1-ray镜像列表"></span>
## Ray image list

Ray is an open\-source distributed computing framework for building and running distributed applications. It supports multiple programming models, including task parallelism and data parallelism, offering high performance and ease of use. Ray simplifies and enhances parallel and distributed computing through its flexible API and efficient runtime.

**Ray provides image repositories for the following scenarios**:


* `emr-vke-public-{region}.cr.volces.com/emr/ ray`: Contains images for Ray and its required dependencies, with Conda, Java8, and Hadoop services built in.

* `emr-vke-public-{region}.cr.volces.com/emr/ ray-ds`: Based on the Ray base image, provides Spark, RayDP, and their dependencies for data processing scenarios.

* `emr-vke-public-{region}.cr.volces.com/emr/ ray-ml`: Built on the Ray\-ds image, provides Torch, Tensorflow, and their dependencies for machine learning scenarios.

* `emr-vke-public-{region}.cr.volces.com/emr/ ray-llm`: Built on the ray\-ml image, provides vllm and its dependencies for model inference scenarios.


Here, `{region}` refers to the English name of the region where the Ray cluster is located. Currently supported regions include North China, East China, South China, and Asia Pacific Southeast (Johor).


|Region (Chinese name) |Region (English name) |Image repository names for different scenarios |
|---|---|---|
|North China 2 (Beijing) |cn\-beijing |* emr\-vke\-public\-cn\-beijing.cr.volces.com/emr/ray<br><br>* emr\-vke\-public\-cn\-beijing.cr.volces.com/emr/ray\-ds<br><br>* emr\-vke\-public\-cn\-beijing.cr.volces.com/emr/ray\-ml |
|North China 2 (Beijing) Autonomous Driving Cloud |cn\-beijing\-selfdrive |* emr\-vke\-public\-cn\-beijing\-selfdrive.cr.volces.com/emr/ray<br><br>* emr\-vke\-public\-cn\-beijing\-selfdrive.cr.volces.com/emr/ray\-ds<br><br>* emr\-vke\-public\-cn\-beijing\-selfdrive.cr.volces.com/emr/ray\-ml |
|East China 2 (Shanghai) |cn\-shanghai |* emr\-vke\-public\-cn\-shanghai.cr.volces.com/emr/ray<br><br>* emr\-vke\-public\-cn\-shanghai.cr.volces.com/emr/ray\-ds<br><br>* emr\-vke\-public\-cn\-shanghai.cr.volces.com/emr/ray\-ml |
|East China 2 (Shanghai) Autonomous Driving Cloud 1 |cn\-shanghai\-autodriving |* emr\-vke\-public\-cn\-shanghai\-autodriving.cr.volces.com/emr/ray<br><br>* emr\-vke\-public\-cn\-shanghai\-autodriving.cr.volces.com/emr/ray\-ds<br><br>* emr\-vke\-public\-cn\-shanghai\-autodriving.cr.volces.com/emr/ray\-ml |
|South China 1 (Guangzhou) |cn\-guangzhou |* emr\-vke\-public\-cn\-guangzhou.cr.volces.com/emr/ray<br><br>* emr\-vke\-public\-cn\-guangzhou.cr.volces.com/emr/ray\-ds<br><br>* emr\-vke\-public\-cn\-guangzhou.cr.volces.com/emr/ray\-ml |
|Asia Pacific Southeast (Johor) |ap\-southeast\-1 |* emr\-vke\-public\-ap\-southeast\-1.cr.volces.com/emr/ray<br><br>* emr\-vke\-public\-ap\-southeast\-1.cr.volces.com/emr/ray\-ds<br><br>* emr\-vke\-public\-ap\-southeast\-1.cr.volces.com/emr/ray\-ml |


**Additionally, different EMR product versions may provide different Ray versions and operating system versions.**  **Distinguish by image tag**:


* For CPU: `{ray.version}-py{python.version}-ubuntu{ubuntu.version}[-{build.version}]-{emr.version}`

* For GPU: `{ray.version}-cu{cuda.version}-py{python.version}-ubuntu{ubuntu.version}[-{build.version}]-{emr.version}`



|Parameters |Note |
|---|---|
|ray.version |Ray version number. Example: 2.9.3 |
|python.version |Python version. Example: 3.9 |
|ubuntu.version |Ubuntu system version. Example: 20.04 |
|cuda.version |CUDA version. Example: 11.8.0 |
|emr.version |Product version of the EMR on VKE service. Example: 1.2.0 |
|build.version |Ray build version information, which is maintained internally by EMR. |


**Supported tag list:** 


* `2.9.3-py3.9-ubuntu20.04-1.2.0` Compatible with EMR product version 1.2.0 and above

* `2.9.3-cu11.8.0-py3.9-ubuntu20.04-1.2.0` Compatible with EMR product version 1.2.0 and above

* `2.22.0-py3.9-ubuntu20.04-1.4.0` Compatible with EMR product version 1.2.0 and above

* `2.22.0-py3.9-ubuntu20.04-155-1.4.0` Compatible with EMR product version 1.2.0 and above

* `2.22.0-cu11.8.0-py3.9-ubuntu20.04-155-1.4.0` Compatible with EMR product version 1.2.0 and above

* `2.30.0-py3.11-ubuntu20.04-207-1.5.0` Compatible with EMR product version 1.2.0 and above

* `2.30.0-cu11.8.0-py3.11-ubuntu20.04-207-1.5.0` Compatible with EMR product version 1.2.0 and above

* `2.30.0-cu12.1.0-py3.11-ubuntu20.04-211-1.5.0` Compatible with EMR product version 1.2.0 and above

* `2.33.0-py3.11-ubuntu20.04-244-1.6.0` Compatible with EMR product version 1.2.0 and above

* `2.33.0-cu11.8.0-py3.11-ubuntu20.04-244-1.6.0` Compatible with EMR product version 1.2.0 and above

* `2.36.0-py3.11-ubuntu20.04-329-3.12.0` Compatible with EMR product version 3.12.0 and above

* `2.36.0-cu11.8.0-py3.11-ubuntu20.04-329-3.12.0` Compatible with EMR product version 3.12.0 and above

* `2.39.0-cu11.8.0-py3.11-ubuntu20.04-380-3.13.0` Compatible with EMR product version 3.14.0 and above

* `2.39.0-py3.11-ubuntu20.04-380-3.13.0` Compatible with EMR product version 3.14.0 and above

* `2.44.0-cu12.2.2-py3.11-ubuntu22.04-562-3.15.1` Compatible with EMR product version 3.15.0 and above

* `2.44.0-py3.11-ubuntu22.04-562-3.15.1` Compatible with EMR product version 3.15.0 and above

* `2.46.0.0-py3.11-ubuntu22.04-680-3.17.0` Compatible with EMR product version 3.17.0 and above

* `2.46.0.0-cu12.4.1-py3.11-ubuntu22.04-680-3.17.0` Compatible with EMR product version 3.17.0 and above

* `2.46.0.1-py3.11-ubuntu22.04-729-3.18.0`Compatible with EMR product version 3.18.0 and later

* `2.46.0.1-cu12.4.1-py3.11-ubuntu22.04-729-3.18.0`Compatible with EMR product version 3.18.0 and later

* `2.50.1.0-py3.11-ubuntu22.04-845-3.19.0`Compatible with EMR product version 3.19.0 and later

* `2.50.1.0-cu12.9.1-py3.11-ubuntu22.04-845-3.19.0`Compatible with EMR product version 3.19.0 and later

* `2.54.0.0-py3.11-ubuntu24.04-958-3.21.0`Compatible with EMR product version 3.21.0 and later

* `2.54.0.0-cu12.9.1-py3.11-ubuntu24.04-958-3.21.0`Compatible with EMR product version 3.21.0 and later

* `2.56.0.0-py3.12-ubuntu24.04-1040-4.0.0`Compatible with EMR product version 4.0.0 and later

* `2.56.0.0-cu13.0.0-py3.12-ubuntu24.04-1040-4.0.0`Compatible with EMR product version 4.0.0 and later


<span id="_1-1-华北region镜像列表"></span>
### Image lists

For example, in the North China region:


|Ray version |Image name |Size |Dependency packages |Note |
|---|---|---|---|---|
|2.56.0.0 |emr\-vke\-public\-cn\-beijing.cr.volces.com/emr/ray:2.56.0.0\-py3.12\-ubuntu24.04\-1040\-4.0.0 |1.40 GiB |* Ray 2.56.0.0 |To obtain the image ID for other Python versions, replace py3.12 with the corresponding Python version, and replace the ending `1040-4.0.0` with one of the following: Python 3.11 corresponds to `1039-4.0.0`, Python 3.10 corresponds to `1041-4.0.0`. Important: ray\-llm only supports Python 3.12. |
||emr\-vke\-public\-cn\-beijing.cr.volces.com/emr/ray:2.56.0.0\-cu13.0.0\-py3.12\-ubuntu24.04\-1040\-4.0.0 |7.13 GiB |* Ray 2.56.0.0<br><br>* CUDA 13.0.0 ||
||emr\-vke\-public\-cn\-beijing.cr.volces.com/emr/ray\-ml:2.56.0.0\-py3.12\-ubuntu24.04\-1040\-4.0.0 |13.26 GiB |* torch 2.11.0+cu130<br><br>* Transformers 4.36.2<br><br>* DeepSpeed 0.17.2 ||
||emr\-vke\-public\-cn\-beijing.cr.volces.com/emr/ray\-ml:2.56.0.0\-cu13.0.0\-py3.12\-ubuntu24.04\-1040\-4.0.0 |18.92 GiB |* torch 2.11.0+cu130<br><br>* Transformers 4.36.2<br><br>* DeepSpeed 0.17.2 ||
||emr\-vke\-public\-cn\-beijing.cr.volces.com/emr/ray\-llm:2.56.0.0\-cu13.0.0\-py3.12\-ubuntu24.04\-1040\-4.0.0 |27.92 GiB |* vLLM 0.22.0<br><br>* Transformers 5.8.0 ||
|2.54.0.0 |emr\-vke\-public\-cn\-beijing.cr.volces.com/emr/ray:2.54.0.0\-py3.11\-ubuntu24.04\-958\-3.21.0 |3.45GiB |* Java 8<br><br>* Hadoop 3.3.4 |To obtain the image ID for other Python versions, replace py3.11 with the corresponding Python version, and replace the ending `958-3.21.0` with one of the following: Python 3.10 corresponds to `959-3.21.0`, Python 3.12 corresponds to `961-3.21.0`. Important: ray\-llm only supports Python 3.11. |
||emr\-vke\-public\-cn\-beijing.cr.volces.com/emr/ray:2.54.0.0\-cu12.9.1\-py3.11\-ubuntu24.04\-958\-3.21.0 |9.37GiB |* Java 8<br><br>* Hadoop 3.3.4 ||
||emr\-vke\-public\-cn\-beijing.cr.volces.com/emr/ray\-ml:2.54.0.0\-py3.11\-ubuntu24.04\-958\-3.21.0 |10.17GiB |* torch 2.8.0+cu129<br><br>* tensorflow 2.15.1<br><br>* deepspeed 0.18.1<br><br>* transformers 4.57.3 ||
||emr\-vke\-public\-cn\-beijing.cr.volces.com/emr/ray\-ml:2.54.0.0\-cu12.9.1\-py3.11\-ubuntu24.04\-958\-3.21.0 |16.02GiB |* torch 2.8.0+cu129<br><br>* tensorflow 2.15.1<br><br>* deepspeed 0.18.1<br><br>* transformers 4.57.3 ||
||emr\-vke\-public\-cn\-beijing.cr.volces.com/emr/ray\-llm:2.54.0.0\-cu12.9.1\-py3.11\-ubuntu24.04\-958\-3.21.0 |20.67GiB |* vllm 0.15.0<br><br>* Triton 3.5.1 ||
|2.50.1.0 |emr\-vke\-public\-cn\-beijing.cr.volces.com/emr/ray:2.50.1.0\-py3.11\-ubuntu22.04\-845\-3.19.0 |2.64GiB |* Java 8<br><br>* Hadoop 3.3.4 |To obtain the image ID for other Python versions, replace py3.11 with the corresponding Python version, and replace the ending 845\-3.19.0 with one of the following:<br><br><br>* Python 3.9 corresponds to 848\-3.19.0<br><br>* Python 3.10 corresponds to 847\-3.19.0<br><br>* Python 3.12 corresponds to 852\-3.19.0 |
||emr\-vke\-public\-cn\-beijing.cr.volces.com/emr/ray\-ds:2.50.1.0\-py3.11\-ubuntu22.04\-845\-3.19.0 |2.96GiB |* Spark 3.5.1<br><br>* RayDP 1.7.0b20250423.dev0 ||
||emr\-vke\-public\-cn\-beijing.cr.volces.com/emr/ray\-ml:2.50.1.0\-py3.11\-ubuntu22.04\-845\-3.19.0 |4.43GiB |* tensorflow 2.15.1<br><br>* torch 2.8.0+cpu ||
||emr\-vke\-public\-cn\-beijing.cr.volces.com/emr/ray:2.50.1.0\-cu12.9.1\-py3.11\-ubuntu22.04\-845\-3.19.0 |8.49GiB |* Java 8<br><br>* Hadoop 3.3.4 ||
||emr\-vke\-public\-cn\-beijing.cr.volces.com/emr/ray\-ds:2.50.1.0\-cu12.9.1\-py3.11\-ubuntu22.04\-845\-3.19.0 |8.81GiB |* Spark 3.5.1<br><br>* RayDP 1.7.0b20250423.dev0 ||
||emr\-vke\-public\-cn\-beijing.cr.volces.com/emr/ray\-ml:2.50.1.0\-cu12.9.1\-py3.11\-ubuntu22.04\-845\-3.19.0 |14.01GiB |* tensorflow 2.15.1<br><br>* torch 2.8.0+cu129 ||
|2.46.0.1 |emr\-vke\-public\-cn\-beijing.cr.volces.com/emr/ray:2.46.0.1\-py3.11\-ubuntu22.04\-729\-3.18.0 |2.55GiB |* Java 8<br><br>* Hadoop 3.3.4 |To obtain the image ID for other Python versions, replace py3.11 with the corresponding Python version, and replace the ending 729\-3.18.0 with one of the following:<br><br><br>* Python 3.9 corresponds to 732\-3.18.0<br><br>* Python 3.10 corresponds to 730\-3.18.0<br><br>* Python 3.12 corresponds to 731\-3.18.0 |
||emr\-vke\-public\-cn\-beijing.cr.volces.com/emr/ray\-ds:2.46.0.1\-py3.11\-ubuntu22.04\-729\-3.18.0 |2.88GiB |* Spark 3.5.1<br><br>* RayDP 1.7.0b20250423.dev0 ||
||emr\-vke\-public\-cn\-beijing.cr.volces.com/emr/ray\-ml:2.46.0.1\-py3.11\-ubuntu22.04\-729\-3.18.0 |4.27GiB |* tensorflow 2.15.1<br><br>* torch 2.6.0+cpu ||
||emr\-vke\-public\-cn\-beijing.cr.volces.com/emr/ray:2.46.0.1\-cu12.4.1\-py3.11\-ubuntu22.04\-729\-3.18.0 |6.92GiB |* Java 8<br><br>* Hadoop 3.3.4 ||
||emr\-vke\-public\-cn\-beijing.cr.volces.com/emr/ray\-ds:2.46.0.1\-cu12.4.1\-py3.11\-ubuntu22.04\-729\-3.18.0 |7.24GiB |* Spark 3.5.1<br><br>* RayDP 1.7.0b20250423.dev0 ||
||emr\-vke\-public\-cn\-beijing.cr.volces.com/emr/ray\-ml:2.46.0.1\-cu12.4.1\-py3.11\-ubuntu22.04\-729\-3.18.0 |10.99GiB |* tensorflow 2.15.1<br><br>* torch 2.6.0+cu124 ||
|2.46.0.0 |emr\-vke\-public\-cn\-beijing.cr.ivolces.com/emr/ray:2.46.0.0\-py3.11\-ubuntu22.04\-680\-3.17.0 |4.85GiB |* Java 8<br><br>* Hadoop 3.3.4 |To obtain the image ID for other Python versions, replace py3.11 with the corresponding Python version, and replace the ending 680\-3.17.0 with one of the following:<br><br><br>* Python 3.9 corresponds to 682\-3.17.0<br><br>* Python 3.10 corresponds to 681\-3.17.0<br><br>* Python 3.12 corresponds to 683\-3.17.0 |
||emr\-vke\-public\-cn\-beijing.cr.ivolces.com/emr/ray\-ds:2.46.0.0\-py3.11\-ubuntu22.04\-680\-3.17.0 |5.35GiB |* Spark 3.5.1<br><br>* RayDP 1.7.0.dev0 ||
||emr\-vke\-public\-cn\-beijing.cr.ivolces.com/emr/ray\-ml:2.46.0.0\-py3.11\-ubuntu22.04\-680\-3.17.0 |9.37GiB |* tensorflow 2.15.1<br><br>* torch 2.6.0+cpu ||
||emr\-vke\-public\-cn\-beijing.cr.ivolces.com/emr/ray:2.46.0.0\-cu12.4.1\-py3.11\-ubuntu22.04\-680\-3.17.0 |12.9GiB |* Java 8<br><br>* Hadoop 3.3.4 ||
||emr\-vke\-public\-cn\-beijing.cr.ivolces.com/emr/ray\-ds:2.46.0.0\-cu12.4.1\-py3.11\-ubuntu22.04\-680\-3.17.0 |13.4GiB |* Spark 3.5.1<br><br>* RayDP 1.7.0.dev0 ||
||emr\-vke\-public\-cn\-beijing.cr.ivolces.com/emr/ray\-ml:2.46.0.0\-cu12.4.1\-py3.11\-ubuntu22.04\-680\-3.17.0 |21.5GiB |* tensorflow 2.15.1<br><br>* torch 2.6.0+cu124 ||
|2.44.0 |emr\-vke\-public\-cn\-beijing.cr.volces.com/emr/ray:2.44.0\-py3.11\-ubuntu22.04\-562\-3.15.1 |4.2GiB |* Java 8<br><br>* Hadoop 3.3.4 |To obtain the image ID for other Python versions, replace py3.11 with the corresponding Python version, and replace the ending 562\-3.15.1 with one of the following:<br><br><br>* Python 3.9 corresponds to 565\-3.15.1<br><br>* Python 3.10 corresponds to 566\-3.15.1<br><br>* Python 3.12 corresponds to 563\-3.15.1 |
||emr\-vke\-public\-cn\-beijing.cr.volces.com/emr/ray:2.44.0\-cu12.2.2\-py3.11\-ubuntu22.04\-562\-3.15.1 |13.3GiB |* Java 8<br><br>* Hadoop 3.3.4 ||
||emr\-vke\-public\-cn\-beijing.cr.volces.com/emr/ray\-ds:2.44.0\-py3.11\-ubuntu22.04\-562\-3.15.1 |4.7GiB |* Spark 3.5.1<br><br>* RayDP 1.7.0.dev0 ||
||emr\-vke\-public\-cn\-beijing.cr.volces.com/emr/ray\-ds:2.44.0\-cu12.2.2\-py3.11\-ubuntu22.04\-562\-3.15.1 |13.8GiB |* Spark 3.5.1<br><br>* RayDP 1.7.0.dev0 ||
||emr\-vke\-public\-cn\-beijing.cr.volces.com/emr/ray\-ml:2.44.0\-py3.11\-ubuntu22.04\-562\-3.15.1 |8.7GiB |* tensorflow 2.15.1<br><br>* torch 2.4.1+cpu ||
||emr\-vke\-public\-cn\-beijing.cr.volces.com/emr/ray\-ml:2.44.0\-cu12.2.2\-py3.11\-ubuntu22.04\-562\-3.15.1 |21.8GiB |* tensorflow 2.15.1<br><br>* torch 2.4.1+cu121 ||
|2.39.0 |emr\-vke\-public\-cn\-beijing.cr.volces.com/emr/ray:2.39.0\-cu11.8.0\-py3.11\-ubuntu20.04\-380\-3.13.0 |7.1GiB |* Java 8<br><br>* Hadoop 3.3.4 |— |
||emr\-vke\-public\-cn\-beijing.cr.volces.com/emr/ray:2.39.0\-py3.11\-ubuntu20.04\-380\-3.13.0 |2.18GiB |* Java 8<br><br>* Hadoop 3.3.4 ||
||emr\-vke\-public\-cn\-beijing.cr.volces.com/emr/ray\-ds:2.39.0\-py3.11\-ubuntu20.04\-380\-3.13.0 |2.54GiB |* Spark 3.5.1<br><br>* RayDP 1.7.0 ||
||emr\-vke\-public\-cn\-beijing.cr.volces.com/emr/ray\-ds:2.39.0\-cu11.8.0\-py3.11\-ubuntu20.04\-380\-3.13.0 |7.45GiB |* Spark 3.5.1<br><br>* RayDP 1.7.0 ||
||3emr\-vke\-public\-cn\-beijing.cr.volces.com/emr/ray\-ml:2.39.0\-cu11.8.0\-py3.11\-ubuntu20.04\-380\-3.13.0 |10.87GiB |* tensorflow 2.11.0<br><br>* torch 2.0.1 ||
||emr\-vke\-public\-cn\-beijing.cr.volces.com/emr/ray\-ml:2.39.0\-py3.11\-ubuntu20.04\-380\-3.13.0 |3.91GiB |* tensorflow 2.11.0<br><br>* torch 2.0.1 ||
|2.36.0 |emr\-vke\-public\-cn\-beijing.cr.volces.com/emr/ray:2.36.0\-py3.11\-ubuntu20.04\-329\-3.12.0 |4.11GiB |* Java 8<br><br>* Hadoop 3.3.4 |— |
||emr\-vke\-public\-cn\-beijing.cr.volces.com/emr/ray:2.36.0\-cu11.8.0\-py3.11\-ubuntu20.04\-329\-3.12.0 |13.6GiB |* Java 8<br><br>* Hadoop 3.3.4 ||
||emr\-vke\-public\-cn\-beijing.cr.volces.com/emr/ray\-ds:2.36.0\-py3.11\-ubuntu20.04\-329\-3.12.0 |4.6GiB |* Spark 3.5.1<br><br>* RayDP 1.7.0 ||
||emr\-vke\-public\-cn\-beijing.cr.volces.com/emr/ray\-ds:2.36.0\-cu11.8.0\-py3.11\-ubuntu20.04\-329\-3.12.0 |14.1GiB |* Spark 3.5.1<br><br>* RayDP 1.7.0 ||
||emr\-vke\-public\-cn\-beijing.cr.volces.com/emr/ray\-ml:2.36.0\-py3.11\-ubuntu20.04\-329\-3.12.0 |8.84GiB |* tensorflow 2.11.0<br><br>* torch 2.0.1 ||
||emr\-vke\-public\-cn\-beijing.cr.volces.com/emr/ray\-ml:2.36.0\-cu11.8.0\-py3.11\-ubuntu20.04\-329\-3.12.0 |22.1GiB |* tensorflow 2.11.0<br><br>* torch 2.0.1 ||
|2.33.0 |emr\-vke\-public\-cn\-beijing.cr.volces.com/emr/ray:2.33.0\-cu11.8.0\-py3.11\-ubuntu20.04\-244\-1.6.0 |6.67GiB |* Java 8<br><br>* Hadoop 3.3.4 |— |
||emr\-vke\-public\-cn\-beijing.cr.volces.com/emr/ray:2.33.0\-py3.11\-ubuntu20.04\-244\-1.6.0 |1.75GiB |* Java 8<br><br>* Hadoop 3.3.4 ||
||emr\-vke\-public\-cn\-beijing.cr.volces.com/emr/ray\-ds:2.33.0\-cu11.8.0\-py3.11\-ubuntu20.04\-244\-1.6.0 |7.02GiB |* Spark 3.5.1<br><br>* RayDP 1.7.0 ||
||emr\-vke\-public\-cn\-beijing.cr.volces.com/emr/ray\-ds:2.33.0\-py3.11\-ubuntu20.04\-244\-1.6.0 |2.11GiB |* Spark 3.5.1<br><br>* RayDP 1.7.0 ||
||emr\-vke\-public\-cn\-beijing.cr.volces.com/emr/ray\-ml:2.33.0\-cu11.8.0\-py3.11\-ubuntu20.04\-244\-1.6.0 |10.44GiB |* tensorflow 2.11.0<br><br>* torch 2.0.1 ||
||emr\-vke\-public\-cn\-beijing.cr.volces.com/emr/ray\-ml:2.33.0\-py3.11\-ubuntu20.04\-244\-1.6.0 |3.48GiB |* tensorflow 2.11.0<br><br>* torch 2.0.1 ||
|2.30.0 |emr\-vke\-public\-cn\-beijing.cr.volces.com/emr/ray:2.30.0\-py3.11\-ubuntu20.04\-207\-1.5.0 |1.76GiB |* Java 8<br><br>* Hadoop 3.3.4 |— |
||emr\-vke\-public\-cn\-beijing.cr.volces.com/emr/ray\-ds:2.30.0\-py3.11\-ubuntu20.04\-207\-1.5.0 |2.11GiB |* Spark 3.5.1<br><br>* RayDP 1.7.0 ||
||emr\-vke\-public\-cn\-beijing.cr.volces.com/emr/ray\-ml:2.30.0\-py3.11\-ubuntu20.04\-207\-1.5.0 |3.46GiB |* tensorflow 2.11.0<br><br>* torch 2.0.1 ||
||emr\-vke\-public\-cn\-beijing.cr.volces.com/emr/ray:2.30.0\-cu11.8.0\-py3.11\-ubuntu20.04\-207\-1.5.0 |6.67GiB |* Java 8<br><br>* Hadoop 3.3.4 ||
||emr\-vke\-public\-cn\-beijing.cr.volces.com/emr/ray\-ds:2.30.0\-cu11.8.0\-py3.11\-ubuntu20.04\-207\-1.5.0 |7.02GiB |* Spark 3.5.1<br><br>* RayDP 1.7.0 ||
||emr\-vke\-public\-cn\-beijing.cr.volces.com/emr/ray\-ml:2.30.0\-cu11.8.0\-py3.11\-ubuntu20.04\-207\-1.5.0 |10.42GiB |* tensorflow 2.11.0<br><br>* torch 2.0.1 ||
||emr\-vke\-public\-cn\-beijing.cr.volces.com/emr/ray:2.30.0\-cu12.1.0\-py3.11\-ubuntu20.04\-211\-1.5.0 |6.66GiB |* Java 8<br><br>* Hadoop 3.3.4 ||
||emr\-vke\-public\-cn\-beijing.cr.volces.com/emr/ray\-ds:2.30.0\-cu12.1.0\-py3.11\-ubuntu20.04\-211\-1.5.0 |7.01GiB |* Spark 3.5.1<br><br>* RayDP 1.7.0 ||
||emr\-vke\-public\-cn\-beijing.cr.volces.com/emr/ray\-ml:2.30.0\-cu12.1.0\-py3.11\-ubuntu20.04\-211\-1.5.0 |10.82GiB |* tensorflow 2.11.0<br><br>* torch 2.0.1 ||
|2.22.0 |emr\-vke\-public\-cn\-beijing.cr.volces.com/emr/ray:2.22.0\-py3.9\-ubuntu20.04\-178\-1.5.0 |1.66GiB |* Java 8<br><br>* Hadoop 3.3.4 |— |
||emr\-vke\-public\-cn\-beijing.cr.volces.com/emr/ray\-ds:2.22.0\-py3.9\-ubuntu20.04\-178\-1.5.0 |2.01GiB |* Spark 3.5.1<br><br>* RayDP 1.7.0 ||
||emr\-vke\-public\-cn\-beijing.cr.volces.com/emr/ray\-ml:2.22.0\-py3.9\-ubuntu20.04\-178\-1.5.0 |3.45GiB |* tensorflow 2.11.0<br><br>* torch 2.0.1 ||
||emr\-vke\-public\-cn\-beijing.cr.volces.com/emr/ray:2.22.0\-cu11.8.0\-py3.9\-ubuntu20.04\-178\-1.5.0 |6.56GiB |* Java 8<br><br>* Hadoop 3.3.4 ||
||emr\-vke\-public\-cn\-beijing.cr.volces.com/emr/ray\-ds:2.22.0\-cu11.8.0\-py3.9\-ubuntu20.04\-178\-1.5.0 |6.91GiB |* Spark 3.5.1<br><br>* RayDP 1.7.0 ||
||emr\-vke\-public\-cn\-beijing.cr.volces.com/emr/ray\-ml:2.22.0\-cu11.8.0\-py3.9\-ubuntu20.04\-178\-1.5.0 |12.09GiB |* tensorflow 2.11.0<br><br>* torch 2.0.1 ||
|2.9.3 |emr\-vke\-public\-cn\-beijing.cr.volces.com/emr/ray:2.9.3\-py3.9\-ubuntu20.04\-1.2.0 |1.66GiB |* Java 8<br><br>* Hadoop 3.3.4 |— |
||emr\-vke\-public\-cn\-beijing.cr.volces.com/emr/ray\-ds:2.9.3\-py3.9\-ubuntu20.04\-1.2.0 |2.01GiB |* Spark 3.5.1<br><br>* RayDP 1.7.0 ||
||emr\-vke\-public\-cn\-beijing.cr.volces.com/emr/ray\-ml:2.9.3\-py3.9\-ubuntu20.04\-1.2.0 |3.45GiB |* tensorflow 2.11.0<br><br>* torch 2.0.1 ||
||emr\-vke\-public\-cn\-beijing.cr.volces.com/emr/ray:2.9.3\-cu11.8.0\-py3.9\-ubuntu20.04\-1.2.0 |6.56GiB |* Java 8<br><br>* Hadoop 3.3.4 ||
||emr\-vke\-public\-cn\-beijing.cr.volces.com/emr/ray\-ds:2.9.3\-cu11.8.0\-py3.9\-ubuntu20.04\-1.2.0 |6.91GiB |* Spark 3.5.1<br><br>* RayDP 1.7.0 ||
||emr\-vke\-public\-cn\-beijing.cr.volces.com/emr/ray\-ml:2.9.3\-cu11.8.0\-py3.9\-ubuntu20.04\-1.2.0 |12.09GiB |* tensorflow 2.11.0<br><br>* torch 2.0.1 ||


<span id="_2-使用场景"></span>
## Use cases


* Direct use: The images provided by EMR are ready to use out of the box and support task execution for relevant scenarios.

* As a base image: If the images provided by EMR do not fully meet requirements, you can perform secondary development based on these images to define images for specific tasks.


<span id="_3-使用示例"></span>
## **Usage examples**

The following explains direct use as an example. You can also refer to [Run jobs with a custom Docker image](https://docs.byteplus.com/docs/E-MapReduce/Run_jobs_with_a_custom_Docker_image).


1. Environment preparation

   1. Deploy the Ray service in the EMR on VKE product.

   2. To run RayJob tasks using the kubectl command, you need to install the kubectl tool (refer to [Install and configure kubectl](https://kubernetes.io/docs/tasks/tools/)), and configure the connection information for the Volcano Engine VKE cluster (refer to [Connect to the VKE cluster](https://www.volcengine.com/docs/6460/100919#%E6%AD%A5%E9%AA%A4%E4%BA%8C%EF%BC%9A%E8%BF%9E%E6%8E%A5%E9%9B%86%E7%BE%A4)).

2. Generate a secret


You can use the following command to generate a secret:

```Bash
kubectl create secret docker-registry my-docker-secret --docker-server={DOCKER_REGISTRY_SERVER} --docker-username={DOCKER_USER} --docker-password={DOCKER_PASSWORD}  -n {YOUR_NAMESPACE}
```


Where:


* `my-docker-secret`: Secret name. Used as the value for `imagePullSecrets` in the following Yaml file.

* `YOUR_NAMESPACE`: The namespace for running Ray tasks.

* `DOCKER_REGISTRY_SERVER`, `DOCKER_USER`, `DOCKER_PASSWORD`: Docker image repository address, username, and password. You can contact the EMR service engineer to obtain the relevant parameter values.

3. RayJob usage examples


test.yaml file examples

```YAML
apiVersion: ray.io/v1
kind: RayJob
metadata:
  name: rayjob-sample
spec:
  entrypoint: python /home/ray/samples/sample_code.py
  # shutdownAfterJobFinishes specifies whether the RayCluster should be deleted after the RayJob finishes. Default is false.
  shutdownAfterJobFinishes: true

  # ttlSecondsAfterFinished specifies the number of seconds after which the RayCluster will be deleted after the RayJob finishes.
  ttlSecondsAfterFinished: 300

  submitterPodTemplate:
    spec:
      imagePullSecrets:
         - name: my-docker-secret
      restartPolicy: OnFailure
      containers:
         - name: submit-image
           image: emr-vke-public-cn-beijing.cr.volces.com/emr/ray-ds:2.9.3-py3.9-ubuntu20.04-1.2.0

  # rayClusterSpec specifies the RayCluster instance to be created by the RayJob controller.
  rayClusterSpec:
    rayVersion: '2.9.3' # should match the Ray version in the image of the containers
    # Ray head pod template
    headGroupSpec:
      rayStartParams:
        dashboard-host: '0.0.0.0'
      template:
        spec:
          imagePullSecrets:
            - name: my-docker-secret
          restartPolicy: OnFailure
          containers:
            - name: ray-head
              image: emr-vke-public-cn-beijing.cr.volces.com/emr/ray:2.9.3-py3.9-ubuntu20.04-1.2.0
              ports:
                - containerPort: 6379
                  name: gcs-server
                - containerPort: 8265 # Ray dashboard
                  name: dashboard
                - containerPort: 10001
                  name: client
              resources:
                limits:
                  cpu: "1"
                requests:
                  cpu: "200m"
              volumeMounts:
                - mountPath: /home/ray/samples
                  name: code-sample
          volumes:
            - name: code-sample
              configMap:
                # Provide the name of the ConfigMap you want to mount.
                name: ray-job-code-sample
                # An array of keys from the ConfigMap to create as files
                items:
                  - key: sample_code.py
                    path: sample_code.py
    workerGroupSpecs:
      # the pod replicas in this group typed worker
      - replicas: 1
        minReplicas: 1
        maxReplicas: 5
        # logical group name, for this called small-group, also can be functional
        groupName: small-group
        # The `rayStartParams` are used to configure the `ray start` command.
        # See https://github.com/ray-project/kuberay/blob/master/docs/guidance/rayStartParams.md for the default settings of `rayStartParams` in KubeRay.
        # See https://docs.ray.io/en/latest/cluster/cli.html#ray-start for all available options in `rayStartParams`.
        rayStartParams: {}
        #pod template
        template:
          spec:
            imagePullSecrets:
              - name: my-docker-secret
            restartPolicy: OnFailure  
            containers:
              - name: ray-worker
                image: emr-vke-public-cn-beijing.cr.volces.com/emr/ray:2.9.3-py3.9-ubuntu20.04-1.2.0
                lifecycle: 
                  preStop:
                    exec:
                      command: [ "/bin/sh","-c","ray stop" ]
                resources:
                  limits:
                    cpu: "1"
                  requests:
                    cpu: "200m"
---
apiVersion: v1
kind: ConfigMap
metadata:
  name: ray-job-code-sample
data:
  sample_code.py: |
    import ray
    import os
    import requests

    ray.init()

    @ray.remote
    class Counter:
        def __init__(self):
            self.name = "test_counter"
            self.counter = 0

        def inc(self):
            self.counter += 1

        def get_counter(self):
            return "{} got {}".format(self.name, self.counter)

    counter = Counter.remote()

    for _ in range(5):
        ray.get(counter.inc.remote())
        print(ray.get(counter.get_counter.remote()))
```


Submit a RayJob:

```Bash
 kubectl apply -f test.yaml -n {YOUR_NAMESPACE}
```
