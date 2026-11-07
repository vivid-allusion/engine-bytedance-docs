---
title: "Managing public commands"
product: "Elastic Compute Service"
product_code: "ecs"
source: "https://docs.byteplus.com/en/docs/ecs/Managing-public-command"
---

Public commands are preset by the cloud assistant based on common O&M operations, such as "Change Linux instance password" and "Install Cloud Monitor Agent on Linux instance". You can use public commands to quickly create O&M tasks and complete common O&M operations.

<span id=".5rOo5oSP5LqL6aG5"></span>
## Considerations

You can not add, edit, or delete public commands.

<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure

<span id=".5p-l55yL5ZG95Luk6K-m5oOF"></span>
### View public command details

Before using public commands, you can view command information, such as the execution path, execution user, and specific content. This allows you to confirm whether the target public command meets your O&M requirements.


1. Log in to the [ECS console](https://console.byteplus.com/ecs/instance). 

2. In the left\-side navigation pane, select "Maintenance & Monitoring \> Cloud Assistant" and then select the "Public commands" tab. 

3. In the top menu bar, select the region where your business is located. 

4. Select the target command to view and then click the "View details" button.

5. On the pop\-up command details page, you can view the basic information of the command (such as the command name, execution path, execution user, and timeout period), the command content, and command parameters.

   > "Argument" information is displayed only when the command supports custom parameters.   
   

<span id=".5Yib5bu65L2c5Lia"></span>
### Create jobs

If there are public commands that meet your O&M requirements, you can directly and quickly create jobs and perform O&M operations on the Public commands page for execution. For detailed job configurations​, refer to [Creating jobs](https://docs.byteplus.com/en/docs/ecs/Creating-a-job).

<span id=".5YWL6ZqG5Yiw6Ieq5a6a5LmJ5ZG95Luk"></span>
### Clone public commands into custom commands

You can use the public command cloning feature to make personalized changes based on public commands. With this feature, you can clone public commands and use the cloned commands as custom commands.


1. Log in to the [ECS console](https://console.byteplus.com/ecs/instance). 

2. In the left\-side navigation pane, select "Maintenance & Monitoring \> Cloud Assistant" and then select the "Public commands" tab. 

3. In the top menu bar, select the region where your business is located. 

4. Select the target command to clone and click the "Clone" button.

5. Change the information of the following configurations as needed.

   
   |Parameter​ |Description |Sample value |
   |---|---|---|
   |**Basic information** |||
   |Command name |Set the command name. |Change login password |
   |Command source |Select the command type. For the current version, `Linux Shell`, `Python`, `Windows PowerShell`, and `Windows Bat` can be selected. |Linux Shell |
   |Command contents |Write the specific command content based on the requirements.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">The size of the command content must not exceed 16 KB.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">You can set custom parameters in the command content for dynamic parameter passing. For details, refer to <a href="https://docs.byteplus.com/en/docs/ecs/Custom-argument-description">Custom parameter descriptions</a>.</div><br> |\- |
   |Use argument |You can use custom parameters in the command based on your requirements. After you enable this option, custom parameters in the command content are displayed automatically. For more details on custom parameters, refer to [Custom parameter descriptions](https://docs.byteplus.com/en/docs/ecs/Custom-argument-description). |\- |
   |**Execute configuration** |||
   |Execution path |Enters the command execution path.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">The default command execution path in Linux operating systems is <code>/home</code>.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">The default command execution path in Windows operating systems is <code>C:/Windows/System32</code>.</div><br> |/root |
   |Default executing user |You can specify an existing user in the target instance to execute commands. We recommend that you avoid using the Root or System user to reduce security risks. |user1 |
   |Login password |Enter the login password for the execution user.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">When the command type is <code>Windows PowerShell</code> or <code>Windows Bat</code>, and the execution user is not "system", you are required to enter the login password.</div><br> | |
   |Timeout |Sets the timeout period for command execution on each instance. If the command execution times out, the cloud assistant will mark the task as failed on the corresponding instance.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">The default timeout period varies by commands, and you can manually adjust it within the range of 30 seconds to 24:00:00.</div><br> |\- |
   |**Advanced configuration** |||
   |Project |Project: You can add the cloud assistant to the project and manage it by project dimension, which helps maintain resource independence and ensure data security. For more project details, refer to [Project management](https://docs.byteplus.com/en/docs/ecs/Managing-projects). |default |
   |Tag |A tag is a key\-value pair used to identify cloud resources. Tags help you categorize resources based on different dimensions, such as purpose, owner, or environment. This allows you to search and aggregate your resources. For more information about tags, refer to [Tags](https://docs.byteplus.com/en/docs/ecs/Tag-overview). |Key1:Value1 |
   

6. Click the "Confirm" button to clone.

7. After the command is cloned, you are automatically redirected to the Custom commands page. Here, you can create jobs, clone commands, and perform other operations. For details, refer to [Custom commands](https://docs.byteplus.com/en/docs/ecs/Managing-Custom-Commands).


<span id=".5YWs5YWx5ZG95Luk5rGH5oC7"></span>
## Public command overview

The following table shows public commands currently available and brief usage instructions.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">If preset public commands can not meet your O&M requirements, you can create custom commands. For details, refer to <a href="https://docs.byteplus.com/en/docs/ecs/Managing-Custom-Commands#creating-a-custom-command">Creating custom commands</a>.</div>



|Command name |Type |Parameter description |Description |
|---|---|---|---|
|Update software source key |Linux Shell |\- |Used to update Mirror source key information. For more details, see [How to fix expired software repository keys?](https://docs.byteplus.com/en/docs/ecs/How_to_fix_expired_software_repository_keys#8Sh7bBjG). |
|Install Cloud Monitor Agent on Linux instance |Shell |\- |This command is used to install Cloud Monitor plugins on Linux instances. For more details about Cloud Monitor, refer to [What is Cloud Monitor](https://docs.byteplus.com/en/docs/cloudmonitor/What-is-Vitality-Cloud-Monitor). |
|Change Linux instance password |Shell |* username: Required. The username.<br><br>* password: Required. The login password.<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">You can only change login passwords corresponding to existing usernames for instances.</div><br> |This command is used to change login usernames and passwords of Linux instances. |
|Add SSH public key to Linux instance |Shell |ssh_public_key: Required. The public key of the SSH key pair. |This command is used to add a public key from a key pair to a Linux instance for the SSH login. |
|Replace SSH public key for Linux instance |Shell |* username: Required. The username. The default value is `root`.<br><br>* ssh_public_key: Required. The public key of the SSH key pair. |This command is used to replace the public key from a key pair for a Linux instance for the SSH login. |
|Script to diagnose and troubleshoot RDMA failure |Python |\- |This command is used to troubleshoot RDMA failures on HPC GPU\-optimized instances.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">Only HPC\-optimized instances support this feature. For purchase details, refer to <a href="https://docs.byteplus.com/en/docs/gpu/Buying-High-Performance-Computing-Optimized-instances">Purchasing HPC\-optimized instances</a>.</div><br> |
|Collect Linux instance status |Shell |\- |This command is used to collect status information of a Linux instance, including OS version, network information, memory usage, GPU usage, cloud\-init information, and SOS information. Finally, the command generates the status information as a compressed package in the `/tmp` directory for easy analysis afterwards. |
|Change Windows instance password |PowerShell |* username: Required. The username.<br><br>* password: Required. The login password.<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">You can only change login passwords corresponding to existing usernames for instances.</div><br> |This command is used to change login usernames and passwords of Windows instances. |
|Reset password online |Shell |* Key_Pair_ID: Required. The key pair ID.<br><br>* Encrypted_PassWord: Required. The encrypted password.<br><br>* User_Name: Required. The username.<br><br>* Open_Passwd_Auth: Optional. Indicates whether to enable password authentication for SSH login.<br><br>   * Yes (**default**): Indicates that password authentication is enabled for SSH login.<br><br>   * No: Indicates that password authentication is disabled for SSH login. |This command is used to reset Linux instance passwords online. |
