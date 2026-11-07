---
title: "Enabling API Server private domain access for existing clusters"
product: " Vital Kubernetes Engine"
product_code: "vke"
source: "https://docs.byteplus.com/en/docs/vke/Enabling_API_Server_private_domain_access_for_existing_clusters"
---

This topic describes how to enable API Server private domain access for existing VKE\-managed clusters created before May 15, 2026, and adjust configurations for existing components and nodes accordingly.

## Background

For VKE\-managed clusters created **on or after May 15, 2026**, access to the control plane (API Server) by node\-side components will be gradually migrated from CLB VIP access to internal domain\-based access to enhance cluster control\-plane performance and stability. For details, see [Product announcement](https://docs.byteplus.com/en/docs/vke/Product_announcement_Announcing_API_Server_connectivity_path_switch_for_managed_VKE_clusters).

You can also choose to manually enable API Server private domain access for existing clusters created before this date. If you enable this access method, node\-side components (such as kubelet, kube\-proxy, and vpc\-cni) will switch API Server access from the CLB VIP approach to the direct access mode, where the private domain name is dynamically resolved to the API Server ENI. This improves the performance and stability of node\-side components' access to the API Server.

## Usage instructions

* API Server private domain access applies only to VKE\-managed clusters.

* The following clusters have API Server private domain access enabled by default:

   * VKE\-managed clusters created on or after **May 15, 2026**.

   * You can check whether a cluster has API Server private domain access enabled by calling the [ListClusters](https://docs.byteplus.com/en/docs/vke/ListClusters?lang=en) API. If the `KubernetesConfig.AdvancedConfig.InternalDnsEnabled` parameter in the response is `true`, private domain access is enabled.

## Pre\-checks

Before you begin, be sure to complete the following checks. Otherwise, nodes will fail to connect to the API Server.

1. Check security group configurations.

   * When the direct connection mode is enabled, traffic is directly sent to the ENI of the API Server. Therefore, ensure that the security group rules associated with the ENI allow direct connections.

   * Confirm that security groups for the nodes and ENIs allow ‌outbound traffic on port 6443.

2. Check DNS resolution configurations.

   API Server domain name resolution relies on the default private DNS servers (`100.96.0.2` and `100.96.0.3`) within the VPC.

   * Default DNS configuration: If nodes use the default DNS configuration, no additional operation is required.

   * Custom DNS configuration: If you have configured a custom DNS server on nodes or containers, ensure the DNS server forwards requests for `*.ibytepluses.com` or API Server domain names to the VPC's default private DNS servers for resolution.

## Procedure

### **Step 1:**  Enable API Server private domain resolution

1. Call the [UpdateClusterConfig](https://docs.byteplus.com/en/docs/vke/UpdateClusterConfig?lang=en) API to create an internal network resolution record within the VPC of the cluster.

   The following is an example of the request body:

   ```JSON
   {
       "KubernetesConfig": {
           "AdvancedConfig": {
               "InternalDnsEnabled": true
           }
       }
   }
   ```

2. During the update process, the API Server will restart automatically. You can check the status in the **Cluster jobs** module of the cluster management page in the [VKE console](https://console.byteplus.com/vke).

3. After the job is complete, call the [ListClusters](https://docs.byteplus.com/en/docs/vke/ListClusters?lang=en) API and check the response for the value of the `KubernetesConfig.AdvancedConfig.InternalDnsEnabled` parameter. If the value is `true`, the configuration has taken effect.

### Step 2: Verify the effectiveness of the private domain name

Before modifying the configuration of existing nodes, first verify that domain name resolution takes effect for new resources by creating new nodes or Pods.

**Verify ECS nodes**

1. Add a new node to the cluster. The kubelet on the new node automatically uses the private domain name. For node scale\-out details, see [Adding nodes](https://docs.byteplus.com/en/docs/vke/Adding-nodes).

2. After the node is ready, log in to the node via the [ECS Terminal](https://docs.byteplus.com/en/docs/vke/Managing-nodes?lang=zh#ecs-terminal) and run the following command to check whether the server address in the kubelet configuration file is the private domain name.

   ```Shell
   cat /etc/kubernetes/kubelet.conf
   ```

**Verify VCI Pods**

After private domain access is enabled, newly created VCI Pods communicate with the API Server via the private domain name by default.

Add a VCI Pod to the cluster and confirm that the VCI Pod can enter the Ready state normally. For details, see [Creating VCIs](https://docs.byteplus.com/en/docs/vke/Creating-an-instance).

### **Step 3: Recreate Pods for key components in the existing cluster** to apply the new configuration

**Flannel cluster**

In the Flannel cluster, recreate the existing kube\-proxy Pods to apply the new configuration.

> **warning**

> To ensure business stability, delete Pods in batches in the test or development environment first and verify that the Pods are recreated before deleting Pods in the production environment.

After the API Server domain name takes effect, VKE automatically switches the kube\-proxy connection configuration from the IP address to this domain name. You need to recreate its existing Pods to load the new configuration.

1. Log in to the [VKE console](https://console.byteplus.com/vke).

2. On the **Cluster** page, click the name of the target Flannel cluster.

3. In the left navigation pane of the cluster management page, click **Configurations \> ConfigMap**.

4. Select the **kube\-system** namespace and check whether `kubeconfig.conf` in the kube\-proxy configuration is effective.

   ![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_4fb28a2be903a13b656e5271a4ba2ea5.png)

5. Delete the Pods in the kube\-proxy DaemonSet to recreate them and load the new configuration.

   **Method 1**

   Delete existing kube\-proxy Pods manually through the console. The Pods will be recreated and load the new configuration.

   1. In the left navigation pane, click **Workload \> DaemonSet**.

   2. Select the **kube\-system** namespace, find the **kube\-proxy** DaemonSet, and click the name of the DaemonSet.

   3. On the **List of instances** page of the kube\-proxy details page, delete the Pods one by one to recreate them and load the new configuration.

   **Method 2**

   Alternatively, perform a rolling update on the kube\-proxy DaemonSet via kubectl to apply the new configuration to all kube\-proxy Pods.

   1. Connect to the target cluster using kubectl. For details, see [Connecting to clusters via kubectl](https://docs.byteplus.com/en/docs/vke/Connecting_to_clusters).

   2. Run the following command to perform a rolling update on the kube\-proxy DaemonSet.

      ```Bash
      kubectl rollout restart daemonset kube-proxy -n kube-system
      ```

   3. Run the following command to view the result of the rolling update.

      ```Bash
      kubectl rollout status daemonset kube-proxy -n kube-system
      ```

      The expected response is as follows:

      ```Bash
      daemonset "kube-proxy" successfully rolled out
      ```

**VCP-CNI cluster**

In the VPC\-CNI cluster, update vpc\-cni to ensure the new configuration takes effect for existing components.

> **warning**

> To ensure business stability, we recommend performing this operation during off\-peak hours.

1. Log in to the [VKE console](https://console.byteplus.com/vke).

2. On the **Cluster** page, click the name of the target VPC\-CNI cluster.

3. In the left navigation pane of the cluster management page, click **Addons**. Find vpc\-cni and click **Configuration**.

4. In the **vpc\-cni Parameter configuration** dialog box, update the parameters as needed or keep the current configuration, then click **Confirm** to trigger a configuration update.

5. In the left navigation pane, click **Workload \> DaemonSet**. Locate the **cello** DaemonSet in the **kube\-system** namespace, and in the right **Actions** column, click `...` \> **Edit Yaml** to check whether the domain name exists in the cello environment variables.

   ![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_63e2a1c635aef0f592e4c64502d15a63.png)

6. Confirm that the rolling update of the cello DaemonSet is completed.

   ```Bash
   kubectl rollout status daemonset/cello -n kube-system
   ```

   The expected response is as follows:

   ```Bash
   daemonset "cello" successfully rolled out
   ```

### Step 4: Modify the kubelet configurations of existing nodes

Update the kubelet configurations of existing nodes and restart the service to complete the switch to private domain\-based access. To ensure cluster stability, this section covers two procedures: single\-node verification and batch O&M.

1. Perform single\-node verification.

   1. Log in to an existing node using the [ECS Terminal](https://docs.byteplus.com/en/docs/vke/Managing-nodes?lang=en#ecs-terminal), run the following command to switch the API Server address from its IP to its domain name, and then restart kubelet.

      ```Bash
      # The following single-line command replaces the configuration and restarts the service.
      sed -i.bak 's#https://{clb-ip}:6443#https://{cluster-id}.vke.{region-id}.ibytepluses.com:6443#g' /etc/kubernetes/kubelet.conf && \ 
      systemctl restart kubelet && \
      systemctl status kubelet 
      ```

      The following table describes the variables in the command:

      |Variable |Description |
      |---|---|
      |{clb\-ip} |The CLB IP address specified in the `/etc/kubernetes/kubelet.conf` configuration of the node.<br><br>Run the `cat /etc/kubernetes/kubelet.conf` command on the node to view the CLB IP address in the `server` parameter.<br><br>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_713b84dcdef7ee2caec8e466a914fb80.png) |
      |{cluster\-id} |Cluster ID. You can obtain it on the **Overview** page of the cluster. |
      |{region\-id} |Region ID. To obtain the ID (RegionId) of a specific region, see [Service addresses](https://docs.byteplus.com/en/docs/vke/Service_addresses). |

      The complete example is as follows:

      ```Bash
      sed -i.bak 's#https://10.**.**.**:6443#https://cd6ptisscv4o*********.vke.cn-beijing.ibytepluses.com:6443#g' /etc/kubernetes/kubelet.conf && \ 
      systemctl restart kubelet && \
      systemctl status kubelet 
      ```

   2. In the [VKE console](https://console.byteplus.com/vke), go to **Nodes** \> **Node** to verify that the node is in the **Running** state.

2. After single\-node verification is successful, use the [Cloud Assistant](https://console.byteplus.com/ecs/region:ecs+cn-beijing/invocations) feature in the ECS console to operate on the remaining existing nodes in batches.

   You need to create a job on the Cloud Assistant page. Configure some parameters as described in the following table. For other steps and parameters, see [Creating jobs](https://docs.byteplus.com/en/docs/ecs/Creating-a-job).

   |Parameter |Description |
   |---|---|
   |**Command** ||
   |Command source |Select **Manual input**. |
   |Command type |Select **Linux Shell** and enter the following code.<br><br>```Bash```<br>```# Enter the following parameters in the command content.```<br>```sed -i.bak 's#https://{clb-ip}:6443#https://{cluster-id}.vke.{region-id}.ibytepluses.com:6443#g' /etc/kubernetes/kubelet.conf && systemctl restart kubelet```<br> |
   |Object |Select the ECS instance corresponding to the node in the VKE cluster.<br><br>You can obtain the **Instance ID** corresponding to the node from **Nodes** \> **Node** in the [VKE console](https://console.byteplus.com/vke). |

   Wait for the job to complete. After confirming that the node status is normal, repeat this operation until all existing nodes have been updated.
