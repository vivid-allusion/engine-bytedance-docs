---
title: "Solution for network unavailability on Linux systems"
product: "Elastic Compute Service"
product_code: "ecs"
source: "https://docs.byteplus.com/en/docs/ecs/Network_Non-existence_Handling_Method_for_Linux_System"
---

This topic describes the solution for network disconnection on a Linux system due to failure to renew IP leases when corresponding network processes are missing under the DHCP configuration.

<span id=".5YmN5o-Q5p2h5Lu2"></span>
## **Prerequisites**

Before you modify the configuration or data of an instance, we recommend that you [create a snapshot](https://docs.byteplus.com/en/docs/ecs/Create-a-snapshot) to improve fault tolerance and ensure data security.

<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure


1. Log in to the target instance. For operation details, refer to [Logging in to Linux instances](https://docs.byteplus.com/en/docs/ecs/Logging-on-to-a-Linux-instance).

2. Execute the `ps -ef |grep [$network process]` command to check whether the network process exists. If the corresponding network process does not exist, this indicates a potential risk. Continue with the following operations.

   Corresponding network processes (network configuration method: DHCP) are as follows:

   
   |OS version |Network process |
   |---|---|
   |CentOS 6/7 |/sbin/dhclient |
   |Debian 8/9/10 ||
   |Ubuntu 14/16 ||
   |CentOS 8 |/usr/sbin/NetworkManager |
   |Ubuntu 18/20 |/lib/systemd/systemd\-networkd |
   |SUSE Linux |/usr/lib/wicked/bin/wickedd\-dhcp4 |
   

3. Execute one of the following commands to restart the network service.

   Network service names vary across Linux systems and even between versions of the same system. Specific network names and commands to restart them are as follows:

   <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="1">warning   </div>
   

   <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">Restarting the network service may cause short\-term network disruption and impact business operations. Restart the network service at an appropriate time.   </div>
   

   
   |OS |Version |Network service |Command to restart network service |
   |---|---|---|---|
   |CentOS |6 |Network |service network restart |
   ||7 |Network |service network restart |
   ||8 |NetworkManager |systemctl restart NetworkManager |
   |Debian |8 |networking |systemctl restart networking |
   ||9 |networking |systemctl restart networking |
   ||10 |networking |systemctl restart networking |
   |Ubuntu |14 |networking |service networking restart |
   ||16 |networking |systemctl restart networking |
   ||18 |systemd\-networkd |systemctl restart systemd\-networkd |
   ||20 |systemd\-networkd |systemctl restart systemd\-networkd |
