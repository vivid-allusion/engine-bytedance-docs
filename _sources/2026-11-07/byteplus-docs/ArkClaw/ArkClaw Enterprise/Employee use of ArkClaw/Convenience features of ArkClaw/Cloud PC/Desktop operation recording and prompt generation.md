---
title: "Desktop operation recording and prompt generation"
product: "BytePlus ArkClaw Enterprise"
product_code: "ArkClaw"
source: "https://docs.byteplus.com/en/docs/ArkClaw/Desktop_operation_recording_and_prompt_generation_"
---

To efficiently and accurately match your task procedures and expected results, ArkClaw delivers an end\-to\-end workflow covering recording, extraction, and execution and saving. You can record actual operation steps in a cloud PC. The system automatically analyzes video content in the cloud and converts it into a structured prompt. The generated task procedures can be executed automatically or saved as exclusive skills with one click for reuse by individuals or teams, enabling efficient accumulation of automation assets.

<span id="yEiTLeZt"></span>
## Usage notes


* If you refresh the browser during recording, the recording task will not be interrupted. You can resume operation demonstration after the page is restored.

* The recording duration is displayed in real time on the interface throughout the recording process. The system supports the following recording parameters:

   
   |**Parameter​**  |**Value** |**Description** |
   |---|---|---|
   |Maximum duration |10 minutes |The system will automatically stop recording once the duration reaches 10 minutes. |
   |Video format |MP4 or MKV (H.264 encoded) |It is compatible with mainstream players and supports stream writing. |
   |Resolution |Consistent with the cloud desktop resolution |Typically 1920 x 1080. |
   |Frame rate |15 fps or 30 fps |Achieve a balance between image clarity and file size. |
   |Audio |None |Only screen operations are recorded without audio capture. |
   |Single file size |200 MB |If the file size exceeds the upper limit, the system will automatically compress the file or display an error message. |
   


<span id="N3FR08zh"></span>
## Record and generate prompts


1. Open your browser, enter the ArkClaw login URL in the address bar, and press Enter.

2. Go to the target ArkClaw page. In the upper\-right corner of the page, click <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_debe1670e9e734dc5913a7e4f591e928.png) </span>.

3. Click "<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_74569899b7883fb9291dc70a8a3e5909.png) </span> \> Record and generate prompts" button.

4. In the pop\-up dialog box, click the "Start recording" button and start your manual operations in the cloud PC.

   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">If you refresh the browser during recording, the recording task will not be interrupted. You can resume recording your operations after the page is restored.   </div>
   

5. After you complete the operation demonstration, click the "End recording" button.

6. In the pop\-up panel displayed upon the completion of recording, you can view the recording file information and perform the following operations.

   
   |Module |Description |
   |---|---|
   |**Preview videos** |You can preview or play videos, and save video files to the cloud disk.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="default">You can preview or play videos only when the cloud disk feature is enabled. If you have not enabled it yet, click "Go to enable cloud disk" to enable the feature. If the "Your enterprise has not enabled the cloud disk feature. Online playback or preview is currently not available." message appears, contact your administrator to enable the cloud disk feature and try again. <a href="https://docs.byteplus.com/en/docs/ArkClaw/Claw_cloud_disk?lang=en">Learn more</a>.</div><br><br><br>* <div data-tips="true" data-tips-type="default">When you preview or play a video online, the system will temporarily cache the video to your cloud disk, which may incur small storage fees. <a href="https://docs.byteplus.com/en/docs/tos/docs-product-billing?lang=en">Learn more</a>.</div><br> |
   |**Recording information section** |Includes the file storage path, video recording duration, recording time, file size, resolution, video format, and other information. |
   |**Re\-record** |Click the "Re\-record" button. The system will restart recording without keeping the original file. |
   

7. Click the "Generate prompt" button. The system automatically uploads the recorded video to the cloud and performs intelligent analysis.

   > It takes approximately 30 seconds to complete analysis and extraction. Wait patiently.   
   

8. After prompt generation is complete, the system displays the analysis results. You can perform the following operations based on your actual needs:

   
   <Tabs>
   <Tab zoneid="jwmkB77G" title="Edit prompt">
   <TabTitle>Edit prompt</TabTitle>
   
   If you are not satisfied with the prompt automatically extracted by the system or need to add specific details, you can modify it manually.
   
   
   1. Click the "Edit" button.
   
   2. In the displayed prompt editing panel, you can modify the following parameters based on your needs:
   
      
      |Parameter​ |**Description** |
      |---|---|
      |Task name |Update the name of the task. |
      |Task description |Update the overall textual description of the task. |
      |Prerequisites |Modify the prerequisites required for task execution. |
      |Step management |* Add a step: Click the "+Add step" button to add a new step to the task.<br><br>* Delete a step: At the end of the step that you want to delete, click the <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_6fa959fe0ae35c820818810672b3d6aa.png) </span> button to delete it.<br><br>* Adjust the order: Press and hold the <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_64fdc318c9ee3d16dfdecde486b705ab.png) </span> icon before the step number, and then drag up or down to adjust the execution order of steps. |
      |Expected results |Modify the expected status upon task completion. |
      
   
   3. After you modify the parameters, click the "Save" button to complete the operation.
   
   
   </Tab>
   <Tab zoneid="IWEdHUwx" title="Execute now">
   <TabTitle>Execute now</TabTitle>
   
   Click the "Execute now" button. The system will submit the prompt as an automation task for direct execution on the cloud PC.
   
   
   * Execution process: The system converts the prompt into cloud PC task data. \-\> The system automatically switches to the cloud PC execution mode. \-\> The agent proceeds with step\-by\-step execution.
   
   * Process observability: You can observe the entire execution progress through real\-time VNC video streams. After the execution completes, the system will display the execution result report.
   
   
   </Tab>
   <Tab zoneid="Ffr5vAvO" title="Save as task template">
   <TabTitle>Save as task template</TabTitle>
   
   Click "Save as task template". The system saves the current prompt. Subsequently, you can search for, edit, execute with one click, or delete this task template in the [Task templates](https://docs.byteplus.com/en/docs/394/108409#kUuPkMhj) module at any time.
   
   
   </Tab>
   </Tabs>
   


<span id="kUuPkMhj"></span>
## Manage task templates

The "Task templates" module centrally saves various automated task templates that you previously saved by recording desktop operations and generating prompts. You can search for, edit, execute, or delete saved templates in the "Task templates" module to efficiently reuse tasks.


1. Open your browser, enter the ArkClaw login URL in the address bar, and press Enter.

2. Go to the target ArkClaw page. In the upper\-right corner of the page, click <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_debe1670e9e734dc5913a7e4f591e928.png) </span>.

4. Click "<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_74569899b7883fb9291dc70a8a3e5909.png) </span> \> Task templates".

5. In the pop\-up "Task templates" window, you can view the saved automated tasks and perform the following management operations.

   
   |Actions |Description |
   |---|---|
   |Search for and locate a task |Enter the task name or core keywords in the search box to quickly locate the target task. |
   |Edit a task |1. In the "Actions" column of the target task, click "<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_74569899b7883fb9291dc70a8a3e5909.png) </span> \> Edit".<br><br>2. Change the task content as needed in the "Edit task template" pop\-up window.<br><br>3. After you modify the parameters, click the "Save" button to complete the operation. |
   |Perform task |1. In the "Actions" column of the target task, click the <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_b50c8b6d311825782fa2c57fb2546c8f.png) </span> button. The system will automatically populate the chat box with the task content. You can also make minor adjustments.<br><br>2. On the right of the chat box, click the <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_2331cbe9eda1f210d55abcc14de1277c.png) </span> button to execute the task. |
   |Delete a task |1. In the "Actions" column of the target task, click "<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_74569899b7883fb9291dc70a8a3e5909.png) </span> \> Edit".<br><br>2. In the pop\-up window, click the "Delete" button to complete the operation. |
   


<span id="CFiyfuy9"></span>
## Common issues & troubleshooting

If you encounter any of the following exceptions during recording, refer to the corresponding solutions:


|**Abnormal scenarios** |Cause analysis and solution |
|---|---|
|Cloud desktop disconnected. Recording saved automatically. |* Cause: The cloud desktop connection is interrupted due to network fluctuation or anomaly.<br><br>* Solution: The system has automatically stopped recording and saved content before disconnection. Check your network status, reconnect to the cloud desktop to view extracted prompts, or start a new recording task. |
|Failed to start recording. Try again later. |* Cause: The backend recording service fails to launch properly.<br><br>* Solution: Wait for a while and click the recording button again. If the issue persists after multiple attempts, contact technical support. |
|Insufficient storage space. Free up space first. |* Cause: There is insufficient free disk space to save video files (maximum required space: 200 MB).<br><br>* Solution: Delete unnecessary files in the cloud desktop or relevant directories to free up sufficient storage space, and then restart recording. |
