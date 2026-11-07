---
title: "Using the console to log in to a Linux instance"
product: "Elastic Compute Service"
product_code: "ecs"
source: "https://docs.byteplus.com/en/docs/ecs/Using-the-console-to-log-on-to-a-Linux-instance"
---

In the ECS console, you can log in to an instance that runs the Linux operating system through ECS Terminal or VNC.

<span id=".5L2_55So6ZmQ5Yi2"></span>
## Limits

The number of users that can remain logged in to an ECS instance varies based on the login method and user type. See details in the following table:


|User type |VNC |ECS Terminal |
|---|---|---|
|Cloud platform account |Multiple authorized accounts (primary accounts or IAM users) can log in to an instance at the same time. The number of accounts is not limited.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">When multiple accounts are logged in, they can see the same console and share all actions.</div><br> |A primary account (including all IAM users under it) can have a maximum of 100 remote connections open at the same time. |
|Operating system user |Only one user can log in to an instance at a time. |You can log in as multiple users from different browser tabs at the same time. |


<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites

Make sure that the ECS instance to log in meets the conditions in the [Login restrictions](https://docs.byteplus.com/en/docs/ecs/Overview-1).

<span id=".5pON5L2c5q2l6aqk"></span>
## Login procedure


<Tabs>
<Tab zoneid="oIo0maR6Yr" title="ECS Terminal (recommended)">
<TabTitle>ECS Terminal (recommended)</TabTitle>

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Convenient interaction: You can directly copy or paste text when logging in to the instance with ECS Terminal. Therefore, we recommend you use ECS Terminal to enjoy a smoother user experience. ECS Terminal is applicable to scenarios where the instance is in <strong>Running</strong> state and the operating system runs normally. If you use key for authentication, ECS Terminal is your ideal choice for login.</div>



1. Log in to [the ECS console](https://console.byteplus.com/ecs/instance). 

2. In the top menu bar, select the project and region of the target instance.

3. Click "Connect" in the "Actions" column of the target instance.

4. Click "Log in now" under **ECS Terminal**.

5. On the remote login page, configure login information by referring to the table below.

   
   |Configuration item |Note |
   |---|---|
   |Port |When you log in to a Linux instance, SSH uses its default port (22). Make sure the security group associated with your instance allows inbound TCP traffic on port 22.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="default">If you need to change the connection port of your target instance, refer to <a href="https://docs.byteplus.com/en/docs/ecs/How-to-modify-the-default-remote-port-of-an-ECS-instance">Changing the ECS default remote port</a>. After this, you can log in to the instance with the updated port.</div><br><br><br>* <div data-tips="true" data-tips-type="default">If the security group associated with the instance does not allow the corresponding port, refer to <a href="https://docs.byteplus.com/en/docs/ecs/Modifying-security-group-rules">Viewing/Modifying security group access rules</a>, or <a href="https://docs.byteplus.com/en/docs/ecs/Changing-security-groups">Changing security group</a> to complete the operation.</div><br> |
   |Username |The default username for Linux instances is root.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">You can also <a href="https://docs.byteplus.com/en/docs/ecs/Self-building-users-log-in-to-the-ECS">create a new user</a> and log in with a custom username.</div><br> |
   |Authentication method |* Password: The login password is the password set when you create the instance. If you forget your password, [reset the password](https://docs.byteplus.com/en/docs/ecs/Resetting-passwords) first.<br><br>* Key: If the instance is associated with a key pair, the name/ID of the key pair appears in the "Attach Key" section. Then click the<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_0dd4c724d65673d6ba7dd349122a57f1.png) </span>icon to upload the corresponding private key for login. If you have lost the private key, or no key pair is associated with the instance, you need to[ associate a key pair](https://docs.byteplus.com/en/docs/ecs/Binding-key-pairs-to-instances) with the instance before logging in.<br><br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">In addition to the above methods, for instances created from a custom image or shared image, you can also use the password or key pair preset in the image to log in to the instance. <a href="https://docs.byteplus.com/en/docs/ecs/Using-the-wizard-to-buy-ECS-instances#.6Ieq5a6a5LmJ6YWN572u">Learn more</a></div><br> |
   

6. You can check "Save the log in information and log in credentials, and quickly log in next time.". Then, click "Login".

   * After login, you enter the terminal command page. The response is as follows:

      <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_0ce437421769610dbaab79a67807bab7.png) </span>

   * If login fails, you can click  or "view document" on the remote login page. Then,  the   refer to [What should I do if I cannot remotely connect to the instance?](https://docs.byteplus.com/en/docs/ecs/What_should_I_do_if_I_can_not_remotely_log_into_the_instance) for troubleshooting.


</Tab>
<Tab zoneid="KvnBGNG61n" title="VNC">
<TabTitle>VNC</TabTitle>

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">You cannot directly copy or paste text. Only commands that do not contain Chinese characters can be copied or pasted.</div>


* <div data-tips="true" data-tips-type="tip">You can log in to <strong>Running instances (including instances in the OS startup stage)</strong> or <strong>Stopped</strong> instances through VNC. This method is suitable for emergency O&M scenarios, allowing you to check the ECS status or perform maintenance tasks, such as <a href="https://docs.byteplus.com/en/docs/ecs/Booting-in-single-user-mode">enabing single\-user mode</a>.</div>


* <div data-tips="true" data-tips-type="tip">If the system detects no operation within 180 seconds after login with VNC, disconnection occurs.</div>


1. Log in to the [ECS console](https://console.byteplus.com/ecs/instance).  

2. In the top menu bar, select the project and region of the target instance.

3. Click the "Connect" button in the "Actions" column of the target instance.

4. Click "Log in now" under **VNC**.

5. Input the login user. The default user for Linux instances is root, or you can [create a new user](https://docs.byteplus.com/en/docs/ecs/Self-building-users-log-in-to-the-ECS). Then, press the `Enter` key.

6. Input the password to log in to the instance. Then, press the `Enter` key.

   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   * <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">The login password is the password set when you <a href="https://docs.byteplus.com/en/docs/ecs/Using-the-wizard-to-buy-ECS-instances#.6Ieq5a6a5LmJ6YWN572u">create the instance. </a>When you log in to a Linux instance, the interface does not display the password input process. Please ensure the password entered is correct.   </div>
   

   * <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">If you are unsure of your login password, you can <a href="https://docs.byteplus.com/en/docs/ecs/Resetting-passwords">reset the password</a> and log in again.   </div>
   

   * The response for successful login is as follows:

      <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_a7eee0b408240a03fd5ce7a154090966.png) </span>

   * If login fails, you can click  or "view document" on the remote login page. Then,  the   refer to [What should I do if I cannot remotely connect to the instance?](https://docs.byteplus.com/en/docs/ecs/What_should_I_do_if_I_can_not_remotely_log_into_the_instance) for further problem detection.

7. Copy command: Click the clipboard button on the left, copy and paste the command into the clipboard box. Then click "Send" to copy the command to Linux.


</Tab>
</Tabs>


&nbsp;
