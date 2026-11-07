---
title: "How do I handle add-ons with the error message \"Image pull failed\"?"
product: " Vital Kubernetes Engine"
product_code: "vke"
source: "https://docs.byteplus.com/en/docs/vke/What-can-I-do-with-add-ons-in-the-ImagePullBackOff-state"
---

<span id=".6Zeu6aKY5o-P6L-w"></span>
## Issue description

After you install an add\-on in the [VKE console](https://console.byteplus.com/vke), the add\-on is in the **Fail** state with the error message **Image pull failed** displayed.

<span id=".5Y6f5Zug5YiG5p6Q"></span>
## Cause analysis

This issue occurs because the pod related to the add\-on failed to pull the container image.

<span id=".6Kej5Yaz5pa55rOV"></span>
## Solution


1. Log in to the [VKE console](https://console.byteplus.com/vke) **.** 

2. In the left navigation bar, click **Cluster**.

3. On the Cluster page, click the name of the target cluster.

4. In the left navigation bar of the cluster management page, click **Workload** \> **Pod**.

5. Select the namespace where the add\-on pod is located from the **Namespace** drop\-down list, and find the add\-on pod in the **ImagePullBackOff** or **ErrImagePull** state.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">The prefix of the add\-on pod name is usually the add\-on name. For example, if the pod name is <strong>csi\-nas\-node\-drhh2</strong>, it indicates that the pod is related to the csi\-nas add\-on.   </div>
   

6. See [The Pod is in the ImagePullBackOff state](https://docs.byteplus.com/en/docs/vke/Pod-in-the-ImagePullBackOff-state) for troubleshooting.
