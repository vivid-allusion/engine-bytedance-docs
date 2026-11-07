---
title: "How do I fix a situation where a VCI pod remains in the Pending state with no image pull events?"
product: " Vital Kubernetes Engine"
product_code: "vke"
source: "https://docs.byteplus.com/en/docs/vke/How-do-I-fix-VCI-pod-Pending-state-with-no-image-pull-events"
---

<span id=".6Zeu6aKY5o-P6L-w"></span>
## Problem description

A VCI needs to access the API Server of the cluster during startup. If a pod stays in the Pending state without triggering any image pull\-related events, the problem may be caused by security group configurations associated with the API Server. This blocks the VCI from connecting to the API Server during initialization.

<span id=".6Kej5Yaz5pa55rOV"></span>
## Solution

You need to modify the security group associated with the API Server of the cluster to allow traffic over the relevant ports between the VCI and the API Server. Follow the steps below to locate and modify the security group associated with the API Server:


1. Log in to the [VKE console](https://console.byteplus.com/vke).

2. In the left navigation bar, click **Cluster**.

3. On the cluster list page, click the target cluster.

4. On the **Overview** page of the cluster, go to the **Overview** tab, click the default security group for nodes, then modify the security group to allow traffic on the relevant ports between the VCI and the API Server.

   <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="1">Warning   </div>
   

   * <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">The default security group for nodes is the security group associated with the API Server of the cluster.   </div>
   

   * <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">When modifying the default security group for nodes, follow the VKE security group usage rules. For details, see <a href="https://docs.byteplus.com/en/docs/vke/Security-group-settings#.6IqC54K56buY6K6k5a6J5YWo57uE6KeE5YiZ">Default security group rules for nodes</a> and <a href="https://docs.byteplus.com/en/docs/vke/Cluster-access-rules">Cluster access rules</a>.   </div>
   


&nbsp;
