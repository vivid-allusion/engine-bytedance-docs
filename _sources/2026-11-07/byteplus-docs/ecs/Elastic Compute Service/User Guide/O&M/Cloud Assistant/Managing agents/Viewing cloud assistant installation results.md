---
title: "Viewing cloud assistant installation results"
product: "Elastic Compute Service"
product_code: "ecs"
source: "https://docs.byteplus.com/en/docs/ecs/Viewing-agent-installation-results"
---

To view cloud assistant installation results, you can log in to the Cloud Assistant console, or the target instance.

<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisite

You have [installed the cloud assistant Agent](https://docs.byteplus.com/en/docs/ecs/Install-the-Cloud-Assistant-client).

<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure

<span id=".6YCa6L-H5om56YeP5L2c5Lia5o6n5Yi25Y-w5p-l55yL"></span>
### View cloud assistant installation results in the Cloud Assistant console

On the Agent management tab, you can view the installation and running status​, and version of the cloud assistant Agent for instances.


1. Log in to the [ECS console](https://console.byteplus.com/ecs/instance). 

2. In the left\-side navigation pane, select "Maintenance & Monitoring \> Cloud Assistant" and then select the "Agent management" tab. 

3. In the top menu bar, select the region where your business is located. 

4. After searching for and locating the target instance, you can check the running status of the cloud assistant Agent in the "Agent status" column. Supported statuses are listed below:

   
   |Status |Description |Executable operation |
   |---|---|---|
   |Uninstalled |Indicates that the target instance does not have the cloud assistant Agent installed. |Install |
   |Initialization |Indicates that the cloud assistant Agent is being initialized. |\- |
   |Awaiting restart |Indicates that you have installed the cloud assistant Agent but have not restarted the instance. |Restart |
   |Instance restarting |Indicates that the target instance is being restarted. |\- |
   |Installation failed |Indicates that the cloud assistant Agent fails to be installed and to run. |Install |
   |In service |Indicates that the target instance has the cloud assistant Agent installed and the cloud assistant Agent runs normally. |Upgrade, Uninstall |
   |Uninstalling |Indicates that the cloud assistant Agent is being uninstalled in the target instance. |\- |
   |Upgrading |Indicates that the version of the cloud assistant Agent is being upgraded. |\- |
   |Error |Indicates that the cloud assistant Agent has an exception. |Restart |
   |To start |Indicates that the instance with the cloud assistant Agent installed is in the **Stopped** state. |Start |
   


<span id=".55m75b2V5a6e5L6L5p-l55yL"></span>
### View cloud assistant installation results by logging in to instances


<Tabs>
<Tab zoneid="JAqWkfTsi8" title="">
<TabTitle></TabTitle>

View installation results for Linux instances

View installation results for Linux instances




</Tab>
</Tabs>



<Tabs>
<Tab zoneid="rTX20ULAVs" title="View installation results for Linux instances">
<TabTitle>View installation results for Linux instances</TabTitle>

1. Log in to the Linux instance. For more information, refer to [Logging in to Linux instances](https://docs.byteplus.com/en/docs/ecs/Using-the-console-to-log-on-to-a-Linux-instance).

2. Execute the following command to view the running status of the cloud assistant Agent.

   ```JSON
   systemctl status assist-client.service
   ```
   

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_05b6fe76db992bfa0e04268fad2c334a.png) </span>

3. You can also execute the following command to view the log of the cloud assistant Agent. If heartbeat messages are sent normally, this also indicates a successful installation.

   ```Apex
   tail -f  /var/log/assist_client/assist-client.log
   ```
   

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_8e7af2a449c6d718c78e2f7796b70b65.png) </span>


</Tab>
<Tab zoneid="avgcxASM2a" title="View installation results for Windows instances">
<TabTitle>View installation results for Windows instances</TabTitle>

1. Log in to the Windows instance. For more information, refer to[ Logging in to Windows instances](https://docs.byteplus.com/en/docs/ecs/Logging-on-to-a-Windows-instance).

2. Execute the following command in Command Prompt to view the running status of the cloud assistant Agent.

   ```Plain Text
   tasklist /fi "imagename eq assist-client.exe"
   ```
   

3. You can also execute the following command to view the log of the cloud assistant Agent. If heartbeat messages are sent normally, this also indicates a successful installation.

   ```Plain Text
   C:\ProgramData\AssistClient\assist-client.log
   ```
   

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_96d3a28875fe78ca86ec9e7d3f1367dd.png) </span>


</Tab>
<Tab zoneid="BiRzL3N72Q" title="">
<TabTitle></TabTitle>

1. Log in to the Linux instance. For more information, refer to [Logging in to Linux instances](https://docs.byteplus.com/en/docs/ecs/Using-the-console-to-log-on-to-a-Linux-instance).

2. Execute the following command to view the running status of the cloud assistant Agent.


```Plain Text
systemctl status assist-client.service
```


<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_05b6fe76db992bfa0e04268fad2c334a.png) </span>


3. You can also execute the following command to view the log of the cloud assistant Agent. If heartbeat messages are sent normally, this also indicates a successful installation.


```Plain Text
tail -f  /var/log/assist_client/assist-client.log
```


<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_8e7af2a449c6d718c78e2f7796b70b65.png) </span>

View installation results for Windows instances


</Tab>
</Tabs>


<span id=".55u45YWz5paH5qGj"></span>
## Related documents

[DescribeCloudAssistantStatus - Queries cloud assistant Agent statuses](https://docs.byteplus.com/en/docs/ecs/DescribeCloudAssistantStatus)
