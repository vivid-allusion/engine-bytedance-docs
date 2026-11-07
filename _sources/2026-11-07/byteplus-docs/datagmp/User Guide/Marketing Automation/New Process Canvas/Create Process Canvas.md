---
title: "Create Process Canvas"
product: "Byteplus GMP"
product_code: "datagmp"
source: "https://docs.byteplus.com/en/docs/datagmp/Create_Process_Canvas"
---

To address the issue of a high entry barrier on the current process canvas and dense information in strategy forms, BytePlus has iterated the "New Process Canvas" in version V6.3. This allows the arrangement of process canvases through atomic components, enhancing the operating experience. **Historical version users will not automatically have this feature enabled after upgrading; contact BytePlus service personnel to enable it.**  **If a process canvas was created in a historical version, enabling this feature will mean new tasks use a new interaction style, while viewing historical tasks will use the original interaction style.** 

<span id="da1d9fe8"></span>
## **1. Usage Restrictions**


| **[ 📢 Prerequisites for using this feature ]**  ||
|---|---|
|System Integration |**If BytePlus's VeCDP or Datafinder are not purchased, technical implementation staff must complete interface integration before usage.**  |
|**Activate GMP Permission** |The administrator activates the permission to create tasks, Permission path: Activate permission in GMP "Process Canvas \- New/View/Edit/Delete" |
|**Activate Segment Permission** |There are 3 scenarios for activating segment permission:<br><br>If VeCDP is purchased, permissions need to be activated in VeCDP "User Segment \- Private Domain Segment \- View/Add/Delete/Modify Segment", and once activated, the segment function in task creation can be used.<br><br>If VeCDP is not purchased and only Datafinder is purchased, permission needs to be activated in Datafinder "User Segment", and once activated, the segment function in task creation can be used.<br><br>If neither VeCDP nor Datafinder is purchased, this permission can be ignored. |


<span id="e99191a8"></span>
## **2. Basic Information Settings**

Open the process canvas page: Marketing Strategy \- Process Canvas, then click "Add Flow Canvas". You can use an empty process canvas for creation, or you can use a template.

<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/4e5ebd464c3d4a28bfd8ea190787d93c~tplv-goo7wpa0wc-image.image" width="439px" /></div>


<span id="78ff222d"></span>
## **3. Canvas Design**

Canvas design is used to arrange the processing logic at each step of the process canvas.

**Scheduled: Configuration of Triggers**

First, configure the "triggers", which determine when and which users can enter this canvas through settings. The system supports four ways to enter the process:


* **Scheduled \- One\-Time**: Mainly used to create a one\-time execution process where users enter the process at a set time.

* **Scheduled \- Repeated**: Mainly used to create recurring execution processes, where users enter the process at one or several fixed times each cycle, such as 10 AM daily in March, or 4 PM every Friday in April.

* **Event\-Triggered: Completion of Event A**: Activates the process when a user completes an action (immediate/delayed), such as triggering a points deposit reminder when a user completes actions like post saving/liking/sharing. During the task's valid timeframe, meeting the trigger conditions can activate the process multiple times.

* **Event\-Triggered: Event A Completed & Event B Incomplete**: Creates an event\-triggered task that activates the process if the user completes an action A and does not complete another action B within a specific time after, like not visiting a page within 20 minutes after launching the app triggers the process execution. Commonly used for interruption marketing.


<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/dddbfc546ced4568981e5a21748f1c39~tplv-goo7wpa0wc-image.image" width="1920px" /></div>


 **(1) Meaning of the field Scheduled \- One\-Time**


|Field |Meaning and Purpose of the Field |
|---|---|
|**Task Start Time** |Required. This field represents the start time for running this process canvas. |
|**Task end time** |Required. After reaching the "Task end time," the process canvas status becomes completed, and all logic flows of the process canvas will no longer execute. |
|**Approval timeout** |Required. If the task has not been approved by the “reach time,” you can choose to cancel the task, or approve it and execute immediately. Even if "Execute immediately after approval" is selected, if the approval is not completed within 72 hours, the task will be automatically cancelled. |


<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/2f47679fc04c4a25a7d9c864b1f2c732~tplv-goo7wpa0wc-image.image" width="1257px" /></div>


 **(2) Scheduled \- Repeated: Meaning of Fields**


|Field |Field Meaning and Purpose |
|---|---|
|**Task Cycle Period** |Mandatory. This field represents the time to start running the process canvas for each cycle period. |
|**Task End Time** |Mandatory. Upon reaching the "Task End Time," the status of the process canvas changes to completed, and all process canvas workflow logic ceases. |
|**Enter Frequency Limit** |Scheduled \- Repeated process canvas, where a user may enter the process multiple times. This feature restricts the frequency of each user entering the process to avoid overly disturbing the user. The settings are only effective for the current process canvas, and each successful entry into the process (regardless of whether the customer is reached or not) reduces the frequency control quota by one. |


<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/62df7d721dc547dd8e09f40d33cc5d56~tplv-goo7wpa0wc-image.image" width="1256px" /></div>


 **(3) Event\-Triggered: Completion of Event A: Meaning of Fields**


|Field |Field Meaning and Purpose |
|---|---|
|**Event Description** |Required. This field is used to describe the event and is only applicable in the preview and view of the process canvas, without affecting the outreach to users. |
|**Event A Start and End Time** |Mandatory. The events of A occurring during this period will trigger the process. |
|**Trigger Event** |Required.<br><br>**After the user completes a certain event, this process is triggered**, and users who complete the event will be filtered based on the "target audience", only those who meet both "trigger condition + target audience" will actually proceed with the engagement.<br><br><span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/c5e75f834c9543cba1a1723a90c0ca3b~tplv-goo7wpa0wc-image.image) </span><br><br>**Accumulative completion of A / Each completion of A / Completed separately**<br><br><br>* Accumulating 3 completions of Event A means that the user will enter the process only once after completing the event.<br><br>* Each completion of 3 occurrences of Event A means that the process will be triggered every time the user completes Event A three times.<br><br>* Completed separately means that after completing an event, the user will only be reached once. Separate events completed can have configurable AND/OR relationships, and the number of each event can also be configured individually.<br><br><br>**How to select GMP\-related events:** <br><br>In the event box, search for "GMP" to query GMP events, which are usually named "GMP Response", and all actions of GMP message delivery and process canvas are included in this event.<br><br>After selecting the event, the system will automatically load three attribute options that need to be filled in manually:<br><br><br>* Activity type/task type: Whether the GMP event that needs to be triggered is for message delivery or process canvas.<br><br>* Campaign ID/Task ID: The task ID corresponding to the GMP event that needs to be triggered.<br><br>* Indicator Name: Refers to the name of the metric that corresponds to the event needed to trigger in GMP, such as "sending volume" or "successful delivery volume" for successful dispatches. |
|**Task end time** |Mandatory. After reaching the "Task end time," the state of the process canvas becomes ended, and all logic flows of the process canvas are no longer executed. |
|**Enter rate limiting** |Event\-Triggered: Completion of Event A process canvas; a user may enter the process multiple times. This feature limits the frequency of each user entering the process to avoid excessive disturbances. The setting is only effective for the current process canvas; each successful entry into the process (irrespective of whether it reaches the user, as long as it successfully enters), reduces the rate control quota by 1. |


<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/28ac388999fc4302ad61fd1a93887b8d~tplv-goo7wpa0wc-image.image" width="1920px" /></div>


 **(4) Event\-Triggered: Event A Completed & Event B Incomplete: Meaning of Fields**


|Field |Meaning and purpose of the field |
|---|---|
|**Event Description** |Mandatory. This field is for describing the event and is only used in the preview and view modes of the process canvas, without affecting user outreach. |
|**Event A Start and End Times** |Mandatory. This field triggers the process for all occurrences of Event A within this time period. |
|**Trigger Event** |Mandatory.<br><br>**Completing Event A triggers this process after the user completes a certain event**, and the users who complete this event will be filtered based on "target audience." Only users meeting both 'trigger conditions + target audience' will actually be reached.<br><br>**Uncompleted Event B**: Unlike 'Event\-Triggered: Completion of Event A', this task type awaits a certain period after Event A is completed to determine if Event B is completed; the process is triggered only if Event B remains uncompleted.<br><br><span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/431ecb6449bb474795ac10ffc80fa42f~tplv-goo7wpa0wc-image.image) </span><br><br>**Accumulatively Completing/Upon Each Completion of/Each Separate Completion of Event A**<br><br><br>* Completing Event A 3 times accumulates, ensuring users only enter the process once after completing the event.<br><br>* Each completion of Event A 3 times triggers the process execution every time the user completes Event A.<br><br>* Each unique completion corresponds only to a single contact after the event is completed; multiple event completions can be configured with 'and/or' relationships, and the count for each event can be individually set.<br><br><br>**After completing Event A, determine whether Event B has not been completed**: Supports assessing completion of Event B within a specific period after Event A and also on the same day Event A is completed. |
|**End date of the task** |Mandatory. Upon reaching the 'End date of the task,' thestatus changes to completed, and alllogic ceases execution. |


<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/ca80280485904ce5885a78cb37997616~tplv-goo7wpa0wc-image.image" width="1237px" /></div>


**Step 2: Configuration of Atomic Nodes**

Atomic nodes come in three types: "Judgment", "Process", and "Message Delivery". A detailed introduction to the usage of each atomic node will follow.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/6fff7601861146aba4e36e62aa593d24~tplv-goo7wpa0wc-image.image) </span>

 **(1) Segment Judgment Node**


|Field |Field meaning and purpose |
|---|---|
|**Node configuration** |<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/2c271e4da4e0488d856ff4db0f893722~tplv-goo7wpa0wc-image.image) </span><br><br>**Rule creation segment**<br><br><br>1. Node name: Provide a name to differentiate between atomic nodes<br><br>2. Segment rule creation: After purchasing VeCDP, you can use "rule creation segment" for creating segments, which allows selection through labels, attributes, segment packs, detailed data, and behavioral data.<br><br>3. Segment estimation: Calculate the number of segments in advance and decide whether to adjust the segment rule creation settings based on the estimation results.<br><br>   * The estimated audience for this level is calculated based on the current "segment rule creation conditions".<br><br>   * The joint audience estimate is calculated based on the current "segment rule creation conditions" and the intersection of all "upper\-level atomic nodes".<br><br>4. If selected, sync the newly added segment to the CDP segment list: The segment will be displayed in the CDP segment list.<br><br><br>**Existing segments**<br><br>Represents that you can directly select a segment for judgment in this layer. |
|**After completion** |The system will extend two branches under this atomic node, namely "satisfied" and "not satisfied", representing two types of processing logic after segment judgment.<br><br><span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/524a68f598b84203bc715a8c701dbb23~tplv-goo7wpa0wc-image.image) </span> |


 **(2) Event Judgment Node**


|Field |Field meaning and purpose |
|---|---|
|**Node configuration** |<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/28e26aaeabca4de4bfe8e796a10897e0~tplv-goo7wpa0wc-image.image) </span><br><br>**Configuration information**<br><br><br>1. Node name: Enter a name to distinguish different atomic nodes<br><br>2. Event rule: Represents whether the user meets the event criteria within a certain period after entering this atomic node (i.e., after flowing out of the upper node).<br><br>   1. **Accumulated done**: Supports multiple events, only 'or' logic between events, representing if multiple events complete the specified number of times within a certain period, conditions can be satisfied. If multiple events are entered, then meeting the corresponding number of times for 'one event' is sufficient.<br><br>   2. **Done separately**: Supports multiple events, with 'and/or' logic between events:<br><br>      1. Or: Fulfillment is achieved by completing the corresponding number of times for just '1 event'.<br><br>      2. And: Each event must be completed the corresponding number of times to meet the requirement.<br><br>   3. **Not done**: Supports multiple events, and the events support 'and/or' logic.<br><br>      1. Or: If at least 1 event has a count of 0 occurrences within a certain period, the trigger condition is fulfilled.<br><br>      2. And: If all events have a count of 0 occurrences within a certain period, the trigger condition is fulfilled. |
|**After completion,**  |The system will extend two branches under this atomic node, representing 'satisfied' and 'not satisfied', which denote the two types of processing logic after event judgment.<br><br><span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/48e11ed060de404bba6c51d374c98b93~tplv-goo7wpa0wc-image.image) </span> |


 **(3) Delay Node**


|Field |Field Meaning and Purpose |
|---|---|
|**Node Configuration** |<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/0a551fee820a43dbac4ccd1986341801~tplv-goo7wpa0wc-image.image) </span><br><br>**Delay Rules**<br><br><br>1. **Relative Delay Time**: Supports delays of X seconds/minutes/hours/days. For example, a delay of 1 day represents a 24\-hour delay.<br><br>2. **Delay Until a Specified Time**: Supports delaying until a specified time. If the user has not entered this node by the specified time, they will not be reached.<br><br>3. **Delay Until a Specified Day**: Delay to a specific day and time, which refers to the closest upcoming specified time. For instance, if set to delay until 8:00 on the first day, those entering the delay timer before 8:00 will exit the timer at 8:00 on that day; those entering after 8:00 will exit the next day at 8:00.<br><br>4. **Delay Until a Specific Weekday**: Delay to a specific weekday means waiting for the next occurrence of that weekday after an event. For example, if set to delay until Tuesday and the event occurs on Monday, it will be reached this Tuesday; if the delay is until Tuesday and the event occurs on Wednesday, it will be reached next Tuesday.<br><br>5. **Delay To a Trading Day**: Delays until a trading day in the week or month that the node is entered. This feature is an value\-added service. If needed, please contact Vulcan customer service.<br><br>6. **Delay Until a Specific Natural Day of the Month**: Specifies delaying to a certain day of the nearest month. For example, if set to the 15th day of each month at 8:00, those entering the delay timer before 8:00 on the 15th will exit the timer on the 15th at 8:00 of the current month; those entering after 8:00 on the 15th will exit the timer at 8:00 on the 15th of the next month. |
|**After filling out** |The system will display the latency handling logic of this node, and you can add other processing conditions below<br><br><span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/fe97f46381a449838b3d1496a91e46a6~tplv-goo7wpa0wc-image.image) </span> |


 **(4) A/B Split Node**


|Field |Field Meaning and Purpose |
|---|---|
|**Node Configuration** |**A/B Split** refers to diversifying traffic according to the set "branch traffic", and after setting, users entering this node will randomly be assigned to one of the groups based on traffic proportions.<br><br><span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/7fcbd2fef74c4c849603ee515f47f273~tplv-goo7wpa0wc-image.image) </span> |
|**After Filling Out** |The system will display information for each experiment group, and you can configure the subsequent processing logic under different branches.<br><br><span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/f09d79d53b9244ea8e22385062a64b19~tplv-goo7wpa0wc-image.image) </span> |


 **(5) A/B Racing**


|Field |Field Meaning and Purpose |
|---|---|
|**Node Configuration** |**A/B horseracing refers to conducting experiments at a set low flow rate, manually selecting the remaining flow for the experiment groups after reviewing the data,**  a process canvas only supports one A/B horseracing node.<br><br><span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/324a69defc234d9f8d6222685ae426f5~tplv-goo7wpa0wc-image.image) </span><br><br><br>1. **Horseracing flow**: This flow represents the proportion of traffic to be chosen during the horseracing phase. For example, you can select 30% of the horseracing traffic for comparison between experiment and control groups, and after identifying the superior group, readjust the remaining 70% of the traffic to the winning group.<br><br>2. **Experiment versions**: Represents during the horseracing period, how many groups need to be compared.<br><br>3. **Experiment notification**: If an experimental index is set, once the horseracing stage is completed, the creator will be notified via SMS or email to allocate the remaining traffic fully. |
|**After completing the fill\-out,**  |The system will display information of each experimental group, where you can configure the subsequent processing logic under different branches.<br><br><span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/b5a2c969561e447997742459a04f33f1~tplv-goo7wpa0wc-image.image) </span> |


**Segmentation and Routing**


|Field |Field definition and purpose |
|---|---|
|**Node Configuration** |<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/77636d32d2d342e1b153a8046c3496cc~tplv-goo7wpa0wc-image.image) </span><br><br>Segmentation and traffic distribution are similar to segment judgment, the difference being that 'segment judgment' is for a single segment, while 'segmentation distribution' is for multiple segments, used based on actual business needs.<br><br>**Two methods of segmentation distribution**<br><br><br>1. **Enter branches by priority**: Users who meet the conditions enter the corresponding branches one by one in the order of configured priorities. This function is similar to the logic of the 'Strategy\-User Distribution' in the old version of the Process Canvas.<br><br>2. **Enter branch if conditions are met**: Users can enter the corresponding branch if they meet the conditions. If a user meets multiple conditions, they will enter multiple branches at the same time.<br><br><br>**Label and behavior\-based rule creation segment**<br><br><br>1. Node name: Fill in a name to distinguish different atomic nodes.<br><br>2. Segment rule creation: After purchasing VeCDP, you can use the 'Label and Behavior\-based Rule Creation Segment' to create segments, which can be selected through labels, attributes, segment packages, detailed data, and behavioral data.<br><br>3. Segment estimation: Calculate the number of segments in advance, and decide whether to adjust the segment rule creation conditions based on the estimation results.<br><br>   * This layer's audience estimation is based on the current 'segment rule creation conditions' to calculate the number of segments in advance.<br><br>   * Combined audience estimation is based on the current 'segment rule creation conditions' and all 'upper layer atomic nodes' intersections to calculate the number of segments in advance.<br><br><br>**Existing segment**<br><br>Representatives can directly select a segment for judgment at this node level. |
|**After completion** |The system will extend multiple branches under this atomic node:<br><br><br>1. **If 'Enter branches by priority' was selected during node configuration,**  users will judge from left to right after entering this node<br><br>2. **If 'Enter branch if condition met' was selected during node configuration,**  users will judge if all the segments of this branch meet the conditions after entering this node; if a user meets multiple conditions, they will enter multiple branches simultaneously<br><br><br><span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/20e558a41d894e02add020d949ef930a~tplv-goo7wpa0wc-image.image) </span> |


**Event Routing**


|Field |Field meaning and purpose |
|---|---|
|**Node configuration** |<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/14856210d01a4552b15363eb57357e34~tplv-goo7wpa0wc-image.image) </span><br><br>Event branching and event judging are similar, but the difference lies in that 'event judging' pertains to judging single set event condition logic, while 'event branching' involves judging multiple segmented condition logic based on actual business needs. |
|**After filling out the form** |The system will extend multiple branches under that atomic node:<br><br><span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/c48080a1a0aa4294b03b4a85ba677298~tplv-goo7wpa0wc-image.image) </span> |


 **(8) Webhook, SMS, and other Channels**

Channels logic is similar and will not be explained one by one; this time, we will use Webhook as an example.


|Field |Field meaning and purpose |
|---|---|
|**Node configuration** |<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/a369218489d3419c97d412b3cb5d8d4e~tplv-goo7wpa0wc-image.image) </span> |
|**Node configuration** |The node name is used for internal logic identification and does not affect actual sending. |
|**Subject transformation** |<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/63a08781faf34c3292572b6dc1da21dd~tplv-goo7wpa0wc-image.image) </span><br><br><br>1. **Application scenario**: The process canvas circulates a subject throughout the process. Before reaching the target, it supports transforming the subject to meet cross\-subject business scenarios. For example, the entire process canvas circulates with a vehicle as the subject. When the vehicle insurance expires, it reaches out to the car buyer, reminding them to renew their insurance. In such cases, this function can be used to meet the requirement.<br><br>2. **Prerequisites for using this function**: Purchase of CDP multi\-subject and GMP multi\-subject outreach. If this value\-added feature is not activated, the function will not be available.<br><br>3. **Subject Transformation**: This feature allows the current subject on the process canvas to be transformed into another subject related to it, with options to select the target subject and the relationship between the original and target subjects.<br><br>4. **Reach Rules**: When a single original subject corresponds to multiple target subjects, one can choose either "Reach any one" or "Reach all"; when multiple original subjects correspond to a single target subject, it must reach all (i.e., if several original subjects correspond to one target subject, it will reach this target subject multiple times). |
|**Reach Content** |Fill in the reach content as needed for different channels |
|**Non\-trading Day Reach** |1. **Prerequisites**: This function is an added\-value service in the securities industry, and contact with Volcano staff is necessary to enable it. If this added\-value service is not activated, the function will not be available.<br><br>2. **Non\-trading Day Reach**:<br><br>   1. When the send Date is a non\-trading day, you can set it to be postponed to the next trading day, not to send, or to send as usual.<br><br>   2. Popup\-type channels currently do not support non\-trading day settings.<br><br><br><span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/f2f393dd93a54caa8c337e717c6eecd7~tplv-goo7wpa0wc-image.image) </span> |
|**Channel black and white list** |1. Here you can set whether to enable "channel black and white list" for this contact<br><br>2. **Channel reach range blacklist**: This feature supports not sending messages in this channel if the user ID is in the blacklisted segment during actual transmission. If not selected, it means there will be no restrictions.<br><br>3. **Channel frequency control whitelist**: This feature allows user IDs in the segment to be exempt from channel frequency control during actual transmission in this channel. |
|**Do Not Disturb Configuration** |You can set a do not disturb period. If the atomic node plans to send messages during this period, it will be restricted by do not disturb. If it is filtered due to hitting the do not disturb criteria, you can choose to "abandon this contact" or "continue contacting after do not disturb ends". |
|**Key Metrics** |You can set the key metrics that this atomic node needs to monitor. |
|**Continuous Contact** |This feature allows you to configure the subsequent processing logic after the touch node is reached. It can be configured in combination with actual business scenarios. The system will display the subsequent branches of the Process Canvas touch node based on the selected configuration.<br><br><span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/c05cdf279e7d42f1b4833c45299d182e~tplv-goo7wpa0wc-image.image) </span><br><br><span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/b4f51541910346c88079e74c0bf29624~tplv-goo7wpa0wc-image.image) </span> |


<span id="07aaf2b8"></span>
## **4. Basic Information**

<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/d747487b4dbc46d6b187a9810ec2ebbb~tplv-goo7wpa0wc-image.image" width="1920px" /></div>



|Field |Meaning and purpose of the field |
|---|---|
|**Canvas name** |Required, used to distinguish between different tasks (strategies), cannot be duplicated with other tasks |
|**Task type** |Required, includes general activities, emergency activities, and notification activities.<br><br>**Task type affects task priority, and task priority affects the logic of which task is triggered first when multiple tasks are triggered simultaneously (when the message queue being sent is backlogged): the task with higher priority is triggered first.** <br><br>Priority: Notification messages \> Urgent activities \> Regular activities. Each task triggers once and consumes one frequency control count for the corresponding channel. |
|**Group** |Optional, you can place different tasks into different groups for subsequent analysis based on task grouping. Message Delivery and Process Canvas groups are isolated; their data do not intercommunicate. |
|**Associated Campaign** |Optional, tasks can be attributed to different campaigns, such as the "Double Eleven Campaign," for subsequent analysis based on the campaign associated with the task. Tasks from Message Delivery, Process Canvas, or Placement can be linked to the same campaign. |
|**Do Not Disturb Configuration** |You can set a Do Not Disturb period. If the system is scheduled to enter the Process Canvas during this period, it will be restricted by the Do Not Disturb setting, meaning it cannot enter this Process Canvas. |
|**Process Mutex** |Optional. This indicates that the selected task has a mutually exclusive relationship with the current task, targeting only one task can be successfully reached for the target user (same user id). For example, if Task A and Task B are mutually exclusive, if a user is successfully reached by Task A, they will not be reached by Task B, and vice versa. Supports searching by task name or ID. Currently, only the first 50 task data are displayed. For more tasks, please search. |


<span id="17f8da38"></span>
## **5. Key Indicators**

This feature allows the setting of overall key indicators for the process canvas, meaning all users who successfully enter the process canvas will be tracked.

<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/3dda10ce84d949e08f931eb7635f5259~tplv-goo7wpa0wc-image.image" width="1920px" /></div>



|**Field** |Field meaning and purpose |
|---|---|
|**Configuration method** |You can choose to "Create New Indicator" or directly use the "Existing Indicator". |
|**Indicator Name** |Mandatory.<br><br>Examples: Add to shopping cart, create an order, GMV. When creating a task, the indicator name you enter will be reflected on the data analysis page. |
|**Manage Indicators** |On the right side of the indicator name, there is an entrance to "Manage Indicators," where you can view all indicators in the system, check their configuration rules, and also delete indicators. Deleting indicators will not affect the data already set in the task; it will only affect the inability to select when choosing existing indicators.<br><br><span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/b5fae7e52cb94418bf9b43222bb50e94~tplv-goo7wpa0wc-image.image) </span> |
|**Calculation Conditions**<br><br>**Calculated based on real\-time behavioral data** |**Examples of Indicators**: visits to the product detail page, add\-to\-cart, views on the mini\-program's homepage<br><br>**Conditions Required for Use**: If a behavioral data source has "real\-time behavioral messages," you can set real\-time behavior count/person statistics indicators for that data source. If you are unsure whether the data source meets the conditions, you may consult the project manager or customer success manager.<br><br>**How to configure**: Select data sources and events, and add filter conditions if necessary by clicking "Filter Conditions". For example, to count the visits to the product detail page, restrict the product detail page address using this feature.<br><br><span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/6c8f649fceba46d7805e1332cad90d67~tplv-goo7wpa0wc-image.image) </span><br><br>**What are the results of data analysis after configuration**:<br><br><br>* After configuration, the channel's message delivery and process canvas tasks will automatically focus on this indicator.<br><br>* This indicator will track user conversions within a specified window after being reached.<br><br>* Once a conversion event occurs after configuration, this indicator will be updated in real\-time. |
|**Calculation Conditions**<br><br>**Calculated through offline behavioral data** |**Indicator examples**: Product detail page visits, add\-to\-cart volume, Home page views of the mini\-program<br><br>**Conditions needed for use**: If a behavioral data source is updated daily as an "incremental table", you can set the count/number of people statistics for actions under this data source. If you are unsure whether the data source meets the requirements, you can consult a project manager or a customer success manager.<br><br>**How to Configure**: Choose the data source and event, and if you need to add restrictions to the event, you can click on 'Filter Conditions' to add them. For instance, to count the number of visits to a product details page, you can use this feature to restrict the product details page URL.<br><br><span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/a3f962344fac479cb2d0c8149808f63f~tplv-goo7wpa0wc-image.image) </span><br><br>**What are the results of data analysis after configuration**:<br><br><br>* After configuration, message delivery and process canvas tasks of this channel will automatically monitor the indicator.<br><br>* This indicator will track user conversions within the specified window period after reaching them.<br><br>* After configuration, as long as the conversion event occurs, the system will count the indicator data at 5, 11, 17, and 23 o'clock every day.<br><br><br>**The difference between this data source and 'using real\-time behavior data source'** : If there is 'real\-time behavior message', prioritize using the 'using real\-time behavior data source' feature. If not, use 'computing through offline behavior data'. |
|**Calculation Conditions**<br><br>**Computing through detailed data** |**Indicator Examples**: Order count, GMV<br><br>**Conditions required for use**: If the detail data is updated daily as an "incremental table," you can set the detail row as a statistics indicator for this data source. If you are unsure whether the data source meets the conditions, you can consult the project manager or customer success manager.<br><br>**How to configure**:<br><br>Select the data source and fields, and if you need to add conditions to events, you can click "Filter Conditions" to add them. For example, to calculate the number of orders, if you need to restrict the product category, you can use this feature.<br><br>If you want to count the occurrences of a field, choose "Count/Number of People".<br><br><span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/7329d651b4a6445db0f61e7edd0c176b~tplv-goo7wpa0wc-image.image) </span><br><br>If you want to sum the fields, choose "Sum". For example, the GMV indicator requires summing the amount of goods.<br><br><span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/0001e2cc75dc431287c91e8b82af1fc7~tplv-goo7wpa0wc-image.image) </span><br><br>**What are the results of data analysis after configuration**:<br><br><br>* Once configured, the channel will automatically monitor the metric for message delivery and process canvas tasks.<br><br>* This metric will track user conversions within a designated window period after being reached.<br><br>* Once configured, as soon as a conversion event occurs, the system will compile the metric data at 5, 11, 17, and 23 o'clock daily. |
|**Calculation Conditions**<br><br>**Composite Metrics** |**Composite Metrics**<br><br>Metric examples: Add\-to\-cart rate, per customer transaction, SMS sending cost<br><br>After clicking, you can perform composite operations between metrics. You can select a metric or enter a value.<br><br>Select a metric: Only supports selecting volume sent, delivery volume **and the metrics already selected on the current page**.<br><br><span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/6f37796b026047f6b30650afaefd0c17~tplv-goo7wpa0wc-image.image) </span><br><br>Enter the value: You can also directly enter numbers by clicking the selection box, used to calculate indicators similar to "SMS Sending Cost".<br><br><span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/4b4dbcb89ad04135bc1039815bb27903~tplv-goo7wpa0wc-image.image) </span> |
|**Window Period** |This refers to recording how long the data is collected within the window period after the user has been reached. |
