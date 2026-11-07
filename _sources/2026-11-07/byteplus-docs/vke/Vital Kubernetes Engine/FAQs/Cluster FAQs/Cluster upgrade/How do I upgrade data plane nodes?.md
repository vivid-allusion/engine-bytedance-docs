---
title: "How do I upgrade data plane nodes?"
product: " Vital Kubernetes Engine"
product_code: "vke"
source: "https://docs.byteplus.com/en/docs/vke/How-are-data-plane-nodes-upgraded"
---

Data plane nodes adopt the in\-place upgrade method. This method involves pulling binary versions of add\-ons for the corresponding Kubernetes version (such as kubelet and containerd) and distributing relevant add\-on parameters.

You can also perform in\-place upgrades in the console. The specific steps are as follows.


1. Make sure that the control plane upgrade is complete. If **Upgrade successful** is displayed in the console, it indicates that the upgrade is complete.

2. Add new nodes. For detailed operations, see [Adding nodes](https://docs.byteplus.com/en/docs/vke/Adding-nodes). 

3. Cordon existing nodes and change their status to unschedulable. For detailed operations, see [Cordoning nodes](https://docs.byteplus.com/en/docs/vke/Managing-nodes#.5bCB6ZSB6IqC54K5).

4. Take existing nodes offline and evict pods that run on the existing nodes to new nodes. For detailed operations, see [Taking nodes offline](https://docs.byteplus.com/en/docs/vke/Managing-nodes#.5LiL57q_6IqC54K5).

5. After you confirm that your workloads are running as expected, remove the existing nodes. For detailed operations, see [Removing nodes](https://docs.byteplus.com/en/docs/vke/Managing-nodes#.56e76Zmk6IqC54K5).
