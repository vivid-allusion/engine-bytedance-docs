---
title: "Accelerating node scale-out by using data volume snapshots"
product: " Vital Kubernetes Engine"
product_code: "vke"
source: "https://docs.byteplus.com/en/docs/vke/Accelerating_node_scale-out_by_using_data_volume_snapshots"
---

You can use volume snapshots to reuse configured node environments and data, which skips node initialization. This shortens the deployment cycle for each node and ensures environment consistency. As a result, node pool scale\-out is greatly accelerated to ensure quick business response. This topic describes how to use data volume snapshots of nodes to accelerate node scale\-out.

<span id="7sOMvFCR"></span>
## Background

During cluster O&M, node pool scale\-out is critical for handling traffic spikes and ensuring service stability. Most of the time is spent in the following stages:


1. The installation and deployment of the node operating system and basic environment require downloading system images and performing configuration initialization on each node. This process is cumbersome and time\-consuming.

2. The installation and configuration of the application software and dependency packages required by the cluster require repeatedly running deployment scripts, which can easily lead to environment inconsistencies.

3. Data initialization requires synchronizing baseline data to new nodes. Traditional methods suffer from low transmission efficiency.


Volume snapshots can effectively address the preceding issues. Their core advantage lies in the ability to quickly reuse configured node environments and data. By pre\-creating snapshots for well\-configured node volumes, you can directly create node volumes by using these snapshots during scale\-out, without the need to repeatedly perform system installation, application deployment, and data synchronization. This skips redundant steps, which significantly shortens the deployment cycle per node. In addition, this ensures the consistency between the environment of new nodes and that of existing nodes, which reduces environment adaptation costs. As a result, the node pool scale\-out is greatly accelerated, and quick business responses are ensured.

<span id="KeiyJ8qE"></span>
## Usage limits


* Only ESSD volumes support snapshot creation.

* You are charged for volume snapshots based on capacity and duration. For details, see [Snapshot billing](https://docs.byteplus.com/en/docs/ecs/Snapshot_billing).


<span id="22ZrC1GG"></span>
## Procedure

<span id="nEURI5ME"></span>
### Step 1: Create a data volume snapshot


1. Log in to the [VKE console](https://console.byteplus.com/vke).

2. In the left navigation bar, click **Cluster**. Click the target cluster name to go to the management page of this cluster.

3. In the left navigation bar of the cluster management page, click **Nodes** \> **Node pool**.

4. Create a node pool or edit an existing node pool. On the node pool configuration page, add a data volume, and select **Format and mount to the container or image directory**.

   <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="1">warning   </div>
   

   <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">When you use a data volume snapshot, the target data volume capacity must be greater than the source data volume capacity at the time the snapshot was created. For example, if you set the data volume capacity to 40 GiB when creating the snapshot, the node data volume capacity must be greater than 40 GiB when you use the snapshot subsequently.   </div>
   

5. After specifying other parameters of the node pool, click **Confirm** to complete the configuration. For the descriptions of other parameters for the node pool, see [Creating managed node pools](https://docs.byteplus.com/en/docs/vke/Creating-a-managed-NodePool).

6. Click the node pool name to go to the node pool details page. Click the **Node list** tab. Find a node newly added to the node pool and click the ID in the **Instance** **ID** column to go to the corresponding ECS details page.

7. In the upper\-right corner of the page, click **Stop**. In the pop\-up dialog box, select **Keep charging** for the **Stop mode** parameter to stop the current ECS instance.

8. Wait for the ECS instance to stop. Then, click the **Volumes** tab of the ECS details page. Find the corresponding data volume, and click **Create snapshot** in the **Actions** column.

9. Specify the parameters of the snapshot, such as Snapshot name and Retention time, and then click **Create snapshot** to create the snapshot. For more snapshot configuration methods and parameter descriptions, see [Creating snapshots](https://docs.byteplus.com/en/docs/ecs/Create-a-snapshot).

10. In the left navigation bar, click **Storage** \> **Snapshots**. You can view the creation progress of the current snapshot in the snapshot list.


<span id="mC119dLm"></span>
### Step 2: Modify configurations for pulling cluster images


1. Log in to the [VKE console](https://console.byteplus.com/vke).

2. In the left navigation bar, click **Cluster**. Click the target cluster name to go to the management page of this cluster.

3. In the left navigation bar, click **Overview**.

4. Click the **Control plane parameter configuration** tab. Unselect **AlwaysPullImages** to prevent images from being forcibly pulled again when you create Pods in the cluster, which affects acceleration.


<span id="tPJ1WXyN"></span>
### Step 3: Use the snapshot to accelerate node scale\-out


1. In the left navigation bar of the cluster management page, click **Nodes** \> **Node pool**.

2. Create a node pool or edit an existing node pool. On the node pool configuration page, add a data volume, click **Use snapshots to create EBS**, and then select the created snapshot.

3. After specifying other parameters of the node pool, click **Confirm** to complete the configuration.


<span id="j7Hp8qWk"></span>
### Step 4: Enable the retention of the containerd directory

Call the [UpdateNodePoolConfig ](https://docs.byteplus.com/en/docs/vke/UpdateNodePoolConfig)API to update the PreScript configuration of the node pool.

```Bash
sed -i 's/^KEEP_CONTAINERD_DIRECTORY=.*/KEEP_CONTAINERD_DIRECTORY=true/' /root/deploy-pkg/user-data-config.sh
```


<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">When you use the <a href="https://docs.byteplus.com/en/docs/vke/UpdateNodePoolConfig">UpdateNodePoolConfig</a> API, the script content needs to be Base64 encoded before being passed in. The Base64\-encoded value of the preceding script is <code>c2VkIC1pICdzL15LRUVQX0NPTlRBSU5FUkRfRElSRUNUT1JZPS4qL0tFRVBfQ09OVEFJTkVSRF9ESVJFQ1RPUlk9dHJ1ZS8nIC9yb290L2RlcGxveS1wa2cvdXNlci1kYXRhLWNvbmZpZy5zaA==</code>.</div>


<span id="oKDlm4ND"></span>
## Validating results

After the configuration is complete, scale out the node pool. This reduces the time spent pulling system images during scale\-out and shortens the overall scale\-out duration.
