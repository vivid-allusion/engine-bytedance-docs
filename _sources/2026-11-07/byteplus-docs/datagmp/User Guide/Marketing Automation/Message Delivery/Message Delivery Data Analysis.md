---
title: "Message Delivery Data Analysis"
product: "Byteplus GMP"
product_code: "datagmp"
source: "https://docs.byteplus.com/en/docs/datagmp/Message_Reach_Effect_Evaluation"
---

<span id="d554c480"></span>
### **1. Product Overview**

Click "Data Analysis" in the message delivery task list to enter the data analysis report panel for that task. Tasks with statuses "Running," "Paused," "Canceled," "Ended," or "Abnormal" can all undergo "Data Analysis." Data Analysis includes: funnel graphs, key metrics, execution records, detailed data, benefit data, and activity landing page data.

<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/c24a1cb99b514901a384c6a984723134~tplv-goo7wpa0wc-image.image" width="439px" /></div>


<span id="338df4b4"></span>
### **2. Function Description**

**2.1 Funnel Diagram**

By default, the funnel data for this outreach is displayed, allowing examination of the conversion rate for each layer. The funnel can display data for each step of the process, including task execution, sending, delivery, and clicking links.

If the purchased package is GMP + VeCDP, clicking on a hyperlink metric allows to save the funnel metric to a segment or carry out portrait insights.

<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/4907ce5ccfe04e99a2beabbf1c981eb9~tplv-goo7wpa0wc-image.image" width="439px" /></div>


**2.2 Key Focus Areas**

Metrics set at the channel level or task level will ultimately be reflected in the "Key Focus Areas" module on the "Data Analysis" page of the task. If you purchase the GMP + VeCDP package, you can click on the "Real\-Time Update" metrics, which can be saved for segmentation or used for profiling insights.

<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/5dab0504409545dbb38e35d1f5d77eb5~tplv-goo7wpa0wc-image.image" width="361px" /></div>


**2.3 Execution Records**

The Execution Records module allows viewing of task approval completion times, segmentation preparation times, task execution status, and sending progress. **When a task is abnormal or cancelled, the cause can be identified based on the execution records**.

If the task is abnormal due to unsuccessful segmentation preparation, the task creator can restart the execution from the Data Analysis page by clicking "Restart Execution". The task will resume operation at the moment "Restart Execution" is clicked.

<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/f1593b90c9574204b8e045348a9c4608~tplv-goo7wpa0wc-image.image" width="301px" /></div>


**2.4 Detailed Data**

You can view the task's sending, delivery, and click data, which is tracked by default by "Per Visit"; the top "Visitor/Visit" tab can be switched to visitor metrics. If you purchase the GMP + VeCDP package, clicking on hyperlinked metrics allows you to save these funnel metrics for segmentation or perform profiling insights. The type of indicators displayed is related to the task trigger conditions.

<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/66a3f5f0365645399224ba026709f33f~tplv-goo7wpa0wc-image.image" width="439px" /></div>


 **(1) Scheduled \- One\-Time, Scheduled \- Repeated**


| |Index and Meaning Explanation |
|---|---|
|Audience Members |The number of IDs in the task segment. What's special: If it is scheduled \- repeated, under the dimension of the number of people, it represents the accumulation of the number of IDs counted each time the task runs. |
|Prepared Sending Volume |The number of IDs that meet all filter conditions such as frequency control, do not disturb, and task exclusion among the target audience. |
|Sending Volume |The number of messages sent by GMP. |
|Sending Rate |Sending Volume / Prepared Sending Volume |
|Delivery Volume |The actual number delivered by downstream channels, this indicator depends on the receipt data from downstream channels. |
|Delivery Rate |Delivery Ratio |
|Clicks |Actual number of clicks. |
|Click Rate |Clicks/Deliveries |


 **(2) Event\-Triggered: Completion of Event A, Event\-Triggered: Event A Completed & Event B Incomplete**


| |Indicator and Meaning Description |
|---|---|
|Completion of Event A Quantity |Number of 'Event A' completions within the designated 'Start to End Time Range for Event A' |
|**Event A Completed & Event B Incomplete Quantity** |From the start of Event A to the end of the Message Delivery Task period: the combined event quantity of completing Event A and not completing Event B within the designated delay judgment time.<br><br>\*This indicator is only shown under "Event\-Triggered: Event A Completed & Event B Incomplete" scenarios. |
|Prepared Send Volume |The number of IDs among the audience that satisfy all the filter conditions such as frequency control, Do Not Disturb, exclusion of tasks, etc. |
|Send Volume |The number of messages sent by GMP. |
|Send Rate |Send Volume / Prepared Send Volume |
|Delivery Volume |The actual number of deliveries by downstream channels, dependent on receipt data from those channels. |
|Delivery Rate |Delivery Rate/Sent Rate |
|Clicks |The actual number of clicks.<br><br>Specially, under the "Popup" channel, it displays as: Clicks (1), Clicks (2).<br><br><br>* If it is just an image: It will only show Clicks (1), which represents the clicks on the image<br><br>* If it includes a button: Clicks (1) refers to the clicks on the first button; Clicks (2) refers to the clicks on the second button<br><br>* For popups created with a drag\-and\-drop template (not a preset template), it refers to the cumulative number of all clicks. |
|Click Rate |Clicks/Delivery Rate |
|Successful Popup Count |The number of successfully opened pop\-ups.<br><br>\*This indicator is displayed only under the "pop\-up" channel. |
|Successful pop\-up rate |Number of successful pop\-ups / number prepared for sending<br><br>\*This indicator is displayed only under the "pop\-up" channel. |


**2.5 Filter Details**

Clicking 'Filter Details' will expand the filtering reasons for each layer of the funnel. Some filtering reasons allow you to click 'Resend'. By clicking, the system will filter users associated with that reason and redirect to the 'Send Details' page where you can resend to these users.

<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/4fa0697f185c4619a704a5731aaf6cfd~tplv-goo7wpa0wc-image.image" width="439px" /></div>


Common filtering reasons in the funnel are shown in the table below.


| |**Explanation of filtering reasons** |
|---|---|
|ID mapping failure |During the ID mapping from ID_A to ID_B, an error occurred in the interface service used for the conversion, resulting in the ID not being successfully converted. |
|ID mapping is empty |During the ID mapping from ID_A to ID_B, the original ID did not yield the corresponding target ID. |
|No sending for experiment segment |The following two scenarios will result in this filtering: 1. If a race experiment is set, during the small traffic testing phase, only users who hit the experiment will be reached; the rest will be filtered. 2. If a race experiment is set, when reaching the remaining traffic users, the system will filter out users who were already reached in the small traffic phase. |
|Task fallback de\-duplication |When there are duplicate IDs in the sent segment document or when the system performs internal retries, duplicate send IDs are generated, and the system filters them out. |
|Sender task frequency control |The task has set frequency control conditions, and the system automatically filters out users who have reached the frequency control limits. |
|Error in reading sender task frequency control information |An abnormal issue occurred when the system was reading the configuration for frequency control conditions. |
|Sender channel frequency control |Frequency control conditions are set in the channel, and the system automatically filters out users who meet the frequency control restrictions. |
|Do not disturb for sender tasks |Do not disturb conditions are set in the process canvas configurator and others, so the system automatically filters out users scheduled to be sent during the do not disturb period. |
|Channel do not disturb |Do not disturb conditions are set in the channel, and the system automatically filters out users scheduled to be sent during the do not disturb period. |
|Do not disturb for rule engine tasks |Do not disturb conditions are set in the conditions for entering message delivery tasks or process canvas tasks, and the system automatically filters out users scheduled to be sent during the do not disturb period. |
|Do not disturb for scheduling tasks |Do not disturb conditions are set in scheduled tasks, and the system automatically filters out users planned to be sent during the do not disturb period. |
|Blacklist interception |Blacklist user filtering was configured on the channel side, and filtering was performed based on these conditions. |
|Non\-whitelist user interception |Non\-whitelist user non\-reach was configured on the channel side, and filtering was performed based on these conditions. |
|Mutually exclusive interception |"Exclude task" conditions were configured in the task, and the current user was already reached by another task, thus, the system filtered it out. |
|Error while reading mutually exclusive configurations |The system ran into an abnormal issue while reading the "Exclude task" conditions. |
|Channel sending failure |GMP had prepared the users and content for sending, but the channel send interface failed when called. |
|Failed channel receipt |The channel provided a receipt but failed during actual sending. |
|Rule engine task frequency control |The task set frequency control conditions, and the system automatically filters out users who have met these conditions. |
|Entry conditions not met |The user does not meet the audience conditions set in the process canvas entry settings. |
|Segmentation interface error |Judging whether the user is in the specified segmentation interface resulted in an error and an Abnormal occurrence. |
|Attribute replacement failed |Errors occurred while replacing labels, attributes, IDs, or short\-links. |
|Copy replacement failed |The service reports an error when replacing labels, attributes, IDs, or short links. |
|The getprofile interface reports an error. |The interface for fetching user label/attribute values reports an error. |
|User attributes/ID/labels are empty. |After calling the interface to fetch user label/attribute values, the data for that user is empty. |
|AB segmentation fails. |During AB segmentation, idmapping fails, or the segmentation interface reports an error. |
|Objective B completed. |This user has completed the event configured in the task as Objective B, did not meet the conditions, and was filtered. |
|Main objective completion does not trigger message delivery. |The task is set to "Do not reach after completing the primary target," and when the user completes the primary objective set in the task, the system automatically filters out the user. |
|No channel acknowledgement received |After sending the content to the channel, the channel side did not provide an acknowledgement. |
|Other |Unknown reason for filtering |


**2.6 Sending Details and Resending**

Clicking on 'Sending Details' will expand a pop\-up window where you can view the reached users, the sending status, and the actual arrival status. The 'Sending Details' page allows for resending.

**You can directly apply filters or resend selected options.**  After clicking "Resend", you will be redirected to the "Send Details" page, where the system automatically filters users affected by the filtering reason. You can choose to resend to all users under the "current filter conditions." After confirming your choice, the system will resend to the users based on the selected conditions. The content sent includes task\-configured content, and if labels, properties, or other variables were included in the task, the latest data will be retrieved for sending.

<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/c11a14af32a24efcb719c9e1d4486152~tplv-goo7wpa0wc-image.image" width="439px" /></div>


**2.7 Benefit Data**

If a "Benefit" is included in the task, data on the issuance and reception of benefits will be displayed below the detailed data analysis.

<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/44797ba2f1364fc6834b32014d4850d7~tplv-goo7wpa0wc-image.image" width="439px" /></div>


**2.8 Activity Landing Page Data**


* Click on Activity Data, and enter the Campaign ID or Campaign Name to view related campaign data.


<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/e466a54621934a11b8bba70d89b0d4d7~tplv-goo7wpa0wc-image.image" width="439px" /></div>



* The Campaign ID can be found on the campaign list page.


<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/f1d33dff1160406e8634dc451605b37c~tplv-goo7wpa0wc-image.image" width="439px" /></div>
