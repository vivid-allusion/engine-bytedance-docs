---
title: "Deploying and running DPDK applications"
product: " Vital Kubernetes Engine"
product_code: "vke"
source: "https://docs.byteplus.com/en/docs/vke/Deploying_and_running_DPDK_applications"
---

The VKE supports enabling DPDK in pods, suitable for scenarios requiring low latency and high throughput. This topic describes how to deploy and run DPDK apps in a cluster.

## Background

DPDK (Data Plane Development Kit) is a high\-performance network data plane development toolkit. By using technologies such as userspace polling drivers, huge pages, CPU affinity, and lock\-free queues, it bypasses the traditional Linux kernel network stack, significantly reducing overhead from interrupts, context switching, and system calls. This greatly improves packet transfer performance, achieving tens of millions of PPS processing capability on a single CPU core.

In DPDK mode, the host network interface can be assigned to a container to create a direct connection. This allows it to be used as a DPDK high\-performance data plane interface. By mounting two network interfaces to a pod, traffic between the data plane and control plane can be physically isolated. This avoids bandwidth contention and latency interference, ensuring stable microsecond\-level forwarding.

## Prerequisites

* The vpc\-cni add\-on has been installed and upgraded to v1.9.6 or later.

* The VFIO device driver has been enabled on the nodes of the cluster. You can run the following command on the node to check whether the VFIO driver is enabled.

   ```Bash
   lsmod | grep vfio-pci
   ```

   The expected result is as follows.

   ```Bash
   vfio_pci                 65536    0
   vfio_iommu_type1         36864    0
   vfio                     36864    2   vfio_iommu_type1, vfio_pci
   vfio_virqfd              16384    1   vfio_pci
   irqbypass                16384    1   vfio_pci
   ```

## Usage limits

* Only supported in clusters using the VPC\-CNI network model.

* The number of network interfaces that can be mounted to a node is ≥ 3, meaning it must include at least a primary interface, a secondary interface, and a dedicated interface.

* DPDK can only be enabled on new nodes. We recommend using a dedicated node pool.

## Procedure

### Step 1: Enable the DPDK feature

1. Log in to the [VKE console](https://console.byteplus.com/vke).

2. In the left navigation bar, click **Cluster**. Click the name of the target cluster to go to the cluster management page.

3. In the left navigation bar, select **Configurations \> ConfigMap**.

4. In the **Namespace** drop\-down list, select **kube\-system**. Locate **cello\-config** on the page, and click **Edit Yaml** in the **Actions** column.

5. In the `data.conf` field, add the `exclusiveENIPoolQuota` field to enable the DPDK feature on the node.

   > **tip**

   > We recommend enabling the DPDK feature at the node pool level. You can add the `exclusiveENIPoolQuota` field in the node pool configuration. For the configuration at the node pool level, see [Configuring pod security groups and subnets at the node pool level](https://docs.byteplus.com/en/docs/vke/Configuring-pod-security-groups-and-subnets-on-a-NodePool-basis).

   ```YAML
   apiVersion: v1
   kind: ConfigMap
   metadata:
     name: cello-config
     namespace: kube-system
   data:
     conf: |
       {
         "exclusiveENIPoolQuota": 2,
         "subnets": [
           "subnet-22joc5bb2g***",
           "subnet-22joc64wj5***"
         ],
         ...
       }
   ...
   ```

   The parameter descriptions are shown in the following table.

   |Parameter |Description |
   |---|---|
   |exclusiveENIPoolQuota |Number of pods that require DPDK network interfaces on a single node. |

   > Note

   > If you need to modify the above configuration afterwards, please note that the cello pod needs to be restarted for the changes to take effect.

6. [Connect to the cluster via kubectl](https://docs.byteplus.com/en/docs/vke/Connecting-to-a-cluster), and execute the following command to perform a rolling restart of the Cello Pod so that the configuration can take effect.

   ```Bash
   kubectl rollout restart daemonset cello -n kube-system
   ```

### Step 2: Enable DPDK dependencies on the node

**Configure manually**

You can manually configure the HugePages feature on specified nodes. The procedure is as follows:

1. Use **ECS Terminal** to log in to the target node. For details, see [ECS Terminal](https://docs.byteplus.com/en/docs/vke/Managing-nodes#ecs-terminal).

2. Run the following command to configure the number of HugePages on the node in the sysctl configuration file.

   ```Bash
   sysctl -w vm.nr_hugepages=1024
   ```

   > **tip**

   * > This example configures 2Mi HugePages. In practice, adjust the configuration based on your needs.

   * > For more information about node HugePages features, see the [official documentation](https://www.kernel.org/doc/html/latest/admin-guide/mm/hugetlbpage.html).

3. Run the following command to restart kubelet.

   ```Bash
   systemctl restart kubelet
   ```

**Configure via script**

When creating or editing a node pool, you can use deployment scripts to configure the HugePages feature on nodes in batch. Procedure:

1. Log in to the [VKE console](https://console.byteplus.com/vke).

2. In the left navigation bar, click **Cluster**. Click the target cluster name to go to the management page of this cluster.

3. In the left navigation bar, select **Nodes** \>**Node pool**, create a node pool or edit an existing one.

4. In the **Advanced settings** \> **InitializeScript** textbox, paste the following script.

   ```Bash
   #!/bin/bash
   set -e
   
   echo "====================="
   echo "  DPDK HugePages script  "
   echo "====================="
   
   # 1. Back up the original sysctl.conf
   cp /etc/sysctl.conf /etc/sysctl.conf.bak.$(date +%Y%m%d%H%M%S)
   
   # 2. Write HugePages configuration (create a new configuration if it does not exist, otherwise replace the existing one)
   sed -i '/^vm.nr_hugepages/d' /etc/sysctl.conf
   sed -i '/^vm.nr_overcommit_hugepages/d' /etc/sysctl.conf
   
   cat >> /etc/sysctl.conf <<EOF
   # DPDK HugePages config
   vm.nr_hugepages = 1024
   EOF
   
   # 3. Load configuration
   sysctl -p
   
   # 4. Restart kubelet and report HugePages resources
   systemctl daemon-reload
   systemctl restart kubelet
   
   # 5. Validate result
   echo -e "\n Configuration complete. Current HugePages status:"
   grep Huge /proc/meminfo | head -5
   
   echo -e "\n Node DPDK environment initialization complete!"
   ```

5. After completing all the node pool settings, click **Confirm** to finish the node pool configuration. For descriptions of more node pool parameters, see [Creating managed node pools](https://docs.byteplus.com/en/docs/vke/Creating-a-managed-NodePool).

After completing the configuration, you can [connect to the cluster via kubectl](https://docs.byteplus.com/en/docs/vke/Connecting-to-a-cluster) and run the following command to view node information. Here, `${node-ip}` is the node IP address, for example, 192.168.1.188.

```Bash
kubectl describe node ${node-ip}
```

The expected output is as follows, showing the number of HugePages and ENIs that can be allocated or have already been allocated to the node.

```Bash
Addresses:
  InternalIP:  192.168.2.188
  Hostname:    192.168.2.188
Capacity:
  cpu:                        4
  ephemeral-storage:          102626232Ki
  hugepages-1Gi:              0
  hugepages-2Mi:              2Gi
  memory:                     16122304Ki
  pods:                       46
  vke.volcengine.com/eni:     2
  vke.volcengine.com/eni-ip:  10
Allocatable:
  cpu:                        3900m
  ephemeral-storage:          94580335255
  hugepages-1Gi:              0
  hugepages-2Mi:              2Gi
  memory:                     11255454105600m
  pods:                       46
  vke.volcengine.com/eni:     2
  vke.volcengine.com/eni-ip:  10
```

### Step 3: Use DPDK in the pod

1. (Optional) You can use the following Dockerfile example to build a DPDK test image. and install testpmd in the image for testing.

   ```Dockerfile
   FROM ubuntu:20.04
   ARG DPDK_VERSION=21.11.3
   
   # Install DPDK compilation dependencies
   RUN apt-get update && \
       apt-get install -y build-essential python3 python3-pip pciutils iproute2 libnuma-dev && \
       pip3 install meson ninja==1.8.2 pyelftools
   
   # Compile and install DPDK + testpmd
   RUN mkdir -p /dpdk_build && cd /dpdk_build && \
       curl -OL http://fast.dpdk.org/rel/dpdk-${DPDK_VERSION}.tar.xz && \
       tar -xvf dpdk-${DPDK_VERSION}.tar.xz && \
       cd dpdk-stable-${DPDK_VERSION} && \
       meson build && cd build && \
       ninja && \
       ninja install && \
       ldconfig
   ```

2. Create a pod using the above image and configure DPDK. The key settings are as follows:

   * Mount VFIO devices: Use a `hostPath` volume to mount the host's `/dev` directory to the container's `/dev`.

   * HugePages memory request: Declare the HugePages and memory limits required by the DPDK application in the pod configuration.

   * Network interface driver binding: Before the container starts, run `mount -o remount,rw /sys/ && dpdk-devbind.py --force -b vfio-pci eth0` to bind the pod's network interface driver to the vfio\-pci driver.

   ```YAML
   apiVersion: v1
   kind: Pod
   metadata:
     name: pod-demo
     annotations:
       k8s.volcengine.com/pod-networks: | # Configure dual network interfaces for the pod
         [
           {
             "cniConf":{
                 "name":"eni"
             }
           }
         ]
   spec:
     containers:
     - name: dpdk-demo
       image: doc-demo-cn-shanghai.cr.volces.com/demo/dpdk-demo:v1.4
       args: 
       - "-c"
       - "sleep infinity &&mount -o remount,rw /sys/ && dpdk-devbind.py --force -b vfio-pci eth1 && dpdk-testpmd -- --forward-mode icmpecho"
       command:
       - bash
       tty: true 
       resources:
         limits:
           vke.volcengine.com/eni: 1
           hugepages-2Mi: 1Gi # Number of HugePages requested
           memory: 1Gi
         requests:
           hugepages-2Mi: 1Gi # requests configuration must be consistent with limits
           memory: 1Gi
       securityContext:
         privileged: true # Enable privileged container
         capabilities:
           add:
           - IPC_LOCK
       volumeMounts: # mount VFIO device
       - name: host-dev
         mountPath: /dev
       - mountPath: /hugepages-2Mi
         name: hugepage-2mi
     volumes:
     - name: host-dev
       hostPath:
         path: /dev
     - name: hugepage-2mi
       emptyDir:
         medium: HugePages-2Mi
   ```

## Validating results

### Viewing settings

1. After the configuration is completed, the system will automatically add the annotation `k8s.volcengine.com/network-status` to the pod, displaying the network interface information mounted to the pod. For example, in this case, the pod has 2 network interfaces mounted, with IP addresses `192.168.1.242` and `192.168.1.244`, respectively.

2. Run the following command to enter the corresponding pod.

   ```Bash
   kubectl exec -it dpdk-demo -- bash
   ```

3. Run the following command to view the environment variables in the pod.

   ```Bash
   env
   ```

   The expected output is as follows, where:

   * `RESOURCE_NAME`: Indicates the device name of the PCI device in the pod.

   * `PCIDEVICE_VOLCENGINE_COM_ENI`: Indicates the address (BDF) of the corresponding PCI device.

   ```Bash
   KUBERNETES_SERVICE_PORT_HTTPS=443
   KUBERNETES_SERVICE_PORT=443
   HOSTNAME=pod-demo
   PCIDEVICE_VOLCENGINE_COM_ENI=0000:03:02.0
   PWD=/
   HOME=/root
   DPDK_EXPORTER_DIR=/dpdk-telemetry-exporter
   RTE_SDK=/dpdk
   DPDK_DIR=/dpdk
   RESOURCE_NAME=PCIDEVICE_VOLCENGINE_COM_ENI
   KUBERNETES_PORT_443_TCP_PROTO=tcp
   ...
   ```

### Validating via tests

You can install testpmd in the pod to validate the DPDK feature. For more details, see the [official documentation](https://doc.dpdk.org/guides/testpmd_app_ug).

1. Run the following command to view the DPDK version.

   ```Bash
   dpdk-testpmd -v
   ```

2. Run the following command to view the DPDK port status.

   ```Bash
   show port info all
   ```

   The expected output is as follows.

   ```Bash
   Telling cores to stop...
   Waiting for lcores to finish...
   
     +++++++++++++++ Accumulated forward statistics for all ports+++++++++++++++
     RX-packets: 0              RX-dropped: 0             RX-total: 0
     TX-packets: 0              TX-dropped: 0             TX-total: 0
     ++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++
   
   Done.
   
   Bye...
   ```

3. Run the following command to start testpmd and check whether DPDK is working properly.

   ```Bash
   dpdk-testpmd -l0-1 -n4 -- -i
   ```

   The expected result is as follows, and the log shows that DPDK is working normally.

   ```Bash
   EAL: Detected CPU lcores: 4
   EAL: Detected NUMA nodes: 1
   EAL: Detected static linkage of DPDK
   EAL: Multi-process socket /var/run/dpdk/rte/mp_socket
   EAL: Selected IOVA mode 'PA'
   EAL: Probe PCI devices: 0000:xx:xx.x 
   EAL: Probe PCI devices: 0000:xx:xx.x
   ...
   Interactive-mode selected 
   testpmd: create a new mbuf pool <mbuf_pool_socket_0>: size=xxx, nb_mbufs=xxx 
   Configuring Port 0 (socket 0) 
   Port 0: xx:xx:xx:xx:xx:xx 
   Checking link statuses... 
   Port 0 Link Up - speed 10000 Mbps - full-duplex 
   Done 
   ...
   ```

## Subsequent configurations

After the DPDK program exits, run the following command in the pod to manually clear driver_override.

```Bash
echo > /sys/bus/pci/devices/<pciaddr>/driver_override
```
