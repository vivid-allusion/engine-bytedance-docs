---
title: "Using cloud PC"
product: "BytePlus ArkClaw Enterprise"
product_code: "ArkClaw"
source: "https://docs.byteplus.com/en/docs/ArkClaw/Using_cloud_PC_"
---

When ArkClaw is executing tasks in the cloud PC (such as desktop software operations or browser web interactions), it may encounter complex graphical verification codes, QR code login, or steps requiring manual confirmation. Under such circumstances, ArkClaw will automatically pause the task, push a takeover prompt, and wait for your manual intervention. You can also proactively take control of the cloud PC for manual operations.

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">The cloud PC feature is in<strong> Beta</strong>. Your participation and feedback are welcome. If you experience any problems, exceptions or have any suggestions during use, submit feedback by clicking "Settings \> Feedback".</div>


<span id="xGqowZhC"></span>
## Usage notes


* It is only supported on **PCs**, **Feishu**, and **WeChat**.

* If you use an ArkClaw Starter instance, due to instance configuration limitations, the cloud PC may respond slowly when handling complex tasks. To enjoy a smoother experience, you can click "Upgrade now" to upgrade to a higher specification. [Learn more](https://docs.byteplus.com/en/docs/ArkClaw/ArkClaw_specifications_and_applicable_scenarios).

   > Specification upgrading requires restarting the instance, during which the conversation feature will be suspended. Therefore, we recommend that you perform the upgrade during off\-peak hours.   
   

* When switching conversations or ArkClaw instances, the displayed cloud PC interface may temporarily differ from the actual running status in the background. This is a normal phenomenon and does not affect task execution or the final result. Our technical team has included this experience issue in the upgrade plan and will resolve it in an upcoming version.

* To enable ArkClaw to better understand and operate graphical interface applications (that is, execute CUA tasks), please use a GUI model that supports visual understanding. If the current model does not support visual GUI, ArkClaw will prompt you to switch the model as shown in the figure below. Click "Configure model" and follow the instructions to switch the model. 


<span id="37TKafBO"></span>
## Scenarios

You can use cloud PCs to meet the needs in the following scenarios:


* **System and application management**: Access the cloud PC desktop at any time to perform operations, such as **shutdown**, **restart**, **opening the terminal**, or **starting other applications**, just like on a regular computer.

* **Highly compatible browser tasks**: For websites with special risk control measures that cannot be accessed through conventional automation (such as some recruitment websites), cloud PCs provide a cloud browser mode that enables human\-like operations to improve task success rates. After the cloud browser automation task is completed, the system will automatically close the corresponding browser tab to release instance resources.

* **Graphical operations in a Linux environment**: If you need to run software with a graphical interface in a Linux environment, cloud PCs provide a convenient visual environment.


<span id="W3tzWpV2"></span>
## Step 1: Upgrade with one click to use the cloud PC feature

If you are currently using the cloud browser in ArkClaw and want a more comprehensive desktop\-level office experience, you can upgrade to cloud PC with one click through this operation. The upgraded cloud PC has a built\-in browser feature, fully meeting your work requirements.


1. Log in to the [ArkClaw console](https://console.byteplus.com/arkclaw/management).

2. Click the "Enter chat" button in the target ArkClaw card.

3. In the upper\-right corner of the  ArkClaw conversation page, click "<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_debe1670e9e734dc5913a7e4f591e928.png) </span>".

4. Click the "One\-click upgrade" button.

5. In the pop\-up dialog box, click "Confirm upgrade".

   > The upgrade process is expected to complete within 4–8 minutes. During the upgrade, do not close the terminal window. ArkClaw does not support chat during this period. Select an appropriate time to perform the upgrade.   
   

6. After the upgrade is complete, the system will automatically refresh and display the cloud PC desktop, allowing you to immediately start using the cloud PC.


<span id="nKb7pqg2"></span>
## Step 2: Use the cloud PC

You can use the cloud PC in any of the following ways.


<Tabs>
<Tab zoneid="uMzgfPk7" title="Active takeover">
<TabTitle>Active takeover</TabTitle>

1. Log in to the [ArkClaw console](https://console.byteplus.com/arkclaw/).

2. Go to the target ArkClaw page. In the upper\-right corner of the page, click the "<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_debe1670e9e734dc5913a7e4f591e928.png) </span>" button.

3. Click the "Start takeover" button in the upper\-right corner of the cloud PC page to take over the cloud PC and enter split\-screen mode to complete the task.

4. After the operation is complete, click "Exit takeover" or click the "<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_120966d3c6a34172a9db1207120aefa3.png) </span>" button to exit takeover. This returns control to ArkClaw to complete the subsequent process.


</Tab>
<Tab zoneid="uOv5QlNS" title="Automatic task pause">
<TabTitle>Automatic task pause</TabTitle>

This topic uses the following example to explain how to take over the cloud PC: When ArkClaw executes the task of **logging in to the BytePlus console** and detects a GUI interaction issue related to **QR code login**, it automatically pauses the task and sends a takeover prompt.


1. Log in to the [ArkClaw console](https://console.byteplus.com/arkclaw/).

2. Go to the target ArkClaw page.

3. Click the "Start takeover" button to enter the cloud PC operating environment.

4. In the browser opened on the cloud PC, enter the account and password.

5. After the operation is complete, click "Exit the takeover and AI continues" or click the "<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_120966d3c6a34172a9db1207120aefa3.png) </span>" button to exit takeover. This returns control to ArkClaw to complete the subsequent process.


</Tab>
<Tab zoneid="QFOy68ilXz" title="Use prompt">
<TabTitle>Use prompt</TabTitle>

1. Log in to the [ArkClaw console](https://console.byteplus.com/arkclaw/).

2. Go to the target ArkClaw page.

3. In the ArkClaw chat box, directly use the `/cua run <specific task>` command to quickly trigger ArkClaw to execute the cloud PC task.


</Tab>
</Tabs>


<div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="0">tip</div>


<div data-tips="true" data-tips-type="default" data-wrapper-indent="0">Task execution capabilities vary across different large models in the Coding Plan. If a cloud PC task cannot be automatically taken over due to intent recognition failure by the large model, you can enter the prompt "<strong>Take over cloud PC operations</strong>" in the dialog box for manual intervention.</div>


<span id="8P5oHiNI"></span>
## Other related operations


* **Enter full screen**: Click the <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_25630d04bd9957c042fd9ac9eaf29d10.png) </span> button in the upper\-right corner of the cloud PC to switch to full screen mode.

   * **Exit full screen**: In full screen mode, click the <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_101b53822bb89f0c5145f7fdd6e5a49c.png) </span> button to return to window mode.

   * **Adjust split\-screen ratio**: You can manually adjust the width ratio between the ArkClaw conversation page and the cloud PC by dragging the divider line. This helps adapt to view requirements in different operation scenarios.

   * **Restore cloud PC display**: When the cloud PC suffers from display interruption, slow response, abnormal display, or other problems, click the "<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_b8a0cf7be58683d89bbd14849171b6e6.png) </span>" button to attempt to restore the display. If the restoration fails, select "Settings ** \>**  Feedback" to obtain help.
