---
title: "FAQ"
product: " Vital Kubernetes Engine"
product_code: "vke"
source: "https://docs.byteplus.com/en/docs/vke/FAQ"
---

This topic provides answers to frequently asked questions during the use of VCI Agent Sandbox.


<span id="YmAz6ppa"></span>
### How do I handle generation failures for system volume snapshots?

Check the resource status in the `status` field of the SandboxSnapshot CR resource.

The `status` field records the specific reason for failure. You can try to resolve the issue. If the issue persists, you can [submit a ticket](https://console.byteplus.com/workorder/create) or contact your BytePlus account manager for assistance.



<span id="1VTYg5ba"></span>
###  How do I handle errors that occur during sandbox operation?

You can view the logs of the pod that corresponds to the agent\-sandbox application to resolve the issue.


1. Log in to the [VKE console](https://console.byteplus.com/vke).

2. In the left navigation bar, click **Application center \> Helm**.

3. On the **Helm** page, select the target project, cluster, and namespace, and find the application deployed based on the agent\-sandbox template.

4. On the agent\-sandbox application details page, click the name of the cluster associated with the application on the **Overview** tab.

5. On the cluster management page, click **Workload** \> **Pod** in the left navigation bar. Find the pod named agent\-sandbox\-controller in the agent\-sandbox\-system namespace or the namespace you specify and view its logs.

6. Resolve the issue based on the logs. If the issue persists, you can [submit a ticket](https://console.byteplus.com/workorder/create) or contact your BytePlus account manager for assistance.
