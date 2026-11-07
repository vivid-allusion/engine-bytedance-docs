---
title: "Troubleshooting ArkClaw failures through AI diagnosis"
product: "BytePlus ArkClaw Enterprise"
product_code: "ArkClaw"
source: "https://docs.byteplus.com/en/docs/ArkClaw/One-click_diagnosis_of_ArkClaw__"
---

AI diagnosis is a set of troubleshooting and recovery capabilities provided by ArkClaw. You can use this feature to identify and fix common operational issues in ArkClaw. When ArkClaw exceptions occur, such as no response or startup failure, you can manually trigger AI diagnosis, and the system will automatically perform troubleshooting and repair.

<span id="hSUpwFDQ"></span>
## Applicable scenarios


|Issue type |Applicable scenarios |
|---|---|
|ArkClaw unresponsiveness |Applicable when ArkClaw exceptions or crashes cause long\-term unresponsiveness. |
|ArkClaw startup failure |Applicable when ArkClaw fails to start properly, or keeps showing that `ArkClaw is being connected`. |
|ArkClaw slow response |Applicable when the conversation can be completed, but the overall response time is long. |
|Feature usage exceptions |Applicable to scenarios where functions such as models, plugins, Skills, and scheduled tasks encounter errors, execution failures, or abnormal results. |
|Other exceptions/uncertain issues |When the cause of the issue cannot be determined, you can prioritize selecting this option to perform a basic diagnosis of core services. For example, check whether ArkClaw is online, whether the service is running properly, and whether the responses stay stable. |


<span id="gwE0tveD"></span>
## Operation instructions


* Only ArkClaw instances in the **running** or **restarting** status support the AI diagnosis feature.

* AI diagnosis only supports fixing some automatically identifiable failures and **cannot cover** all issue scenarios (such as plugin/skill errors and third\-party IM connection exceptions). If your issue is not resolved through this diagnosis, you can provide feedback by referring to the "Issue not resolved" below for help.

* You can select multiple issue types simultaneously for batch troubleshooting, or repeatedly initiate diagnosis for issues of the same type to verify the issue status.


<span id="8dUq7AU9"></span>
## Procedure


1. Open your browser, enter the ArkClaw login URL in the address bar, and press Enter to access the ArkClaw conversation page.

2. Switch to the target ArkClaw.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_5c2bbeb3f786fde66eca65e3c98d4a8d.png) </span>

3. In the upper\-right corner of the page, click "...  **\>**  AI diagnosis".

4. Select the corresponding issue card based on the issue you encountered.

   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">Because the observability data masking capability has been enabled, some information required for diagnosis cannot be obtained, and deep diagnosis for slow responses may be difficult. To obtain more complete diagnosis results, contact the administrator to evaluate whether to temporarily disable this configuration.   </div>
   

5. (Optional) Enter issue symptoms, error messages and other details in the supplementary information field, such as specific scenarios of unresponsive instances and key error log snippets, to help the AI diagnosis assistant identify issues more accurately.

6. Click the "Start diagnosis" button and wait for the system to perform diagnosis and repair.

   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   * <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">The diagnosis and repair process is expected to take 3\-5 minutes. Please wait.   </div>
   

   * <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">To stop the diagnosis midway, click the "Cancel diagnosis" button. After the cancellation, the system will immediately stop subsequent diagnosis steps. Completed actions will not be automatically undone.   </div>
   

7. Based on the diagnosis result, you can perform the following operations:

   * **Continue diagnosis: ** You can further supplement the issue description based on the current diagnosis result, and the system will initiate a new diagnosis task.

   * **Evaluate the diagnosis result: ** You can provide feedback on each AI diagnosis by clicking the thumbs\-up or thumbs\-down button. The platform will identify issues arising during diagnosis based on your feedback and continuously optimize the diagnostic performance.

      * **Give a thumbs\-up for the diagnosis result:** 

         Below any satisfactory AI diagnostic response, click the <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_66b02a2acf5e3dccb0c12c5c9d84055d.png) </span>.

      * **Give a thumbs\-down for the diagnosis result:** 

         1. Below any unsatisfactory AI diagnostic response, click the <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_c1bdf3b26d4936c2db73b8b9e24c3743.png) </span> button.

         2. In the pop\-up window, select the reasons for your dissatisfaction (multiple selections allowed). Click the "Submit" button to complete the operation.


<span id="SEB1o7qo"></span>
## Related features


|Feature |Actions |
|---|---|
|Active pushing of diagnosis cards |When the AI diagnosis module detects an exception, it proactively pushes a diagnosis card via the ArkClaw Console or Feishu message channel to help you quickly identify the issue.<br><br><br>1. Install and enable the "ArkClaw error AI diagnosis plugin".<br><br>   1. This feature requires "ArkClaw Error AI Diagnosis plugin" `v 2026.7.14` or later. [Learn more](https://docs.volcengine.com/docs/87732/2275231)<br><br>   2. By enabling the "ArkClaw error AI diagnosis plugin", you can enable active pushing of diagnosis cards. [Learn more](https://docs.volcengine.com/docs/87732/2371396)<br><br>      <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="2">tip      </div><br>      <br><br>      <div data-tips="true" data-tips-type="default" data-wrapper-indent="2">By disabling the "ArkClaw error AI diagnosis plugin", you can disable active pushing of diagnosis cards.      </div><br>      <br><br>2. When the AI diagnosis module detects an exception in ArkClaw, it will push a diagnosis card to you when you send a message to ArkClaw.<br><br>3. Click the "Initiate diagnosis" button. The AI diagnosis module will automatically identify potential causes based on exception information and provide resolution suggestions. |
|View diagnosis history |You can also view the records and details of previous AI diagnoses to trace the troubleshooting process and repair result of the target diagnosis task.<br><br><br>1. Click <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_540b45c3f6349c15e87c0684db69a9ef.png) </span>.<br><br>2. In the diagnosis history list, find the target record and click the "View conversation" button to view details. |
|Create multiple diagnosis tasks |During **the current diagnosis**, you can initiate new diagnosis tasks. Multiple diagnosis tasks do not interfere with each other.<br><br><br>1. In the upper\-right corner of the AI diagnosis pane, click the ➕ icon to initiate a new diagnosis task.<br><br>2. Refer to the above [procedure](https://docs.byteplus.com/en/docs/394/104351#8dUq7AU9) to perform the diagnosis.<br><br>   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div><br>   <br><br>   * <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">Creating a new diagnosis does not interrupt ongoing diagnosis tasks.   </div><br>   <br><br>   * <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">To return to a previous diagnosis, click <img src="https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_540b45c3f6349c15e87c0684db69a9ef.png" width="20px" /> (diagnosis history) to view and switch.   </div><br>    |
