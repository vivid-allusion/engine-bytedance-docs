---
title: "Changing default ports for logging in to ECS instances remotely"
product: "Elastic Compute Service"
product_code: "ecs"
source: "https://docs.byteplus.com/en/docs/ecs/How-to-modify-the-default-remote-port-of-an-ECS-instance"
---

When you use ECS Terminal or a third\-party tool to log in to an instance via remote desktop, a Linux instance defaults to the TCP protocol and port 22, and a Windows instance defaults to the TCP protocol and port 3389.

If you need to change the default remote login ports to reduce the risk of scanning and attacks by malicious software and improve instance security, this topic is for your reference.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">After the change, you can no longer access the ECS instance using the original default port.</div>



* <div data-tips="true" data-tips-type="warning">If you need to change the port again or reuse the original default port, perform as instructed in this topic again.</div>


* <div data-tips="true" data-tips-type="warning">If you cannot remotely log in to the instance after changing the port,<a href="https://docs.byteplus.com/en/docs/ecs/Using-the-console-to-log-on-to-a-Linux-instance"> log in via VNC tools</a>, and then perform as instructed in this topic for changes.</div>



<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure


<Tabs>
<Tab zoneid="P92TXjOoaW" title="Linux operating system">
<TabTitle>Linux operating system</TabTitle>

CentOS is used as an example.


1. [Log in to the instance](https://docs.byteplus.com/en/docs/ecs/Using-the-console-to-log-on-to-a-Linux-instance#.5pON5L2c5q2l6aqk) with the root administrator account.


> You can change the default login port only after logging in as the root account.



2. Execute the following command to back up the configuration file of the sshd service.


```Plain Text
cp /etc/ssh/sshd_config /etc/ssh/sshd_config_bak
```



3. Execute the following command to modify the sshd_config configuration file.


```Plain Text
vim /etc/ssh/sshd_config
```



4. Press the `i` key to enter edit mode. Then, under the `#Port 22 line`, add a new line with the new port in the format `Port [new port number]`, for example, `Port 1122`.

   <span>![图片](https://lf6-volc-editor.volccdn.com/obj/volcfe/sop-public/upload_917fd4fc2b8a95d4b42bbd29b27aba49) </span>

5. Press the `Esc` key, enter `:wq`, and then press Enter to save and exit the sshd_config configuration file.

6. Execute the following command to restart the sshd service. After the restart, you can log in to the Linux instance via SSH on port `1122`.


```Plain Text
systemctl restart sshd
```



7. [Configure the security group rule of the instance](https://docs.byteplus.com/en/docs/ecs/Modifying-security-group-rules) `1122` as follows.

   This allows TCP requests from any address to connect to the ECS instance on port 1122. You can also specify a source address range to control where requests come from.

8. [Log in to the instance](https://docs.byteplus.com/en/docs/ecs/Using-the-console-to-log-on-to-a-Linux-instance#.5pON5L2c5q2l6aqk) again as a new account via password.

9. Click "Confirm". If you can log in to the instance, the port is configured successfully.


</Tab>
<Tab zoneid="SGjRvgM7sn" title="Windows operating system">
<TabTitle>Windows operating system</TabTitle>

1. [Log in to the instance ](https://docs.byteplus.com/en/docs/ecs/Using-the-console-to-log-on-to-a-Windows-instance#.5pON5L2c5q2l6aqk)with the Administrator account.


> You can change the default login port only after logging in as the Administrator account.



2. Click "Start \> Windows Administrative Tools \> Registry Editor" to open the registry editor.

3. In the left navigation pane, select "HKEY_LOCAL_MACHINE \> System \> CurrentControlSet \> Control \> Terminal Server \> WinStations \> RDP\-Tcp".

4. Find "PortNumber" in the list on the right, right\-click it, and then select "Modify...".

5. In the pop\-up dialog box, specify "Base" as "Decimal". In the text box under "Value data", enter the new port number for remote login, such as 3300, and then click "OK".

6. In the firewall settings, configure the new port number to be added, and then allow port connections. For details, see [Firewall settings in Windows ECS instances](https://docs.byteplus.com/en/docs/ecs/Security-FAQs).

7. Select "Start \> Windows PowerShell". In the Windows PowerShell window, enter "services.msc" and press Enter to open the **Services** window.

8. In the **Services** window, find "Remote Desktop Services" and right\-click this option. Then, select "Restart" to restart the remote login services.

9. [Configure the security group rule of the instance](https://docs.byteplus.com/en/docs/ecs/Modifying-security-group-rules) by allowing TCP port 3300 .

   This allows TCP requests from any address to connect to the ECS instance on port 3300. You can also specify the range of source addresses to control where requests come from.

10. [Log in to the instance](https://docs.byteplus.com/en/docs/ecs/Using-the-console-to-log-on-to-a-Windows-instance#.5pON5L2c5q2l6aqk) again as a new account via password.

11. Click "Confirm". If you can log in to the instance, the port is configured successfully.


</Tab>
</Tabs>
