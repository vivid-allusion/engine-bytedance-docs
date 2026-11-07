---
title: "Creating instances by specifying subnets"
product: " Vital Kubernetes Engine"
product_code: "vke"
source: "https://docs.byteplus.com/en/docs/vke/Creating-an-instance-based-on-specified-subnets"
---

VCI supports creating instances using the default subnet or a specified subnet. This topic describes the steps of creating a VCI based on a specified subnet.

<span id=".6IOM5pmv5L-h5oGv"></span>
## Background information

If no subnet is specified, the system uses the default subnet, that is, the pod subnet specified during cluster creation.

<span id=".5L2_55So6ZmQ5Yi2"></span>
## Usage limits


* The availability zone to which the subnet belongs must already have a virtual node.

* After the instance is created, its subnet cannot be changed.


<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites


* A cluster for VCI applications has been created. For details, see [Using VCI in VPC-CNI clusters](https://docs.byteplus.com/en/docs/vke/Using-VCI-in-Vital-Kubernetes-Engine) and [Using VCI in Flannel clusters](https://docs.byteplus.com/en/docs/vke/Using-VCI-in-Flannel-cluster).

* A VPC and its subnet have been created. For details, see [Creating VPCs](https://docs.byteplus.com/en/docs/vpc/Creating-a-VPC).


<span id=".a3ViZXJuZXRlcy3mlrnlvI_liJvlu7o="></span>
## Using the Kubernetes approach

When creating a pod or workload (including Deployment, StatefulSet, Job, or CronJob), specify the subnet by adding an annotation.

The annotation description is as follows.


|Annotation key |Annotation sample value |Description |Required |
|---|---|---|---|
|vke.volcengine.com/preferred\-subnet\-ids |subnet\-3tispp1nai\*\*\*\* |Specify a subnet.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">You can specify multiple subnets across multiple availability zones. Separate them with commas (<code>,</code>).</div><br><br><br>* <div data-tips="true" data-tips-type="tip">If you specify multiple subnets, the system selects the subnet with the most available IP addresses to create the VCI.</div><br> |Required for this scenario |


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
        vke.volcengine.com/preferred-subnet-ids: subnet-3tispp1nai**** # Specify the ID of the subnet.
      labels:
        app: nginx
    spec:
      containers:
      - name: nginx
        image: cr-cn-beijing.volces.com/tw/nginx:1.0 # The address and version of the container image. Replace the value with your actual information.
        ports:
        - containerPort: 80
```


<span id=".5o6n5Yi25Y-w5pa55byP"></span>
## Using the console

Similarly, specify the subnet by adding an annotation when creating a workload.

The following figure shows how to create a stateless workload (Deployment). The procedure for creating other workloads is similar. For detailed steps of creating workloads, see [Workloads](https://docs.byteplus.com/en/docs/vke/Workload-overview).

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">VCI does not support DaemonSets. For more information, see <a href="https://docs.byteplus.com/en/docs/vke/VCI-limits">Limits</a>.</div>


<span id=".5p-l6K-i5a6e5L6L5omA5bGe5a2Q572R"></span>
## Querying the subnet of an instance

Obtain the ID of the subnet used by the VCI by using the pod annotation.


|Annotation key |Annotation sample value |Description |
|---|---|---|
|vke.volcengine.com/used\-subnet\-id |subnet\-128fhnvjjgg\*\*\*\* |The ID of the subnet to which the instance belongs. |


<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_54fae51f7a230a3c7088d1e1799a254c.png) </span>
