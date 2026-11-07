---
title: "Manual checkpoint"
product: "Code Pipeline"
product_code: "cp"
source: "https://docs.byteplus.com/en/docs/cp/Manual_checkpoint"
---

Code Pipeline provides a pre\-configured **manual confirmation** task, making it convenient for users to handle scenarios that require manual confirmation during pipeline execution, such as manual testing, security review, and more.

<span id=".6IOM5pmv5L-h5oGv"></span>
## Background Information

Code Pipeline allows users to configure the approver, approval rules, notification method, and timeout period for manual approval tasks. When the pipeline reaches a manual checkpoint task, it will enter a paused state and will resume only after the approver has granted approval. If approval is not completed within the specified time, the manual checkpoint task will fail.

<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites

If you wish to receive manual checkpoint task notifications via internal message, SMS, or email, please prepare the following in advance:


* Internal message

   The BytePlus account can receive site messages by default. Sub\-users must complete the following steps to receive internal messages.

   * You must configure the [SiteMessageReadOnlyAccess](https://console.byteplus.com/iam/policymanage/System/SiteMessageReadOnlyAccess) policy for sub\-users of your BytePlus account to obtain permission to view site messages.

   * BytePlus account users need to go to the [Message Center](https://console.byteplus.com/message/setting) to configure the receiving rules, add sub\-users as message recipients, and subscribe to operation and maintenance messages.

* SMS

   To receive notification messages via SMS, ensure that a security phone number is configured for the notification account.

* Emails

   If you want to receive notifications by email, please ensure that a security email is configured for the notification account.


<span id=".5L2_55So6ZmQ5Yi2"></span>
## Limit

To prevent excessive messaging, limits are placed on how frequently site messages, SMS, and emails can be received. For more details, see [Usage restrictions](https://docs.byteplus.com/en/docs/cp/Limit).

<span id=".5re75Yqg5Lu75Yqh"></span>
## Add tasks

When creating or editing a pipeline, go to the **Process Orchestration** tab, click **Add Job**, and the **Add Job** drawer will pop up. Select a task template **Process control \> Manual checkpoint**.

<span id=".5Y-C5pWw6K-05piO"></span>
## Parameter descriptions

Configure the manual checkpoint task as required.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Manual checkpoint tasks do not support adding other steps.</div>



|Configuration Item |Descriptions |
|---|---|
|Task name |Defaults to a manual checkpoint and supports custom task names. |
|Upstream task |Display the names of upstream serial tasks for the current task. Shown when there are no upstream tasks`-`。 |
|Approval methods |The following options are supported; please select as required.<br><br><br>* **Joint approval**: When all approvers have approved, the task is considered successful and the pipeline continues to run.<br><br>* **Any approver**: If any approver approves, the task is considered successful and the pipeline continues.<br><br>* **Partial approval**: If some people approve, the task is considered successful, and the pipeline continues to run. |
|Approvers |Select one or more target approvers. When the pipeline reaches a manual checkpoint task, it enters a paused state and will only resume running after the approver grants approval. |
|Number of people who passed |When configuring the number of approvals required for partial countersignature, it must be a positive integer greater than or equal to 2. The partial countersignature functionality, used in conjunction with the required number of approvals, defines the threshold for successful execution of a manual checkpoint task. |
|Timeout period |Set the automatic timeout for manual checkpoint tasks. If the approver does not complete the approval within the specified time, the manual approval task will automatically fail. The default timeout is 24 hours and can be modified. |
|Notification |After enabling Notification, the approver will be notified automatically when the pipeline reaches the manual checkpoint stage. |
|Notification rules |Select specific notification rules. Multiple selections supported.<br><br><br>* **Notify all approvers when approval is pending**: When the pipeline reaches the manual approval gate, a notification will be automatically sent to all approvers.<br><br>* **Notify the pipeline operator on approval failure**: When approval of a manual checkpoint task fails, a notification will be automatically sent to the operator of the current pipeline. If the pipeline is automatically triggered, a notification will be sent to the creator of the current pipeline. |
|Notification methods |Select specific notification methods, including internal message, SMS, and email. Supports multiple selection. |
|Task output |Display the current task artifacts. Display value when there are no products`-`。 |
|Advanced settings |**Webhook notification**: Supports sending task\-related notifications via Webhook, helping you stay informed about task updates. |


<span id=".6L-Q6KGM6K-05piO"></span>
## Operating instructions

When the pipeline reaches a manual checkpoint task, it enters a waiting state and waits for manual confirmation to continue running the pipeline.


* Approver: After receiving a pending approval notification, click the link to access the pipeline details, and review and approve the task as appropriate.

* Non\-approver: The manual checkpoint task is shown as pending approval. You can click to view the specific approver.


<span id=".5pel5b-X6K-m5oOF"></span>
## Log details

On the **Recent run details \> Run process** tab of the current pipeline, click the title of the manual checkpoint task card to view the run log and basic information about the task.


* Log: Displays the task's execution log in real time.

* Basic information: displays task details, including approver and approval status, as well as task configuration.
