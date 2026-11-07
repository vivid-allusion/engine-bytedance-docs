---
title: "Tuning net.ipv4.tcp_max_tw_buckets parameter in Linux operating system"
product: "Elastic Compute Service"
product_code: "ecs"
source: "https://docs.byteplus.com/en/docs/ecs/net_ipv4_tcp_max_tw_buckets"
---

This topic describes how to modify the value of the `net.ipv4.tcp_max_tw_buckets` parameter in the Linux operating system.

<span id=".5YWz5LqObmV0LmlwdjQudGNwX21heF90d19idWNrZXRz5Y-C5pWw"></span>
## About the net.ipv4.tcp_max_tw_buckets parameter

This parameter specifies the maximum number of socket connections in the `TIME_WAIT` state that the system can maintain simultaneously. By default, its value is calculated as total memory (in MB) multiplied by 4. When the number of connections in the `TIME_WAIT` state within an instance exceeds the upper limit, the kernel closes the excess TCP connections and displays a warning message `TCP: time wait bucket table overflow` in the /var/log/messages log.

<span id=".5pON5L2c5Zy65pmv"></span>
## Applicable scenario

The number of TCP connections varies across different business scenarios. To avoid resource waste and prevent business interruptions, you can modify the value of the `net.ipv4.tcp_max_tw_buckets` parameter based on your actual needs.


* If your business involves a large number of TCP connections with many in the `TIME_WAIT` state, you can try increasing the value of this parameter.

* If your business sees an unusually high number of TCP connections in the `TIME_WAIT` state, which leads to slow system performance, service lag, or even business disruptions, you can try lowering the value of this parameter.


<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure

<span id=".5q2l6aqk5LiA77ya5p-l6K-i5b2T5YmN5Y-C5pWw5YC8"></span>
### Step 1: Query the current parameter value

Execute the following command on the target Linux instance to check the current system configuration for the maximum number of TCP connections that can simultaneously be in the `TIME_WAIT` state.

```Plain Text
cat /proc/sys/net/ipv4/tcp_max_tw_buckets
```


If the following output is displayed, the current maximum number of TCP connections that can simultaneously be in the `TIME_WAIT` state is `5000`.

<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_39ff11bf5e21ae8412874176fd757b0f.png) </span>

<span id=".5q2l6aqk5LqM77ya5p-l6K-i5Y-v6YWN572u6IyD5Zu0"></span>
### Step 2: Query the configurable range of the parameter

Execute the following command on the target Linux instance to query the range of ports that Linux randomly assigns.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">The theoretical maximum number of randomly assigned ports available externally on Linux is <code>65535</code>. Excluding reserved and occupied ports, the actual available number is approximately <code>60000</code>. Therefore, the value of the <code>tcp_max_tw_buckets</code> parameter should not exceed this available range.</div>


```Plain Text
cat /proc/sys/net/ipv4/ip_local_port_range
```


If the following output is displayed, the available port range is `[32768, 60999]`. The theoretical maximum configurable value for the `net.ipv4.tcp_max_tw_buckets` parameter is `60999 - 32768 + 1 = 28238`.

<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_f919efb12d6ddb78453b624bee2f147a.png) </span>

<span id=".5q2l6aqk5LiJ77ya5L-u5pS55Y-C5pWw6YWN572u"></span>
### Step 3: Modify the parameter configuration

<span id=".5pa55byP5LiA77ya6YCa6L-HcHJvY-aOpeWPo-mFjee9rg=="></span>
#### Method 1: Configuration by using the proc interface

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">This method allows configuration changes to be made and applied while the system is running. However, the configuration will reset after an operating system restart and must be reconfigured.</div>


* <div data-tips="true" data-tips-type="tip">Replace <code>20000</code> in the command with your desired maximum number of TCP connections that can simultaneously be in the <code>TIME_WAIT</code> state.</div>


1. Execute the following command on the target Linux instance to temporarily configure the `net.ipv4.tcp_max_tw_buckets` parameter by using the proc interface.

   ```Plain Text
   echo 20000 > /proc/sys/net/ipv4/tcp_max_tw_buckets
   ```
   

2. Execute the following command to view the current parameter value.

   ```Plain Text
   cat /proc/sys/net/ipv4/tcp_max_tw_buckets
   ```
   


<span id=".5pa55byP5LqM77ya6YCa6L-Hc3lzY3RsLmNvbmbmlofku7bphY3nva4="></span>
#### Method 2: Configuration by using the sysctl.conf file

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">This method allows configuration changes to be made and applied while the system is running. The configuration changes remain effective after the operating system restarts and no reconfiguration is required.</div>


* <div data-tips="true" data-tips-type="tip">Replace <code>20000</code> in the command with your desired maximum number of TCP connections that can simultaneously be in the <code>TIME_WAIT</code> state.</div>


1. Execute the following command on the target Linux instance to open the sysctl.conf file.

   ```Plain Text
   vim /etc/sysctl.conf
   ```
   

2. Press the `i` key to enter edit mode.

3. Modify the value of the `net.ipv4.tcp_max_tw_buckets` parameter in the file.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_0d7496a2a256422dc53d5f3cde2d9b81.png) </span>

4. Press `Esc`, enter `:wq`, and then press Enter to save and close the file.

5. Execute the following command to make the configuration take effect.

   ```Plain Text
   sysctl -p
   ```
   

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_d68e31fbcffc0dbd0868996d72a41bf3.png) </span>
