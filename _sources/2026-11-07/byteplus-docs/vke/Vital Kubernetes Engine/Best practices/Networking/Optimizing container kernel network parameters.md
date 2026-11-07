---
title: "Optimizing container kernel network parameters"
product: " Vital Kubernetes Engine"
product_code: "vke"
source: "https://docs.byteplus.com/en/docs/vke/Optimizing_container_kernel_network_parameters"
---

VKE has optimized and adjusted node network parameters to meet the requirements of most scenarios. If the default kernel parameters do not suit your workload, you can further customize node or pod network configurations.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>



* <div data-tips="true" data-tips-type="warning">Kernel parameter adjustments must be driven by actual requirements. Conduct thorough testing and small\-scale validation in a test environment before deciding whether to make changes in the production environment. Never modify kernel parameters without testing. Improper changes or insufficient testing may cause cluster failures or business losses.</div>


* <div data-tips="true" data-tips-type="warning">‌Never modify parameters without understanding their purpose‌. Note that kernel parameters may vary across cluster types or versions.</div>


* <div data-tips="true" data-tips-type="warning">Modifying node system parameters carries risks. Conduct comprehensive evaluation or testing and make changes during off\-peak hours.</div>



In container environments, non\-HostNetwork pods run in isolated network namespaces. Therefore, kernel parameters are categorized as **Node\-level network parameters** and **Pod\-level network parameters**. This topic describes how to modify the kernel network parameters for nodes and pods.

<span id=".5L-u5pS56IqC54K5572R57uc5YaF5qC45Y-C5pWw"></span>
## Modifying node kernel network parameters

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">This configuration method only supports modifying kernel parameters for newly added nodes. Supported nodes include those added to a new node pool upon creation, or to an existing node pool after its configuration is modified.</div>


* <div data-tips="true" data-tips-type="tip">To modify kernel parameters of existing nodes, you can use the <strong>cloud assistant</strong> provided by ECS. For details, see <a href="https://docs.byteplus.com/en/docs/ecs/Overview-of-cloud-assistant">Cloud assistant overview</a>. Before you begin, ensure that all nodes have the cloud assistant client installed.</div>



When you create or modify a node pool, you can configure the kernel network parameters of new nodes added to the node pool by using the startup script of the node pool. This topic uses the node pool creation process as an example.


1. Log in to the [VKE console](https://console.byteplus.com/vke).

2. In the left navigation bar of VKE console, click **Cluster**. Click the name of the target cluster to go to the cluster management page.

3. In the left navigation bar of the cluster management page, click **Nodes** \> **Node pool**.

4. Click **Create node pool**. In the **Advanced settings** section, enter the script for modifying network parameters in the **InitializeScript** text box.


The following script provides an example:

```shell
#!/bin/bash

echo "kernel_parameter1 = value1" >> /etc/sysctl.conf
echo "kernel_parameter2 = value2" >> /etc/sysctl.conf
echo "kernel_parameter3 = value3" >> /etc/sysctl.conf

sysctl -p

echo "end"
```


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">In the above example, <code>kernel_parameter1</code> represents the kernel parameter name, and <code>value1</code> represents the kernel parameter value. For details on specific kernel parameters, see <a href="https://docs.byteplus.com/en/docs/vke/Optimizing_container_kernel_network_parameters#.572R57uc5YaF5qC45Y-C5pWw6K-05piO">Kernel network parameters</a>.</div>


<span id=".5L-u5pS5LXBvZC3nvZHnu5zlhoXmoLjlj4LmlbA="></span>
## Modifying pod kernel network parameters

<span id=".5pa55byP5LiA77ya6YCa6L-HLWluaXRjb250YWluZXIt6YWN572u"></span>
### Method 1: Using initContainer

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">This method does not apply to VCI scenarios.</div>


When creating a workload or pod, you can define pod network kernel parameters by adding an `initContainer` configuration. The following is an example:

```yaml
apiVersion: v1
kind: Pod
metadata:
  name: sysctl-example-init
spec:
  initContainers:
  - image: busybox
    command:
    - sh
    - -c
    - |
      sysctl -w kernel_parameter1 = value1
    imagePullPolicy: Always
    name: netsysctl
    securityContext:
      privileged: true
  containers:
  ...
```


<span id=".5pa55byP5LqMLe-8mumAmui_hy1zZWN1cml0eWNvbnRleHQt6YWN572u"></span>
### Method 2: using SecurityContext

In Kubernetes, you can configure a pod's kernel parameters via its sysctl security context. For details, see the [official documentation](https://kubernetes.io/docs/tasks/administer-cluster/sysctl-cluster).

Kubernetes categorizes sysctl parameters as either **safe** or **unsafe**. **safe** sysctl parameters can be configured directly. The following parameters are safe:


* `net.ipv4.ip_local_port_range`

* `net.ipv4.tcp_syncookies`

* `net.ipv4.ping_group_range` (since Kubernetes 1.18)

* `net.ipv4.ip_unprivileged_port_start` (since Kubernetes 1.22)

* `net.ipv4.ip_local_reserved_ports` (since Kubernetes 1.27, needs kernel 3.16+)

* `net.ipv4.tcp_keepalive_time` (since Kubernetes 1.29, needs kernel 4.5+)

* `net.ipv4.tcp_fin_timeout` (since Kubernetes 1.29, needs kernel 4.6+)

* `net.ipv4.tcp_keepalive_intvl` (since Kubernetes 1.29, needs kernel 4.5+)

* `net.ipv4.tcp_keepalive_probes` (since Kubernetes 1.29, needs kernel 4.5+)


Except the parameters mentioned above, all other parameters are **unsafe** sysctl parameters and are disabled by default.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">To configure <strong>unsafe</strong> sysctl parameters, the cluster administrator must manually enable them on each node. If these parameters are not enabled, pods configured with unsafe sysctl parameters will still be scheduled but cannot start normally.</div>


To enable **unsafe** sysctl parameters, execute the following kubelet command on each node.

```bash
kubelet --allowed-unsafe-sysctls \
  'kernel.msg*,net.core.somaxconn' ...
```


After enabling **unsafe** sysctl parameters on a node, you can modify the pod kernel network parameters by using the following configuration.

```yaml
apiVersion: v1
kind: Pod
metadata:
  name: sysctl-example
spec:
  securityContext:
    sysctls:
    - name: net.ipv4.tcp_keepalive_time
      value: "60"
  ...
```


<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">The Kubernetes SecurityContext supports a limited number of parameters. Take note of the following information:</div>



* <div data-tips="true" data-tips-type="warning">Pay attention to the Kubernetes version and kernel version supported by the SecurityContext.</div>


* <div data-tips="true" data-tips-type="warning">When configuring kernel network parameters for pods, first confirm whether they can be configured via the SecurityContext method. If yes, use this method. Otherwise, consider using the initContainer method.</div>


* <div data-tips="true" data-tips-type="warning">In VCI scenarios, most network parameters (except <code>net.ipv4.ip_local_port_range</code> and <code>net.ipv4.tcp_syncookies</code>) are supported by the SecurityContext. For details, see <a href="https://docs.byteplus.com/en/docs/vke/Configuring-a-security-context">Configuring SecurityContext</a>.</div>



<span id=".572R57uc5YaF5qC45Y-C5pWw6K-05piO"></span>
## Kernel network parameters

The following table describes common kernel network parameters.


|Parameters |Scopes |Descriptions |Recommendation |
|---|---|---|---|
|net.core.netdev_max_backlog |Node level |Sets the maximum length of the receive queue for each network interface. When a network interface receives packets, these packets are first placed in the receive queue to wait for soft interrupt processing. If the receive queue is full, new packets will be dropped. |When the host processing performance is relatively insufficient, this value can be appropriately increased. |
|net.core.optmem_max |Node level |Sets the default maximum socket buffer size (in bytes) for all sockets in the system.<br><br>This parameter affects socket buffer optimization. When a new socket is created, the system allocates memory as the socket buffer. This parameter limits the maximum size of the buffer to prevent unnecessary memory usage. |The parameter value can be appropriately increased as needed to improve the size of the socket buffer.<br><br>The default value for VKE clusters is 20480. |
|net.ipv4.neigh.default.gc_stale_time<br><br>net.ipv4.neigh.default.gc_thresh1<br><br>net.ipv4.neigh.default.gc_thresh2<br><br>net.ipv4.neigh.default.gc_thresh3 |Node level |* gc_stale_time sets the expiration time for ARP cache entries (neighbor cache entries).<br><br>* gc_thresh1 sets the minimum number of retainable cache entries. If entries are below this value, the Garbage Collector (GC) does not run. This parameter defaults to 128.<br><br>* gc_thresh2 indicates that when the number of entries exceeds this value, GC will clear entries older than 5 seconds. The default value is 512.<br><br>* gc_thresh3 indicates the maximum number of allowed non\-permanent entries. If the system has a large number of incoming connections or directly connected devices, this value should be increased. The default value is 1024. |These kernel parameters set the reclamation and threshold of node\-level ARP table entries. In VKE clusters that use the VPC\-CNI network model, traffic access depends on the system ARP table.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">The VKE cluster has already optimized the kernel parameters, and the default values are as follows:</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">gc_thresh1: 10240</div><br><br><br>* <div data-tips="true" data-tips-type="tip">gc_thresh2: 20480</div><br><br><br>* <div data-tips="true" data-tips-type="tip">gc_thresh3: 40960</div><br><br><br><br><div data-tips="true" data-tips-type="tip">In larger clusters, you can further adjust these values to meet your requirements.</div><br> |
|net.ipv4.tcp_mem |Node level |Sets the total buffer size or range for TCP. The value format is `[min, default, max]`. The units for all elements in the value are pages, with each page being 4 KB in size. The specific value is calculated during system startup based on system memory size.<br><br><br>* When TCP memory is less than the minimum value, the receive buffer does not need to be automatically adjusted.<br><br>* When TCP memory is between the minimum value and the default value, the kernel starts to adjust the size of the receive buffer.<br><br>* When TCP memory is greater than the maximum value, the kernel no longer allocates new memory for TCP, and new connections cannot be established at this time. |The default value of this parameter varies by node specification. As a global TCP buffer configuration for the node, increase it based on your scenario and specifications. |
|net.core.somaxconn |Pod level |Sets the maximum listening queue length for each port in the system. This is a global parameter, with a default value of 128. This parameter limits the size of the listening queue for new TCP connections on each port. |Increasing the value of this parameter can help prevent failures caused by traffic spikes in high\-concurrency services.<br><br>For server\-type services, this value can be appropriately increased. |
|net.ipv4.tcp_max_syn_backlog |Pod level |Sets the maximum size of the TCP half\-open connection queue (SYN queue). The default value is 1024.<br><br>If the queue is full, new connection requests will be rejected or discarded.<br><br>A small value of this parameter may cause the SYN queue to overflow, making it impossible to process all connection requests. This may cause client\-side connection timeouts or rejections. |This value can be adjusted based on your business scenarios to increase the concurrent connection count of the server. |
|net.ipv4.tcp_rmem |Pod level |Sets the receive buffer size and range, in the format `[min, default, max]`. The default value is `[4096, 87380, 6291456]`. The units for all elements of the value are bytes.<br><br><br>* The first element sets the minimum receive buffer size.<br><br>* The second element sets the initial default size of the receive buffer.<br><br>* The third element sets the maximum receive buffer size. |The value can be adjusted according to the workloads in pods to improve concurrent connection performance. |
|net.ipv4.tcp_wmem |Pod level |Sets the send buffer size and range, in the format `[min, default, max]`. The default value is `[4096, 16384, 4194304]`.<br><br><br>* The first element sets the minimum send buffer size.<br><br>* The second element sets the initial default size of the send buffer.<br><br>* The third element sets the maximum send buffer size. |The value can be adjusted according to the workloads in pods to improve concurrent connection performance. |
|net.ipv4.tcp_max_tw_buckets |Pod level |Sets the maximum number of TCP connections in the `TIME_WAIT` state. The default value is 5000, which will be adjusted according to system memory.<br><br>When the number of TCP connections in the `TIME_WAIT` state in the system exceeds this value, newly closed connections skip the `TIME_WAIT` state and are directly closed with a warning logged. |If the system handles a large number of connections, increase this value as needed. An overly large value easily consumes node resources. |
|net.ipv4.tcp_tw_reuse |Pod level |Sets whether to reuse TCP connections in the `TIME_WAIT` state. The default is 0, which means that connection reuse is prohibited. This setting applies only to the client side (the party that actively initiates TCP connections).<br><br>When this option is enabled, if the port selected by the client when it calls `connect()` is already occupied by a connection with the same 4\-tuple, the system checks if that connection is in the `TIME_WAIT` state. If it is in the `TIME_WAIT` state, and the `TIME_WAIT` duration exceeds 1 second, the connection is reused, and the port can be used normally.<br><br>This parameter is effective only for clients (including reverse proxy servers when connecting the upstream, which can be considered clients). |For scenarios with a large number of client connection requests, enable this setting (setting the value to 1) to improve performance.<br><br>The default value for a VKE cluster is 2. |
|net.ipv4.tcp_fin_timeout |Pod level |Specifies the maximum time the active closing party waits for a FIN packet from the passive closing party (third handshake). This sets the maximum duration the active closing party remains in the `FIN-WAIT-2` state. The default time is 60 seconds. |Decrease this value to speed up the closure of TCP connections in the `FIN-WAIT2` state. For server\-side services, if clients leave connections open for long periods, the server will accumulate `FIN-WAIT2` connections, leading to kernel crashes. |
|net.ipv4.tcp_keepalive_time |Pod level |Defines the idle time of a TCP connection. This is a TCP parameter. If no data is transmitted within this time, the system sends a probe packet to check if the connection is still alive. The default time is 7200 seconds (2 hours). The parameter can be modified by changing the system configuration file. |Adjust the value based on business needs (this is a TCP kernel timeout setting). |
|net.ipv4.tcp_keepalive_intvl |Pod level |Specifies the interval (in seconds) between retransmitting probe packets if no response is received from the initial probe. |Adjust the value based on business needs (this is a TCP kernel timeout setting). |
|net.ipv4.tcp_keepalive_probes |Pod level |Sets the maximum number of keepalive probe packets sent before a TCP connection is declared dead. |Adjust the value based on business needs (this is a TCP kernel timeout setting). |
|net.netfilter.nf_conntrack_buckets |Pod level |Sets the number of hash buckets in the connection tracking table of the Linux system. |The capacity of the connection tracking table can be adjusted based on your business needs. |
|net.netfilter.nf_conntrack_max |Pod level |Sets the size of the connection tracking table. The default value is `net.netfilter.nf_conntrack_buckets * 4`. |This parameter controls the maximum number of entries in the connection tracking table. It can be adjusted based on your business needs. If the connection tracking table is full, new connections will fail. |
