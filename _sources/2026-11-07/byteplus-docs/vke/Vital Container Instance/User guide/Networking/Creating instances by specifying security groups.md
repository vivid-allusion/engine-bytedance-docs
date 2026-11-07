---
title: "Creating instances by specifying security groups"
product: " Vital Kubernetes Engine"
product_code: "vke"
source: "https://docs.byteplus.com/en/docs/vke/Creating-an-instance-based-on-specified-security-groups"
---

VCI supports creating instances using the default security group or a specified security group. This topic describes the steps of creating a VCI based on a specified security group.

<span id=".6IOM5pmv5L-h5oGv"></span>
## Background information

If no security group is specified, the default security group used is the pod security group, which is created by default during VKE cluster creation and allows all inbound and outbound traffic.

<span id=".5L2_55So6ZmQ5Yi2"></span>
## Usage limits


* From the Kubernetes perspective, VCIs do not support updating security groups. If modification is required, we recommend updating the security group and then creating another instance with the updated security group specified for it.

* From the perspective of the elastic network interface (ENI, that is, the primary NIC), VCIs support updating security groups. However, after each update or scaling operation on a VCI, the associated security group will revert to the one specified when the VCI was initially created. In this scenario, you need to create a new instance with the security group re\-specified for it.


<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites


* A cluster for VCI applications has been created. For details, see [Using VCI in VPC-CNI clusters](https://docs.byteplus.com/en/docs/vke/Using-VCI-in-Vital-Kubernetes-Engine) and [Using VCI in Flannel clusters](https://docs.byteplus.com/en/docs/vke/Using-VCI-in-Flannel-cluster).

* A security group has been created. For details, see [Creating security groups](https://docs.byteplus.com/en/docs/vpc/Creating-a-security-group).

* A security group has been configured for the cluster where the VCI application resides. For details, see [Security group settings](https://docs.byteplus.com/en/docs/vke/Security-group-settings).


<span id=".a3ViZXJuZXRlcy3mlrnlvI_liJvlu7o="></span>
## Using the Kubernetes approach

When creating a pod or workload (including Deployment, StatefulSet, Job, or CronJob), specify the security group by adding an annotation.

The annotation description is as follows.


|Annotation key |Annotation sample value |Description |
|---|---|---|
|vke.volcengine.com/security\-group\-ids |`sg-3thbinrkp94bwbh****, sg-2b49fbsd723bf4****` |Specify security groups for the VCI.<br><br><br>* To specify multiple security groups, separate them with commas (,).<br><br>* For security group quantity limits, see [security group limits](https://docs.byteplus.com/en/docs/vpc/Limits#.5a6J5YWo57uE).<br><br>* If you create a VCI with a security group specified for it, the rules of the default security group will not be added.<br><br>* When specifying multiple security groups, pay attention to the impact of combining multiple security groups on network connectivity. For information about combining multiple security groups, see [Security group examples](https://docs.byteplus.com/en/docs/vpc/Security-group-use-cases). |


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
        vke.volcengine.com/security-group-ids: sg-mjpdqrxka3nk5smt1a****** # Specify security group IDs.
      labels:
        app: nginx
    spec:
      containers:
      - name: nginx
        image: cr-cn-beijing.volces.com/tw/nginx:1.0 # The address and version of the container image. Replace the value with your actual information.
        ports:
        - containerPort: 80
```


<span id=".5o6n5Yi25Y-w5pa55byP5Yib5bu6"></span>
## Using the console

Similarly, specify the security group by adding an annotation when creating a workload.

The following figure shows how to create a stateless workload (Deployment). The procedure for creating other workloads is similar. For detailed steps of creating workloads, see [Workloads](https://docs.byteplus.com/en/docs/vke/Workload-overview).

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">VCI does not support DaemonSets. For more information, see <a href="https://docs.byteplus.com/en/docs/vke/VCI-limits">Limits</a>.</div>


<span id=".5p-l6K-i5a6e5L6L5omA5bGe5a6J5YWo57uE"></span>
## Querying security groups of an instance

Security groups of ENIs can be updated. You can query the security groups of an ENI bound to a VCI by using the ID of the ENI.


1. Obtain the VCI ID or the ID of the ENI bound to the VCI.

   * Obtain the VCI ID by checking the value of the pod annotation `vci.vke.volcengine.com/instance-id`.

   * Obtain the ENI ID by checking the value of the pod annotation `vke.volcengine.com/eni-id`.

   <span>![图片](https://lf3-volc-editor.volccdn.com/obj/volcfe/sop-public/upload_5aff8cf5e584e950e465132d8f7b565c.png) </span>

2. Use the ENI ID or instance ID to query associated security groups.

   * Console:

      1. Log in to [VPC console](https://console.byteplus.com/vpc).

      2. Click **Network Interface** in the left navigation bar. On the **Network Interface** page, search for the ENI by its ID.

      3. Click the name of the ENI. On the **Associated Security Groups** tab of the ENI details page, view the security groups.

   * OpenAPI:

      Call the DescribeNetworkInterfaces API to query network interfaces. For details, see [DescribeNetworkInterfaces](https://docs.byteplus.com/en/docs/vpc/DescribeNetworkInterfaces).
