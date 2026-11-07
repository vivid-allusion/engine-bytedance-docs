---
title: "Login overview"
product: "Elastic Compute Service"
product_code: "ecs"
source: "https://docs.byteplus.com/en/docs/ecs/Overview-1"
---

After creating the instance, you must remotely log in to the ECS instance from your local host for subsequent actions, such as setting up a website. You can log in to an ECS instance with various methods. This topic introduces how to choose an appropriate tool to log in to your ECS instance.

<span id=".55m75b2V6ZmQ5Yi2"></span>
## Restrictions

Before you log in to the instance, make sure that the instance to be logged in meets the following conditions. Otherwise, the login may fail.


|Type |Restrictions |
|---|---|
|Instance state |You can only log in to instances in the **Running** status. |
|Protocol and port |When you use ECS Terminal or third\-party tools for remote desktop connection, make sure that the inbound rules of security groups associated with the instance's primary network interface have the relevant protocols and ports enabled. [How to view or modify security group rules in the ECS console?](https://docs.byteplus.com/en/docs/ecs/Modifying-security-group-rules) or [How to change the security group associated with an ECS instance?](https://docs.byteplus.com/en/docs/ecs/Changing-security-groups)<br><br><br>* For the Linux operating system, the default protocol is TCP, and the port is 22.<br><br>* For Windows operating system, the default protocol is RDP, and the port is 3389.<br><br><br>> You can also [modify the default remote port of the ECS instance](https://docs.byteplus.com/en/docs/ecs/How-to-modify-the-default-remote-port-of-an-ECS-instance), and then log in to the instance with the modified port. |
|Login username |* The default login username for Linux instances is root.<br><br>* The default login username for Windows instances is Administrator.<br><br><br>> You can also [create a new user](https://docs.byteplus.com/en/docs/ecs/Self-building-users-log-in-to-the-ECS) and log in with a custom username. |
|Authentication method |The following authentication methods are available:<br><br><br>* Password: The login password is the password set when you create the instance. If you forget your password, [reset the password](https://docs.byteplus.com/en/docs/ecs/Resetting-passwords) first.<br><br>* Key: After associating the instance with a key pair, you can use the private key to log in to your ECS instance.To view the key pair associated with the instance, refer to [Viewing key pairs associated with instances](https://docs.byteplus.com/en/docs/ecs/Viewing-key-pairs-bound-to-instances).  If you lost the private key, [reassociate the key pair](https://docs.byteplus.com/en/docs/ecs/Binding-key-pairs-to-instances).<br><br><br>> In addition to the above methods, for instance created using a custom image or shared image, you can also use the password or key pair preset in the image to log in to the instance. [Learn more](https://docs.byteplus.com/en/docs/ecs/Using-the-wizard-to-buy-ECS-instances#.6Ieq5a6a5LmJ6YWN572u) |
|Troubleshooting for login failure |* [What should I do if I can not remotely connect to the instance?](https://docs.byteplus.com/en/docs/ecs/What_should_I_do_if_I_can_not_remotely_log_into_the_instance)<br><br>* [Why can't I connect to my instance even after enabling the port?](https://docs.byteplus.com/en/docs/ecs/Logon-and-connection-FAQs#.5Li65LuA5LmI5pS-6YCa5LqG56uv5Y-j5LuN5peg5rOV6L-e5o6l5a6e5L6L77yf) |


<span id=".55m75b2V5pa55byP"></span>
## Login methods

When you log in to an ECS instance, methods and tools vary based on the operating system of your local host. The following table provides a comparison of available login tools for your reference. For detailed instructions, refer to relevant documents.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">If the system detects no operation within 180 seconds after a successful VNC login, disconnection occurs.</div>


* <div data-tips="true" data-tips-type="tip">When you use third\-party tools for login, make sure that the instance to be logged in has an EIP associated. Otherwise, you cannot connect to the instance. <a href="https://docs.byteplus.com/en/docs/ecs/Instance-overview-1">How can I view the EIP address associated with an instance?</a> <a href="https://docs.byteplus.com/en/docs/ecs/associating-an-EIP">How can I associate an EIP with an instance?</a></div>


* <div data-tips="true" data-tips-type="tip">When you use the ECS Terminal or third\-party tools for remote desktop connection, <a href="https://docs.byteplus.com/en/docs/ecs/Enable-SSH-on-Linux-instance">enable SSH for Linux instances</a>, or <a href="https://docs.byteplus.com/en/docs/ecs/Method_for_enable_Remote_Desktop_Connection_RDP_service_for_Windows_system_instances">enable RDP for Windows ECS instances</a>. Otherwise, you cannot connect to the instance.</div>




<Tabs>
<Tab zoneid="MtYsUIuhzp" title="Log in to a Linux instance">
<TabTitle>Log in to a Linux instance</TabTitle>


|**Login tool type** |**Operating system of the local host** |**Login tool** |**Whether SSH needs to be turned on** |**Login authentication method** |**Ease of interaction** |**Association with an EIP required** |**Actions guide** |
|---|---|---|---|---|---|---|---|
|Login tool provided by the cloud platform |ECS console |ECS Terminal (recommended) |Yes |Password and key |You can directly copy or paste text. Therefore, we recommend this type of tool as it provides a smoother user experience. |No |[Using password or key to log in to the Linux instance via ECS console](https://docs.byteplus.com/en/docs/ecs/Using-the-console-to-log-on-to-a-Linux-instance) |
|||VNC |No |Password |You can not directly copy or paste text. Only commands that do not include Chinese can be pasted or copied. |No ||
|Third\-party login tools |Windows |Built\-in Command Prompt of Windows\-\-SSH command |Yes |Password and key |Situations vary based on the specific tool. |Yes |[Using a Windows host to log in to a Linux instance](https://docs.byteplus.com/en/docs/ecs/Using-a-Windows-host-to-log-on-to-a-Linux-instance) |
|||PuTTY ||||||
||Linux |SSH command ||Password and key |||[Using a Linux host to log in to a Linux instance](https://docs.byteplus.com/en/docs/ecs/Using-a-Linux-host-to-log-on-to-a-Linux-instance) |
||macOS |Built\-in terminal of macOS\-\-SSH command ||Password and key |||[Using MacOS to log in to a Linux instance](https://docs.byteplus.com/en/docs/ecs/Using-MacOS-to-log-on-to-a-Linux-instance) |
||Mobile (IOS) |Termius\-SSH ||Password |||[Using a mobile client to log in to a Linux instance](https://docs.byteplus.com/en/docs/ecs/Using-a-mobile-client-to-log-on-to-a-Linux-instance) |
||Mobile (Android) |JuiceSSH ||Password ||||





</Tab>
<Tab zoneid="LG71CNqYt6" title="Log in to a Windows instance">
<TabTitle>Log in to a Windows instance</TabTitle>

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="default">When you log in to the Windows ECS instance, log in to the ECS with VNC first, and then <a href="https://docs.byteplus.com/en/docs/ecs/Method_for_enable_Remote_Desktop_Connection_RDP_service_for_Windows_system_instances">enable RDP (Remote Desktop Protocol)</a>. Otherwise, remote desktop connection fails.</div>


* <div data-tips="true" data-tips-type="default">For ECS instances created with public images provided by BytePlus, RDP is turned on by default.</div>




|**Login tool type** |**Operating system of the local host** |**Login tool** |**RDP required** |**Login authentication method** |**Ease of interaction** |**Association with an EIP required** |**Actions guide** |
|---|---|---|---|---|---|---|---|
|BytePlus console |BytePlus console |ECS Terminal (recommended) |Yes |Password |You can directly copy or paste text. Therefore, we recommend this type of tool as it provides a smoother user experience. |No |[Logging in to a Windows instance through ECS console](https://docs.byteplus.com/en/docs/ecs/Using-the-console-to-log-on-to-a-Windows-instance) |
|||VNC |No ||You can not directly copy or paste text. Only commands that do not include Chinese can be pasted or copied. |No ||
|Third\-party login tool |Windows |MSTSC, a remote desktop connection tool that comes with Windows |Yes ||Situations vary based on the specific tool. |Yes |[Using a Windows host to log in to a Windows instance via MSTSC tool](https://docs.byteplus.com/en/docs/ecs/Using-a-Windows-host-to-log-on-to-a-Windows-instance) |
||Linux |rdesktop with Remote Desktop Protocol (RDP) enabled |||||[Using a Linux host to log in to a Windows instance](https://docs.byteplus.com/en/docs/ecs/Using-a-Linux-host-to-log-on-to-a-Windows-instance) |
||macOS |Microsoft Remote Desktop for Mac |||||[Using MacOS to log in to a Windows instance via MRD](https://docs.byteplus.com/en/docs/ecs/Using-MacOS-to-log-on-to-a-Windows-instance) |
||Mobile (IOS) |Microsoft remote desktop |||||[Log in to Windows instance via mobile](https://docs.byteplus.com/en/docs/ecs/Using-a-mobile-client-to-log-on-to-a-Windows-instance) |
||Mobile (Android) |Remote Desktop ||||||



</Tab>
</Tabs>


<span id="A5ax2yJv"></span>
##
