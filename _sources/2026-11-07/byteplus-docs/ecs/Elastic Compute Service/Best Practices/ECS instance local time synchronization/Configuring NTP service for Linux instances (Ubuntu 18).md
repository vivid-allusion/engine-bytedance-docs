---
title: "Configuring NTP service for Linux instances (Ubuntu 18)"
product: "Elastic Compute Service"
product_code: "ecs"
source: "https://docs.byteplus.com/en/docs/ecs/Configure-the-NTP-service-for-Linux"
---

This topic describes how to modify the time zone of a Linux instance, as well as how to enable and configure the Linux NTP service to ensure accurate local time synchronization of the instance. In the example provided in this topic, Ubuntu 18.04 is used.

<span id=".5LuA5LmI5pivTlRQ77yf"></span>
## What is NTP?

Network Time Protocol (NTP) is an application\-layer protocol in the TCP/IP protocol suite, designed for clock synchronization between clients and servers and providing highly accurate time calibration.

<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites


* If NTP is not installed, execute the following command to install it.

   ```Bash
   sudo apt-get update
   sudo apt-get install ntp
   ```
   

* The NTP service uses the User Datagram Protocol (UDP) to send and receive timestamps over port 123. Make sure that an inbound rule is added to the security group of the instance to allow inbound traffic on UDP port 123. For more information, see [Creating a security group](https://docs.byteplus.com/en/docs/vpc/Creating-a-security-group).


<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure

<span id=".5L-u5pS5TGludXjlrp7kvovml7bljLo="></span>
### Modify the time zone of a Linux instance


1. Connect to the Linux instance. For more information, refer to [Logging in to Linux instances](https://docs.byteplus.com/en/docs/ecs/Using-the-console-to-log-on-to-a-Linux-instance).

   > You need to modify the time zone as the root account. Therefore, use the `sudo` command.   
   

2. Execute the `timedatectl list-timezones` command to view the list of available time zones.

   > You can also quickly view the list of available time zones in a continent. For example, you can execute the `timedatectl list-timezones | egrep -o "Asia/*.*"` command to quickly find available time zones in Asia.   
   

3. Execute the following command to modify the time zone. In the example provided in this topic, the time zone is changed to `Shanghai`.

   ```Plain Text
   timedatectl set-timezone "Asia/Shanghai"
   ```
   

4. Execute the following command to view the current time zone and check whether the modification is successful.

   ```Plain Text
   timedatectl status | grep Time
   ```
   

   Sample output:

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_1ce56bdd9ad0cfdaeaeabfb31b51edf2.png) </span>


<span id=".5ZCv5Yqo5qCH5YeGTlRQ5pyN5Yqh"></span>
### Start the standard NTP service


1. Connect to the Linux instance. For more information, refer to [Logging in to Linux instances](https://docs.byteplus.com/en/docs/ecs/Using-the-console-to-log-on-to-a-Linux-instance).

2. Execute the `sudo systemctl restart ntp` command to start the NTP service.

3. Execute the `systemctl enable ntp` command to specify that the NTP service automatically starts upon instance startup.

4. Execute the `sudo systemctl status ntp` command to view the running status of the NTP service.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_b60dc0f8d207fd8a56356203574e654a.png) </span>

5. Execute the `ntpq -p` command to view the list of NTP service peers (optional).


<span id=".6YWN572u6Ieq5a6a5LmJTlRQ5pyN5Yqh"></span>
### Configure custom NTP service


1. Connect to the Linux instance. For more information, refer to [Logging in to Linux instances](https://docs.byteplus.com/en/docs/ecs/Using-the-console-to-log-on-to-a-Linux-instance).

2. Execute the `sudo vim /etc/ntp.conf` command to open and edit the NTP service configuration file.

3. Enter `i` to start editing the file, and add `#` to the beginning of the NTP server lines that you currently do not need to comment them out.

4. Add the NTP server information in the following format: `server <NTP_server_address> iburst`. After you complete the editing, press the `Esc` key to exit the edit mode, enter `:wq`, and then press Enter to save the changes and exit the file.

5. Execute the `sudo systemctl restart ntp` command to start the custom NTP service.

6. Execute the `sudo systemctl status ntp` command to view the running status of the NTP service.

7.  **(Optional)**  Execute the `ntpq -p` command to view the list of NTP service peers.
