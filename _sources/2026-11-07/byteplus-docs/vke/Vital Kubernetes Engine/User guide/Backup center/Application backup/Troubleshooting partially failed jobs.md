---
title: "Troubleshooting partially failed jobs"
product: " Vital Kubernetes Engine"
product_code: "vke"
source: "https://docs.byteplus.com/en/docs/vke/Handling_partial_failure_issues"
---

If a backup or restore job partially fails, you can perform troubleshooting based on the cause of the failure and retry the job. This topic describes common cases of partially failed backup or restore jobs and their solutions.

<span id="qmF5qe10"></span>
## migrate\-plugin OOM 

<span id="XBVaqFmr"></span>
### Issue description

The backup or restore job partially failed, and the YAML configuration for the migrate\-plugin add\-on shows OOMKilled.

<span id="AbcrkmFo"></span>
### Cause analysis

The migrate\-plugin add\-on has a default memory limit of 512 MiB. When a backup or restore job involves a large number or size of resources, insufficient memory will cause an OOM (Out of Memory).

<span id="oIw4ASEa"></span>
### Solution

Modify the migrate\-plugin add\-on configuration to appropriately increase the memory limit. It is recommended to increase 512 MiB of memory for every 1,000 resources. You can adjust available memory based on your actual requirements. Procedure:


1. In the [VKE console](https://console.byteplus.com/vke/overview), go to the **Cluster** list and click the name of the source cluster of the backup to go to the cluster management page.

2. Click **Workload \> Deployment**. On the page that appears, search for migrate\-plugin in the kube\-system namespace.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_ea2beeca3a29f6f575805d6b1b783404.png) </span>

3. Click **Update** or **Edit Yaml** to modify the memory limit of the migrate\-plugin add\-on. Then, save the configuration.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_bf557fe74050dd8c5e79b2754d845007.png) </span>


<span id="z9F3XVqJ"></span>
## Insufficient RBAC permissions for migrate\-plugin

<span id="s1L9DuKC"></span>
### Issue description

The backup or restore job partially failed, and the job log shows `forbidden: User "xxxx" cannot get resource "xxxx" in API group "xxxx" at the cluster scope`.

<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_0897d4c83b5075030dc81cc0dc04298a.png) </span>

<span id="ms5mgnDF"></span>
### Cause analysis

For data security reasons, some components of the migrate\-plugin add\-on have limited RBAC permissions by default. This results in some resources failing to be backed up or restored due to insufficient permissions.

<span id="kzuUnSdV"></span>
### Solution

Manually modify the configuration of migrate\-plugin\-server in the ClusterRole to grant resource permissions. Procedure:


1. In the [VKE console](https://console.byteplus.com/vke/overview), go to the **Cluster** list and click the name of the source cluster of the backup to go to the cluster management page.

2. Click **Workload \> Resource Explorer**. On the page that appears, find `rbac.authorization.k8s.io` in the API Group category, and click the name to go to the management page.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_de39b076872eeb58231e79676a2f8ed1.png) </span>

3. Click ClusterRole in the Resource definition list. In the list of resources, find migrate\-plugin\-server, and click **Edit Yaml** in the Actions column.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_e59481629a18861891911e7f04d5155d.png) </span>

4. Find the configuration by the API group indicated in the error, and add the missing permissions indicated in the error message. For example, add `priorityclasses` to resources in the `scheduling.k8s.io` API group.

   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">If the migrate\-plugin\-server YAML configuration is missing the API group indicated in the error, add the apiGroup, resources, and verbs configuration items sequentially in accordance with the YAML format.   </div>
   

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_1b8f34d6f1b6c4b9acb2085b74a81d27.png) </span>
