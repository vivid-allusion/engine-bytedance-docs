---
title: "Project-based bill splitting"
product: " Vital Kubernetes Engine"
product_code: "vke"
source: "https://docs.byteplus.com/en/docs/vke/Project-based-bill-splitting-for-instances"
---

VCI supports classification of VCI pods by project. This topic describes how to classify and manage VCI resources from the project dimension to address the issue of financial cost allocation.

<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites

To use a project other than **default**, ensure that the project has been created.  For an introduction to projects, see [Project overview](https://docs.byteplus.com/en/docs/resourcemanagement/Project_Overview).

<span id=".5Li6LXZjaS1wb2Qt5oyH5a6a6aG555uu"></span>
## Specifying projects for VCI pods

Specify the project to which a VCI Pod belongs by using a pod annotation.


|Annotation Key |Type |Annotation sample value |Description |
|---|---|---|---|
|vci.vke.volcengine.com/project\-name |String |test\-project |The name of the project to which the VCI pod belongs. |


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">Tip</div>



* <div data-tips="true" data-tips-type="tip">When creating a VCI pod, if the project to which the VCI pod belongs is not specified with this annotation:</div>


   * <div data-tips="true" data-tips-type="tip">If the VCI pod is created in a VKE cluster, it belongs by default to the project of the VKE cluster. If the cluster does not belong to any project, the VCI pod will belong to the <strong>default</strong> project.</div>


   * <div data-tips="true" data-tips-type="tip"> If the VCI pod is created according to <a href="https://docs.byteplus.com/en/docs/vke/Elastically-using-VCI-for-self-managed-Kubernetes-clusters">Using VCI elastically in self\-hosted Kubernetes clusters</a>, the VCI pod will belong to the <strong>default</strong> project.</div>


* <div data-tips="true" data-tips-type="tip">VCI also supports appending this annotation to the VCI pod by using the vci\-profile file. For information about vci\-profile, see <a href="https://docs.byteplus.com/en/docs/vke/Using-VCI-by-configuring-vci-profile">Using VCI by configuring vci\-profile</a>.</div>



The following sample code creates a VCI pod. For more information about creating VCI pods, see [Creating instances](https://docs.byteplus.com/en/docs/vke/Creating-an-instance).

```YAML
apiVersion: v1
kind: Pod
metadata:
  name: demo-vci-pod  # Pod Name.
  namespace: default  # Namespace to which the pods belong.
  annotations:
    vke.volcengine.com/burst-to-vci: enforce  # Force the use of VCI.
    vke.volcengine.com/preferred-subnet-ids: subnet-3tispp1n******** # Specify the ID of a subnet. You can specify multiple subnets within the same availability zone. To do so, separate them with commas (,).
    vci.vke.volcengine.com/preferred-instance-family: vci.u1 # Specify the instance family of the VCI.
    vci.vke.volcengine.com/project-name: doc-project  # The project to which the VCI pod belongs.
spec:
  containers:
  - image: cr-cn-beijing.volces.com/tw/nginx:1.0 # The address and version of the container image. Replace the value with your actual information.
    imagePullPolicy: Always
    name: nginx
    resources:
      requests:  # Specify the vCPU, memory, and GPU settings for the container as needed.
        cpu: 2
        nvidia.com/gpu: 2 # Specify the number of GPUs for the container as needed (same as native one). You can specify both limits and requests, but the values must be equal.
      limits:
        cpu: 2
        nvidia.com/gpu: 2
```


<span id=".5YiG6LSm5ZCO5p-l55yL6K-05piO"></span>
## Viewing results after configuring bill splitting

After you specify the project for the VCI pod, the project will be shown in the **Project** column on the **Split Bills** page. You can query the result by using the following steps:


1. Log in to the BytePlus [Cost Center](https://console.byteplus.com/finance).

2. Select **Bill management** \> **Split bills** in the left navigation bar.

3. On the **Split bills** page, view the project to which the VCI pod bill belongs in the **Project** column.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">After the split bills are issued, the project information will not be immediately reflected on the bills. There will be a delay of 3 to 4 hours.   </div>
