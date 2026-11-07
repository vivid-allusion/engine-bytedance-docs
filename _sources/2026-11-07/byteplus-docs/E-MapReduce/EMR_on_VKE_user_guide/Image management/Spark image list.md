---
title: "Spark image list"
product: "BytePlus EMR"
product_code: "E-MapReduce"
source: "https://docs.byteplus.com/en/docs/E-MapReduce/Spark_image_list"
---

The EMR on VKE service provides a prebuilt image repository for Spark, making it convenient for users to perform secondary development based on these images.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



1. <div data-tips="true" data-tips-type="tip">The external image list provided by the EMR service is configured with a username and password. You can contact the EMR service engineer to obtain the username and password.</div>


2. <div data-tips="true" data-tips-type="tip">The image list provided by EMR is, by default, only accessible on ECS instances of Volcano Engine, including Pod services and other services deployed on ECS instances, due to network restrictions.</div>



<span id="_1-spark镜像列表"></span>
## Spark image list

**Regarding Spark, the following image repositories are provided for these use cases**:

`emr-vke-public-{region}.cr.volces.com/emr/ spark`: Contains images for Spark and its required dependencies. On top of this base image, it also provides a jar package for accessing StarRocks, which is used to access databases and tables in a StarRocks cluster. This is a Volcano Engine self\-developed connector that can directly read and write StarRocks tables. Here, `{region}` is the English name of the region where the Spark cluster is located. Currently supported regions include North China, East China, South China, and Southeast Asia Pacific (Johor).


|Region (Chinese name) |Region |
|---|---|
|North China |cn\-beijing |
|East China |cn\-shanghai |
|South China |cn\-guangzhou |
|Southeast Asia Pacific (Johor) |ap\-southeast\-1 |


**At the same time, different EMR product versions may provide different Spark versions and operating system versions.**  **Distinguish by image tag**:

`{spark.version}--py{python.version}-ubuntu{ubuntu.version}[-{build.version}]-{emr.version}`


|Parameter |Note |
|---|---|
|`spark.version` |Version number of Spark. Example: 3.5.1 |
|`python.version` |Python version. Example: 3.9 |
|`ubuntu.version` |Version of the Ubuntu operating system. Example: 20.04 |
|`build.version` |Internal version number for tracking Spark source code information in EMR; users do not need to pay attention to this. |
|`emr.version` |Product version of the EMR on VKE service. Example: 1.5.0 |


**Supported tag list:** 


* 3.5.1\-1.0.0.87\-1.4.0

* 3.5.1\-py3.9\-ubuntu20.04\-57\-1.5.0


<span id="70eb3806"></span>
### North China region image list


|Image name |Size |Dependency package notes |
|---|---|---|
|emr\-vke\-qa\-cn\-beijing.cr.volces.com/emr/spark:3.5.1\-py3.9\-ubuntu20.04\-57 |1.68GiB |Java：1.8<br><br>Python：3.9<br><br>Hadoop：3.3.4<br><br>Scala：2.12.18<br><br>StarRocks：3.2.3 |
|emr\-vke\-public\-cn\-beijing.cr.volces.com/emr/spark:3.5.1\-1.0.0.87\-1.4.0 |1.68GiB |Java：1.8<br><br>Python：3.9<br><br>Hadoop：3.3.4<br><br>Scala：2.12.18 |


<span id="28e47a2c"></span>
### East China region image list


|Image name |Size |Dependency package notes |
|---|---|---|
|emr\-vke\-public\-cn\-shanghai.cr.volces.com/emr/spark:3.5.1\-py3.9\-ubuntu20.04\-57\-1.5.0 |1.68GiB |Java：1.8<br><br>Python：3.9<br><br>Hadoop：3.3.4<br><br>Scala：2.12.18<br><br>StarRocks：3.2.3 |


<span id="a8c89c9e"></span>
### South China region image list


|Image name |Size |Dependency package notes |
|---|---|---|
|emr\-vke\-public\-cn\-guangzhou.cr.volces.com/emr/spark:3.5.1\-py3.9\-ubuntu20.04\-57\-1.5.0 |1.68GiB |Java：1.8<br><br>Python：3.9<br><br>Hadoop：3.3.4<br><br>Scala：2.12.18<br><br>StarRocks：3.2.3 |


<span id="c6e91efd"></span>
### Johor region image list


|Image name |Size |Dependency package notes |
|---|---|---|
|emr\-vke\-public\-ap\-southeast\-1.cr.volces.com/emr/spark:3.5.1\-py3.9\-ubuntu20.04\-57\-1.5.0 |1.68GiB |Java：1.8<br><br>Python：3.9<br><br>Hadoop：3.3.4<br><br>Scala：2.12.18<br><br>StarRocks：3.2.3 |


<span id="_2-使用场景"></span>
## Use cases


* Direct use: The images provided by EMR are ready to use out of the box and can meet the task execution requirements for relevant scenarios.

* As a base image: To meet requirements not fully covered by the images provided by EMR, secondary development can be performed based on these images to define images for specific tasks.


<span id="_3-使用示例"></span>
## **Usage example**

The following provides an example of direct use. You can also refer to [Run jobs with a custom Docker image](https://docs.byteplus.com/docs/E-MapReduce/109074).


1. Environment preparation

   1. Deploy the Spark service in the EMR on VKE product.

   2. To run SparkJob tasks using the kubectl command, you need to install the kubectl tool (see [Install and configure kubectl](https://kubernetes.io/docs/tasks/tools/)) and configure the connection information for the Volcano Engine VKE cluster (see [Connect to VKE cluster](https://www.volcengine.com/docs/6460/100919?lang=en&_vtm_=a106466.b106468.0_0.0_0.0.897_7633364552918697512#.5q2l6aqk5LqM77ya6L-e5o6l6ZuG576k)).

2. Generate a secret


You can use the following command to generate a secret:

```bash
kubectl create secret docker-registry my-docker-secret --docker-server={DOCKER_REGISTRY_SERVER} --docker-username={DOCKER_USER} --docker-password={DOCKER_PASSWORD}  -n {YOUR_NAMESPACE}
```


Where


* `my-docker-secret`: The name of the secret. Used as the value of `imagePullSecrets` in the following YAML file.

* `YOUR_NAMESPACE`: The namespace for running Spark jobs.

* `DOCKER_REGISTRY_SERVER`, `DOCKER_USER`, `DOCKER_PASSWORD`: The Docker image repository address, username, and password. You can contact the EMR service engineer to obtain the relevant parameter values.

3. SparkPi usage example


test.yaml file example

```yaml
apiVersion: "sparkoperator.k8s.io/v1beta2"
kind: SparkApplication
metadata:
  name: spark-pi
spec:
  type: Scala
  sparkVersion: 3.5.1
  mainClass: org.apache.spark.examples.SparkPi
  mainApplicationFile: "local:///opt/spark/examples/jars/spark-examples_2.12-3.5.1.jar"
  arguments:
    - "100"
  driver:
    cores: 1
    coreLimit: 1000m
    memory: 1g
    image: emr-vke-public-cn-beijing.cr.volces.com/emr/spark-sr:3.5.1-1.0.0.87-1.4.0  # Specify the Driver image
  executor:
    cores: 1
    coreLimit: 1000m
    memory: 1g
    instances: 1
    image: emr-vke-public-cn-beijing.cr.volces.com/emr/spark-sr:3.5.1-1.0.0.87-1.4.0 # Specify the Executor image
  imagePullSecrets:
    - my-docker-secret # Specify the secret for vke to download the docker image
```


Submit SparkJob:

```bash
kubectl apply -f test.yaml -n {YOUR_NAMESPACE}
```
