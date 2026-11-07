---
title: "Create and Manage Push Tasks"
product: "BytePlus DataTester"
product_code: "DataTester"
source: "https://docs.byteplus.com/en/docs/DataTester/Create-and-Manage-Push-Tasks"
---

<span id="_1-界面组成"></span>
## 1. Interface composition


* Search push task: You can enter the task ID, push task name, and creation date to search.

* Create a new push task.

* New push experiment: Only DataTester supports it. After clicking, you can jump to the process of creating a push experiment.

* The list contains: task ID, push task name, task type (filterable), creation time, update time, creator (filterable), send scope, task status (filterable), action.

   * Sort display by creating time from near to far.

   * Task type: including single push, routine push, automatic push.

   * Task status: including pending approval, rejected, running, suspended, completed.

   * Send range: including test and formal. Select the test range, and only the users in the "General Settings \- Test Whitelist" will be pushed; select the official range, and the task will be pushed normally; **Note that select "Send range" first, and then "Approval" task, the setting of the sending range can take effect normally.** 

   * Operation: including approval, reject, modification, copy, deletion, suspension, data report, activation.

      * Different task states, different actionables.

      * Different operation items have different permissions for creators, administrators, and group administrators.

* Support page turning.


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/7963b37131254481a37a7d1ac352b617~tplv-goo7wpa0wc-image.image) </span>

<span id="_2-新建推送任务"></span>
## 2. Create a new push task

The push task is divided into manual push and automatic push, among which manual push is divided into single push and routine push. The meaning of each push mode is as follows, and you can choose it on demand.


* Single push: "push immediately" or "push regularly" to the circled target user

* Routine push: "Timed cyclic push" to the circled target user

* Automatic push: Set the push time based on the event and time, and push the crowd that meets the push time


<span id="_2-1-推送目标"></span>
### **2.1 Push target**

Click "+ New Push Task" on the interface above, and select Manual Push or Automatic Push.


* Push task name: Set the task name, which cannot be repeated within the same application

* Push crowd:

   * All users: active users in the last 90 days (active users are defined as those who actively trigger any events)

   * User grouping: Only "manual push" is supported. The saved user grouping will intersect with "active users in the last 90 days" by default.

   * Segmented users: circle users according to time, events, and attributes. The logic is the same as the "user grouping" module, and will intersect with "active users in the last 90 days" by default.

* Push platform: only "manual push" support, support setting push platform to all, Android, iOS


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/44a7be72b70c4b17aa3364dd0e6a6c9f~tplv-goo7wpa0wc-image.image) </span>

<span id="_2-2-推送时机，仅「自动推送」支持"></span>
### **2.2 Push timing, only "automatic push" support**

The push timing setting is divided into two stages. The first stage is for the user to trigger certain behaviors, and the second stage is for the user's follow\-up actions. Users who meet the two\-stage conditions will run the push action.


* Phase 1: Users trigger certain behaviors that can be divided into three categories, broken down as follows.

   * Trigger a single action: a condition is satisfied when a user performs an action

   * Trigger multiple behaviors: The user completes the "setting behavior" in any order within the "setting time" and reaches the "setting number of times", which means the condition is met

   * Trigger multiple actions in sequence: The user completes the "setting actions" in sequence within the "setting time", which means the condition is met

* Phase 2: The user's follow\-up actions can also be classified as follows.

   * Wait for a period of time: After the first\-stage conditions are met, wait for the "set time" to meet the conditions

   * No specific behavior is triggered: After the first\-stage conditions are met, the "setting behavior" is not triggered within the "setting time", which means the condition is met

   * Trigger a specific behavior: After the first\-stage conditions are met, the "setting behavior" is triggered within the "setting time" to meet the conditions


You can set a deadline for automatically pushing tasks. If you don't choose it, it will start from the time the task was created by default and end after 365 days.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/e8b1931c1c124bfe8722c7d6dafdfa7e~tplv-goo7wpa0wc-image.image) </span>

<span id="_2-3-推送动作"></span>
### **2.3 Push action**

It is divided into setting push content and task settings, among which push content will distinguish between AppPush and Webhook;

<span id="_2-3-1-apppush推送内容"></span>
#### 2.3.1 AppPush push content

It mainly includes selecting the channel, the push configuration of the selected channel, and testing the user preview. Of which,


* Select channel: Support three channels: JPush, GeTui, and Umeng. You need to correctly configure the corresponding channel in the "Push Channel Management" to push.

* Push configuration of channels

   * **JPush**

      * Push title: the title of the message.

      * Push content: the content of the message.

      * Corner mark number increase: Corner mark number increase value, this field is currently only valid for Huawei EMUI 8.0 and above, Xiaomi MIUI 6 and above equipment; if this field is not filled in, it means that the corner mark number will not be changed (Xiaomi equipment due to system control, regardless of whether it is pushed through the JPush channel or the manufacturer channel, even if it is not delivered, it is still the default + 1 effect.); It is recommended to configure it to 1; for example: this field is set to 1, and the number of corner marks before application is 2. After sending this corner mark message, the number of corner marks in the application is displayed as 3.

         * Android application entrance: The application entrance activity class corresponding to the desktop icon, such as "com.test.badge. MainActivity", **Only Android push needs to be configured and effective, and needs to be used together with the corner mark number.** 

      * Follow\-up action

         * Launch the app: It will be sent with a **notification message** (including message title and content).

         * Custom behavior: It will be delivered as a **notification message** (including message title, message content and custom key, value) + **passthrough message** (including message title, message content and custom key, value). **The transparent message will not be displayed on the notification bar, and the message content will be transparent to the App, which needs to be handled by the App itself.** 

            * Password message: Custom key and value can be set. After pushing notification to the client side, this part of the message can be obtained through the JPush SDK.

            * Transfer to manufacturer notification: Custom message transfer to manufacturer notification, for Android devices, if the APP long connection is not online, the message cannot be delivered in time, and can be displayed in the form of **manufacturer notification** through the manufacturer channel to remind users in time. **Only Android system is supported, and a JPush VIP account is required.** 

               * uri_activity: specify the jump page; this field is used to specify the activity that the developer wants to open, and the value is the "android: name" attribute value of the activity node; it is suitable for Huawei, Xiaomi, and vivo manufacturers channel jump.

               * uri_action: specify the jump page; this field is used to specify the activity that the developer wants to open, the value is the "android: name" attribute value of the "activity" \- "intent\-filter" \- "action" node; adapt to oppo, fcm jump.

      * More options

         * Android

            * Reminder: Notification reminder method.

            * Priority: Notification bar shows priority.

            * You can set the APP to still display reminders when it is in the foreground.

         * iOS: Support to select production environment or development environment, the default push production environment; APNs production and development certificates can be configured in the JPush console, and the message will be pushed using the selected environment.

* **Push**

   * Follow\-up actions:

      * Open the application homepage: **Click Notification to open the application template, support notification messages**

         * Push title: the title of the message.

         * Push content: the content of the message.

         * More options

            * Android

               * Reminder: Notification reminder method.

               * The importance of notification channels: different importance has different display formats.

               * Notification can be cleared.

            * iOS

               * Increase in the number of corner marks: After sending the message, the increase in the number of corner marks is recommended to be set to 1.

      * Custom action: **Custom message template, support notification message + passthrough message.** 

         * Description

         * Pass\-through message: Set the pass\-through message key and value, the **pass\-through message will not be displayed on the notification bar, the message content will be passed to the App, and the App needs to handle it by itself.** 

         * More options

            * Push Title: The title of the notification message \*\* (the notification message will be sent from the vendor channel) \*\*

            * Push content: the content of the notification message.

            * Android

               * Vendor notification type

                  * Intent: Click on the notification to open the application\-specific page, the intent format must be correct and not empty, length ≤ 4096; example: intent: #Intent; component = your package name/full path of the activity you want to open; S.parm1 = value1; S.parm2 = value2; end Reference: [a push document center](https://docs.getui.com/getui/mobile/vendor/androidstudio/?id=doc-title-5).

                  * URL: Click the notification to open the link, the length is ≤ 1024.

            * iOS

               * Increase in the number of corner marks: After sending the message, the increase in the number of corner marks is recommended to be set to 1.

   * Keep offline messages: Set whether to push offline as well.

   * Keep offline message expiration time: Messages are stored offline for a valid period.

* **Friendly alliance**

   * follow\-up action

      * Open the app: **Notification message template, support notification message**

         * Push title: the title of the message.

         * Push content: the content of the message.

         * More options

            * Android

               * Reminder: Notification reminder method.

            * iOS

               * Reminder: Notification reminder method.

               * Increase in the number of corner marks: After sending the message, the increase in the number of corner marks is recommended to be set to 1.

               * silent push

      * Custom action: **Custom message template, Android supports transparent message, iOS supports notification message + transparent message.** 

         * Description

         * Pass\-through message: Set the pass\-through message key and value, the **pass\-through message will not be displayed on the notification bar, the message content will be passed to the App, and the App needs to handle it by itself.** 

         * More options

            * iOS

               * Reminder: Notification reminder method.

               * Increase in the number of corner marks: After sending the message, the increase in the number of corner marks is recommended to be set to 1.

               * Push Title: The title of the notification message \*\* (the notification message will be sent from the APNs channel) \*\*

               * Push content: the content of the notification message.

               * silent push

   * Keep messages offline: whether to set a message expiration time.

   * Keep offline message expiration time: Set the message expiration time, the default is 72 hours.

* Test user preview: Fill in the caliber id of the test user (enter uuid in the webhook channel), and send a preview message.


<span id="_2-3-2-webhook推送内容"></span>
#### 2.3.2 Webhooks Push Content

It mainly includes channel selection, parameter configuration, and test user preview, in which the parameter configuration items correspond to the settings of the selected channel in "Push Channel Management".

<span id="_2-3-3-任务设置"></span>
#### 2.3.3 Task Settings


* Task type: **manual push support only**

   * Single push

      * Push time: immediate push, regular push (date, hour, minute can be set, and the push will start at the time)

   * Routine push

      * Cycle: You can set daily, weekly, monthly fixed times, as well as the start and end times of the cycle


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/03a8e891dda34f438066a551c523c5b8~tplv-goo7wpa0wc-image.image) </span>


* Frequency control rules:

   * Global frequency control: The default frequency control is that each user receives up to 20 Pushes within 1 day, and up to 1 Push per hour, which can be modified on the "General Settings" page.

   * Not subject to frequency control: 1 user may receive multiple pushes in 1 day.

* Task participation restrictions: **Only auto\-push support**, setting whether to allow users to enter again after completing the task. If this item is turned on, the same user may be reached multiple times.


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/faf8c453773f4bf79f03ec3fb23b5654~tplv-goo7wpa0wc-image.image) </span>

After filling in the above content, you can click "Submit", jump to the push task management page, the task enters the pending approval state, and will not be pushed. **Select the correct sending range** , after the administrator approves, the task will enter the running state and be pushed normally

<span id="_2-4-多任务分流"></span>
### 2.4 Multitasking offloading

Combine push capability and AB test to support a push task with different push copy settings. When setting up tasks, click the plus sign in the image below to create multiple experimental groups (up to 5 tasks are supported), and push policies are supported. There are three types of push strategies:


* Multitasking offloading (supports all push task types)

* Task horse racing (supports single push, automatic push, process canvas)

* Dynamic task horse racing (support routine push, automatic push, process canvas)


<span id="_2-4-1-多任务分流"></span>
#### 2.4.1 Multitasking

Applicable scenarios are judged by human experience or have been pre\-verified, and there are relative differences in different task configurations, but the number of users is relatively small, and the A/B experiment is not easy to draw confidence conclusions. At this time, different experimental groups are assigned different traffic ratios. For example:


* Experimental group 1: The human judgment effect was relatively good, and 70% of the traffic was allocated.

* Experimental group 2: The human judgment effect may be worse than copy 1, and 30% of the traffic is allocated.


<span id="_2-4-2-任务赛马"></span>
#### 2.4.2 Mission house\-racing mechanism

When it is impossible to determine which experimental group configuration works better, multiple experimental groups can be set, and a certain experimental traffic ratio can be set, such as 10%, so that multiple tasks will be **evenly divided** The 10% experimental traffic is pushed at the specified experimental traffic push time; after the experimental traffic is pushed for a period of time, the system selects the indicator according to the set "preferred indicator" data **The optimal** experimental group, that is, the preferred group, and the remaining 90% of the traffic is pushed to the preferred group configuration (the preferred group push time can be set relative time or absolute time, and the time interval with the push time of the experimental traffic is preferably 4 **hours or more** , so that the system can draw an accurate conclusion).

<span id="_2-4-3-动态任务赛马"></span>
#### 2.4.3 Dynamic Mission Racing

In order to **reduce the experimental cost and support the task horse racing in the cyclic push scenario**, the dynamic task horse racing strategy realizes the overall optimal distribution ratio of copywriting traffic. When the first push, the system **divides** the traffic according to the number of experimental groups configured. From the second push, a higher proportion of traffic will be dynamically allocated to the experimental group with higher indicators in the push. It can be understood that the traffic allocation ratio is proportional to the indicator value.

<span id="_3-任务操作"></span>
## 3. Task operation


* **View**


You can click "Operation\-View" to view the configuration content of the push task.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/abf63d4edefd428eb4fc9fc8223a8549~tplv-goo7wpa0wc-image.image) </span>


* **Copy**


You can click "Operation\-Copy" to copy the corresponding push task.


* Copy task name will add " (copy) " suffix

* The replication task is pending approval


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/491e05d6519649578bc4fb34a5f93f67~tplv-goo7wpa0wc-image.image) </span>


* **Modify**


**Tasks with the status "Completed" do not support modification, and tasks with other states can be modified** \*\*, the running tasks need to be suspended before modification \*\* **；**  You can click "Operation\-Modify" to modify the push task


* The previous task configuration can be modified

* After modification and submission, the task will re\-enter the pending approval state and will not be pushed. After administrator approval, the task will enter the running state and be pushed normally.


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/748e5d204329445687c129a586850a1f~tplv-goo7wpa0wc-image.image) </span>


* **Delete**


\*\* Only the creator, administrator, and group administrator can delete the task, and it cannot be restored after the task is deleted; \*\* You can click "Operation\-Delete" to delete the push task;


* After deletion, the push task stops working, and subsequent pushes will no longer be carried out; ongoing pushes will also stop, and the stop process will last for a few minutes.

* The task is cleaned up, and the subsequent task list no longer displays the task


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/c4b9a682d22b4a89ab8ef7df47e31bf2~tplv-goo7wpa0wc-image.image) </span>


* **Pause, activate**


\*\* Only the creator, administrator, and group administrator can activate the task; \*\* You can click "Operation \- Pause/Activate" to pause or activate the push task.


* Pause: After the pause, the ongoing push of the current task and subsequent pushes will all stop, and the task status will be changed to Pause.

* Activation: After activation, the current task is running normally, and the task status is changed to running.


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/64d17eabe89940bda3068f62d1dd825a~tplv-goo7wpa0wc-image.image) </span>


* **Approval, reject**


**Only administrators and group administrators can approve or reject tasks.**  You can click "Action\-Approval/Reject" to approve or reject push tasks.


* Approval: After approval, the task status changes to Running

* Rejected: After rejection, the task status becomes rejected, and the rejected task can be viewed and modified to initiate the next approval.


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/b9ba33b264054985953be129c5c6ca4a~tplv-goo7wpa0wc-image.image) </span>

<span id="_4-不同任务状态说明"></span>
## 4. Description of different task status


* Pending approval: The task setting/modification is completed, but it does not run. After approval, the task needs to run and be pushed.

* Rejected: The task is not running, the task configuration needs to be modified, and the approval is restarted.

* Running: The task is running, pushing according to the task configuration, and counting data.

* Pause: The task is not running for the time being. You need to "activate" and restart the operation and push it.

* Completed: The task will no longer continue to run and push, and the statistics will proceed normally.


<span id="_5-数据报表"></span>
## 5. Data reports


* You can click "Operation \- Data Report" to enter the data report page.


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/4f8ebae63bbc417fae1d8b160ae652c8~tplv-goo7wpa0wc-image.image) </span>

The push data report is as follows:


* Data statistics range: Time support Select "after startup" to date/7 days/30 days, the last x days, and select the time range. The data is displayed on a day\-by\-day basis.

* Analysis chart: A data overview of the push effect, displayed as a bar chart/line chart; the card above the chart shows the most recent day's metrics.

* Detailed data: Display statistics in a table, support download.

* Statement indicator description:

   * Scheduled Triggers: Number of Pushes Scheduled to Send.

   * Actual reach: the number of pushes actually delivered.

   * Clicks: The number of push clicks by users.

   * Number of successful deliveries: Number of successful deliveries.

   * Arrival rate:the actual number of people reached/successful number of people sent.

   * Click through rate: click through/actual reach.


Note: There is sometimes a discount between the planned triggering number and the successful sending number. The reason is that before calling the channel interface for actual sending, it may be filtered out for various reasons: such as triggering frequency control, pushing user information verification fails, etc.; Second, it is intercepted by the channel and the call channel interface fails to return and is not sent.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/146e968259344fe9943cf4bcae94fe71~tplv-goo7wpa0wc-image.image) </span>


* Webhook data report (webhook report is different from other channel reports: it shows the indicators of successful delivery, but does not show indicators such as arrival and click, which will be supported later).

   * Scheduled Triggers: Number of Pushes Scheduled to Send.

   * Number of successful deliveries: Number of successful deliveries.

   * Successful sending rate: successful sending/scheduled triggering.


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/1e51adf07c644dbbbc12f37e46e94182~tplv-goo7wpa0wc-image.image) </span>


* Multitasking/Task Racing Data Report

   * Task 1, Task 2... Corresponding to the experimental group 1 and experimental group 2 set in the push task...

   * The drop\-down box supports the selection of different metrics: "Planned trigger visits, actual touch visits, click hits", and "Arrival rate and click through rate". The meaning of the metrics is the same as above.


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/1fb51a2626f3402893bb8110a5c23ae8~tplv-goo7wpa0wc-image.image) </span>
