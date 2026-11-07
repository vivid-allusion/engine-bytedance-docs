---
title: "Manually installing migration tool Agent and importing migration sources"
product: "Server Migration Center"
product_code: "smc"
source: "https://docs.byteplus.com/en/docs/smc/Step-1-Import-Migration-Sources"
---

Before using Server Migration Center (SMC) to migrate a migration source to the platform, you need to first import the migration source information and connect it to your platform account via the migration tool Agent.

This topic describes the procedure for manually installing the migration tool Agent and importing the migration source.

<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites

Make sure that you have completed the preparations as required. For details, see [Preparations](https://docs.byteplus.com/en/docs/smc/Preparations).

<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure

You need to install the migration tool Agent on the migration source. The Agent can collect migration source information and import it to the platform.

<span id=".5q2l6aqk5LiA77ya5a-85YWl6L-B56e75rqQ"></span>
### Step 1: Import the migration source


<Tabs>
<Tab zoneid="nBbHrSp7lI" title="Linux operating system">
<TabTitle>Linux operating system</TabTitle>

1. Log in to the source server to be migrated.

2. Execute the following command to download the migration tool agent over the public network.

   ```Plain Text
   sudo wget -O smc-agent_Linux_amd64.tar.gz https://smc.tos-ap-southeast-1.bytepluses.com/smc-agent_Linux_amd64.tar.gz
   ```
   

   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">You can also use any server connected to the public network to download the migration tool Agent, and then upload the Agent to the source server to be migrated via FTP or other tools. For more information, see <a href="https://docs.byteplus.com/en/docs/ecs/Uploading-local-data">Overview of local data upload</a>.   </div>
   

3. Execute the following command to decompress and start the migration tool Agent, and import the source server information to the platform.

   ```Plain Text
   sudo tar -zxvf smc-agent_Linux_amd64.tar.gz && sudo ./smc_manage start -ak <your_access_key> -sk <your_secret_key>
   ```
   

   <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="1">warning   </div>
   

   * <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">You need to run the migration tool Agent with administrator (root) privileges.   </div>
   

   * <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">Replace <code><your_access_key></code> and <code><your_secret_key></code> with the actual API Access Key. For information about how to obtain an Access Key, see <a href="https://docs.byteplus.com/en/docs/byteplus-platform/docs-managing-an-accesskey">Managing an access key</a>.   </div>
   

   * <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">After the Agent starts running, it will generate a temporary key pair id_rsa (temporary private key) and id_rsa.pub (temporary public key) in the smc_tools directory.   </div>
   

      * <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">The target instance or relay instance will use this temporary key pair during the migration process. This reduces the risk of leakage of your proprietary key and ensures your key security.   </div>
   

      * <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">Do not delete this key pair. Otherwise, the migration will fail.   </div>
   

      * <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">To resolve migration failure caused by accidental deletion of the key pair, you can execute the <code>sudo ./smc_manage stop</code> and <code>sudo ./smc_manage start</code> commands in the directory where the migration Agent is located to restart the Agent. This will allow you to re\-import the migration source and generate a temporary key pair.   </div>
   

      * <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">After a successful migration, use the source server login credentials (password or key pair) to log in to the target instance or custom image.   </div>
   

   * <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">After decompression, you will obtain the following files:   </div>
   

   <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">   
   |<strong>File name</strong> |<strong>Description</strong> |
   |---|---|
   |Linux\-version |The version information of the current package. |
   |smc_agent |The binary file serving as the main file of the migration tool. |
   |smc_manage |The binary file serving as the migration management tool. |
   |agent_cfg.json |The JSON file used to record migration process information. |
   |excludes.txt |The txt file. The paths of files and directories not to be migrated need to be written into this file. |
   |user_cfg.json |The JSON file serving as the user information configuration file. |
   |smc_tools |The folder containing temporary key pairs, block replication tools, detection scripts, and other content used by SMC during the migration process. |
      </div>
   

4. When the migration tool Agent starts as expected, it will upload migration source information to SMC.

   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">Do not close the migration tool Agent before the import process completes. Otherwise, the migration source will disconnect from the SMC console, and the import will fail.   </div>
   

5. You can execute the following command in the directory where the Agent is running to view the `SourceId` (migration source ID) and Agent running logs to troubleshoot migration issues.

   ```Plain Text
   tail -f smc.log
   ```
   

   Sample output

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_6b8cce27c5e56984ac948064af6f6e01.png) </span>


**Related operation**

You can also perform the following operations on the migration Agent.


|**Operation** |**Description** |
|---|---|
|```Bash```<br>```sudo ./smc_manage start```<br> |Start the Agent. |
|```Bash```<br>```sudo ./smc_manage stop```<br> |Stop the Agent. |
|[Configure proxy server information](https://docs.byteplus.com/en/docs/smc/Management-Migration-Tool-Agent#.6YWN572u5Luj55CG5pyN5Yqh5Zmo5L-h5oGv) |When the source server accesses the public network through a proxy, you need to configure proxy server information for the Agent as well. |
|[Exclude files or directories that do not need to be migrated](https://docs.byteplus.com/en/docs/smc/Management-Migration-Tool-Agent#.5o6S6Zmk5peg6ZyA6L-B56e75paH5Lu25oiW55uu5b2V) |You can add information about files that do not need to be migrated to prevent their data from being migrated to the platform. |
|[Modify the Access Key](https://docs.byteplus.com/en/docs/smc/Management-Migration-Tool-Agent#.5L-u5pS5QWNjZXNzIEtlee-8iOWvhumSpe-8iQ==) |If the key you entered is incorrect or you need to change the key configuration, you can modify the Access Key. |
|[Specify the project associated with the migration source](https://docs.byteplus.com/en/docs/smc/Management-Migration-Tool-Agent#.5oyH5a6a6L-B56e75rqQ5omA5bGe6aG555uu) |You can specify the project to which the imported migration source belongs to facilitate management. |





</Tab>
<Tab zoneid="iY7v8seUpM" title="Windows operating system">
<TabTitle>Windows operating system</TabTitle>

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">Since the Windows operating system only supports data migration by using block replication, excluding files or directories that do not need to be migrated is not supported.</div>



1. Log in to the source server to be migrated.

2. You can download and run the migration tool Agent through **PowerShell** or **graphical user interface**.

   <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="1">warning   </div>
   

   * <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">You can also use any server connected to the public network to download the migration tool Agent, and then upload the Agent to the source server to be migrated via FTP or other tools. For more information, see <a href="https://docs.byteplus.com/en/docs/ecs/Uploading-local-data">Overview of local data upload</a>.   </div>
   

   * <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">You need to run the migration tool as an administrator.   </div>
   

   * <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">Antivirus software may prohibit the migration tool from running. Check the antivirus software configuration.   </div>
   

   * <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">Once the Agent starts running, it will automatically generate the smc.txt file to record the Agent running logs, facilitating the troubleshooting of migration issues.   </div>
   

   * **PowerShell**

      1. Execute the following command in PowerShell to download the migration tool Agent.

         ```PowerShell
         (New-Object -TypeName System.Net.WebClient).DownloadFile('https://smc.tos-ap-southeast-1.bytepluses.com/smc-agent_Windows_x86_64.zip', 'C:\smc-agent_Windows_x86_64.zip') 
         ```
         

         <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="3">tip         </div>
         

         <div data-tips="true" data-tips-type="default" data-wrapper-indent="3">By default, it is downloaded to the <code>C:\</code> directory.         </div>
         

      2. Execute the following command in PowerShell to decompress the migration tool Agent package.

         
         <Tabs>
         <Tab zoneid="OX28EkCqYA" title="Use Unzip for decompression">
         <TabTitle>Use Unzip for decompression</TabTitle>
         
         &nbsp;
         
         ```PowerShell
         cd C:\ ; unzip -o .\smc-agent_Windows_x86_64.zip ; C:\smc_agent -autostart=true -ak=<your_access_key> -sk=<your_secret_key> 
         ```
         
         
         
         
         
         </Tab>
         <Tab zoneid="hueJH7twPh" title="PowerShell 5.0 or later">
         <TabTitle>PowerShell 5.0 or later</TabTitle>
         
         &nbsp;
         
         ```PowerShell
         cd C:\ ; Expand-Archive -LiteralPath 'C:\smc-agent_Windows_x86_64.zip' -DestinationPath C:\ ; C:\smc_agent -autostart=true -ak=<your_access_key> -sk=<your_secret_key>
         ```
         
         
         
         
         
         </Tab>
         <Tab zoneid="IXwXskizwa" title="PowerShell 3.0 or later">
         <TabTitle>PowerShell 3.0 or later</TabTitle>
         
         &nbsp;
         
         ```PowerShell
         powershell.exe -nologo -noprofile -command "& { Add-Type -A 'System.IO.Compression.FileSystem'; [IO.Compression.ZipFile]::ExtractToDirectory('C:\smc-agent_Windows_x86_64.zip', 'C:\'); }" ; C:\smc_agent -autostart=true -ak=<your_access_key> -sk=<your_secret_key>
         ```
         
         
         
         
         
         </Tab>
         </Tabs>
         

         <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="3">tip         </div>
         

         * <div data-tips="true" data-tips-type="default" data-wrapper-indent="3">Replace <code><your_access_key></code> and <code><your_secret_key></code> with the actual API Access Key. For information about how to obtain an Access Key, see <a href="https://docs.byteplus.com/en/docs/byteplus-platform/docs-managing-an-accesskey">Managing an access key</a>.         </div>
         

         * <div data-tips="true" data-tips-type="default" data-wrapper-indent="3">After decompression, you will obtain the following files:         </div>
         

   <div data-tips="true" data-tips-type="default" data-wrapper-indent="3">   
   |<strong>File name</strong> |<strong>Description</strong> |
   |---|---|
   |Windows\-version.txt |The version information of the current Agent. |
   |smc_agent.exe |The application file serving as the main file of the migration tool. |
   |agent_cfg.json |The JSON file used to record migration process information. |
   |user_cfg.json |The JSON file serving as the user information configuration file. |
   |bin |The folder where binary files are stored. |
   |sciter.dll |The library file required by the migration tool. |
   |notice.txt |The compliance specifications for the migration tool. |
      </div>
   

      3. The system will automatically open the migration Agent graphical user interface, fill in the Access Key provided in the command, and automatically import migration source information.

   * **Graphical user interface**

      1. Log in to the source server.

      2. Open the [Agent download link](https://smc.tos-cn-beijing.volces.com/smc-agent_Windows_x86_64.zip) in your browser to download the migration tool Agent.

         <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="3">tip         </div>
         

         <div data-tips="true" data-tips-type="default" data-wrapper-indent="3">You can also use any server connected to the public network to download the migration tool Agent, and then upload the Agent to the source server to be migrated via FTP or other tools. For more information, see <a href="https://docs.byteplus.com/en/docs/ecs/Uploading-local-data">Overview of local data upload</a>.         </div>
         

      3. Decompress the migration tool package. For details about the files obtained after decompression, see [Agent file information](https://vsop-online.bytedance.net/doc/manage/detail/85008/detail/?DocumentID=1407757&lang=zh#file).

      4. Right\-click smc_agent.exe and click "Run as administrator" to run the migration tool Agent.

      5. Enter the Access Key ID and Secret Access Key contained in the platform Access Key, and click the "Run" button to start the migration Agent.

         <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="3">tip         </div>
         

         <div data-tips="true" data-tips-type="default" data-wrapper-indent="3">For information about how to obtain an Access Key, see <a href="https://docs.byteplus.com/en/docs/byteplus-platform/docs-managing-an-accesskey">Managing an access key</a>.         </div>
         

3. When the migration tool Agent starts as expected, it will upload migration source information to SMC.

   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">Do not close the migration tool Agent before the import process completes. Otherwise, the migration source will disconnect from the SMC console, and the import will fail.   </div>
   

4. You can view the Agent running log file smc.txt in the directory where the Agent is running to obtain the SourceId (migration source ID) and Agent running logs, which helps troubleshoot migration issues.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_5d4830ef91b93dcc30b00f1164ecf3ec.png) </span>


**Related operation**

You can also perform the following operations on the migration Agent.


|**Operation** |**Description** |
|---|---|
|[Configure proxy server information](https://docs.byteplus.com/en/docs/smc/Management-Migration-Tool-Agent#.6YWN572u5Luj55CG5pyN5Yqh5Zmo5L-h5oGv) |When the source server accesses the public network through a proxy, you need to configure proxy server information for the Agent as well. |
|[Specify the project associated with the migration source](https://docs.byteplus.com/en/docs/smc/Management-Migration-Tool-Agent#.5oyH5a6a6L-B56e75rqQ5omA5bGe6aG555uu) |You can specify the project to which the imported migration source belongs to facilitate management. |





</Tab>
</Tabs>


<span id=".5q2l6aqk5LqM77ya6YCa6L-H6L-B56e75rqQ6aKE5qOA"></span>
### Step 2: Perform a precheck on the migration source

SMC will automatically perform a precheck on the migration source when you import the source, helping eliminate configurations that do not meet migration requirements.


1. View the precheck result. [Learn more](https://docs.byteplus.com/en/docs/smc/Perform-a-migration-precheck#.5p-l55yL6aKE5qOA5oql5ZGK).

2. Based on the precheck result of the migration source, you can fix exceptions in each [check item](https://docs.byteplus.com/en/docs/smc/Test-item-description) and [perform the precheck on the migration source again](https://docs.byteplus.com/en/docs/smc/Perform-a-migration-precheck#.6L-b6KGM6L-B56e75rqQ6aKE5qOA).

3. After the migration source passes the precheck, you can create a migration task for it to migrate data from the source server to the platform. [Learn more](https://docs.byteplus.com/en/docs/smc/Step-2-Create-and-launch-the-migration-task).


**Related operation**

You can also perform the following operations on the migration source.


|Operation |Description |
|---|---|
|[View migration source details](https://docs.byteplus.com/en/docs/smc/Managing-Migration-Sources#.5p-l55yL6L-B56e75rqQ6K-m5oOF) |You can view basic information, attributes, and disk details of the migration source to confirm whether the target instance specified in the migration task can support the migration source data. |
|[Modify basic information of the migration source](https://docs.byteplus.com/en/docs/smc/Managing-Migration-Sources#.5L-u5pS56L-B56e75rqQ5Z-656GA5L-h5oGv) |You can modify the migration source name to distinguish between different migration sources. |
|[Delete the migration source](https://docs.byteplus.com/en/docs/smc/Managing-Migration-Sources#.5Yig6Zmk6L-B56e75rqQ) |You can delete the migration source that is no longer used. |


<span id="8eCNX72Z"></span>
## Subsequent operations

After the migration source is imported, we recommend that you [create and start a migration task](https://docs.byteplus.com/en/docs/smc/Step-2-Create-and-launch-the-migration-task) within 24 hours to prevent the migration tool Agent from going offline due to prolonged idleness of the migration source.
