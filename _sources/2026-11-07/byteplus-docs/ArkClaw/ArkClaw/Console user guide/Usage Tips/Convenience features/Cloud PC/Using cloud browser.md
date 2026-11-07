---
title: "Using cloud browser"
product: "BytePlus ArkClaw Enterprise"
product_code: "ArkClaw"
source: "https://docs.byteplus.com/en/docs/ArkClaw/Using_cloud_browser_"
---

ArkClaw may execute browser automation tasks or encounter graphical interface interactions that it cannot handle independently. These include complex graphic captchas, QR code login, high\-risk permission confirmation, and other similar scenarios. You can then manually take over the cloud\-hosted browser (cloud browser for short) and enter split\-screen mode to complete verification and processing. During task execution, you can also invoke the cloud browser at any time to check progress and details.

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="default">The cloud browser has been upgraded to a cloud PC. You can <a href="https://docs.byteplus.com/en/docs/ArkClaw/Using_cloud_PC_#W3tzWpV2">upgrade with one click to use the cloud PC</a> and run and manage various applications just as you would on a local computer.</div>


* <div data-tips="true" data-tips-type="default">This document <strong>applies only to users who have not upgraded and are still using the standalone "cloud browser" feature</strong>.</div>



<span id="RinJ1voi"></span>
## Usage notes


* It is only supported on **PCs**, **Feishu**, and **WeChat**.

* After the cloud browser automation task is completed, the system will automatically close the corresponding browser tab to release instance resources.

* A cloud browser is not supported when the ArkClaw runtime environment is being modified or its business logic is unavailable. Specific scenarios include:

   * ArkClaw is in the initialization phase.

   * ArkClaw is in the process of restarting.

   * ArkClaw is being fixed.

   * ArkClaw is restoring factory settings.

   * The ArkClaw account is in arrears.


<span id="WDRUsFtC"></span>
## Usage notes


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

   To ensure that ArkClaw can properly execute cloud browser tasks, the system has preset startup parameters for the cloud browser (such as limiting GPU usage and blocking system pop\-up windows). If the current cloud browser configuration cannot meet your needs, [contact us for feedback](https://docs.byteplus.com/en/docs/ArkClaw/Feedback__).


<span id="dc43xEJd"></span>
## Take over a cloud browser

You can take over a cloud browser in either of the following two ways.


<Tabs>
<Tab zoneid="zVNWJ0Gxiz" title="Active takeover">
<TabTitle>Active takeover</TabTitle>

1. Log in to the [ArkClaw console](https://console.byteplus.com/arkclaw/).

2. Go to the target ArkClaw page. In the upper\-right corner of the page, click the "<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_debe1670e9e734dc5913a7e4f591e928.png) </span>" button.

3. Click the "Start takeover" button in the upper\-right corner of the cloud browser page to take over the cloud browser and enter split\-screen mode to complete the task.

4. After the operation is complete, click "Exit takeover" or click the "<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_120966d3c6a34172a9db1207120aefa3.png) </span>" button to exit takeover. This returns control to ArkClaw to complete the subsequent process.


</Tab>
<Tab zoneid="DfgeodZDaL" title="Automatic task pause">
<TabTitle>Automatic task pause</TabTitle>

This topic uses the following example to explain how to take over the cloud browser: When ArkClaw executes the task of **logging in to the BytePlus console** and detects a GUI interaction issue related to **QR code login**, it automatically pauses the task and sends a takeover prompt.


1. Log in to the [ArkClaw console](https://console.byteplus.com/arkclaw/).

2. Go to the target ArkClaw page.

3. On the ArkClaw conversation page, click the "Start takeover" button to enter the cloud browser operation environment.

4. Enter your account and password in the cloud browser.

5. After the operation is complete, click "Exit the takeover and AI continues" or click the "<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_120966d3c6a34172a9db1207120aefa3.png) </span>" button to exit takeover. This returns control to ArkClaw to complete the subsequent process.


</Tab>
</Tabs>


<div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="0">tip</div>


<div data-tips="true" data-tips-type="default" data-wrapper-indent="0">Task execution capabilities vary among different large models in the Coding Plan. When a cloud browser task cannot be automatically taken over due to intent recognition failure of the large model, you can enter the instruction <strong>Take over browser operations</strong> in the chat box for manual intervention.</div>


<span id="iBoj7B2C"></span>
## View task progress and details

During task execution, you can invoke the cloud browser at any time to view task progress and details without waiting for the task to complete and without interrupting the current operation flow.

Click the "<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_debe1670e9e734dc5913a7e4f591e928.png) </span>" button in the upper\-right corner of the ArkClaw conversation page to view task progress and details.

<span id="k6kVDgG4"></span>
## Other related operations


* **Enter full screen**: Click the <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_25630d04bd9957c042fd9ac9eaf29d10.png) </span> button in the upper\-right corner of the cloud PC to switch to full screen mode.

   * **Exit full screen**: In full screen mode, click the <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_101b53822bb89f0c5145f7fdd6e5a49c.png) </span>" button to return to window mode.

   * **Adjust split\-screen ratio**: You can manually adjust the width ratio between the ArkClaw conversation page and the cloud browser by dragging the divider line. This helps adapt to view requirements in different operation scenarios.

   * **Restore cloud browser display**: When the cloud browser suffers from display interruption, slow response, abnormal display, or other problems, click the "<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_b8a0cf7be58683d89bbd14849171b6e6.png) </span>" button to attempt to restore the display. If the restoration fails, select "Settings ** \>**  Feedback" to obtain help.
