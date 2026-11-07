---
title: "How do I view the allocatable resources of a node?"
product: " Vital Kubernetes Engine"
product_code: "vke"
source: "https://docs.byteplus.com/en/docs/vke/How-do-I-query-the-allocatable-resources-of-a-node"
---

VKE allows you to view the allocatable resources of a node, such as CPU, memory, and the number of schedulable pods, by using kubectl or the console.

<span id=".a3ViZWN0bC3mlrnlvI8="></span>
## kubectl


1. Connect to the cluster where the target node is located. For details, see [Connecting to clusters](https://docs.byteplus.com/en/docs/vke/Connecting-to-a-cluster).

2. Run the following command to view the allocatable resources of the node.

   ```bash
   kubectl get node ${your_node_name} -o jsonpath={.status.allocatable}
   ```
   

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">Replace <code>${your_node_name}</code> with your node name. For example, if the node name is <code>172.16.**.**</code>, the complete command is as follows:   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">   ```bash
   kubectl get node 172.16.**.** -o jsonpath={.status.allocatable}
   ```
      </div>
   

   The expected response is as follows.

   ```json
   {"cpu":"32","ephemeral-storage":"123787820Ki","hugepages-1Gi":"0","hugepages-2Mi":"0","memory":"65691932Ki","pods":"110"}
   ```
   


<span id=".5o6n5Yi25Y-w5pa55byP"></span>
## Console


1. Log in to [the VKE console](https://console.byteplus.com/vke) .

2. In the left navigation bar, click **Cluster**.

3. In the cluster list, click the name of the cluster where the target node is located.

4. In the left navigation bar of the cluster management page, click **Workload \> Resource Explorer**.

5. Select **API Group** from the Category drop\-down list. In the API group list, click **core**.

6. On the **core** details page, click **Node** in the **Resource definition** section.

7. In the node list, find the target node (node private IP address) and view the YAML file content.

   The following fields in the YAML file indicate the allocatable resources of the node.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_bf1525ee1f373818e826a2fdd88688ca.png) </span>
