---
title: "Managing migration tool Agent"
product: "Server Migration Center"
product_code: "smc"
source: "https://docs.byteplus.com/en/docs/smc/Management-Migration-Tool-Agent"
---

After installing migration tool Agent, you can manage Agent running status and modify its configuration file.

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">For the migration tool Agent installed before June 30, 2025, it is recommended to modify the <code>host</code> value in the Agent configuration file user_cfg.json to <code>smc.byteplusapi.com</code>, or <a href="https://docs.byteplus.com/en/docs/smc/Step-1-Import-Migration-Sources">download and install the migration tool Agent of the latest version​</a>.</div>


<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites

The migration tool Agent has been installed. For details, see [Importing migration sources](https://docs.byteplus.com/en/docs/smc/Step-1-Import-Migration-Sources).

<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure

<span id=".6YWN572u5Luj55CG5pyN5Yqh5Zmo5L-h5oGv"></span>
### Configure proxy server information

Migration commands of the migration tool Agent must be transmitted over the public network. Therefore, when data is migrated in the "Private network" mode, you also need to ensure that the source server can connect to BytePlus over the public network.


<Tabs>
<Tab zoneid="jMSuZe7y29" title="Linux operating system">
<TabTitle>Linux operating system</TabTitle>

1. Log in to the server where the migration tool Agent is installed.

2. Execute the following commands in the migration source to verify whether the migration source can access SMC over the public network.

   ```Plain Text
   ping smc.byteplusapi.com
   ```
   

   * If access succeeds, you do not need to configure a proxy server.

   * If access fails, check the public network configuration of the migration source, or configure a proxy server as follows to enable proxy\-based access.

      1. Configure the proxy server by referring to [Configuring proxy servers](https://docs.byteplus.com/en/docs/smc/Configuring-a-Proxy-Server).

      2. Execute the following command to stop Agent.

         ```Plain Text
         sudo ./smc_manage stop
         ```
         

      3. Execute the following command to open the tool user information configuration file.

         ```Plain Text
         vim user_cfg.json
         ```
         

      4. Press the `i` key to enter edit mode.

      5. Add the proxy server information to the file.

         * `ip_port` (required): Specifies the `private network IP address:port` of the proxy server. This indicates the source server is allowed to access the SMC service via the proxy server port.

         * `user_pwd`: Optional (required if the proxy server requires a login password). This parameter specifies the `username:password` for logging in to the proxy server.

            ```Plain Text
            "proxy": {
               "ip_port": "xx.xx.xx.xx:xx",
               "user_pwd": "xxxx:xxxx"
            }
            ```
            

      6. Press `ESC`, enter `:wq`, and then press Enter to save the modifications and close the file.

3. After the modification, you can execute the following command to start the migration tool Agent and import migration source information.

   ```Plain Text
   sudo ./smc_manage start
   ```
   


</Tab>
<Tab zoneid="fR33Nn8w4G" title="Windows operating system">
<TabTitle>Windows operating system</TabTitle>

1. Log in to the server where the migration tool Agent is installed.

2. Execute the following commands via PowerShell in the migration source to verify whether the migration source can access SMC over the public network.

   ```Plain Text
   ping smc.byteplusapi.com
   ```
   

   * If access succeeds, you do not need to configure a proxy server.

   * If access fails, check the public network configuration of the migration source, or configure a proxy server as follows to enable proxy\-based access.

      1. Configure the proxy server by referring to [Configuring proxy servers](https://docs.byteplus.com/en/docs/smc/Configuring-a-Proxy-Server).

      2. Enter the folder where Agent is located.

      3. Right\-click the user_cfg.json, select "Open with", and open the configuration file by using Notepad.

      4. Add the proxy server information to the file.

         * `ip_port` (required): Specifies the `private network IP address:port` of the proxy server. This indicates the source server is allowed to access the SMC service via the proxy server port.

         * `user_pwd`: Optional (required if the proxy server requires a login password). This parameter specifies the `username:password` for logging in to the proxy server.

         ```Plain Text
         "proxy": {
            "ip_port": "xx.xx.xx.xx:xx",
            "user_pwd": "xxxx:xxxx"
         }
         ```
         

      5. Save the changes and close the file.

3. After the modification, you can start the migration tool Agent and import migration source information.


</Tab>
</Tabs>


<span id=".5o6S6Zmk5peg6ZyA6L-B56e75paH5Lu25oiW55uu5b2V"></span>
### Exclude files or directories that you do not need to migrate

You can enter the paths of files and directories that you do not need to migrate to the platform in the Agent configuration file. SMC will then not migrate the corresponding files or directories.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">This feature is not supported when the source server operating system is Windows.</div>



1. Log in to the server where the migration tool Agent is installed.

2. Execute the following command to enter the directory where the migration tool Agent is located.

   ```Plain Text
   cd <Agent directory>
   ```
   

3. Execute the following command to stop Agent.

   ```Plain Text
   sudo ./smc_manage stop
   ```
   

4. Execute the following command to open the excludes.txt file.

   ```Plain Text
   vim excludes.txt
   ```
   

5. Press the `i` key and enter the path of the file or directory that does not need to be migrated.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">You need to enter the relative path of the file/directory relative to the mount point of its residing directory. For example, to exclude the file /etc/test.txt, enter test.txt as the relative path.   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">In the excludes.txt file, only modify the content that you have manually written in. Do not modify the original content of the file.   </div>
   

6. Press the `ESC` key to exit editing, enter `:wq`, and press Enter to save the changes and exit the file.

7. After the modification, you can execute the following command to start the migration tool Agent and import migration source information.

   ```Plain Text
   sudo ./smc_manage start
   ```
   


<span id=".5L-u5pS5QWNjZXNzIEtlee-8iOWvhumSpe-8iQ=="></span>
### Modify Access Key

If the Access Key ID and Secret Access Key you entered are incorrect or you need to update the key configuration, follow the steps below to modify the configuration:

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">This feature is not supported when the source server operating system is Windows.</div>



1. Log in to the server where the migration tool Agent is installed.

2. Execute the following command to enter the directory where the migration tool Agent is located.

   ```Plain Text
   cd <Agent所在目录>
   ```
   

3. Execute the following command to stop Agent.

   ```Plain Text
   sudo ./smc_manage stop
   ```
   

4. Execute the following command to open the user information configuration file.

   ```Plain Text
   vim user_cfg.json
   ```
   

5. Press the `i` key to enter edit mode.

6. Delete the existing values of `ak` and `sk` parameters in the file, and enter the new Access Key ID and Secret Access Key. To obtain platform Access Key (API access key), see [Managing an access key](https://docs.byteplus.com/en/docs/byteplus-platform/docs-managing-an-accesskey).

7. Press the `ESC` key to exit editing, enter `:wq`, and press Enter to save the changes and exit the file.

8. After the modification, you can execute the following command to start the migration tool Agent and import migration source information.

   ```Plain Text
   sudo ./smc_manage start
   ```
   


<span id=".5oyH5a6a6L-B56e75rqQ5omA5bGe6aG555uu"></span>
### Specify the owning project of the migration source

You can specify the project to which the imported migration source belongs to facilitate management. For more project details, refer to [Project management](https://docs.byteplus.com/en/docs/ecs/Managing-projects).


<Tabs>
<Tab zoneid="Mi8shiPcuu" title="Linux operating system">
<TabTitle>Linux operating system</TabTitle>

1. Log in to the server where Agent is installed.

2. Execute the following command to stop Agent.

   ```Plain Text
   sudo ./smc_manage stop
   ```
   

3. Execute the following command to open the tool user information configuration file.

   ```Plain Text
   vim user_cfg.json
   ```
   

4. Press the `i` key to enter edit mode.

5. Modify the `projectName` parameter value in the file to the target project name.

6. Press `ESC`, enter `:wq`, and then press Enter to save the modifications and close the file.

7. After the modification, you can execute the following command to start the migration tool Agent and import migration source information.

   ```Plain Text
   sudo ./smc_manage start
   ```
   


</Tab>
<Tab zoneid="wbcBUkoJye" title="Windows operating system">
<TabTitle>Windows operating system</TabTitle>

1. Log in to the server where the migration tool Agent is installed.

2. Enter the folder where Agent is located.

3. Right\-click the user_cfg.json, select "Open with", and open the configuration file by using Notepad.

4. Modify the `projectName` parameter value to the target project name.

   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">By default, the project is <code>default</code>.   </div>
   

5. Save the changes and close the file.

6. After modification, you can start Agent and import migration source information.


</Tab>
</Tabs>
