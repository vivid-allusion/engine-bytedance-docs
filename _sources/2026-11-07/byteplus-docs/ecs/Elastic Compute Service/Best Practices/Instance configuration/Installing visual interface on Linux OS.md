---
title: "Installing visual interface on Linux OS"
product: "Elastic Compute Service"
product_code: "ecs"
source: "https://docs.byteplus.com/en/docs/ecs/Install-a-GUI-in-Linux"
---

The public images provided by BytePlus do not have graphical desktop components installed by default. You can refer to this topic for installation instructions.

<span id=".5rOo5oSP5LqL6aG5"></span>
## Considerations


* The ECS instance is in the ** Running ** state.

* If the visual interface is installed improperly, you may fail to start the instance. Therefore, please [back up data](https://docs.byteplus.com/en/docs/ecs/Disaster_recovery_and_restoration) in advance.

* A graphical desktop uses system resources (such as memory, CPU, and disk space), which may lead to a decline in instance performance.


<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure


<Tabs>
<Tab zoneid="wLH5lcv77S" title="CentOS">
<TabTitle>CentOS</TabTitle>

This section uses CentOS 7.9 as an example to describe how to install the GUI.


1. Log in to the target Linux\-based instance. For more information, refer to [Logging in to Linux instances](https://docs.byteplus.com/en/docs/ecs/Logging-on-to-a-Linux-instance).

2. Execute the following command to update the software list.


```Bash
sudo yum update -y
```



3. Execute the following command to install X Window.


```Bash
sudo yum groupinstall "X Window System" -y
```



4. Execute the following command to install the GNOME desktop environment.


```Bash
sudo yum groupinstall "GNOME Desktop" --skip-broken -y
```



5. Execute the following command to set the system to start the graphical interface by default on startup.


```Bash
sudo systemctl set-default graphical.target
```



6. Execute the following command to restart the instance.


```Bash
reboot
```



7. Log in to the instance again via VNC to access the GUI. For detailed operations, refer to [Using the console to log in to a Linux instance](https://docs.byteplus.com/en/docs/ecs/Using-the-console-to-log-on-to-a-Linux-instance).

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_59df6cd1f93ceea977b56077bb30ce9a.png) </span>


</Tab>
<Tab zoneid="WecQTW9E8L" title="Ubuntu">
<TabTitle>Ubuntu</TabTitle>

In the example provided in this section, Ubuntu Server 22.04 LTS is used to install GUI interface.


1. Log in to the target Linux\-based instance. For more information, refer to [Logging in to Linux instances](https://docs.byteplus.com/en/docs/ecs/Logging-on-to-a-Linux-instance).

2. Execute the following command to update the software list.


```Bash
sudo apt-get update -y
```



3. Execute the following command to install the GNOME desktop environment.


```Bash
sudo apt-get install ubuntu-desktop -y
```



4. Execute the following command to restart the instance.


```Bash
reboot
```



5. Log in to the instance again via VNC to access the GUI. For detailed operations, refer to [Using the console to log in to a Linux instance](https://docs.byteplus.com/en/docs/ecs/Using-the-console-to-log-on-to-a-Linux-instance).

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_04eaf056e49132cad81697bff53731de.png) </span>


</Tab>
<Tab zoneid="iovX1epylP" title="Debian">
<TabTitle>Debian</TabTitle>

In the example provided in this section, Debian 10 is used to install GUI interface.


1. Log in to the target Linux\-based instance. For more information, refer to [Logging in to Linux instances](https://docs.byteplus.com/en/docs/ecs/Logging-on-to-a-Linux-instance).

2. Execute the following command to update the software list.


```Bash
sudo apt-get update -y
```



3. Execute the following command to install the GNOME desktop environment.


```Bash
sudo apt-get install task-gnome-desktop -y
```



4. Execute the following command to restart the instance.


```Bash
reboot
```



5. Log in to the instance again via VNC to access the GUI. For detailed operations, refer to [Using the console to log in to a Linux instance](https://docs.byteplus.com/en/docs/ecs/Using-the-console-to-log-on-to-a-Linux-instance).

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_6ef6aa79ddfeea096031c5cfcb469da9.png) </span>


</Tab>
</Tabs>
