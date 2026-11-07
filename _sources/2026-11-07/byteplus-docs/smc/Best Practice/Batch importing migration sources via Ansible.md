---
title: "Batch importing migration sources via Ansible"
product: "Server Migration Center"
product_code: "smc"
source: "https://docs.byteplus.com/en/docs/smc/Use_Ansible_to_batch_import_Migration_Sources"
---

This topic describes how to use the open\-source tool Ansible to batch import source servers running Linux or Windows into the platform.

<span id=".5LuA5LmI5pivQW5zaWJsZe-8nw=="></span>
## Scenario

Before importing the migration source, you need to complete operations such as downloading and installing the migration tool Agent, modifying configuration files, and starting services on the source server. When there are many source servers to be migrated, these configurations are repetitive and cumbersome. Ansible is an open source IT automation tool developed in Python. It is simple to use, secure, and reliable. It can perform automated configurations, application deployments, orchestrations, and other tasks on multiple managed nodes remotely, helping you quickly configure and import source server. [Learn more](https://docs.ansible.com/ansible/latest/index.html).

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">If you need to batch migrate servers from different cloud vendors to BytePlus, it is recommended to use the <a href="https://docs.byteplus.com/en/docs/smc/One-click_import_from_the_console">One\-click import from the console</a> feature to batch import multiple sources.</div>


<span id=".5ZCN6K-N6Kej6YeK"></span>
## Terms


|Term |Description |
|---|---|
|Primary control node |Refers to the server on which the Ansible tool is installed, and from which you can remotely connect to and manage managed nodes via protocols such as SSH or WinRm. |
|Managed node |Refers to servers that are managed by Ansible. In the context of this migration practice, they specifically refer to the source servers that need to be imported into the platform. |


<span id=".5L2_55So6K-05piO"></span>
## Usage notes


|Nodes |Description |
|---|---|
|Primary control node |* Linux operating system server.<br><br>* Installed Python 2.7+ or Python 3.5+ versions, [Learn more](https://docs.byteplus.com/en/docs/ecs/Setting_up_Python_environment).<br><br>* An EIP has been associated.<br><br>* For more requirements, refer to [Control node requirements](https://docs.ansible.com/ansible/latest/installation_guide/intro_installation.html#control-node-requirements). |
|Managed node |* An EIP needs to be associated.<br><br>* Python version 2.6+ or Python 3.5+ is already installed, [Learn more](https://docs.byteplus.com/en/docs/ecs/Setting_up_Python_environment).<br><br>* If the source server is a Windows operating system, you must also meet the following:<br><br>   * Powershell version must be no less than 3.0.<br><br>   * The .Net framework version must not be lower than 4.0.<br><br>* For detailed requirements, see [Managed node requirements](https://docs.ansible.com/ansible/latest/installation_guide/intro_installation.html#managed-node-requirements). |


<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure

<span id="enbuNL8G"></span>
### Step 1: Configure the primary control node

Install and configure the Ansible tool as the primary control node on any Linux server that can access the internet.


1. Log in to the server serving as the primary control node.

2. When logging in to a managed node by using a key pair, please create a private key file for login.

   1. Execute the following command to create a new private key file.

      ```Plain Text
      vim /root/linux_1.pem
      ```
      

      <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="2">tip      </div>
      

      <div data-tips="true" data-tips-type="default" data-wrapper-indent="2">Please replace <code>linux_1</code> with your desired private key file name.      </div>
      

   2. Press the `i` key and paste the private key information for logging in to the target instance into this file.

   3. Press `esc` and type `:wq`, to save the change and exit.

   4. Execute the following command to add read/write permissions on the private key file.

      ```Plain Text
      chmod 600 /root/linux_1.pem
      ```
      

   5. Replace ~/key.pem with actual path where the login key for managed nodes is stored.

      <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="2">tip      </div>
      

      <div data-tips="true" data-tips-type="default" data-wrapper-indent="2">This practice has created two private key files: <code>/root/linux_1.pem</code> and <code>/root/linux_2.pem</code>.      </div>
      

3. Execute the following command to install the dependency tools.

   * If there is a Linux operating system server as a managed node, execute the following command to install the dependencies.

      ```Plain Text
      sudo apt update
      sudo apt install -y sshpass
      ```
      

   * If there is a Windows operating system server as a managed node, execute the following command to install the dependencies.

      ```Plain Text
      pip3 install pywinrm
      ```
      

4. Install Ansible.

   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">For more installation methods of the operating system, see the <a href="https://docs.ansible.com/ansible/latest/installation_guide/index.html">Installation Guide</a>.   </div>
   

   
   <Tabs>
   <Tab zoneid="dirySVrpPp" title="Ubuntu">
   <TabTitle>Ubuntu</TabTitle>
   
   &nbsp;
   
   ```Plain Text
   sudo apt update
   sudo apt install -y software-properties-common
   sudo apt-add-repository --yes --update ppa:ansible/ansible
   sudo apt install -y ansible
   ```
   
   
   
   
   
   </Tab>
   <Tab zoneid="wUA1wWmdhr" title="CentOS">
   <TabTitle>CentOS</TabTitle>
   
   &nbsp;
   
   ```Plain Text
   yum install -y epel-release
   sudo yum install -y ansible
   ```
   
   
   
   
   
   </Tab>
   </Tabs>
   

5. Configure Ansible.

   1. Execute the following command to add EIPs of servers serving as managed nodes.

      ```Plain Text
      vim /etc/ansible/hosts
      ```
      

   2. Press the `i` key to add the EIP addresses of managed servers.

      * If the managed node server uses a Linux operating system:

         * When using password for login, configure in the format `<EIP> ansible_ssh_user=<username> ansible_ssh_pass=<Password>`.

         * When using key pair for login, configure in the format `<EIP> ansible_ssh_user=<username> ansible_ssh_private_key_file=<path to private key file>`.

      * If the managed node server uses a Linux operating system:

         * When using password login, configure in the format `<EIP> ansible_user=<username> ansible_password=<Password> ansible_port=5985 ansible_connection=winrm ansible_winrm_transport=basic ansible_winrm_server_cert_validation=ignore`.

      <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="2">tip      </div>
      

      <div data-tips="true" data-tips-type="tip" data-wrapper-indent="2">You can also group IP addresses by <code>[$groupname$]</code> for easy batch operations by group. To learn more about Ansible grouping, see <a href="https://docs.ansible.com/ansible/latest/inventory_guide/intro_inventory.html#inventory-basics-formats-hosts-and-groups">Inventory basics</a>.      </div>
      

      For example, you can group into two groups based on the operating system type of the managed node server: `[linux_smc]` (Linux operating system) and `[windows_smc]` (Windows operating system).

      <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_21326147bc70a3f24a66d79d47d923d2.png) </span>

   3. Press `esc` and enter `:wq` to save the change and exit.

   4. Edit the Ansible configuration file.

      1. Execute the following command to generate the Ansible configuration file.

         ```Plain Text
         ansible-config init --disabled -t all > ansible.cfg
         ```
         

      2. Execute the following command to modify the Ansible configuration file.

         ```Plain Text
         vim /etc/ansible/ansible.cfg
         ```
         

      5. Press the `/` key and input `host_key_checking` as the search term.

      6. Remove the comment symbol at the beginning of `host_key_checking = True` and modify the argument value to `False`.

         <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_d24e9ea447f1a5ca86c9d838285d8755.png) </span>

      7. Press `esc` and enter `:wq` to save the change and exit.


<span id="5t4Ra1RP"></span>
### Step 2: Configure the managed node (Optional)

If the server to be migrated uses the Windows operating system, follow the guidance in this section to complete the configuration.


1. Log in to the Windows server as the managed node.

2. Click the Windows icon, right\-click "Windows PowerShell" in the Windows PowerShell directory, and then select "More \> Run as administrator".

3. Execute the following command in PowerShell to view whether the WinRm listener service has been enabled.

   ```PowerShell
   winrm enumerate winrm/config/Listener
   ```
   

   * If the listener service is already enabled, please skip this step.

      <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_f22218dc46e5316ceccc9ce6b898980a.png) </span>

   * If the listener service is not enabled, please follow the instructions below to create the WinRm HTTP(s) listener service.

      1. Execute the following command in PowerShell to enable the WinRm remote connection feature.

         ```PowerShell
         Enable-PSRemoting –force 
         ```
         

      2. Execute the following command in PowerShell to create a listener service.

         <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="3">tip         </div>
         

         <div data-tips="true" data-tips-type="default" data-wrapper-indent="3">For HTTP and HTTPS listener services, please choose either one as needed.         </div>
         

         
         <Tabs>
         <Tab zoneid="GCxW5FC0VS" title="Create HTTP listener">
         <TabTitle>Create HTTP listener</TabTitle>
         
         &nbsp;
         
         ```PowerShell
         winrm quickconfig
         ```
         
         
         
         
         
         </Tab>
         <Tab zoneid="UaRvvszfKE" title="Create HTTPS listener">
         <TabTitle>Create HTTPS listener</TabTitle>
         
         &nbsp;
         
         ```PowerShell
         winrm quickconfig -transport:https
         winrm set winrm/config/service '@{AllowUnencrypted="true"}'
         winrm set winrm/config/service/auth '@{Basic="true"}'
         ```
         
         
         
         
         
         </Tab>
         </Tabs>
         

4. Execute the following command in PowerShell to open the ports dependent on the service.

   * If the HTTP listener service has been enabled, please enable port `5985`.

      ```PowerShell
      New-NetFirewallRule -DisplayName "WinRM-HTTP-In-TCP" -Direction Inbound -Protocol TCP -LocalPort 5985 -Action Allow
      ```
      

   * If the HTTPS listener service has been enabled, please enable port `5986`.

      ```PowerShell
      New-NetFirewallRule -DisplayName "WinRM-HTTPS-In-TCP" -Direction Inbound -Protocol TCP -LocalPort 5986 -Action Allow
      ```
      

   <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="1">warning   </div>
   

   <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">When the managed node servers have security group configurations, it is also necessary to allow related port TCP connections in the <strong>inbound direction</strong> of the security group.   </div>
   

   * <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">If HTTP listening service is enabled, please allow the TCP protocol <code>5985</code> port.   </div>
   

   * <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">If HTTPS listening service is enabled, please allow the TCP protocol <code>5986</code> port.   </div>
   


<span id="WZvEV4Py"></span>
### Step 3: Batch create migration sources


1. Log in to the management node server.

2. Create a script for batch importing migration sources.

   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">Based on the OS type of managed nodes (i.e., source servers to be imported), create the corresponding script file. When both Linux and Windows operating systems exist on managed nodes, both scripts need to be created.   </div>
   

   
   <Tabs>
   <Tab zoneid="BTFe3r0reT" title="Import Linux server">
   <TabTitle>Import Linux server</TabTitle>
   
   1. Execute the following command to create a script file for batch import of Linux\-managed nodes.
   
      ```Plain Text
      vim /root/start_smc_linux.sh
      ```
      
   
   2. Press the `i` key to enter edit mode, and then copy and paste the following content into the file.
   
      ```Bash
      #!/bin/bash
      
      set -eux
      
      WORKDIR="/root"
      
      HOST="smc.byteplusapi.com" 
      
      AK="<your_ak>"
      SK="<your_sk>"
      
      REGION="ap-southeast-1"
      
      SOURCE="https://smc.tos-ap-southeast-1.bytepluses.com/smc-agent_Linux_amd64.tar.gz"
      
      mkdir -p "$WORKDIR"
      cd "$WORKDIR"
      
      wget -P /root $SOURCE
      mkdir -p smc/linux_smc && tar -zxvf smc-agent_Linux_amd64.tar.gz -C smc/linux_smc
      
      sed -i  's#\("ak": "\).*#\1'"${AK}"'",#g' user_cfg.json
      sed -i  's#\("sk": "\).*#\1'"${SK}"'",#g' user_cfg.json
      
      ansible linux_smc -m copy -a "src=/root/smc/linux_smc/ dest=/root"
      ansible linux_smc -m shell -a "cd /root && chmod +x smc_manage"
      ansible linux_smc -m shell -a "cd /root && chmod +x smc_agent"
      ansible linux_smc -m shell -a "cd /root && ./smc_manage start"
      ```
      
   
   3. Please replace `<your_ak>` and `<your_sk>` with the actual API access key of your BytePlus Account. For information about how to obtain an Access Key, see [Managing an access key](https://docs.byteplus.com/en/docs/byteplus-platform/docs-managing-an-accesskey).
   
   4. Press the `Esc` key to exit edit mode, enter `:wq`, and then press Enter to save and exit the file.
   
   
   </Tab>
   <Tab zoneid="vdLAX66Taz" title="Import Windows server">
   <TabTitle>Import Windows server</TabTitle>
   
   1. Execute the following command to create a script file for batch import of Linux\-managed nodes.
   
      ```Plain Text
      vim /root/start_smc_windows.sh
      ```
      
   
   2. Press the `i` key to enter edit mode, and then copy and paste the following content into the file.
   
      ```Bash
      #!/bin/bash
      
      set -eux
      
      WORKDIR="/root"
      
      HOST="smc.byteplusapi.com" 
      
      AK="<your_ak>"
      SK="<your_sk>"
      
      REGION="ap-southeast-1"
      
      SOURCE="https://smc.tos-ap-southeast-1.bytepluses.com/smc-agent_Windows_x86_64.zip"
      
      mkdir -p "$WORKDIR"
      cd "$WORKDIR"
      
      wget -P /root $SOURCE
      mkdir -p smc/windows_smc && unzip smc-agent_Windows_x86_64.zip -d smc/windows_smc
      
      ansible windows_smc -m win_copy -a "src=/root/smc/windows_smc/ dest=C:/Users/Administrator/Downloads/ansible"
      ansible windows_smc -m win_shell -a "cd C:\Users\Administrator\Downloads\ansible; .\smc_agent.exe -autostart=true -ak=${AK} -sk=${SK} "
      ```
      
   
   3. Please modify `<your_ak>` and `<your_sk>` to the actual API access key (AK) of your BytePlus Account. For information about how to obtain an Access Key, see [Managing an access key](https://docs.byteplus.com/en/docs/byteplus-platform/docs-managing-an-accesskey).
   
   4. Press the `Esc` key to exit edit mode, enter `:wq`, and then press Enter to save and exit the file.
   
   
   </Tab>
   </Tabs>
   

3. Execute the following command to run the batch import script.

   * Batch import Linux servers

      ```Plain Text
      /bin/bash /root/start_smc_linux.sh
      ```
      

   * Batch import Windows servers

      ```Plain Text
      /bin/bash /root/start_smc_windows.sh
      ```
      


<span id="AAaakcAg"></span>
## Subsequent operations

You can go to the SMC console [to view migration source details](https://docs.byteplus.com/en/docs/smc/Managing-Migration-Sources), and based on the [Server Migration Job](https://docs.byteplus.com/en/docs/smc/Server-Migration-Task) instructions, create and start migrating data from the source server.
