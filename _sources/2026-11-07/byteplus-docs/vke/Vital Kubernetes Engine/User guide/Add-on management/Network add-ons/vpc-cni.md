---
title: "vpc-cni"
product: " Vital Kubernetes Engine"
product_code: "vke"
source: "https://docs.byteplus.com/en/docs/vke/vpc-cni-add-on"
---

vpc\-cni is a high\-performance container network add\-on for VKE clusters. This topic describes how to deploy and use the vpc\-cni add\-on in a cluster.

## Add\-on overview

vpc\-cni is a container network add\-on developed for VKE. It primarily manages elastic network interfaces (ENIs) and container IP addresses in clusters that use the VPC\-CNI network model. For more details, please see [Network overview](https://docs.byteplus.com/en/docs/vke/Container-networks).

After the add\-on is installed in a cluster, the system will create the following Kubernetes resources under the kube\-system namespace.

|Resource name |**Resource type** |**Resource description** |
|---|---|---|
|cello |DaemonSet |The network proxy on nodes. It manages secondary ENIs on nodes and allocates private IP addresses to Pods. |
|cello\-controller |Deployment |The add\-on controller. It coordinates network resources and states globally. |
|cello\-config |ConfigMap |The global add\-on configurations, such as VPC\-CNI networks, security groups, and IP types. |

> **tip**

* > Only clusters that use the VPC\-CNI network model support this add\-on, and the add\-on is required.

* > The preceding table only lists the main resources of the add\-on, as well as resources that may be used when the add\-on or the corresponding feature is configured. This helps you understand the main components of this add\-on. Other resources, such as ConfigMap and Secret, related to the add\-on are not described here. The actual resources in the cluster shall prevail.

## Add\-on versions

For information about the historical release records of the add\-on, as well as new features and optimization descriptions for each version, see [Add-on release records](https://docs.byteplus.com/en/docs/vke/vpc-cni).

## Installing add\-ons

> **tip**

> This add\-on is mandatory for VPC\-CNI clusters. It is automatically installed upon cluster creation. You can configure add\-on parameters by following the steps below.

1. Log in to the [VKE console](https://console.byteplus.com/vke).

2. In the left navigation pane, click **Cluster**. In the right part of the page, click the target cluster name to open the management page of this cluster.

3. In the left navigation pane, click **Addons**. On the page that appears, click the **Network** tab.

4. Move the pointer over the add\-on card and click **Configuration** to configure parameters for the add\-on.

   |Parameter |Description |
   |---|---|
   |Cello resource configuration |Configure the CPU and memory resource requests and limits for the cello container based on your business requirements.<br><br>cello is a container in the pod corresponding to the vpc\-cni add\-on. cello is used to manage auxiliary elastic network interfaces of a node and allocate private IP addresses to pods. The amount of resources required by the cello container is positively correlated to the number of pods. |
   |Cilium resource configuration |Configure the CPU and memory resource requests for the cilium container based on your business requirements.<br><br>cilium is a container in the Pod for the vpc\-cni add\-on. This container provides Service and NetworkPolicy capabilities. The amount of resources required by the cilium container is positively correlated to the number of pods. |
   |Cello IP pooling configuration |Configure the node IP cache pool. The system caches some IP resources on the node by pre\-requesting IP addresses to accelerate Pod creation.<br><br><br>* **idle IP target**: The number of idle, allocatable Pod IP addresses continuously reserved on each node. After Pods consume the idle IP addresses on the node, the add\-on will request and replenish IPs to reach this value to reduce the probability of waiting for IP allocation during Pod creation.<br><br>* **total IP target**: The minimum threshold that triggers the add\-on to submit an IP scale\-out request to the VPC control plane. When the remaining number of idle IP addresses on the node drops to this value, a batch IP request action is triggered. |
   |Istio compatibility mode |Set whether to disable Socket\-level Service load balancing in the container network.<br><br>> **warning**<br><br><br><br>* > You can specify this parameter only for the vpc\-cni add\-on of v1.7.5 and later. You cannot specify this parameter for existing versions. For details, see [Add\-on release notes](https://docs.byteplus.com/en/docs/vke/vpc-cni).<br><br><br>* > You can enable or disable this feature for existing clusters.<br><br><br>* > After you enable or disable this feature, you need to manually restart the pods of the vpc\-cni add\-on for the changes to take effect. Business traffic will be affected during the pod restart process. We recommend performing this operation during low\-traffic hours.<br><br><br>* > You cannot enable this feature for IPv6 clusters.<br> |
   |NetworkPolicy |[[Beta - apply for trial](https://docs.byteplus.com/en/docs/vke/How-do-I-apply-for-beta-features)] Specify whether to enable the NetworkPolicy feature. For details, see [Using NetworkPolicy for network access control](https://docs.byteplus.com/en/docs/vke/Using-NetworkPolicies-for-network-access-control). |
   |Cilium parameter configuration |Configure the scope of pod labels recognized by cilium to reduce performance consumption in the large\-scale cluster. |
   |operator configuration |Configure the cilium operator in the large\-scale cluster to reduce the load on kube\-apiserver.<br><br><br>* **Replicas**: Specify the number of independently deployed operator instances. We recommend configuring three to five replicas. When the value is set to 0, it indicates that the operator instances are not independently deployed.<br><br>* **cilium operator resource configuration**: Adjust the CPU and memory resources of the cilium operator as needed based on the cluster size.<br><br><br>> **tip**<br><br><br>> For a cluster with up to 1,000 nodes and 50,000 pods, we recommend that you configure cilium operator resources as follows:<br><br><br><br>* > CPU request: 0.1 core. Memory request: 128 MiB.<br><br><br>* > CPU limit: 1 core. Memory limit: 8 GiB.<br><br><br><br>> When your cluster exceeds the preceding scale, we recommend that you contact your account manager or [submit a ticket](https://console.byteplus.com/workorder/create?step=2&SubProductID=P00000210) to evaluate the resource configuration.<br> |

5. Click **Confirm** to finish configuration.

## Upgrading add\-ons

The add\-on is released in new versions at irregular intervals to provide new features or fix known bugs. When the add\-on card displays that a new version is available, we recommend upgrading the add\-on promptly. To ensure a smooth business transition, we recommend upgrading the add\-on during business off\-peak hours. For upgrade procedures and considerations, see [Upgrading add-ons](https://docs.byteplus.com/en/docs/vke/Upgrading-an-add-on).

> **warning**

> If the add\-on card still displays **Upgradable** after the update, you can upgrade it again to a higher version. Ensure the last upgrade is completed successfully if you choose to keep upgrading. The following methods can be used to validate the upgrade.

## Check add\-on status

After the add\-on installation/upgrade is complete, confirm whether the add\-on is working normally by using the console or the command\-line tool kubectl.

**Use the console**

1. In the left navigation bar of the Cluster management page, select **Addons**, then enter **Network** tab.

2. Select the vpc\-cni add\-on card and click  **\-\>**  in the upper\-right corner of the card to view the deployment details.

3. Check whether the `cello` DaemonSet in the `kube-system` namespace is in the `Running` state and whether the **Updated** count equals the total number of Pods. If all Pods are in the `Running` state and all Pods are updated, the upgrade is successful.

   ![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_228e5613dadb2d69f6015a3ef0fe1e74.png)

4. Check whether the **Updated** count for the `cello-operator` Deployment in the `kube-system` namespace equals the total number of Pods. If all Pods are updated, the upgrade is successful.

**Use the kubectl CLI**

1. [Connect to the target cluster using kubectl.](https://docs.byteplus.com/en/docs/vke/Connecting-to-a-cluster)

2. Run the following command to check whether the DaemonSet `cello` in the `kube-system` namespace is in the READY state and whether the value of `UP-TO-DATE` equals the total number of pods.

   ```Bash
   kubectl get daemonset cello -n kube-system
   ```

   If all pods are in the `READY` status and the value of `UP-TO-DATE` equals the total number of pods, the upgrade is successful.

   ![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_41001c2701d6574fd6a1738f24e3a3c4.png)

3. Run the following command to check whether the **UP\-TO\-DATE** count of the `cello-operator` Deployment in the `kube-system` namespace equals the total number of Pods.

   ```Bash
   kubectl get deployment cello-operator -n kube-system
   ```

   If the value of `UP-TO-DATE` equals the total number of pods, the upgrade is successful.

   ![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_f78eb941145d6513eebe66be53ac533e.png)

## Related documentation

* [Binding dedicated EIP to pods](https://docs.byteplus.com/en/docs/vke/Associating-an-EIP-with-a-pod)

* [Configuring Static IPs for pods](https://docs.byteplus.com/en/docs/vke/Configuring-a-fixed-IP-address-for-a-pod)

* [Elastic network interface dedicated to a pod with Trunk ENI](https://docs.byteplus.com/en/docs/vke/Using-Trunk-ENI-to-enable-the-exclusive-ENI-mode-for-pods)

* [Access control by NetworkPolicy](https://docs.byteplus.com/en/docs/vke/Using-NetworkPolicies-for-network-access-control)

* [Deploying and running DPDK applications](https://docs.byteplus.com/en/docs/vke/Deploying_and_running_DPDK_applications)
