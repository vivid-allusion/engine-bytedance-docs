---
title: "Installing cloud assistant Agent"
product: "Elastic Compute Service"
product_code: "ecs"
source: "https://docs.byteplus.com/en/docs/ecs/Install-the-Cloud-Assistant-client"
---

Before using cloud assistant, you need to install the cloud assistant Agent on all target instances. Otherwise, target instances can not be specified as the execution objects in O&M tasks.

<span id=".5L2_55So6K-05piO"></span>
## Usage notes


* Currently, you can only install and use the cloud assistant Agent on instances running operating systems specified in​ the [Limits](https://docs.byteplus.com/en/docs/ecs/Overview-of-cloud-assistant#limits).

* If you are logging in to the Cloud Assistant console for the first time, follow the instructions to grant cross\-service access permissions to the cloud assistant.


<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure

<span id=".5Yib5bu65LqR5pyN5Yqh5Zmo5a6e5L6L5pe25a6J6KOF"></span>
### Install cloud assistant Agent during ECS instance creation

You can select the option of installing cloud assistant Agent when creating an ECS instance. This allows the cloud assistant Agent to be installed automatically after the instance is created.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Currently, this feature is supported only when you are creating instances based on operating systems from "Public Images" (CentOS images earlier than version 6.9 are excluded). For more details on supported images, refer to <a href="https://docs.byteplus.com/en/docs/ecs/Overview-of-cloud-assistant#limits">Limits</a>.</div>



1. Log in to the [ECS console](https://console.byteplus.com/ecs/instance). 

2. In the left\-side navigation pane, select "Instances & Images \> Instances".

3. Click the "Create instance" button to purchase an ECS instance. Then, configure the instance as the page guidance. For detailed operations, refer to [Purchasing instances via wizard](https://docs.byteplus.com/en/docs/ecs/Using-the-wizard-to-buy-ECS-instances).

4. At the bottom of the "Basic configuration" page, select the needed public image, and then check the option "Install cloud assistant agent on startup".

5. After the instance is started, view the cloud assistant Agent status to confirm whether the cloud assistant Agent is installed. For detailed operations, refer to [Viewing installation results](https://docs.byteplus.com/en/docs/ecs/Viewing-agent-installation-results).


<span id=".5bey5pyJ5LqR5pyN5Yqh5Zmo5a6e5L6L5a6J6KOF"></span>
### Install the cloud assistant Agent on the existing ECS instances

For existing ECS instances, you can install the cloud assistant Agent in the console or by logging in to the created instances to install the cloud assistant Agent.


<Tabs>
<Tab zoneid="rQpn3CzCHD" title="Install cloud assistant Agent in the console">
<TabTitle>Install cloud assistant Agent in the console</TabTitle>

You can go to the console to install the cloud assistant Agent for multiple instances at the same time. You need to restart the instances first to make the changes take effect.

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">Currently, this feature is not supported for Windows operating system instances. Please follow the guide in "Install cloud assistant Agent by executing the scripts manually" to install the cloud assistant Agent.</div>



1. Log in to the [ECS console](https://console.byteplus.com/ecs/instance). 

2.  Select "Monitoring \> Cloud assistant."

3. On theCloud assistantpage, select the "Client Management" tab.

4. Use any of the following methods to installCloud assistantclient.

   **Install the cloud assistant Agent on multiple instances**

   1. On the Agent management page, select multiple target instances that require the cloud assistant Agent installation.

      > You can select up to 50 instances at a time.      
      

   2. Click the "Install" button below the list.

   3. Confirm whether you can install selected instances. If you can not install some selected instances, click the "Disallow install instance" tab to resolve issues as instructed, and then install instances. Or ignore instances on the "Disallow install instance" tab first and click the "Confirm" button to install instances on the "Allow install instance" tab.

   4. After the installation is complete, the Installation result window pops up. Here, you can view the installation results. Then, click the "Restart" button to restart the instance for the cloud assistant Agent to take effect.

   **Install the cloud assistant Agent on one instance**

   1. Search for or query information about the target instance from the instance list.

   2. Click the "Install" button in the "Action" column on the right side of the target instance.

   3. After the installation is complete, the Installation result window pops up. Here, you can view the installation results. Then, click the "Restart" button to restart the instance for the cloud assistant Agent to take effect.

   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">If you do not want to restart the instance now, click the × icon in the upper\-right corner of the pop\-up window to exit. Later, you can <a href="https://docs.byteplus.com/en/docs/ecs/Restarting-instances">restart the instance</a> at your convenience.   </div>
   


</Tab>
<Tab zoneid="EgJlX9s52J" title="Install cloud assistant Agent by executing the scripts manually">
<TabTitle>Install cloud assistant Agent by executing the scripts manually</TabTitle>

You can manually execute the scripts provided by BytePlus in the instance to install the cloud assistant Agent. After successful installation, you do not need to restart the instance.


1. Log in to the instance. For more information, refer to [Login overview](https://docs.byteplus.com/en/docs/ecs/Overview-1).

2. Select installation commands based on operating system types.

   * **Windows operating system**

      <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="2">tip      </div>
      

\*BytePlusIf you use the script provided by Byteplus, the cloud assistant Agent will be installed at the "C:/ProgramData/AssistClient" directory by default.


* <div data-tips="true" data-tips-type="default" data-wrapper-indent="2">In this example, the CMD (Command Prompt) tool is used to execute related commands.</div>


      * Installation​ through intranet

         Due to differences in access regions, the executed commands also vary. Please input the corresponding command based on the actual region to install the cloud assistant Agent through the BytePlus intranet.

               * Command format: `curl http://assist-client-{region-code}.tos-{region-code}.ivolces.com/install.bat -o install.bat && install.bat`

            <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="4">tip            </div>
            

            <div data-tips="true" data-tips-type="default" data-wrapper-indent="4">Please replace {region\-code} with the actual Region code you are accessing.            </div>
            

               * Example: In the Beijing Region, please execute the following command to install the Cloud assistant client.

            ```Plain Text
            curl http://assist-client-cn-beijing.tos-cn-beijing.ivolces.com/install.bat -o install.bat && install.bat
            ```
            

      * Installation​ through internet

         If your ECS instance has been [associated with an EIP](https://docs.byteplus.com/en/docs/ecs/Assigning-or-releasing-a-private-IPv4-address), you can execute the following command on an instance in any region to install the cloud assistant Agent through the internet.

         ```Plain Text
         curl http://assist-client-cn-beijing.tos-cn-beijing.volces.com/install.bat -o install.bat && install.bat
         ```
         

   * **Linux operating system**

      <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="2">tip      </div>
      

\*BytePlusThe script provided by Byteplus installs the cloud assistant Agent into the "/usr/local/assist\-client" directory by default.


      * Installation​ through intranet

         Due to differences in access regions, the executed commands also vary. Please input the corresponding command based on the actual region to install the Cloud assistant client through the BytePlus intranet.

         * Command format: `sudo bash -c \"$(curl http://assist-client-{region-code}.tos-{region-code}.ivolces.com/install.sh)\"`

            <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="4">tip            </div>
            

            <div data-tips="true" data-tips-type="default" data-wrapper-indent="4">Please replace {region\-code} with the actual Region code you are accessing.            </div>
            

         * Example: In the Beijing Region, please execute the following command to install the Cloud assistant client.

            ```Plain Text
            sudo bash -c "$(curl http://assist-client-cn-beijing.tos-cn-beijing.ivolces.com/install.sh)"
            ```
            

      * Installation​ through internet

         If your ECS instance has been [associated with an EIP](https://docs.byteplus.com/en/docs/ecs/Assigning-or-releasing-a-private-IPv4-address), you can execute the following command on an instance in any region to install the cloud assistant Agent through the internet.

         ```Plain Text
         sudo bash -c "$(curl http://assist-client-cn-beijing.tos-cn-beijing.volces.com/install.sh)"
         ```
         

3. Confirm whether the installation is complete based on the guidance in [Viewing installation results](https://docs.byteplus.com/en/docs/ecs/Viewing-agent-installation-results).


</Tab>
</Tabs>


<span id=".5ZCO57ut5q2l6aqk"></span>
## Subsequent steps

Once the cloud assistant Agent is running normally, you can use the cloud assistant to perform O&M tasks. For details, refer to [Creating O&M tasks](https://docs.byteplus.com/en/docs/ecs/Creating-a-job).

<span id=".55u45YWz5paH5qGj"></span>
## Related documents


* [InstallCloudAssistant](https://docs.byteplus.com/en/docs/ecs/InstallCloudAssistant_-_Install_Cloud_assistant_Agent)

* [DescribeCloudAssistantStatus](https://docs.byteplus.com/en/docs/ecs/DescribeCloudAssistantStatus)
