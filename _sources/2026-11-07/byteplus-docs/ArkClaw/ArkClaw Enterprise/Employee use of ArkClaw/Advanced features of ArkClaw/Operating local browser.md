---
title: "Operating local browser"
product: "BytePlus ArkClaw Enterprise"
product_code: "ArkClaw"
source: "https://docs.byteplus.com/en/docs/ArkClaw/Operating_local_browser"
---

ArkClaw Janus is a browser extension that connects a local browser with the cloud\-based AgentKit runtime/OpenClaw to execute browser automation tasks or fetch webpage information. This topic describes how to install and use ArkClaw Janus, and how to record and automatically generate skill\-related operations. This allows you to quickly create standardized automation skills with no professional programming skills required.

<span id="JAHxzWGA"></span>
## Install the Janus browser extension


1. Open your browser, enter the ArkClaw login URL in the address bar, and press Enter.

2. Switch to the target ArkClaw page and click the details icon in the upper\-right corner.

3. Click the "Operate local browser" button.

4. In the pop\-up window, click "Download Janus extension" and extract the package locally.

5. Open Google browser, enter `chrome://extensions/` in the address bar to open the extension center, check "Developer mode" in the upper\-right corner, and click the "Load unpacked" button.

6. Select the extracted extension package, and click the "Select" button.

   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">If you download and extract the Janus installation package on a Windows system, select the corresponding Janus browser extension package in the extracted Janus folder for installation.   </div>
   

7. After the extension is loaded successfully, the following output is displayed.

8. On the ArkClaw conversation page, start the browser extension.

9. In the "ArkClaw Enterprise Edition" card, select the ArkClaw instance where you want to use the browser extension, and click "Use this instance".

   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">If an older version of Janus is detected, click the "Update Janus" button and then reconnect.   </div>
   

10. After the connection is established, you can start using the Janus extension.

   
   |Module no. |Description |
   |---|---|
   |1 |Command input box. You can enter` @` to quickly select a browser tab that is open in the current window. |
   |2 |The "Select element" feature is available, allowing you to select page elements quickly and precisely.<br><br><br>1. Click the "Select element" button.<br><br>2. Select the target button or area.<br><br>3. After selection, the name of the selected area or module is displayed in the command input box. |
   |3 |Two command types are supported: "Basic" and "Enhanced".<br><br><br>* **Basic**: No restrictions are applied to the current command.<br><br>* **Enhanced**: Allows you to constrain a command by "Target object", "Applicable scope", "Success criteria", and "Ambiguity handling". Therefore, you can execute the target command more precisely. |
   |4 |Constraint conditions available in Enhanced mode. |
   |5 |Conversation history. Click a conversation record to switch to that conversation for details. |
   |6 |New conversation. Create a new conversation. Multiple conversations can coexist and can be viewed in the conversation history. |
   |7 |Manage the Janus browser extension.<br><br><br>* **View logs**: Click to view operation logs. On the log details page, you can copy the log ID or download the log information to your local device.<br><br>* **Restart Janus**: Allows restarting the Janus browser extension.<br><br>* **Copy conversation**: Allows copying the command of the current conversation.<br><br>* **My commands**: Click the <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_a2f50cd95c15a397038da856096abd1d.png) </span> icon below the target command in a conversation, specify the command name, and save it. You can then quickly reuse the saved quick command from your commands. |
   |8 |Exit the Janus browser extension. |
   

&nbsp;

   <span id="aZSwS3ke"></span>
   ## Janus browser extension usage example

   <span id="hGXAlAqB"></span>
   ### Scenario example

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">The form system in this example is a simulated form used only for demonstration purposes.</div>


By sending a command to the Janus browser extension, you can specify the requirements for filling out a form in the simulated form system and quickly reuse the command later.

<span id="DoFnAfH5"></span>
### Procedure

1. Open Google Chrome, enter the ArkClaw login URL in the address bar to open the ArkClaw conversation page, and start the Janus browser extension.

2. Refer to the figure below to send a command and check the execution progress.

3. After successful execution, click the favorite icon.

4. Specify the quick command name and save command.

5. Click "+" to create a new conversation.

6. Click "... \> My commands".

7. Click the quick command name.

8. The quick command information is displayed in the input box. Update the fields you want to change, such as the departure date and return date. After modification, send the command to execute it.
