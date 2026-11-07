---
title: "Initiating tasks"
product: "BytePlus ArkClaw Enterprise"
product_code: "ArkClaw"
source: "https://docs.byteplus.com/en/docs/ArkClaw/Initiating_tasks"
---

By default, purchased ArkClaw provides only one conversation page for initiating conversation tasks. You can create a new conversation to start a brand\-new task unrelated to the current conversation while keeping your existing conversation for parallel task processing. This allows you to switch task scenarios, avoid interference from historical context, and support categorized archiving and later review.

<span id="h2y3JMit"></span>
## Usage notes

To create multiple conversation tasks, you need to complete the first interaction in the newly created conversation before creating the next one.

**Example**: After creating Conversation A, you need to send a message in Conversation A (complete one round of initial interaction) for the operation to take effect. Then, you can create Conversation B, and so on to create more new conversations.

<span id="OTzwtDfz"></span>
## Initiating tasks


1. Open your browser, enter the ArkClaw login URL in the address bar, and press Enter.

2. Switch to the target ArkClaw page. In the directory tree on the left, select "Initiate task" to create a new conversation.

1. You can also view the created conversations in the left navigation pane:

   * The first new conversation is named "New chat" by default. After the first round of conversation, the system will automatically rename it to the content of the first round of interaction, truncating any content beyond 60 characters. You can also[ manually rename](https://docs.byteplus.com/en/docs/394/104329#ZFIj3X1R) the conversation.

   * Subsequent conversations are automatically named using the content of the first message (truncated to a maximum of 60 characters). You can also[ manually rename](https://docs.byteplus.com/en/docs/394/104329#ZFIj3X1R) the conversation.

   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">You can view the new conversations created under an ArkClaw instance only after you switch to the ArkClaw page.   </div>
   

2. Enter the newly created conversation page to get started with ArkClaw.

   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">The platform provides preset prompts for various scenarios. You can select a prompt to quickly start a conversation.   </div>
   

   1. <div data-tips="true" data-tips-type="default" data-wrapper-indent="1"><strong>Select the target task scenario:</strong> Perform the corresponding operations based on the agent type:   </div>
   

      * <div data-tips="true" data-tips-type="default" data-wrapper-indent="1"><strong>Primary agent</strong> (<strong>ID: main</strong>):   </div>
   

      <div data-tips="true" data-tips-type="default" data-wrapper-indent="1"><strong>Reuse prompt</strong>: Click the target tab (such as "Information acquisition" and "Scheduled task"). Find the target card under the corresponding type, and simply click the "<strong>Replicate"</strong> button to reuse the configuration for this scenario.      </div>
      

      * <div data-tips="true" data-tips-type="default" data-wrapper-indent="1"><strong>Other agents</strong>:   </div>
   

         * <div data-tips="true" data-tips-type="default" data-wrapper-indent="1"><strong>Reuse prompt</strong>: Select a preset prompt, or select the target card and click the "<strong>Replicate"</strong> button to reuse the configuration for this scenario.   </div>
   

         * <div data-tips="true" data-tips-type="default" data-wrapper-indent="1"><strong>Replay</strong>: In the target card, click the "<strong>Replay</strong>" button to preview the operation demo (this feature is only available for partial agents currently).   </div>
   

   2. <div data-tips="true" data-tips-type="default" data-wrapper-indent="1"><strong>Confirm the prompt content</strong>   </div>
   

   <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">The system will automatically prefill the prompt based on the selected scenario. Confirm that the prefilled content is correct, or change it as needed.   </div>
   

   3. <div data-tips="true" data-tips-type="default" data-wrapper-indent="1"><strong>Submit and send the prompt</strong>   </div>
   

   <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">After confirming the content, send it to complete the operation.   </div>
   


<span id="qGcMRrGZ"></span>
## Sandbox execution instructions

A sandbox is an independent, isolated runtime environment used to securely execute tasks, run code, or perform debugging. You can regard it as a temporary controlled workspace where tasks are executed, minimizing impacts on external environments.

When you initiate a task, the system automatically determines whether the current task needs to be executed in the sandbox environment. If needed, the system will automatically start the corresponding sandbox instance to execute the task within the sandbox and return results upon completion. The overall workflow is as follows:

**Initiate a task → Automatically start a sandbox instance → Execute the task in the sandbox → Return results**

> If the system prompts that the Sandbox Center is not activated, contact your enterprise administrator to complete the activation and try again.


During execution, the real\-time progress of tool calls is displayed in the conversation area. You can click the "Expand" or "Collapse" button in the tool call module to view or hide execution details such as tool parameters and returned results.

<span id="ZFIj3X1R"></span>
## Related features


|Feature |Description |
|---|---|
|/new command: creates a conversation and switches to the new conversation |Send the `/new` command, and ArkClaw will immediately create a conversation task and automatically switch to the new conversation. This feature enables context isolation between different tasks, allowing you to quickly start an independent conversation. |
|Speech\-to\-text |When typing is inconvenient or you need to enter long texts, click the <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_223c62a3491804f51a274a3c138eebdc.png) </span> **button** on the right side of the chat box to input task requirements by voice. This enhances interaction and command delivery efficiency. |
|Download the output |After the task is completed, the output is only temporarily saved. Please download it to your local device or transfer it to your cloud disk promptly.<br><br>> If you do not have a personal cloud disk, you can [activate the personal cloud disk service](https://docs.byteplus.com/en/docs/ArkClaw/Personal_cloud_disks?lang=en) first. |
|Share the output |You can share the generated output (PPT, PDF, image, static website, etc.) in the form of link for preview by enterprise internal employees as needed.<br><br>> When employees open the shared link, they need to log in via enterprise SSO first. Employees without Claw accounts cannot view the content. Contact the enterprise administrator to grant them access permissions.<br><br><br><br>1. Click the output card. In the expanded panel on the right, click the <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_7dbd0ae998fefed8564c92f675e63693.png) </span>.<br><br>2. In the pop\-up dialog box, click the "Copy link" button.<br><br>3. Send the copied link to the personnel who need to view the content.<br><br>   > The maximum size for a single shared file is 20 MB. If the size exceeds this limit, sharing is not supported. Download the file directly or streamline the content and try again.   <br>   <br><br>   4. (Optional) Download the output file to local storage or transfer it to the cloud disk.<br><br>   > To transfer to the cloud disk, you need to activate the personal cloud disk. If you have not activated it yet, refer to [How to activate personal cloud disk](https://docs.byteplus.com/en/docs/ArkClaw/Personal_cloud_disks?lang=en). |
|Rename |You can modify the conversation name based on your needs.<br><br><br>1. In the left navigation pane, click the name of the conversation to be renamed.<br><br>2. Click "···  **\>**  Rename" **.** <br><br>3. Enter the name in the pop\-up dialog box, and click the "Confirm" button to complete the operation. |
|Delete |If an existing conversation does not meet your needs, you can delete it at any time.<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">Deleted conversations cannot be restored. Proceed with caution.</div><br><br><br><br>1. In the left navigation pane, click the name of the conversation to be deleted.<br><br>2. Click "···  **\>**  Delete" **.** <br><br>3. Confirm the conversation to be deleted is correct, and then click the "Confirm" button to complete the operation. |
|Clear history |Clearing history only empties the chat context of the current session and does not affect your long\-term memory.<br><br>> Long\-term memory: Key information that the system persistently stores for you. It will not be lost when you clear the history of a single conversation. In subsequent conversations, the system will provide more coherent responses that better align with your habits based on this stored key information.<br><br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">Once the historical context of a session is cleared, it cannot be restored. Proceed with caution.</div><br><br><br><br>1. In the left navigation pane, click the name of the conversation to be deleted.<br><br>2. Click "···  **\>**  Clear history" **.** <br><br>3. Confirm the history you want to clear and click the "Confirm clear" button to complete the operation. |
