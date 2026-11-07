---
title: "Login and connection FAQ"
product: "Elastic Compute Service"
product_code: "ecs"
source: "https://docs.byteplus.com/en/docs/ecs/Logon-and-connection-FAQs"
---


|Category |Question |
|---|---|
|Login username |[Why am I unable to log in to an instance by using the root account?](https://docs.byteplus.com/en/docs/ecs/Logon-and-connection-FAQs#.5Li65LuA5LmI5peg5rOV5L2_55Socm9vdOeUqOaIt-eZu-W9leWunuS-i--8nw==) |
|Login port |* [What ports need to be opened to log in to an instance?](https://docs.byteplus.com/en/docs/ecs/Logon-and-connection-FAQs#.55m75b2V5a6e5L6L6ZyA6KaB5pS-6YCa5LuA5LmI56uv5Y-j77yf)<br><br>* [Why do I fail to connect to a Windows ECS instance via a certain port?](https://developer.volcengine.com/articles/7270815832781897765)<br><br>* [Why can an ECS instance be pinged successfully but the port is unreachable?](https://developer.volcengine.com/articles/7077451232066928654)<br><br>* [Why can't I connect to my instance even after opening the port?](https://docs.byteplus.com/en/docs/ecs/Logon-and-connection-FAQs#.5Li65LuA5LmI5pS-6YCa5LqG56uv5Y-j5LuN5peg5rOV6L-e5o6l5a6e5L6L77yf)<br><br>* [How do I modify the remote login port?](https://docs.byteplus.com/en/docs/ecs/How-to-modify-the-default-remote-port-of-an-ECS-instance) |
|Login password |* [What do I do if I forget the instance password and want to recover it?](https://docs.byteplus.com/en/docs/ecs/Logon-and-connection-FAQs#.5b-Y6K6w5LqG5a6e5L6L55qE5a-G56CB77yM5aaC5L2V5oGi5aSN77yf)<br><br>* [How do I resolve the issue where a user account on a Windows instance becomes locked due to multiple login attempts with incorrect passwords?](https://docs.byteplus.com/en/docs/ecs/Method_for_adjusting_the_account_lockout_policy_threshold_for_Windows_instances) |
|Multi\-user login |* [Can multiple users remotely log in to the same ECS instance at the same time via VNC?](https://docs.byteplus.com/en/docs/ecs/Logon-and-connection-FAQs#.6YCa6L-HVk5D6L-c56iL55m75b2V5p-Q5Y-w5LqR5pyN5Yqh5Zmo5a6e5L6L77yM5pSv5oyB5aSa55So5oi35ZCM5pe255m75b2V5ZCX77yf) |
|Login tool |* [Can I log in to an ECS instance via a mobile phone?](https://docs.byteplus.com/en/docs/ecs/Logon-and-connection-FAQs#.5piv5ZCm5Y-v5Lul6YCa6L-H5omL5py655m75b2V5LqR5pyN5Yqh5Zmo77yf)<br><br>* [Can I log in to an instance via a self-built web page in an external system?](https://docs.byteplus.com/en/docs/ecs/Logon-and-connection-FAQs#FT8sib3T) |
|Query login records |[How do I query the login information of an ECS instance?](https://developer.volcengine.com/articles/7270815820761169957) |
|Connection failure |* [Why does the remote connection to my instance frequently disconnect?](https://docs.byteplus.com/en/docs/ecs/Logon-and-connection-FAQs#.5Li65LuA5LmI6L-c56iL6L-e5o6l5a6e5L6L57uP5bi45pat5byA77yf)<br><br>* [Why cannot I access an instance from the public network?](https://docs.byteplus.com/en/docs/ecs/Logon-and-connection-FAQs#.5Li65LuA5LmI6L-c56iL6L-e5o6l5a6e5L6L57uP5bi45pat5byA77yf) |
|SSH remote issues |[What do I do if the session is automatically disconnected after being inactive for a certain period of time after I log in to the instance via SSH?](https://docs.byteplus.com/en/docs/ecs/Logon-and-connection-FAQs#.U1NI55m75b2V5pyN5Yqh5Zmo5ZCO77yM5LiA5a6a5pe26Ze05LiN5pON5L2c5Lya6Ieq5Yqo5pat5byA5Lya6K-d5aaC5L2V5aSE55CG77yf) |
|VNC issues |[How do I set VNC full-screen display?](https://docs.byteplus.com/en/docs/ecs/Logon-and-connection-FAQs#.5aaC5L2V6K6-572uVk5D5YWo5bGP5pi-56S677yf) |
|Close remote connection |[Will the ECS instance shut down after I close the remote connection?](https://docs.byteplus.com/en/docs/ecs/Logon-and-connection-FAQs#.5YWz6Zet6L-c56iL6L-e5o6l5ZCO77yM5LqR5pyN5Yqh5Zmo5Lya5YWz5py65ZCX77yf) |


<span id=".5Li65LuA5LmI5peg5rOV5L2_55Socm9vdOeUqOaIt-eZu-W9leWunuS-i--8nw=="></span>
### Why am I unable to log in to an instance by using the root account?

Execute the `vi /etc/ssh/sshd_config` command to check whether `PermitRootLogin` is set to `yes` in the file. Logging in to the instance as the root user is allowed only when `PermitRootLogin` is set to `yes`.

<span id=".55m75b2V5a6e5L6L6ZyA6KaB5pS-6YCa5LuA5LmI56uv5Y-j77yf"></span>
### What ports need to be opened to log in to an instance?

Linux instances use the TCP protocol and port 22 for login by default, while Windows instances use the TCP protocol and port 3389 by default. You can also [modify the default login port](https://docs.byteplus.com/en/docs/ecs/How-to-modify-the-default-remote-port-of-an-ECS-instance) to reduce the risk of being scanned and attacked by malicious software, thereby improving the security of the instance.

<span id=".5Li65LuA5LmI5pS-6YCa5LqG56uv5Y-j5LuN5peg5rOV6L-e5o6l5a6e5L6L77yf"></span>
### Why can't I connect to my instance even after opening the port?

Check whether the port is correctly configured and whether the firewall has been disabled.


|Troubleshooting item |Description |Solution |
|---|---|---|
|Check whether the security group configuration is correct. |To log in to a Linux instance, you need to open the default TCP port 22. |In the ECS console, click the name of the instance you cannot log in to to go to the instance details page, select the "Security Group" tab, and make sure that port 22 is added to the inbound rules of a security group associated with the instance.<br><br>If the port is not added, [modify the security group access rules](https://docs.byteplus.com/en/docs/ecs/Modifying-security-group-rules). |
|Check whether the configuration of the firewall is correct. |Check whether the internal firewall (iptables, firewalld) of the ECS instance is blocking SSH (port 22). |If the instance has the firewall enabled and has configured rules to block external access, remote login to the instance may fail.<br><br>[How do I configure the firewall for a Linux instance?](https://developer.volcengine.com/articles/7270815826700140600)<br><br>[How do I configure the firewall for a Windows ECS instance?](https://docs.byteplus.com/en/docs/ecs/Security-FAQs#.5aaC5L2V6YWN572uIFdpbmRvd3Mg5LqR5pyN5Yqh5Zmo6Ziy54Gr5aKZ77yf) |


<span id=".5b-Y6K6w5LqG5a6e5L6L55qE5a-G56CB77yM5aaC5L2V5oGi5aSN77yf"></span>
### What do I do if I forget the instance password and want to recover it?

You can use the [login password reset](https://docs.byteplus.com/en/docs/ecs/Resetting-passwords) feature of the ECS instance to specify a new password.

<span id=".5aaC5L2V6Kej5YazV2luZG93c-WunuS-i-eUseS6juWkmuasoei-k-WFpemUmeivr-WvhueggeWvvOiHtOiiq-mUgeWumueUqOaIt-i0puWPt--8jOaXoOazleeZu-W9leeahOmXrumimO-8nw=="></span>
### How do I resolve the issue where a user account on a Windows instance becomes locked due to multiple login attempts with incorrect passwords?

When you connect to an ECS instance via Remote Desktop, multiple login attempts with incorrect passwords may result in an error message as shown in the following figure: "The user account has been locked".

<span id=".6Zeu6aKY5YiG5p6Q"></span>
#### Issue analysis


1. The account is locked by the system's security mechanism due to excessive login attempts with incorrect passwords.

2. If the login attempts are not made by the user, it may be caused by someone attempting a brute\-force attack.

3. Generally, this error can be resolved, and normal login will be restored after the specified account lockout duration has elapsed.


<span id=".6Zeu6aKY6Kej5Yaz"></span>
#### Solution


1. Use VNC to access the instance in the console.

2. In the search box, enter "Run", double\-click to open it, and enter "gpedit.msc" to open the Local Group Policy Editor.

3. Expand the following path in sequence: Computer Configuration \> Windows Settings \> Security Settings \> Account Policies \> Account Lockout Policy. On the right panel, double\-click "Account lockout threshold". We recommend that you set this threshold to "0", which means no limit, or increase the threshold.

4. The settings will take effect immediately. You do not need to restart the instance.


<span id=".6YCa6L-HVk5D6L-c56iL55m75b2V5p-Q5Y-w5LqR5pyN5Yqh5Zmo5a6e5L6L77yM5pSv5oyB5aSa55So5oi35ZCM5pe255m75b2V5ZCX77yf"></span>
### Can multiple users remotely log in to the same ECS instance at the same time via VNC?

"Users" are divided into two types: BytePlus accounts and operating system users. The limits vary for different types of users. Specifically:


* For BytePlus accounts, multiple authorized accounts (primary accounts or IAM users) are allowed to log in to the instance at the same time, with no limit on the number of accounts. When multiple accounts are logged in, they can see the same console and share all actions.

* For operating system users, only one user is allowed to log in to the instance at the same time.


<span id=".6YCa6L-HRUNTIFRlcm1pbmFs6L-c56iL55m75b2V5p-Q5Y-w5LqR5pyN5Yqh5Zmo5a6e5L6L77yM5pSv5oyB5aSa55So5oi35ZCM5pe255m75b2V5ZCX77yf"></span>
### Can multiple users remotely log in to the same ECS instance at the same time via the ECS Terminal?

"Users" are divided into two types: BytePlus accounts and operating system users. The limits vary for different types of users. Specifically:


* For BytePlus accounts, a single primary account (including its IAM users) can open up to 100 remote connections at the same time.

* For operating system users:

   * For Linux operating systems, multiple users can log in simultaneously via different browser tabs.

   * For Windows operating systems, whether multiple users can log in at the same time is restricted by the operating system configuration. If multiple users cannot log in simultaneously, the remote connection of the previous user will be automatically disconnected when a new user logs in.


<span id=".5piv5ZCm5Y-v5Lul6YCa6L-H5omL5py655m75b2V5LqR5pyN5Yqh5Zmo77yf"></span>
### Can I log in to an ECS instance via a mobile phone?

You can log in to an ECS instance using remote access software on mobile devices such as iOS and Android. For more information, see [Using a mobile client to log in to a Linux instance](https://docs.byteplus.com/en/docs/ecs/Using-a-mobile-client-to-log-on-to-a-Linux-instance) and [Using a mobile client to log in to a Windows instance](https://docs.byteplus.com/en/docs/ecs/Using-a-mobile-client-to-log-on-to-a-Windows-instance).

<span id=".5Li65LuA5LmI6L-c56iL6L-e5o6l5a6e5L6L57uP5bi45pat5byA77yf"></span>
### Why does the remote connection to my instance frequently disconnect?


* After successful login via VNC, if there is no interactive operation in your management terminal window within 180 seconds, the connection will be automatically disconnected.

* Remote connection may also disconnect when resources are overloaded. We recommend that you refer to the following table to troubleshoot resource usage.

   
   |Troubleshooting item |Description |Solution |
   |---|---|---|
   |Check whether Internet bandwidth exceeds the upper limit. |If the Internet bandwidth upper limit is exceeded, you may fail to log in to the instance. |Check whether Internet bandwidth exceeds the upper limit. For more information, see [Checking Internet bandwidth upper limit of instance](https://docs.byteplus.com/en/docs/ecs/Instance-overview-1#.5p-l55yL56S65L6L) and [Checking Internet bandwidth usage](https://docs.byteplus.com/en/docs/ecs/Monitoring-FAQs#.5aaC5L2V5p-l55yL5a6e5L6L55qE5bim5a6955So6YeP77yf).<br><br>For information about how to increase bandwidth, see [Modifying the maximum bandwidth](https://docs.byteplus.com/en/docs/eip/Modifying-the-maximum-bandwidth). |
   |Check whether CPU or memory load is too high. |High CPU or memory usage on an instance may prevent users from logging in to it. |If you have already [created an alert task](https://docs.byteplus.com/en/docs/ecs/Collecting-alerts-triggered-by-ECS-metrics) by using the Cloud Monitor service, the system will automatically send you an alert when CPU or memory usage is too high.<br><br>You can upgrade vCPU and memory by [changing the instance type](https://docs.byteplus.com/en/docs/ecs/Overview-2). |
   


<span id=".5Li65LuA5LmI5peg5rOV6YCa6L-H5aSW572R6K6_6Zeu5a6e5L6L77yf"></span>
### Why cannot I access an instance from the public network?

To allow an instance to be accessed from the public network or to access the public network, an EIP must be associated with the instance. Access is only possible through this EIP and the opened service ports.


|Troubleshooting item |Description |Solution |
|---|---|---|
|Check whether the security group configuration is correct. |You need to open the ports used by the instance to provide services externally. |In the ECS console, click the name of the instance you cannot log in to to go to the instance details page, select the "Security Group" tab, and make sure that port 22 is added to the inbound rules of a security group associated with the instance.<br><br>If the port is not added, [modify the security group access rules](https://docs.byteplus.com/en/docs/ecs/Modifying-security-group-rules). |
|Check whether an EIP is associated with the instance. |You need to use the EIP associated with the instance to access the instance. |For information about how to view the EIPs associated with an instance, see [Viewing instance information](https://docs.byteplus.com/en/docs/ecs/Instance-overview-1).<br><br>If no EIP is associated with the instance, associate one with the instance. For more information, see [Associating EIPs](https://docs.byteplus.com/en/docs/ecs/associating-an-EIP). |


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">You can also indirectly associate an EIP with the instance by using products such as a NAT gateway. For more information, see <a href="https://docs.byteplus.com/en/docs/vpc/Application-scenarios">Internet access</a>.</div>


<span id=".U1NI55m75b2V5pyN5Yqh5Zmo5ZCO77yM5LiA5a6a5pe26Ze05LiN5pON5L2c5Lya6Ieq5Yqo5pat5byA5Lya6K-d5aaC5L2V5aSE55CG77yf"></span>
### What do I do if the session is automatically disconnected after being inactive for a certain period of time after I log in to the instance via SSH?

After you log in to an ECS instance via SSH, you can execute the following command as the `root` user to disable automatic session disconnection.

```Plain Text
TMOUT=0
```


<span id=".5aaC5L2V6K6-572uVk5D5YWo5bGP5pi-56S677yf"></span>
### How do I set VNC full\-screen display?

VNC does not support full\-screen display. By default, VNC logs directly in to the host. Unlike ECS Terminal's remote desktop, VNC can only display the entire page of the host in a fixed size. If you need full\-screen display, we recommend that you use ECS Terminal's remote desktop for login.

<span id=".5YWz6Zet6L-c56iL6L-e5o6l5ZCO77yM5LqR5pyN5Yqh5Zmo5Lya5YWz5py65ZCX77yf"></span>
### Will the ECS instance shut down after I close the remote connection?

No, it will not. If you do not shut down the instance, the instance remains in the **Running** state.
