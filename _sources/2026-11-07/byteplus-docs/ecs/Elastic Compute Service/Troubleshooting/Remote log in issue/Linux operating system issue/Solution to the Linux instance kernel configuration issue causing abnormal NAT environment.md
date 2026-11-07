---
title: "Solution to the Linux instance kernel configuration issue causing abnormal NAT environment access to the instance"
product: "Elastic Compute Service"
product_code: "ecs"
source: "https://docs.byteplus.com/en/docs/ecs/Linux_solution_to_NAT_environment_access_instance_exception_caused_by_kernel_configuration_problem"
---

You can resolve issues caused by abnormal kernel parameter configurations in a NAT environment by fixing the `tcp_tw_recycle` and `tcp_timestamps` parameters. These issues include failure to connect to the instance via SSH, abnormalities when you access HTTP services on the instance, and connection resets when you use the telnet command for network testing.

<span id="kHMdC5yR"></span>
### Causes

Due to the local network accessing the internet via NAT sharing and abnormal Linux system\-related kernel argument configuration, the involved abnormal kernel arguments include `tcp_tw_recycle` and `tcp_timestamps`.

<span id="2MP5oWbT"></span>
### Procedure


1. Log in to the target instance. For operation details, refer to [Logging in to Linux instances](https://docs.byteplus.com/en/docs/ecs/Overview-1).

2. Execute the following commands in sequence to view whether the current kernel configuration is normal.

   ```Plain Text
   cat /proc/sys/net/ipv4/tcp_tw_recycle
   cat /proc/sys/net/ipv4/tcp_timestamps
   ```
   

   * If the result is `1`, the configuration is abnormal. Follow the following steps to fix the `tcp_tw_recycle` and `tcp_timestamps` parameters.

   * If the result is `0`, the configuration is normal. There is no need to fix the `tcp_tw_recycle` and `tcp_timestamps` parameters.  contact your account manager for technical support.

3. Execute the following command to add kernel arguments in the `/etc/sysctl.conf` configuration file.

   ```Plain Text
   net.ipv4.tcp_tw_recycle=0
   net.ipv4.tcp_timestamps=0
   ```
   

4. Execute the following command to make the configuration take effect.

   ```JavaScript
   sysctl -p
   ```
