---
title: "Modifying net.core.somaxconn parameter in Linux operating system"
product: "Elastic Compute Service"
product_code: "ecs"
source: "https://docs.byteplus.com/en/docs/ecs/net-core-somaxconn"
---

This topic describes how to modify the `net.core.somaxconn` parameter in the Linux operating system.

<span id=".5YWz5LqObmV0LmNvcmUuc29tYXhjb25u5Y-C5pWw"></span>
## About the net.core.somaxconn parameter

This parameter specifies the maximum capacity of the connection queue. That is, the maximum number of connections allowed to wait in the queue. When the server receives new connection requests, they are temporarily stored in the connection queue, pending acceptance by the server program via the `accept` function. Increasing the value of this parameter can theoretically boost the number of new concurrent TCP connections.

<span id=".5pON5L2c5Zy65pmv"></span>
## Applicable scenario

If you need to increase the maximum number of clients a server can handle, you may try raising this value.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">The tcp_max_syn_backlog parameter specifies the maximum number of half\-open connections, which affects the number of new concurrent TCP connections.</div>


<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure


<Tabs>
<Tab zoneid="OtDCNdoI0X" title="Configuration by using the proc interface">
<TabTitle>Configuration by using the proc interface</TabTitle>

You can use this method to temporarily modify the parameter value while the operating system is running. Each time the instance restarts, you need to configure the parameter again.


1. Log in to the target instance. For more information, see [Logging in to Linux instances](https://docs.byteplus.com/en/docs/ecs/Logging-on-to-a-Linux-instance).

2. Execute the following command on the target Linux instance to view the parameter value.

   ```Plain Text
   cat /proc/sys/net/core/somaxconn
   ```
   

3. Execute the following command to specify a value for the `net.core.somaxconn` parameter.

   ```Plain Text
   echo 4096 > /proc/sys/net/core/somaxconn
   ```
   

   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">Replace <code>4096</code> with the required value.   </div>
   


</Tab>
<Tab zoneid="onS0cNNXVZ" title="Configuration by using the net_tcp.conf file">
<TabTitle>Configuration by using the net_tcp.conf file</TabTitle>

You can use this method to permanently modify the parameter value while the operating system is running. You do not need to configure the parameter again after the instance restarts.


1. Log in to the target instance. For more information, see [Logging in to Linux instances](https://docs.byteplus.com/en/docs/ecs/Logging-on-to-a-Linux-instance).

2. Execute the following command to view the current parameter value.

   ```Plain Text
   sysctl net.core.somaxconn
   ```
   

   Sample output:

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_6a22185ae5191fd8d9d460cddf0f1758.png) </span>

3. Modify the value of the `net.core.somaxconn` parameter.

   1. Execute the following command to create the net_tcp.conf file.

      ```Plain Text
      vim /etc/sysctl.d/net_tcp.conf
      ```
      

   2. Press the `i` key to enter edit mode, and add the following content to the configuration file.

      ```Plain Text
      net.core.somaxconn=4096
      ```
      

      <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="2">tip      </div>
      

      <div data-tips="true" data-tips-type="default" data-wrapper-indent="2">Replace <code>4096</code> with the required value.      </div>
      

   3. Press the `Esc` key to exit edit mode, enter `:wq`, and then press Enter to save and exit the file.

4. Execute the following command to make the configuration take effect.

   ```Plain Text
   sysctl -p /etc/sysctl.d/net_tcp.conf
   ```
   


</Tab>
</Tabs>
