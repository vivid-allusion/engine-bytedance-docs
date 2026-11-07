---
title: "Enabling or disabling the system firewall on a Linux instance"
product: "Elastic Compute Service"
product_code: "ecs"
source: "https://docs.byteplus.com/en/docs/ecs/Enable_or_Disable_the_system_firewall_in_the_Linux_instance"
---

This topic describes how to enable or disable the system firewall on a Linux instance.


> * A firewall is a technology that builds a relatively isolated protective barrier between the internal network and external network of a computer (instance), thereby protecting data and information.

> * If the instance has the firewall enabled and has configured rules to block external access, remote connection to the instance may fail.


<span id=".5YmN5o-Q5p2h5Lu2"></span>
## **Prerequisites**

To modify the configuration or data of an instance, we recommend that you [create a snapshot](https://docs.byteplus.com/en/docs/ecs/Create-a-snapshot) to improve fault tolerance and ensure data security.

<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure


1. Log in to the target instance. For operation details, refer to [Logging in to Linux instances](https://docs.byteplus.com/en/docs/ecs/Logging-on-to-a-Linux-instance).

2. Commands to enable or disable the firewall vary based on the Linux system version. Select the corresponding command for your system.

   * **CentOS 5 and CentOS 6**

      ```Plain Text
      # Enable the firewall
      service iptables start
      # Disable the firewall
      service iptables stop
      # Check firewall running status
      service iptables status
      ```
      

   * **CentOS 7/Red Hat 7**

      ```Plain Text
      # Enable the firewall
      systemctl start firewalld.service
      # Disable the firewall
      systemctl stop firewalld.service
      # Check firewall running status
      firewall-cmd --state
      ```
      

   * **Ubuntu**

      ```Plain Text
      # Enable the firewall
      ufw enable
      # Disable the firewall
      ufw disable
      # Check firewall running status
      ufw status
      ```
      

   * **Debian**

      In Debian systems, you can clear a firewall policy to delete the related blocking rule. The steps are as follows:

      1. Execute the following commands in sequence to back up the firewall policy.

         ```Plain Text
         touch [$Iptables]
         iptables-save > [$Iptables]
         
         ```
         

         <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="3">tip         </div>
         

         <div data-tips="true" data-tips-type="tip" data-wrapper-indent="3">[$Iptables] is the backup file address of a firewall policy. Before you clear the firewall policy, back up the policy first.         </div>
         

      2. Execute the following command to clear the firewall policy.

         ```Plain Text
         iptables -F
         ```
