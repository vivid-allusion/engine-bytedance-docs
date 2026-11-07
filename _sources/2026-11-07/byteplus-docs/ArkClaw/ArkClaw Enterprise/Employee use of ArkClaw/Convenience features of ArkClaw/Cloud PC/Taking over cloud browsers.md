---
title: "Taking over cloud browsers"
product: "BytePlus ArkClaw Enterprise"
product_code: "ArkClaw"
source: "https://docs.byteplus.com/en/docs/ArkClaw/Taking_over_cloud_browsers__"
---

ArkClaw may execute browser automation tasks or encounter graphical interface interactions that it cannot handle independently. These include complex graphic captchas, QR code login, high\-risk permission confirmation, and other similar scenarios. You can then take over the cloud\-hosted browser (cloud browser for short) and enter split\-screen mode to complete verification and processing. During task execution, you can also invoke the cloud browser at any time to check progress and details.

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="default">You can <a href="https://docs.byteplus.com/en/docs/ArkClaw/Taking_over_cloud_PC_#Ki12IJPP">one\-click upgrade cloud browser to cloud PC</a>, allowing you to run and manage various applications just as you would on a local computer.</div>


* <div data-tips="true" data-tips-type="default">This document <strong>applies only to users who have not upgraded and are still using the standalone "cloud browser" feature</strong>.</div>



<span id="7WptoNqt"></span>
## Usage notes


* It is only supported on **PCs**, **Feishu**, and **WeChat**.

* If the system prompts that your current ArkClaw version does not support the cloud PC feature, you can click "One\-click upgrade" to perform a upgrade and use the [cloud PC](https://docs.byteplus.com/en/docs/ArkClaw/Taking_over_cloud_PC_) feature.

* When you use an ArkClaw Starter instance, cloud browser operations may experience lag due to instance resource limitations. For better performance and smoother cloud experience, we recommend that you [purchase a higher-specification instance package](https://docs.byteplus.com/en/docs/ArkClaw/Creating_ArkClaw_#SdWGV7CH).

* A cloud browser is not supported when the ArkClaw runtime environment is being modified or its business logic is unavailable. Specific scenarios include:

   * ArkClaw is in the initialization phase.

   * ArkClaw is in the process of restarting.

   * ArkClaw is being fixed.

   * ArkClaw is restoring factory settings.

   * The ArkClaw account is in arrears.


<span id="njuM2baV"></span>
## Precautions


* **Task\-triggered website security interception (risk control/captcha)** 

   Some websites (such as e\-commerce and social platforms) adopt strict security risk control policies. Accessing these websites through a cloud browser can be easily identified and blocked, and may even lead to account restrictions in serious cases. To avoid account risks, we recommend that you use a cloud browser to visit such websites with caution and do not log in to important accounts.

* **Browser website login cache**

   After you log in to a website via the default cloud browser, the system will not automatically clear the website login cache.

   To log in again or log out of your account, you can send a logout command in the chat box for ArkClaw to perform the operation, or manually take over the browser to complete relevant operations.

* **Browser password saving**

   Cloud browser supports password saving, but does not save passwords automatically. You need to manually enable this feature and save passwords. To clear saved passwords, take over the cloud browser first.

   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">To ensure account security, we <strong>recommend that you do not</strong> save accounts and passwords related to personal assets or important information in the cloud browser environment.   </div>
   

* **Default browser startup configuration**

   To ensure that ArkClaw can properly execute cloud browser tasks, the system has preset startup parameters for the cloud browser (such as limiting GPU usage and blocking system pop\-up windows). If the current cloud browser configuration cannot meet your needs, [contact us for feedback](https://docs.byteplus.com/en/docs/ArkClaw/Feedback_).


<span id="Kw0GKtDv"></span>
## Take over a cloud browser

You can take over a cloud browser in either of the following two ways.


<Tabs>
<Tab zoneid="88Z0fbbt" title="Active takeover">
<TabTitle>Active takeover</TabTitle>

1. Open your browser, enter the ArkClaw login URL in the address bar, and press Enter.

2. Go to the target ArkClaw page.

3. In the upper\-right corner of the page, click <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_debe1670e9e734dc5913a7e4f591e928.png) </span>.

4. Click the "Start takeover" button in the upper\-right corner of the cloud browser page to take over the cloud browser.

   After the takeover, the page displays **Manual takeover in progress**.

5. After the operation is complete, click "Exit takeover" or click the <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_120966d3c6a34172a9db1207120aefa3.png) </span> button to exit takeover. This returns control to ArkClaw to complete the subsequent process.





</Tab>
<Tab zoneid="XXyTXSuG" title="Automatic task pause">
<TabTitle>Automatic task pause</TabTitle>

This topic uses the following example to explain how to take over the cloud browser: When ArkClaw executes the task of **logging in to the BytePlus console** and detects a GUI interaction issue related to **QR code login**, it automatically pauses the task and sends a takeover prompt.


1. On the ArkClaw conversation page, click the "Start takeover" button to enter the cloud browser operation environment.

2. Enter your account and password in the cloud browser.

3. After the operation is complete, click "Exit takeover" or click the "<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_120966d3c6a34172a9db1207120aefa3.png) </span>" button to exit takeover. This returns control to ArkClaw to complete the subsequent process.


</Tab>
</Tabs>


<div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="0">tip</div>


<div data-tips="true" data-tips-type="default" data-wrapper-indent="0">Task execution capabilities vary among different large models in the Coding Plan. When a cloud browser task cannot be automatically taken over due to a large model intent\-recognition failure, you can enter the instruction "<strong>Take over browser operations</strong>" in the chat box for manual intervention.</div>


<span id="nzXAHOZ7"></span>
## View task progress and details

During task execution, you can invoke the cloud browser at any time to view task progress and details without waiting for the task to complete and without interrupting the current operation flow.


1. Open your browser, enter the ArkClaw login URL in the address bar, and go to the session window.

2. Switch to the target ArkClaw page and click the <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_debe1670e9e734dc5913a7e4f591e928.png) </span> button in the upper\-right corner of the ArkClaw conversation page to view task progress and details.


<span id="OqxSIjCx"></span>
## Other related operations


* **Enter full screen**: Click the <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_25630d04bd9957c042fd9ac9eaf29d10.png) </span> button in the upper\-right corner of the cloud PC to switch to full screen mode.

   * **Exit full screen**: In full screen mode, click the <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_101b53822bb89f0c5145f7fdd6e5a49c.png) </span> button to return to window mode.

   * **Adjust split\-screen ratio**: You can manually adjust the width ratio between the ArkClaw conversation page and the cloud PC by dragging the divider line. This helps adapt to view requirements in different operation scenarios.

   * **Restore cloud PC display**: When the cloud PC suffers from display interruption, slow response, abnormal display, or other problems, click the <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_5aec990f4a7216d8f9de59552349332d.png) </span> button to attempt to restore the display. If the restoration fails, select "Settings ** \>**  Feedback" to obtain help.


&nbsp;
