---
title: "Modifying net.ipv4.udp_mem parameter in Linux operating system"
product: "Elastic Compute Service"
product_code: "ecs"
source: "https://docs.byteplus.com/en/docs/ecs/Adjust_the_net_ipv4_udp_mem"
---

By modifying the `net.ipv4.udp_mem` parameter, you can adjust UDP memory management policies of the kernel, thereby controlling UDP packet caching and processing capabilities of the system.

<span id=".5YWz5LqObmV0LmlwdjQudWRwX21lbeWPguaVsA=="></span>
## About the net.ipv4.udp_mem parameter

`net.ipv4.udp_mem` is a 3\-integer array structured as `[min pressure max]`. These values represent memory usage limits for the UDP protocol stack under different states, respectively. The three values define memory thresholds, with the unit being `Page` (kernel page; typically, 1 kernel page equals 4 KiB). Their meanings are as follows:


* `min`: The threshold at which the kernel starts reclaiming memory. When the UDP memory usage of the system reaches this value, the kernel starts reclaiming memory to prevent overuse.

* `pressure`: The soft limit for kernel memory usage. When this value is exceeded, UDP adjusts its memory consumption and enters memory pressure mode. When memory consumption drops below the value specified by `min`, UDP exits memory pressure mode.

* `max`: The hard limit for kernel memory usage. That is, the maximum number of pages allowed for all UDP sockets to queue and buffer datagrams. When this value is exceeded, the system refuses to allocate new sockets.


<span id=".5pON5L2c5Zy65pmv"></span>
## Applicable scenario


* **Scenarios with heavy network load**

   In scenarios that require processing a large number of UDP packets, such as real\-time video streaming or large\-scale data transmission, servers may encounter packet loss. This happens because the total memory of UDP sockets reaches the upper limit. In such cases, you can refer to the following adjustment plan:

   * `min`: Set this parameter to a relatively high value to reduce the impact of frequent memory reclamation on high\-traffic requests.

   * `pressure`: Set this parameter to 4/3 times the value of the `min` parameter.

   * `max`: Set this parameter to twice the value of the `pressure` parameter.

* **Scenarios with light network load**

   In scenarios involving basic internal network services with low UDP usage, such as file transfer and printing services, servers may experience unnecessary memory usage due to a high memory reclamation threshold. In such cases, you can refer to the following adjustment plan:

   * `min`: Set this parameter to a relatively low value to lower the threshold for triggering memory reclamation and avoid unnecessary memory usage.

   * `pressure`: Set this parameter to 4/3 times the value of the `min` parameter.

   * `max`: Set this parameter to twice the value of the `pressure` parameter.


<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure


<Tabs>
<Tab zoneid="DWWvUfGCUK" title="Configuration by using the proc interface">
<TabTitle>Configuration by using the proc interface</TabTitle>

You can use this method to temporarily modify the parameter value while the operating system is running. Each time the instance restarts, you need to configure the parameter again.


1. Log in to the target instance. For more information, see [Logging in to Linux instances](https://docs.byteplus.com/en/docs/ecs/Logging-on-to-a-Linux-instance).

2. Execute the following command on the target Linux instance to view the current value of the `net.ipv4.udp_mem` parameter.

   ```Plain Text
   cat /proc/sys/net/ipv4/udp_mem
   ```
   

   Sample output:

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_3c09244d9fe3316fabc6aba77d3c5cf7.png) </span>

3. Execute the following command to configure the `net.ipv4.udp_mem` parameter.

   ```Plain Text
   echo "42396 56530 84792" > /proc/sys/net/ipv4/udp_mem
   ```
   

   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">Replace <code>42396 56530 84792</code> with the actual value required for your business. For more information, see <a href="https://docs.byteplus.com/en/docs/ecs/Adjust_the_net_ipv4_udp_mem#.5YWz5LqObmV0LmlwdjQudWRwX21lbeWPguaVsA==">About the net\-ipv4\-udp\-mem parameter</a>.   </div>
   


</Tab>
<Tab zoneid="OdrYT6zoUm" title="Configuration by using the net_udp.conf file">
<TabTitle>Configuration by using the net_udp.conf file</TabTitle>

You can use this method to permanently modify the parameter value while the operating system is running. You do not need to configure the parameter again after the instance restarts.


1. Log in to the target instance. For more information, see [Logging in to Linux instances](https://docs.byteplus.com/en/docs/ecs/Logging-on-to-a-Linux-instance).

2. Execute the following command to view the current parameter value.

   ```Plain Text
   sysctl net.ipv4.udp_mem
   ```
   

   Sample output:

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_f0e0fece9591a3ed1d9aa0d048260c7b.png) </span>

3. Modify the `net.ipv4.udp_mem` parameter value.

   1. Execute the following command to create the net_udp.conf file.

      ```Plain Text
      vim /etc/sysctl.d/net_udp.conf
      ```
      

   2. Press the `i` key to enter edit mode and add the following content to the end of the file.

      ```Plain Text
      net.ipv4.udp_mem = 42396 56530 84792
      ```
      

      <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="2">tip      </div>
      

      <div data-tips="true" data-tips-type="default" data-wrapper-indent="2">Replace <code>42396 56530 84792</code> with the actual value required for your business. For more information, see <a href="https://docs.byteplus.com/en/docs/ecs/Adjust_the_net_ipv4_udp_mem#.5YWz5LqObmV0LmlwdjQudWRwX21lbeWPguaVsA==">About the net\-ipv4\-udp\-mem parameter</a>.      </div>
      

   3. Press the `Esc` key to exit edit mode, enter `:wq`, and then press Enter to save and exit the file.

4. Execute the following command to make the configuration take effect.

   ```Plain Text
   sysctl -p /etc/sysctl.d/net_udp.conf
   ```
   


</Tab>
</Tabs>
