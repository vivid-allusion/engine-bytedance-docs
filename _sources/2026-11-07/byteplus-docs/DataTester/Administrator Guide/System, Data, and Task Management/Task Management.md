---
title: "Task Management"
product: "BytePlus DataTester"
product_code: "DataTester"
source: "https://docs.byteplus.com/en/docs/DataTester/Task-Management"
---

DataTester provides you with task management functions. You can set up and manage global experimental indicator calculation tasks on the task management page. This article introduces you to the operational essentials of the task management function.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">The task management page provides you with the setting, query, management and other operations of the global experiment\-related tasks. The current privatized 4.9.2 version has launched the global task function, and other sub\-functions will be launched one after another. Please look forward to it.</div>


<span id="c6ea1d78"></span>
# Global task

<span id="d59eee2d"></span>
## Application scenario

The global task page can set the trigger time and task execution switch of the global experimental indicator calculation task. After setting:


* The indicator calculation tasks that do not require analysis can be closed, saving computing resources, avoiding task queues due to insufficient computing resources, and generating more valuable indicator results too late.

* The trigger time of the relevant task can be set to avoid the inaccurate data of the indicator result due to the fact that the data output time relied on by some experimental indicators is later than the default indicator calculation task time.


<span id="1647c8ce"></span>
## Precautions


* Permission requirements: Only group administrators can modify global task settings.


<span id="ea5ca993"></span>
## Operation steps


1. After logging in to the DataTester console, click **Global Settings** \> **System Settings** \> **Task Management** in the left navigation bar to enter the task management page. In the **Global Task** tab, click the Edit button to modify the trigger time and task switch of the global task.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/69fda964c3b74c8484e2fb95f289fb94~tplv-goo7wpa0wc-image.image) </span>

2. Modify the global task configuration and click OK when finished.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/a53c9bf1559f46dd8f9e4f46c3d595ea~tplv-goo7wpa0wc-image.image) </span>

   * Modify the task trigger time: Click the task trigger time selection button on the left to modify the settings according to the business data output time. If your experiment relies on the output of some business data, set the task trigger time to the time after the output of the business data.

   * Modify the indicator task switch: According to the actual demands of the experimental analysis, turn off the useless indicator tasks, which can save the indicator calculation resources, avoid too many calculation tasks, and produce more valuable indicator results too late.
