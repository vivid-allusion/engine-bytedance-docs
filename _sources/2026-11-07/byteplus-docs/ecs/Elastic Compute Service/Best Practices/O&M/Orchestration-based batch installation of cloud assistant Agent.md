---
title: "Orchestration-based batch installation of cloud assistant Agent"
product: "Elastic Compute Service"
product_code: "ecs"
source: "https://docs.byteplus.com/en/docs/ecs/Orchestration-based_batch_installation_of_cloud_assistant_Agent"
---

This topic describes how to batch install cloud assistant Agent on ECS instances associated with the same [tag](https://docs.byteplus.com/en/docs/ecs/Tag-overview).

<span id="qdl4Y2Ov"></span>
## Scenarios

If you need to install cloud assistant Agent on a large number of newly purchased ECS instances, you can use the batch installation feature. Specifically, you can filter target instances by tags first and then install cloud assistant Agent on them via script execution as specified in a custom template\-based orchestration plan. This helps improve maintenance efficiency and reduce manual effort.

<span id="5HrFCmjC"></span>
## Prerequisites


* You have [purchased instances](https://docs.byteplus.com/en/docs/ecs/Overview-of-methods-for-buying-ECS-instances?lang=zh)[ tag](https://docs.byteplus.com/en/docs/ecs/Tag-overview?lang=zh#.5Yib5bu65bm257uR5a6a5qCH562-)[ tag](https://docs.byteplus.com/en/docs/ecs/Tag-overview?lang=zh#.5Yib5bu65bm257uR5a6a5qCH562-).

   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">The total number of instances on which cloud assistant Agent will be installed in a batch cannot exceed 1,000. If the total number of instances exceeds this limit, associate multiple tags with the target instances and perform installation in separate batches.   </div>
   

* You have not installed cloud assistant Agent on the target instances.


<span id="pIhP3z9q"></span>
## Limits

Currently, only Linux instances support orchestration\-based batch installation of cloud assistant Agent **. ** For Windows instances, install cloud assistant Agent manually via script execution. [Learn more](https://docs.byteplus.com/en/docs/ecs/Install-the-Cloud-Assistant-client?lang=zh).

<span id="JTJvewsn"></span>
## Usage notes

Ensure that the selected tag is associated only with instances that do not have the cloud assistant Agent installed. Alternatively, configure a rule to filter instances without the cloud assistant Agent installed when you create a custom template in Step 1. Otherwise, the cloud assistant Agent will be reinstalled on instances where it is already installed.

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="default">No further attention is required if reinstalling cloud assistant Agent and restarting instances has no impact on your business.</div>


* <div data-tips="true" data-tips-type="default">Installing the cloud assistant Agent requires restarting the instances, which may affect your business. Perform this operation during an appropriate maintenance window.</div>



<span id="jfDX1I73"></span>
## Procedure

<span id="9zqlOnFS"></span>
### Step 1: Create a custom template

Create a template for installing cloud assistant Agent. This enables you to preset a standardized orchestration process for batch installation.


1. Log in to the [ECS console](https://console.byteplus.com/ecs/instance).

2. In the left\-side navigation pane, click "Maintenance & Monitoring \> Orchestration".

3. In the top menu bar, select the project and the region where your business is located. In this practice, China (Beijing) and the default project are used as examples.

4. On the CloudOps Orchestration page, click the "Custom template" tab.

5. Click the "Create custom templates" button and configure the parameters in the following table.

   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">The following only describes parameters related to this practice. For complete parameter descriptions and more details, refer to <a href="https://docs.byteplus.com/en/docs/ecs/Creating_custom_templates?lang=zh">Creating custom templates</a>.   </div>
   

   
   |Parameter​ |Description |Sample value |
   |---|---|---|
   |Name |Specify the name of the custom template.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">The template name must be unique within the current account or project. It cannot be the same as the name of the <a href="https://docs.byteplus.com/en/docs/ecs/Summary_of_orchestration_steps">public template</a>, nor can it be the same as the name of any other custom template.</div><br> |Cloud assistant Agent batch installation template |
   |JSON schema |Define the "Cloud assistant Agent batch installation template" file (orchestration process) in JSON format. For example:<br><br>```JSON```<br>```{```<br>```    "Parameters": {```<br>```        "targets": {```<br>```            "Type": "Map"```<br>```        },```<br>```        "NeedReboot": {```<br>```            "Type": "Boolean"```<br>```        },```<br>```        "ForceStop": {```<br>```            "Type": "Boolean"```<br>```        }```<br>```    },```<br>```    "Tasks": [```<br>```        {```<br>```            "Name": "getInstances",```<br>```            "Action": "VOS::SelectTargetInstances",```<br>```            "Parameters": {```<br>```                "Filters": "{{ .targets }}"```<br>```            },```<br>```            "Outputs": {```<br>```                "instanceIds": {```<br>```                    "Type": "List",```<br>```                    "Value": "{{ [.Instances[].InstanceId] }}"```<br>```                }```<br>```            }```<br>```        },```<br>```        {```<br>```            "Name": "InstallCloudAssistant",```<br>```            "Action": "VOS::ECS::InstallCloudAssistant",```<br>```            "Parameters": {```<br>```                "InstanceId": "{{ VOS::LoopItem }}",```<br>```                "NeedReboot": "{{ .NeedReboot }}",```<br>```                "ForceStop": "{{ .ForceStop }}"```<br>```            },```<br>```            "Outputs": {```<br>```                "InstallResult": {```<br>```                    "Type": "Boolean",```<br>```                    "Value": "{{ .InstallResult }}"```<br>```                }```<br>```            },```<br>```            "Loop": {```<br>```                "LoopItem": "{{ .\"getInstances.instanceIds\" }}",```<br>```                "Outputs": {```<br>```                    "LoopInstanceStatus": {```<br>```                        "SelectedOutputFiled": "InstallResult"```<br>```                    }```<br>```                }```<br>```            }```<br>```        }```<br>```    ],```<br>```    "Outputs": {```<br>```        "InstanceStatus": {```<br>```            "Type": "List",```<br>```            "Value": "{{ .\"InstallCloudAssistant.LoopInstanceStatus\" }}"```<br>```        }```<br>```    }```<br>```}```<br><br><br> |\- |
   |Project |Specify the project to which the custom template belongs.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">The project displayed in the configuration item is the one you select in step 3. To change projects, follow the instructions in step 3.</div><br> |Default configuration |
   

6. Click "Confirm" to complete the custom template creation.

   At this point, a custom template named "Cloud assistant Agent batch installation template" is displayed on the custom templates list page.


<span id="aJIQEpVq"></span>
### Step 2: Create an orchestration plan

Create an orchestration plan in the "Execute immediately" mode to batch install the cloud assistant Agent.


1. Log in to the [ECS console](https://console.byteplus.com/ecs/instance).

2. In the left\-side navigation pane, click "Maintenance & Monitoring \> Orchestration".

3. In the top menu bar, select the region where your business is located. In this practice, China (Beijing) and the default project are used as examples.

   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">The following only describes parameters related to this practice. For complete parameter descriptions and more details, refer to <a href="https://docs.byteplus.com/en/docs/ecs/Create_an_orchestration_plan?lang=zh">Creating orchestration plans</a>.   </div>
   

   
   |Parameter​ |Description |Sample value |
   |---|---|---|
   |**Basic information** |||
   |Name |Specify the name of the orchestration plan. |Cloud assistant Agent batch installation O&M plan |
   |Role |Select a role with read and write permissions on your ECS resources. The default role is "CustomRoleForOOS," which integrates all permissions supported by Orchestration by default. This prevents permission issues during usage. |Default configuration |
   |**Execution mode** |||
   |Execution mode |Select a mode of executing the orchestration plan task. In this practice, "Execute immediately" is selected.<br><br>> Execute immediately: After the orchestration plan task is created, execute it immediately. |Execute immediately |
   |**Task steps** |||
   |Step creation type |Select a mode of executing the task steps of the orchestration plan. In this practice, "Select an existing template" is selected. |Select an existing template |
   |**Select template** |||
   |\- |Select the orchestration plan template for task execution. Click the dropdown list for template selection and select the template "Cloud assistant Agent batch installation template" you have created in step 1. |Cloud assistant Agent batch installation template |
   |**Parameter configuration**<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">The parameters vary depending on the selected template. The parameters displayed in the console prevail. The following only describes parameters related to this practice.</div><br> |||
   |targets (Map) |Enter the value of `{key}` in JSON format as follows:<br><br>```JSON```<br>```{```<br>```        "Type": "Tags",```<br>```        "Tags": [```<br>```            {```<br>```                "Key": "purpose",```<br>```                "Value": "Agent"```<br>```            }```<br>```        ]```<br>```    }```<br><br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="default">Replace <code>purpose </code>and <code>Agent </code>with the actual key (Key) and value (Value) associated with your instances. The specified tag key and value must match those of the instances where cloud assistant Agent is to be installed.</div><br><br><br>* <div data-tips="true" data-tips-type="default">Configure the parameter "targets (Map)" based on the template you select.</div><br> |\-<br><br> |
   |NeedReboot (Boolean) |Select whether to restart the corresponding instances after cloud assistant Agent installation is complete.<br><br><br>* Enable: Instance restart required.<br><br>* Disable (default): Instance restart not required.<br><br>   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div><br>   <br><br>   <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">If you have not enabled the automatic instance restart feature, manually restart the corresponding instances after installing cloud assistant Agent to ensure the installation succeeds.   </div><br>    |Enable |
   |ForceStop (Boolean) |Select whether to forcibly terminate related processes, dependent services, and other running entities during O&M operations.<br><br><br>* Enable: Force termination of all related processes.<br><br>* Disable (default): No force termination of related processes. |Default configuration |
   

4. Click "Create" to complete the operation.

   At this point, an orchestration plan named "Cloud assistant Agent batch installation O&M plan" is displayed on the orchestration plans list page.


<span id="xxXecvw7"></span>
### Step 3: View the Agent installation result

For installation results of the target instances, log in to the cloud assistant console or the target instances. [Learn more](https://docs.byteplus.com/en/docs/ecs/Viewing-agent-installation-results?lang=zh).
