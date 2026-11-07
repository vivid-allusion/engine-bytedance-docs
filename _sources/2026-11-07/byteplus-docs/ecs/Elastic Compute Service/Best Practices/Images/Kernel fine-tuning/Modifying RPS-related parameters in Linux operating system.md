---
title: "Modifying RPS-related parameters in Linux operating system"
product: "Elastic Compute Service"
product_code: "ecs"
source: "https://docs.byteplus.com/en/docs/ecs/Adjust-RPS-in-Linux"
---

This topic describes how to configure parameters related to the Receive Packet Steering (RPS) feature in the Linux operating system to optimize network packet processing and improve network performance and load balancing on multicore systems.

<span id=".5Y-C5pWw6K-05piO"></span>
## Parameter description

<span id="net.core.rps_sock_flow_entries"></span>
### net.core.rps_sock_flow_entries

This parameter specifies the maximum number of flow table entries in the Linux kernel, that is, the number of network flows that can be tracked simultaneously. Increasing the value of this parameter can improve RPS performance, thereby enabling more efficient utilization of multiple CPU cores for processing network traffic. Each flow in the flow table corresponds to a network connection. When a packet arrives, the kernel determines the corresponding flow based on the source address, destination address, protocol, and other information of the packet, and then dispatches the packet to the CPU core associated with that flow for processing.

<span id="rps_cpus"></span>
### rps_cpus

In this practice, rps_cpus refers to the `/sys/class/net/<interface>/queues/rx-<queue>/rps_cpus` parameter, which specifies the CPU cores that process network flow packets from the specified queue queues of a single network interface. By configuring this argument, you can limit the number of CPU cores involved in RPS processing, thereby improving system performance.

<span id="rps_flow_cnt"></span>
### rps_flow_cnt

In this practice, rps_flow_cnt refers to the `/sys/class/net/<interface>/queues/rx-<queue>/rps_flow_cnt` parameter, which specifies the maximum number of flows that can be cached in the RPS queue on each CPU core, within the specified queues of a single network interface. By increasing the value of this parameter, more data packets can be distributed across multiple processing cores, thereby accelerating the processing of data packets.

<span id=".5pON5L2c5Zy65pmv"></span>
## Applicable scenario


* When the number of CPUs is much greater than the number of network interface queues, you can improve network performance by configuring the `rps_sock_flow_entries` parameter.

* When an ECS instance uses a virtual network interface (for example, veth), you can configure the `rps_sock_flow_entries` parameter to significantly improve network performance.


<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>



* <div data-tips="true" data-tips-type="warning">We recommend that you do not configure parameters related to the RPS feature for regular physical network interfaces, as this may increase inter\-core interrupt overhead and degrade performance.</div>


* <div data-tips="true" data-tips-type="warning">RFS depends on RPS. RPS is disabled by default, and you need to enable RPS for RFS\-related configuration to take effect. When you configure the CPU list for RPS, we recommend that you select CPUs within the same NUMA domain as the interrupt CPU, and do not select CPUs that are already heavily loaded.</div>



<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure


<Tabs>
<Tab zoneid="YjAmojaqaa" title="Configuration by using the proc interface">
<TabTitle>Configuration by using the proc interface</TabTitle>

You can use this method to temporarily modify the parameter values while the operating system is running. You need to configure the parameters again after the instance restarts.


1. Log in to the target instance. For more information, see [Logging in to Linux instances](https://docs.byteplus.com/en/docs/ecs/Logging-on-to-a-Linux-instance).

2. Execute the following commands to view the parameter values.

   * View the value of the `rps_sock_flow_entries` parameter.

      ```Plain Text
      cat /proc/sys/net/core/rps_sock_flow_entries
      ```
      

      Sample output:

      <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_d4c68afd58f9000fb23fcfbd7cd98c05.png) </span>

   * View the value of the `rps_cpus` parameter.

      ```Plain Text
      cat /sys/class/net/eth0/queues/rx-*/rps_cpus
      ```
      

      Sample output:

      <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_1a41eaee43b0d64c60d47ec47399870f.png) </span>

   * View the value of the `rps_flow_cnt` parameter.

      ```Plain Text
      cat /sys/class/net/eth0/queues/rx-*/rps_flow_cnt
      ```
      

      Sample output:

      <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_b57100d32ea9baef92fe7503cb0a0220.png) </span>

3. Execute the following command to configure parameters.

   * Configure the `rps_sock_flow_entries` parameter.

      <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="2">tip      </div>
      

      <div data-tips="true" data-tips-type="default" data-wrapper-indent="2">We recommend that you set this parameter to 32768. You can also modify the parameter based on your actual needs.      </div>
      

      ```Plain Text
      echo 32768 > /proc/sys/net/core/rps_sock_flow_entries
      ```
      

   * Configure the `rps_cpus` parameter.

      <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="2">tip      </div>
      

      <div data-tips="true" data-tips-type="default" data-wrapper-indent="2">This command is executed to specify that all available CPU cores are used for processing when the <code>eth0</code> network interface receives data packets. Replace <code>eth0</code> with the actual name of the network interface.      </div>
      

      ```Plain Text
      echo ff > /sys/class/net/eth0/queues/rx-*/rps_cpus
      ```
      

   * Configure the `rps_flow_cnt` parameter.

      <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="2">tip      </div>
      

      <div data-tips="true" data-tips-type="default" data-wrapper-indent="2">In this practice, the number of CPU cores for the instance is 8, and the name of the network interface is eth0.      </div>
      

      * <div data-tips="true" data-tips-type="default" data-wrapper-indent="2">Replace <code>4096</code> with the value of <code>rps_sock_flow_entries</code> divided by the number of CPU cores.      </div>
      

      * <div data-tips="true" data-tips-type="default" data-wrapper-indent="2">Replace <code>eth0</code> with the actual name of the network interface.      </div>
      

      ```Plain Text
      echo 4096 > /sys/class/net/eth0/queues/rx-*/rps_flow_cnt
      ```
      





</Tab>
<Tab zoneid="O7iXRvfbZM" title="Configuration by using a file">
<TabTitle>Configuration by using a file</TabTitle>

You can use this method to permanently modify the parameter values while the operating system is running. You do not need to configure the parameters again after the instance restarts.


1. Log in to the target instance. For more information, see [Logging in to Linux instances](https://docs.byteplus.com/en/docs/ecs/Logging-on-to-a-Linux-instance).

2. Execute the following commands to view the parameter values.

   View the value of the `net.core.rps_sock_flow_entries` parameter.

   ```Plain Text
   sysctl net.core.rps_sock_flow_entries
   ```
   

   Sample output:

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_c981fcd564940f306f537dc2801c7cbd.png) </span>

3. Modify values of RPS\-related parameters.

   * CentOS and Fedora

      1. Execute the following command to create the /etc/sysctl.d/rps.conf file.

         ```Plain Text
         sudo vim /etc/sysctl.d/rps.conf
         ```
         

      2. Press the `i` key to enter edit mode, and add the following content to the configuration file.

         ```Plain Text
         net.core.rps_sock_flow_entries=32768
         ```
         

      3. Press the `Esc` key to exit edit mode, enter `:wq`, and then press Enter to save and exit the file.

      4. Execute the following command to create the /etc/sysfs\-ng.d/rps.conf file.

         ```Plain Text
         sudo vim /etc/sysfs-ng.d/rps.conf
         ```
         

      5. Press the `i` key to enter edit mode, and add the following content to the configuration file.

         <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="3">tip         </div>
         

         <div data-tips="true" data-tips-type="default" data-wrapper-indent="3">In this practice, the number of CPU cores for the instance is <code>8</code>, and the name of the network interface is <code>eth0</code>.         </div>
         

         * <div data-tips="true" data-tips-type="default" data-wrapper-indent="3">Replace <code>4096</code> with the value of <code>rps_sock_flow_entries</code> divided by the number of CPU cores.         </div>
         

         * <div data-tips="true" data-tips-type="default" data-wrapper-indent="3">Replace <code>eth0</code> with the actual name of the network interface.         </div>
         

         ```Plain Text
         class/net/eth0/queues/rx-*/rps_cpus = ff
         class/net/eth0/queues/rx-*/rps_flow_cnt = 4096
         ```
         

      6. Press the `Esc` key to exit edit mode, enter `:wq`, and then press Enter to save and exit the file.

   * Debian and Ubuntu

      7. Execute the following command to create the /etc/sysctl.d/rps.conf file.

         ```Plain Text
         sudo vim /etc/sysctl.d/rps.conf
         ```
         

      8. Press the `i` key to enter edit mode, and add the following content to the configuration file.

         ```Plain Text
         net.core.rps_sock_flow_entries=32768
         ```
         

      9. Press the `Esc` key to exit edit mode, enter `:wq`, and then press Enter to save and exit the file.

      10. Execute the following command to create the /etc/sysfs.d/rps.conf file.

         ```Plain Text
         sudo vim /etc/sysfs.d/rps.conf
         ```
         

      11. Press the `i` key to enter edit mode, and add the following content to the configuration file.

         <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="3">tip         </div>
         

         <div data-tips="true" data-tips-type="default" data-wrapper-indent="3">In this practice, the number of CPU cores for the instance is <code>8</code>, and the name of the network interface is <code>eth0</code>.         </div>
         

         * <div data-tips="true" data-tips-type="default" data-wrapper-indent="3">Replace <code>4096</code> with the value of <code>rps_sock_flow_entries</code> divided by the number of CPU cores.         </div>
         

         * <div data-tips="true" data-tips-type="default" data-wrapper-indent="3">Replace <code>eth0</code> with the actual name of the network interface.         </div>
         

         ```Plain Text
         class/net/eth0/queues/rx-*/rps_cpus = ff
         class/net/eth0/queues/rx-*/rps_flow_cnt = 4096
         ```
         

      12. Press the `Esc` key to exit edit mode, enter `:wq`, and then press Enter to save and exit the file.

4. Execute the following command to restart the instance for the configuration to take effect.

   ```Plain Text
   reboot
   ```
   


</Tab>
</Tabs>
