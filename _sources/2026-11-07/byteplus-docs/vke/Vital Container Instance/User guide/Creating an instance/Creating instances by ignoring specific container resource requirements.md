---
title: "Creating instances by ignoring specific container resource requirements"
product: " Vital Kubernetes Engine"
product_code: "vke"
source: "https://docs.byteplus.com/en/docs/vke/Creating-instances-by-ignoring-specific-container-resource-requirements"
---

VCI allows you to ignore the resource requirements of specific containers during the creation of instances. In this way, exclusive resources are not allocated to some containers that do not affect your business in certain scenarios.

<span id=".5Yqf6IO96K-05piO"></span>
## Feature description

You can configure the following environment variable for a container in a VCI pod. VCI will ignore the resource requests of the container during resource adjustment.

```yaml
env:
- name: "__VCI_RESOURCE_IGNORE__"  # Ignore the resources of the container during automatic specification matching.
  value: "TRUE"
```


If a VCI pod has n containers, when VCI matches instance (pod) specifications, it traverses the n containers in the following priority order and matches only one of the following cases:


1. If `"__VCI_RESOURCE_IGNORE__"="TRUE"` is configured, the resource requirements of the container are skipped.

2. If a resource (such as CPU, memory, and GPU) is configured with a `limit`, the `limit` value of the container is added to the resource requirement.

3. If a resource is configured with a `request`, the `request` value of the container is added to the resource requirement.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">VCI matches instance specifications based on the accumulated values of CPU, memory. For more information about specification calculation and matching, see <a href="https://docs.byteplus.com/en/docs/vke/Instance_specification_adjustment_description">Instance specification normalization</a>.</div>


<span id=".5L2_55So6ZmQ5Yi2"></span>
## Limits


* The method described in this topic applies to scenarios such as [creating general-purpose instances by specifying container vCPUs and memory](https://docs.byteplus.com/en/docs/vke/Creating-a-general-purpose-instance-based-on-specified-container-vCPUs-and-memory).

* After the resource requirements of specific containers are ignored, the total resources provided by the matched VCI instance specification may be less than the total resources declared by all containers in the pod. For example:

   * If CPU and memory resource requirements are ignored, CPU and memory resources are shared among containers, and multiple containers may compete for resources.

   * If GPU resource requirements are ignored, GPU resources cannot be shared among containers. In this way, the VCI pod will fail to be created (data plane failure) if its matched instance specification has fewer GPUs than the total declared by all containers.

* We recommend that you use this feature in the following way:

   * For CPU and memory, you can ignore the resource requirements of specified containers. In this way, multiple containers will compete for resources. In addition, you can specify the `limit` for each pod. This prevents containers without a configured `limit` from occupying resources for other containers, improving resource utilization within the pod.

   * For GPU, we recommend that you configure the environment variable only for containers that do not require GPU resources, such as sidecar containers. In this way, other containers can use as much CPU and memory as possible.


<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites

A cluster for VCI applications has been created. For details, see [Using VCI in VPC-CNI clusters](https://docs.byteplus.com/en/docs/vke/Using-VCI-in-Vital-Kubernetes-Engine) and [Using VCI in Flannel clusters](https://docs.byteplus.com/en/docs/vke/Using-VCI-in-Flannel-cluster).

<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure

<span id=".a3ViZXJuZXRlcy3mlrnlvI_liJvlu7o="></span>
### Using the Kubernetes approach

The following sample code shows how to create a Deployment.

```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: nginx-deployment
  labels:
    app: nginx
spec:
  replicas: 2
  selector:
    matchLabels:
      app: nginx
  template:
    metadata:
      annotations:
        vke.volcengine.com/burst-to-vci: enforce  # Force the use of VCI.
      labels:
        app: nginx
    spec:
      containers:
      - name: nginx1
        image: doc-cn-beijing.cr.volces.com/vke/nginx-demo:v1.0 # The address and version of the container image. Replace the value with your actual information. If you need to use a public image, make sure that the cluster can access the public network.
        resources:
          limits:
            cpu: "2000m"
            memory: "4096Mi"
      - name: nginx2
        image: doc-cn-beijing.cr.volces.com/vke/nginx-demo:v1.0 # The address and version of the container image. Replace the value with your actual information. If you need to use a public image, make sure that the cluster can access the public network.
        resources:
          limits:
            cpu: "1000m"
            memory: "2048Mi"
        env:
        - name: "__VCI_RESOURCE_IGNORE__"  # Ignore the resources of the container during automatic specification matching.
          value: "TRUE"
      restartPolicy: Always
```


<span id=".5o6n5Yi25Y-w5pa55byP5Yib5bu6"></span>
### Creating instances by using the console

Specify the following parameters when you [create a workload](https://docs.byteplus.com/en/docs/vke/Workload-overview) in a VCI cluster.


1. **Basic information**: Select **Vital Container Instance** for the **Computing power type** parameter.

2. **Container configuration**: Enable **Ignore resource alignment** in the **ResourceQuota** section.
