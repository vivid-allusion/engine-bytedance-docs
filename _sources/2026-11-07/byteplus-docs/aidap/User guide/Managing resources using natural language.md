---
title: "Managing resources using natural language"
product: "AI Native BaaS for Supabase"
product_code: "aidap"
source: "https://docs.byteplus.com/en/docs/aidap/Managing_resources_with_natural_language"
---

The AI Native Database Platform provides a friendly and powerful intelligent assistant. You can manage all AI Native Database Platform resources by conversing with the assistant in natural language.

<span id="CVcIvQJf"></span>
## Function list

Resource management operations fall into three categories: create, modify, and query. For create and modify operations, the intelligent assistant pops up a form in the dialog. After confirming or modifying the information in the form, click Execute to start the operation.

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">The intelligent assistant automatically uses the resources displayed on the current page as the operation target. If the resources displayed on the current page are not the operation target, specify the target resource by resource ID or resource name in the conversation.</div>


The following table shows the resource management operations supported by the intelligent assistant. The variables in the operation examples are explained as follows:


* `WorkspaceName` is the name of the workspace.

* `WorkspaceId` is the ID of the workspace.

* `BranchName` is the branch name.

* `BranchId` is the branch ID.

* `ComputeName` of the compute name.

* `ComputeId` is the compute ID.

* `AccountName` of the account name.

* `DatabaseName `is the name of the database.



|**Category** |**Feature** |**Supported or not** |**Intelligent assistant operation example** |
|---|---|---|---|
|Workspace management |Creating a workspace<br><br> |Support<br><br> |In the intelligent assistant dialog box, enter “Create a workspace”, then confirm the information or make necessary modifications in the form before clicking ** Execute**. |
||View the workspace list |Support |In the intelligent assistant dialog box, enter "View workspace list", then confirm information or make necessary changes in the form before clicking **Execute**. |
||Viewing Workspace details |Support |In the intelligent assistant dialog box, enter "Show details of [WorkspaceName\|WorkspaceId]".<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">Specify the workspace to modify using either <code>WorkspaceName</code> or <code>WorkspaceId</code>.</div><br> |
||Modify workspace configuration<br><br> |Support |In the intelligent assistant dialog box, enter "configure [WorkspaceName\|WorkspaceId]," then confirm the information or make necessary modifications in the form before clicking **Execute**.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">Specify the workspace to modify by either <code>WorkspaceName</code> or <code>WorkspaceId</code>.</div><br> |
||Deleting a workspace |Not support |Not involved |
|Branch management |Create a branch |Support |In the intelligent assistant dialog box, enter "Create a branch", then confirm the information or make necessary modifications in the form before clicking **Execute**. |
||Create a child branch |Support |In the intelligent assistant dialog box, enter "Create a child branch", then confirm the information or make necessary modifications in the form before clicking **Execute**. |
||Viewing branch details |Support |In the intelligent assistant dialog box, enter “Show details of [BranchName\|BranchId].”<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">You can specify the branch to modify by either <code>BranchName</code> or <code>BranchId</code>.</div><br> |
||Rename a branch |Support |In the intelligent assistant dialog box, enter “Rename [BranchName\|BranchId] to [BranchName_New]”, then confirm or modify the information in the form before clicking **Execute**.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">You can specify the branch to modify by either <code>BranchName</code> or <code>BranchId</code>. <code>BranchName_New</code> is the new branch name.</div><br> |
||Enable branch protection |Support |In the intelligent assistant dialog box, enter "Enable branch protection for branch [BranchName\|BranchId]", then confirm or modify the information in the form before clicking **Execute**.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">You can specify the branch to modify by either <code>BranchName</code> or <code>BranchId</code>.</div><br> |
||Reset branch |Not support |Not involved |
||Set as default branch |Support |In the intelligent assistant's dialog box, enter “Set branch [BranchName\|BranchId] as default branch,” then confirm or modify the information in the form before clicking **Execute**.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">You can specify the branch to modify by either <code>BranchName</code> or <code>BranchId</code>.</div><br> |
||Delete a branch |Not support |Not involved |
||Data recovery |Not support |Not involved |
|Compute management |Create compute |Support |In the intelligent assistant dialog box, enter "Create a compute," then confirm the information or make necessary modifications in the form before clicking **Execute**. |
||Connect compute |Support |In the intelligent assistant dialog box, enter “Show the connect information of compute [ComputeName\|ComputeId],” then confirm the information or make necessary modifications in the form before clicking **Execute**.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">You can specify the branch to modify by either <code>ComputeName</code> or <code>ComputeId</code>.</div><br> |
||Modify compute |Support |In the intelligent assistant dialog box, enter “Modify compute [ComputeName\|ComputeId]”, then confirm the information or make necessary modifications in the form before clicking **Execute**.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">You can specify the branch to modify by either <code>ComputeName</code> or <code>ComputeId</code>.</div><br> |
||Delete compute |Not support |Not involved |
|Account management<br><br> |Creating an account |Support |In the intelligent assistant dialog box, enter “Create an account,” then confirm the information or make necessary modifications in the form before clicking **Execute**. |
||Resetting an account password |Support |In the intelligent assistant dialog box, enter “Reset password of account [AccountName] under branch [BranchName\|BranchId]”, then confirm or modify the information in the form before clicking **Execute**.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">You can specify the branch to modify by either <code>BranchName</code> or <code>BranchId</code>.</div><br> |
||Delete an account |Not support |Not involved |
|Database management |Creating a database |Support |In the intelligent assistant dialog box, enter “Create database [DatabaseName] for branch [BranchName\|BranchId]”, then confirm or modify the information in the form before clicking **Execute**.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">You can specify the branch to modify by either <code>BranchName</code> or <code>BranchId</code>.</div><br> |
||Deleteing a database |Not support |Not involved |
|Monitoring |View monitoring information |Not support |Not involved |


<span id="crgqd1Lw"></span>
## Conversation management


* Create new conversation

   At the bottom of the intelligent assistant dialog box, click <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_6aa461210ee1e7bad6d039eb1a1f91b0.png)<sub> </sub></span>A new conversation can be created

* View historical conversations

   At the bottom of the intelligent assistant dialog box, click <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_bb943ab67ce812e08ded4282404cd260.png)<sub> </sub></span>You can view historical conversations and switch between multiple conversations
