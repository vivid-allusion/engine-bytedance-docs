---
title: "Switching execution mode of cloud PC"
product: "BytePlus ArkClaw Enterprise"
product_code: "ArkClaw"
source: "https://docs.byteplus.com/en/docs/ArkClaw/Switching_execution_mode_of_cloud_PC_"
---

The cloud PC has four built\-in task execution modes: auto mode, OpenCli mode, browser mode, and cloud desktop mode. Before executing a task, you can specify which task execution mode will be prioritized for the current task based on the specific scenario. If the preferred task execution mode fails to run properly, ArkClaw will automatically switch to another mode and continue the task.

<span id="wLmKby25"></span>
## Descriptions of task execution modes


|Task execution mode |**Main capabilities** |**Applicable scenarios** |Limits |
|---|---|---|---|
|Auto mode (default) |ArkClaw intelligently decides and automatically selects the most suitable execution mode based on the task content. |ArkClaw intelligently analyzes task requirements and automatically matches the most efficient operating environment (terminal, web page, or desktop) for you, without manual intervention. |Decisions are based on ArkClaw's task understanding and may occasionally be suboptimal. |
|OpenCli mode |Provides a robust command\-line terminal environment, prioritizing CLI script capability. |Tasks are primarily executed through the underlying terminal and code scripts. Featuring ultra\-high speed and low resource overhead, this mode is applicable for pure text/data tasks such as batch file processing and code execution. |Not applicable for operating applications with complex GUIs. OpenCLI permission is required. |
|Browser mode |Executes tasks in the cloud browser environment, prioritizing browser tools. After the cloud browser automation task is completed, ArkClaw will automatically close the corresponding browser tab to release instance resources. |Applicable for online information search, filling web forms, or operating internal systems. ArkClaw will open a browser for you in the cloud, and automatically complete clicks and content searches. |Not applicable for operating local desktop applications. Before using this mode, you need to activate cloud browser resources. |
|Cloud desktop mode |Provides a complete cloud virtual desktop environment, automating operations on various applications as if performed by a real person. |Applicable for tasks that require operating specific client software, cross\-application collaboration, or complex visual interactions. |This mode depends on screen visibility and virtual mouse and keyboard. The performance varies by cloud PC specification. Cloud PC resources, image, and relevant permissions are required. |


<span id="Fmqrt1yr"></span>
## Usage notes


* Do not **switch task execution mode** while a task is being executed, as this may interrupt the current task and result in an error.

* After you switch the task execution mode, the current chat history and context will be retained, and no new session will be created.

* The current cloud browser environment **does not support** the cloud desktop mode. To have full desktop office experience and try other modes, we recommend that you [upgrade to cloud PC](https://docs.byteplus.com/en/docs/ArkClaw/Taking_over_cloud_PC_#Ki12IJPP).


<span id="7kv8zhZX"></span>
## Procedure


1. Open your browser, enter the ArkClaw login URL in the address bar, and press Enter.

2. Switch to the target ArkClaw.

3. In the upper\-right corner of the page, click <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_debe1670e9e734dc5913a7e4f591e928.png) </span>.

4. On the cloud PC page, click "<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_c8bb842f223dfaeb4e7faa4528f5029e.png) </span> \> Task execution preferences", and select the execution mode (for example, "Auto mode") for the current task.

5. (Optional) If the platform detects that ArkClaw has not installed the mode management plugin, a "Mode management plugin not installed" prompt will appear. Please click the “Confirm and install” button. The Platform will automatically configure the environment for you and restart the instance. After the instance has restarted, you can switch modes normally.

6. In the pop\-up window, select a task execution mode based on your needs.

   **Example**: You want to switch the mode to **Browser**. If the message  **"The preferred task execution mode for the cloud PC switched to: Browser"**  is displayed after you select this mode, the switch succeeded. Afterward, ArkClaw will prioritize calling the Browser Tool skill to execute browser\-related operations.
