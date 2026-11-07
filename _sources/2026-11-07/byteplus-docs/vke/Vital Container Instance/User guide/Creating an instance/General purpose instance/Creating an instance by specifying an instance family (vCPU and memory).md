---
title: "Creating an instance by specifying an instance family (vCPU and memory)."
product: " Vital Kubernetes Engine"
product_code: "vke"
source: "https://docs.byteplus.com/en/docs/vke/Creating-a-general-purpose-instance-based-on-specified-container-vCPUs-and-memory"
---

VCI allows you to specify instance families and subnets by using a specific annotation and create general\-purpose instances by specifying the container vCPU and memory.

<span id=".5L2_55So6ZmQ5Yi2"></span>
## Limits


* The supported regions and availability zones vary based on different [general-purpose](https://docs.byteplus.com/en/docs/vke/VCI-General-purpose) instance families. For details, see [Regions and availability zones](https://docs.byteplus.com/en/docs/vke/VCI-Regions-and-Availability-Zones).

* You can configure custom specifications for each container, but the specifications need to meet the vCPU and memory constraints of a VCI when they are aggregated at the instance level.

   If the requirements are not met, the system automatically adjusts the specifications and bills you based on the adjusted specifications. For the adjustment logic, see [Instance specification adjustment description](https://docs.byteplus.com/en/docs/vke/Instance_specification_adjustment_description).


<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites


* A cluster for VCI applications has been created. For details, see [Using VCI in VPC-CNI clusters](https://docs.byteplus.com/en/docs/vke/Using-VCI-in-Vital-Kubernetes-Engine) and [Using VCI in Flannel clusters](https://docs.byteplus.com/en/docs/vke/Using-VCI-in-Flannel-cluster).

* A VPC and its subnet have been created. For details, see [Creating VPCs](https://docs.byteplus.com/en/docs/vpc/Creating-a-VPC).


<span id=".a3ViZXJuZXRlcy3mlrnlvI_liJvlu7o="></span>
## Creating instances by using Kubernetes

You can directly define the request and limit for the corresponding container to specify its vCPU and memory. You can specify instance families by adding an annotation when creating VCIs. The following table describes the annotation used for specifying instance families.


|Annotation key |Annotation sample value |Description |Required |
|---|---|---|---|
|vci.vke.volcengine.com/preferred\-instance\-family |vci.u1 |The **instance specifications** of the [general-purpose](https://docs.byteplus.com/en/docs/vke/VCI-General-purpose) type.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">If you do not specify this annotation, the default instance family <code>vci.u1</code> specified by VCI is used.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">Billing is performed based on the matched instance specification. For billing descriptions, see <a href="https://docs.byteplus.com/en/docs/vke/VCI-billing-overview">Product billing</a>.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">You can specify multiple general\-purpose instance families (annotation values). Separate multiple instance families with commas (<code>,</code>), and determine the priority by the order in which they are entered. If the higher\-priority instance family has no available resources, the lower\-priority instance family will be used to create instances.</div><br> |Optional |


The following sample code shows how to create a Deployment.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">For more information about annotations, see <a href="https://docs.byteplus.com/en/docs/vke/VCI-Pod-annotations">Pod annotation descriptions</a>.</div>


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
        vke.volcengine.com/preferred-subnet-ids: subnet-3tispp1nai**** # Specify the ID of a subnet. You can specify multiple subnets within the same availability zone. To do so, separate them with commas (,).
        vci.vke.volcengine.com/preferred-instance-family: vci.u1 # Specify the instance family of VCI.
      labels:
        app: nginx
    spec:
      containers:
      - name: nginx
        image: doc-cn-beijing.cr.volces.com/vke/nginx-demo:v1.0 # The address and version of the container image. Replace the value with your actual information. If you need to use a public image, make sure that the cluster can access the public network.
        ports:
        - containerPort: 80
        resources:
          requests:  # Specify the container vCPU and memory.
            cpu: "500m"      
            memory: "1024Mi"
          limits:
            cpu: "1"      
            memory: "2048Mi"
```


<span id=".5o6n5Yi25Y-w5pa55byP5Yib5bu6"></span>
## Creating instances by using the console

Specify the following parameters when you [create a workload](https://docs.byteplus.com/en/docs/vke/Workload-overview) in a VCI cluster.


1. **Basic information**: Select **Vital Container Instance** for the **Computing power type** parameter.

2. **Container configuration**: Specify the requests and limits of CPU and memory in the **ResourceQuota** section based on your business requirements.

3. **Advanced configurations**: Configure the instance specifications in the **VCI specification settings** section. You can use the default instance family or specify a custom instance family.

   When specifying instance families, you can select multiple families under the same instance type. Their priority is determined by the order in which they are selected. For details, see **Specific specifications**. If resources are unavailable in a higher\-priority family, VCI uses a lower\-priority family to create the instance.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_a2a2179f0b071caedd6b07d13ab0562b.png) </span>
