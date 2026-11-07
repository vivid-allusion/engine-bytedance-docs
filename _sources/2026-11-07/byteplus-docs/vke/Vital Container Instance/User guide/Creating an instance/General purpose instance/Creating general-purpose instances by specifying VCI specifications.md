---
title: "Creating general-purpose instances by specifying VCI specifications"
product: " Vital Kubernetes Engine"
product_code: "vke"
source: "https://docs.byteplus.com/en/docs/vke/Creating_a_general_purpose_instance_based_on_specified_VCI_instance_type"
---

You can create VCIs by specifying VCI specifications. This topic mainly describes how to specify VCI specifications to create **general\-purpose** instances.

<span id=".5L2_55So6ZmQ5Yi2"></span>
## Limits


* The supported regions and availability zones vary based on different [general-purpose](https://docs.byteplus.com/en/docs/vke/VCI-General-purpose) instance families. For details, see [Regions and availability zones](https://docs.byteplus.com/en/docs/vke/VCI-Regions-and-Availability-Zones).

* After you specify VCI specifications, if you do not specify container specifications (`spec.resource`), a pod is created based on the specified specifications. If you specify both VCI and container specifications, the Pod specification is calculated as described in [Instance specification normalization](https://docs.byteplus.com/en/docs/vke/Instance_specification_adjustment_description).


<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites


* A cluster for VCI applications has been created. For details, see [Using VCI in VPC-CNI clusters](https://docs.byteplus.com/en/docs/vke/Using-VCI-in-Vital-Kubernetes-Engine) and [Using VCI in Flannel clusters](https://docs.byteplus.com/en/docs/vke/Using-VCI-in-Flannel-cluster).

* A VPC and its subnet have been created. For details, see [Creating VPCs](https://docs.byteplus.com/en/docs/vpc/Creating-a-VPC).


<span id=".a3ViZXJuZXRlcy3mlrnlvI_liJvlu7o="></span>
## Creating instances by using Kubernetes

When you create a pod or a workload, including a Deployment, StatefulSet, Job, and CronJob, specify VCI specifications by adding an annotation.

The following table describes the annotation.


|Annotation key |Annotation sample value |Description |Required |
|---|---|---|---|
|vci.vke.volcengine.com/preferred\-instance\-types |vci.u1.4c\-8gi |The instance specifications of the [general-purpose](https://docs.byteplus.com/en/docs/vke/VCI-General-purpose) type.<br><br>The instance specifications include the quantity of CPUs and memory. You can specify the vCPU and memory quantity for each container by defining the request and limit for the container. For detailed specifications, see [General-purpose](https://docs.byteplus.com/en/docs/vke/VCI-General-purpose).<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">Billing is performed based on the specified instance specification. For billing descriptions, see <a href="https://docs.byteplus.com/en/docs/vke/VCI-billing-overview">Product billing</a>.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">You can specify multiple specifications (annotation values). Separate multiple specifications with commas (<code>,</code>), and determine the priority by the order in which they are entered. If the higher\-priority specification has no available resources, the lower\-priority specification will be used to create instances.</div><br> |Required for this scenario |


The following sample code shows how to create a Deployment.

```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: nginx-deployment
spec:
  replicas: 2
  selector:
    matchLabels:
      app: nginx
  template:
    metadata:
      annotations:
        vke.volcengine.com/burst-to-vci: enforce  # Force the use of VCI.
        vci.vke.volcengine.com/preferred-instance-types: vci.u1.4c-8gi # Specify general-purpose instance specifications.
      labels:
        app: nginx
    spec:
      containers:
        - image: doc-cn-beijing.cr.volces.com/vke/nginx-demo:v1.0 # The address and version of the container image. Replace the value with your actual information. If you need to use a public image, make sure that the cluster can access the public network.
        imagePullPolicy: Always
        name: nginx
        resources:
          requests:  # Specify the vCPU, memory, and GPU for containers.
            cpu: "2"      
            memory: "4096Mi"
          limits:
            cpu: "4"      
            memory: "8192Mi"
```


<span id=".5o6n5Yi25Y-w5pa55byP5Yib5bu6"></span>
## Creating instances by using the console

Specify the following parameters when you [create a workload](https://docs.byteplus.com/en/docs/vke/Workload-overview) in a VCI cluster.


1. **Basic information**: Select **Vital Container Instance** for the **Computing power type** parameter.

2. **Container configuration**: Specify the requests and limits of CPU and memory in the **ResourceQuota** section based on your business requirements.

3. **Advanced configurations**: Configure the instance specifications in the **VCI specification settings** section. You can use the default instance family or specify a custom instance family.

   When specifying instance families, you can select multiple families under the same instance type. Their priority is determined by the order in which they are selected. For details, see **Specific specifications**. If resources are unavailable in a higher\-priority family, VCI uses a lower\-priority family to create the instance.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_a2a2179f0b071caedd6b07d13ab0562b.png) </span>
