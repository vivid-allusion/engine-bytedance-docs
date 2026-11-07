---
title: "Modifying net.ipv4.tcp_slow_start_after_idle parameter in Linux operating system"
product: "Elastic Compute Service"
product_code: "ecs"
source: "https://docs.byteplus.com/en/docs/ecs/tcp_slow_start_after_idle"
---

This topic describes how to configure the `net.ipv4.tcp_slow_start_after_idle` parameter in the Linux operating system.

<span id=".5YWz5LqObmV0LmlwdjQudGNwX3Nsb3dfc3RhcnRfYWZ0ZXJfaWRsZeWPguaVsA=="></span>
## About the net.ipv4.tcp_slow_start_after_idle parameter

This parameter is used to control the behavior of a TCP connection when it is reactivated after being idle for a period of time. By default, the value of this parameter in the Linux kernel is `1`, which means the TCP connection will immediately enter the slow start phase upon reactivation. If the value is `0`, the TCP connection will not enter the slow start phase and will directly enter the congestion avoidance phase when reactivated.

<span id=".5pON5L2c5Zy65pmv"></span>
## Applicable scenario


* **Scenarios with relatively light network load**

   In cases of light network load, you can set this parameter to `0`. This avoids every request going through the slow start process, reduces the congestion window when reactivating connections, and improves network transmission speed.

* **Scenarios with relatively heavy network load**

   In cases of heavy network load, you can set this parameter to `1` to avoid network congestion as much as possible.


<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure


<Tabs>
<Tab zoneid="IPsdme6Qy8" title="Configuration by using the proc interface">
<TabTitle>Configuration by using the proc interface</TabTitle>

You can use this method to temporarily modify the parameter value while the operating system is running. Each time the instance restarts, you need to configure the parameter again.


1. Log in to the target instance. For more information, see [Logging in to Linux instances](https://docs.byteplus.com/en/docs/ecs/Logging-on-to-a-Linux-instance).

2. Execute the following command on the target Linux instance to view the current value of the `tcp_slow_start_after_idle` parameter.

   ```Plain Text
   cat /proc/sys/net/ipv4/tcp_slow_start_after_idle
   ```
   

3. Execute the following command to configure the `tcp_slow_start_after_idle` parameter.

   ```Plain Text
   echo 0 > /proc/sys/net/ipv4/tcp_slow_start_after_idle
   ```
   

   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">Replace 0 with the required value. Value:   </div>
   

   * <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">0: When a TCP connection is reactivated, it will not enter the slow start phase and will directly enter the congestion avoidance phase.   </div>
   

   * <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">1: When a TCP connection is reactivated, it will immediately enter the slow start phase.   </div>
   


</Tab>
<Tab zoneid="VBASoSOUni" title="Configuration by using the net_tcp.conf file">
<TabTitle>Configuration by using the net_tcp.conf file</TabTitle>

You can use this method to permanently modify the parameter value while the operating system is running. You do not need to configure the parameter again after the instance restarts.


1. Log in to the target instance. For more information, see [Logging in to Linux instances](https://docs.byteplus.com/en/docs/ecs/Logging-on-to-a-Linux-instance).

2. Execute the following command to view the current parameter value.

   ```Plain Text
   sysctl net.ipv4.tcp_slow_start_after_idle
   ```
   

   Sample output:

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_e5be8bf985b7b19bbbb69942151f541a.png) </span>

3. Modify the value of the `somaxconn` parameter.

   1. Execute the following command to create the net_tcp.conf file.

      ```Plain Text
      vim /etc/sysctl.d/net_tcp.conf
      ```
      

   2. Press the `i` key to enter edit mode and add the following content to the end of the file.

      ```Plain Text
      net.ipv4.tcp_slow_start_after_idle = 0
      ```
      

      <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="2">tip      </div>
      

      <div data-tips="true" data-tips-type="default" data-wrapper-indent="2">Replace 0 with the required value. Valid values:      </div>
      

      * <div data-tips="true" data-tips-type="default" data-wrapper-indent="2">0: When a TCP connection is reactivated, it will not enter the slow start phase and will directly enter the congestion avoidance phase.      </div>
      

      * <div data-tips="true" data-tips-type="default" data-wrapper-indent="2">1: When a TCP connection is reactivated, it will immediately enter the slow start phase.      </div>
      

   3. Press the `Esc` key to exit edit mode, enter `:wq`, and then press Enter to save and exit the file.

4. Execute the following command to make the configuration take effect.

   ```Plain Text
   sysctl -p /etc/sysctl.d/net_tcp.conf
   ```
   


</Tab>
</Tabs>
