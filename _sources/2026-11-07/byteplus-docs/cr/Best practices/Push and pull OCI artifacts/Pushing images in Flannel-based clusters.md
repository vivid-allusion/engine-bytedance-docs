---
title: "Pushing images in Flannel-based clusters"
product: "Container Registry"
product_code: "cr"
source: "https://docs.byteplus.com/en/docs/cr/push-images-in-the-flannel-network-cluster"
---

This topic describes how to fix image push failures in Flannel\-based clusters under high\-concurrency traffic.

## Background

### Problem scenario

In clusters using the Flannel network model, image pushes may fail under high\-concurrency traffic. Excessive concurrent traffic may cause TCP `ack` packets to exceed the window limit. This causes the ECS protocol stack to return `reset` packets. These packets interrupt the push stream and cause image push failures. For example, image pushes may fail when Kaniko is used in a Flannel\-based cluster.

### Solutions

This issue can be resolved by adjusting kernel parameters on physical nodes. On the client ECS, set `/proc/sys/net/netfilter/nf_conntrack_tcp_be_liberal` to 1. This setting allows TCP `ack` packets to exceed the window limit under heavy concurrent traffic. It prevents push interruptions caused by `reset` packets returned by the ECS protocol stack. Adjusting the `/proc/sys/net/netfilter/nf_conntrack_tcp_be_liberal` parameter does not affect business operations.

* Solution 1: Create a DaemonSet to modify node parameters. It changes kernel parameters on all cluster nodes at once. It is suitable for large clusters that scale frequently. No manual maintenance is needed after node pool scaling.

* Solution 2: Modify node parameters through node pool settings. This solution takes effect only on newly added nodes. For existing nodes, log in to the node. Then run `sysctl -w net.netfilter.nf_conntrack_tcp_be_liberal=1`.

* Solution 3: [[Beta - apply for trial](https://docs.byteplus.com/en/docs/vke/How-do-I-apply-for-beta-features)] Use a custom image to deploy the operating system on nodes. In a node pool, this change affects all **future nodes**. Existing nodes must be updated on each target node.

> **tip**

> The VPC\-CNI network model can effectively avoid these image push failures. To use VPC\-CNI, **recreate** the container cluster. For **Network model**, select `VPC-CNI`. For information about how to create a cluster, see [Creating managed clusters](https://docs.byteplus.com/en/docs/vke/Creating-a-cluster).

## Procedure

### Solution 1: Create a DaemonSet to modify node parameters

> **tip**

> This solution changes kernel parameters on all cluster nodes at once. It is suitable for large clusters that scale frequently. No manual maintenance is needed after node pool scaling.

Use a DaemonSet to deploy privileged Pods to the target cluster and modify kernel parameters on all cluster nodes.

1. Log in to the [VKE console](https://console.byteplus.com/vke).

2. In the target cluster, select **Workload** \> **DaemonSet**.

3. Create a DaemonSet by using YAML. The sample code is as follows.

   ```yaml
   apiVersion: apps/v1
   kind: DaemonSet
   metadata:
     name: sysctl-conf
     namespace: kube-system
   spec:
     selector:
       matchLabels:
         name: sysctl-conf
     template:
       metadata:
         labels:
           name: sysctl-conf
       spec:
         hostPID: true
         hostIPC: true
         hostNetwork: true
         containers:
         - name: sysctl
           image: busybox
           securityContext:
             privileged: true
           command: ["/bin/sh"]
           args: ["-c", "sysctl -w net.netfilter.nf_conntrack_tcp_be_liberal=1 && sleep 86400"]
   ```

4. Check whether `/proc/sys/net/netfilter/nf_conntrack_tcp_be_liberal` on ECS has been changed to `1`.

   ```shell
   cat /proc/sys/net/netfilter/nf_conntrack_tcp_be_liberal
   ```

### Solution 2: Modify node parameters through node pool settings

> **tip**

* > This solution takes effect only on newly added nodes.

* > For existing nodes, log in to the node. Then run `sysctl -w net.netfilter.nf_conntrack_tcp_be_liberal=1`.

Use the console to manage node pool execution scripts and adjust the target kernel parameter for newly added nodes.

1. Log in to the [VKE console](https://console.byteplus.com/vke).

2. In the target cluster, select **Nodes** \> **Node pool**.

3. Click **Edit** in the **Actions** column of the target node pool.

4. Under "Advanced settings", set the deployment script. A sample script is shown below.

   ```shell
   sysctl -w net.netfilter.nf_conntrack_tcp_be_liberal=1
   ```

5. Click **Confirm** to finish the configuration.

### Solution 3: Use a custom image to deploy the operating system on nodes

> **tip**

> [[**Beta \- apply for trial**](https://docs.byteplus.com/en/docs/vke/How-do-I-apply-for-beta-features)] VKE supports custom images as node operating systems. For details, see [Description of custom images](https://docs.byteplus.com/en/docs/vke/Overview-of-operating-system-images#yvu3XMsY).

Use a custom image in VKE to deploy an operating system with `/proc/sys/net/netfilter/nf_conntrack_tcp_be_liberal` set to `1`.

* Parameter changes for **new nodes** in a node pool: Use a custom image in the node pool to deploy the operating system. For more information, see [How to package and use custom images?](https://docs.byteplus.com/en/docs/vke/Overview-of-operating-system-images) and [Managing node pools](https://docs.byteplus.com/en/docs/vke/Managing-NodePools).

* Parameter changes for **existing nodes** in a node pool: Use a custom image on the nodes to deploy the operating system. For more information, see [How to package and use custom images?](https://docs.byteplus.com/en/docs/vke/Overview-of-operating-system-images)
