---
title: "Modifying net.ipv4.tcp_mem parameter in Linux operating system"
product: "Elastic Compute Service"
product_code: "ecs"
source: "https://docs.byteplus.com/en/docs/ecs/Adjust_the_net_ipv4_tcp_mem"
---

Modifying the `net.ipv4.tcp_mem` parameter allows you to specify the memory available to the TCP stack for processing network data, thereby controlling memory allocation and release in TCP network connections.

<span id=".5YWz5LqObmV0LmlwdjQudGNwX21lbeWPguaVsA=="></span>
## About the net.ipv4.tcp_mem parameter

`net.ipv4.tcp_mem` is an array of three integers in the format `[min pressure max]`. These values represent the memory usage limits of the TCP protocol stack in different states. These three values define memory thresholds, with the unit set to `Page` (kernel page; one kernel page is normally 4 KiB). Their definitions are as follows:


* `min`: The threshold at which the kernel starts reclaiming memory. When the TCP memory usage of the system reaches this value, the kernel starts reclaiming memory to prevent overuse.

* `pressure`: The soft limit for kernel memory usage. When this value is exceeded, TCP adjusts its memory consumption and enters memory pressure mode. When memory consumption drops below the value specified by `min`, TCP exits memory pressure mode.

* `max`: The hard limit for kernel memory usage. That is, the maximum number of pages allowed for all TCP sockets to queue. When this value is exceeded, the system refuses to allocate new sockets.


<span id=".5pON5L2c5Zy65pmv"></span>
## Applicable scenario


* **Scenarios with heavy network load**

   In high\-traffic scenarios that require handling large numbers of concurrent HTTP requests, such as high\-load web servers, streaming media servers, and big data transmission services, servers may encounter TCP connection bottlenecks or excessive memory usage. In such cases, you can use the following recommendations:

   * `min`: Set this parameter to a relatively high value to reduce the impact of frequent memory reclamation on high\-traffic requests.

   * `pressure`: Set this parameter to 4/3 times the value of the `min` parameter.

   * `max`: Set this parameter to twice the value of the `pressure` parameter.

* **Scenarios with light network load**

   In low\-traffic scenarios, such as file sharing or basic web services, servers may use memory unnecessarily because of a high memory reclamation threshold. In such cases, you can use the following recommendations:

   * `min`: Set this parameter to a relatively low value to lower the threshold for triggering memory reclamation and avoid unnecessary memory usage.

   * `pressure`: Set this parameter to 4/3 times the value of the `min` parameter.

   * `max`: Set this parameter to twice the value of the `pressure` parameter.


<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure


<Tabs>
<Tab zoneid="gp7BbYaHUm" title="Configuration by using the proc interface">
<TabTitle>Configuration by using the proc interface</TabTitle>

You can use this method to temporarily modify the parameter value while the operating system is running. Each time the instance restarts, you need to configure the parameter again.


1. Log in to the target instance. For more information, see [Logging in to Linux instances](https://docs.byteplus.com/en/docs/ecs/Logging-on-to-a-Linux-instance).

2. Execute the following command on the target Linux instance to view the current value of the `net.ipv4.tcp_mem` parameter.

   ```Plain Text
   cat /proc/sys/net/ipv4/tcp_mem
   ```
   

   Sample output:

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_f23f21d758f65ad1025d09de48fc409e.png) </span>

3. Execute the following command to configure the `net.ipv4.tcp_mem` parameter.

   ```Plain Text
   echo "21198 28265 42396" > /proc/sys/net/ipv4/tcp_mem
   ```
   

   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">Replace <code>21198 28265 42396</code> with the actual value required for your business. For more information, see <a href="https://docs.byteplus.com/en/docs/ecs/Adjust_the_net_ipv4_tcp_mem#.5YWz5LqObmV0LmlwdjQudGNwX21lbeWPguaVsA==">About the net\-ipv4\-tcp\-mem parameter</a>.   </div>
   


</Tab>
<Tab zoneid="xMNJFPCwIW" title="Configuration by using the net_tcp.conf file">
<TabTitle>Configuration by using the net_tcp.conf file</TabTitle>

You can use this method to permanently modify the parameter value while the operating system is running. You do not need to configure the parameter again after the instance restarts.


1. Log in to the target instance. For more information, see [Logging in to Linux instances](https://docs.byteplus.com/en/docs/ecs/Logging-on-to-a-Linux-instance).

2. Execute the following command to view the current parameter value.

   ```Plain Text
   sysctl net.ipv4.tcp_mem
   ```
   

   Sample output:

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_fb41ea0b9605bc91c8baed301b6159f2.png) </span>

3. Modify the value of the `net.ipv4.tcp_mem` parameter.

   1. Execute the following command to create the net_tcp.conf file.

      ```Plain Text
      vim /etc/sysctl.d/net_tcp.conf
      ```
      

   2. Press the `i` key to enter edit mode and add the following content to the end of the file.

      ```Plain Text
      net.ipv4.tcp_mem = 21198 28265 42396
      ```
      

      <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="2">tip      </div>
      

      <div data-tips="true" data-tips-type="default" data-wrapper-indent="2">Replace <code>21198 28265 42396</code> with the actual value required for your business. For more information, see <a href="https://docs.byteplus.com/en/docs/ecs/Adjust_the_net_ipv4_tcp_mem#.5YWz5LqObmV0LmlwdjQudGNwX21lbeWPguaVsA==">About the net\-ipv4\-tcp\-mem parameter</a>.      </div>
      

   3. Press the `Esc` key to exit edit mode, enter `:wq`, and then press Enter to save and exit the file.

4. Execute the following command to make the configuration take effect.

   ```Plain Text
   sysctl -p /etc/sysctl.d/net_tcp.conf
   ```
   


</Tab>
</Tabs>
