---
title: "Enhancing container resource visibility"
product: " Vital Kubernetes Engine"
product_code: "vke"
source: "https://docs.byteplus.com/en/docs/vke/Enhanced_visibility_of_container_resources"
---

VKE provides container resource view features at the kernel level to enhance the visibility of container resources. This topic provides a detailed introduction to the background and usage of enhanced container resource visibility.

<span id=".5Zy65pmv5LuL57uN"></span>
## Scenario introduction

By default, the container resource view feature is disabled. This means that CPU, memory, and other resource information for a container comes from the host (ECS instance) instead of the actual resource view of the container. This scenario aims to enhance container resource visibility by enabling the container resource view feature. The container resource view feature ensures that when using commands like top or free in the container to read interface data, you directly obtain container\-specific resource information (not the resource information of the host).

The description of files and resource information supported by enhanced container resource visibility is as follows.


|**File** |**Description** |<div style="text-align: center"><br><strong>Supported</strong></div><br> |
|---|---|---|
|/proc/cpuinfo |Obtains CPU\-related information, such as the processor model and name, number of cores, number of threads, CPU frequency, cache size, and supported instruction sets. |<div style="text-align: center"><br>✔️</div><br> |
|/proc/meminfo |Obtains memory\-related information, such as the total memory, used memory, free memory, cached memory, and swap space usage. |<div style="text-align: center"><br>✔️</div><br> |
|/proc/stat |Obtains system statistics, including: user time, system time, idle time, and other CPU usage information for each CPU core; process statistics such as process creation, exit, and running time; system activity data such as system startup time, running time, and number of interrupts.  Obtains system statistics, including CPU usage (such as user time, system time, and idle time) for each CPU core, process statistics (such as creation, exit, and runtime), and system activity (such as boot time, uptime, and number of interruptions). |<div style="text-align: center"><br>✔️</div><br> |
|/proc/uptime |Provides system uptime information, including current system time, system uptime, number of currently logged\-in users, and  average system load over the past 1, 5, and 15 minutes. |<div style="text-align: center"><br>✔️</div><br> |
|/sys/devices/system/cpu/online |Displays online CPU cores. Each CPU core has a corresponding entry indicating whether the core is online. |<div style="text-align: center"><br>✔️</div><br> |


<span id=".6IOM5pmv5L-h5oGv"></span>
## Background information

Container technology provides an environment isolation method that is different from traditional virtual machine technology. While Linux containers accelerate container packaging and startup, they also reduce the isolation level, with resource view isolation in Linux containers being a typical example of this issue.

Containers can limit resource usage (such as CPU and memory) via cgroups. However, note that when a process inside a container uses common commands like free or top to query monitoring data, it only retrieves physical server (host) metrics. It does not retrieve the actual resource usage of containers. This happens because containers do not isolate resource views for file systems like `/proc` and `/sys`.

From the perspective of applications, the runtime environment for processes in a container differs from that on a physical machine or virtual machine. Some applications encounter issues when running in containers. For example, in NGINX worker_processes auto configuration, programs that need host CPU information typically auto\-detect the number of CPUs in their environment. But if a containerized process reads `/proc/cpuinfo`, it returns the total CPU cores of the host. This issue affects the running state of the service inside the container.

<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites

VKE has been activated and a compliant cluster has been created. For specific requirements, see the "Limits" section of this topic. For more information about creating clusters, see [Creating clusters](https://docs.byteplus.com/en/docs/vke/Creating-a-cluster).

<span id=".5L2_55So6ZmQ5Yi2"></span>
## Limits


* Enhanced container resource visibility is not supported for existing nodes and existing pods in a node pool. We recommend that you create a new node pool to benefit from this feature.

* The container resource visibility enhancement feature depends on the cluster version, operating system image of nodes, and image version. The following table provides details of resource dependencies.

   
   |**Dependent resource** |**Dependency details** |
   |---|---|
   |Kubernetes |You can find the current version of Kubernetes in the basic information section of the cluster details page in the VKE console. For details, see [How can I find the Kubernetes version of a cluster?](https://docs.byteplus.com/en/docs/vke/How-do-I-view-the-Kubernetes-version-of-a-cluster)<br><br><br>* v1.28 for v1.28.3\-vke.6 and later.<br><br>* v1.26 for v1.26.10\-vke.12 and later.<br><br>* v1.24 for v1.24.15\-vke.28 and later. |
   |Node image |* **velinux 1.0**: 5.4.250\-2\-velinux1u3\-amd64 or later.<br><br>* **velinux 1.0 CentOS\-compatible version**: 5.4.250\-2.3.ve1.x86_64 or later.<br><br>* **velinux 1.0 with 5.10 kernel**: 5.10.135\-6\-velinux1u1\-amd64 or later.<br><br>* **velinux 1.0 CentOS\-compatible version with 5.10 kernel**: 5.10.135\-6.1.ve1.x86_64 or later. |
   


<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure

<span id=".5q2l6aqk5LiA77ya5Yib5bu66IqC54K55rGg5bm25byA5ZCv5a655Zmo6LWE5rqQ5Y-v6KeB5oCn5aKe5by6"></span>
### Step 1: Create a node pool and enable enhanced container resource visibility

In the [VKE console](https://console.byteplus.com/vke), create a new node pool on the node pool page. Note that in the Advanced configuration section, enter the following command in the **InitializeScript** field to enable the container resource visibility enhancement feature: `sysctl -w kernel.cgroup_override_proc=1 >> /etc/sysctl.conf`. Other parameters can be configured as needed. For details, see [Creating node pools](https://docs.byteplus.com/en/docs/vke/Creating-a-NodePool).

<span id=".5q2l6aqk5LqM77ya5Yib5bu6LXBvZC3lubblvIDlkK_lrrnlmajotYTmupDlj6_op4HmgKflop7lvLo="></span>
### Step 2: Create a pod and enable enhanced container resource visibility

On the Workload page of the [VKE console](https://console.byteplus.com/vke), create a new workload (a Deployment in this example). Note that in the **Advanced settings** step, add the instance annotation `vke.volcengine.com/host-resource-view: false`. Other parameters can be configured as needed. For details, see [Creating Deployments](https://docs.byteplus.com/en/docs/vke/Creating-a-Deployment).

<span id=".57uT5p6c6aqM6K-B"></span>
## Validating results

You can verify the result by comparing the resource information before and after enabling the enhanced container resource visibility feature. In this scenario, a Docker application has been deployed on a Linux host, and a container with a memory size of 1 GiB has been created.


* If enhanced container resource visibility is not enabled, running the `free -m` command in the container will return the resource information of the host (where the container resides), as shown in the figure below.


<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_80eb4334461c30034ca007d558ca3a9a.png) </span>


* If enhanced container resource visibility is enabled, running the `free -m` command in the container will return the actual resource information of the container, as shown in the figure below.


<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_93b2472d8a222eec9026a6082be4b3e6.png) </span>

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">Enhanced container resource visibility can meet regular requirements. However, note that this feature does not support the following special scenarios.</div>


<div data-tips="true" data-tips-type="warning">If the PID 1 process in the container is systemd, the monitoring data collection task may reside in a sub\-cgroup of the container (instead of the root cgroup). This results in incorrectly collected data.</div>


<div data-tips="true" data-tips-type="warning">For example, when you log in to the container via SSH and run the <code>cat /proc/cpuinfo</code> command, the session process actually resides in the sub\-cgroup created by systemd, and the result displayed will be incorrect.</div>
