---
title: "nvidia-device-plugin"
product: " Vital Kubernetes Engine"
product_code: "vke"
source: "https://docs.byteplus.com/en/docs/vke/nvidia-device-plugin-add-on"
---

nvidia\-device\-plugin‌ is the add\-on that manages NVIDIA GPU resources in VKE clusters. This topic describes the functionality, core resources, and installation and upgrade instructions of this add\-on.

## Add\-on overview

The nvidia\-device\-plugin add\-on manages GPU devices in VKE clusters. It offers NVIDIA device drivers and enables GPU usage in containers.

After the nvidia\-device\-plugin add\-on is installed in the cluster, the system will create the following Kubernetes resources in the kube\-system namespace.

|Resource name |**Resource type** |**Resource description** |
|---|---|---|
|nvidia\-device\-plugin |DaemonSet |The core workload of the add\-on. It is responsible for GPU discovery, registration, and health checks on the node where it is deployed. |
|dcgm\-exporter |DaemonSet |The NVIDIA GPU metric collector. It collects operational states of underlying GPU cards (such as VRAM usage and compute utilization). |

> **tip**

> The preceding table only lists the main resources of the add\-on, as well as resources that may be used when the add\-on or the corresponding feature is configured. This helps you understand the main components of this add\-on. Other resources, such as ConfigMap and Secret, related to the add\-on are not described here. You should refer to the actual resources in the cluster.

## Add\-on versions

For information about the historical release records of the add\-on, as well as new features and optimization descriptions for each version, see [Add-on release records](https://docs.byteplus.com/en/docs/vke/nvidia-device-plugin).

## Install the add\-on

1. Log in to the [VKE console](https://console.byteplus.com/vke).

2. In the left navigation pane, click **Cluster**. Click the target cluster name to go to the management page of this cluster.

3. In the left navigation pane, click **Addons**. On the page that appears, click the **GPU** tab.

4. Move the pointer over the add\-on card, click **Deploy**, and configure the add\-on parameters.

   |Parameter |Description |
   |---|---|
   |Deploy addons |Select whether to install the dcgm\-exporter add\-on for monitoring NVIDIA GPU resources. The add\-on is installed by default.<br><br>> **tip**<br><br><br>> We recommend that you use the default value. If you do not install the dcgm\-exporter, you cannot leverage cloud\-native observability to monitor NVIDIA GPU\-related metrics.<br> |
   |Collection interval |Configure the metric collection interval for the dcgm\-exporter. You can set the metric collection interval based on your timeliness requirement. |
   |Disable XID health check |Select whether to disable the XID health check feature of NVIDIA GPUs. After you disable this feature, the system will no longer automatically isolate abnormal GPU devices based on XID errors.<br><br>> **tip**<br><br><br><br>* > When the nvidia\-device\-plugin add\-on version is v2.2.0 or later, the XID health check feature is disabled by default.<br><br><br>* > When the nvidia\-device\-plugin add\-on version is earlier than v2.2.0, the XID health check feature is enabled by default.<br> |
   |Exporter metrics port |Configure the metric collection port for dcgm\-exporter. The default port is 9400. |
   |Exporter host network |Configure whether dcgm\-exporter uses the node's host network (that is, `hostNetwork` mode).<br><br><br>* Enabled: dcgm\-exporter runs on the hostNetwork and can access metrics locally on the node via `localhost:<collection port>`.<br><br>* Disabled: (Default) dcgm\-exporter runs on the Pod network and cannot directly access metrics on the node via `localhost:<collection port>`.<br><br><br>> **tip**<br><br><br>> Before enabling this feature, ensure that the TCP collection port (for example, 9400) on all target nodes is not occupied. Otherwise, dcgm\-exporter will fail to start due to port conflicts.<br> |
   |Resource configuration |Specify the CPU requests, CPU limits, memory requests, and memory limits of various resources in the add\-on. |

5. Click **Confirm** to finish configuration.

## Upgrading add\-ons

New versions of the add\-on are released at irregular intervals to provide new features or fix known issues. When the add\-on card displays that a new version is available, we recommend upgrading the add\-on promptly. To ensure a smooth service transition, perform the upgrade during off\-peak hours whenever possible. For the upgrade procedure and considerations, see [Upgrading the add-on](https://docs.byteplus.com/en/docs/vke/Upgrading-an-add-on).

## Reset the add\-on

When installing, updating, or upgrading the add\-on, you can click **Reset to default** in the parameter configuration window to reset the parameters on the current page to the default values for this add\-on version. After the reset action, the current configuration that has been filled in or modified but not yet submitted will be overwritten. Confirm that the parameters are correct, then click **Confirm** to submit the configuration.

> **warning**

> After the add\-on configuration is reset, the add\-on parameters revert to the default values for the current version, not the configuration submitted last time, and the current configuration will not be retained. This feature is typically used in scenarios such as configuration anomalies, when original parameters are no longer applicable after an upgrade, or when it is necessary to reconfigure the add\-on using the default parameter values. Before resetting the add\-on configuration, confirm that the current configuration is no longer needed and proceed with caution.

## Related documentation

* [Configuring NVIDIA GPU scheduling](https://docs.byteplus.com/en/docs/vke/NVIDIA-GPU-scheduling)

* [AI resource observability](https://docs.byteplus.com/en/docs/vke/AI-resource-observability)
