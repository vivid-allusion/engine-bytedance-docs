---
title: "Run jobs with a custom Docker image"
product: "BytePlus EMR"
product_code: "E-MapReduce"
source: "https://docs.byteplus.com/en/docs/E-MapReduce/Run_jobs_with_a_custom_Docker_image"
---

EMR On VKE supports using custom Docker images as the default runtime for workloads of tasks in the cluster. The following are the advantages of using custom images:


* You can define software packages or libraries that are not provided in the official EMR version to improve workload performance or support your tasks.

* You can use existing pipelines to unify the development, testing, and deployment processes, simplifying dependency management.

* You can control the images released to the production environment to meet requirements such as organizational compliance for workloads.


<span id="自定义镜像的基本运行原理"></span>
## Basic operating principle of custom images

We use a Spark cluster as an example for illustration. The operating principle of SparkOperator in EMR On VKE is as follows:

<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_6abb3962c8485b4016eef7c42f448281.png) </span>

After submitting a task, Spark Operator uses the image defined in the pre\-customized template or task template to start the Driver Pod, and then starts the Executor Pod. Therefore, you can modify the configuration to enable the use of custom images in both the Driver Pod and Executor Pod.

<span id="自定义镜像使用流程"></span>
## Custom image usage process

<span id="步骤一：获取-spark-或-ray-的基础镜像"></span>
### Step 1: Obtain the base image for Spark or Ray

EMR On VKE provides base images for running Spark and Ray jobs, which include the basic dependencies required by the open\-source versions.

You can obtain the base images for Spark and Ray using the following commands:

```bash
# Spark base image
docker pull emr-vke-public-cn-beijing.cr.volces.com/emr/spark:3.5.1-1.0.0.59-1.3.0
# Ray base image
docker pull emr-vke-public-cn-beijing.cr.volces.com/emr/ray:2.9.3-py3.9-ubuntu20.04-1.2.0
```


<span id="步骤二：自定义基础镜像"></span>
### Step 2: Customize the base image


1. Create a new Dockerfile with the following content:


```bash
# Please replace xxxx with the image version you require
FROM emr-vke-public-cn-beijing.cr.volces.com/emr/spark:xxxx
# Other installation commands, such as RUN pip3 install --upgrade boto3 pandas numpy // For python 3
```



2. Run the command in the directory where the Dockerfile is located to generate the corresponding image:


```bash
docker build -t $(PUB_TAG_VKE):$(VERSION) .
```


<span id="步骤三：（可选）验证自定义镜像"></span>
### Step 3 (optional): Validate the custom image


* Basic image validation

   * Validation of username, workingdir, and entrypoint.

   * Validation of env.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">You can use the docker inspect command to view the relevant details.</div>



* Job validation

   * Validation of required component files, such as the corresponding Spark directory, startup scripts, and so on.

   * Execute simple commands to ensure the job can run.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Depending on the image, you can use different docker run commands to perform specific simple tasks.</div>


<span id="步骤四：发布自定义镜像"></span>
### Step 4: Publish the custom image

You can use the Docker push command to publish the image to the Volcano Engine image center under your account, so that the image can be used in subsequent jobs:

```bash
docker push xxx/spark:3.5.1-customized
```


To ensure that the image can be correctly obtained in the VKE cluster later, configure the corresponding [image pull secret](https://kubernetes.io/docs/tasks/configure-pod-container/pull-image-private-registry/) for the VKE cluster according to the permissions of your image repository.

For example, you can use the following command to generate a secret key:

```bash
kubectl create secret docker-registry my-docker-secret --docker-server=DOCKER_REGISTRY_SERVER --docker-username=DOCKER_USER --docker-password=DOCKER_PASSWORD --docker-email=DOCKER_EMAIL -n YOUR_NAMESPACE
```


<span id="步骤五：提交作业"></span>
### Step 5: Submit Job

<span id="提交-spark-作业"></span>
#### Submit Spark job

Currently, jobs can be submitted using Spark Submit (log in to the SparkOperator node) or using kubectl to submit SparkApplication jobs. We use the SparkApplication method as an example.

Use `kubectl apply -f` to submit the following job:

```yaml
apiVersion: "sparkoperator.k8s.io/v1beta2"
kind: SparkApplication
metadata:
  name: spark-wordcount
spec:
  type: Scala
  sparkVersion: 3.2.1
  mainClass: org.apache.spark.examples.SparkPi
  mainApplicationFile: "tos://yourTosPath"
  arguments:
    - "1000"
  driver:
    cores: 1
    coreLimit: 1000m
    memory: 8g
    image: xxx/spark:3.5.1-customized  # Specify custom Driver image
  executor:
    cores: 1
    coreLimit: 1000m
    memory: 4g
    memoryOverhead: 2g
    instances: 1
    image: xxx/spark:3.5.1-customized # Specify custom Driver image
  imagePullSecrets:
    - {{ your-secret }} # Specify the secret key for vke to download docker images
```


<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">You can also specify the image address and download secret key for Executor Pod and Driver Pod by modifying the default configuration.</div>


<div data-tips="true" data-tips-type="warning">In Spark on Kubernetes, the priority order for images is:</div>



1. <div data-tips="true" data-tips-type="warning">Settings in the SparkApplication specification (submitted using kubectl apply).</div>


2. <div data-tips="true" data-tips-type="warning">Configuration of spark.kubernetes.container.image in spark\-defaults.conf.</div>


3. <div data-tips="true" data-tips-type="warning">Settings in spark.kubernetes.driver.podTemplateFile or spark.kubernetes.executor.podTemplateFile.</div>



<span id="提交-kuberay-作业"></span>
#### Submit KubeRay job

Currently, Ray supports both RayCluster and RayJob methods. The RayJob method supports specifying custom images. To submit RayJob jobs, refer to the usage example in [Ray image list](https://docs.byteplus.com/docs/undefined/69aa39258f7b90052e4c5ea4).

<span id="修改-raycluster-crd-以使用自定义镜像"></span>
#### Modify the RayCluster CRD to use a custom image

We need to modify the custom resource RayCluster created in the Ray cluster to submit tasks using Pods pre\-launched by RayCluster. The header section of the CRD definition is as follows:

```yaml
apiVersion: ray.io/v1
kind: RayCluster
```


You can use kubectl to view the relevant information:

```bash
kubectl get raycluster ray-cluster-kuberay -n {您的 EMR 集群 ID} > raycluster.yaml
```


Open the raycluster.yaml file. In its Spec section, you can see the image configuration for the corresponding rayCluster as shown below. Replace the red text with your new image.


1. ray\-head


```yaml
apiVersion: ray.io/v1
kind: RayCluster
metadata:
  ...
spec:
  headGroupSpec:
    ...
    template:
      ...
      spec:
        affinity: {}
        containers:
        - env: []
          image: xxx/ray:2.9.1-customized
          imagePullPolicy: IfNotPresent
          name: ray-head
          ...
          securityContext: {}
          volumeMounts:
          - mountPath: /tmp/ray
            name: log-volume
        imagePullSecrets:
        - name: {{ your-secret }}
  ...
```



2. ray\-worker


```yaml
apiVersion: ray.io/v1
kind: RayCluster
metadata:
  ...
spec:
  headGroupSpec:
    ...
  workerGroupSpecs:
  - groupName: workergroup
    ...
    replicas: 1
    template:
      metadata:
        ...
      spec:
        affinity: {}
        containers:
        - env: []
          image: xxx/ray:2.9.1-customized
          imagePullPolicy: IfNotPresent
          name: ray-worker
          resources:
            ...
        imagePullSecrets:
        - name: {{ your-secret }}
```


After modification, use kubectl to apply the changes:

```bash
kubectl get raycluster {您的 ray cluster 名称} -n {您的 EMR 集群 ID} > raycluster.yaml
```


Then, you need to manually delete the corresponding Pods so that ray\-operator can rebuild the cluster using the new image:

```bash
kubectl delete pod ray-cluster-kuberay-head-{可以通过 kubectl get pod 获取} -n {您的 EMR 集群 ID}
kubectl delete pod ray-cluster-kuberay-worker-workergroup-{可以通过 kubectl get pod 获取} -n {您的 EMR 集群 ID}
```
