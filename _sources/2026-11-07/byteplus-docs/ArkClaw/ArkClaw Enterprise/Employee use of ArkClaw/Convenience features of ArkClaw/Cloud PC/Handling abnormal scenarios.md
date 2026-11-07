---
title: "Handling abnormal scenarios"
product: "BytePlus ArkClaw Enterprise"
product_code: "ArkClaw"
source: "https://docs.byteplus.com/en/docs/ArkClaw/Handling_abnormal_scenarios_"
---

<span id="Aqlnyn11"></span>
## Black screen on the cloud browser

A cloud browser may experience a temporary black screen or hide under the following operation scenarios. This is a normal interaction phenomenon and usually requires no operation. The system will recover automatically after a short while.


* Scenario 1: Initial loading phase

   Due to different network environments on different devices, the initial loading of the cloud browser may not be completed immediately, resulting in a temporary black screen.

   Recommendation: Wait a few seconds and the page will load normally.

* Scenario 2: Exiting the cloud browser

   A temporary black screen appears when you click the "Exit" button to exit the cloud browser.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_57aeaa0c7110f2e42d90b602d529be82.png) </span>

   Recommendation: Wait a few seconds. The system will automatically finish reloading and resume normal use.

* Scenario 3: Minimizing the cloud browser

   After you click the "Minimize" button, the browser window is hidden to the system navigation bar, causing a black screen.

   Solution: If in full screen mode, first click the "<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_6cac8c456778ebdc4615823b720eac04.png) </span>" button to exit full screen, and then send the instruction: "My browser has been minimized. Please relaunch it". The system will automatically invoke the cloud browser again.


&nbsp;

<span id="nEhaseRb"></span>
## File download failures in the cloud browser

**Solution:** 


1. Open your browser, enter the ArkClaw login URL in the address bar, and press Enter to access the ArkClaw conversation page.

2. Go to the target ArkClaw page, enter the following content in the ArkClaw chat box, and send the message:

   ```Plain Text
   Optimize browser capabilities. Before triggering actions such as downloading or clicking "Download", run the command: curl -fsSL https://browser-use.tos-cn-beijing.volces.com/fix-cdp-download.py | python3. Then, proceed with the downloading or saving tasks.
   ```
   

3. ArkClaw will automatically execute the repair script and update the browser skill configuration. Once it is completed, you can proceed with file download tasks normally.

   > To perform further operations based on the downloaded content, send the corresponding prompt in the dialog box to complete the task.

   > **Sample prompt**: After I click "Download" in the browser, the file can be read from `/home/browser/Downloads`.
