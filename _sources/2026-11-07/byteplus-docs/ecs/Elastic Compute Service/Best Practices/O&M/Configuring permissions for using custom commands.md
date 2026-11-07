---
title: "Configuring permissions for using custom commands"
product: "Elastic Compute Service"
product_code: "ecs"
source: "https://docs.byteplus.com/en/docs/ecs/Configuring_permissions_for_using_custom_commands"
---

This topic describes how to grant limited permissions to IAM users for using custom commands via the IAM (Identity and Access Management) feature.

<span id=".5pON5L2c5Zy65pmv"></span>
## Applicable scenario

Custom commands created via cloud assistant​ may include operations that require high permissions, such as formatting disks, deleting files, and modifying system parameters. With IAM custom policies, you can restrict IAM user access to specified custom commands and control the scope of command execution.

<span id=".5pON5L2c5rWB56iL"></span>
## Operation processes

<span id=".5q2l6aqk5LiA77ya5Yib5bu66Ieq5a6a5LmJ562W55Wl"></span>
### Step 1: Create a custom policy


1. Log in to the IAM [Policy Management](https://console.byteplus.com/iam/policymanage?scope=All) console as the root user.

2. Select the custom policy tab to enter the custom policy list page.

3. Click the "Create custom policy" button and configure the parameters described in the following table.

   > This practice only explains the configuration content of custom command usage permissions. For more details on custom policies, you can view the [Policy Overview](https://docs.byteplus.com/en/docs/byteplus-platform/docs-managing-policies).   
   

   
   |Parameter |Description |Sample value |
   |---|---|---|
   |Policy name |Specify the name of the new policy. |DeleteVirtio |
   |Edit policy content |Configure the policy based on the following rules:<br><br><br>* Effect: Must be set to `Allow`. "Allow" indicates that operations on the custom commands specified in this policy are permitted.<br><br>* Action: Specify the actions to be performed on custom commands. `ecs:InvokeCommand` is required.<br><br>   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div><br>   <br><br>   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">Since policies can not restrict IAM users from calling the RunCommand interface to execute custom commands, do not add this interface.   </div><br>   <br><br>* Resource: Specify the custom commands for which permission usage needs to be restricted. The format is `trn:ecs:[command region]:[root user ID]:command/[custom command ID]`.<br><br><br>Complete example:<br><br>The following policy grants permissions to query, modify, and use the custom commands `cmd-ycn5dc9qf9l8j0v*****` and `cmd-tsx0gy9rslp90k3z*****` via cloud assistant in China (Beijing).<br><br>```Plain Text```<br>```{```<br>``` "Statement": [```<br>```   {```<br>```       "Effect": "Allow",```<br>```       "Action": [```<br>```           "ecs:Describe*",```<br>```           "ecs:ModifyCommand",```<br>```           "ecs:InvokeCommand"```<br>```       ],```<br>```       "Resource": [```<br>```           "trn:ecs:cn-beijing:210001*****:command/cmd-ycn5dc9qf9l8j0v*****",```<br>```           "trn:ecs:cn-beijing:210001*****:command/cmd-tsx0gy9rslp90k3z*****"```<br>```       ]```<br>```   }```<br>``` ]```<br>```}```<br> |\- |
   

4. Click the "Create policy" button to complete creation.

5. After the policy is created, if an IAM user without permission tries to use the custom commands covered by the policy, the message "The specified resource is not allowed to operate." is prompted on the job creation page.


<span id=".5q2l6aqk5LqM77ya5Li65a2Q6LSm5Y-35re75Yqg5p2D6ZmQ"></span>
### Step 2: Grant permission for an IAM user


1. Log in to the IAM [Policy Management](https://console.byteplus.com/iam/policymanage?scope=All) console as the root user.

2. Select the custom policy tab to enter the custom policy list page.

3. On the custom policy tab, find the policy you created, and click the "Manage" button in the "Action" column to the right of the target policy.

4. On the policy details page, select the "Authorization" tab and then choose "Global Authorization".

5. Click the "Add Authorization" button, select "User", and select the IAM user who can execute the policy\-specified custom commands.

6. Click the "Confirm" button to add permission.

7. After the permission is added, the IAM user can use the corresponding custom command via cloud assistant. For operation details, see [Creating jobs](https://docs.byteplus.com/en/docs/ecs/Creating-a-job).
