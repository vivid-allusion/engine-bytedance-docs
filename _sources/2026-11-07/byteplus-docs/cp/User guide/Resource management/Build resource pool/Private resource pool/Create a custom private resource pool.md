---
title: "Create a custom private resource pool"
product: "Code Pipeline"
product_code: "cp"
source: "https://docs.byteplus.com/en/docs/cp/Create_a_custom_private_resource_pool"
---

A private resource pool is a build resource pool that you connect to your own Kubernetes Cluster and manage independently. When the public resource pool based on the VKE Cluster cannot meet build requirements, you can create a private resource pool to run pipeline build tasks. This article describes how to create a private resource pool.

<span id=".6IOM5pmv5L-h5oGv"></span>
## Background

CP supports connecting to a private resource pool (private build cluster) via Agent to run pipeline tasks. This method does not require exposing the cluster's API Server public network address, providing enhanced security.

The Agent connects to the imported external cluster based on the provided Kubeconfig. The external cluster to be imported must meet the following conditions:


* The Server address in the Kubeconfig must be accessible by the Agent.

* Importing clusters running the Windows operating system is not supported.

* Each cluster can only be connected once. If the connection is abnormal, please delete and reconnect.


<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites


* The Kubernetes Cluster to be used as a private resource pool must be prepared in advance. Only certain Kubernetes versions support this feature. For specific Version numbers, refer to the Console.

* Kubeconfig for the cluster has been obtained, see [Organize cluster access using the kubeconfig file](https://kubernetes.io/zh-cn/docs/concepts/configuration/organize-cluster-access-kubeconfig/) for how to obtain it. If using a VKE cluster, log in to the container service console, on the **Basic information \> Connection information** tab of the target cluster, obtain the **Private network access Config**.


<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure


1. Log in to [CP Console ](https://console.byteplus.com/cp).

2. In the left navigation bar, click **Resource management \> ** **Build resource pool ** .

3. Click **Create private resource pool**.

4. On the **Create private resource pool** page, configure the private resource pool information as required.

   
   |Parameter |Description |
   |---|---|
   |Name |Custom private resource pool name. |
   |Sharing scope |Control the workspace permission of the private resource pool.<br><br><br>* All workspaces: All workspaces can use this private resource pool.<br><br>* Specified workspace (recommended): Only specified workspaces can use this private resource pool. |
   |Connection type |Select **Custom,**  and connect your own custom cluster. |
   |Region |Select the scope of the region where the resources are located. |
   |Kubernetes version |Select the Kubernetes version of the custom cluster to be connected. The platform will automatically deploy the corresponding resource build Agent and pipeline engine (Tekton) Addon according to the selected Version.<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><br>* <div data-tips="true" data-tips-type="warning">The selected Version must match the Kubernetes version of the Cluster corresponding to the Kubeconfig. Otherwise, Agent deployment may fail or build tasks may be abnormal.</div><br><br><br>* <div data-tips="true" data-tips-type="warning">After creation, this Version cannot be modified. If the Cluster is upgraded to a new Kubernetes version later, please re\-create the private resource pool.</div><br> |
   |Kubeconfig file |Kubeconfig is the credential for accessing the cluster. Paste the Kubeconfig obtained in the prerequisites into this field. |
   

5. Click **Confirm** to complete the creation of the private resource pool.


<span id=".5ZCO57ut5pON5L2c"></span>
## Subsequent operations


1. Click the private resource pool name to go to the private resource pool details page. On the **Agent** tab, follow the console guide to add an Agent and connect to the private resource pool via Agent.

2. After Agent deployment is complete, you can use the Agent to process pipeline tasks. On the **Create/Edit pipeline \> Basic information** page, in the build resource pool section, select your private resource pool.
