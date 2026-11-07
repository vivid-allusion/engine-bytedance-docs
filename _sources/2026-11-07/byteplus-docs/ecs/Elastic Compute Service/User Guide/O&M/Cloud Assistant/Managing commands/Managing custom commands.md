---
title: "Managing custom commands"
product: "Elastic Compute Service"
product_code: "ecs"
source: "https://docs.byteplus.com/en/docs/ecs/Managing-Custom-Commands"
---

Custom commands are a feature of the cloud assistant designed to meet your personalized O&M requirements. When preset public commands can not meet your requirements, you can create custom commands. After this, you can run the custom commands you have written on multiple instances at the same time via O&M tasks.

<span id=".5rOo5oSP5LqL6aG5"></span>
## Usage notes


* In the same region, the maximum number of custom commands you can create is 500, and the content size of a custom command must not exceed 16 KB.

* You can configure custom commands to be used only by specific IAM users. For detailed operations, refer to [Configuring permissions for using custom commands](https://docs.byteplus.com/en/docs/ecs/Configuring_permissions_for_using_custom_commands).


<span id=".5Yib5bu66Ieq5a6a5LmJ5ZG95Luk"></span>
## Create custom commands

You can create custom commands as needed and use them to create O&M tasks.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">You can also create custom commands by using the public command cloning feature. For operation details, refer to<a href="https://docs.byteplus.com/en/docs/ecs/Managing-Custom-Commands#cloning-a-custom-command">Cloning into custom commands</a>.</div>


<span id=".5pON5L2c5q2l6aqk"></span>
### Procedure


1. Log in to the [ECS console](https://console.byteplus.com/ecs/instance). 

2. In the left\-side navigation pane, select "Maintenance & Monitoring \> Cloud Assistant" and then select the "Custom commands" tab. 

3. In the top menu bar, select the region where your business is located. 

4. Click the "Create a custom command" button and enter the command configuration information as needed. For parameter descriptions, refer to [Cloning into custom commands](https://docs.byteplus.com/en/docs/ecs/Managing-Custom-Commands#cloning-a-custom-command).

5. Click the "Confirm" button to create a custom command.


<span id=".5ZCO57ut5q2l6aqk"></span>
### Subsequent steps

After the command is created successfully, you are automatically redirected to the Custom commands page. Here, you can [create jobs](https://docs.byteplus.com/en/docs/ecs/Creating-a-job), [clone commands into custom commands](https://docs.byteplus.com/en/docs/ecs/Managing-Custom-Commands#cloning-a-custom-command), or perform other operations.

<span id=".55u45YWz5Yqf6IO9"></span>
### Related features


|Feature |Description |
|---|---|
|Edit custom commands |If an existing custom command cannot meet your O&M requirements, you can change its command content and other information. Specific steps are as follows:<br><br><br>1. In the "Action" column of the target command, click the "Edit" button.<br><br>2. Change the command configuration information as needed. For parameter descriptions, refer to [Cloning into custom commands](https://docs.byteplus.com/en/docs/ecs/Managing-Custom-Commands#cloning-a-custom-command).<br><br>3. Click the "Confirm" button to complete the operation. |
|Delete custom commands |You can delete custom commands that are no longer required. However, you can not restore deleted custom commands, so please proceed with caution. Steps to delete a custom command are as follows:<br><br><br>1. In the "Action" column of the target command, click the "Delete" button.<br><br>2. Click the "Confirm" button to complete the operation. |


<span id=".5p-l55yL5ZG95Luk6K-m5oOF"></span>
## View command information

Before using custom commands, you can view the command information, such as the execution path, execution user, and specific content. This allows you to confirm whether the target custom command meets your O&M requirements.


1. Log in to the [ECS console](https://console.byteplus.com/ecs/instance). 

2. In the left\-side navigation pane, select "Maintenance & Monitoring \> Cloud Assistant" and then select the "Custom commands" tab. 

3. In the top menu bar, select the region where your business is located. 

4. Select the target command to view, then click its name.

5. On the pop\-up command details page, you can view the basic information of the command (such as the command name, execution path, execution user, and timeout), the command content, and command parameters.

   > "Argument" information is displayed only when the command supports custom parameters.   
   

<span id=".5Yib5bu656uL5Y2z5omn6KGM5Lu75Yqh"></span>
## Create tasks to be executed immediately

To help you quickly perform O&M operations via custom commands, you can create O&M tasks directly on the Custom commands page. For detailed task configurations, refer to [Creating jobs](https://docs.byteplus.com/en/docs/ecs/Creating-a-job).

<span id=".5YWL6ZqG6Ieq5a6a5LmJ5ZG95Luk"></span>
## Clone custom commands

You can use the cloning feature to make personalized changes based on the target custom command, and then clone the command into a new custom command for use.


1. Log in to the [ECS console](https://console.byteplus.com/ecs/instance). 

2. In the left\-side navigation pane, select "Maintenance & Monitoring \> Cloud Assistant" and then select the "Custom commands" tab. 

3. In the top menu bar, select the region where your business is located. 

4. Select the target command to clone, and click the "Clone" button in the "Action" column on the right.

5. Change command configurations as needed. For parameter descriptions, refer to [Cloning into custom commands](https://docs.byteplus.com/en/docs/ecs/Managing-Custom-Commands#cloning-a-custom-command).

6. Click the "Confirm" button to clone.

7. After the command is cloned, you are automatically redirected to the Custom commands page. Here, you can use the cloned command to create O&M tasks or perform other operations.


<span id=".55u45YWz5paH5qGj"></span>
## Related documents


* [CreateCommand](https://docs.byteplus.com/en/docs/ecs/CreateCommand-Creating_a_custom_command)

* [ModifyCommand](https://docs.byteplus.com/en/docs/ecs/ModifyCommand_-_Modify_custom_command)

* [DescribeCommands](https://docs.byteplus.com/en/docs/ecs/DescribeCommands_-_Query_the_command_list)

* [DeleteCommand](https://docs.byteplus.com/en/docs/ecs/DeleteCommand_-_Deleting_a_custom_command)
