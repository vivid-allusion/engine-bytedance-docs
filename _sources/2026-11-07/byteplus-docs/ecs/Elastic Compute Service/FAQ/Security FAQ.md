---
title: "Security FAQ"
product: "Elastic Compute Service"
product_code: "ecs"
source: "https://docs.byteplus.com/en/docs/ecs/Security-FAQs"
---


|Category |Question |
|---|---|
|Key pair |* [Can I use key pairs to log in to Linux instances and Windows instances?](https://docs.byteplus.com/en/docs/ecs/Security-FAQs#.TGludXjlrp7kvovlkoxXaW5kb3dz5a6e5L6L6YO95Y-v5Lul5L2_55So5a-G6ZKl5a-555m75b2V5ZCX77yf)<br><br>* [Why cannot I associate a key pair with an instance?](https://docs.byteplus.com/en/docs/ecs/Security-FAQs#.5a6e5L6L5Li65LuA5LmI5peg5rOV57uR5a6a5a-G6ZKl5a-577yf)<br><br>* [How do I use a local key pair to log in to a Linux instance?](https://docs.byteplus.com/en/docs/ecs/Security-FAQs#.5aaC5L2V5L2_55So5pys5Zyw5a-G6ZKl5a-555m75b2VTGludXjlrp7kvovvvJ8=)<br><br>* [Why cannot I log in to a Linux instance by using a local key pair?](https://docs.byteplus.com/en/docs/ecs/Security-FAQs#.5Li65LuA5LmI5L2_55So5pys5Zyw5a-G6ZKl5a-55peg5rOV55m75b2VTGludXjlrp7kvovvvJ8=)<br><br>* [How can I log in to an instance if I lose the private key of my key pair?](https://docs.byteplus.com/en/docs/ecs/Security-FAQs#.5a-G6ZKl5a-555qE56eB6ZKl5Lii5aSx77yM5aaC5L2V55m75b2V5a6e5L6L77yf) |
|Ubuntu firewall |[How do I configure the firewall for an Ubuntu ECS instance?](https://docs.byteplus.com/en/docs/ecs/Security-FAQs#.5aaC5L2V6YWN572uVWJ1bnR15LqR5pyN5Yqh5Zmo6Ziy54Gr5aKZ77yf) |
|Windows firewall |[How do I configure the firewall for a Windows ECS instance (enable/disable/modify ports)?](https://docs.byteplus.com/en/docs/ecs/Security-FAQs#.5aaC5L2V6YWN572uIFdpbmRvd3Mg5LqR5pyN5Yqh5Zmo6Ziy54Gr5aKZ77yf) |


<span id=".5a-G6ZKl5a-56Zeu6aKY"></span>
## Key pair FAQ

<span id=".TGludXjlrp7kvovlkoxXaW5kb3dz5a6e5L6L6YO95Y-v5Lul5L2_55So5a-G6ZKl5a-555m75b2V5ZCX77yf"></span>
### Can I use key pairs to log in to Linux instances and Windows instances?

Currently, Linux instances support two login methods: password and SSH key, while Windows instances currently support only password login.

<span id=".5a6e5L6L5Li65LuA5LmI5peg5rOV57uR5a6a5a-G6ZKl5a-577yf"></span>
### Why cannot I associate a key pair with an instance?

You can associate a key pair with an instance that is installed with the reset\-authentication plug\-in. [Install the plug-in](https://docs.byteplus.com/en/docs/ecs/Installing-the-password-plug-in) first.

After you associate a key pair with an instance, you need to restart the instance for the key pair to take effect.

<span id=".5aaC5L2V5L2_55So5pys5Zyw5a-G6ZKl5a-555m75b2VTGludXjlrp7kvovvvJ8="></span>
### How do I use a local key pair to log in to a Linux instance?


1. View the public key of the local key pair. For more information, see [Viewing public key information](https://docs.byteplus.com/en/docs/ecs/Viewing-public-keys).

2. [Create a key pair](https://docs.byteplus.com/en/docs/ecs/Creating-key-pairs) by **importing an existing public key**.

3. [Associate the key pair with the instance](https://docs.byteplus.com/en/docs/ecs/Binding-key-pairs-to-instances) and restart the instance for the key pair to take effect.

4. [Log in to the Linux instance](https://docs.byteplus.com/en/docs/ecs/Using-the-console-to-log-on-to-a-Linux-instance).


<span id=".5Li65LuA5LmI5L2_55So5pys5Zyw5a-G6ZKl5a-55peg5rOV55m75b2VTGludXjlrp7kvovvvJ8="></span>
### Why cannot I log in to a Linux instance by using a local key pair?

The reset authentication plug\-in may not be installed on the instance. [Install the plug-in](https://docs.byteplus.com/en/docs/ecs/Installing-the-password-plug-in) and try again.

<span id=".5a-G6ZKl5a-555qE56eB6ZKl5Lii5aSx77yM5aaC5L2V55m75b2V5a6e5L6L77yf"></span>
### How can I log in to an instance if I lose the private key of my key pair?

If the private key is lost, you can only log in to the instance after you associate a new key pair with the instance. The specific operations are as follows:


1. [Disassociate the original key pair](https://docs.byteplus.com/en/docs/ecs/Unbinding-key-pairs-from-instances) from the instance.

2. [Create a new key pair](https://docs.byteplus.com/en/docs/ecs/Creating-key-pairs).

3. [Associate the new key pair with the instance](https://docs.byteplus.com/en/docs/ecs/Binding-key-pairs-to-instances).

4. Use the new key pair to [log in to the Linux instance](https://docs.byteplus.com/en/docs/ecs/Using-the-console-to-log-on-to-a-Linux-instance).


<span id=".VWJ1bnR16Ziy54Gr5aKZ"></span>
## Ubuntu firewall

<span id=".5aaC5L2V6YWN572uVWJ1bnR15LqR5pyN5Yqh5Zmo6Ziy54Gr5aKZ77yf"></span>
### How do I configure the firewall for an Ubuntu ECS instance?

This section uses an ECS instance running the Ubuntu 20.04.5 LTS operating system as an example to describe how to enable or disable the firewall on Ubuntu\-based instances, and how to add port rules to the firewall.


<Tabs>
<Tab zoneid="gEQouTdf6a" title="Install the Ubuntu firewall">
<TabTitle>Install the Ubuntu firewall</TabTitle>

1. [Log in to the ECS instance](https://docs.byteplus.com/en/docs/ecs/Using-the-console-to-log-on-to-a-Windows-instance).

2. Execute the following command to check whether Uncomplicated Firewall is installed.


```Bash
ufw status
```



3. If Uncomplicated Firewall is not installed, execute the following commands in sequence to install it.


```Plain Text
sudo apt update
sudo apt install ufw
```





</Tab>
<Tab zoneid="LLcrRU4KZb" title="Enable or disable Uncomplicated Firewall">
<TabTitle>Enable or disable Uncomplicated Firewall</TabTitle>

1. [Log in to the ECS instance](https://docs.byteplus.com/en/docs/ecs/Using-the-console-to-log-on-to-a-Windows-instance).

2. Execute the following command to enable the SSH remote login service.


```Bash
sudo ufw allow ssh
```



3. Execute the following command to enable Uncomplicated Firewall.


```Bash
sudo ufw enable
```


<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">If the rule allowing SSH remote login services is not configured in advance, enabling Uncomplicated Firewall will disconnect the ECS Terminal remote login, and subsequent remote logins via the ECS Terminal will fail. Proceed with caution.</div>



4. Execute the following command to disable Uncomplicated Firewall.


```Bash
sudo ufw disable
```





</Tab>
<Tab zoneid="pwNXWEt2ol" title="Configure firewall rules">
<TabTitle>Configure firewall rules</TabTitle>

* **Add rules**

   1. [Log in to the ECS instance](https://docs.byteplus.com/en/docs/ecs/Using-the-console-to-log-on-to-a-Windows-instance).

   2. Add rules to allow specific ports to be accessed. Examples:

      * Allow SSH (default port 22):


```Bash
sudo ufw allow ssh
```



      * Allow specific ports to be accessed. For example, allow HTTP (port 80):


```Bash
sudo ufw allow 80/tcp
```



   3. Add a rule to deny access to specific ports.


For example, deny access to port 80.

```Bash
sudo ufw deny 80/tcp
```


<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">For the same port, newly configured firewall rules will overwrite existing ones. For example, if you first configure a rule to block port 80 and then configure a rule to allow port 80, only the "allow port 80" rule will remain in effect.</div>



* **Delete a rule**

   1. [Log in to the ECS instance](https://docs.byteplus.com/en/docs/ecs/Using-the-console-to-log-on-to-a-Windows-instance).

   2. Execute the following command to query the rule IDs.


```Bash
ufw status numbered
```



<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_45dd4438481604f25a0d48549d61b73d.png) </span>

   3. Execute the following command to delete a rule.


```Bash
sudo ufw delete <rule_number>
```





</Tab>
<Tab zoneid="AQM9MNwlGU" title="View firewall details">
<TabTitle>View firewall details</TabTitle>

1. [Log in to the ECS instance](https://docs.byteplus.com/en/docs/ecs/Using-the-console-to-log-on-to-a-Windows-instance).

2. Execute the following command to view the rules configured for Uncomplicated Firewall.


```Bash
sudo ufw status
```



3. Execute the following command to view Uncomplicated Firewall logs.


```Bash
cat /var/log/ufw.log
```





</Tab>
</Tabs>


<span id=".V2luZG93c-mYsueBq-WimQ=="></span>
## Windows firewall

<span id=".5aaC5L2V6YWN572uIFdpbmRvd3Mg5LqR5pyN5Yqh5Zmo6Ziy54Gr5aKZ77yf"></span>
### How do I configure the firewall for a Windows ECS instance?

This section uses an ECS instance running the Windows Server 2019 operating system as an example to describe how to enable or disable the firewall on Windows\-based instances, and how to add port rules to the firewall.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">If you disable the firewall, your device may be vulnerable to attacks. Proceed with caution. If you disable the firewall, we recommend that you exercise caution when you open ports in security groups.</div>


* <div data-tips="true" data-tips-type="tip">If you enable the firewall, the firewall must allow the local remote desktop port to permit remote connections. The default port for the remote server is TCP 3389. For specific operations, see the following "Configure port rules for the firewall" tab.</div>


* <div data-tips="true" data-tips-type="tip">If the port specified in the inbound rules of the firewall does not match the port specified on the remote server, remote access to the server will fail. You can refer to the following "Configure port rules for the firewall" tab to add a new port to the inbound rules of the firewall.</div>




<Tabs>
<Tab zoneid="ryGoBStGkU" title="Enable or disable the firewall">
<TabTitle>Enable or disable the firewall</TabTitle>

1. [Log in to the ECS instance](https://docs.byteplus.com/en/docs/ecs/Using-the-console-to-log-on-to-a-Windows-instance).

2. On the desktop of the Windows instance, click "Start \> Control Panel".

3. In the "Control Panel" window, click "System and Security."

4. On the "System and Security" page, click "Windows Defender Firewall".

5. On the "Windows Defender Firewall" page, click "Turn Windows Defender Firewall on or off".

6. View and specify the firewall status: enable or disable.


</Tab>
<Tab zoneid="x0YObtjZuC" title="Configure port rules for the firewall">
<TabTitle>Configure port rules for the firewall</TabTitle>

1. [Log in to the ECS instance](https://docs.byteplus.com/en/docs/ecs/Using-the-console-to-log-on-to-a-Windows-instance).

2. On the desktop of the Windows instance, click "Start \> Control Panel".

3. In the "Control Panel" window, click "System and Security."

4. On the "System and Security" page, click "Windows Defender Firewall".

5. On the "Windows Defender Firewall" page, click "Advanced settings".

6. On the "Windows Defender Firewall with Advanced Security" page, click "Inbound Rules \> New Rule".

7. In the pop\-up "New Inbound Rule Wizard" window, select "Port", and click "Next".

8. In the pop\-up window, select "TCP" and specify a value for "Specific local port". In the example provided in this topic, port 3389 is opened. Click "Next."

9. In the pop\-up window, select "Allow the connection". Click "Next".

10. In the pop\-up window, retain the default settings. Click "Next".

11. In the pop\-up window, enter the rule name. Click "Finish".

12. After you add the rule, the rule will appear as the first entry in the "Inbound Rules" list on the "Windows Defender Firewall with Advanced Security" page.


</Tab>
</Tabs>
