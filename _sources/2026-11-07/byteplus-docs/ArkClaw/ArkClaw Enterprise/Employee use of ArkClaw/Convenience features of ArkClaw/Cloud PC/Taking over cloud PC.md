---
title: "Taking over cloud PC"
product: "BytePlus ArkClaw Enterprise"
product_code: "ArkClaw"
source: "https://docs.byteplus.com/en/docs/ArkClaw/Taking_over_cloud_PC_"
---

When ArkClaw is executing tasks in the cloud PC (including desktop software operations or browser web interactions), it may encounter complex graphical verification codes, QR code login, or steps requiring manual confirmation. Under such circumstances, ArkClaw will automatically pause the task, push a takeover prompt, and wait for your manual intervention. You can also proactively take control of the cloud PC for manual operations.

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">The cloud PC feature is in<strong> Beta</strong>. Your participation and feedback are welcome. If you experience any problems, exceptions or have any suggestions during use, submit feedback by clicking "Settings \> Feedback".</div>


<span id="xGqowZhC"></span>
## Usage notes


* It is only supported on **PCs**, **Feishu**, and **WeChat**.

* When switching conversations or ArkClaw instances, the displayed cloud PC interface may temporarily differ from the actual running status in the background. This is a normal phenomenon and does not affect task execution or the final result. Our technical team has included this experience issue in the upgrade plan and will resolve it in an upcoming version.

* To enable the AI to understand better and operate graphical interface applications (i.e., perform CUA tasks), use a GUI model that supports visual understanding. If the current model does not support GUI, ArkClaw will prompt you to switch the model as shown in the figure below. Click "Configure model" and follow the instructions to switch the model. [Learn more](https://docs.byteplus.com/en/docs/ArkClaw/Adjusting_ArkClaw_inference_models__).


<span id="37TKafBO"></span>
## Scenarios

You can use cloud PCs to meet the needs in the following scenarios:


* **System and application management**: Access the cloud PC desktop at any time to perform operations, such as **shutdown**, **restart**, **opening the terminal**, or **starting other applications**, just like on a regular computer.

* **Highly compatible browser tasks**: For websites with special risk control measures that cannot be accessed through conventional automation (such as some recruitment websites), cloud PCs provide a cloud browser mode that enables human\-like operations to improve task success rates. 

* **Graphical operations in a Linux environment**: If you need to run software with a graphical interface in a Linux environment, cloud PCs provide a convenient visual environment.


<span id="Ki12IJPP"></span>
## Step 1: Upgrade with one click to use the cloud PC feature


<Tabs>
<Tab zoneid="h8supohE" title="Upgrade from a cloud browser to a cloud PC">
<TabTitle>Upgrade from a cloud browser to a cloud PC</TabTitle>

**Applicable scenario**: If you are currently using the cloud browser in ArkClaw and want a more comprehensive desktop\-level office experience, you can upgrade to cloud PC with one click through this operation. The upgraded cloud PC has a built\-in browser feature, fully meeting your work requirements.


1. Open your browser, enter the ArkClaw login URL in the address bar, and press Enter.

2. Go to the target ArkClaw page.

3. In the upper\-right corner of the page, click <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_debe1670e9e734dc5913a7e4f591e928.png) </span>.

4. Click the "One\-click upgrade" button.

5. In the pop\-up dialog box, click "Confirm upgrade".

   > The upgrade process is expected to complete within 4–8 minutes. During the upgrade, do not close the terminal window. ArkClaw does not support chat during this period. Select an appropriate time to perform the upgrade.   
   

6. After the upgrade is complete, the system will automatically refresh and display the cloud PC desktop, allowing you to immediately start using the cloud PC.


</Tab>
<Tab zoneid="AhyXPvvE" title="Directly upgrade to a cloud PC">
<TabTitle>Directly upgrade to a cloud PC</TabTitle>

**Applicable scenario:**  If you have never used the cloud browser in ArkClaw, you can upgrade to the cloud PC with one click through this opeation.


1. Open your browser, enter the ArkClaw login URL in the address bar, and press Enter.

2. Go to the target ArkClaw page.

3. In the upper\-right corner of the page, click <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_debe1670e9e734dc5913a7e4f591e928.png) </span>.

4. Click the "One\-click upgrade" button.

   > The upgrade process is expected to complete within 4–8 minutes. During the upgrade, do not close the terminal window. ArkClaw does not support chat during this period. Select an appropriate time to perform the upgrade.   
   

5. After the upgrade is complete, the system will automatically refresh and display the cloud PC desktop, allowing you to immediately start using the cloud PC.


</Tab>
</Tabs>


<span id="eJC4wBIV"></span>
## Step 2: Take over a cloud PC

You can take over a cloud PC in either of the following two ways.


<Tabs>
<Tab zoneid="uMzgfPk7" title="Active takeover">
<TabTitle>Active takeover</TabTitle>

1. Open your browser, enter the ArkClaw login URL in the address bar, and press Enter.

2. Go to the target ArkClaw page.

3. In the upper\-right corner of the page, click <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_debe1670e9e734dc5913a7e4f591e928.png) </span>.

4. Click the "Start takeover" button in the upper\-right corner of the cloud PC page to take over the cloud PC and enter split\-screen mode to complete the task.

5. After the operation is complete, click "Exit takeover" or click the "<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_120966d3c6a34172a9db1207120aefa3.png) </span>" button to exit takeover. This returns control to ArkClaw to complete the subsequent process.


</Tab>
<Tab zoneid="uOv5QlNS" title="Automatic task pause">
<TabTitle>Automatic task pause</TabTitle>

This topic uses the following example to explain how to take over the cloud browser: When ArkClaw executes the task of **logging in to the BytePlus console** and detects a GUI interaction issue related to **QR code login**, it automatically pauses the task and sends a takeover prompt.


1. On the ArkClaw conversation page, click the "Start takeover" button to enter the cloud browser operation environment. 

2. In the browser opened on the cloud PC, complete operations such as entering your account, scanning QR code, and verification.

3. After the operation is complete, click "Exit takeover" or click the "<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_120966d3c6a34172a9db1207120aefa3.png) </span>" button to return control to ArkClaw to complete the subsequent process.


</Tab>
<Tab zoneid="xcKZ2rCYga" title="Use prompt">
<TabTitle>Use prompt</TabTitle>

1. Open your browser, enter the ArkClaw login URL in the address bar, and press Enter.

2. Go to the target ArkClaw page.

3. In the dialog box, enter the `/cua run <specific task>` command to quickly trigger ArkClaw to execute the cloud PC task.


</Tab>
</Tabs>


<div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="0">tip</div>


<div data-tips="true" data-tips-type="default" data-wrapper-indent="0">Task execution capabilities vary among different large models in the Coding Plan. If a cloud browser task cannot be automatically taken over due to intent recognition failure by the large model, you can enter the prompt "<strong>Take over cloud PC operations</strong>" in the dialog box for manual intervention.</div>


<span id="8P5oHiNI"></span>
## Other related operations


* **Enter full screen**: Click the <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_25630d04bd9957c042fd9ac9eaf29d10.png) </span> button in the upper\-right corner of the cloud PC to switch to full screen mode.

   * **Exit full screen**: In full screen mode, click the <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_101b53822bb89f0c5145f7fdd6e5a49c.png) </span> button to return to window mode.

   * **Adjust split\-screen ratio**: You can manually adjust the width ratio between the ArkClaw conversation page and the cloud PC by dragging the divider line. This helps adapt to view requirements in different operation scenarios.

   * **Restore cloud PC display**: When the cloud PC suffers from display interruption, slow response, abnormal display, or other problems, click the <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_5aec990f4a7216d8f9de59552349332d.png) </span> button to attempt to restore the display. If the restoration fails, select "Settings ** \>**  Feedback" to obtain help.

   * **Download output files**: After ArkClaw completes a task involving file generation, the system will display a card containing the output files in the chat window. You can click the "..." button on the card to **download the files to a local device** or **save them to a cloud disk**.

   > * Note: If you are prompted to activate personal space first, refer to [enterprise cloud drive](https://docs.byteplus.com/en/docs/ArkClaw/Claw_cloud_disk?lang=en) or [personal cloud drive](https://docs.byteplus.com/en/docs/ArkClaw/Personal_cloud_disks?lang=en) to complete the activation.

   > * Note: If you are prompted that the administrator has not activated the cloud drive, contact the administrator to activate it and try again.
