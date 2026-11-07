---
title: "Installing RDMA Agent in HPC-optimized instances"
product: "GPU Compute Service"
product_code: "gpu"
source: "https://docs.byteplus.com/en/docs/gpu/Installing_RDMA_Agent_in_HPC-optimized_instances"
---

RDMA (Remote Direct Memory Access) is a network technology for remote direct memory access. It is a common end\-to\-end transmission technology in high\-speed networks and is widely applied to ECS instances. The RDMA Agent is designed to enhance the reliability and stability of RDMA networks. You can use RDMA Agent to manage RDMA configuration of HPC\-optimized instances, with its main functions as follows:


* Delivers and manages configurations related to RDMA network interfaces, such as QoS, DSCP, PFC, and MTU.

* Generates GPU Topo files.

* Generates RDMA policy\-based routes.

* Deploys self\-developed congestion control algorithms.


<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>



* <div data-tips="true" data-tips-type="warning">In an HPC\-optimized instance created based on a public image, the RDMA Agent is preinstalled by default. No additional installation is required. For a non\-GPU instance, you do not need to install the RDMA Agent.</div>


* <div data-tips="true" data-tips-type="warning">If the RDMA Agent is installed in instances created based on non\-public images, normal service operations can not be guaranteed. When exceptions occur, please contact technical support timely.</div>



<span id="WxZlv3Yi"></span>
## Usage notes


* The instance must be in the **Running** status.

* Recommended operating systems for using the RDMA Agent include:

   * Debian 10

   * Ubuntu 20.04/22.04

   * CentOS 8.3

   * Rocky Linux 9.1

   * veLiunx 1.0

* Hardware driver dependency: Network interface driver and the corresponding version of Firmware.

* The naming format of RDMA network interfaces is `eth*` (standard), and that of their device names is `mlx5_*`.


<span id="Cf48SzLf"></span>
## Install RDMA Agent


<Tabs>
<Tab zoneid="AfFdBZJiAS" title="Method 1: Quick installation via script (recommended)">
<TabTitle>Method 1: Quick installation via script (recommended)</TabTitle>

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">Script\-based installation is strongly recommended. Due to its automatic download and OS\-based installation operations, you only need to select an appropriate region.</div>



1. [Log in to the target instance](https://docs.byteplus.com/en/docs/ecs/Using-the-console-to-log-on-to-a-Linux-instance).

2. Pull the deployment script.

   * Download via the public network:

      Download link: [https://rdma-toc-config-cn-beijing.tos-cn-beijing.volces.com/install_new.sh](https://rdma-toc-config-cn-beijing.tos-cn-beijing.volces.com/install_new.sh). If direct access fails, download the script to your local computer first, and then manually upload it to your ECS instance. [How to upload files to an ECS instance?](https://docs.byteplus.com/en/docs/ecs/Local-data-uploading-overview)

   * Download via the private network:

      ```Bash
      REGION=$(wget -O - -a /var/log/wget.log -t 1 --timeout=10 "http://100.96.0.96/latest/region_id" 2>/dev/null)
      wget "https://rdma-toc-config-${REGION}.tos-${REGION}.ivolces.com/install_new.sh"
      ```
      

      3. Execute the following command to install. Replace <version\> with the actual version number (for example, `bash ./install.sh 1.1.11`).

   ```Bash
   bash ./install.sh <version>  
   ```
   





</Tab>
<Tab zoneid="ypKSBnS3jC" title="Method 2: Manual package download">
<TabTitle>Method 2: Manual package download</TabTitle>

1. [Log in to the target instance](https://docs.byteplus.com/en/docs/ecs/Using-the-console-to-log-on-to-a-Linux-instance).

2. Download the package.

   * Download via the public network:

      ```Shell
      VERSION=1.1.11
      deb：https://rdma-toc-config-cn-beijing.tos-cn-beijing.volces.com/rdma-agent_${VERSION}-0_all.deb
      
      rpm：https://rdma-toc-config-cn-beijing.tos-cn-beijing.volces.com/rdma-agent-${VERSION}-0.noarch.rpm
      ```
      

   * Download via the private network:

      * deb:

         ```Shell
         REGION=$(wget -O - -a /var/log/wget.log -t 1 --timeout=10 "http://100.96.0.96/latest/region_id" 2>/dev/null)
         RDMA_BUCKET_URL="rdma-toc-config-${REGION}.tos-${REGION}.ivolces.com"
         PKG_FILE="rdma-agent_${VERSION}-0_all.deb"
         PKG_URL="http://${RDMA_BUCKET_URL}/$PKG_FILE"
         wget "$PKG_URL"
         ```
         

      * rpm:

         ```Shell
         REGION=$(wget -O - -a /var/log/wget.log -t 1 --timeout=10 "http://100.96.0.96/latest/region_id" 2>/dev/null)
         RDMA_BUCKET_URL="rdma-toc-config-${REGION}.tos-${REGION}.ivolces.com"
         PKG_FILE="rdma-agent-${VERSION}-0.noarch.rpm"
         PKG_URL="http://${RDMA_BUCKET_URL}/$PKG_FILE"
         wget "$PKG_URL"
         ```
         

3. Execute the following commands to install.

   * deb:

      ```Shell
      dpkg -i rdma-agent_${VERSION}-0_all.deb
      ```
      

   * rpm:

      ```Shell
      rpm -i rdma-agent-${VERSION}-0.noarch.rpm
      ```
      





</Tab>
</Tabs>


<span id="IuJZFSlP"></span>
## View RDMA Agent status


1. Execute the following command to check the status of rdma_agent.service.

   ```Shell
   systemctl status rdma_agent.service
   ```
   

   If **active (running)**  is returned, the service is running normally.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_265553c6457c8da43b5734316e22d011.png) </span>

2. During normal operations of the service, execute the following commands to check whether the configuration items delivered by rdma_agent meet your expectations.

   ```Shell
   /etc/sysop/rdma_service/agent_tobhpc/rdma-agent-check &> /dev/null
   echo $?
   ```
   

   If a number that is **not 0** is returned, this indicates that an unexpected configuration exception occurs.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_15ae811778d7d463cae9fef83b3d8c1e.png) </span>

3. Execute the following commands to view the rdma_agent version.

   * Manage rpm package:

      ```Shell
      rpm -qa | grep rdma-agent
      ```
      

   * Manage deb package:

      ```Shell
      dpkg -l | grep rdma-agent
      ```
      

4. Execute the following command to check whether the network congestion control configuration is correct.

   ```Shell
   tail /var/log/rdma/rdma_cc_tool.log
   ```
   


<span id="s2VzCKky"></span>
## Version release notes


|RDMA Agent version |Release content |
|---|---|
|1.1.11 |* Supported: RockyOS.<br><br>* Added: ARP configuration and checks:<br><br>   ```Shell```<br>```   sysctl net.ipv4.conf.all.arp_ignore=1; sysctl net.ipv4.conf.all.arp_announce=2```<br>```   ```<br>   <br><br>* Added: automatic stopping and disabling is executed after the rdma_agent package is removed. This stops and disables the rdma agent and removes the /etc/sysop/rdma_service directory.<br><br>   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_d385e361613cf38a1c3585ff22feab78.png) </span> |
|1.1.10 |* Supported: content updates for the vRDMA hot\-plug network interface Topo file.<br><br>* Fixed issue: the Agent exits abnormally when the mlnx_qos command fails. |
|1.1.9 |Supported: the NPU model. |
|1.1.8 |* Rdmacctool\-related updates:<br><br>   * Supported: automatically selecting and deploying DCQCN and BCC. DCQCN covers the entire cluster.<br><br>   * Updated: BCC of a more stable algorithm version.<br><br>   * Fixed issue: PCC is enabled in the online cluster but the algorithm is not enabled. This prevents cluster CC failures.<br><br>* Supported: nvidia_peermem check.<br><br>* Supported: Mlxreg roce_tx_window_en configuration. |


<span id="TPa2KbtM"></span>
## FAQ

<span id="tpyzlh6d"></span>
### How can I determine whether to update the version of the current rdma\-agent component?

You can check the current component version by executing the following commands. Note that version 1.0.x does not support persistent configuration processes or the new version algorithm for congestion control. As a result, if your current component version is 1.0.x, configuration failures, connectivity issues, or performance problems may occur in some scenarios. Therefore, we strongly recommend that you upgrade the version to 1.1.11 or later. For upgrade methods, refer to [Installing RDMA Agent](https://docs.byteplus.com/en/docs/gpu/Installing_RDMA_Agent_in_HPC-optimized_instances?lang=zh#Cf48SzLf).

```Bash
# Velinux/Ubuntu/Debian
dpkg -l | grep "rdma-agent"
# RockyLinux/CentOS
rpm -qa | grep "rdma-agent"
```
