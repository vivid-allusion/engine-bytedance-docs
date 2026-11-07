---
title: "Why is the pod instance always in the \"ContainerCreating\" state after the workload is created?"
product: " Vital Kubernetes Engine"
product_code: "vke"
source: "https://docs.byteplus.com/en/docs/vke/Why-is-the-pod-status-always-displayed-as-ContainerCreating-after-a-workload-is-created"
---

<span id=".6Zeu6aKY5o-P6L-w"></span>
### Issue description


1. [A workload](https://docs.byteplus.com/en/docs/vke/Workload-overview) (Deployment, StatefulSet, DaemonSet, Job, or CronJob) was created.

2. On the workload details page, the pod instance remains in the **ContainerCreating** state.


<span id=".6Kej5Yaz5pa55rOV"></span>
### Solution

After you select the container image when creating a workload, if you do not specify an image tag, the system pulls the image with the `latest` tag by default. If the selected image does not have a version with the `latest` tag, the issue described above will occur.

Update the workload by following the steps below:


1. In the upper\-right corner of the workload details page, click **Update**.

   The following figure uses the Deployment details page as an example.

2. In the **Container configuration** step of the workload update procedure, select a specific image tag and complete the update according to the configuration wizard.

3. On the **List of instances** tab of the workload details page, view the pod instance status. If the status is **Running**, the workload has been successfully created and is running normally.
