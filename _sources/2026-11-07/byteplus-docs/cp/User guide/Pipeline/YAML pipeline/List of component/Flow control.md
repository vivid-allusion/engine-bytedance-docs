---
title: "Flow control"
product: "Code Pipeline"
product_code: "cp"
source: "https://docs.byteplus.com/en/docs/cp/Process_control_steps"
---

<span id="ZMgxQcAJ"></span>
## Selectors

Create an interactive selection node in the pipeline. When this Addon is executed, it will suspend and provide predefined options to specified operators. After the operators make a selection, the corresponding subsequent task branch is triggered. If no selection is made before the timeout, the task will fail and terminate.


* **Addon**: selector@1.0.0

* **Parameter**:

   
   |Parameter |Type |Required |Default value |Description |
   |---|---|---|---|---|
   |operators |string |Yes |\- |List of users allowed to perform selection actions, format is AccountId,UserId. If the user performing the selection action is the primary account, UserId is 0, such as `21004****,0`. |
   |selectors |list |Yes |\- |Define the list of options visible to the user.<br><br><br>* label **: ** Text displayed for the option in the interface.<br><br>* select: Option ID, must be unique within the current pipeline, used for subsequent branch determination. |
   |timeout |duration |Yes |2h |Timeout time for selection actions, maximum is 3 days. Supported time units:<br><br><br>* m: Minutes.<br><br>* h: Hours.<br><br>* d: Days. |
   

* **Example**

   ```YAML
   tasks:
     - task: task-selector
       displayName: "Version Selector"
       component: selector@1.0.0
       inputs:
         operators:
           - 210048****,6162****
           - 210048****,0
         selectors:
           - label: "Deploy v2"
             select: "deploy-v2"
           - label: "Deploy v1"
             select: "deploy-v1"
         timeout: 2h
   ```
   


<span id="8fnNqQ1M"></span>
## Manual checkpoint

Set a suspend point at a key node in the pipeline, waiting for specified approvers to manually approve or reject. Once the approval policy is met, the pipeline will continue or terminate, providing manual review assurance for high\-risk actions. If approval is not completed before the timeout, the task will fail.


* **Addon**: manual\-approval@1.0.0

* **Parameter**:

   
   |Parameter |Type |Required |Default value |Description |
   |---|---|---|---|---|
   |approvalType |enum |Yes |And |Approval policy.<br><br><br>* And: All approvers pass.<br><br>* Or: Any approver passes.<br><br>* Partial: A specified quantity of approvers pass. When quota is set for this parameter, approveCount must be greater than 0 and not exceed the length of the approvers list. |
   |approveCount |int |No |\- |The quantity of approvers required to pass, scope 1 <= approveCount <= total number of approvers.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">Required when approvalType is Partial.</div><br> |
   |approvers |list |Yes |\- |Approver list, format is AccountId,UserId. If the approver is the primary account, UserId is 0, such as `21004****,0`. |
   |notification |object |No |enable: false |Approval notification configuration.<br><br><br>* enable **: ** Whether to enable notification.<br><br>   * true: Yes.<br><br>   * false: Default value, disable.<br><br>* methods: Supported when enable is true. Notification method, supports the following values:<br><br>   * StationLetter: Station letter.<br><br>   * Sms: SMS.<br><br>   * Email: Email.<br><br>* rules **: ** Supported when enable is true. Notification rule, supports the following values:<br><br>   * NotifyTriggererWhenDeclined: Notify the runner when declined.<br><br>   * NotifyAllApproversWhenWaitApproval: Notify all approvers when waiting for approval. |
   |timeout |duration |Yes |2h |Timeout time for approval actions. |
   

* **Example**

   ```YAML
   tasks:
     - task: task-manual-approval-partial
       displayName: "Security Audit Approval (2/3)"
       component: manual-approval@1.0.0
       inputs:
         approvalType: Partial
         approveCount: 2
         approvers:
           - 210048****,0
           - 210048****,***1
           - 210048****,***2
         timeout: 2h
   ```
