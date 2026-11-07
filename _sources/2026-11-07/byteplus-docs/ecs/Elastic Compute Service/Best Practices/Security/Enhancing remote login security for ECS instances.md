---
title: "Enhancing remote login security for ECS instances"
product: "Elastic Compute Service"
product_code: "ecs"
source: "https://docs.byteplus.com/en/docs/ecs/Enhancing_remote_login_security_for_ECS_instances"
---

This topic describes how to optimize the security configuration of ECS instances to enhance login security.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>



* <div data-tips="true" data-tips-type="warning">If you have authorized or submitted login accounts, passwords, or other security\-related information on the cloud platform, we recommend you update your login details in time.</div>


* <div data-tips="true" data-tips-type="warning">When you change SSH service configurations such as ports, the current login becomes invalid. Please proceed with caution.</div>



<span id="RE29LGHU"></span>
## Change the default login port

The default login port of Linux instances is TCP port 22, and the default login port of Windows instances is TCP port 3389. By changing the default remote login port, you can reduce automated attacks and malicious scans targeting common ports. This can lower the risk of unauthorized access to your ECS instances or services and enhance system security. [How to change the default port for remote ECS login?](https://docs.byteplus.com/en/docs/ecs/How-to-modify-the-default-remote-port-of-an-ECS-instance)

After modifying the login port of the instance, you need to add a new rule to the security group. When you add the new rule, do not use the IP address `0.0.0.0/0`. `0.0.0.0/0` allows all inbound access, which exposes all ports to the public network. This can be extremely insecure and poses major risks. [How to configure security group rules?](https://docs.byteplus.com/en/docs/ecs/How-to-configure-security-group-rules)

<span id="duuuZ0oI"></span>
## Restrict login accounts

Linux instances default to login by the root administrator account, and Windows instances by the Administrator account. The two administrator accounts both have the highest permission for operating system management. You can disable login by administrator accounts, create custom accounts within the instance, and manage account permission to enhance instance security. [How to log in to an ECS instance with a custom account?](https://docs.byteplus.com/en/docs/ecs/Self-building-users-log-in-to-the-ECS)

**Disable administrator account login for Linux instances**

By prohibiting direct login by the root account, you can avoid malicious attackers from gaining full system permissions through brute\-force attacks or weak passwords. This can reduce the risk of data leaks or system compromise.


1. [Log in to the Linux instance](https://docs.byteplus.com/en/docs/ecs/Using-the-console-to-log-on-to-a-Linux-instance).

2. Execute the following command to open the sshd_config file.

   ```Bash
   vim /etc/ssh/sshd_config
   ```
   

3. Press `i`key to enter the edit mode and set `PermitRootLogin` to `no`.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_01da737258a3c2438289a03d4fbb1af7.png) </span>

4. Press the `Esc` key to exit editing. Then, enter`:wq`, and press Enter to save and exit the vim editor.

5. Restart the sshd service to make the configuration take effect.

   ```Bash
   systemctl restart sshd
   ```
   


**We recommend you do not disable Administrator account login for Windows instances** to ensure normal use of the server. Otherwise, the following issues may occur:


* You cannot log in to the instance through Remote Desktop (RDP) or in the console.

* System maintenance features, such as snapshot backups and cloud assistant operations, may be invalid.

* If you need an emergency recovery, you can only log in to the instance with other administrator accounts or VNC.


<span id="ouQ7oWLI"></span>
## Change the login method to key pair (Linux instances)

The key pair method provides higher security than password\-based login. You can also associate a key pair and edit the ssh server configuration file sshd_config to disable the password login.


1. [Create a key pair](https://docs.byteplus.com/en/docs/ecs/Creating-key-pairs) and keep the private key file properly.

2. [Associate a key pair with a Linux instance](https://docs.byteplus.com/en/docs/ecs/Binding-key-pairs-to-instances). After this, restart the instance to enable the key pair.

3. Use the private key of the key pair to [log in to the instance](https://docs.byteplus.com/en/docs/ecs/Using-the-console-to-log-on-to-a-Linux-instance).

4. Edit the configuration file to disable password login.

   1. Execute the following command to open the sshd_config file.

      ```Bash
      vim /etc/ssh/sshd_config
      ```
      

   2. Press `i`key to enter edit mode and set `PasswordAuthentication` to `no`.

   3. Press the `Esc` key to exit editing. Then, enter`:wq`, and press Enter to save and exit the vim editor.

   4. Restart the sshd service to make the configuration take effect.

      ```Bash
      systemctl restart sshd
      ```
      

   5. The configuration succeeds if you cannot log in to the instance with the password.


<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">Windows instances only support password\-based login. To ensure login security, you can adopt a strong password policy. For example, you can use more complex passwords, avoid common passwords, and change passwords regularly. For detailed steps, refer to <a href="https://docs.byteplus.com/en/docs/ecs/Resetting-passwords">Reseting login passwords</a>.</div>


<span id="DGCS5In8"></span>
## Disable IPs or IP segments access that are not required

**Linux instances**

By configuring the /etc/hosts.allow and /etc/hosts.deny files which control remote access, you can allow or deny specific IPs or IP segments access to certain services on a Linux instance. For example, the SSH service is typically only accessible to administrators. To enhance security, you can disable unnecessary IPs and only allow access from IP segments that administrators may use.


1. Edit the /etc/hosts.deny configuration file to disable all IP connections via SSH.

   > You can also identify security risks of the instance by checking the SSH status or viewing IPs with suspicious malicious login attempts. After this, disable these addresses in /etc/hosts.deny.   
   

   1. [Log in to the instance](https://docs.byteplus.com/en/docs/ecs/Using-the-console-to-log-on-to-a-Linux-instance).

   2. Execute the following command to open the /etc/hosts.deny file.

      ```Bash
      vim /etc/hosts.deny
      ```
      

   3. Press `i`key to enter edit mode and add `sshd:all:deny`at the end.

   4. Press the `Esc` key to exit editing. Then, enter`:wq`, and press Enter to save and exit the vim editor.

2. Refer to Step 1 to edit the /etc/hosts.allow configuration file, and add `sshd:XXX.XXX.XXX.XXX:allow` at the end of the file to specify allowed IP address connections via SSH.

   Since you may need to log in to ECS instances in different locations, overly strict restrictions may affect normal use. We recommend you edit the /etc/hosts.allow file by adding `sshd:ALL` at the end of the file. This allows login from all IP addresses, and thereby ensures unaffected access to the instance.


**Windows instances**

For detailed steps to restrict IP access via Windows firewall, refer to [Configuring firewall policies for ECS instances on Windows Server](https://docs.byteplus.com/en/docs/ecs/Configuration_method_for_firewall_policies_on_ECS_instances_with_Windows_Server_system).
