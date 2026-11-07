---
title: "Configuring Chrony service for Linux instances (CentOS 7)"
product: "Elastic Compute Service"
product_code: "ecs"
source: "https://docs.byteplus.com/en/docs/ecs/Configure-the-Chrony-service-for-Linux"
---

This topic describes how to modify the time zone of a Linux ECS instance, as well as how to enable, configure, and use the Chrony service to ensure accurate local time synchronization for the instance. In the example provided in this topic, CentOS 7.9 is used.

<span id=".5YWz5LqOIENocm9ueQ=="></span>
## About Chrony

Chrony is a general\-purpose implementation of the Network Time Protocol (NTP). In CentOS 7, you can use the Chrony tool to synchronize the local time with standard time, minimizing time and frequency discrepancies to the greatest extent possible. Chrony is also particularly useful for systems that do not run continuously or operate on virtual machines. For more information, see [Chrony](https://chrony.tuxfamily.org/index.html).

<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites


* CentOS 7 comes with Chrony preinstalled. If not, install it by executing the `yum install chrony -y` command.

* Chrony uses the User Datagram Protocol (UDP) to send and receive timestamps over port 123. Make sure that an inbound rule is added to the security group of the instance to allow inbound traffic on UDP port 123. For more information, see [Creating a security group](https://docs.byteplus.com/en/docs/vpc/Creating-a-security-group).


<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure

<span id=".5L-u5pS5TGludXjns7vnu5_lrp7kvovml7bljLo="></span>
### Modify the time zone of a Linux instance


1. Connect to the Linux instance. For more information, refer to [Logging in to Linux instances](https://docs.byteplus.com/en/docs/ecs/Using-the-console-to-log-on-to-a-Linux-instance).

2. Execute the following command to view the list of time zones.

   ```Plain Text
   ls /usr/share/zoneinfo/<时区文件夹名称>
   ```
   

   For example, you can execute the following command to view the list of time zones in Asia.

   ```Plain Text
   ls /usr/share/zoneinfo/Asia
   ```
   

3. Execute the following command to modify the time zone. In the example provided in this topic, the time zone is changed to `Shanghai`.

   ```Plain Text
   ln -sf /usr/share/zoneinfo/Asia/Shanghai /etc/localtime
   ```
   

4. Execute the following command to update the Real\-Time Clock (RTC).

   ```Plain Text
   hwclock -w
   ```
   

5. Execute the following command to view the time zone.

   ```Plain Text
   timedatectl status
   ```
   

6. If the following query result is displayed, the time zone is changed to `Shanghai`.

   ```Plain Text
   Local time: Sat 2022-10-08 03:26:16 UTC 
   Universal time: Sat 2022-10-08 03:26:16 UTC
         RTC time: Sat 2022-10-08 03:26:16
        Time zone: Asia/Shanghai (UTC, +0800)
   ```
   


<span id=".5ZCv55SoQ2hyb2555pyN5Yqh"></span>
### Enable the Chrony service


1. Connect to the Linux instance. For more information, refer to [Logging in to Linux instances](https://docs.byteplus.com/en/docs/ecs/Using-the-console-to-log-on-to-a-Linux-instance).

2. Execute the following commands to start the chronyd service and specify that the service automatically starts upon instance startup.

   ```Plain Text
   systemctl start chronyd.service
   systemctl enable chronyd.service
   ```
   

3. Execute the following command to view the time synchronization status of the ECS instance and verify whether the service is started.

   ```Plain Text
   chronyc tracking
   ```
   

4. Execute the following command to view the list of time synchronization servers.

   ```Plain Text
   chronyc -n sources -v
   ```
   


<span id=".6YWN572uQ2hyb2555pyN5Yqh"></span>
### Configure the Chrony service


1. Connect to the Linux instance. For more information, refer to [Logging in to Linux instances](https://docs.byteplus.com/en/docs/ecs/Using-the-console-to-log-on-to-a-Linux-instance).

2. Execute the following command to open the chrony configuration file. For more information about the chrony.conf file, see [chrony.conf](https://chrony.tuxfamily.org/doc/3.4/chrony.conf.html).

   ```Plain Text
   vim /etc/chrony.conf
   ```
   

3. Press the `i` key to start editing the file. Delete any unnecessary NTP server lines, or add a `#` at the beginning of the lines to comment them out.

4. Add the required NTP servers. After you complete the editing, press the `Esc` key to exit edit mode, enter `:wq`, and then press Enter to save and exit the file.

   ```Plain Text
   server ntp0.ivolces.com minpoll 4 maxpoll 10 iburst
   server ntp1.ivolces.com minpoll 4 maxpoll 10 iburst
   server ntp2.ivolces.com minpoll 4 maxpoll 10 iburst
   server ntp3.ivolces.com minpoll 4 maxpoll 10 iburst
   ```
   

5. Execute the following commands to start the chronyd service and specify that the service automatically starts upon instance startup.

   ```Plain Text
   systemctl start chronyd.service
   systemctl enable chronyd.service
   ```
   

6. Execute the following command to view the list of time synchronization servers.

   ```Plain Text
   chronyc -n sources -v
   ```
   


<span id=".5L2_55SoQ2hyb2555omL5Yqo5ZCM5q2l5pe26ZKf"></span>
### Manually synchronize the clock by using Chrony


1. Connect to the Linux instance. For more information, refer to [Logging in to Linux instances](https://docs.byteplus.com/en/docs/ecs/Using-the-console-to-log-on-to-a-Linux-instance).

2. Execute the following command to enter the Chrony tool.

   ```Plain Text
   chronyc
   ```
   

3. In the Chrony tool, execute the following command to synchronize the clock.

   > You can execute the `help` command to obtain usage instructions for common Chrony commands.   
   

   ```Plain Text
   makestep
   ```
