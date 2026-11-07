---
title: "Why cannot I delete a cluster that fails to be created?"
product: " Vital Kubernetes Engine"
product_code: "vke"
source: "https://docs.byteplus.com/en/docs/vke/Why-cannot-I-delete-a-cluster-that-failed-to-be-created"
---

<span id=".6Zeu6aKY5o-P6L-w"></span>
### Issue description

After you try to **delete** a cluster that fails to be created, the system displays **Deleting** or **Deletion failed** in the Status column that corresponds to the cluster.

<span id=".6Kej5Yaz5pa55rOV"></span>
### Solution


1. Delete the cluster again

   * If the cluster is in the Deletion failed state, click ... \> Delete in the Actions column to try to delete the cluster again.

   * If the cluster is in the Deleting state, refresh the page multiple times and check whether the cluster remains in the **Deleting** status.

2. If you still cannot delete the cluster after multiple attempts, record information about the cluster, such as the cluster name and cluster ID. [Submit a ticket](https://console.byteplus.com/ticket/createTicketV2/?step=2&Service=vke) to obtain technical support.
