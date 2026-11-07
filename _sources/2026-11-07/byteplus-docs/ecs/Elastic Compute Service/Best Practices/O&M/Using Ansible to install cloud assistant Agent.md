---
title: "Using Ansible to install cloud assistant Agent"
product: "Elastic Compute Service"
product_code: "ecs"
source: "https://docs.byteplus.com/en/docs/ecs/Installing-Cloud-assistant-Agent-using-Ansible"
---

This topic describes how to use the open\-source tool Ansible to batch install cloud assistant Agent for Linux ECS instances.

<span id=".5LuA5LmI5pivQW5zaWJsZe-8nw=="></span>
## What is Ansible

Ansible is an open\-source tool for IT automation, which is developed based on Python. It is simple to use, secure, and reliable, with OpenSSH used for transmitting data (other transmission modes, such as the pull mode, are also supported). It is used to automatically configure, deploy applications, perform orchestration, and complete other remote tasks on managed nodes. For more details, see [Ansible](https://docs.ansible.com/ansible/latest/index.html).

<span id=".5ZCN6K-N6Kej6YeK"></span>
## Terms


|Term |Description |
|---|---|
|Primary control node |Server with Ansible installed. It remotely logs in to and manages managed nodes via the SSH protocol. |
|Managed node |The server to be managed by Ansible. In this practice, it refers to ECS instances on which cloud assistant Agent is to be installed. |


<span id=".5L2_55So6K-05piO"></span>
## Usage notes


|Nodes |Description |
|---|---|
|Primary control node |* Non\-Windows servers.<br><br>* An associated EIP is required. For more information, see [Associating EIPs](https://docs.byteplus.com/en/docs/ecs/associating-an-EIP).<br><br>* Installing Ansible is required.<br><br>* For more requirements, please view [Control node requirements](https://docs.ansible.com/ansible/latest/installation_guide/intro_installation.html#control-node-requirements). |
|Managed node |* An associated EIP is required. For more information, see [Associating EIPs](https://docs.byteplus.com/en/docs/ecs/associating-an-EIP).<br><br>* Installing Ansible is not required.<br><br>* For detailed requirements, see [Managed node requirements](https://docs.ansible.com/ansible/latest/installation_guide/intro_installation.html#managed-node-requirements). |


<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure


1. Install Ansible on the primary control node.

   > In the example provided in this practice, an ECS instance with the operating system CentOS 7.9 serves as the primary control node. To install Ansible on more operating systems, see[ Installation guide](https://docs.ansible.com/ansible/latest/installation_guide/index.html).   
   

   1. Log in to the ECS instance serving as the primary control node. For more information, see [Logging in to Linux instances](https://docs.byteplus.com/en/docs/ecs/Logging-on-to-a-Linux-instance).

   2. Execute the following command to install EPEL repository.

      ```Plain Text
      yum install -y epel-release
      ```
      

   3. Execute the following command to install Ansible.

      ```Plain Text
      yum install -y ansible
      ```
      

2. Configure Ansible.

   1. Execute the following command to add EIPs of servers serving as managed nodes.

      ```Plain Text
      vim /etc/ansible/hosts
      ```
      

   2. Press the `i` key to add EIP addresses of managed nodes.

      <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="2">tip      </div>
      

      <div data-tips="true" data-tips-type="tip" data-wrapper-indent="2">You can also group different IP addresses in the format of <code>[$groupname$]</code> for easier batch operations by group. To learn more about Ansible grouping, see <a href="https://docs.ansible.com/ansible/latest/inventory_guide/intro_inventory.html#inventory-basics-formats-hosts-and-groups">Inventory basics</a>      </div>
      

      For example, instances can be divided into two groups: `[keypair]` (key pair\-based login) and `[password]` (password\-based login).

      <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_f8f3c0f922cef2c15e9fb2119849e3ad.png) </span>

   3. Press `esc` and enter `:wq` to save the change and exit.

   4. Execute the following command to modify the Ansible configuration file.

      ```Plain Text
      vim /etc/ansible/ansible.cfg
      ```
      

   5. Press the `/` key and enter `host_key_checking` to search for the keyword.

   6. At the beginning of the line containing `host_key_checking = False`, delete the `#` (comment character).

      <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="2">tip      </div>
      

      <div data-tips="true" data-tips-type="tip" data-wrapper-indent="2">After performing the above steps, you do not need to verify via SSH host key when logging in to managed nodes for the first time.      </div>
      

      <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_76c82944d318d0ba92742bffe330cb17.png) </span>

   7. Press `esc` and enter `:wq` to save the change and exit.

3. (Optional) When logging in to a managed node by using a key pair, you can create a private key file for login.

   1. Execute the following command to create and edit the private key file.

      > In this practice, all managed nodes with key pair\-based login use the same key pair.      
      

      ```Plain Text
      vim /root/key.pem
      ```
      

   2. Press the `i` key to paste the private key information into this file.

   3. Press `esc` and enter `:wq` to save the change and exit.

   4. Execute the following command to add read/write permissions on the private key file.

      ```Plain Text
      chmod 600 /root/key.pem
      ```
      

4. Install cloud assistant Agent on managed nodes.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">In the example provided in this practice, after cloud assistant Agent is installed, restarting managed nodes is not required.   </div>
   

   * On the ECS instance serving as the primary control node, execute the following command to install Agent for ECS instances with key pair\-based login grouped in `[keypair]`.

      <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="2">tip      </div>
      

      * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="2">Replace <code>keypair</code> with actual group name.      </div>
      

      * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="2">Replace <code>~/key.pem</code> with actual path where the login key for managed nodes is stored.      </div>
      

      ```Plain Text
      sudo ansible -i /etc/ansible/hosts keypair -b --become-user=root -m shell -a  'sudo bash -c "$(curl https://assist-client.tos-cn-beijing.volces.com/install.sh)"'  --private-key=~/key.pem
      ```
      

      You can view the installation progress and results for each instance based on script responses.

      <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_07b2c5dfbac4968988697246a369fe01.png) </span>

   * On the ECS instance serving as the primary control node, execute the following command and enter the login password of the managed node. This enables you to install Agent for the instance with password\-based login grouped in `[password]`.

      <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="2">tip      </div>
      

      <div data-tips="true" data-tips-type="tip" data-wrapper-indent="2">Replace <code>password</code> with the actual group name.      </div>
      

      ```Plain Text
      sudo ansible -i /etc/ansible/hosts password -b --become-user=root -m shell -a  'sudo bash -c "$(curl https://assist-client.tos-cn-beijing.volces.com/install.sh)"'  -k
      ```
      

      <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_ef63affe8318f1f6d9e8a013cc801a65.png) </span>

5. Check the running status of cloud assistant Agent on each managed node.

   * Execute the following command to view the Agent status on ECS instances with key pair\-based login and grouped in `[keypair]`.

      ```Plain Text
      sudo ansible -i /etc/ansible/hosts keypair -b --become-user=root -m shell -a  'systemctl status assist-client.service'  --private-key=~/key.pem
      ```
      

      Sample instance in a normal status:

      <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_75f54b79eba8713d36014f89ad935d92.png) </span>

   * To view the Agent status on the ECS instance with password\-based login grouped in `[password]`, execute the following command and then enter the login password of the managed node.

      ```Plain Text
      sudo ansible -i /etc/ansible/hosts password -b --become-user=root -m shell -a  'systemctl status assist-client.service'  -k
      ```
      

      Sample instance in a normal status:

      <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_4d43c8b7023386ccb6597d729737cf08.png) </span>
