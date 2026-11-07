---
title: "Batch sending remote commands"
product: "Elastic Compute Service"
product_code: "ecs"
source: "https://docs.byteplus.com/en/docs/ecs/Batch_send_remote_commands"
---

If you want to quickly complete routine maintenance for multiple instances (for example, batch view ECS instance information, install or uninstall software, reset user password, and automate operation and maintenance scripts), you can use the remote command sending feature in the ECS console. This topic introduces how to send commands to one or more instances on the Instances page.

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">This feature relies on the cloud assistant Agent and orchestration. You can also send and execute commands directly on the operation and maintenance orchestration page. For details, refer to <a href="https://docs.byteplus.com/en/docs/ecs/Creating_a_batch_actions_instance_task">Creating batch instance tasks</a>.</div>


<span id="5wQ02p9r"></span>
## Prerequisites


* When using the Orchestration service for the first time, you need to create the CustomRoleForOOS role to complete the authorization. [Learn more](https://docs.byteplus.com/en/docs/ecs/Preparation).

* When batch sending commands, you need to ensure that the selected instances meet the following conditions:

   * All instances must be Linux or Windows instances.

   * All instances must be in the **Running** state.

   * The cloud assistant Agent has been installed on all instances, and its state is **Running**.


<span id="qnLZkLrd"></span>
## Procedure


1. Log in to the [ECS console](https://console.byteplus.com/ecs/instance).

2. In the left\-side navigation pane, select "Instances & Images \> Instances".

3. In the top menu bar, select the project and region to which the target instance belongs.

4. On the Instances page, select one or more instances and click the "··· \> Send command" button at the bottom of the list.

5. The system pops up a "In bulk send command" window. Here, you can view operable instances, inoperable instances, and the reasons.

   > If there are inoperable instances, this indicates that some instances do not meet the conditions required to perform this action. You can address the issue based on prompts and try again once the conditions are met.   
   

6. Click the "Continue" button to go to the operation orchestration page and configure related parameters. For specific configurations, please refer to [Creating batch instance tasks - Send commands](https://docs.byteplus.com/en/docs/ecs/Creating_a_batch_actions_instance_task).


<span id="uNdG1jot"></span>
## Related documents


* [Installing the cloud assistant Agent](https://docs.byteplus.com/en/docs/ecs/Install-the-Cloud-Assistant-client)

* [Managing commands](https://docs.byteplus.com/en/docs/ecs/Managing-commands)

* [Orchestration overview](https://docs.byteplus.com/en/docs/ecs/Overview_of_Process_Orchestration)
