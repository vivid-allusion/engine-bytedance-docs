---
title: "Using the console to log in to a Windows instance"
product: "Elastic Compute Service"
product_code: "ecs"
source: "https://docs.byteplus.com/en/docs/ecs/Using-the-console-to-log-on-to-a-Windows-instance"
---

In the ECS console, you can log in to a Windows instance through ECS Terminal or VNC. Only password authentication is supported.

<span id=".5L2_55So6ZmQ5Yi2"></span>
## Limits

The number of users that can remain logged in to an ECS instance varies based on the login method and user type. See details in the following table:


|User type/Login method |VNC |ECS Terminal |
|---|---|---|
|Cloud platform account |Multiple authorized accounts (primary accounts or IAM users) can log in to an instance at the same time. The number of accounts is not limited.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">When multiple accounts are logged in, they can see the same console and share all actions.</div><br> |A primary account (including all IAM users under it) can have a maximum of 100 remote connections open at the same time. |
|Operating system user |Only one user can log in to an instance at a time. |This depends on the operating system configuration. If multiple users cannot log in simultaneously, the remote connection of the previous user will be automatically disconnected when a new user logs in. |


<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites


* Make sure the ECS instance you log in to meets the conditions in the [Login restrictions](https://docs.byteplus.com/en/docs/ecs/Overview-1).

* When you log in through ECS Terminal, make sure the security group associated with the primary network interface of the instance has an inbound rule that allows TCP port 3389 from 100.64.0.0/10.


<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure


<Tabs>
<Tab zoneid="guGApgCsMh" title="ECS Terminal (Recommended)">
<TabTitle>ECS Terminal (Recommended)</TabTitle>

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">ECS Terminal supports text copy and paste for a smoother interaction experience, and is the recommended method. ECS Terminal is applicable to scenarios where the instance is in the <strong>Running</strong> state and the operating system runs normally.</div>



1. Log in to the [ECS console](https://console.byteplus.com/ecs/instance). 

2. In the top menu bar, select the region and project where the target instance resides.

3. Click "Connect" in the "Actions" column of the target instance.

4. Click the "Log in now" button under **ECS Terminal**.

5. On the "Remote login" page, configure login information by referring to the table below.



|Configuration Item |Notes |
|---|---|
|Port |When you log in to a Windows instance, RDP uses its default port (3389). Make sure the security group associated with your instance allows inbound TCP traffic on port 3389.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="default">If you need to change the connection port of your target instance, please refer to <a href="https://docs.byteplus.com/en/docs/ecs/How-to-modify-the-default-remote-port-of-an-ECS-instance">Changing the ECS default remote port</a>. After this, you can log in to the instance with the updated port.</div><br><br><br>* <div data-tips="true" data-tips-type="default">If the security group associated with the instance does not allow the corresponding port, please refer to <a href="https://docs.byteplus.com/en/docs/ecs/Modifying-security-group-rules">Viewing/Modifying security group access rules</a>, or <a href="https://docs.byteplus.com/en/docs/ecs/Changing-security-groups">Changing security group to </a>complete the operation.</div><br> |
|Username |The default login username for Windows instances is Administrator.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">You can also <a href="https://docs.byteplus.com/en/docs/ecs/Self-building-users-log-in-to-the-ECS">create a new user</a> and log in with a custom username.</div><br> |
|Authentication method |Password authentication: The login password is the one you set when creating the instance. If you forget your password, please [reset the password](https://docs.byteplus.com/en/docs/ecs/Resetting-passwords) first.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">For instances created using custom or shared Windows images, you can log in to the instance with the image's pre\-configured password after adjusting the Cloudbase\-init file of the image. <a href="https://docs.byteplus.com/en/docs/ecs/Using-the-wizard-to-buy-ECS-instances#.6Ieq5a6a5LmJ6YWN572u">Learn more</a>.</div><br> |



6. You can check "Save the login information and login credentials, and quickly log in next time". Then, click the "Login" button.

   * If the login succeeds, you will be directed to the Windows desktop.

   * If login fails, you can click  or "View document" on the remote login page. Then,  the . You can also refer to [What should I do if I cannot remotely connect to the instance?](https://docs.byteplus.com/en/docs/ecs/What_should_I_do_if_I_can_not_remotely_log_into_the_instance) for troubleshooting.

7. Copy text: Due to Safari and Edge browser restrictions, after you log in to a Windows ECS instance through ECS Terminal, you cannot directly copy text to or from the instance. As a workaround, use the [clipboard interception mini program](https://docs.byteplus.com/en/docs/ecs/Copy-text-in-Safari-and-Edge-browsers) to copy text.


</Tab>
<Tab zoneid="dZKkwH71KE" title="VNC">
<TabTitle>VNC</TabTitle>

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">You can not directly copy or paste text. Only commands that do not include Chinese can be pasted or copied.</div>


* <div data-tips="true" data-tips-type="tip">You can log in to <strong>Running instances (including instances in the OS startup stage)</strong> or <strong>Stopped</strong> instances through VNC. This method is applicable to emergency O&M and allows you check your ECS status. Therefore, you can perform maintenance tasks, including <a href="https://docs.byteplus.com/en/docs/ecs/Booting-in-single-user-mode">enabing single\-user mode</a>.</div>


* <div data-tips="true" data-tips-type="tip">If the system detects no operation within 180 seconds after login with VNC, disconnection occurs.</div>


1. Log in to [the ECS console](https://console.byteplus.com/ecs/instance). 

2. In the top menu bar, select the region and project where the target instance resides.

3. Click "Connect" in the "Actions" column of the target instance.

4. Click the "Log in Now" button under **VNC**.

5. On the Windows login page, click the "Show/Hide Control Bar" icon on the left, and then click the button shown in the following figure to enable "Ctrl+Alt+Delete" for unlocking.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_3ba910da59f941157a65c79b5e50b6c9.png) </span>

6. Enter the instance password and press the "Enter" key.

   * If the login succeeds, you will be directed to the Windows desktop.

   * If the login fails, you can click  or "View document" on the remote login page. Then,  the . You can also refer to [What should I do if I cannot remotely connect to the instance?](https://docs.byteplus.com/en/docs/ecs/What_should_I_do_if_I_can_not_remotely_log_into_the_instance) for troubleshooting.

7. Copy command: Click the clipboard button on the left, copy and paste the command into the clipboard box. Then click "Send" to copy the command to Windows.


</Tab>
</Tabs>
