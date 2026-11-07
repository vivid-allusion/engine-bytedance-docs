---
title: "Using Windows instance logs"
product: "Elastic Compute Service"
product_code: "ecs"
source: "https://docs.byteplus.com/en/docs/ecs/Using-the-log-of-a-Windows-ECS-instance"
---

This topic describes how to use the log feature in a Windows instance, with Windows Server 2012 R2 used as an example.

<span id=".6IOM5pmv5L-h5oGv"></span>
## Background

During operation lifecycle, the Windows operating system records a large volume of logs, such as system logs, security logs, application logs, and application and service logs. Logs contain detailed information about hardware, software, and server issues within the system, as well as event monitoring data. When an operation exception or a security attack occurs in an ECS instance, you can quickly diagnose and find the exception based on log contents. Therefore, you can perform O&M operations for business\-related resources more efficiently.

<span id=".6L-b5YWl5LqL5Lu25p-l55yL5Zmo5p-l55yL5pel5b-X"></span>
## Open event viewer to view logs


1. [Log in to the ECS instance](https://docs.byteplus.com/en/docs/ecs/Using-the-console-to-log-on-to-a-Windows-instance).

2. On the server desktop, click "Start" in the lower left corner, click the drop\-down arrow at the bottom, and open the **Run** application.

3. In the "Run" window, enter the command `eventvwr` to open **event viewer**.

4. There, you can view the following four types of logs:

   * **Application logs**

      In the left navigation pane, click "Windows Logs \> Application" to view the application logs.

      Application logs cover events related to applications installed on the operating system. These events cover errors, warnings, and any information that applications need to report. Application developers can determine which information to report.

   * **Security logs**

      In the left navigation pane, click "Windows Logs \> Security" to view the security logs.

      Security logs cover security\-related events, such as user permission changes, logins and logouts, access to files and folders, and printing activities.

   * **System logs**

      In the left navigation pane, click "Windows Logs \> System" to view the system logs.

      System logs cover system processes, device and disk activities, and events. These events record issues related to hardware, software, and system operations.

   * **Application and service logs**

      In the left navigation pane, expand the "Applications and Services" option, select the needed program, and view its logs.

      Application and service logs cover events from individual applications or components, rather than events that may affect the entire system.


<span id=".5L-u5pS55pel5b-X6Lev5b6E5bm25aSH5Lu95pel5b-X"></span>
## Modify log path and back up logs

Logs are saved to a system volume by default. The default log size is 20 MB. When the log size exceeds 20 MB, the system overwrites previous events by default. You can modify related settings based on needs.

To modify the log path and back up logs, follow the steps below.


1. In the "Event Viewer" window, click "Windows Logs" on the left.

2. In the right\-side list of "Windows Logs", right\-click the target log and then click "Properties".

3. In the "Log Properties" window, you can modify the information of the following properties:

   * Log path

   * Upper limit of log size

   * System operation to be executed​ when the upper limit of the event log size is reached.
