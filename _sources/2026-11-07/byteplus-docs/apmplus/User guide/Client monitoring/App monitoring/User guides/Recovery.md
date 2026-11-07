---
title: "Recovery"
product: "Application Performance Management Plus"
product_code: "apmplus"
source: "https://docs.byteplus.com/en/docs/apmplus/Recovery"
---

Recovery supports both log recovery and custom recovery. By printing a custom log and a business custom file, it helps with single point tracing and locating problems.

When log files are encrypted and compressed locally, the operating system's mmap mechanism is used to ensure efficient log writing. The system also supports writing log files according to log levels.

<span id=".5L2_55So5Zy65pmv"></span>
## Application scenarios


* Enable the log recovery feature during initialization. The business logic prints custom logs using a specified class, and the logs are saved to the local disk.

* Log queries report performance and interaction data through sampling, and the sampling rate is generally low. As a result, when troubleshooting issues, the corresponding log cannot be found. To address this issue, the SDK provides a built\-in APMPlus log and uses custom log to collect all core data and store it locally. You can obtain logs using recovery to assist in analyzing performance issues when no user data is available and special exit issues.


<span id="eab35712"></span>
## Usage Limits

The modules supported by APMPlus log are listed below:


* Android client

   * Interaction: startup log, page load, user session duration, network analytics, event.

   * Stability: application exit, custom exception, crash, Dart exception.

   * Performance: CPU, memory

* iOS platform

   * Startup time, page load time, network latency, event tracking, custom exception, CPU metric, memory metric, FPS, and frame loss.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">The Harmony operating system only supports the <strong>custom log</strong> type and does not support APMPlus log.</div>


<span id="51d1f0aa"></span>
## Task trigger condition

If any of the following conditions is met, the recovery task will be triggered:


* The network is good. Restart the app.

* Network is good; you can switch between foreground and background states.

* When the network is stable and the app remains running, periodic triggers will occur at intervals of up to five minutes.


<span id="0a9727ef"></span>
## Log recovery

<span id="a4c83fb4"></span>
### Prerequisites


* Log recovery has been integrated. For iOS, refer to [log recovery](https://docs.byteplus.com/en/docs/apmplus/Report_verification_data#5e60c23f); for Android, refer to [log recovery](https://docs.byteplus.com/en/docs/apmplus/Use_advanced_features_Android#1dc51677); for Harmony, refer to [recovery](https://docs.byteplus.com/en/docs/apmplus/Report_verification_data_Harmony#f1c76fdc).

* Crash analytic has been configured. For details, please refer to [SDK setting](https://docs.byteplus.com/en/docs/apmplus/SDK_reporting_configuration).


<span id=".5paw5bu65Lu75Yqh"></span>
### Create a log recovery task


1. Log in to the [Application Performance Management Plus console](https://console.byteplus.com/observe/apmplus-client).

2. On the top navigation bar, select the target region.

3. In the left\-side menu, select **Client Monitoring**, then locate and click the target application name.

4. Click **App Monitoring** under the target application.

5. In the upper left corner of the console, select **All features \> Recovery**, and then click  **"Create task"** .

6. On the **Create task** page, complete the following configuration, and then click **Save**.

   
   |**Configuration area** |**Parameters** |**DescriptionS** |
   |---|---|---|
   |Basic information |Task name |A custom name used to identify this task. |
   ||System |Select an operating system. It supports Android, iOS, and HarmonyOS. |
   ||Task descriptions |Enter the task description, for example, its usage scenario. |
   |Task configurations |Recovery types |Select recovery type: log recovery.<br><br>Log recovery is custom logs printed on the recovery end. |
   ||log type |* APMPlus log: Log data on exceptions, performance, network, events, and more collected by the built\-in instrumentation of the APMPlus SDK<br><br>* Custom log: Log data instrumented by the business itself<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">When creating a log recovery task for the Harmony operating system, only the custom log type is supported.</div><br> |
   ||Time range for data retrieval |The configuration must specify the time range for retrieving log files. |
   ||Select device |The configuration must specify which device's log file to retrieve. Support setting the target device based on **DID** and **UID**.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">The values of DID and UID should be consistent with the SDK configuration used during initialization.</div><br> |
   |Notification configurations |Lark webhook |If you want to receive a Lark message notification when the task is completed, please enter the Lark webhook.<br><br>Only supports adding one address. |
   ||WeCom webhook |To receive a WeCom notification when the task is completed, enter the WeCom webhook.<br><br>Only one address can be added. |
   ||DingTalk webhook |If you want to receive a DingTalk message notification when the task is completed, please enter the DingTalk webhook.<br><br>Only one address can be added. |
   ||Email notification group |If you want to receive an email notification when the task is completed, select the target recipient group from the dropdown list. You can also create a recipient group and add email addresses.<br><br>You can add multiple email addresses in the receiving group. |
   


<span id="08cac45b"></span>
### View custom logs


1. Log in to the [Application Performance Management Plus console](https://console.byteplus.com/observe/apmplus-client).

2. On the top navigation bar, select the target region.

3. In the left\-side menu, select **Client Monitoring**, then find and click the target application name.

4. Click **App Monitoring** under the target application.

5. In the upper left corner of the console, select **All features \> recovery**.

6. On the **recovery** page, find the target task name in the task list, then click **task details**.

   * Device: If multiple users are fetched at once, you can filter different users by device.

   * Task information: Displays an overview of task information, including task name, creator, execution time, task progress, recovery scope, and other task information.

   * Log list:

      * Supports filtering logs by time, log keywords, log level, and log type.

         <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="3">tip         </div>
         

         <div data-tips="true" data-tips-type="tip" data-wrapper-indent="3">Harmony system logs recovery only supports the <strong>business log</strong> type.         </div>
         

      * Supports online viewing of logs and allows log files to be downloaded to the local machine.


<span id="01a3f55f"></span>
## Custom recovery

<span id="1d822874"></span>
### Prerequisites


* Custom recovery has been integrated. For iOS, refer to [custom recovery](https://docs.byteplus.com/en/docs/apmplus/Report_verification_data#601121a2); for Android, refer to [custom recovery](https://docs.byteplus.com/en/docs/apmplus/Use_advanced_features_Android#f076a974).

* The custom file has been configured. Refer to [SDK setting](https://docs.byteplus.com/en/docs/apmplus/SDK_reporting_configuration) for details.


<span id="a5d4bd06"></span>
### Create a custom recovery task


1. Log in to the [Application Performance Management Plus console](https://console.byteplus.com/observe/apmplus-client).

2. On the top navigation bar, select the target region.

3. In the left\-side menu, select **Client Monitoring**, then locate and click the target application name.

4. Click **App Monitoring** under the target application.

5. In the upper left corner of the console, select **All features \> recovery**, and then click **Create task**.

6. On the **Create Task** page, complete the following configuration, then click **Save**.

   
   |**Configuration area** |**Parameters** |**DescriptionS** |
   |---|---|---|
   |Basic information |Task name |A custom name used to identify this task. |
   ||System |Select an Operating System.<br><br><br>* Android and iOS operating systems support the creation of custom recovery tasks.<br><br>* The Harmony operating system does not support creating custom recovery tasks. |
   ||The task description |Enter the task description, for example, a usage scenario for this task. |
   |Task configuration |Recovery types |Select recovery type: custom recovery.<br><br>A custom recovery command is issued for business configuration. After receiving the command, the business returns a custom file, which the platform can download to troubleshoot issues. |
   ||Recovery parameters |Configure recovery parameters. For details, refer to [iOS custom recovery configuration](https://docs.byteplus.com/en/docs/apmplus/Report_verification_data#601121a2) and [Android custom recovery configuration](https://docs.byteplus.com/en/docs/apmplus/Use_advanced_features_Android#f076a974).<br><br>Input on Android only supports the JSON format, and SDK integrators are responsible for implementing their own code parsing. |
   ||Select a device |The configuration specifies which device's log file needs to be retrieved. Set the target device based on **DID** and **UID**.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">The values of DID and UID should be consistent with the SDK configuration used for initialization.</div><br> |
   |Notification configurations |Lark webhook |If you want to receive a Lark notification when the task is completed, please enter the Lark webhook.<br><br>Only one address can be added. |
   ||WeCom webhook |If you want to receive a WeCom notification when the task is completed, please enter the WeCom webhook.<br><br>Only one address can be added. |
   ||DingTalk webhook |If you want to receive a DingTalk notification when the task is completed, please enter the DingTalk webhook.<br><br>Only one address is supported. |
   ||Email notification group |If you want to receive an email notification when the task is completed, select the target recipient group from the dropdown list. You can also create a recipient group and add email addresses.<br><br>You can add multiple email addresses to the receiving group. |
   


<span id="a01a6a8e"></span>
### View a custom file


1. Log in to the [Application Performance Management Plus console](https://console.byteplus.com/observe/apmplus-client).

2. On the top navigation bar, select the target region.

3. In the left\-side menu, select **Client Monitoring**, then find and click the target application name.

4. Click **App Monitoring** under the target application.

5. In the upper left corner of the console, select **All features \> recovery**.

6. On the **recovery** page, find the target task name in the task list, then click **task details**.

   * Device: When retrieving multiple users at once, you can filter different users by device.

   * Task information: Displays the task summary and custom log. The custom log can be viewed online or downloaded for local analysis.

   * Recovery content:

      * Recovery file`common_params.txt`: The basic parameter file on the device

      * Recovery file`files-cloudMsg.zip`: File returned by the client\-side service

      * String: recovery content returned by client\-side business logic


<span id="5f6f95ea"></span>
## View task list

<span id="be93c60c"></span>
### List descriptions

After creating a task, you can view the tasks currently being executed in the list.

The task list displays the task name, log type, creator, creation time, and task progress.


* **Task progress**: Indicates the status of the current task.

   * **Completed**: Click **Task details** to view detailed log information to analyze problems.

   * **Failure**: Failed to obtain log. The details page contains the specific reason for the failure.

   * **Not issued**: Indicates a status where the app has not yet retrieved the command.

* **Task details**: Click to go to the **Task details** page to view task information and log list.

* **Create a copy**: Click to enter the **Create task** page, edit the new task using the configuration of the original task as a template, and then generate a new task.

* **Edit**: Click to enter the **Edit Task** page, and edit the original task using its existing configuration.

* **Delete**: Delete this log recovery task.


<span id="a1088ffe"></span>
### Troubleshooting exceptions

If the task remains in the unissued status, it may be caused by a mismatch between the SDK reporting parameters and the log recovery settings. Please perform the following steps to troubleshoot:


1. Check whether the UID/DID in the console and SDK setting are consistent.

   On the **log recovery** page, click **task details**, and check whether the device has an identifier.

   * DID: Without an identifier, it is displayed as *device name*.

   * UID: With identifier, displayed as *device name* (uid).

      Compare the UID/DID set in the console with those in the SDK to check for consistency:

   * Consistency: Please execute Step 2.

   * Inconsistent: Please modify to ensure consistency before executing Step 2. Modify the SDK configuration, refer to [How to configure DID and UID in the SDK?](https://docs.byteplus.com/en/docs/apmplus/How_to_configure_DID_and_UID_in_the_SDK).

2. Use packet capture to confirm whether the device values displayed on the console match the SDK configuration.

   Packet capture path: https://apmplus.volces.com/monitor/collect/c/cloudcontrol/get.

   Compare the UID and DID carried by the request in the captured packet information with those in the console for consistency:

   * Consistent: Task progress is still **unreported**. Please submit a ticket for feedback.

   * Inconsistency: Edit or modify on the **log recovery** page, or modify the SDK configuration.

      Modify the SDK configuration, refer to [How to configure DID and UID in the SDK?](https://docs.byteplus.com/en/docs/apmplus/How_to_configure_DID_and_UID_in_the_SDK).
