---
title: "DolphinScheduler supports Volcano Voice alerts"
product: "BytePlus EMR"
product_code: "E-MapReduce"
source: "https://docs.byteplus.com/en/docs/E-MapReduce/DolphinScheduler_supports_Volcano_Voice_alerts"
---

<span id="497dd4f0"></span>
## Prerequisites


* The Volcano Voice service has been enabled. For detailed instructions, see [Voice Service](https://www.volcengine.com/docs/6358/66622).

* The DolphinScheduler component has been installed in the EMR cluster. For detailed instructions, see DolphinScheduler component.

* The EMR cluster has been bound to a public IP. For detailed instructions, see [Public Access](https://www.volcengine.com/docs/6396/67793).


<span id="d0531f00"></span>
## Environment configuration

<span id="37bef4ce"></span>
### Configure Alert\-Server


1. Log in to the ECS node where Alert\-Server is located. Navigation path: **on ECS Console \> Cluster Name \> Service List \> DolphinScheduler \> Alert\-Server**.

2. Place the following files in the Alert\-Server libs directory. The default libs path is `/usr/lib/emr/current/dolphin_scheduler/alert-server/libs`.


<Attachment link="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/3fb242ef8d9c4f0c92c4445e1849d595~tplv-goo7wpa0wc-image.image" name="dolphinscheduler-alert-volcanovoice-3.1.9.jar">dolphinscheduler-alert-volcanovoice-3.1.9.jar</Attachment>


&nbsp;

<span id="09a2966b"></span>
### Configure Api\-Server


1. Log in to the ECS node where Api\-Server is located. Navigation path: **on ECS Console \> Cluster Name \> Service List \> DolphinScheduler \> Api\-Server**.

2. Download the following UI files and replace the original UI files in the Api\-Server runtime directory. The default runtime directory is `/usr/lib/emr/current/dolphin_scheduler/api-server`.


<Attachment link="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/c894ebb8534547599461ea7df180aa3e~tplv-goo7wpa0wc-image.image" name="dolphin-ui.tar.gz">dolphin-ui.tar.gz</Attachment>


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Please back up the original UI file before proceeding with the replacement.</div>



3. Configure DolphinScheduler permissions.


```Bash
chown -R dolphinscheduler:dolphinscheduler ui
```


<span id="9ea587f7"></span>
## Service restart


1. After environment configuration is complete, you must restart Api\-Server and Alert\-Server.

2. After the restart, check the logs of Alert\-Server to verify whether the volcano\-voice plugin is registered correctly.


<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/49ef9ebd7c774d94a0dc5294c42f8274~tplv-goo7wpa0wc-image.image" width="3420px" /></div>


<span id="98c71fe7"></span>
## Using voice alerts

<span id="ba60a0ef"></span>
### Create an alert instance

Log in to DolphinScheduler, select **Security Center \> Alert Instance Management \> Create Alert Instance**, choose the VolcanoVoice plugin in the alert instance configuration, and fill in the relevant parameters.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">You can view the voice resource ID, voice resource type, and call number pool in <a href="https://console.volcengine.com/cloud_vms/number-pool">Volcano Voice Service</a>.</div>


* <div data-tips="true" data-tips-type="tip">The domain name for Volcano VMS is cloud\-vms.volcengineapi.com.</div>


* <div data-tips="true" data-tips-type="tip">Fill in the region according to your actual situation. For example, users in North China 2 (Beijing) should enter: cn\-beijing.</div>



&nbsp;

<span id="5e3372a7"></span>
#### TTS template

Currently, TTS alert templates are supported. The following variables are available in the template:


|Variable name |Meaning |
|---|---|
|projectName |The project to which the workflow belongs |
|owner |Workflow owner |
|processName |Workflow instance name |


**It is recommended to configure the alert template in the voice service as follows:** 

```Bash
尊敬的客户您好，您项目An alert has occurred in the workflow #processName# under #projectName#. The workflow owner is #owner#. Please check.
```


<span id="e88f33d4"></span>
#### **Advanced configuration**

In DolphinScheduler 3.1.x, the owner in alert information can only display the owner of the project to which the alert workflow belongs. In many cases, it is preferable to show the actual creator of the workflow. You can proceed as follows:


1. Go to the Master\-Server libs directory. The default libs path for the cluster is `/usr/lib/emr/current/dolphin_scheduler/master-server/libs`.

2. Replace the original dolphinscheduler\-service\-3.1.9.jar with the following JAR file.


<Attachment link="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/417fe1557ae7442dbd9b83a52104b31e~tplv-goo7wpa0wc-image.image" name="dolphinscheduler-service-3.1.9.jar">dolphinscheduler-service-3.1.9.jar</Attachment>



3. Restart the master\-server service.


<span id="f1d83bc7"></span>
### Create an alert group

Create an alert group and add the alert instances you have already created.

<span id="2b1265da"></span>
### Add alerts to jobs


1. Configure before starting the workflow.

   1. Notification policy: decide whether to send on success, failure, or both

   2. Select the alert group to determine which alert instances will receive notifications

2. After configuration is complete, start the workflow and check whether you receive a voice alert after execution is finished.


<span id="71d99170"></span>
## FAQs

Q: When an alert event occurs, no voice alert is received.

A: Please check the following configuration items.


1. Check the alter\-server logs to confirm whether the alert plugin is loaded properly or if there are any errors related to alert delivery failures.

2. Verify that the workflow is configured with an alert group, that the alert group includes a Volcano Voice alert instance, and check the notification policy.

3. Go to the **Voice Service \> Voice Records \> Data Statistics** page to check whether calls are exceeding frequency limits. If you find that calls are exceeding frequency limits, contact Volcano Voice Service for assistance.
