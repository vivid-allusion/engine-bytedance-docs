---
title: "Create Message Delivery Task"
product: "Byteplus GMP"
product_code: "datagmp"
source: "https://docs.byteplus.com/en/docs/datagmp/Create_Message_Reach_Tasks"
---

> Message Delivery: A fundamental module of GMP, designed to assist operators in swiftly creating marketing campaigns through SMS, App Pop\-ups, Webhooks, and other methods to reach target audiences that meet certain trigger conditions. The difference between Message Delivery and Process Canvas is that Message Delivery is single\-channel while Process Canvas allows multiple channels to be configured for automated execution.

> Channel: Refers to the medium through which message content is presented, including SMS, App Pop\-ups, and custom Webhook channels.


<span id="b6c4b04e"></span>
## **1.1 SMS**

<span id="80c7c3c8"></span>
### **1. Product Overview**

Sending SMS can occur in two scenarios:

 **(1) If there are no accounts for "BytePlus SMS, YUNPIAN SMS, Alibaba Cloud SMS, Tencent Cloud SMS, Jiguang SMS, Mengwang SMS," but accounts for other SMS platforms**: SMS can be sent via Webhook; contact the project manager or customer success manager for channel integration process. Once integration is complete, please refer to the operational instructions in the Webhook section.

 **(2) If accounts for "BytePlus SMS, YUNPIAN SMS, Alibaba Cloud SMS, Tencent Cloud SMS, Jiguang SMS, Mengwang SMS" are already available**: Only configure the relevant secret keys on the platform and obtain the necessary permissions to send SMS. The module enables the capability to send messages through the GMP platform.

<span id="41881ac8"></span>
### **2. Prerequisites**


| |**Detailed Description** |
|---|---|
|**Prepare SMS Account** |Provide an account on any platform among "BytePlus Messaging, Yunpian SMS, Alibaba Cloud SMS, Tencent Cloud SMS, Jiguang SMS, and Mengwang SMS" |
|**Configure the channel in GMP** |Complete the channel configuration on the GMP "Management Center \- Channel Management \- SMS" interface, and **you also need to fill in the receipt address on the corresponding SMS platform to receive the SMS delivery receipt messages**. This step is usually completed by technical personnel. For details, please refer to the "Technical Integration Document". |
|**Activate GMP Permission** |The administrator activates SMS signature permission, permission path: Management Center \- Channel Management \- SMS Signature<br><br>The administrator activates SMS template permission, permission path: Marketing Strategy \- SMS Template<br><br>The administrator activates Link Tool permission (optional), permission path: Marketing Strategy \- Content Management \- Link Tool, if GMP side short link is not used, this permission can be optional.<br><br>The administrator enables the permission to create tasks, permission path: Message Delivery \- Message Delivery Task \- New<br><br>The administrator enables the viewing permission for the SMS channel, permission path: Management Center \- Channel Management \- SMS \- View |
|**Enable segment permission** |Enabling segment permission comes in 3 scenarios:<br><br>If VeCDP is purchased, the permission "Segment \- Private Domain Segment \- View/Add/Delete Segment" needs to be enabled in VeCDP, and once enabled, the segment function in task creation can be used.<br><br>If VeCDP is not purchased but only Datafinder is purchased, the permission "Segment" needs to be enabled in Datafinder, and once enabled, the segment function in task creation can be used.<br><br>If neither VeCDP nor Datafinder is purchased, this permission can be ignored. |


<span id="207a6bd7"></span>
### **3. Function Description**

**3.1 Prepare SMS Signature**

SMS Signature creation entry: Management Center \- SMS Signature. Different SMS channels handle signature logic differently, **for detailed function description please refer to "Management Center \- SMS Signature"** . Using "SMS Signature" requires simultaneous activation of "Management Center\-Channel Management\-SMS Signature\-All" and "Management Center\-Channel Management\-SMS Channel\-View" permissions.


* **If the SMS Channel is "BytePlus SMS"** : You can create a new SMS signature on GMP and manage existing ones.

* **If the SMS Channel uses "Montnets"** : One account is bound to one signature, GMP does not support individual signature management at this time.

* **If the SMS Channel uses "Yunpian"** : You can include the signature in the SMS Template, GMP does not support individual signature management at this time.

* **If the SMS channel used is "Alibaba Cloud/Tencent Cloud/Aurora Channel"** : After applying for signatures on the corresponding platforms, add them manually to the GMP system.


<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/8aa1ac2dd00b4be2b923763a12c4e251~tplv-goo7wpa0wc-image.image" width="678px" /></div>


<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/532c6bdc27134a7fbece77c79f8d5b36~tplv-goo7wpa0wc-image.image" width="708px" /></div>


**3.2 Prepare SMS Template**

Entry point for creating an SMS template: Marketing Strategy \- Content Management \- SMS Template. Different SMS channels handle templates differently; **for detailed function descriptions, please refer to "Content Management \- SMS Template"** .


* **If the SMS channel is "BytePlus Messaging"** : You can directly create a new SMS template in GMP, manage existing templates

* **If the SMS channel used is "Montnets/Cloud SMS/Alibaba Cloud/Tencent Cloud/Aurora"** : You can import "Template ID" or "Template Content" in GMP, and use them when creating marketing tasks after import.


<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/0b10eeb49e784b30ae4a4995a62395a1~tplv-goo7wpa0wc-image.image" width="660px" /></div>


<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/af4ba5079a9a4d06b1156bff67b932e6~tplv-goo7wpa0wc-image.image" width="668px" /></div>


**3.3 Prepare Short Links**

SMS length is limited, so it is typical to insert short links to reduce the number of characters. GMP offers "Link Tool" capabilities, which support converting long URLs to short URLs and measure PV, UV. If you do not use short links from the GMP side, you can skip this section. Short links are categorized into three types: general short links, long\-to\-short parameterized links, and mini\-program short links. **Please refer to "Content Management \- Link Tool" for a detailed description of the functionality.** 


| |**Description** |
|---|---|
|**Generic short link** |**A generic short link is a short link converted from an original long link**<br><br>**Usage scenario**: Insert a short link in the SMS content, users can click to open the original link directly, used for scenarios such as user re\-engagement, and campaign marketing.<br><br>**Validity**: Expires upon term completion, perpetually valid. If an expiration is set, then the expiration date must be entered, and the validity period cannot exceed one year; if it exceeds one year, it can only be set to perpetual.<br><br>**Expiration Date**: It is necessary to set an expiration date; after which the short link will lead to a 404 page.<br><br>**Track Click UV**:<br><br>If not tracked, then the short links generated by all users will be the same, making it impossible to track Click UV data.<br><br>**Track**: **To measure Click UV by generating different short links for different users at the time of engagement.**  **If it is necessary to track which users clicked the short link, then it must be set to "Track Click UV: Track".** <br><br>**Original Link**: Mandatory; the original long link to be converted to a short link must be entered.<br><br><span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/df2680ba059b4e98bda194ca8bb387bb~tplv-goo7wpa0wc-image.image) </span> |
|**Conversion from parameterized long link to short link.**  |**Convert long URLs with parameters into short URLs, which can insert variables like ID, labels, and attributes into the original long URL**<br><br>**Use Case**: Insert short URLs into SMS content, which users can click to directly open the original link. This is useful for user re\-engagement, campaign marketing, etc., and allows the insertion of user attributes and IDs into the link. Users can view personalized page content based on their attributes and IDs when opening the link, or track data about user actions like button clicks and payments after opening the link.<br><br>**Validity**: Expires after a set period or is valid permanently. If the 'expires after a set period' option is selected, an expiration date must be set, and the validity cannot exceed one year. If more than one year is needed, it can only be set to permanently valid.<br><br>**Expiration Date**: An expiration date must be set. After this date, the short URL will lead to a 404 page.<br><br>**Subject ID**: The Subject ID represents the subject targeted by this short URL deployment. The queried attributes/IDs will be filtered based on this subject type. If this module has not been purchased, this option will not be displayed.<br><br>**Original Link**: Supports the insertion of variables such as user attributes, user IDs, and activity landing pages.<br><br><span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/9b92aeafdaf74ef49477dbbe59b73706~tplv-goo7wpa0wc-image.image) </span><br><br>**Note: When inserting variables into the original link, add a “?” after the original link, fill in the parameter name and “=” before each variable, and join multiple parameters with “&”.** <br><br><br>* Enter the original link<br><br>* Enter the "?" symbol<br><br>* Enter the name of the first parameter with an "=" sign, e.g., "userid="<br><br>* Click to insert the user ID and select the required user ID<br><br>* Enter the "&" symbol<br><br>* Enter the name of the first parameter with an "=" sign, e.g., "username="<br><br>* Click to insert the user ID and select the required user attributes<br><br><br><span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/c98bd4c6239440fc9fd4eadabcd0ec89~tplv-goo7wpa0wc-image.image) </span> |
|**Mini Program Short Link** |**Convert the Mini Program link into a short link, which can directly invoke the Mini Program and jump to the corresponding page when clicked**<br><br>**Expiration Date**: The expiration date needs to be entered, with a validity period of up to 3 months.<br><br>**Usage Scenario**: Insert the short link in the SMS content, enabling users to directly invoke the Mini Program page upon clicking, used for recalling lost users of the Mini Program, event marketing, and other scenarios. Supports "On\-the\-fly GMP Task Generation" and "Generic WeChat Mini Program Short Link" two methods of short link generation<br><br>WeChat Mini Program links support generating up to 500,000 short links per mini program per day<br><br><br>* On\-the\-fly GMP Task Generation: Used in scenarios such as message delivery tasks and process canvas by inserting a short link function; the system generates different GMP short links for different users when sending message delivery tasks, invokes WeChat's interface upon click to generate the original short link, allowing to track click UV of the short link; supports query parameters where you can insert fixed content to identify user source etc., or insert user attributes, ID, etc. as variables, displaying personalized page content based on user attributes and IDs when users open the link, or tracking data on user behaviors like clicking page buttons or making purchases<br><br>* Generic WeChat Mini Program Short Link: Only generates one GMP short link, on its first click, it will call WeChat's interface to generate the original short link, does not support UV tracking, and does not support inserting user attributes, ID, or other variables in the query parameters<br><br><br>Note: WeChat Mini Program links support generating up to 500,000 original short links per mini program **per day**; if the number of original short links generated by the method "On\-the\-fly GMP Task Generation" exceeds 500,000, it will result in the failure of sending the task<br><br>**Mini Program**: Select a mini program that has been integrated; if there is no desired mini program, refer to the "Management Center \- WeChat Mini Program" section for integration<br><br>**Mini Program Page Path**: Must be an existing page of a published mini program, cannot carry a query, will redirect to the homepage if the path is empty<br><br>**Query Parameters**:<br><br>Only supports numbers, upper and lower case English letters, and some special characters: !#$&'()\*+,/;:=?@\-_~<br><br><br>* For the short links of the type "On\-the\-fly GMP Task Generation", query parameters can include user attributes, label, ID, and other variables; when users open the link, the fixed query can display personalized page content or track the source of page visits based on user attributes and ID, parameter names need to be provided before inserting variables, multiple parameters must be separated by the "&" symbol For example, if you need to insert a user ID and user attributes, the steps required are:<br><br>   * Enter the name of the first parameter followed by an "=" sign, such as "userid=".<br><br>   * Click to insert the user ID, and select the required user ID.<br><br>   * Enter the "&" symbol.<br><br>   * Enter the name of the first parameter followed by an "=" sign, such as "username=".<br><br>   * Click to insert the user ID, and select the required user attributes.<br><br><br>For a "General WeChat Mini Program Short Link", the query parameter can contain fixed content in the format of key1=value1&key2=value2, where key1 and key2 are the parameter names, and value1 and value2 are the parameter values.<br><br>**Fallback link**: Used when the call to WeChat interface to generate the original short link fails.<br><br><span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/bf47fc25ea274a7cb0a38291b270fdea~tplv-goo7wpa0wc-image.image) </span> |


**3.4 Send SMS**

**Step1: Create a new Message Delivery Task.** 

Add a new Message Delivery Task and select the SMS Channel to be used for sending SMS.

Subject: The subject, also known as the entity/object, often refers to people, vehicles, or places that can be targeted for operational growth or insight analysis. If there are multiple analysis or outreach subjects, it is referred to as multi\-subject. **If you purchase VeCDP and additionally acquire the "Multi\-Subject Module", you can support outreach to any subject in GMP,**  such as needing to reach users and merchants, which necessitates activating multi\-subject. If this module is not purchased, then this concept and its functionalities can be disregarded.

<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/d34b87c0ec694a81a01013f1f2ee6fb6~tplv-goo7wpa0wc-image.image" width="658px" /></div>


**Step2: Enter the basic information for the task.** 

<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/e8c909e5fc2c4a0baa0555e60d89cb9c~tplv-goo7wpa0wc-image.image" width="658px" /></div>



|**Field** |**Purpose and significance of the field** |
|---|---|
|**Task Name** |Mandatory, used to distinguish between different tasks (strategies), must not be the same as other tasks |
|**Task Grouping** |Optional, allows tasks to be categorized into different groupings for subsequent analysis based on task grouping. Grouping for message delivery and process canvas are isolated; data is not shared.<br><br>If existing grouping options do not meet the requirements, new groups can be created or edited through "Manage Groups." Only project administrators and group administrators can add new groups. If there are existing message delivery tasks in a group, the group cannot be "deleted" until there are no message delivery tasks left in it. |
|**Associated Campaign** |Optional, tasks can be attributed to different campaigns, such as the "Double Eleven Campaign," for subsequent analysis based on the campaign associated with the task. Tasks involving message delivery, process canvas, or placement can be associated with the same campaign. |
|**This task is associated with the application.**  |The behavioral data generated by this task will be fed back to Datafinder under this application; if Datafinder is not purchased, this capability can be ignored. |


**Step3: Specify the target audience.** 

The audience represents the range of users this task needs to reach. The SMS channel supports four types of audience targeting: label and behavior selection, existing segments, uploaded segments, and all users. If the purchase combinations differ, the capabilities of the target audience will also vary.

If you purchase GMP along with VeCDP, you can create a new segment under "rule creation segment".

If you purchase GMP and Datafinder (without purchasing VeCDP), you can create a new segment in the existing "Segment".

**If neither is purchased, it is not possible to support creating segments on the GMP side.** 

<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/ebf0ddb26dd14bb4b3e45757937abd29~tplv-goo7wpa0wc-image.image" width="680px" /></div>


 **(1) Label and behavior selection.** 

**After purchasing VeCDP, you can create segments using the "rule creation segment" method, selecting through labels, attributes, segment packages, detailed data, and Behavioral Data.** 


|**Field** |**Meaning and purpose of the field** |
|---|---|
|**Selection conditions** |**After purchasing VeCDP, segment creation can be done using 'rule creation segment,' allowing selections through labels, attributes, segment packs, detailed data, and behavioral data, and supports filtering users by ID type of the crowd.**  Detailed operation instructions for selection can be found in the VeCDP manual (chapter: Creating Private Domain Segments); the function permissions for this selection capability are consistent with VeCDP segment edit permission, therefore, using this selection capability requires the activation of VeCDP 'Add/Delete/Edit Segments' permission, otherwise, new segments cannot be created.<br><br><span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/6d1e754d18a54670beeb257f40e6fe2f~tplv-goo7wpa0wc-image.image) </span> |
|**Sync to VeCDP Segment List** |Turning on the switch here makes the segment created in this section visible in the VeCDP segment list. The segment name is by default the task name plus the task ID. Turning off the switch will make this newly created segment invisible in the VeCDP segment list, and it cannot be used again for segment selection. Administrators can "set" the default check status.<br><br><span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/4644b69a787847bba9abefe9fcab60e6~tplv-goo7wpa0wc-image.image) </span> |
|**Audience Estimate** |After configuring the segment conditions, clicking on "Audience Estimate" calculates the number of IDs in the segment beforehand, including two types: OneID count and current channel delivery ID count. Based on the estimate, decide whether to adjust the segment selection settings. |
|**Segment Authorization** |Optional, authorize the segment generated through rule creation segment, selecting which roles can view this segment. If not authorized, viewing, editing, or copying tasks will prompt a no segment permission message. |
|**Supplementary Sending** |Optional, enter the tester's ID information, which will default this user as the target audience when the task is executed. Multiple IDs can be entered. |


When saving a draft or submitting for approval, the system will automatically create the segment, and the ID type of the segment will correspond to the target ID type of the channel, such as the SMS channel creating a segment package corresponding to mobile numbers.

 **(2) Existing segment.** 

By utilizing this feature, it directly selects the predefined segment for immediate outreach.

**Permissions required to use this feature:** 

If both GMP and VeCDP are purchased together, this feature will pull segments from VeCDP. Using this feature requires the activation of VeCDP "View Segment" permission.

If GMP is purchased along with Datafinder (without purchasing VeCDP), then this feature will pull segments from Datafinder. Using this feature requires the activation of Datafinder "User Segment" permission.

<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/9b46217563c2442ca7978fbaf461aea5~tplv-goo7wpa0wc-image.image" width="634px" /></div>



|**Field** |**Field meaning and usage** |
|---|---|
|**Segment** |You must choose a segment, as it's necessary to select the segment for this outreach. If you have purchased VeCDP's multi\-principal capabilities, the segmentation list of the task principal will be automatically pulled. |
|**Audience estimation** |After selecting a segment, the system will automatically calculate the number of sending IDs on the current channel. |
|**Create new segment** |If you purchased GMP and VeCDP, clicking this function will redirect to the VeCDP segmentation list, where you can create a new segment. If you purchased GMP and Datafinder (without purchasing VeCDP), clicking this function will support the creation of a new segment. If VeCDP or Datafinder is not purchased, this capability is not available.<br><br><span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/c050cd40847f4d08b62792a4b8ad509f~tplv-goo7wpa0wc-image.image) </span> |
|**Supplemental Sending** |Optional, you can enter the tester's ID information. Once entered, this user will be set as the target audience by default during task execution. Multiple IDs can be entered. |


 **(3) Upload Segment**

Supports uploading segments through local CSV files, but the specific upload entry is in "Message Delivery Configuration" and not completed at this step.

**Segment upload does not support event\-triggered tasks:**  Currently, segment upload only supports scheduled message delivery tasks.

**Segment upload does not support task exclusion feature:**  After choosing this selection method, the option to exclude tasks in the Message Delivery Configuration will not be displayed.

**During segment upload**: The segment ID type only supports the upload of target IDs of types sent through this channel. For instance, if it is the SMS channel, only mobile numbers can be uploaded.

**If the uploaded user IDs in the segment are not in the VeCDP system or Datafinder system** : It can still support sending. Specifically, if tags, attributes, or ID information is inserted in the content reached under these circumstances, the sending will fail.

<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/f8313ebbf2b44a88861a27699f8dd05d~tplv-goo7wpa0wc-image.image" width="610px" /></div>



|**Field** |**Field Meaning and Purpose** |
|---|---|
|**Supplemental Sending** |Optional, you can enter the tester's ID information. Once entered, this user will be set as the target audience by default during task execution. Multiple IDs can be entered. |


 **(4) All users**

No user audience filtering is applied; **all users only support Event\-Triggered: Completion of Event A and Event\-Triggered: Event A Completed & Event B Incomplete**, indicating no further user audience filters after a user trigger event, and all users meeting the event criteria will be reached.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/3e68cec3116a4714b10003c6ed5c3fb0~tplv-goo7wpa0wc-image.image) </span>

**Step3: Configuration of trigger conditions**

Supports four types: Scheduled \- One\-Time, Scheduled \- Repeated, Event\-Triggered: Completion of Event A, Event\-Triggered: Event A Completed & Event B Incomplete. This type represents the timing of the message delivery trigger.


* **Scheduled \- One\-Time**: Will only reach users at one fixed time point.

* **Scheduled \- Repeated**: Within a timeframe, it can reach users multiple times at multiple points, such as every day at 10 a.m. within March, every Friday at 4 p.m. within April.

* **Event\-Triggered: Completion of Event A**: Triggered when a user completes an action (can occur immediately/delayed), such as when a user completes actions like post liking/sharing/saving, prompting a notification of points credited. Within the valid task period, meeting the trigger conditions can trigger multiple times.

* **Event\-Triggered: Event A Completed & Event B Incomplete**: Create an event\-triggered task, which is triggered if after completing action A, another action B is not completed within a set time, such as triggering a reminder if a page is not visited 20 minutes after app launch. Within the valid task period, meeting the trigger conditions can trigger multiple times. Typically used for interruption marketing.


<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/4d711be7e3064772b0352eaab3d121ca~tplv-goo7wpa0wc-image.image" width="604px" /></div>


 **(1) Meaning of the field 'Scheduled \- One\-Time'** 


|**Field** |**Meaning and Use of the Field** |
|---|---|
|**Reach Time** |Required. If the trigger condition type is "Scheduled \- One\-Time," this field is required and represents the moment to reach the user. |
|**Approval Timeout** |Required. If by the "Reach Time" the task has not been approved, you can choose to cancel the task or execute it immediately after approval. Even if you choose "Execute Immediately After Approval," if not approved within 72 hours, the task will be automatically cancelled. |
|**Refresh Segment Before Execution** |Required.<br><br>**If GMP + VeCDP or GMP + DateFinder is purchased**<br><br>**If the selected segment is set to "On\-Demand Update"** : If 'Refresh Segment Before Execution' is checked, the system will automatically refresh the segment data 15 minutes in advance. If the task is scheduled for 15:00, the system will refresh the segment at 14:45. If an adjustment is desired for the 15\-minute interval, you can contact the project manager or the Customer Success Manager for adjustments.<br><br>**If the selected segment is updated "Daily"** : The segment will be updated at the time set during its creation.<br><br>**If the selected segment is 'Real\-Time Update'** : The segment will be updated in real\-time.<br><br>Specifically, **Scheduled \- One\-Time, rule creation segment** will by default create a segment set for 'On\-Demand Update'.<br><br><span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/2945ec636d4a4d2bacbb56b35260c81d~tplv-goo7wpa0wc-image.image) </span><br><br>**If GMP + VeCDP or GMP + DataFinder has not been purchased**<br><br>Then the system does not support refreshing segments. |
|**Segment refresh failed** |Required.<br><br>**If GMP + VeCDP or GMP + DataFinder are purchased**:<br><br>**If the chosen segment is "update on demand"** : After a refresh failure, you can opt to use the segment data currently obtained by the system for sending, or choose not to send.<br><br>**If the chosen segment is "update daily"** : A refresh failure will default to using the segment data currently obtained by the system for sending.<br><br>**If GMP + VeCDP or GMP + DataFinder are not purchased**<br><br>Then this option is not available. |


 **(2) Meaning of the field 'Scheduled \- Repeated'** 


|**Field** |**Field meaning and usage** |
|---|---|
|**Recurrence cycle** |If the trigger condition type is "Scheduled \- Repeated," then this field is required. It represents the time point for reaching the user for each recurrence cycle. |
|**Start and End Time** |If the condition type is "Scheduled \- Repeated," this field is mandatory, indicating the operational duration of the task. |
|**Approval Timeout** |Mandatory. If the "arrival time" is reached and the task has not been approved, you can choose to cancel the task or execute it immediately after approval. Even if "execute immediately after approval" is selected, if not approved within 72 hours, the task will be automatically canceled. |
|**Refresh Segment before Execution** |Mandatory.<br><br>**If you have purchased GMP + VeCDP or GMP + DataFinder**<br><br>**If the selected segment is "updated on demand,"**  if the "Refresh Segment before Execution" option is ticked, the system will default to refresh the segment data 15 minutes in advance. If the task is set for 15:00, the system will refresh the segment at 14:45. If you wish to adjust the 15\-minute interval, please contact the Project Manager or Customer Success Manager.<br><br>**If the selected segment is "updated daily",**  it will be refreshed at the time set during the creation of the segment.<br><br>**If the selected segment is "updated in real\-time",**  the segment will be updated instantly.<br><br>Specifically: **For schedule\-based, label and rule creation segments, a "on\-demand update" segment will be created by default.** <br><br><span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/7808b78d3686460fbb13af1f0e321b04~tplv-goo7wpa0wc-image.image) </span><br><br>**If GMP + VeCDP or GMP + DataFinder are not purchased,** <br><br>then the system temporarily does not support segment refresh. |
|Segment refresh failed |Required.<br><br>**If GMP + VeCDP or GMP + DataFinder were purchased,** <br><br>**If the selected segment is "refresh as needed"** : After a refresh failure, you can choose to use the current segment data obtained by the system for sending, or not send it at all.<br><br>**If the selected segment is "refresh daily"** : After a refresh failure, the system will default to using the current segment data obtained for sending.<br><br>**If GMP + VeCDP or GMP + DataFinder is not purchased**<br><br>Then, this option is not available. |


 **(3) Meaning of the field 'Event\-Triggered: Completion of Event A'** 


|**Field** |**Meaning and purpose of the field** |
|---|---|
|**Trigger Event** |Required.<br><br>**This represents the event completed by the user that triggers this process**; users who complete the event are filtered based on "Target Users," and only users who meet both "Trigger Condition + Target Users" will actually be reached.<br><br><span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/a2904e7464184eca9c9f20d55b7bfd18~tplv-goo7wpa0wc-image.image) </span><br><br>**Accumulate Completion of A / Every Completion of A**: Accumulating 3 completions of A means the user, after completing the event, will only be reached once; every 3 completions of A means that the process will be triggered each time the user completes A three times.<br><br>**Immediate Reach / Delayed Reach / Specified Delay Time / Delay to a Specific Weekday**:<br><br><br>* Immediate reach means to deliver the message immediately after the event is completed.<br><br>* Delayed reach means to delay the delivery for a relative amount of time; delaying 1 day means delaying 24 hours; you can delay up to 365 days.<br><br>* Specified delay time reach means that the delivery will only occur after waiting until a specified time after the event has occurred.<br><br><br>Delay to a specific weekday means waiting until the nearest specified weekday after the event to deliver the message. For example, if set to delay until Tuesday and the event occurs on Monday, the delivery will happen on this Tuesday; if set to delay until Tuesday and the event occurs on Wednesday, the delivery will happen on the next Tuesday.<br><br>**Common questions:** <br><br>**Event source grayed out**: If the event source is grayed out and cannot be selected, it means that the data source has not been fully integrated, and you need to contact the project manager or customer success manager.<br><br><span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/b4e81ba92b1840fba0a6cb86ca6b7690~tplv-goo7wpa0wc-image.image) </span><br><br>**Cannot select event attributes**: Some attributes are temporarily not supported for selection — whether it‘s the first day visit, the first\-time visit, or distinguishing between new and returning customers.<br><br>**How to select events related to GMP:** <br><br><br>* Search for "GMP" in the event box to inquire about GMP events, which are typically named "GMP feedback." All actions related to GMP message delivery and process canvas are included in this event. As shown in the diagram below.<br><br>* After selecting an event, the system will automatically load three attribute options that require manual entry:<br><br>   * Campaign type/task type: Refers to the GMP event that needs to be triggered, whether it's message delivery or process canvas.<br><br>   * Campaign ID/task ID: Refers to the task ID corresponding to the GMP event that needs to be triggered.<br><br>   * Indicator Name: Refers to the name of the indicator corresponding to the GMP event that needs to be triggered, for example, if successful, one can refer to indicators such as "quantity sent" or "successful delivery amount."<br><br><br><span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/15cb9b8f08044eabb57b26573ec1bee3~tplv-goo7wpa0wc-image.image) </span> |
|**Start and end time of Event A.**  |Required. This field will trigger the process during the time period when Event A occurs. |
|**Message Delivery Task end time.**  |System defaults to autofill.<br><br>After reaching the end time, the status of the message delivery task will change to "completed," and the system will no longer continue message delivery, even if Event A is delayed. |
|**Refresh the segment before execution.**  |**If GMP + VeCDP or GMP + DateFinder were purchased.** <br><br>**If the selected segment is "update on demand"** : The segment will not be refreshed.<br><br>**If the selected segment is "update daily"** : The system will refresh according to the set time. If the "rule creation segment" is used, the segment defaults to refresh every day at 06:00.<br><br>**If the selected segment is "real\-time update"** : The segment will be updated in real\-time.<br><br>Specifically: **Event\-Triggered: Completion of Event A, rule creation segment, will by default create a "daily update" segment.** <br><br><span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/cfa2cbe350d34ce18d0e8cd56054f8d0~tplv-goo7wpa0wc-image.image) </span><br><br>**If GMP + VeCDP or GMP + DateFinder were not purchased.** <br><br>The system currently does not support refreshing segments. |
|Refreshing segments failed. |Required.<br><br>**If GMP + VeCDP or GMP + DateFinder is purchased**: Even after a refresh failure, the latest data will be used for decision\-making.<br><br>**If neither GMP + VeCDP nor GMP + DateFinder is purchased**: this option is not available. |


 **(4) Meaning of the field 'Event\-Triggered: Event A Completed & Event B Incomplete'** 


|**Field** |**Field Meaning and Purpose** |
|---|---|
|**Trigger Event** |Required.<br><br>**Completing Event A triggers this process once a user completes the specified event**, filtering users as "target audience". Only users meeting both "trigger criteria + target audience" will genuinely be reached.<br><br>**Uncompleted Event B**: Unlike "Event\-Triggered: Completion of Event A," this task type requires a waiting period after completing Event A to determine if Event B is completed; if not completed, the process will be triggered.<br><br><span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/ce7a679c727d4879ab5fa30fc088fc0f~tplv-goo7wpa0wc-image.image) </span><br><br>**Accumulative Completion of Event A / Each Completion of Event A**: Completing Event A 3 times means the user will only be reached once after completion; completing Event A 3 times each means the process will be activated each time Event A is completed three times.<br><br>**Immediate Message Delivery / Delayed Message Delivery / Delayed to a Specific Time / Delayed to a Specific Day of the Week Message Delivery**:<br><br>Immediate Message Delivery happens right after the event is completed.<br><br>Delayed Message Delivery represents a delay in a relative time, delaying for 1 day means a 24\-hour delay; the maximum delay can be up to 365 days.<br><br>Delayed to a Specific Time Message Delivery means waiting until the specified time after the event occurs to reach out.<br><br>Delayed to a Specific Day of the Week Message Delivery means waiting until the nearest specified weekday after the event occurs to reach out. For example, if an event occurs on Monday and the delay is set to Tuesday, it will be reached this Tuesday; if the delay is set to Tuesday and the event occurs on Wednesday, it will be reached the following Tuesday.<br><br>**Common Questions:** <br><br>**Event Source Grayed Out**: If the event source is grayed out and cannot be selected, it indicates that the data source has not been fully integrated, and you should contact the project manager or Customer Success Manager.<br><br><span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/9d1855c1fac64153a2ec10731b97d3fe~tplv-goo7wpa0wc-image.image) </span><br><br>**Unable to select event attributes**: Certain attributes such as whether it's a first\-day visit, a first\-time visit, or whether the visitor is new or recurring, are currently unsupported.<br><br>**How to select events related to GMP:** <br><br>To search for GMP events, type "GMP" in the event box. The names usually appear as "GMP Callback". All actions related to GMP message delivery and the process canvas are included in this event. As shown in the figure below.<br><br>After selecting the event, the system will automatically load three attribute options that need to be manually entered:<br><br><br>* Activity Type/Task Type: Refers to whether the GMP event to be triggered is for message delivery or process canvas<br><br>* Campaign ID/Task ID: Refers to the task ID associated with the GMP event to be triggered<br><br>* Indicator Name: Refers to the metric name associated with the GMP event to be triggered; for example, if successful delivery is required, look for "Delivery Volume" or "Success Delivery Volume".<br><br><br><span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/0c045397b8e549c1b6a33f91112f78fd~tplv-goo7wpa0wc-image.image) </span> |
|Event A start and end time |Mandatory. All events A that occur during this period will trigger the process. |
|End time of the message delivery task |System default fill.<br><br>After reaching the end time, the status of the message delivery task becomes 'completed'. Even if Event A is delayed, the system will not continue the delivery. |
|Refresh segmentation before execution |**If GMP + VeCDP or GMP + DateFinder has been purchased**<br><br>**If the selected segment is 'on\-demand'** : the segment will not be refreshed.<br><br>**If the selected segment is 'updated daily'** : the system will refresh according to the set time. If 'rule creation segment' is used, the segment will be refreshed daily at 06:00 by default.<br><br>**If the selected segment is 'real\-time update'** : the segment will be updated in real\-time.<br><br>Uniquely, **event\-triggered: completion of Event A, rule creation segment, will by default create a "Refresh Daily" segment.** <br><br><span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/9e81ec28c3dd49fe833c9c09b4322a43~tplv-goo7wpa0wc-image.image) </span><br><br>**If GMP + VeCDP or GMP + DateFinder have not been purchased**<br><br>then the system does not support refreshing segments. |
|Segment refresh failed |Required.<br><br>**If GMP + VeCDP or GMP + DateFinder has been purchased**: The system will use the latest data for assessment even if the refresh fails.<br><br>**If GMP + VeCDP or GMP + DateFinder has not been purchased**: This option is not available. |


**Step 4: Configuration for reaching out**

This step involves filling in the content for the outreach, designing task priority, and setting frequency control/do not disturb/mutual exclusion conditions for the outreach.

<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/d6b58feb547147fd9511db1efd99ba07~tplv-goo7wpa0wc-image.image" width="439px" /></div>



|**Field** |**Meaning and purpose of the field** |
|---|---|
|**Channels** |The system defaults to the channel selected in Step1, which can be modified. After modification, the filled\-in message content will be cleared, but other data will be preserved. |
|**Start a segmentation experiment** |For detailed logic, please refer to the "A/B Experiment" section. |
|**Task Type** |Required, includes general, urgent, and notification campaigns.<br><br>**Task type affects task priority, which influences the logic of which task is triggered first when multiple tasks are activated simultaneously (i.e., when the message queue is backlogged)** : tasks with higher priority are triggered first.<br><br>Priority: Notification messages \> Urgent campaigns \> General campaigns. Each task consumes a frequency control count per each activation.<br><br>For special notification message tasks, they can still be triggered after the channel frequency control count is exhausted. |
|**Region Selection** |Required, to differentiate between domestic and international/Hong Kong/Macao/Taiwan.<br><br>**Domestic SMS Signature Instructions**: Domestic SMS consists of a signature and main content, with the signature symbol being 【】(note: full\-width). When sending an SMS, the signature must be included.<br><br>**International/Hong Kong/Macau/Taiwan SMS Signature Instructions**: The signature symbol for International/Hong Kong/Macau/Taiwan SMS is [] (note: half\-width). When sending an SMS, the signature can be included or omitted. |
|**Signature Selection** |Referring to SMS signatures, domestic SMS must include a signature, while for international/Hong Kong/Macau/Taiwan, it is optional. |
|**Template ID** |Mandatory. Select specific SMS templates, only those approved will be displayed.<br><br>Domestic template types include: verification, notification, and marketing.<br><br>International/Hong Kong/Macau/Taiwan template types include: verification and non\-verification.<br><br><span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/b3f1b2cfb19441648a15c4361ae32b7a~tplv-goo7wpa0wc-image.image) </span> |
|**Template Content** |If the template contains parameters, you need to fill in the parameter content, supporting the insertion of user attributes, user IDs, user labels, and event attributes. In addition, after inserting parameters, it is advisable to set default values for the parameters to increase the success rate of sending. If the system cannot retrieve the parameter value or the parameter value for the user is empty, it will substitute the default value for sending; if no default value is set, the sending will be canceled.<br><br>**Inserting a short link: If you need to insert a GMP short link in the reach content, you need to use the ability to insert short links on the page. If you need to track the click UV of the short links sent in the SMS, you need to choose a short link that can track UV, such as "General Short Link" or "Long Link to Short Link with Parameters".** <br><br><span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/c08a541246d94f9ea5e386402315f021~tplv-goo7wpa0wc-image.image) </span><br><br>**Inserting labels, attributes, ID**: If the 'Multi\-Subject' feature is purchased, you can insert associated subject's labels, attributes, and ID in the reach content.<br><br><span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/45190f4e3da5487dbeebb5f7708685ea~tplv-goo7wpa0wc-image.image) </span><br><br>**Inserting event attributes**: When the task trigger condition is "Event\-Triggered," you can insert the event attributes of the triggering event.<br><br><span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/825851bb6fd2470ba28b85e4799720a5~tplv-goo7wpa0wc-image.image) </span><br><br>**Inserting uploaded file parameters**: When the target audience selects "Segment Upload," you can insert uploaded file parameters by entering the header name of the corresponding column that needs to be inserted.<br><br><span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/4d828a3676f441d68fd6533d19cbabdd~tplv-goo7wpa0wc-image.image) </span><br><br>**Inserting benefits**: After turning on the function switch, you can see the entrance, click to insert the benefits configured in the GMP system, locking inventory with the task. If set to "Do Not Allow Over\-Issuance," sending will stop after exceeding the locked inventory. If set to "Allow Over\-Issuance," sending will continue with the unlocked available inventory after exceeding the locked inventory.<br><br><span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/48677aa633a748bfb9a04a5c93ee6c84~tplv-goo7wpa0wc-image.image) </span><br><br>**Inserting trajectory materials**: After turning on the function switch, you can see the entrance. Once the trajectory material is activated, it can obtain the user's WeChat authorization and accordingly count the PV/UV of the material being opened, thus it is recommended to insert trajectory material in WeChat official account messages.<br><br>**Activity Landing Page**: After enabling the feature switch, the entry can be seen, where you can insert the link to the activity landing page |
|**Word count sent** |Counts the number of words sent; SMS will be split into multiple messages if it exceeds 70 words. |
|**Test sending** |Conduct real tests on the push content, requiring the filling of target ID, variable values, etc. |
|**Upload file** |If 'Upload file' is selected in the 'Audience Users' step, you must upload the segment file in the 'Message Delivery Configuration' step. The location for uploading the segment file is below the message delivery content. You can first do a 'Template download', fill out the content, and then proceed to upload.<br><br><span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/378febb1216d45c0b98ebccc19a2520a~tplv-goo7wpa0wc-image.image) </span> |
|**Global message delivery limit** |The channel reach frequency control limit is displayed on the page according to the chosen channel frequency control. If it does not meet the requirements, you can adjust the channel frequency control by clicking "View" \-\-\> entering the "Settings Center". Note that the page will not automatically synchronize after adjusting the frequency control; you must manually update the configuration page to synchronize to the latest frequency control status.<br><br>Turning off "Global Reach Limit" means that the message sent this time will not be subject to frequency control limits of this channel or cross\-channel frequency control. |
|**Cross\-channel Frequency Control** |The current version supports setting cross\-channel frequency control, for example, Channel A + Channel B, reaching a maximum of once per day. The corresponding configuration data will be displayed here. |
|**Message Delivery Task Frequency Control** |If the current task's trigger condition is "Scheduled \- Repeated", "Event\-Triggered: Completion of Event A", or "Event\-Triggered: Event A Completed & Event B Incomplete", the user could potentially be reached multiple times. This field allows setting how frequency control is conducted within this task.<br><br><span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/181749909d00465abba73c75200d7cae~tplv-goo7wpa0wc-image.image) </span> |
|**Channel Do Not Disturb Period** |The SMS channel can ignore this field. |
|**Do Not Disturb Settings** |You can set a Do Not Disturb period, during which any messages scheduled to be sent will be restricted by the Do Not Disturb settings. |
|**Do Not Disturb Period Rules** |If filtered due to hitting Do Not Disturb conditions, you can choose to either 'Give up on this reach' or 'Continue reaching after Do Not Disturb ends'. |
|**Exclude Task** |Optional.<br><br>Refers to the chosen tasks having a mutually exclusive relationship with the current task. The target user (with the same user ID) will only be reached by one of the tasks. For example, if Task A and Task B are mutually exclusive, if a user is successfully reached by Task A, they will not be reached by Task B, and vice versa. Supports search by task name or ID, currently displaying only the first 50 task data, for more tasks please search and find. |


**Step 5: Focus on Metrics**

**This feature can be used to track users' post\-outreach conversion statistics**. "Set Focus Metrics" is off by default; toggling it on allows you to set the task's focus metrics.

<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/5e8937da3a974783ac96358fa763fba1~tplv-goo7wpa0wc-image.image" width="508px" /></div>



|**Field** |**Meaning and Purpose of Fields** |
|---|---|
|**Configuration Methods** |You can choose to "Create New Indicator" or use "Existing Indicator" directly |
|**Indicator Name** |Required.<br><br>Examples: Add to Cart, Generate Order, GMV. The indicator name entered when creating a task will be reflected on the data analysis page.<br><br><span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/58e7c35404af449d9ed9e814a9260cbb~tplv-goo7wpa0wc-image.image) </span> |
|**Manage Indicators** |There is a "Manage Indicators" entry to the right of the indicator name; clicking on it allows you to view all the indicators in the system, view their configuration rules, and delete indicators. Deleting an indicator will not affect the data already set in the task, but will affect the ability to choose it when selecting an "Existing Indicator".<br><br><span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/1bcfb332c61d400eaa5a95388fe00b8a~tplv-goo7wpa0wc-image.image) </span> |
|**Calculation Conditions**<br><br>**Calculate using real\-time behavioral data** |**Indicator Example**: Product detail page visits, add to cart, homepage views on mini\-program<br><br>**Conditions for Use**: If a behavioral data source has "real\-time action messages," you can set statistics of actions per person or per action under this data source. If you are unsure whether the data source meets the requirements, you can consult the project manager or customer success manager.<br><br>**How to Configure**: Select the data source and event, if you need to add restrictions to the event, click "Filter Conditions" to add them. For example, to count visits to the product detail page, you need to restrict the page's URL, which can be done with this function.<br><br><span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/a340ca7f98d14f12935c823e503d5952~tplv-goo7wpa0wc-image.image) </span><br><br>**Results of Data Analysis After Configuration**:<br><br>After configuration, the channel's message delivery and process canvas tasks will automatically monitor this indicator.<br><br>This indicator will account for user conversions during a specified window of time after they have been reached.<br><br>Once configured, the indicator will update in real\-time whenever a conversion event occurs. |
|**Calculation Conditions**<br><br>**Calculated through offline behavioral data** |**Examples of indicators**: visits to product detail pages, cart additions, home page views on mini\-programs<br><br>**Conditions required for use**: If a source of behavioral data updates daily as an "incremental table," you can set up the occurrence/population statistics indicators under this data source. If you are unsure whether the data source meets the requirements, you can consult the project manager or the client success manager.<br><br>**How to configure**: Select data sources and events. If you need to impose restrictions on the events, click "Filter Conditions" to add them. For instance, to count visits to a product detail page, you can restrict the URL of the product detail page using this feature.<br><br><span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/0f8ebab503804892b323eefe378fb3e8~tplv-goo7wpa0wc-image.image) </span><br><br>**Results of data analysis after configuration**:<br><br><br>* After configuration, the channel's message delivery and process canvas tasks will automatically focus on this indicator.<br><br>* The indicator will track conversions within a specified window period after users are reached.<br><br>* Once configured, as soon as a conversion event occurs, the system will calculate indicator data daily at 5, 11, 17, and 23 hours.<br><br><br>**The difference between this data source and the 'via real\-time behavioral data source'** : If 'real\-time behavior messages' are available, prioritize the 'via real\-time behavioral data source' feature; if not, use the 'via offline behavior data calculation' to perform the analysis. |
|**Calculation Conditions**<br><br>**Calculation via Detailed Data** |**Examples of indicators**: Number of Orders, GMV<br><br>**Conditions required for use**: If the detailed data is updated daily as an 'incremental table', then you can set up indicators for detailed data under this data source. If you are unsure whether this data source meets the requirements, consult the project manager or customer success manager.<br><br>**How to configure**:<br><br>Select the data source and fields, and if you need to add restrictions to the event, click 'Filter Conditions' to add them. For example, to count the number of orders and limit the product categories, you can use this function.<br><br>If you need to count the occurrences of a field, simply select "Person/Number of Times".<br><br><span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/a5ef69555b7a4f69873343886985b875~tplv-goo7wpa0wc-image.image) </span><br><br>If you need to sum up a field, simply select "Sum". For instance, the GMV metric requires summing up the product amounts.<br><br><span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/768eb91fb01449e9b247bd18b600a0be~tplv-goo7wpa0wc-image.image) </span><br><br>**What are the results of the data analysis after configuration**:<br><br><br>* After configuration, the message reach and process canvas tasks of this channel will automatically monitor the metric.<br><br>* The metric will count the user's conversions within a specified window period after being reached.<br><br>* After configuration, as long as the conversion event occurs, the system will count the metric data at 5, 11, 17, and 23 o'clock every day. |
|**Calculation Conditions**<br><br>**Combined Metrics** |**Composite Indicator**<br><br>Examples of indicators: cart addition rate, customer transaction value, SMS sending cost<br><br>After clicking, you can perform composite operations between indicators. You can select indicators or enter values.<br><br>Select indicators: only supports the selection of sent volume, delivery volume **and the indicators already selected on the current page**<br><br><span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/f130cbef790a48b0bb08a851a466270e~tplv-goo7wpa0wc-image.image) </span><br><br>Enter values: Clicking the selection box also allows direct entry of values, which are used to calculate indicators similar to "SMS sending cost."<br><br><span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/69b95c72ecf446bb8174be492086f229~tplv-goo7wpa0wc-image.image) </span> |
|**Look\-back Window** |Refers to the duration of the look\-back window for the data after the user has been reached. |
|**Do not reach after completing events** |For timing repetitive, trigger\-type tasks where a user is reached multiple times, if you want to stop reaching them after they complete a certain action, you can select this option. This capability can only be set when the selected event is "real\-time behavior data source".<br><br><span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/d26d5fde068d4931949680a38167e930~tplv-goo7wpa0wc-image.image) </span> |


You can add up to 7 focus metrics; after adding metrics, **attribution statistics involving full participation will be conducted, meaning as long as the user completes the behavior or generates an order within the window period, it will be recorded**. Example: If a user is reached by task a and task b, and both tasks have set "Mini Program Page View" as the focus metric, then the data will be counted in both tasks.

<span id="ba766285"></span>
### **4. Other SMS Scenario Solutions**

**4.1 Video SMS**

Video SMS supports sending SMS to users via "BytePlus Messaging" that contains text/image/video content. It is commonly used for marketing promotions and user recall scenarios. The video SMS feature of GMP currently only supports "BytePlus Dedicated SMS Channel" and has not yet integrated video SMS capabilities with third\-party SMS channels like AliCloud, Tencent Cloud, or Jiguang. The steps to send a video SMS are as follows:


|**Step** |**Step Description** |
|---|---|
|**Enable Video SMS** |**Enable the video SMS capability of BytePlus SMS**: Clients need to first connect with BytePlus Communication to enable the video SMS capability for the current main account. If needed, please contact the BytePlus project manager or customer success manager.<br><br>**Enable the video SMS capability on the GMP side**: If needed, please contact the BytePlus project manager or customer success manager. |
|**Apply for SMS Template** |It is currently not supported to configure video SMS templates on the GMP side; you need to go to BytePlus SMS to apply for the SMS template. Application entry: SMS Service \- Video SMS. Video SMS templates must contain at least one text component and can support video, audio, picture, and text components. Detailed operating steps can be viewed in the operation document for BytePlus SMS video messages.<br><br><span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/837c9a524fa54b988179fffa12dedd25~tplv-goo7wpa0wc-image.image) </span><br><br><span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/bab84ff511644309a364bc8e2c483392~tplv-goo7wpa0wc-image.image) </span> |
|**Create a video SMS message delivery task** |Create a message delivery task and select a video SMS template;<br><br><span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/84b8a5e52fae4dcf800eb6bc99a79f63~tplv-goo7wpa0wc-image.image) </span> |


**4.2 Send SMS focused on benefit scenarios**


|**Scenario** |**Configuration Method** |
|---|---|
|**Points Expiry Reminder** |Target Audience: Select users whose points are about to expire<br><br><span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/c682e560de7f42659bda19edf0bc919e~tplv-goo7wpa0wc-image.image) </span><br><br>Trigger Condition: Scheduled repetition, running daily to identify users whose points are expiring<br><br><span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/688d48c71a0f46f9839807b54173a7b3~tplv-goo7wpa0wc-image.image) </span><br><br>Message Delivery Content: Fill in the SMS content<br><br><span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/388f3a882160487a87c011690a082beb~tplv-goo7wpa0wc-image.image) </span> |
|**Distribute coupons and send SMS notifications** |The current process requires experimentation on the Process Canvas; for details, please refer to the Process Canvas section. |


<span id="123373d0"></span>
## **1.2 Webhook**

<span id="3b867b93"></span>
### **1. Product Overview**

Webhook is a "pipeline" that serves as a bridge for information, connecting different applications or systems. If you want to integrate a system with the GMP marketing platform to send in\-app messages or external calls, you can achieve message delivery through this "Webhook pipeline."

<span id="bf069729"></span>
### **2. Usage Restrictions**


| |Detailed Explanation |
|---|---|
|**Complete the channel integration** |This step is completed by technical personnel, who can consult the "Technical Integration Document" for the necessary configuration. |
|**Activate GMP permissions** |The administrator grants permission to create tasks; the permission path is: activate permissions in GMP under "Content Management \- Webhook Template," which can optionally be activated.<br><br>The administrator grants permission to create tasks; the permission path is: activate permissions in GMP under "Message Delivery \- Message Delivery Task \- New/View/Edit/Delete."<br><br>The administrator grants viewing permissions for the Webhook channel; the permission path is: Management Center \- Channel Management \- Webhook \- View. |
|**Activate segmentation permissions** |Activation of segmentation permissions falls into 3 scenarios:<br><br>If you purchased VeCDP, you need to enable the "Segment \- Private Domain Segment \- View/Add/Delete Segment" permission in VeCDP. Once authorized, you can use the segment function in task creation.<br><br>If you only purchased Datafinder without VeCDP, you need to enable the "Segment" permission in Datafinder. Once authorized, you can use the segment function in task creation.<br><br>If you have not purchased either VeCDP or Datafinder, you can ignore this permission. |


<span id="224dce45"></span>
### **3. Feature Description**

**3.1 Prepare Webhook Templates**

If the content sent via Webhook involves the concept of templates (such as outbound call templates), then technical personnel will need to integrate with "Webhook Templates". After the integration is complete, you can view the template fields retrieved by GMP in GMP \- Content Management \- Webhook Templates. Different Webhook channels can integrate different Webhook Templates; the system will display template content, creator, template number, and other information.

<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/dbad0eb8907048b3bd105feb4669ef41~tplv-goo7wpa0wc-image.image" width="688px" /></div>


**3.2 Send Webhook**

**Step 1: Create a new Message Delivery Task**

Add a new Message Delivery Task, choose the subject and the SMS channel.

Subject: A subject, also referred to as an entity/object, typically represents individuals, vehicles, venues, etc., that can be targeted for operational growth or insight analysis. If there are multiple subjects for analysis or outreach, it is referred to as multi\-subject. **If you purchase VeCDP and additionally buy the 'Multi\-Subject Module', you can support targeting any subject in GMP**, for instance, to target users or merchants, you need to activate the multi\-subject. If you did not purchase this module, you can ignore this concept and function description.

<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/88569fc7070b42a08a243ed3311d1862~tplv-goo7wpa0wc-image.image" width="439px" /></div>


**Step 2: Fill in the basic information for the task**

<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/3287253ae04a40d793b33e8dfbe9c0e3~tplv-goo7wpa0wc-image.image" width="439px" /></div>



|**Field** |**Field Meaning and Purpose** |
|---|---|
|**Task Name** |Required, used to differentiate between different tasks (strategies), must not be identical to other task names. |
|**Task Grouping** |Optional, allows for placing different tasks in different groups for subsequent analysis based on task grouping. Message Delivery and the process canvas groups are isolated; their data are not interconnected.<br><br>If the existing task grouping options do not meet your needs, you can create or edit them via "Manage Groupings". Only project administrators and group administrators can add new groups. If there are Message Delivery Tasks under a group, it cannot be "Deleted." A group can only be deleted when there are no Message Delivery Tasks left under it. |
|**Associated Campaigns** |Optional, you can categorize tasks into different campaigns, such as "Double Eleven Campaign," for subsequent analysis based on the tasks' associated campaigns. You can link Message Delivery, Process Canvas, and Placement tasks to the same campaign. |
|**This task is associated with an application** |It represents that the data from the Message Delivery behavior generated by this task will be fed back to the application under Datafinder. If you haven't purchased Datafinder, you can ignore this feature. |


**Step3: Fill Out the Target Audience**

The target audience represents the range of users that need to be reached for this task. The target audience supports four methods: rule creation segment, existing segment, upload segment, and all users. If the purchase combinations differ, the capabilities of the target audience will also differ. If both GMP and VeCDP are purchased, a new segment can be created under 'rule creation segment'; if GMP and Datafinder are purchased (without purchasing VeCDP), a new segment can be created under 'existing segment'; **If neither is purchased, it is not supported to create segments on the GMP side.** 

<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/a546a1d241334a32a35cc59f5505f759~tplv-goo7wpa0wc-image.image" width="439px" /></div>


 **(1) Rule Creation Segment**

**After purchasing VeCDP, one can use the 'rule creation segment' method to create a segment**, which can be done through labels, attributes, segment packs, detailed data, and behavioral data.


|**Field** |**Field meaning and purpose** |
|---|---|
|**Filter Conditions** |**After purchasing VeCDP, you can create segments using the "rule creation segment" method,**  allowing segmentation through labels, attributes, segment packages, detailed data, behavioral data, and supports filtering by ID type of the crowd. Detailed operational instructions for segmentation are available in the VeCDP manual (Chapter: Creating Private Domain Segments). The functionality permissions for this segmentation capability are consistent with those for VeCDP segment editing. Therefore, to use this segmentation ability, it is necessary to enable the VeCDP "Add, Delete, Edit Segment" permissions; otherwise, new segments cannot be created.<br><br><span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/6147f78dd73a47bda421f747501460a1~tplv-goo7wpa0wc-image.image) </span> |
|**Sync to CDP Segment List** |Turning on the switch will make the segment created here visible in the VeCDP segment list, with the segment name defaulting to the Message Delivery Task Name + Message Delivery Task ID. Turning off the switch will make the segment created this time invisible in the VeCDP segment list, and it cannot be used again for segment filtering. Administrators can "Set" the default checked status.<br><br><span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/c42cf98b994742a1bcd9ec73805df4ee~tplv-goo7wpa0wc-image.image) </span> |
|**Audience Estimation** |After configuring the segment conditions, click "Audience Estimation" to calculate the number of IDs in the segment in advance. The ID count includes two types: OneID count and the count of IDs currently sent via the channel. The estimate results can help decide whether to adjust the segment filtering conditions. |
|**Segment Authorization** |Optional: Authorize the role creation segment and the action ring selection segment, allowing selected roles to view permissions of the segment. If authorization is not given, prompts stating "No segment permission" will appear when viewing, editing, or copying tasks. |
|**Resend** |Optional: You can enter the ID information of testers. Once entered, this user will be set as the target audience by default during task execution. Multiple IDs can be entered. |


When saving a draft or submitting for approval, the system will automatically create the segment, and the segment's ID type will correspond to the target ID type of the channel, such as creating a segment pack with mobile numbers for the SMS channel.

 **(2) Existing Segment**

Through this function, directly select the already defined segment for reaching out.

**Permissions required to use this feature:** 

If GMP and VeCDP are purchased together, this feature will pull the segments from VeCDP. To use this feature, the 'View Segment' permission for VeCDP is required.

If GMP and Datafinder are purchased together (without purchasing VeCDP), this feature will pull the segments from Datafinder. To use this feature, the 'User Segment' permission for Datafinder is required.

<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/814df19abc4c405ab3805136bf9c4823~tplv-goo7wpa0wc-image.image" width="439px" /></div>



|**Field** |**Meaning and purpose of the field** |
|---|---|
|**Segment List** |Required: You need to select the segment for this Message Delivery Task. If the BytePlus VeCDP multi\-subject capability has been purchased, this list will automatically retrieve the segment list of the task's subject. |
|**Audience Estimate** |After selecting a segment, the system will automatically calculate the number of sent IDs for the current channel. |
|**Create Segment** |If you purchase GMP and VeCDP together, clicking this function will direct you to the VeCDP segment list, where you can create new segments. If you purchase GMP and Datafinder (without purchasing VeCDP), clicking this function will allow you to create new segments. If VeCDP or Datafinder is not purchased, this functionality will not be available.<br><br><span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/130c0e9fd34848878f7e4108a186b28a~tplv-goo7wpa0wc-image.image) </span> |
|Additional Send |Optional, you can enter tester IDs, and after filling it out, the system will default to these users as the target audience during task execution. Multiple IDs can be entered. |


 **(3) Upload Segments**

Supports uploading segments through local CSV files, but the actual upload portal is in "Message Delivery Configuration," not at this step.

**Segment upload does not support event\-triggered tasks**: Currently, segment upload only supports scheduled message delivery tasks.

**Segment upload does not support task exclusion feature**: After choosing this selection method, the option to exclude tasks in the message delivery configuration will not be displayed.

**During segment upload**: Only the type of segment ID related to the channel’s target ID can be uploaded. If it is an SMS channel, only phone numbers can be uploaded.

**If the user ID uploaded in the segment is not in the VeCDP system or Datafinder system,**  it can still support sending. Specifically, if tags, properties, or ID information are inserted into the delivery content in this case, the sending will fail.

<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/060a2dadee9a45a79ecde60253ae86b0~tplv-goo7wpa0wc-image.image" width="439px" /></div>



|**Field** |**Field Meaning and Purpose** |
|---|---|
|**Additional Sending** |Optional, you can enter the ID of a tester; once entered, the system will default this user as the target audience when executing the task. Multiple IDs can be entered. |


 **(4) All Users**

Represents all users under the current project. **All users only support Event\-Triggered: Event A, Event\-Triggered: Event A Completed & Event B Incomplete,**  meaning that after triggering an event, no further audience filtering is conducted, and all users meeting the event conditions will be reached.

<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/3ff5a810e223426089b014da24d59743~tplv-goo7wpa0wc-image.image" width="439px" /></div>


**Step3: Trigger Condition Configuration**

**Supports four methods: Scheduled \- One\-Time, Scheduled \- Repeated, Event\-Triggered: Completion of Event A, Event\-Triggered: Event A Completed & Event B Incomplete.** 

**Message Delivery Task Type**: Represents the trigger timing of this message delivery.


* **Scheduled \- One\-Time**: Will only reach users at a fixed point in time.

* **Scheduled \- Repeated**: Within a time range, users can be reached multiple times at fixed points, such as every day at 10 AM in March.

* **Event\-Triggered: Completion of Event A**: Triggers when a user completes a certain behavior (can be immediate/delayed), such as triggering a points credit reminder when a user completes post bookmarking/liking/sharing. During the valid period of the task, multiple triggers can be achieved as long as the triggering conditions are met.

* **Event\-Triggered: Event A Completed & Event B Incomplete**: Create event\-triggered tasks that activate when a user performs a certain action A and does not complete another action B within a certain period, such as launching the application and not visiting a page after 20 minutes triggering a reminder. During the valid period of the task, multiple triggers can be achieved as long as the triggering conditions are met. This is commonly used in interrupted marketing.


<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/bd6d107d3cb443a8b58d846514f0a4be~tplv-goo7wpa0wc-image.image" width="439px" /></div>


 **(1) Meaning of the field for Scheduled \- One\-Time**


|**Field** |**Field Meaning and Purpose** |
|---|---|
|**Delivery Time** |Mandatory. If the trigger condition type is <Scheduled \- One\-Time\>, this field is mandatory and represents the time point when the user is reached. |
|**Approval Timeout** |Required. If the task has not been approved by the 'reach time,' you may choose to cancel the task or execute it immediately after approval. Even if 'execute immediately after approval' is selected, if the task is not approved within 72 hours, it will be automatically canceled. |
|**Refresh Segment Before Execution** |Required.<br><br>**If you have purchased GMP + VeCDP or GMP + DateFinder**<br><br>**If the selected Segment is 'update on demand'** : If 'Refresh Segment Before Execution' is checked, the system will default to refresh segment data 15 minutes in advance. For example, if the task executes at 15:00, the system will refresh the segment at 14:45. If you wish to adjust the 15\-minute interval, you can contact the project manager or customer success manager.<br><br>**If the selected Segment is 'updated daily'** : Then, the segment will be updated according to the time set during the creation of the segment.<br><br>**If the selected segment is "real\-time update"** : the segment will be updated in real time.<br><br>Specifically: **Scheduled \- One\-Time, rule creation segment will by default create a "on\-demand update" segment.** <br><br><span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/c30e2159893d43e6a48aa409eb78a8be~tplv-goo7wpa0wc-image.image) </span><br><br>**If GMP + VeCDP or GMP + DateFinder has not been purchased**<br><br>The system does not support refreshing segments temporarily. |
|**Refresh segment failed** |Required.<br><br>**If GMP + VeCDP has been purchased or GMP + DateFinder has been purchased:** <br><br>**If the selected segment is "on\-demand update"** : After a refresh failure, you can choose to use the segment data currently obtained by the system for sending, or not send at all.<br><br>**If the selected segment is "daily update"** : In case of a refresh failure, it will by default use the segment data currently obtained by the system for sending.<br><br>**If GMP + VeCDP or GMP + DateFinder has not been purchased**<br><br>This option is not available. |


 **(2) Meaning of the field for Scheduled \- Repeated**


|**Field** |**Field meaning and usage** |
|---|---|
|**Recurrence cycle** |If the trigger condition type is "Scheduled \- Repeated", this field is required, representing the time point when users are reached for each cycle. |
|**Start and end time** |If the trigger condition type is "Scheduled \- Repeated", this field is required, representing the running duration of the task. |
|**Approval timeout** |Required. If the "Message Delivery Time" is reached and the task has not been approved, the task can be canceled, or approved and executed immediately thereafter. Even if the option "Execute immediately after approval" is selected, if the task is not approved within 72 hours, it will be automatically cancelled. |
|**Refresh the segment before execution** |Required.<br><br>**If GMP + VeCDP or GMP + DateFinder is purchased**<br><br>**If the selected segment is "updated on demand"** : If "Refresh the segment before execution" is checked, the system will default to refreshing the data of the segment 15 minutes beforehand. For example, if the task is scheduled at 15:00, the system will refresh the segment at 14:45. If adjustments are desired for the 15\-minute interval, contact the project manager or customer success manager.<br><br>**If the selected segment is "updated daily"** : It will be updated at the time set when the segment was created.<br><br>**If the selected segment is "updated in real\-time"** : The segment will be updated in real\-time.<br><br>Specifically: **Scheduled \- Repeated, rule creation segment** will default to creating a “on\-demand update” segment.<br><br><span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/8598c75e7ac248ae849ab8185dba9d33~tplv-goo7wpa0wc-image.image) </span><br><br>**If GMP + VeCDP or GMP + DateFinder is not purchased**<br><br>the system temporarily does not support refreshing segments. |
|**Segment refresh failed** |Mandatory.<br><br>**If GMP + VeCDP or GMP + DateFinder is purchased**<br><br>**If the selected segment is "on\-demand update"** : After a refresh failure, you can choose to use the segment data currently obtained by the system for sending or choose not to send.<br><br>**If the selected segment is "updated daily"** : In case of a refresh failure, the system will default to using the current segment obtained for sending.<br><br>**If GMP + VeCDP or GMP + DateFinder is not purchased**<br><br>then this option is not available. |


 **(3) Meaning of the field for Event\-Triggered: Completion of Event A**


|**Field** |**Meaning and Purpose of Fields** |
|---|---|
|Trigger Event |Required.<br><br>**This represents the event that must be completed by a user to trigger this process**, only users who also meet the "Audience Users" will be targeted based on "Trigger Condition + Audience Users".<br><br><span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/e5b208e92894407abe9c376d930e7b34~tplv-goo7wpa0wc-image.image) </span><br><br>**Cumulative Completing A / Completing A per Trigger**: Completing event A 3 times means it will trigger the process once after the events; Completing A every 3 times means it will trigger the process execution each time A is completed 3 times.<br><br>**Immediate Delivery / Delayed Delivery / Delayed Specific Time/Delay Until Specific Day of the Week**:<br><br><br>* Immediate Delivery means the message is delivered immediately after the event is completed.<br><br>* Delayed Delivery means delaying the delivery for a relative time frame, delaying by 1 day means a 24\-hour delay; the maximum delay can be up to 365 days.<br><br>* Delivery after Delayed Specific Time means waiting until a specified time after the event has occurred to make the delivery.<br><br><br>Delay Until a Specific Day of the Week means waiting for the next specific day of the week after the event has occurred to make the delivery. For example, setting a delay to Tuesday means if an event occurs on Monday, it will be triggered on this Tuesday; if set to Tuesday and an event happens on Wednesday, it will be triggered on the following Tuesday.<br><br>**Common Questions:** <br><br>**Event Source Disabled**: If the event source is disabled and cannot be selected, it means that the data source has not been integrated yet. Contact the project manager or the customer success manager.<br><br><span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/542f689c5c0d4c20a47aeb2d7a3b323a~tplv-goo7wpa0wc-image.image) </span><br><br>**Event Attribute Unavailable**: Certain attributes do not support selection at the moment — whether it's the first day visit, first time visit, or new vs. returning customer.<br><br>**How to Select GMP Related Events:** <br><br><br>* To look up GMP events, search 'GMP' within the event box. The name is usually 'GMP Return', and all actions related to GMP message delivery and process canvas are included in this event. As shown in the figure below.<br><br>* After selecting the event, the system will automatically load three attribute options that need to be manually filled in:<br><br>   * Activity Type/Task Type: Whether the triggered GMP event is for message delivery or process canvas.<br><br>   * Activity ID/Task ID: The task ID corresponding to the GMP event that needs to be triggered.<br><br>   * Indicator Name: The name of the indicator corresponding to the GMP event to be triggered, such as if successful, one can find the "Sent Volume" or "Successful Reach Volume" indicators.<br><br><br><span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/73a5be63916944288ea7d937a2457056~tplv-goo7wpa0wc-image.image) </span> |
|**Event A Start and End Time** |Mandatory. The events occurring in this time period will trigger the process. |
|**Message Delivery Task End Time** |System default fill.<br><br>After reaching the end time, the message delivery task status changes to completed, even if Event A arrives late, the system will not continue the delivery. |
|**Refresh Before Execution** |**If GMP + VeCDP or GMP + DateFinder is purchased**<br><br>**If the selected segment is "on\-demand update"** : the segment will not be refreshed.<br><br>**If the selected segment is 'Updated Daily'** : the system will refresh according to the set time. If 'Label and Behavioural Selection' is used, the segment will be automatically refreshed daily at 06:00.<br><br>**If the selected segment is 'Real\-time Update'** : the segment will be updated in real time.<br><br>Specifically: **Event\-Triggered: Completion of Event A, Label and Behavioural Selection, will by default create a 'Daily Updated' segment.** <br><br><span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/f1d3122b2d934d31bd60ae5ff68cc73c~tplv-goo7wpa0wc-image.image) </span><br><br>**If GMP + VeCDP or GMP + DateFinder are not purchased**<br><br>the system does not support segment refresh. |
|**Segment refresh failed** |Mandatory.<br><br>**If GMP + VeCDP or GMP + DateFinder were purchased**: even if refreshing fails, the latest data will still be used for decision\-making.<br><br>**If GMP + VeCDP or GMP + DateFinder were not purchased**: this option is not available. |


 **(4) Meaning of the field for Event\-Triggered: Event A Completed & Event B Incomplete**


|**Field** |**Meaning and Purpose of the Field** |
|---|---|
|**Trigger Event** |Mandatory.<br><br>**Completing Event A represents the event a user completes to trigger this process**, and users who have completed this event will be filtered based on 'target audience'. Only users who fulfill both 'trigger condition and target audience' will actually be reached.<br><br>**Event B Not Completed:**  Unlike 'Event\-Triggered: Completion of Event A', this task type waits for a period after completing Event A to determine if Event B is completed; the process is triggered if not completed.<br><br><span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/0935f439d3c44d06b830db7b715cf63c~tplv-goo7wpa0wc-image.image) </span><br><br>**Cumulative Completion of A / Each Completion of A**: Cumulative completion of A 3 times means the user is reached only once after completing the event; each completion of A 3 times means the process is triggered each time the user completes A three times.<br><br>**Immediate Reach / Delayed Reach / Delay Specify Time/Delay to a Specific Day of the Week:** <br><br>Immediate reach means reaching the user immediately after the completion of the event.<br><br>Delayed reach means delaying reach by a relative time; delaying by 1 day means a 24\-hour delay; it is possible to delay up to 365 days.<br><br>Delaying a specific time until an event is considered to occur only after waiting until the specified time.<br><br>Delaying until a specific day of the week means waiting until the next occurrence of that weekday after the event happens. For example, if you set a delay until Tuesday and the event occurs on Monday, it will be reached this Tuesday; if the delay is set until Tuesday but the event occurs on Wednesday, it will be reached the following Tuesday.<br><br>**Frequently Asked Questions:** <br><br>**The event source is greyed out**: If you cannot select the event source because it is greyed out, it means that the data source has not been integrated yet, and you need to contact the project manager or Customer Success Manager.<br><br><span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/d2b009cb44c8475bb092f57a9d5d27b3~tplv-goo7wpa0wc-image.image) </span><br><br>**Unable to select event attributes**: Some attributes are temporarily not supported for selection — whether it is the first day visit, first\-time visit, or distinguishing new versus returning customers.<br><br>**How to select events related to GMP:** <br><br><br>* Search for 'GMP' within the event box to find events related to GMP, usually named 'GMP Transmission,' and all activities in the GMP message delivery and process canvas are included in this event. As shown in the diagram below.<br><br>* After selecting the event, the system will automatically load three attribute options, which need to be manually filled in:<br><br>   * Campaign type/task type: The event that needs to be triggered in GMP is either message delivery or process canvas<br><br>   * Campaign ID/task ID: The event to be triggered in GMP corresponds to the task ID<br><br>   * Indicator Name: What is the name of the indicator corresponding to the event that needs to be triggered in GMP, for example, if successful sending, you can find indicators like "sending volume" or "successful delivery volume."<br><br><br><span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/708661e4708441288998476da07417e4~tplv-goo7wpa0wc-image.image) </span> |
|**Event A start and end time** |Required. During this time period, any occurrence of event A will trigger the process. |
|**Message Delivery Task end time** |System default fill.<br><br>After reaching the end time, the status of the message delivery task becomes ended, and even if event A is delayed, the system will not continue the message delivery. |
|**Refresh before execution** |**If GMP + VeCDP or GMP + DateFinder are purchased**<br><br>**If the selected segment is 'Update on Demand'** : the segment will not be refreshed.<br><br>**If the selected segment is 'Update Daily'** : the system will refresh according to the set time. If 'Label and Behavior\-based Segmentation' is used, the segment will be refreshed daily at 06:00 by default.<br><br>**If the selected segment is 'Real\-time Update'** : the segment will be updated in real time.<br><br>Specifically, **Event\-Triggered: Completion of Event A, with label and behavior\-based segmentation, will by default create a 'Daily Update' segment.** <br><br><span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/5cab79367b674479b97e66b9d9fd42ab~tplv-goo7wpa0wc-image.image) </span><br><br>**If GMP + VeCDP or GMP + DateFinder are not purchased**<br><br>Then the system does not support segment refresh. |
|**Segment refresh failed** |Required.<br><br>**If GMP + VeCDP or GMP + DateFinder is purchased**: The system will use the latest data for evaluation even after a refresh failure.<br><br>**If GMP + VeCDP or GMP + DateFinder is not purchased**: This option will not be available. |


**Step4: Message Delivery Configuration**

This step involves filling in the content for message delivery and setting frequency control/do not disturb/mutual exclusion conditions.

<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/5e53ae763ff24691835ae160f37d4e14~tplv-goo7wpa0wc-image.image" width="439px" /></div>



|**Field** |**Field Meaning and Purpose** |
|---|---|
|**Channels** |The system will default to the channel selected in Step1, which can be modified. After modification, the entered message delivery content will be cleared, but other data will be retained. |
|**Enable Split Testing** |For detailed logic, please refer to the "A/B Experiment" section |
|**Task Type** |Mandatory, includes regular, urgent, and notification campaigns.<br><br>**Task type affects task priority, and task priority influences which task is triggered first when multiple tasks are triggered simultaneously (when a backlog occurs in the message queue being sent)** : higher priority tasks are triggered first.<br><br>Priority: Notification messages \> Urgent campaigns \> Regular campaigns, where each task triggers once, consuming a channel frequency control count.<br><br>For specific notification message type tasks, they can still be triggered after the channel frequency control count is exhausted. |
|**Message Delivery Content** |Supports insertion of user attributes, user ID, labels, and event attributes. Additionally, after inserting parameters, it is recommended to set default values to increase the success rate of sending. If the system cannot retrieve a parameter value or the user’s parameter value is empty, the default value will be used for sending; if no default value is set, sending will be cancelled.<br><br>**Inserting a short link: If a GMP short link needs to be added to the message delivery content, the ability to insert a short link on the page must be used, otherwise the short link click data cannot be tracked.** <br><br><span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/056f003d0b1642bf8fd1cfe4af4da57c~tplv-goo7wpa0wc-image.image) </span><br><br>**Inserting labels, attributes, ID**: If the "multiple subjects" capability is purchased, labels, attributes, and IDs of the associated subjects can be inserted into the message delivery content.<br><br><span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/8b2fd24238254ef9a0f99cd08b2eeeb5~tplv-goo7wpa0wc-image.image) </span><br><br>**Inserting event attributes**: When the task trigger condition is "Event\-Triggered," the event properties of the triggering event can be inserted.<br><br><span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/bc011bf0b4b346758595f88fe46eccd6~tplv-goo7wpa0wc-image.image) </span><br><br>**Insert Upload File Parameters**: When the target audience selects "Segment Upload," they can insert upload file parameters. Enter the header name of the column containing the content to be inserted.<br><br><span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/1f60cfb209ad4ac49278fc5f12a5b692~tplv-goo7wpa0wc-image.image) </span><br><br>**Insert Benefit**: After enabling the feature switch, the entry becomes visible. Click to insert the benefits configured in the GMP system. Benefits can be locked as stock with the task; stock will stop being sent if "Over\-release Not Allowed" is set or continue with available stock not locked if "Over\-release Allowed" is set.<br><br><span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/0b974e7c9cf54bba8095b2deeb2d3a82~tplv-goo7wpa0wc-image.image) </span><br><br>**Insert Material**: Materials from the material management can be inserted.<br><br>**Insert Copy**: Copies from material management can be inserted.<br><br>**Insert Trajectory Material**: After enabling the feature switch, the entry becomes visible. Once trajectory materials are opened, users' openings of the material, authenticated via WeChat, can be tracked to count PV/UV. Thus, it's advised to include trajectory materials in WeChat public account messages.<br><br>**Insert Activity Landing Page**: After enabling the feature switch, the entry becomes visible. An activity landing page link can be inserted.<br><br>Failed to find the desired tag or attribute: There could be 2 reasons:<br><br><br>* To improve task execution performance, attributes and tags need to be loaded into high\-speed storage before they can be inserted. If the desired attributes or tags are not found, the administrator can hover over the link and go to CDP to import the corresponding attributes or tags. After import, the settings will be effectively used by default, and re\-import is not required<br><br>* You do not have the permission for this label |
|**Test sending** |To conduct an actual test of the push content, you need to fill in the target ID and variable values |
|**Upload file** |If you selected "Upload File" in the "Target Users" step, you must upload a segmentation file in the "Reach Configuration" step The upload location for the segmentation file is below the reach content You can first perform a "Template Download", fill in the content, and then upload it<br><br><span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/63ab49044e764339a11ce3ec420f468c~tplv-goo7wpa0wc-image.image) </span> |
|**Global message delivery restrictions** |This is a channel frequency control restriction. The page displays the selected channel's frequency control. If it does not meet your needs, you can click "View" \-\-\> go to "Settings Center" to adjust the frequency control Note, after the frequency control adjustment, the page will not sync automatically. You must manually refresh the configuration page to sync to the latest frequency control situation.<br><br>If the "Global Reach Limit" is turned off, it indicates that the messages sent this time will not be subject to the frequency control limitations of this channel or cross\-channel. |
|**Cross\-channel Frequency Control** |The current version supports setting up cross\-channel frequency control, like Channel A + Channel B, with a maximum reach of once per day. The corresponding configuration data will be displayed here. |
|**Message Delivery Task Frequency Control** |If the current task's trigger conditions are "Scheduled \- Repeated," "Event\-Triggered: Completion of Event A," or "Event\-Triggered: Event A Completed & Event B Incomplete," then a user may be reached multiple times. This field allows setting how frequency control should be managed within this task for the users.<br><br><span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/ce0d0e57b7d14abc884cfe59dda628e9~tplv-goo7wpa0wc-image.image) </span> |
|**Channel Do Not Disturb Period** |This field can be ignored for SMS channels. |
|**Do Not Disturb Settings** |You can set a Do Not Disturb Period, and if a message is scheduled during this period, it will be restricted by Do Not Disturb. |
|**Do Not Disturb reach rules** |If filtered due to hitting Do Not Disturb conditions, you can choose to "Abandon this reach" or "Continue reaching after Do Not Disturb ends." |
|**Exclusion Task** |Optional.<br><br>It means the selected task has a mutually exclusive relationship with the current task, and the target user (with the same user ID) will only be successfully reached by one of the tasks. That is, Task A and Task B are mutually exclusive. If a user is successfully reached by Task A, they will not be reached by Task B, and vice versa. Supports searching by task name or ID, currently only displaying the first 50 tasks. For more tasks, please search. |


**Step 5: Focus on Metrics**

**This feature can be used to track conversions achieved by users after being reached**. "Set Focus Metrics" is off by default. Once switched on, you can set focus metrics for the task.

<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/57e4fb09a0304ff784d36a05c57b79b7~tplv-goo7wpa0wc-image.image" width="564px" /></div>



|**Field** |**Meaning and purpose of the field** |
|---|---|
|**Setting Method** |You can choose "Create New Indicator" or use "Existing Indicator" directly |
|**Indicator Name** |Required.<br><br>Examples: Add to Cart, Generate Order, GMV. When creating a task, the indicator name you fill in will be reflected on the data analysis page.<br><br><span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/eaea838f66124c81846d2ce64002aef3~tplv-goo7wpa0wc-image.image) </span> |
|**Manage Indicators** |To the right of the indicator name, there is an "Manage Indicators" entry, which upon clicking allows you to view all the indicators in the system, see the configuration rules for indicators, and also delete indicators. Deleting an indicator will not affect the data already set in the task; it only affects the ability to select when choosing an existing indicator.<br><br><span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/3ddacf497ec94fcebec65b518ce5d6ea~tplv-goo7wpa0wc-image.image) </span> |
|**Calculation Conditions**<br><br>**Calculated using real\-time behavioral data** |**Indicator examples**: Product detail page views, added to cart, Home page views of mini\-programs<br><br>**Conditions for usage**: If a data source has "real\-time behavior messages," then it is possible to set indicators for counting instances or unique visitors of real\-time behaviors under that data source. If you are unsure whether a data source meets the requirements, you can consult a project manager or a customer success manager.<br><br>**How to configure**: Select data sources and events, if you need to impose restrictions on events, click "Filter Conditions" to add them. For example, to compile statistics on product detail page views, if it's necessary to restrict the product detail page address, then you can use this feature.<br><br><span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/da25e6929a094848bb5b5fc89a1efaf1~tplv-goo7wpa0wc-image.image) </span><br><br>**Results of data analysis after configuration**:<br><br><br>* After configuration, message reach and process canvas tasks will automatically monitor the indicator.<br><br>* The indicator will count user conversions during a specified window period after being reached.<br><br>* After configuration, as long as the conversion event occurs, the indicator will be updated in real time. |
|**Calculation Conditions**<br><br>**Calculate through offline behavioral data** |**Examples of indicators**: product detail page views, add\-to\-cart amount, mini program home page views<br><br>**Conditions for usage**: If a behavioral data source is updated daily as an 'incremental table', then one can set up count/power statistics indicators for the behaviors under that data source. If you are unsure whether the data source meets the conditions, you can consult the project manager or customer success manager.<br><br>**How to configure**: Select data sources and events; if you need to add constraints on the events, you can click 'Filter Conditions' to add them. For example, when calculating product detail page views, if it's necessary to restrict the product detail page address, this function can be utilized.<br><br><span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/b48d7a8370a0436ab84ab3447eb864f8~tplv-goo7wpa0wc-image.image) </span><br><br>**Results of data analysis after configuration**:<br><br><br>* After configuration, the Message Delivery and Process Canvas tasks will automatically monitor this indicator.<br><br>* This indicator will calculate user conversion within a specified window period after they have been reached.<br><br>* After configuration, the system will compute metric data every day at 5, 11, 17, and 23 hours whenever a conversion event occurs<br><br><br>**The difference between this data source and the one that 'counts via real\-time behavioral data source'** : If there are 'real\-time behavioral messages', the 'real\-time behavioral data source' function should be used preferentially; if not, 'calculation via offline behavioral data' can be used instead |
|**Calculation Conditions**<br><br>**Calculation based on detailed data** |**Examples of indicators**: Number of orders, GMV<br><br>**Conditions required for use**: If a detailed data is updated daily as an 'incremental table', then it is possible to set metrics for detailed behavior data under this data source If you are unsure whether this data source meets the requirements, you can consult the project manager or customer success manager<br><br>**How to configure it**:<br><br>Select a data source and fields, if there is a need to impose conditions on events, you can click 'Filter Conditions' to add them For example, to count order volume, if there is a need to restrict product categories, this function can be utilized<br><br>If you need to count the occurrences of a field, simply choose "Number of People/Occurrences".<br><br><span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/0a004607a7624fb0b514194747b96e41~tplv-goo7wpa0wc-image.image) </span><br><br>If you need to sum the fields, simply select "Sum". For instance, the GMV indicator requires summing the amount of goods.<br><br><span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/c17e1c9cb0c34a9083daac95641ba97b~tplv-goo7wpa0wc-image.image) </span><br><br>**What does the result of data analysis look like after configuration?** <br><br><br>* After configuration, the message reach and process canvas tasks of this channel will automatically focus on this indicator.<br><br>* This indicator will track user conversions within a specified window after being reached.<br><br>* After configuration, as long as a conversion event occurs, the system will calculate the indicator data at 5, 11, 17, and 23 o'clock each day. |
|**Calculation Conditions**<br><br>**Composite Indicators** |**Composite Indicators**<br><br>Examples of indicators: add\-to\-cart rate, per\-customer transaction, SMS sending cost<br><br>After clicking, it is possible to perform combination operations between indicators. You can select indicators or enter values.<br><br>Select indicators: only supports selecting send volume, delivery volume **and indicators already selected on the current page**<br><br><span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/f88aec9c84f64497a35e19f5f8e715b8~tplv-goo7wpa0wc-image.image) </span><br><br>Enter values: Clicking the selection box also allows direct input of values for calculating indicators similar to "SMS sending cost."<br><br><span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/97e55ca1a8d648a790fdb9922bb75ced~tplv-goo7wpa0wc-image.image) </span> |
|**Observation period** |Refers to the period of data collection after the user has been reached. |
|**Do not reach after event completion** |For scheduled repeat and trigger type tasks, there could be situations where a user is reached multiple times. To prevent reaching the user again after they have completed an action, you can select this option. This capability can only be set when only the selected event is "real\-time behavioral data source."<br><br><span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/30c6338630bb473d94f588ef25613369~tplv-goo7wpa0wc-image.image) </span> |


You can add up to 7 focus metrics. After adding metrics, **comprehensive participation\-based attribution will be conducted, meaning any behavior or order data completed within the window period will be included in the statistics**. Example: If a user is reached by Task a and Task b, both set with the "Mini Program Page View" as a focus metric, the data will be counted in both tasks.

<span id="4757d5e9"></span>
## **1.3 Service Account Template Messages**

<span id="2fcf070c"></span>
### **1. Product Overview**

**Service account template messages are primarily used to send important service notifications to followers**, such as reminders for successful group joining, course reminders, product pick\-up reminders, course progress reminders, and appointment success reminders. The effect after being reached is shown in the picture. Use case examples:


* Services notification for flash sale starts with a Scheduled \- One\-Time template (limited time \- single occurrence)

* Daily reminder to sign in for existing users through WeChat, with Scheduled \- Repeated template within a 7\-day cycle; notification sent when order is placed via WeChat that the item has been dispatched(Event\-Triggered: Completion of Event A)

* User cart addition triggers a coupon dispatch via service notification 10 minutes after no purchase (Event\-Triggered: Event A Completed & Event B Incomplete)


<div style="text-align: right">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/811c6649d9a944ab961c10c5b07f59b7~tplv-goo7wpa0wc-image.image" width="439px" /></div>


<span id="7bc8bb35"></span>
###  **<2\>Usage Restrictions**


| **[📢 Use the following precondition**] ||
|---|---|
|Prepare service account message templates |Complete template creation for the corresponding public account on the WeChat public platform. |
|Complete Channel Integration |Provide the public account, and complete the authorization at the GMP "Management Center \- Channel Management \- WeChat Public Accounts" interface. |
|Activate GMP permissions |The administrator activates the viewing permissions for the WeChat public account, access path: Management Center \- Channel Management \- WeChat Public Accounts \- View<br><br>The administrator activates permissions for task creation, selection, with the access path "Message Delivery \- Message Delivery Task \- New/View/Edit/Delete" |
|Activate segmentation permissions |Activation of segmentation permissions is divided into three scenarios:<br><br>If you have purchased VeCDP, you need to activate the permission "User Segmentation \- Private Domain Segmentation \- View/Add/Delete Segmentation" in VeCDP. Once activated, the segmentation function in Task Creation becomes available.<br><br>If you have only purchased Datafinder and not VeCDP, you need to activate the permission "User Segmentation" in Datafinder. Once granted, the segmentation function in Task Creation becomes available.<br><br>If neither VeCDP nor Datafinder has been purchased, this permission can be disregarded. |


<span id="ff8c65c2"></span>
###  **<3\>Function Description**

**Step1: Create a Message Delivery Task**

Add a Message Delivery Task and select the subject and service account template message channel.

Subject: The subject, also known as entity/object, often refers to individuals/vehicles/spaces that can be leveraged for growth or insight analysis. If there are multiple subjects for analysis or message delivery, it is termed multi\-subject. **If VeCDP is purchased along with the 'multi\-subject module', you can perform subject\-specific message delivery on GMP**, such as reaching users and merchants by activating multi\-subject. If the module is not purchased, you may disregard this concept and function description.

<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/973d5dec318f42f694de4a72f7daf469~tplv-goo7wpa0wc-image.image" width="439px" /></div>


**Step 2: Fill in Basic Task Information**

<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/e0dfa40e613144599f5a417f373d2526~tplv-goo7wpa0wc-image.image" width="439px" /></div>



|**Field** |**Field Meaning and Purpose** |
|---|---|
|**Task Name** |Required, used to differentiate between different tasks (strategies), and must not have the same name as other tasks |
|**Task Grouping** |Optional, allows grouping of different tasks into different categories for subsequent analysis based on Task Grouping. The grouping of Message Delivery and Process Canvas are isolated; data is not shared.<br><br>If the existing group options do not meet the requirements, you can create or edit through "Manage Groups". Only project administrators and group administrators can operate the addition of groups. If there are existing Message Delivery Tasks under a group, the group cannot be "Deleted". Deletion is only possible when there are zero Message Delivery Tasks in a group. |
|**Associated Campaign** |Optional. You can attribute tasks to different campaigns such as the "Double Eleven Campaign" for subsequent analysis based on the campaign to which the tasks belong. You can link the tasks from Message Delivery, Process Canvas, and Placement to the same campaign. |
|**Associated application for this task** |This signifies that the data from the outreach behavior generated by this task will be fed back to Datafinder under this application. If Datafinder is not purchased, this feature can be ignored. |


**Step 3: Specify Target Audience**

The target audience represents the range of users that this task aims to reach. The target audience can be supported in four ways: Rule Creation Segment, Existing Segment, Uploaded Segment, and All Users. If the purchase combinations differ, then the scope of capabilities for the target audience also differs. If GMP is purchased along with VeCDP, then a new segment can be created through 'Rule Creation Segment'; if GMP is purchased along with Datafinder (without purchasing CDP), then creating a new segment is permissible under the existing segment; **If neither is purchased, it will not support creating segments on the GMP side.** 

<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/eed4b7b92aa7474ea76023caa240deae~tplv-goo7wpa0wc-image.image" width="439px" /></div>


 **(1) Rule Creation Segment**

**After purchasing VeCDP, you can create a segment through 'Rule Creation Segment.'**  Selection can be done through label, attribute, segment package, detailed data, and behavioral data.


|**Field** |**Meaning and purpose of the field** |
|---|---|
|**Selection Criteria** |**You can create segments using the "rule creation segment" method after purchasing VeCDP, and selection can be conducted through labels, attributes, segment packages, detailed data, and Behavioral Data, and supports user filtering by audience ID types.**  Detailed operation instructions for selection can be found in the VeCDP manual (Chapter: Creating Private Domain Segments). The function permission for this selection capability is consistent with the segmentation edit permission on VeCDP side, hence using this selection capability requires activation of VeCDP "Edit Segment" Permission, otherwise, new segments cannot be created.<br><br><span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/162fe98b30d045dfb91f79f51325bdc9~tplv-goo7wpa0wc-image.image) </span> |
|**Synchronize to CDP Segment List** |Turning on the switch will make the segment created here visible in the VeCDP Segment list, and the segment name will default to the Task Name + Message Delivery Task ID. Turning off the switch will make the segment created this time invisible in the VeCDP Segment list and it cannot be reused for segment selection. Administrators can "set" the default checked status.<br><br><span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/3921eb6f248e40a8ac28f2335002bf6b~tplv-goo7wpa0wc-image.image) </span> |
|**Audience Estimation** |After configuring the segmentation criteria, click "Audience Estimation" to calculate the ID count in the segment in advance. The ID count includes two types: OneID count and the current channel's sending ID count, which can be used to decide whether to adjust the segment selection criteria settings. |
|**Segment Authorization** |Optional, authorizes the segment derived from label and behavior selection, allowing selection of which roles can have view permission for that segment. If authorization is not performed, the user will be prompted with a "No segment permission" message when viewing, editing, or copying tasks. |
|**Additional send** |Optional, you can enter the ID information of the tester. Once filled, this user will be set as the target user by default when the task is executed. Multiple IDs can be entered. |


When saving a draft or submitting for approval, the system will automatically create that segment, and the ID type of the segment will be the sending target ID type of that channel, for instance, the service template message channel will create a segment package combining appid+openid.

 **(2) Existing Segment**

With this feature, you can directly select and engage with the already defined segment.

**Permission required to use this feature:** 

If you purchase GMP and VeCDP together, this feature will pull the segment from VeCDP. Using this feature requires the "View Segment" permission in VeCDP.

If GMP and Datafinder are purchased together (without purchasing VeCDP), this feature will pull the segment from Datafinder. Using this feature requires the "User Segment" permission in Datafinder.

<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/b6b46a2f4e7d44d9b2d81e960ad57601~tplv-goo7wpa0wc-image.image" width="439px" /></div>



|**Field** |**Meaning and purpose of the field** |
|---|---|
|**Segment list** |Mandatory, it is necessary to choose the segment to be reached in this instance. If VeCDP's multi\-principal capability is purchased, this list will automatically pull the segment list of the subject for the task. |
|**Audience Estimation** |After selecting a segment, the system will automatically calculate the number of sending IDs for the current channel. |
|**Create Segment** |If you purchase GMP and VeCDP together, clicking this feature will redirect to the VeCDP segment list, where you can create new segments. If you purchase GMP and Datafinder together (without purchasing VeCDP), clicking this feature will allow you to create new segments. If neither VeCDP nor Datafinder is purchased, this capability is unavailable.<br><br><span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/df158fb6c02642eaab6fcf21c4619edc~tplv-goo7wpa0wc-image.image) </span> |
|**Additional Sending** |Optional, you can enter the IDs of test users. Once entered, the system will automatically use these users as the audience during task execution. Multiple IDs can be entered. |


 **(3) Upload Segment**

Supports uploading segments via local CSV files, but the actual upload portal is in "Message Delivery Configuration," not finalized at this step.

**Segment upload does not support event\-triggered tasks:**  Currently, segment upload only supports scheduled message delivery tasks.

**Segment upload does not support the task exclusion feature:**  After selecting this segmentation method, the option to exclude tasks is not displayed in the message delivery configuration.

**When uploading segments**: Segment ID type only supports uploading target IDs for this channel. For example, if it is an SMS channel, only mobile numbers are supported for upload.

**If the user IDs in the uploaded segment are not in the VeCDP or Datafinder systems**: They can still be supported for sending; specifically, if labels, properties, or ID information is inserted in the contact content under these circumstances, it will result in a sending failure.

<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/686302bf57a544cfa821d3e355ff2d5a~tplv-goo7wpa0wc-image.image" width="439px" /></div>



|**Field** |**Field Definitions and Purposes** |
|---|---|
|**Additional Send** |Optional, testers' ID information can be entered. Once filled, it will default to this user as the target audience during task execution. Multiple IDs can be entered. |


 **(4) All users**

All users in the current project are supported only for these two types of Message Delivery Tasks: **Event\-Triggered: Completion of Event A**, and Event\-Triggered: Event A Completed & Event B Incomplete, which means after a user triggers the event, no further filtering of the audience is done, and all users meeting the event conditions will be reached.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/0d0b0c2105b5432d8a7bb917ede42f7d~tplv-goo7wpa0wc-image.image) </span>

**Step3: Configure Trigger Conditions**

**Supports four modes: <Scheduled \- One\-Time\>, <Scheduled \- Repeated\>, <Event\-Triggered: Completion of Event A\>, and <Event\-Triggered: Event A Completed & Event B Incomplete\>.** 

**Message Delivery Task Type**: Represents the timing of the trigger for this message delivery.


* **Scheduled \- One\-Time**: The user will be reached only at a fixed point in time.

* **Scheduled \- Repeated**: Within a time range, users can be reached multiple times at fixed points, such as every day at 10 am within March.

* **Event\-Triggered: Completion of Event A**: Triggered when a user completes certain actions (immediate/delayed), such as earning points for post favorites, likes, or shares Multiple triggers can be realized within the valid timeframe of the task, provided the trigger conditions are met.

* **Event\-Triggered: Event A Completed & Event B Incomplete**: Triggers a sequence when a user completes event A but does not complete event B within a certain time, such as not visiting a page 20 minutes after app launch. Multiple triggers can be realized within the valid timeframe of the task, provided the trigger conditions are met. Commonly used in interruption marketing.


<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/49169454112b49b498d35b6739d67ee3~tplv-goo7wpa0wc-image.image" width="439px" /></div>


 **(1) Meaning of the field for Scheduled \- One\-Time**


|**Field** |**Field Definitions and Purposes** |
|---|---|
|**Reach Time** |Mandatory. If the trigger condition type is "Scheduled \- One\-Time," this field is required, representing the time point when the user is reached. |
|**Approval Timeout** |Required. If the task is not approved by the "Reach Time," you may choose to cancel the task or approve it for immediate execution. Even if "Execute Immediately After Approval" is selected, if the task is not approved within 72 hours, it will automatically be canceled. |
|**Refresh Segment Before Execution** |Required.<br><br>**If GMP + VeCDP or GMP + DateFinder has been purchased**<br><br>**If the chosen segment is "Update on Demand"** : If "Refresh Segment Before Execution" is selected, the system will, by default, refresh the segment data 15 minutes in advance. For example, if the task is scheduled for 15:00, the system will refresh the segment at 14:45. If you wish to adjust the 15\-minute interval, please contact the project manager or the Customer Success Manager.<br><br>**If the selected segment is "Updated Daily"** : The segment will be updated at the time set during the segment creation.<br><br>**If the selected segment is "real\-time updated"** : the segment will be updated in real time.<br><br>Especially: **Scheduled \- One\-Time, rule creation segment,**  will by default create a "on\-demand updated" segment.<br><br><span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/16061ec2db3f4adabd2bfe6b9e65b5af~tplv-goo7wpa0wc-image.image) </span><br><br>**If GMP + VeCDP or GMP + DateFinder has not been purchased**<br><br>Then the system does not support segment refresh. |
|**Segment refresh failed** |Mandatory.<br><br>**If GMP + VeCDP has been purchased or GMP + DateFinder has been purchased**<br><br>**If the selected segment is "on\-demand updated"** : after a refresh failure, you may choose to use the segment data currently obtained by the system for sending, or choose not to send.<br><br>**If the selected segment is "daily updated"** : refresh failure will by default use the segment currently obtained by the system for sending.<br><br>**If GMP + VeCDP or GMP + DateFinder has not been purchased**<br><br>then this option is not available. |


 **(2) Meaning of the field for Scheduled \- Repeated**


|**Field** |**Field meaning and purpose** |
|---|---|
|**Cycle period** |If the trigger condition type is "Scheduled \- Repeated", this field is required. It represents the time point at which each cycle period reaches the user. |
|**Start and end time** |If the trigger condition type is "Scheduled \- Repeated", this field is required. It represents the operating start and end time of the task. |
|**Approval timeout** |Required. If the "reach time" has arrived and the task has not been approved, you can choose to cancel the task or execute it immediately after approval. Even if "Execute Immediately After Approval" is selected, if it is not approved within 72 hours, the task will be automatically canceled. |
|**Refresh Segment before Execution** |Mandatory.<br><br>**If GMP + VeCDP or GMP + DateFinder are purchased**<br><br>**If the selected segment is "Refresh on Demand"** : If "Refresh Segment before Execution" is selected, the system will by default refresh the segment data 15 minutes beforehand. For example, if a task is scheduled for 15:00, the system will refresh the segment at 14:45. If adjustments to the 15 minute interval are needed, you can contact the project manager or Customer Success Manager for adjustments.<br><br>**If the selected segment is "Refresh Daily"** : It will be updated at the time set during the creation of the segment.<br><br>**If the selected segment is "Real\-Time Refresh"** : The segment will be updated in real time.<br><br>Specifically: **Scheduled \- Repeated, rule creation segment, will by default create a "Refresh on Demand" segment.** <br><br><span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/42e2201440f0493a90a224ede7543750~tplv-goo7wpa0wc-image.image) </span><br><br>**If GMP + VeCDP or GMP + DateFinder are not purchased**<br><br>then the system does not support refreshing the. |
|**refresh failed** |Required.<br><br>**If GMP + VeCDP or GMP + DateFinder have been purchased**<br><br>**If the selectedis 'on\-demand update'** : you can choose to send using the currentdata obtained by the system after a refresh failure, or choose not to send.<br><br>**If the selectedis 'daily update'** : the system will default to sending using the currentdata obtained after a refresh failure.<br><br>**If GMP + VeCDP or GMP + DateFinder are not purchased**<br><br>then this option is not available. |


 **(3) Meaning of the field for Event\-Triggered: Completion of Event A**


|**Field** |**Meaning and Uses of Fields** |
|---|---|
|**Trigger Event** |Mandatory.<br><br>**Represents what kind of event a user needs to complete to trigger this process**. Only users who complete the event and fit the 'target users' criteria, fulfilling both 'trigger conditions + target users', will actually be reached.<br><br><span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/43e20d59af29427c81360bdd3dd310d7~tplv-goo7wpa0wc-image.image) </span><br><br>**Cumulative Completion of A / Each Completion of A**: Cumulative completion of A three times means that the user, after completing the event, will only be reached once; each completion of A three times means the process will be triggered every time the event is completed three times.<br><br>**Immediate Reach / Delayed Reach / Delayed Specific Time / Delay Delayed to a Specific Day of the Week**:<br><br><br>* Immediate reach means the reach happens immediately after the event is completed.<br><br>* Delayed reach implies a delayed reach by a relative time; delaying by one day means delaying by 24 hours; the delay can be up to 365 days.<br><br>* Delayed by specified time means the reach only happens after waiting until a specified time after the event has occurred.<br><br><br>Delay until a specific day of the week means waiting until the nearest specific day of the week after the event has occurred to reach. For example, if a delay is set to Tuesday and an event occurs on Monday, it will be triggered this Tuesday; if set to Tuesday and the event occurs on Wednesday, it will be triggered next Tuesday.<br><br>**Common Questions:** <br><br>**The event source is grayed out**: If the event source is grayed out and not selectable, it means the data source has not been fully integrated, and you need to contact the project manager or Customer Success Manager.<br><br><span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/2a3c0a0b578544bbb345ac5849d2eaa4~tplv-goo7wpa0wc-image.image) </span><br><br>**Cannot select event attributes**: Certain attributes are currently not supported for selection — whether it is the first day visit, the first time visit, or new versus existing customer.<br><br>**How to select GMP\-related events:** <br><br><br>* To search for a GMP event, type "GMP" in the event box. The name is usually "GMP Feedback", and all actions related to GMP message delivery and process canvas are included in this event. As shown in the image below.<br><br>* After selecting the event, the system will automatically load three attribute options that require manual input:<br><br>   * Campaign type/task type: The GMP event that needs to be triggered is either message delivery or process canvas.<br><br>   * Campaign ID/Task ID: The Campaign ID corresponding to the GMP event that needs to be triggered.<br><br>   * Indicator Name: This refers to the name of the indicator corresponding to the event that needs to be triggered in GMP, such as successful sending, where you can locate indicators like "Send Volume" or "Successful Reach Volume".<br><br><br><span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/a0e6a9aa99744c39bfddf4440b82ae87~tplv-goo7wpa0wc-image.image) </span> |
|**Event A Start and End Time** |Mandatory. This field will trigger the process for all occurrences of Event A within this time period. |
|**Message Delivery Task End Time** |System default fill.<br><br>After reaching the end time, the status of the message delivery task changes to completed, and the system will no longer continue message delivery even if Event A is delayed. |
|**Refresh Segment Before Execution** |**If you have purchased GMP + VeCDP or GMP + DateFinder**<br><br>**If the selected segment is 'update on demand'** : the segment will not be refreshed.<br><br>**If the selected segment is "updated daily"** : the system will refresh based on the set time. If "label and action\-based selection" is used, the segment will default to refresh at 06:00 every day.<br><br>**If the selected segment is "updated in real\-time"** : the segment will be updated in real\-time.<br><br>Especially: **For Event\-Triggered: Completion of Event A, label and action\-based selection, a segment set to "update daily" will be created by default.** <br><br><span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/1fab89fb00b94133b28097f2a958bf9d~tplv-goo7wpa0wc-image.image) </span><br><br>**If GMP + VeCDP or GMP + DateFinder has not been purchased**<br><br>then the system does not support refreshing the segment. |
|**Segment refresh failed** |Required.<br><br>**If GMP + VeCDP or GMP + DateFinder has been purchased**: even if the refresh fails, the most recent data will still be used for assessment.<br><br>**If GMP + VeCDP or GMP + DateFinder has not been purchased**: this option is not available. |


 **(4) Meaning of the field for Event\-Triggered: Event A Completed & Event B Incomplete**


|**Field** |**Field Meaning and Usage** |
|---|---|
|**Trigger Event** |Required.<br><br>**Completing Event A triggers this process after a user completes a certain event**, targeting users filtered based on 'Audience'. Only users who meet both 'Trigger Condition + Audience' will actually be reached.<br><br>**Event B Not Completed**: Unlike 'Event\-Triggered: Completion of Event A', this task type waits for a period to ascertain if Event B is completed after completing Event A; the process is triggered if B is not completed.<br><br><span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/efe062de6a464872a11bf9558b493fde~tplv-goo7wpa0wc-image.image) </span><br><br>**Accumulative Completion of A / Each Completion of A**: Accumulating 3 completions of A means users will be reached only once after the event; marking every 3 completions of A means the process will be triggered each time A is completed three times.<br><br>**Immediate Reach / Delayed Reach / Specified Delayed Reach**:<br><br>Immediate reach is initiated right after the event is completed.<br><br>Delayed reach means a relative delay in outreach, with a delay of 1 day equaling 24 hours; the delay can be up to 365 days.<br><br>If a designated delay time is reached, it indicates that one must wait until the specified time after the event occurs before it can be triggered.<br><br>**Frequently Asked Questions:** <br><br>**Event Source Grayed Out**: If the event source is grayed out and cannot be selected, it means the data source has not been fully integrated, and it is necessary to contact the project manager or customer success manager.<br><br><span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/2fc7ace3f10e49ae9db2014ddd7b7136~tplv-goo7wpa0wc-image.image) </span><br><br>**Cannot Select Event Attributes**: Some attributes are temporarily not selectable — whether it is a first\-day visit, a first\-time visit, or whether the visitor is a new or returning customer.<br><br>**How to Select Events Related to GMP:** <br><br><br>* To find events related to GMP, search 'GMP' in the event box. The name is usually 'GMP Feedback', and all behaviors in the GMP message delivery and process canvas are contained in this event. As shown in the picture.<br><br>* After selecting the event, the system will automatically load three attribute options that need to be filled in manually:<br><br>   * Campaign Type/Task Type: Refers to whether the GMP event triggered is message delivery or a process canvas.<br><br>   * Campaign ID/Task ID: Refers to the task ID corresponding to the GMP event triggered.<br><br>   * Indicator Name: What is the indicator name of the GMP event that needs to be triggered, such as successful sending, then look for indicators like "sending volume" or "successful reach".<br><br><br><span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/3c3c7c9b16a940df8bc4d6e6b1576a3c~tplv-goo7wpa0wc-image.image) </span> |
|**Event A Start and End Time** |Mandatory. This field will trigger the process for all Event A occurrences within this time period. |
|**Message Delivery Task End Time** |System defaults.<br><br>After reaching the end time, the message delivery task status changes to completed, even if Event A is delayed, the system will no longer continue the delivery. |
|**Refresh Segment before Execution** |**If you have purchased GMP + VeCDP or GMP + DateFinder**<br><br>**If the chosen segment is "on\-demand update"** : the segment will not be refreshed.<br><br>**If the selected segment is "updated daily",**  the system will refresh according to the set time. If "label and behavior selection" is used, the segment will by default refresh at 06:00 daily.<br><br>**If the selected segment is "updated in real\-time",**  the segment will be updated in real\-time.<br><br>Specifically: **For event\-triggered, label and behavior selection, a "daily update" segment will be created by default.** <br><br><span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/d0becaab010846d5bafe4f5e8d69557e~tplv-goo7wpa0wc-image.image) </span><br><br>**If GMP + VeCDP or GMP + DateFinder are not purchased**<br><br>then the system does not support refreshing segments. |
|**Segment refresh failed** |Mandatory.<br><br>**If GMP + VeCDP or GMP + DateFinder was purchased,**  the latest data will still be used for evaluation even if the refresh fails.<br><br>**If GMP + VeCDP or GMP + DateFinder was not purchased,**  this option is not available. |


**Step4: Message Delivery Configuration**

This step involves filling in the message delivery content, and setting the frequency control/do\-not\-disturb/exclusive conditions for the delivery.

<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/0d5b65804cd34511b1de85ac65bc5a31~tplv-goo7wpa0wc-image.image" width="439px" /></div>



|**Field** |**Meaning and purpose of the field** |
|---|---|
|**Channels** |The system will default to the channel selected in Step1, but it can be changed. After modification, the entered messaging content will be cleared, but other data will be preserved. |
|**Enable split\-testing experiment** |Please refer to the "A/B Experiment" section for detailed logic |
|**Task Type** |Mandatory, includes regular campaigns, urgent campaigns, and notification campaigns.<br><br>**Task type affects task priority, and task priority affects the logic of which task is triggered first when multiple tasks are triggered simultaneously (when there is a backlog in the message queue): the task with higher priority is triggered first.** <br><br>Priority: Notification messages \> Urgent campaigns \> Regular campaigns. Each task triggers once, consuming the frequency control count for the corresponding channel once.<br><br>Special notification message tasks can still be triggered even after the channel frequency control quota is depleted. |
|**Select Template** |Mandatory, click to automatically sync WeChat templates. Each public account can use up to 25 templates at the same time. To create or modify, please operate on the WeChat public platform. The parameters in the template can be customized.<br><br><span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/9d01f0ffba6e4f1390f793e6bbda56e8~tplv-goo7wpa0wc-image.image) </span> |
|**Template Content** |If the template contains parameters, filling in the parameter content is required, supporting the insertion of user attributes, user ID, user labels, event attributes, and other parameters. Additionally, it is advisable to set default values for inserted parameters to increase the success rate of sending. If the system cannot retrieve the parameter value, the default value will be used for sending. If no default value for parameters is set, sending will be canceled.<br><br>**Insert Labels, Attributes, ID**: If the 'Multiple Entities' capability is purchased, labels, attributes, and IDs of associated entities can be inserted into the touchpoint content.<br><br><span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/1322e75b04c24027ba2acffbce186433~tplv-goo7wpa0wc-image.image) </span><br><br>**Insert Event Attributes**: When the task trigger condition is "Event\-Triggered," event attributes of the triggering event can be inserted.<br><br><span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/ccde250839594358b4cadaab559a0638~tplv-goo7wpa0wc-image.image) </span><br><br>**Insert Copy**: Can be inserted from Material Management<br><br>When the inserted variable value exceeds the length of the template content on the WeChat side, you can choose "Do not send" or "Send after truncation"<br><br><span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/d06e555a1cc84f9c975c623959469d20~tplv-goo7wpa0wc-image.image) </span> |
|**Open Method** |Mandatory, divided into 3 scenarios: H5, Mini\-program, None. This item represents how to redirect after a user clicks the "Service Account Template Message" card.<br><br>**If 'H5' is selected**: It means that after clicking the "Service Account Template Message" card, the user needs to be redirected to an H5 page. When configuring GMP, it is necessary to enter the link information related to H5.<br><br><span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/2065ebb8630246d88c45eddad201111a~tplv-goo7wpa0wc-image.image) </span><br><br>**If 'Mini\-program' is selected**: It means that after clicking the "Service Account Template Message" card, the user needs to be redirected to a Mini\-program page. During GMP configuration, it is necessary to select which Mini\-program to open and enter the path of the Mini\-program page. Specifically: This Mini\-program must be authorized in Channel Management in GMP in advance to be selected here.<br><br><span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/4a119aef61d24598b2fe53344df8884c~tplv-goo7wpa0wc-image.image) </span><br><br>**If "None" is selected**, it means after clicking the "Service Number Template Message" card, no redirection is required. |
|**Test sending** |Conduct actual testing of the push content. Fill in the target ID and variable values. |
|**Global Reach Restriction** |That is, the channel access frequency control restriction. The page will display the selected channel frequency control. If it does not meet the requirements, you can click "View" \-\-\> go to "Management Center" to adjust the channel control. Note, currently after adjusting the frequency control, the page will not auto\-sync. You need to manually update the configuration page to sync to the latest frequency control situation.<br><br>If the 'Global Reach Restriction' is turned off, it means that the message sent this time will not be subject to the frequency control of this channel or cross\-channel frequency control restrictions. |
|**Cross\-channel Frequency Control** |The current version supports setting cross\-channel frequency control, such as a maximum of one reach per day for Channel A + Channel B. The corresponding configuration data will be displayed here. |
|**Do Not Disturb Period** |The SMS channel may disregard this field. |
|**Do Not Disturb Settings** |You can set a Do Not Disturb period; if the system plans to send messages during this period, they will be restricted by the Do Not Disturb settings. |
|**Rules for reaching out during Do Not Disturb periods** |If filtered out due to hitting the Do Not Disturb criteria, you can choose either "Abandon this outreach" or "Continue to reach out after Do Not Disturb ends." |
|**Message Delivery Task Frequency Control** |If the current task's trigger condition is "Scheduled \- Repeated", "Event\-Triggered: Completion of Event A", or "Event\-Triggered: Event A Completed & Event B Incomplete", there is a possibility of reaching the same user multiple times. This field allows setting how to control the frequency within this task.<br><br><span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/844d4ee91c3249879e4c48510e1884f8~tplv-goo7wpa0wc-image.image) </span> |
|**Exclude Task** |Optional.<br><br>The selected task has a mutual exclusion relationship with the current task, and the target user (with the same user ID) will only be successfully reached by one of the tasks. For instance, Task A and Task B are mutually exclusive; if a user is successfully reached by Task A, they will not be reached by Task B, and vice versa. Supports searching by task name or ID, currently only displaying the first 50 tasks; for more tasks, please search. |


**Step 5: Monitoring Indicators**

**This feature can be used to track users post\-delivery to document their subsequent conversion activities**. The 'Set Monitoring Indicators' is by default turned off. When switched on, you can set the monitoring indicators for the task.

<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/e6f1bfe86ec44871a1112818ab67fe94~tplv-goo7wpa0wc-image.image" width="439px" /></div>



|**Field** |**Meaning and purpose of the field** |
|---|---|
|**Configuration method** |You can choose to "Create a new indicator" or use an "Existing Indicator" |
|**Indicator Name** |Mandatory.<br><br>Examples: Add to cart, generate order, GMV. When creating a task, the indicator names entered will be reflected on the data analysis page.<br><br><span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/38cd1bf813a448d5a84823d528c1f5b0~tplv-goo7wpa0wc-image.image) </span> |
|**Manage Indicators** |There is an "Manage Indicators" entry to the right of the indicator name. By clicking it, you can view all the indicators in the system, check their configuration rules, and delete indicators. Deleting an indicator will not affect the data already set in the task; it will only prevent the indicator from being selected when choosing an existing one.<br><br><span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/7a33b8ab14be4a1aab7bad001b9e139f~tplv-goo7wpa0wc-image.image) </span> |
|**Calculation Conditions**<br><br>**Calculated based on real\-time behavioral data** |**Examples of indicators**: product detail page views, add\-to\-cart counts, homepage views of a mini program<br><br>**Conditions for use**: If a behavioral data source has "real\-time behavior messages," then it is possible to set the count/statistics of real\-time behaviors under this data source. If you are unsure whether the data source meets the requirements, you can consult the project manager or customer success manager.<br><br>**How to configure**: Select the data source and event, and if you need to add restrictive conditions to the event, you can click "Filter Conditions" to add them. For example, to track visits on a product details page and restrict access to the URL, this feature can be utilized.<br><br><span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/8bae2770901b40baa5b14d8e24d13f2d~tplv-goo7wpa0wc-image.image) </span><br><br>**What does the data analysis look like after configuration**:<br><br><br>* After configuration, message delivery and process canvas tasks for this channel will automatically monitor this indicator.<br><br>* This indicator tracks user conversions within a specified window after contact.<br><br>* After configuration, as long as the conversion event occurs, this indicator will be updated in real\-time. |
|**Calculation Conditions**<br><br>**Calculated using offline behavioral data** |**Examples of indicators**: Visits to product details page, cart additions, home page views of mini\-programs<br><br>**Conditions required for use**: If a source of behavioral data is updated daily as an "incremental table," then it can set statistics on the count/number of people for actions under this data source. If you're unsure whether this data source meets the requirements, consult a project manager or customer success manager.<br><br>**How to Configure**: Select the data source and events. To add filter conditions to the events, click "Filter Conditions". For example, to count the visits to a product detail page, you can limit it to specific page addresses using this feature.<br><br><span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/9ab7956c23164e1bbd64da155bb584f6~tplv-goo7wpa0wc-image.image) </span><br><br>**What the results of data analysis look like after configuration**:<br><br><br>* After configuration, the message delivery and process canvas tasks of this channel will automatically monitor this indicator.<br><br>* This indicator will track the user's conversion within a specified window period after being reached.<br><br>* Once a conversion event occurs, the system will count the indicator data at 5 AM, 11 AM, 5 PM, and 11 PM daily.<br><br><br>**The difference between this data source and 'using real\-time behavioral data source'** : If there is 'real\-time behavioral message', prefer using the 'using real\-time behavioral data source' feature, otherwise, use 'using offline behavioral data for calculation'. |
|**Calculation Conditions**<br><br>**Calculation through detailed data** |**Indicator Examples**: Number of orders, GMV<br><br>**What conditions need to be met to use this feature**: If the detailed data is updated daily as an "incremental table," you can set performance metrics for detailed behavioral data under this data source. If you are unsure whether this data source meets the criteria, consult the project manager or customer success manager.<br><br>**How to configure**:<br><br>Select the data source and fields. If you need to add restrictions to an event, click "Filter Conditions" to do so. For example, to count the number of orders, you can restrict the product categories using this feature.<br><br>If you want to count the occurrences of a field, select "Count/Number of Times."<br><br><span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/a00619c436ed4d4abce9074dbc39bdb4~tplv-goo7wpa0wc-image.image) </span><br><br>If you want to sum up the fields, choose "Sum." For instance, the GMV indicator requires summing up the amounts of goods.<br><br><span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/0eb406fad50241d59593f7107889d3c5~tplv-goo7wpa0wc-image.image) </span><br><br>**What are the results of the data analysis after configuration**:<br><br><br>* After configuration, the message delivery and 'Process Canvas' tasks of this channel will automatically monitor the indicator.<br><br>* This indicator will count users' conversions within a designated window after being reached.<br><br>* Once configured, as long as a conversion event occurs, the system will tally the indicator data at 5, 11, 17, and 23 o'clock each day. |
|**Calculation Conditions**<br><br>**Combined Indicators** |**Combined Indicators**<br><br>Indicator Examples: Add\-to\-Cart Rate, Customer Spending per Transaction, SMS Sending Cost<br><br>After clicking, you can perform combination operations between indicators. You can select indicators or enter values.<br><br>Select Indicators: Supports selecting only the delivery volume, reception volume, **and the indicators already selected on this page**<br><br><span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/c02e368f23974fe0ba203fa0c8fd3936~tplv-goo7wpa0wc-image.image) </span><br><br>Enter Values: Clicking the selection box also allows you to directly enter values, used for calculating indicators similar to "SMS Sending Cost".<br><br><span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/3c920b12f1cc47a59f334bd5afe36605~tplv-goo7wpa0wc-image.image) </span> |
|**Window Period** |Refers to the length of time within which data is considered after a user has been reached. |
|**No Message Delivery after an Event Completion** |"Scheduled \- Repeated" and "Event\-Triggered" tasks may result in a user being reached multiple times. If you want to stop reaching out to the user after they complete a specific action, you can select this option. Only when the selected event is "Behavioral Data Source" can this feature be set.<br><br><span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/7af9bab52ba84813be71e6b3c489b69a~tplv-goo7wpa0wc-image.image) </span> |


You can add up to seven monitoring indicators. After adding the indicators, **comprehensive attribution statistics will be conducted, meaning if users complete an action or generate order data within the window period, it will all be counted**. For example: If a user is reached by tasks a and b, and both have the 'Mini Program Page Browsing' as a monitoring indicator, then the data will be recorded in both tasks.

<span id="c79dce74"></span>
## **1.4 Public Account Active Message**

<span id="7e7dd8e6"></span>
### **1. Product Overview**

After a user interacts with the public account (reply with a keyword, subscribe to the public account, or scan a QR code), an automatic response can be implemented using the GMP Public Account Active Message.

<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/2fafe44971df41feb74ef71e03282ef7~tplv-goo7wpa0wc-image.image" width="439px" /></div>


<span id="a78e4f53"></span>
### **2. Usage Restrictions**


| |**Detailed Description** |
|---|---|
|**Provide an Official Account** |Provide a WeChat Verified Service Account |
|**Complete Channel Access** |Complete the authorization of the Official Account in the GMP "Management Center \- Channel Management \- WeChat Official Account" interface. |
|**Activate GMP permissions** |The administrator activates the permission to view the SMS channel via the following path: Management Center \- Channel Management \- WeChat Official Account \- View<br><br>The administrator activates the permission for creating message delivery tasks through the path "Message Delivery \- Message Delivery Task \- New/View/Edit/Delete" |
|**Activate segmentation permissions** |Activate segmentation permissions in three scenarios:<br><br>If you have purchased VeCDP, you need to activate the permission in VeCDP "Segment \- Private Domain Segment \- View/Add/Delete/Edit", after which the segmentation feature in task creation can be used.<br><br>If you have not purchased VeCDP but have purchased Datafinder, you need to activate the "Segment" permission in Datafinder, after which the segmentation feature in task creation can be used.<br><br>If you have not purchased VeCDP or Datafinder, this permission can be ignored. |


<span id="0ee7dc7d"></span>
### **Function Description**

**Step 1: Create a Message Delivery Task**

Add a message delivery task, select the subject and SMS channel

Subject: A subject, also referred to as an entity/object, usually denotes people, vehicles, or venues that can be targeted for operational growth or insight analysis. If there are multiple analysis or delivery subjects, it is called multi\-subject **If VeCDP is purchased along with the 'multi\-subject module,' it can support reaching any subject in GMP, such as users or merchants needing to enable multi\-subject.**  If this module is not purchased, this concept and function description can be ignored.

<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/b931511b796d41dd84788994c3d28141~tplv-goo7wpa0wc-image.image" width="439px" /></div>


**Step 2: Fill in the Basic Information of the Task**

<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/a06bf71756cc47cfad08cce3630f07ed~tplv-goo7wpa0wc-image.image" width="439px" /></div>



|Field |Field Meaning and Usage |
|---|---|
|Task Name |Mandatory, used to distinguish between different tasks (strategies), and must not be identical to other task names |
|Task Grouping |Optional, allows categorization of different tasks into different groups for subsequent analysis based on task grouping The grouping of message delivery and process canvas is isolated, and data is not shared<br><br>If the existing grouping options do not meet the requirements, new groups can be created or edited via "Manage Groups" Only project administrators and group administrators can add new groups If there are existing message delivery tasks in a group, the group cannot be "deleted" unless there are zero message delivery tasks in the group |
|Associated Campaign |Optional, tasks can be attributed to different campaigns, such as "Singles Day Campaign," for subsequent analysis based on the associated campaign Tasks within the Message Delivery/Process Canvas/Placement can all be linked to the same campaign. |
|This task is associated with an application |The behavior data generated by this task will be sent back to Datafinder under this application; if Datafinder is not purchased, this feature can be ignored. |


**Step 3: Fill in the Target Audience**

The target audience represents the scope of users who need to be reached for this task. The target audience supports 3 methods: rule creation segment, existing segments, and all users. Purchasing different combinations will affect the range of capabilities of the target users. If GMP is purchased along with VeCDP, new segments can be created under "rule creation segment"; if GMP is purchased along with Datafinder (without purchasing CDP), new segments can be created within existing segments; **if neither is purchased, creating segments on the GMP side is not supported.** 

<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/8ac2a3cdb62d49f488345413770904a2~tplv-goo7wpa0wc-image.image" width="439px" /></div>


 **(1) Rule Creation Segment**

**After purchasing VeCDP, segments can be created using "rule creation segment" method**, which allows segment selection through labels, attributes, segment packages, detailed data, and behavioral data.


|Field |Meaning and purpose of the field |
|---|---|
|Selection conditions |**After purchasing VeCDP, you can create a segment using the "rule creation segment," selectable through labels, attributes, segment packages, detailed data, and behavioral data, and supports filtering users by the ID type of the audience.**  Detailed operations for selection can be found in the VeCDP manual (Chapter: Creating Private Domain Segments). The function permissions for this selection capability are consistent with the segment editing permissions on the VeCDP side. Therefore, using this selection capability requires the activation of VeCDP "Add/Delete/Edit Segment" permissions, otherwise it will be impossible to create new segments.<br><br><span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/f1ea5d857d92452f91a66504fb5655bb~tplv-goo7wpa0wc-image.image) </span> |
|Synchronize to the CDP Segment List |Turning on the switch will make the segments created here visible in the VeCDP segment list, with the segment name defaulting to the Message Delivery Task Name + Task ID. Turning off the switch will make the segment created in VeCDP invisible in the segment list, and it cannot be used for segmentation selection again. Administrators can "Set" the default checked state.<br><br><span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/6da408c97583432d8b2aa8900ae8000a~tplv-goo7wpa0wc-image.image) </span> |
|Audience Estimation |After configuring the segmentation conditions, clicking "Audience Estimation" will allow you to calculate the number of IDs in the segment in advance. There are two types of ID counts: OneID count and the current channel's send ID count. You can decide whether to adjust the segmentation selection conditions based on the estimated results. |
|Authorize Segment |Optional, authorize the created segment based on labels and behaviors, selecting which roles can have viewing permissions for the segment. If no authorization is given, a prompt indicating no segment permissions will appear when viewing, editing, or copying tasks. |
|Supplementary Sending |Optional, you can enter the IDs of the test personnel. After entry, these users will be defaulted as the target audience when the task is executed. Multiple IDs can be entered. |


When saving a draft or submitting for approval, the system automatically creates the segment, where the ID type of the segment is the target ID type for that channel, such as creating a segment package with appid+openid for the public account active message channel.

 **(2) Existing Segments**

Using this feature, directly select the already created segment for outreach.

**Permissions required to use this feature:** 

If GMP is purchased along with VeCDP, this feature will pull segments from VeCDP. To use this feature, VeCDP “view segment” permission must be enabled.

If you purchase GMP and Datafinder at the same time (without purchasing VeCDP), this feature will pull segments from Datafinder. To use this feature, you need to activate the "User Segmentation" permission on Datafinder.

<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/4f4994bea6a04696b3ee14e694cc365e~tplv-goo7wpa0wc-image.image" width="439px" /></div>



|Field |Meaning and Purpose of the Field |
|---|---|
|Segment List |Mandatory, please select the segment for this message delivery. If VeCDP's multi\-subject capability is purchased, this list will automatically pull the segment list of the subject for this task. |
|Audience Estimate |After selecting a segment, the system will automatically calculate the number of sending IDs for the current channel. |
|Create New Segment |If GMP and VeCDP are purchased together, clicking this function will redirect to the VeCDP segment list, where you can create a new segment. If GMP is purchased along with Datafinder (without purchasing VeCDP), clicking this function will support the creation of a new segment. If VeCDP or Datafinder is not purchased, this capability is unavailable.<br><br><span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/2cf89390c99140d38f95e5fc5b85251d~tplv-goo7wpa0wc-image.image) </span> |
|Additional Send |Optional, you can enter the ID information of the tester; after filling it out, this user will be set as the target user by default during task execution. Multiple IDs can be entered. |


 **(3) All users**

Represents all users under the current project, **all users only support two types of outreach tasks: Event\-Triggered: Completion of Event A and Event\-Triggered: Event A Completed & Event B Incomplete**, indicating that after the user triggers an event, no further audience filtering is done, and all users meeting the event conditions will be reached.

<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/a0844c7aaea54504ad72f673a42dc75a~tplv-goo7wpa0wc-image.image" width="439px" /></div>


**Step 3: Setting Trigger Conditions**

**Public Account Active Message only supports two methods: Event\-Triggered: Completion of Event A and Event\-Triggered: Event A Completed & Event B Incomplete.** 

**Message Delivery Task Type**: Represents the timing of message delivery triggered this time.


* **Event\-Triggered: Completion of Event A**: Triggered when users complete a certain action (can be immediate/delayed), such as automatically replying when a user responds to a message. Within the effective period of the task, meeting the trigger conditions enables multiple triggers.

* **Event\-Triggered: Event A Completed & Event B Incomplete**: Create an event\-triggered task that is triggered if a user completes action A and does not complete action B within a specified time after completing A, such as if the user does not scan a code 20 minutes after replying to a message. During the valid period of the task, meeting the trigger conditions allows for multiple triggers.


<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/c9f1f844a20849349b382cf8c430a296~tplv-goo7wpa0wc-image.image" width="439px" /></div>


 **(1) Event\-Triggered: Completion of Event A**


|Field |Meaning and use of the field |
|---|---|
|Trigger Event |Mandatory.<br><br>**This represents the type of event that, once completed by the user, triggers this process**. Only users who meet both 'trigger condition + target user' will genuinely be reached.<br><br><span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/2ecd8a4d494240269ce89e4cad2415b2~tplv-goo7wpa0wc-image.image) </span><br><br>WeChat active messages support three trigger events: reply to a keyword, follow an official account, and scan a QR code.<br><br>**Reply with keyword**: You need to set keywords, and you can set three types of keywords: reply containing keywords, reply exact keywords, and reply excluding keywords. If there are multiple keywords, they should be separated by newline characters.<br><br><span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/2c487467bebc42d5b7f3e6ae4ac24e32~tplv-goo7wpa0wc-image.image) </span><br><br>**Subscribe to the official account**: Represents the message content that is automatically sent after subscribing to this official account.<br><br>**Scan QR Code**: You need to set detailed information related to scanning QR codes.<br><br><span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/426dce66b3bb459da33dae8170b0a494~tplv-goo7wpa0wc-image.image) </span><br><br>**Cumulative Completion of A / Each Completion of A**: Cumulative completion of A 3 times means that after the user completes the event, it will only be triggered once; Each completion of A 3 times means that the process will be triggered every time the user completes A 3 times.<br><br>**Immediate Reach / Delayed Reach / Delayed Specific Time/Delay to a Specific Weekday**:<br><br>Immediate reach means that immediately following the event completion, message delivery occurs.<br><br>Delayed reach means delaying for a relative period of time, where delaying for 1 day equates to 24 hours delay; it can be delayed by up to 365 days.<br><br>Delayed specified time reach means that after the event occurs, one must wait until a specified time to proceed with message delivery.<br><br>Delay to a specific weekday reach means that after the event occurs, one must wait until the nearest specific weekday to proceed with message delivery. For example, if a delay is set to Tuesday, and an event occurs on Monday, it will be triggered on this Tuesday; if a delay is set to Tuesday and an event occurs on Wednesday, it will be triggered on the following Tuesday. |
|Event A start and end time |Required. This field triggers the process if event A occurs during this time period. |
|Task Name end time |Automatically filled by the system.<br><br>After reaching the end time, the status of the Message Delivery Task becomes ended; even if Event A is delayed, the system will no longer continue delivery. |
|Refresh Segment before execution |**If purchased GMP + VeCDP or GMP + finder**<br><br>**If the selected segment is "updated on\-demand":**  the segment will not be refreshed.<br><br>**If the selected segment is "updated daily"** : the system will refresh according to the set time. If "rule creation segment" is used, the segment will be refreshed at 06:00 daily by default.<br><br>Specifically: **Event\-Triggered: Completion of Event A, rule creation segment, will by default create a "daily updated" segment.** <br><br><span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/6ac9f58e4e094a6380ae3d36e12424cd~tplv-goo7wpa0wc-image.image) </span><br><br>**If GMP + VeCDP or GMP + finder is not purchased**<br><br>the system does not support refreshing segments. |
|Segment refresh failed |Mandatory.<br><br>**If GMP + VeCDP or GMP + finder is purchased**: after a refresh failure, the system will use the latest data to make judgments.<br><br>**If GMP + VeCDP or GMP + finder is not purchased:**  this option will not be available. |


 **(2) Event\-Triggered: Event A Completed & Event B Incomplete**


|Field |Field Definitions and Purposes |
|---|---|
|Trigger Event |Mandatory.<br><br>**Event A completion indicates the specific event that triggers this process**. Users who complete this event will be filtered based on 'Target Audience', and only users who meet both 'Trigger Condition + Target Audience' will actually proceed with the outreach.<br><br><span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/4346bf61e52a4b03a6ce4fef36782893~tplv-goo7wpa0wc-image.image) </span><br><br>Event A settings: WeChat active messages support three trigger events: Reply to Keyword, Follow Public Account, Scan QR Code.<br><br>**Reply to Keyword**: You need to set keywords, supporting three types of keyword settings: reply containing keywords, reply exact keywords, reply excluding keywords. If multiple keywords are set, use line breaks to separate them.<br><br><span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/d078db5118544322ab26e1365ea283fa~tplv-goo7wpa0wc-image.image) </span><br><br>**Follow Public Account**: Represents the automatic message sent after following this public account.<br><br>**Scan QR Code**: You need to set detailed information related to scanning QR codes.<br><br><span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/10f29d487da94482b7a3cc4552d926a4~tplv-goo7wpa0wc-image.image) </span><br><br>**Cumulative Completion of Event A / Each Completion of Event A**: Cumulative completion of Event A three times means the user will only be reached once after completion; each completion of Event A three times means the process will be triggered every time the user completes Event A three times.<br><br>**Incomplete Event B**: Unlike Event\-Triggered: Completion of Event A, this task type requires a waiting period after completing Event A to determine if Event B has been completed, and the process is triggered only if it is not. Event B supports setting up WeChat events or other types of events. If the user has not completed a purchase within 7 days after following the official account.<br><br><span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/9e23f81f7fce4b0285670fdfa91c9cbf~tplv-goo7wpa0wc-image.image) </span><br><br>**Cumulative Completion of Event A / Completion per Event A**: Cumulative completion of Event A three times means after completing the event, the user will only be reached once; completion per Event A three times means that each time a user completes Event A three times, the process is triggered.<br><br>**Immediate Message Delivery / Delayed Message Delivery / Delayed Specific Time / Delay to a Specific Weekday**:<br><br>Immediate Message Delivery means reaching out immediately after the event is completed.<br><br>Delayed Message Delivery means delaying the outreach by a relative time, where a delay of 1 day means delaying by 24 hours; the maximum delay can be up to 365 days.<br><br>Delayed Specific Time Delivery means waiting until a specific time after the event has occurred to carry out the outreach.<br><br>Delay to a Specific Weekday means waiting until the nearest given weekday after the event has occurred to carry out the outreach. For example, if set to delay to Tuesday and the event happens on Monday, it will reach on this Tuesday; if set to delay to Tuesday and the event happens on Wednesday, it will reach on the next Tuesday. |
|Event A Start and End Time |Required. This field triggers the process for all occurrences of Event A within the specified time range. |
|Message Delivery Task End Time |System default fill.<br><br>After reaching the end time, the message delivery task status changes to completed, and the system will no longer continue deliveries, even if Event A is delayed. |
|Refresh Segment Before Execution |**If GMP + VeCDP or GMP + finder is purchased**<br><br>**If the selected segment is "Refresh on Demand",**  the segment will not be refreshed.<br><br>**If the selected segment is "Daily Refresh",**  the system will refresh according to the set time. If the "rule creation segment" is used, the segment will automatically refresh at 06:00 every day.<br><br>Specifically: **Event\-Triggered: Completion of Event A, rule creation segment, will by default create a "Daily Updated" segment.** <br><br><span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/cd2d0d91e4b245278cd4da8fba106dfd~tplv-goo7wpa0wc-image.image) </span><br><br>**If GMP + VeCDP or GMP + finder has not been purchased**<br><br>then the system does not support refreshing the segment. |
|Segment refresh failed |Mandatory.<br><br>**If GMP + VeCDP or GMP + finder is purchased**: If the refresh fails, the most recent data will still be used for evaluation.<br><br>**If GMP + VeCDP or GMP + finder is not purchased:**  this option will not be available. |


**Step 4: Reach Configuration**

This step involves filling in the reach content and setting the frequency control/disturbance\-free/mutual exclusion conditions for the reach.

<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/bbb21ef6f0e242b3ad9c4d24d329c7dc~tplv-goo7wpa0wc-image.image" width="439px" /></div>



|Field |Field Meaning and Usage |
|---|---|
|Channels |The system defaults to the channel selected in Step1 and allows modifications. Any modifications will clear the input message content, but other data will be preserved. |
|Turn on the traffic allocation experiment |For detailed logic, please refer to the "A/B Experiment" section |
|Task Type |Mandatory, includes regular campaigns, urgent campaigns, and notification campaigns.<br><br>**Task type affects task priority, which influences the logic of prioritizing one task over others when multiple tasks are triggered simultaneously (when the message queue has a backlog).**  Priority is given to tasks with higher priority.<br><br>Priority: Notification messages \> Urgent campaigns \> Regular campaigns. Each task triggers once, consuming one instance of channel frequency control.<br><br>Specifically, tasks of the notification message type can still trigger even after the channel's frequency control limit has been reached. |
|Reply content |Mandatory, the reply content supports six types: text message, resource center, graphic message, WeChat coupon, external page, WeChat Mini Program.<br><br>**Text message**: You need to manually enter the text information you want to reply with.<br><br><span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/1ce06b0e904f4c7cb5ff286a8aa0fe23~tplv-goo7wpa0wc-image.image) </span><br><br>**Resource center**: You can import WeChat\-related images/articles/videos/documents into the GMP side's resource center, and after importing, you can reply directly with images in active WeChat message replies.<br><br>**Graphic message**: The system will automatically pull images and texts previously created on WeChat, allowing you to choose graphic messages created on WeChat to reply with.<br><br>**External page**: You need to manually enter the title, summary, cover, and jump link of the external page.<br><br>**WeChat Mini Program**: Select a designated mini program and set the relevant jump path. Paths support the insertion of user attributes and user ID variables.<br><br>How to insert variables:<br><br><br>* Fill in the path of the mini program, format like pages/index/index.<br><br>* Write the English "?" symbol.<br><br>* Enter the parameter name and the "=" symbol, for example, "userid="<br><br>* Click & select the variable to be inserted, making sure to use the "&" symbol between multiple parameters<br><br><br><span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/d94bb9abea4748cb998f2479bd0b6e36~tplv-goo7wpa0wc-image.image) </span> |
|Global Reach Limit |This is the channel reach frequency control limit; the page will display the selected channel frequency control. If it does not meet the requirements, you can adjust the channel frequency control by clicking "View" \-\-\> "Settings Center". Note that the page will not automatically synchronize after the frequency control adjustment; you need to manually refresh the configuration page to sync the latest control settings.<br><br>If the "Global Reach Limit" is turned off, it means that the message sent this time will not be subject to the frequency control of this channel or cross\-channel frequency control limits. |
|Cross\-channel Frequency Control |The current version supports setting Cross\-channel Frequency Control, such as channel A + channel B, to a maximum reach of once per day. The corresponding configuration data will be displayed here. |
|Do Not Disturb Period for Channels |The SMS channel can ignore this field. |
|Do Not Disturb Settings |You can set a Do Not Disturb period. If the system plans to send messages during this period, they will be restricted by the Do Not Disturb setting. |
|Do Not Disturb Period Rules |If filtered due to hitting a Do Not Disturb condition, you can choose either "Abandon this reach" or "Continue reaching after Do Not Disturb ends." |
|Message Delivery Task Frequency Control |If the current task's trigger condition is 'Scheduled \- Repeated,' 'Event\-Triggered: Completion of Event A,' or 'Event\-Triggered: Event A Completed & Event B Incomplete,' users may be reached multiple times. This field allows setting how frequency control should be handled within this task.<br><br><span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/15a6503f6009434fb097d0ea869b7018~tplv-goo7wpa0wc-image.image) </span> |
|Exclude Tasks |Optional.<br><br>This refers to the selected task having an exclusion relationship with the current task. The target users (with the same User ID) will only be reached by one of the tasks successfully. Task A and Task B are mutually exclusive; if a user is successfully reached by Task A, they will not be reached by Task B, and vice versa. Search by task name or ID is supported, currently displaying only the first 50 task records; search for more tasks if needed. |


**Step 5: Focus Metrics**

**This feature can be used to track the subsequent conversion of users reached after the reach event.**  'Set Focus Metrics' is off by default, switching it to on allows for the setting of the task's focus metrics.

<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/b0f6faf1e39a4a83a0644e68173e3faa~tplv-goo7wpa0wc-image.image" width="439px" /></div>



|Field |Field Meaning and Purpose |
|---|---|
|Setting Method |You can either create a 'New Indicator' or use an 'Existing Indicator'. |
|Indicator Name |Required.<br><br>Examples include: adding to cart, placing an order, GMV. When creating a task, the indicator name entered will be reflected on the data analysis page.<br><br><span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/ceca62d7e9f94bbe88af6c66ab361760~tplv-goo7wpa0wc-image.image) </span> |
|Management Indicators |On the right side of the indicator name, there is an "Management Indicators" entry. Clicking on it allows you to view all indicators in the system, check the configuration rules of the indicators, and delete indicators. Deleting indicators will not affect the data already set in tasks, but will prevent the indicator from being selected under "Choose Existing Indicators."<br><br><span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/8eb62bfbc45c4d5fabced63df16aa26c~tplv-goo7wpa0wc-image.image) </span> |
|Calculation Conditions<br><br>Calculated through real\-time behavioral data |**Indicator examples**: product detail page visits, add\-to\-cart volume, browsing volume on the homepage of the mini program<br><br>**Conditions required for use**: If a behavioral data source has "real\-time behavior messages", then it is possible to set real\-time behavior count/per person statistics indicators under that data source. If you are unsure whether the data source meets the conditions, you can consult a project manager or a customer success manager.<br><br>**How to configure**: choose a data source and events, if you need to add restrictions to the events, you can click "Filter Conditions" to add them. For example, to count visits to the product details page, if you need to limit the address of the product details page, you can use this feature.<br><br><span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/c4d9fb346ea7473ca94353707eab820a~tplv-goo7wpa0wc-image.image) </span><br><br>**What is the result of data analysis after configuration**:<br><br><br>* After configuration, the channel's message delivery and process canvas tasks will automatically monitor this indicator.<br><br>* This indicator will track the conversion rate of users after being reached, within a specific window period.<br><br>* After configuration, as soon as a conversion event occurs, this indicator will be updated in real time. |
|Calculation Conditions<br><br>Calculated from offline behavioral data |**Examples of indicators**: product detail page views, add\-to\-cart numbers, WeChat Mini Program home page views<br><br>**What conditions are required to use it**: If a data source of behavioral data is updated daily as an 'incremental table,' then you can set indicators for the number of actions/persons under this data source. If you're unsure whether the data source meets the requirements, consult with the project manager or customer success manager.<br><br>**How to configure**: Select the data source and event, and if you need to add limiting conditions to the event, you can click 'Filter Conditions' to add them. For instance, to track the number of visits to a product details page, if you need to restrict the URL of the product details page, you can use this feature.<br><br><span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/911ab05ca23f4ee9944c048920aa5ac3~tplv-goo7wpa0wc-image.image) </span><br><br>**What are the results of data analysis after configuration**:<br><br><br>* After configuration, message delivery and process canvas tasks on this channel will automatically monitor this indicator.<br><br>* This indicator tracks user conversions within a specified window after being reached.<br><br>* After setup, as long as the conversion event occurs, the system will count the indicator data at 5, 11, 17, and 23 o'clock each day.<br><br><br>**How this data source differs from the 'Real\-Time Behavioral Data Source'** : If 'real\-time behavior messages' are available, prioritize using the 'Real\-Time Behavioral Data Source' function; if not, use 'Offline Behavioral Data Calculation' for statistics. |
|Calculation Conditions<br><br>Calculate Using Detailed Data |**Indicator Examples**: Order count, GMV<br><br>**Requirements for Use**: If a detailed data is updated daily as an 'incremental table', then you can set the data source to calculate behavioral data statistics under this data source. If you are unsure whether the data source meets the requirements, you can consult the project manager or the customer success manager.<br><br>**How to Configure**:<br><br>Select data sources and fields. If you need to add filter conditions to the event, you can click "Filter Conditions" to add them. For example, to count order volumes, you can use this function to restrict the product category.<br><br>If you want to count the occurrences of a field, select "Count"<br><br><span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/08817c29c7024464908cbeaeca904f60~tplv-goo7wpa0wc-image.image) </span><br><br>If you want to sum up the fields, select "Sum". For instance, the GMV metric requires summing up the product amounts.<br><br><span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/c79089e7b5f3453e88a2fbd384589d03~tplv-goo7wpa0wc-image.image) </span><br><br>**What are the results of data analysis after configuration**:<br><br><br>* After configuration, the process canvas tasks of this channel will automatically focus on this metric.<br><br>* This metric will track the user's conversion within a specified window after reaching the message delivery.<br><br>* After setup, the system will compile the metric data at 5, 11, 17, and 23 o'clock every day whenever a conversion event occurs. |
|Calculation Conditions<br><br>Composite Metrics |**Composite Metrics**<br><br>Examples of metrics: Add\-to\-cart rate, per\-customer transaction value, SMS sending cost<br><br>After clicking, you can perform composite operations between metrics. You can choose a metric or input a value.<br><br>Select a metric: Only the selection of sent volume and delivered volume **and already chosen metrics on the current page** is supported.<br><br><span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/372b25ed943447da8bd420db85d1df25~tplv-goo7wpa0wc-image.image) </span><br><br>Input a value: Clicking on the selection box also allows direct number entry for calculating metrics like "SMS sending cost."<br><br><span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/24a6bdb1ebca422daeacaa6a5fbeba4c~tplv-goo7wpa0wc-image.image) </span> |
|Grace period |This statistic measures the time window after a user is reached. |
|Do not reach out after completing the event |For scheduled repeat and trigger\-based tasks where a user is reached multiple times, you can select this option if you want the user to stop being reached after completing a certain behavior. This feature is only available when the selected event is "Real\-Time Behavioral Data Source".<br><br><span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/d0c6c0d1dada4e1ebabd619c449785c5~tplv-goo7wpa0wc-image.image) </span> |


You can add up to 7 focus metrics. After adding metrics, **full participation attribution analysis will be conducted, meaning that as long as the user completes an action or generates order data within the window period, it will all be included in the statistics**. For example: If a user is reached by both task a and task b, and both tasks have set the 'Mini Program Page View' as a focus metric, then that data will be counted in both tasks.

<span id="4936a08b"></span>
## **1.5 Official Account Group Message**

<span id="d38bbd24"></span>
### **1. Product Overview**

**Official Account Group Messages are primarily used for broadcasting messages to all fans of an official account or to specific fan groups.**  Subscription accounts can only send one message per day, while service accounts can send only four messages per month, and fans receive these group messages through individual WeChat accounts from the official account.

<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/bb3e68d467b44d349db0166adaeacc75~tplv-goo7wpa0wc-image.image" width="439px" /></div>


<span id="be3f50c1"></span>
### **2. Usage Restrictions**


|[ 📢 Prerequisite for using this feature ] ||
|---|---|
|Provide official account |Provide a WeChat verified service account |
|Complete channel integration |In the GMP "Management Center \- Channel Management \- WeChat Official Account" interface, complete the official account authorization. |
|Activate GMP permissions |The administrator enables the viewing permissions for the SMS channel via the path: Management Center\-Channel Management\-WeChat Official Account\-View<br><br>The administrator enables the creation of rule creation segments, with the permission path "Message Delivery \- Message Delivery Task \- New/View/Edit/Delete" |
|Enable Segment Permissions |There are 3 types of Segment Permissions:<br><br>If VeCDP is purchased, then Segment Permissions need to be enabled in VeCDP under "Segment \- Exclusive Segment \- View/Add/Delete/Edit," which allows the use of the segment feature in Task Creation.<br><br>If VeCDP is not purchased but Datafinder is, then Segment Permissions need to be enabled in Datafinder under "Segment," which allows the use of the segment feature in Task Creation.<br><br>If neither VeCDP nor Datafinder is purchased, this Permission can be disregarded. |


<span id="3dbceaa7"></span>
### **3. Function Description**

**Step 1: Create a New Message Delivery Task**

Add a Message Delivery Task, select the subject and the "Official Account Group Message Channel," and choose the corresponding official account.

Subject: Also known as entity/object, commonly refers to individuals, vehicles, venues, etc., that can be operated for growth or subjected to Insight Analysis. If there are multiple analysis or delivery subjects, it is called multi\-subject. **If you buy VeCDP and also purchase the "Multi\-subject Module," you can support reaching any subject on GMP, such as needing to touch users, merchants by activating multiple subjects**. If you did not purchase this module, you can ignore this concept and the function description.

<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/e4ec1e5ad56a44c8812f126fa2444b8a~tplv-goo7wpa0wc-image.image" width="439px" /></div>


**Step 2: Fill in basic task information**

<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/e814173fc9984db795822f564a70c280~tplv-goo7wpa0wc-image.image" width="439px" /></div>



|Field |Meaning and Purpose of Fields |
|---|---|
|Task Name |Mandatory, used to distinguish between different tasks (strategies), and must not be duplicated with other tasks. |
|Task Grouping |Optional; you can group different tasks into separate groups for subsequent analysis based on task grouping. The grouping of Message Delivery and Process Canvas is isolated; the data is not shared.<br><br>If the existing grouping options do not meet the requirements, you can create or edit them through "Manage Groups". Only project administrators and group administrators can add new groups. If there are existing Message Delivery Tasks in a group, you cannot "delete" the group unless there are no Message Delivery Tasks in it. |
|Associated Campaign |Optional; tasks can be attributed to different campaigns, such as "Double Eleven Campaign", for subsequent analysis based on the associated campaign. Tasks related to Message Delivery, Process Canvas, or Placement can be associated with the same campaign. |
|This task is related to the application |Behavioral data generated by this Message Delivery Task will be channeled back to Datafinder. If Datafinder is not purchased, this capability can be ignored. |


**Step 3: Fill in target audience information**

The target audience represents the user scope this task needs to reach. The Official Account group message supports five methods for the target audience: rule creation segment, existing segments, uploaded segments, WeChat Labels segments, and All users. If the purchase combination differs, the capabilities of the target audience will also vary. If you purchase GMP and VeCDP simultaneously, you can create a new segment under "rule creation segment"; if you purchase GMP and Datafinder (without purchasing CDP), you can create a new segment in the existing segments; **if neither is purchased, it is not possible to support segment creation on the GMP side.** 

<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/da4a4ac2100143cf85f64cd93c8fc670~tplv-goo7wpa0wc-image.image" width="439px" /></div>


 **(1) Rule creation segment**

**After purchasing VeCDP, you can use "rule creation segment" to create segments**, which can be done by combining labels, attributes, segment packages, detailed data, and behavioral data.


|Field |Meaning and Usage of Field |
|---|---|
|Filter Conditions |**After purchasing VeCDP, groups can be created via the 'rule creation segment' method**, which allows for filtering through labels, attributes, segments, detailed data, and behavioral data, and supports user filtering by ID type. Detailed operation instructions for filtering can be found in the VeCDP manual (Chapter: Creating Private Segments). The functional permissions for this filtering capability are consistent with the segment editing permissions on the VeCDP side; therefore, the "Edit, Delete, Add Segment" permissions must be activated to use this capability, otherwise, new segments cannot be created.<br><br><span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/c2027e0ddb4c4ccb82bca34f3189d05d~tplv-goo7wpa0wc-image.image) </span> |
|Sync to the CDP Segment List |Turning the switch on means the segments created here will be visible in the VeCDP segment list, and the segment name defaults to the Message Delivery Task Name + Message Delivery Task ID. If the switch is turned off, the segment created this time will not be visible in the VeCDP segment list and cannot be used for segment filtering again. The administrator can "set" the default checkbox status.<br><br><span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/0ce6905121984a96b7b4751b3cee68b9~tplv-goo7wpa0wc-image.image) </span> |
|Audience Estimation |After configuring the segmentation conditions, click "Audience Estimation" to pre\-calculate the number of IDs within the segment. The ID numbers include two types: OneID numbers and the number of IDs currently being sent through the channel. Use the estimated results to decide whether to adjust the segmentation condition settings. |
|Segment Authorization Given To |Optional, authorize the segment created from labels and behaviors, and select which roles can have viewing permissions for this segment. If no authorization is provided, prompts for missing segment permissions will appear when viewing, editing, or copying tasks. |
|Supplemental Delivery |Optional, tester IDs can be entered, and upon submission, the entered user will be set as the target audience by default when the task is executed. Multiple IDs can be entered. |


When saving drafts or submitting for approval, the system will automatically create this segment, and the ID type of the segment will be the target ID type of the channel, such as the Official Account Active Message channel will create a segment package of appid+openid.

 **(2) Existing Segments**

By using this feature, you can directly select and reach out to the pre\-selected segments.

**Permissions required to use this feature:** 

If you purchase GMP and VeCDP simultaneously, this feature will pull segments from VeCDP. To use this feature, you must enable the "View Segments" permission in VeCDP.

If you purchase GMP and Datafinder (without purchasing VeCDP), this feature will pull segments from Datafinder. To use this feature, you must enable the "User Segmentation" permission in Datafinder.

<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/0e6ce08c97a9470eba897813140a45ce~tplv-goo7wpa0wc-image.image" width="439px" /></div>



|Field |Field Meaning and Purpose |
|---|---|
|Segment List |Mandatory, a segment must be selected for this outreach. If the VeCDP's multi\-subject capability is purchased, this list will automatically pull the segment list of this task's subject. |
|Audience Estimate |After selecting a segment, the system will automatically calculate the number of sending IDs on the current channel. |
|Create New Segment |If both GMP and VeCDP are purchased, clicking this feature will redirect to the VeCDP segment list, where a new segment can be created. If GMP and Datafinder are purchased together (without purchasing VeCDP), clicking this feature will allow the creation of new segments. If neither VeCDP nor Datafinder is purchased, this capability is unavailable.<br><br><span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/21749e790b0e4af194756afc38e19d81~tplv-goo7wpa0wc-image.image) </span> |
|Additional dispatch |Optional, the tester's ID information can be entered, and once filled in, this user will be the default recipient when the task is executed. Multiple IDs can be entered. |


 **(3) Upload Segments**

Supports uploading segments via local CSV files, but the actual upload entry is located in "Message Delivery Configuration", not completed in this step.

**Segment uploads do not support event\-triggered tasks**: Current segment uploads only support scheduled message delivery tasks.

**Segment upload does not support task exclusion function**: Once this selection method is chosen, the option to exclude tasks in the reach configuration will not be displayed.

**When uploading segments**: The segment ID type only supports the upload of the target ID type used in this channel. If it's currently the SMS channel, then only mobile numbers are supported for upload.

**If the user IDs in the uploaded segment are not in the VeCDP system or Datafinder system**: \*\*\*\* support for sending is still available. However, if in this situation, tags, properties, and ID information are inserted into the reach content, it will result in a sending failure.

<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/54d7f1028645422ca431a8dfdc131f03~tplv-goo7wpa0wc-image.image" width="439px" /></div>



|Field |Field meaning and purpose |
|---|---|
|Additional dispatch |Optional, the tester's ID information can be entered, and once filled in, this user will be the default recipient when the task is executed. Multiple IDs can be entered. |


 **(4) WeChat Labels Segment**

Official Account Group Messages can be sent through "WeChat Labels Segment." WeChat Labels are synchronized with the WeChat Official Account platform. After selecting a specific label, all users corresponding to that WeChat label will be reached.

<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/9f1e144ee7074c438ea09b8d30707c3a~tplv-goo7wpa0wc-image.image" width="439px" /></div>


 **(5) All Users**

All users in the current project are supported only for the following two types of reach tasks: Event\-Triggered: Completion of Event A, and Event\-Triggered: Event A Completed & Event B Incomplete. This indicates that after the event is triggered, no further audience filtering is performed, and all users meeting the event criteria will be reached.

<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/a56455e39d854b8fb83453129fa7b8a8~tplv-goo7wpa0wc-image.image" width="439px" /></div>


**Step 3: Configuration of Trigger Conditions**

**Supports four modes: Scheduled \- One\-Time, Scheduled \- Repeated, Event\-Triggered: Completion of Event A, and Event\-Triggered: Event A Completed & Event B Incomplete.** 

**Message Delivery Task Type**: Represents the trigger timing for this message delivery, and Official Account Group Message only supports "Scheduled \- One\-Time" and "Scheduled \- Repeated" modes.


* **Scheduled \- One\-Time**: Will only reach users at a fixed point in time.

* **Scheduled \- Repeated**: Within a time period, can reach users at fixed points multiple times, such as daily at 10 AM within March.


An Official Account can send only four group messages to a user in one month (including those created in the Official Account backend). Exceeding this limit will result in delivery failure.

<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/b3f34f55991a4c8db0eb9bb06a572655~tplv-goo7wpa0wc-image.image" width="439px" /></div>


 **(1) Meaning of the term Scheduled \- One\-Time**


|Field |Field meaning and purpose |
|---|---|
|Reach Time |Required. If the trigger condition type is "Scheduled \- One\-Time," this field is required and represents the time point when the user is reached. |
|Approval Timeout |Required. If the task has not been approved by the "Reach Time," you can choose to cancel the task or execute it immediately after approval. Even if "Execute Immediately After Approval" is selected, if not approved within 72 hours, the task will automatically be canceled. |
|Refresh Before Execution |Required.<br><br>**If you have purchased GMP + VeCDP or GMP + finder**<br><br>**If the selected segment is "Update on Demand"** : If "Refresh Segment before Execution" is checked, the system will automatically refresh the segment data 15 minutes in advance. If the task is scheduled for 15:00, the system will refresh the segment at 14:45. If adjustments to the 15\-minute interval are desired, please contact the project manager or Customer Success Manager.<br><br>**If the selected segment is "Update Daily"** : It will be updated at the time set during segment creation.<br><br>Notably: **Scheduled \- One\-Time, rule creation segment, will default to creating a "Update on Demand" segment.** <br><br><span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/0c2e019b275e449abf82449d14b5140d~tplv-goo7wpa0wc-image.image) </span><br><br>**If GMP + VeCDP or GMP + finder are not purchased**<br><br>then the system does not support refreshing segments. |
|Segment refresh failed |Required.<br><br>**If GMP + VeCDP has been purchased or GMP + finder has been purchased:** <br><br>**If the chosen segment is "Update on Demand"** : After a refresh failure, you can choose to send using the currently acquired segment data or not send at all.<br><br>**If the chosen segment is "Update Daily"** : After a refresh failure, it will default to using the currently acquired segment data for sending.<br><br>**If GMP + VeCDP or GMP + finder has not been purchased**<br><br>then this option is not available. |


 **(2) Meaning of the term Scheduled \- Repeated**


|Field |Field Meaning and Usage |
|---|---|
|Recurrence Cycle |If the trigger condition type is "Scheduled \- Repeated", this field is required. It represents the time point for reaching users in each cycle. |
|Start and End Time |If the trigger condition type is "Scheduled \- Repeated", this field is required. It represents the operating duration of the task. |
|Approval Timeout |Required. If the task is not approved by the "arrival time," you can choose to cancel the task or execute it immediately after approval. Even if "execute immediately after approval" is selected, if the approval is not completed within 72 hours, the task will be automatically canceled. |
|Refresh segment before execution |Required.<br><br>**If you purchased GMP + VeCDP or GMP + finder**<br><br>**If the chosen segment is "updated on demand"** : If "Refresh segment before execution" is checked, the system will default to refreshing the segment data 15 minutes in advance. For example, if the task is executed at 15:00, the system will refresh the segment at 14:45. If you wish to adjust the 15\-minute interval, you can contact the project manager or Customer Success Manager.<br><br>**If the selected segment is "updated daily"** : it will be updated according to the time set when the segment was created.<br><br>**If the selected segment is "updated in real\-time"** : the segment will be updated in real\-time.<br><br>Specifically: **Scheduled \- Repeated, rule creation segment, will by default create a "on\-demand update" segment.** <br><br><span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/bee38e07e7244cd9ac1f8ea11223f2bd~tplv-goo7wpa0wc-image.image) </span><br><br>**If GMP + VeCDP or GMP + finder is not purchased**<br><br>then the system temporarily does not support refreshing the segment. |
|Segment refresh failed |Mandatory.<br><br>**If GMP + VeCDP is purchased or GMP + finder is purchased:** <br><br>**If the selected segment is "updated on\-demand"** : after a refresh failure, you can choose to use the segment data currently obtained by the system for sending, or choose not to send.<br><br>**If the selected segment is "updated daily"** : after a refresh failure, it will default to using the segment data currently obtained by the system for sending.<br><br>**If GMP + VeCDP or GMP + finder is not purchased**<br><br>then this option is unavailable. |


**Step 4: Messaging Configuration**

This step involves filling in the messaging content and setting frequency control/do\-not\-disturb/exclusive conditions for delivery.

<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/49def97257c8426dbc1af34d388ce177~tplv-goo7wpa0wc-image.image" width="439px" /></div>



|Field |Meaning and purpose of the field |
|---|---|
|Channels |The system will default to the channels selected in Step1, which can be modified. Upon modification, the entered message content will be cleared, but other data will be preserved. |
|Enable traffic allocation experiment |For detailed logic, please refer to the "A/B Experiment" section |
|Task type |Mandatory, includes regular campaigns, urgent campaigns, and notification campaigns.<br><br>**Task type affects task priority, and task priority affects the logic of which task triggers first when multiple tasks trigger simultaneously (when the message queue sent becomes backlogged)** : tasks with higher priority trigger first.<br><br>Priority: Notification messages \> Urgent campaigns \> Regular campaigns. Each task activation consumes the corresponding channel’s frequency control count once.<br><br>For the special task type of notification messages, they can still be triggered after the channel’s frequency control count is exhausted. |
|Reply content |Mandatory, the reply content is the content that will be sent out in a mass dispatch, supporting four types: text messages, image messages, graphic messages, WeChat coupons.<br><br>**Text messages**: You need to manually enter the information to be sent in the mass dispatch.<br><br>**Image messages**: Relevant WeChat images can be imported into the GMP's Resource Center, and can be used when sending WeChat mass messages after import.<br><br>**Graphic messages**: The system will automatically pull the graphic messages created on WeChat, which can be chosen for use during WeChat mass messaging.<br><br>**WeChat coupons**: The system will automatically retrieve the coupons created on WeChat, which can be selected for use during WeChat mass messaging.<br><br><span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/9ccc02c249dd4105997d2e7e84892fb7~tplv-goo7wpa0wc-image.image) </span> |
|Test sending |To perform an actual test on the push content, please specify the target ID and variable values. |
|Global Reach Limit |Also known as channel access frequency control. The page displays the selected channel's frequency control. If it doesn't meet the requirements, you can adjust the channel frequency control by clicking "View" \-\-\> "Enter 'Settings Center'." Note, the page will not automatically sync after adjusting the frequency control, and you need to manually refresh the configuration page to sync the latest frequency settings.<br><br>Turning off "Global Reach Limit" means that the messages sent this time will not be affected by this channel’s or cross\-channel frequency control limits. |
|Cross\-channel Frequency Control |The current version supports setting up cross\-channel frequency control, for instance, Channel A + Channel B can be reached a maximum of once per day. The corresponding configuration data will be displayed here. |
|Channel Do Not Disturb Period |The SMS channel can ignore this field. |
|Do Not Disturb Settings |You can set a Do Not Disturb period. If the system plans to send messages during this period, they will be restricted by the Do Not Disturb setting. |
|Do Not Disturb Access Rules |If filtered out due to hitting Do Not Disturb conditions, you can choose to "Abandon this reach" or "Continue reaching after Do Not Disturb ends". |
|Message Delivery Task Frequency Control |If the current task's trigger conditions are "Scheduled \- Repeated", "Event\-Triggered: Completion of Event A", or "Event\-Triggered: Event A Completed & Event B Incomplete", the user may be reached multiple times. This field allows you to set how to control frequency within this task.<br><br><span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/d799d28d72b046d5a7ef5c01492c72f5~tplv-goo7wpa0wc-image.image) </span> |
|Exclude Task |Optional.<br><br>This indicates that the selected task is mutually exclusive with the current task, and the target users (same user ID) will only be reached by one of the tasks. That is, Task A and Task B are mutually exclusive. If a user is successfully reached by Task A, they will not be reached by Task B, and vice versa. Search by task name or ID is supported. Currently, only the top 50 task data are displayed. For more tasks, please search and find. |


**Step 5: Monitoring Metrics**

**This feature can be used to track the post\-reach conversions completed by the reached users**. "Focus Metric Settings" is off by default; when switched on, you can set the focus metrics for the task.

<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/de6d3317283a4ffa98fcaefd4b962e86~tplv-goo7wpa0wc-image.image" width="439px" /></div>



|Field |Meaning and Purpose of the Field |
|---|---|
|Configuration Method |You can either create a new indicator or use an existing one. |
|Indicator Name |Mandatory.<br><br>Examples: Add to cart, create order, GMV. When creating a task, the indicator name you enter will be reflected on the Data Analysis page.<br><br><span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/0bba31146b9149aeb2646905a8f492e4~tplv-goo7wpa0wc-image.image) </span> |
|Calculation Conditions |**Calculation based on real\-time behavioral data**<br><br>Real\-time behavioral calculation: If a behavioral data source has real\-time kafka messages, indicators such as the number of occurrences per person for real\-time behaviors can be set. Once set, Data Analysis will reflect the results in real time.<br><br>After selecting the data source and events, the system will automatically tally the occurrence of that behavior post\-engagement. After setting filter conditions, the system will only tally events that meet these conditions.<br><br>Once set, the system will automatically calculate the number of visits and the metrics of individuals.<br><br><span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/5e2eac62cb4b46c0a52b6959ebd13439~tplv-goo7wpa0wc-image.image) </span><br><br>**Calculation based on offline behavioral data**<br><br>Offline behavioral calculation: It is possible to tally the occurrence of all behavior events. Once set, Data Analysis will reflect the results on the following day.<br><br>After selecting the data source and events, the system will automatically tally the occurrence of that behavior post\-engagement. After setting filter conditions, the system will only tally events that meet these conditions.<br><br>Once set, the system will automatically calculate the number of visits and the metrics of individuals.<br><br>The system will compile the metric data at 5, 11, 17, and 23 o'clock every day.<br><br><span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/f9ba145855a34b08b3fb1d356d465995~tplv-goo7wpa0wc-image.image) </span><br><br>**Calculate through detailed data**<br><br>Detailed data calculation: Through the "Detailed Data Source" in the CDP system, you can compile statistics like the number of orders from the order table, and cumulative GMV data.<br><br>After selecting the data source and fields, the system will automatically count the number of entries that meet the filter conditions post\-reach. If the selected field is numeric, it supports operations like "sum" or calculation of the "frequency/number of people".<br><br><span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/84e14c82ec4f4387b206834a13c58c66~tplv-goo7wpa0wc-image.image) </span> |
|Window period |This refers to the window period in which data is compiled after the user has been reached. |
|Do not reach out after event completion |For scheduled repeat and trigger\-based tasks where a user might be reached multiple times, you can select this option if you want no further reach\-outs after a user completes a specific action. This capability is only available when the selected event is a "real\-time behavioral data source".<br><br><span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/6bceca15a2194c199bbbaae04f9a25c8~tplv-goo7wpa0wc-image.image) </span> |


You can add up to 7 focus metrics. After adding metrics, **comprehensive attribution statistics will be conducted, counting users who complete actions or generate order data during the window period**. For instance, if a user is reached by both Task a and Task b, and both tasks set the "Mini Program Page View" as a focus metric, then this data will be counted in both tasks.

<span id="5ca5834a"></span>
## **WeChat Mini Program Pop\-up**

<span id="d3c348a9"></span>
### **Product Overview**

This feature supports millisecond response times, customizable templates, and offers visual editing capabilities.

<span id="3605bc73"></span>
### **Usage Restriction**


| |Detailed description |
|---|---|
|Provide mini programs |Provide mini programs that require pop\-up prompts |
|Complete channel integration |Contact the project manager or the customer success manager to complete the channel integration. |
|Activate GMP permissions |Administrator activates the view permission for the SMS channel; Permission path: Management Center \- Channel Management \- WeChat Mini Program \- View<br><br>Administrator grants permissions for Task Creation rule creation segment; Permission path: Message Delivery \- Message Delivery Task \- Create/View/Edit/Delete |
|Activate segmentation permissions |There are three scenarios for activating segmentation permissions:<br><br>If VeCDP is purchased, you need to activate permissions in VeCDP under "Segment \- Private Domain Segment \- View/Add/Modify/Delete". Once activated, you can use the segment feature in Task Creation.<br><br>If you have not purchased VeCDP and only purchased Datafinder, you need to activate the "Segment" permission in Datafinder. After activation, you can use the segmentation function in Task Creation.<br><br>If neither VeCDP nor Datafinder have been purchased, this permission can be ignored. |


<span id="59bf1cc3"></span>
### **Function Description**

**Step 1: Create New Message Delivery Task**

Add Message Delivery Task, select the mini programs for pop\-up messages.

Subject: Also known as entity/object, this term often refers to people, vehicles, venues, etc., that can be studied for growth or insight analysis. If there are multiple subjects of analysis or engagement, it is referred to as multi\-subject. **If you purchase VeCDP and add the "multi\-subject module" at the same time, you can support engaging any subject in GMP, for instance, reaching out to users and merchants requires enabling multi\-subject.**  If this module is not purchased, you can ignore this concept and its functionalities.

<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/54352b179a6541b38559594d5cbdcbab~tplv-goo7wpa0wc-image.image" width="439px" /></div>


**Step 2: Fill in the Basic Information of the Task**

<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/89ac7b69ca5242128d801c5090bc83f4~tplv-goo7wpa0wc-image.image" width="439px" /></div>



|Field |Meaning and Purpose of the Field |
|---|---|
|Task Name |Required, used to distinguish different tasks (strategies), must not be duplicated with other tasks |
|Task Grouping |Optional, allows placing different tasks into different groups for subsequent analysis based on task grouping. The grouping in Message Delivery and Process Canvas is isolated, data is not interchangeable.<br><br>If the existing grouping options do not meet the requirements, you can create or edit through "Manage Groups". Only project administrators and group administrators can add new groups. If there are existing message delivery tasks in the group, the group cannot be "deleted." It can only be deleted when there are zero message delivery tasks in the group. |
|Associated Campaign |Optional. Tasks can be attributed to different campaigns, such as the "Double Eleven Campaign," for subsequent analysis based on the campaign associated with tasks. Message delivery, process canvas, or placement tasks can be associated with the same campaign. |
|Task\-related applications |This task represents that the data generated by the message delivery behavior will be feedback to Datafinder under this application. If Datafinder is not purchased, this capability can be ignored. |


**Step 3: Fill in the Target Audience**

The target audience represents the range of users the task aims to engage. The target audience supports four methods: rule creation segment, existing segments, uploaded segments, and all users. The scope of capabilities available to the target audience varies with different purchase combinations. If VeCDP is purchased along with GMP, new segments can be created under "rule creation segment"; if Datafinder (without purchasing CDP) and GMP are purchased together, new segments can be created under "existing segments"; **if neither is purchased, it is not possible to create segments in GMP.** 

<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/598b4615eeba48249e28a34ca00ed5c9~tplv-goo7wpa0wc-image.image" width="439px" /></div>


**Label and Behavior Rule Creation Segment**

**After purchasing VeCDP, you can create segments using the method of 'Label and Behavior Rule Creation Segment'** , which allows rule creation through labels, attributes, segment packages, detailed data, and behavioral data.


|Field |Field meaning and purpose |
|---|---|
|Selection conditions |**After purchasing VeCDP, you can use "rule creation segment" to create segments, which allows combining labels, properties, existing segments, detailed data, and behavioral data for selection, and supports filtering users by ID type.**  For detailed operating instructions on selection, refer to the VeCDP manual (chapter: Creating Private Domain Segments). This selection ability has the same function permissions as the VeCDP side segment editing permissions, hence using this ability requires enabling the VeCDP "Add/Delete/Edit Segment" permission, otherwise, it will not be possible to create new segments.<br><br><span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/8fb12d8ab7694f40b4cb269e158d29eb~tplv-goo7wpa0wc-image.image) </span> |
|Synchronize to the CDP segment list |If the switch is turned on, the segments created here will be visible in the VeCDP segment list, and the segment name defaults to Message Delivery Task Name + Message Delivery Task ID. If the switch is turned off, the segments created this time will not be visible in the VeCDP segment list, and cannot be used again for segment selection. The administrator can "set" the default check state.<br><br><span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/ffcc63fb500548aa89999c014ff22b7f~tplv-goo7wpa0wc-image.image) </span> |
|Audience estimation |After configuring the segment conditions, click "Audience estimation" to calculate in advance the number of IDs in the segment. The ID count includes two types: OneID count and the number of IDs sent via the current channel, which can determine whether to adjust the segment selection conditions based on the estimation results. |
|Authorize the segment to |Optional, authorize the segment created by rule creation to certain roles for viewing permission. If authorization is not performed, accessing, editing, or copying tasks will prompt a lack of segment permissions. |
|Supplementary Send |Optional, you can enter the ID information of the tester. After entering, the user will be selected as the target audience by default during task execution. Multiple IDs can be entered. |


When saving a draft or submitting for approval, the system will automatically create the segment. The ID type of the segment corresponds to the target ID type of the channel, such as the Public Account Active Message channel will create a segment package with appid+openid.

 **(2) Existing Segments**

With this function, you can directly choose and reach out using the already created segments.

**Required permissions to use this function:** 

If you purchase GMP and VeCDP simultaneously, this function will pull segments from VeCDP. To use this function, you need to enable the VeCDP 'View Segment' permission.

If you purchase GMP and Datafinder simultaneously (without purchasing VeCDP), then this function will pull segments from Datafinder. To use this function, you need to enable the Datafinder 'Segment' permission.

<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/4c5b8b52d001490a8cfa3f98c033eaa2~tplv-goo7wpa0wc-image.image" width="439px" /></div>



|Field |Field meaning and usage |
|---|---|
|Segment List |Mandatory, you need to select the segment for this message delivery. If the multiple subject capabilities of VeCDP are purchased, this list will automatically pull the segment list of the subject of this task. |
|Audience Estimation |After selecting a segment, the system will automatically calculate the number of IDs sent through the current channel. |
|Create New Segment |If GMP and VeCDP are purchased together, clicking this feature will redirect to the VeCDP segment list, where you can create a new segment. If GMP is purchased along with Datafinder (when VeCDP is not purchased), clicking this feature will support creating a new segment. If neither VeCDP nor Datafinder is purchased, this capability is not available.<br><br><span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/e759c5d689f048468433055a63702482~tplv-goo7wpa0wc-image.image) </span> |
|Supplement Sending |Optional, you can enter the IDs of test personnel; once entered, this user will be set as the audience by default during task execution. Multiple IDs can be entered. |


**All Users**

This represents all users under the current project, **All Users only support two types of outreach tasks: Event\-Triggered: Completion of Event A, and Event\-Triggered: Event A Completed & Event B Incomplete**, meaning that after the user triggers an event, no further audience filtering is done and all users meeting the event conditions are reached.

<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/10d94ce6168a43d6a58259fe8dfdb25d~tplv-goo7wpa0wc-image.image" width="439px" /></div>


**Step 3: Setting Trigger Conditions**

The WeChat Mini Program Pop\-up supports only one method: "Event\-Triggered: Completion of Event A".

**Message Delivery Task Type**: Represents the timing of the trigger for this message delivery.

**Event\-Triggered: Completion of Event A**: Triggers when a user completes an action (can be immediate/delayed), such as triggering a pop\-up when a user completes a post by saving, liking, or sharing it. Within the valid task duration, meeting the trigger conditions can enable multiple triggers.

<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/e9e5aecfb3b54b86b3a7d3caae2bb3bc~tplv-goo7wpa0wc-image.image" width="439px" /></div>


 **(1) Meaning of the fields for Event\-Triggered: Completion of Event A**


|Field |Field Meaning and Purpose |
|---|---|
|Trigger Event |Required.<br><br>**This event represents what kind of event the user completes to trigger this process**, users who complete the event will be filtered based on "target audience," and only those who meet both "trigger conditions + target audience" will actually be contacted.<br><br><span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/a008fa3e7fcd4c50987e664446d78169~tplv-goo7wpa0wc-image.image) </span><br><br>**Cumulative Completion of A / Each Completion of A**: Completing A 3 times cumulatively means the user, after completing the event, will only be contacted once; completing A 3 times each means the process will be triggered every time the user completes A 3 times.<br><br>**Immediate Contact / Delayed Contact / Delay Specified Time Contact**:<br><br>Immediate contact means contacting right after the event is completed.<br><br>Delayed contact means delaying the contact by a relative time, delaying by 1 day means delaying for 24 hours; the delay can be up to 365 days.<br><br>Delay specified time contact means waiting until a specific time after the event has occurred before contacting. |
|Start and End Times of Event A |Required. All events A occurring within this field during this timeframe will trigger the process. |
|Message delivery task end time. |The system fills in defaults automatically.<br><br>After reaching the end time, the status of the message delivery task will change to completed, and the system will not continue message delivery even if event A is delayed. |
|Refresh the segment before executing. |**If you have purchased GMP + VeCDP or GMP + finder.** <br><br>**If the selected segment is "on\-demand update"** , the segment will not be refreshed.<br><br>**If the selected segment is "daily update"** , the system will refresh according to the set time. If the "rule creation segment" is used, segments are by default refreshed daily at 06:00.<br><br>Specifically: **Trigger type \- Completion A, rule creation segment, will by default create a "daily update" segment.** <br><br><span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/7ec37dcbd7fa491b85fa925a93e8b2c3~tplv-goo7wpa0wc-image.image) </span><br><br>**If GMP + VeCDP or GMP + finder is not purchased**<br><br>The system does not support refreshing segments temporarily. |
|Refresh segment failed |Mandatory.<br><br>**If GMP + VeCDP or GMP + finder was purchased**: After a refresh failure, it will still use the latest data for assessment.<br><br>**If GMP + VeCDP or GMP + finder was not purchased:**  This option is not available. |


**Step 4: Message Delivery Configuration**

This step involves writing the message content and setting conditions for frequency control, do not disturb, and mutual exclusion.

<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/864c972fab98466d829c10ae2d6fafdf~tplv-goo7wpa0wc-image.image" width="439px" /></div>



|Field |Field meaning and usage |
|---|---|
|Channels |The system will default to the channel selected in Step1, which can be modified. Modifying will clear the entered message content, but other data will be preserved. |
|Task Type |Mandatory, includes regular campaigns, urgent campaigns, and notifications.<br><br>**Task type affects task priority, which influences the logic of which task gets triggered first when multiple tasks trigger at the same time (when there's a buildup in the message queue)** : the task with higher priority is triggered first.<br><br>Priority: Notification messages \> urgent campaigns \> regular campaigns. Each task is triggered once and consumes a count of frequency control on the respective channel.<br><br>For special notification message type tasks, they can still be triggered even after frequency control limits on the channel are reached. |
|Popup Priority |Mandatory, includes regular campaigns, urgent campaigns, and notifications.<br><br>**Task type affects task priority, which influences the logic of which task gets triggered first when multiple tasks trigger at the same time (when there's a buildup in the message queue)** : the task with higher priority is triggered first.<br><br>Priority: Notification messages \> urgent campaigns \> regular campaigns. Each task is triggered once and consumes a count of frequency control on the respective channel.<br><br>For special notification message type tasks, they can still be triggered even after frequency control limits on the channel are reached. |
|Activate Split Testing |For detailed logic, please refer to the "A/B Experiment" section |
|Popup Content Settings |Required. Popup content settings require selecting a template first before setting detailed content. Popup templates can be either standard templates (system built\-in) or custom templates (created via visual drag\-and\-drop). **Popup content settings include:**  layer settings, component settings, and popup settings.<br><br>**Layer settings** allow custom settings for background color, background image, layer click behavior, and close button positioning.<br><br><span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/4a596193285c4945a5439bac7616ea5a~tplv-goo7wpa0wc-image.image) </span><br><br>**Popup settings** support custom settings for background color, background image, and rounded corners.<br><br>**Component settings** vary in the scope of custom settings for image, document, and button components.<br><br><br>* **Image component**: Supports custom settings for uploading images and actions upon clicking. The width and height cannot be customized and are determined by channel settings.<br><br>* **Text component**: Supports custom settings for font size, color, line spacing, indentation, text alignment, and text (can be multiline). The maximum length cannot be customized and is determined by channel settings.<br><br>* **Button component**: Supports custom settings for corner radius, button color, button text size and text color, button copy content, and clicking actions. Button type, button width and height, and horizontal alignment cannot be customized and are determined by channel settings.<br><br><br><span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/dd9fb19999424c2bb67a7369d24ac391~tplv-goo7wpa0wc-image.image) </span> |
|Test dialog window |Perform actual testing on the mini program dialog, which requires scanning a QR code via WeChat for preview.<br><br><span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/02bb2e44a4d842e4a3af5787cd91a100~tplv-goo7wpa0wc-image.image) </span> |
|Global reach limit |This refers to the channel reach frequency control limits. The page displays the selected channel frequency control. If it does not meet the requirements, you can adjust the channel frequency control by clicking "View" \-\-\> "Enter Settings Center". Note, after the frequency control adjustment, the page will not automatically sync; you must manually update the configuration page to sync with the latest frequency control settings.<br><br>If you turn off "Global Reach Limits," it means the messages sent this time will not be subject to this channel's frequency control or cross\-channel frequency restrictions. |
|Cross\-channel Frequency Control |The current version supports setting Cross\-channel Frequency Control, such as Channel A + Channel B, with a maximum reach of once per day. The corresponding configuration data will be displayed here. |
|Do Not Disturb Period for Channels |The SMS Channel may ignore this field. |
|Do Not Disturb Settings |You can set a Do Not Disturb Period. If the system plans to send a message during this period, it will be restricted by Do Not Disturb. |
|Frequency Control for Message Delivery Tasks |If the trigger conditions for the current task are "Scheduled \- Repeated," "Event\-Triggered: Completion of Event A," or "Event\-Triggered: Event A Completed & Event B Incomplete," the user may be contacted multiple times. This field allows setting how to control the frequency within this task for the user.<br><br><span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/90a1db7cc70c4058aa32d5c3c256e3d3~tplv-goo7wpa0wc-image.image) </span> |


**Step 5: Focus on Metrics**

**This function can be used to track the conversion of users after they have been reached.**  "Set Focus Metrics" is off by default. You can enable it to set focus metrics for a task.

<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/01a1d34fe62448c5a34cb6beff1f2fc4~tplv-goo7wpa0wc-image.image" width="439px" /></div>



|Field |Meaning and Purpose of the Field |
|---|---|
|Setting Method |You can choose to "Create a new metric" or directly use an "Existing Metric." |
|Target Name |Mandatory.<br><br>Examples: Add to cart, generate order, GMV. |
|Calculation Conditions<br><br>Calculated through real\-time Behavioral Data |**Performance indicators example**: item detail page visits, add\-to\-cart quantity, and homepage views on the mini\-program<br><br>**Conditions required for use**: If a behavioral data source contains "real\-time behavioral messages," then it can set the real\-time behavior tally of occurrences/people under that data source. If unsure about whether the data source meets the conditions, consult either the project manager or the customer success manager.<br><br>**How to configure**: Select the data source and event, and if additional conditions are needed on the event, click 'Filter Conditions' to add them. For instance, to count the item detail page visits one might need to specify the URL of the item detail page, then this functionality can be employed.<br><br><span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/0db7ea1f81ab4fa2a2ddca36ecb68f21~tplv-goo7wpa0wc-image.image) </span><br><br>**What the results of the configuration look like after data analysis**:<br><br>After configuration, the message delivery and process canvas tasks of that channel will automatically monitor that metric.<br><br>This metric will tally the user's conversion during a specified time window after being reached.<br><br>After configuration, as long as the conversion events occur, this metric will be updated in real\-time. |
|Calculation Conditions<br><br>Calculation of Behavioral Data through Offline Activities |**Examples of Metrics**: Product detail page visits, add\-to\-cart rates, homepage views in mini\-programs<br><br>**Conditions for Use**: If a source of behavioral data is updated daily as an "incremental table," then it’s possible to set metrics for the number of occurrences/people for activities under this data source. If you're unsure whether the data source meets the criteria, you can consult a project manager or a customer success manager.<br><br>**How to Configure**: Choose the data source and the event; if you need to add restrictions to the event, click "Filter Conditions" to add them. For example, to count visits to the product detail page, you can use this feature to add restrictions based on the URL of the product detail page.<br><br><span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/afefdcd92a494c469eb4cab0e5f7fb16~tplv-goo7wpa0wc-image.image) </span><br><br>**Results of Data Analysis After Configuration**:<br><br>After configuration, the message delivery and process canvas tasks on this channel will automatically focus on this metric.<br><br>This metric will count user conversions during a specified window after being reached.<br><br>After configuration, as soon as a conversion event occurs, the system will calculate the metric data at 5, 11, 17, and 23 o'clock daily.<br><br>**The difference between this data source and "Using Real\-time Behavioral Data" for statistics**: If there are "real\-time behavior messages", the "Using Real\-time Behavioral Data" feature should be prioritized. If not, "Calculation Based on Offline Behavioral Data" can be used for statistics. |
|Calculation Conditions<br><br>Calculation Based on Detailed Data |**Example Indicators**: Number of Orders, GMV<br><br>**Conditions Required for Use**: If a detailed data is updated daily as an "incremental table," then the indices for detailed behavioral data under this data source can be set. If you are unsure whether this data source meets the conditions, you can consult a project manager or a client success manager.<br><br>**How to Configure**:<br><br>Select the data source and fields. If you need to add restrictions on the event, you can click "Filter Conditions" to add them. For example, to calculate order volume, you can use this feature if you need to restrict product categories.<br><br>If you want to count the occurrences of fields, choose "Number of People/Occurrences".<br><br><span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/fb3d0b770fd7422396c1206fdffca2ea~tplv-goo7wpa0wc-image.image) </span><br><br>To sum fields, simply select "Sum". For instance, GMV metrics require summing up the product amounts.<br><br><span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/373fe3d494b64c49a091ab9c69b90349~tplv-goo7wpa0wc-image.image) </span><br><br>**What are the results of data analysis after configuration?** :<br><br><br>* After configuration, the channel will automatically monitor the metric for message delivery and process canvas tasks.<br><br>* The metric will track the user conversions within a specified window after being reached.<br><br>* After configuration, as long as a conversion event occurs, the system will tally the metric data at 5, 11, 17, and 23 o'clock daily. |
|Calculation Conditions<br><br>Composite Metrics |**Composite Metrics**<br><br>Metric examples: Add\-to\-cart rate, customer price per order, SMS sending cost<br><br>Clicking it allows for combinations between indicators. You can select indicators or input values.<br><br>Indicator Selection: Only supports selecting Sent Volume, Delivery Volume **and indicators already selected on the current page**<br><br><span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/dc5394d11d4b4244a4a9e41fc768a688~tplv-goo7wpa0wc-image.image) </span><br><br>Input Values: Clicking the selection box also allows direct input of values for calculating metrics such as "SMS Sending Cost."<br><br><span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/8bb0fef6b59f41bf89f675a4ca812044~tplv-goo7wpa0wc-image.image) </span> |
|Window Period |Refers to the data collected within a specific time window after reaching the user. |


<span id="719cc48e"></span>
## **1.7 Mini Program Subscription Messages**

<span id="274dda71"></span>
### **1. Product Overview**

One\-time subscription messages are designed to address notification needs in the service process following the use of mini programs. After subscribing independently, developers can issue a corresponding service message at any time; each message can be subscribed to or unsubscribed individually. In other words, the customer must first authorize a subscription before they can be reached.

<span id="da81b5b2"></span>
### **2. Usage Restrictions**


| |Detailed Description |
|---|---|
|Provide a mini program |Provide a mini program for subscribing to messages |
|Complete channel integration |Contact the project manager or client success manager to access channels. |
|Enable GMP permissions |The administrator enables the viewing permissions for the SMS channel, permission path: Management Center \- Channel Management \- WeChat Mini Program \- View<br><br>The administrator authorizes task creation for selecting segments, permission path: "Message Delivery \- Message Delivery Task \- Create/View/Edit/Delete" |
|Enable segment permissions |Enable segment permissions are divided into three scenarios:<br><br>If VeCDP is purchased, you need to enable permissions in VeCDP "Segment \- Private Domain Segment \- View/Add/Delete/Edit," then you can use the segment feature in task creation.<br><br>If VeCDP is not purchased but Datafinder is, you need to enable "Segment" permissions in the Datafinder, after which you can use the segment feature in task creation.<br><br>If neither VeCDP nor Datafinder is purchased, this permission can be ignored. |


<span id="9573cfb2"></span>
### **3. Function Description**

**Create a New Message Delivery Task**

Add Message Delivery Task, select the mini program used to send subscription messages.

Subject: Also referred to as an entity/object, it often denotes individuals, vehicles, venues, etc., that can be targeted for operational growth or insight analysis. When multiple analysis or outreach subjects exist, it is referred to as multi\-subject. **If you purchase VeCDP and add the "multi\-subject module," it enables any subject outreach in GMP, such as reaching customers and merchants who require multi\-subject activation.**  If this module is not purchased, the concept and function description can be ignored.

<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/55e94f1159e346a0808b15b847cb87fc~tplv-goo7wpa0wc-image.image" width="439px" /></div>


**Step2: Enter Basic Task Information**

<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/f552f810f874431ea24ec5fea45647ec~tplv-goo7wpa0wc-image.image" width="439px" /></div>



|Field |Field Meaning and Purpose |
|---|---|
|Task Name |Required, used to distinguish different tasks (strategies), must not be duplicated with other tasks |
|Task Grouping |Optional, different tasks can be placed into different groups for subsequent analysis based on task grouping Message Delivery and Process Canvas groupings are isolated; data is not shared<br><br>If existing grouping options do not meet the needs, new groups can be created or edited via "Manage Groups" New group additions can only be managed by project administrators and group administrators If there are existing Message Delivery Tasks in a group, it cannot be "Deleted" unless the number of tasks in the group is zero |
|Associated Campaign |Optional, allows assigning the task to different campaigns such as "Double Eleven Campaign," for analysis based on the associated campaign later. Tasks from message delivery, process canvas, and placement can be associated with the same campaign. |
|This task is associated with an application |The data related to the message delivery behavior produced by this task will flow back to Datafinder under this application. If you have not purchased Datafinder, you may ignore this capability. |


**Step3: Enter the Audience**

The audience represents the scope of users who need to be reached for this task. The audience supports four methods: rule creation segment, existing segmentation, uploaded segmentation, and all users. If different combinations are purchased, the capability range of the audience will also vary. If you purchase GMP and VeCDP together, you can create a new segment under "rule creation segment." If you purchase GMP and Datafinder together (without purchasing CDP), you can create new segments within existing segments. **If neither is purchased, creating segments on the GMP side is not supported.** 

<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/3ad0496b2b694ac3823f5f90ac61bf37~tplv-goo7wpa0wc-image.image" width="439px" /></div>


 **(1) rule creation segment**

**After purchasing VeCDP, you can create segments using "rule creation segment,"**  which allows selection through labels, attributes, segment packages, detailed data, and behavioral data.


|Field |Meaning and usage of the field |
|---|---|
|Segmentation Conditions |**After purchasing VeCDP, you can use the "rule creation segment" method to create segments**, which supports segmentation through labels, attributes, segment bundles, detailed data, behavioral data, and allows user filtering by ID type. Detailed operating instructions for segmentation can be found in the VeCDP operation manual (chapter: Creating Private Domain Segments). The permissions for this segmentation capability are consistent with the VeCDP side segment editing permissions. Hence, using this segmentation capability requires enabling VeCDP "add, delete, modify segments" permissions; otherwise, creating new segments would not be possible.<br><br><span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/51da6a7e5d0d4aaa8353e437ce5d80b3~tplv-goo7wpa0wc-image.image) </span> |
|Sync to CDP Segment List |When the switch is on, the segment created here is visible in the VeCDP Segment list, and the segment name defaults to the Message Delivery Task Name + Task ID. When the switch is off, the segment created this time is not visible in the VeCDP Segment list and cannot be used for segment selection again. Administrators can set the default checked state in "Settings".<br><br><span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/bad75feecf614ae29ef9ce253062d8de~tplv-goo7wpa0wc-image.image) </span> |
|Audience Estimate |After configuring the segment conditions, click "Audience Estimate" to calculate the number of IDs in the segment in advance. The ID count includes two types: OneID count and the number of IDs sent via the current channel, allowing adjustment of segment selection conditions based on the estimated results. |
|Segment Authorization |Optional, authorize the segment selected by labels and behavior, choosing which roles can have the viewing permissions for this segment. If not authorized, prompts for no segment permissions will appear when viewing, editing, or copying tasks. |
|Supplementary Sending |Optional, you can enter the ID information of the test personnel. After entering, this user will be set as the target audience by default when the task is executed. You can input multiple IDs. |


When saving a draft or submitting for approval, the system automatically creates the segment, with the ID type corresponding to the target ID type of the channel, such as a Public Account Active Message channel creating a segment package with appid+openid.

 **(2) Existing segments**

Using this function, you can directly select and reach out to pre\-selected segments.

**Permissions required to use this function:** 

If you purchase GMP and VeCDP together, this function will fetch segments from VeCDP. To use this function, VeCDP "View Segment" permission is required.

If you purchase GMP and Datafinder together (without purchasing VeCDP), this function will fetch segments from Datafinder. Activating this function requires enabling the Datafinder "Segment" permission.

<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/72a7f977a8e4420f961e263dff78fcd4~tplv-goo7wpa0wc-image.image" width="439px" /></div>



|Field |Meaning and purpose of the field |
|---|---|
|Segmentation list |Mandatory, need to select the segment for this outreach. If the multi\-subject capability of VeCDP is purchased, this list will automatically pull the segmentation list of the subject for this task. |
|Audience estimation |After selecting a segment, the system will automatically calculate the number of sending IDs for the current channel. |
|Create new segment |If GMP and VeCDP are purchased together, clicking this function will redirect to the VeCDP segmentation list, where a new segment can be created. If a GMP purchase is combined with purchasing Datafinder (without acquiring VeCDP), this function supports the creation of a new segment. If neither VeCDP nor Datafinder is purchased, this capability is not available.<br><br><span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/5a76b3fb451640fe8fd20e67b61080d3~tplv-goo7wpa0wc-image.image) </span> |
|Additional sending |Optional, you can enter the tester's ID information. Once filled, this user will be the default audience during task execution. Multiple IDs can be entered. |


 **(3) Upload Segment**

Segment can be uploaded via a local CSV file, but the specific entry point is in "Message Configuration," and it is not done at this step.

**Segment uploads do not support trigger\-based tasks**: Current segment uploads only support scheduled message delivery tasks.

**Segment uploads do not support the task exclusion feature**: After selecting this type of selection, the option to exclude tasks in the message configuration will not be displayed.

**During segment upload**: The segment ID type only supports uploading the type of target ID that is sent via this channel. For example, if it is currently the SMS channel, only mobile numbers are supported for upload.

**If the user ID in the uploaded segment is not found in the VeCDP system or Datafinder system**: It is still possible to support sending. Notably, if in this case, any labels, attributes, or ID information are inserted in the content to be delivered, it will result in a sending failure.

<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/0b821e7adcc94cc39f22bee0f002b072~tplv-goo7wpa0wc-image.image" width="439px" /></div>



|Field |Field meaning and purpose |
|---|---|
|Additional sending |Optional, you can enter the tester's ID information. Once filled, this user will be the default audience during task execution. Multiple IDs can be entered. |


 **(4) All Users**

Represents all users under the current project, **All users only support two types of message delivery tasks: Event\-Triggered: Completion of Event A, and Event\-Triggered: Event A Completed & Event B Incomplete**, which means that after user\-triggered events, no further audience filtration is done, and all users meeting the event criteria will be reached.

<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/793963c4f91143abbd79047cf218bed9~tplv-goo7wpa0wc-image.image" width="439px" /></div>


**Step 3: Configure Trigger Conditions**

**Supports four modes: Scheduled \- One\-Time, Scheduled \- Repeated, Event\-Triggered: Completion of Event A, and Event\-Triggered: Event A Completed & Event B Incomplete.** 

**Message Delivery Task Type**: Represents the timing of the trigger for this message delivery.


* **Scheduled \- One\-Time**: Occurs only at a fixed time point.

* **Scheduled \- Repeated**: Within a time range, users can be reached multiple times at fixed intervals, such as daily at 10 AM during March.

* **Event\-Triggered: Completion of Event A**: Triggers when a user completes an action (can be immediate or delayed), such as earning points upon completing actions like post bookmarking, liking, or sharing. During the task’s effective period, multiple triggers can be activated if conditions are met.

* **Event\-Triggered: Event A Completed & Event B Incomplete**: Creates an event\-triggered task that activates if the user completes a certain action A and does not complete another action B within a given time, such as triggering a reminder if the app is launched but a page is not visited within 20 minutes. During the task’s effective period, multiple triggers can be activated if conditions are met. Commonly used in interruption marketing.


<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/0cf8e2468e8942abb957b2dcfa0e3d55~tplv-goo7wpa0wc-image.image" width="439px" /></div>


**Scheduled \- One\-Time Meaning**


|Field |Meaning and Purpose of the Field |
|---|---|
|Contact Time |Required. If the trigger condition type is "Scheduled \- One\-Time," this field is required, and it represents the time point to reach the user. |
|Approval Timeout |Required. If the task has not been approved by the "Contact Time," either cancel the task or approve and execute it immediately. Even if "Execute immediately after approval" is chosen, the task will automatically be canceled if not approved within 72 hours. |
|Refresh Segments Before Execution. |Required.<br><br>**If GMP + VeCDP or GMP + finder is purchased**<br><br>**If the selected segment is "Refresh on Demand"** : If "Refresh Segment Before Execution" is checked, the system will automatically refresh the segment data 15 minutes in advance. For example, if the task is executed at 15:00, the system will refresh the segment at 14:45. If you wish to adjust the 15\-minute interval, you can contact the project manager or Customer Success Manager.<br><br>**If the selected segment is "Refresh Daily"** : The segment will be refreshed at the time set during its creation.<br><br>Specifically: **Scheduled \- One\-Time, rule creation segment, will by default create a "Refresh on Demand" segment.** <br><br><span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/42ac22a64db44806922f27da0fb99494~tplv-goo7wpa0wc-image.image) </span><br><br>**If GMP + VeCDP or GMP + finder is not purchased**<br><br>The system does not support refreshing segments yet. |
|Segment refresh failed |Required.<br><br>**If GMP + VeCDP or GMP + finder is purchased:** <br><br>**If the selected segment is 'refresh on\-demand',**  after a refresh failure, you can choose to send using the currently obtained segment data or not send at all.<br><br>**If the selected segment is 'refresh daily',**  after a refresh failure, it will default to sending using the currently obtained segment data.<br><br>**If GMP + VeCDP or GMP + finder is not purchased**<br><br>then this option is not available. |


**Scheduled \- Repeated Meaning**


|Field |Field Meaning and Usage |
|---|---|
|Recurrence Cycle |If the trigger condition type is 'Scheduled \- Repeated', this field is required and represents the time point for reaching users in each recurrence cycle. |
|Start and End Time |If the trigger condition type is "Scheduled \- Repeated," this field is required and represents the running start and end times of the task. |
|Approval Timeout |Mandatory. If the task is not approved by the "Arrival Time," one has the option to cancel the task or execute it immediately after approval. Even if "Execute Immediately After Approval" is selected, if the approval is not completed within 72 hours, the task will be automatically canceled. |
|Refresh Segment Before Execution |Mandatory.<br><br>**If you have purchased GMP + VeCDP or GMP + finder**<br><br>**If the selected segment is "updated on\-demand"** : If the "Refresh Segment Before Execution" is checked, the system will default to refreshing the segment's data 15 minutes in advance. If Task 15:00 is scheduled, the system will refresh the segment at 14:45 If you want to adjust the 15min interval, you can contact the project manager or customer success manager<br><br>**If the selected segment is 'updated daily'** : It will be refreshed at the time set during the segment's creation<br><br>Specifically: **Scheduled \- Repeated, rule creation segment, will default to creating a 'Refresh on demand' segment**.<br><br><span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/30c6b285d7b643b0bf211e53394784d1~tplv-goo7wpa0wc-image.image) </span><br><br>**If GMP + VeCDP or GMP + finder are not purchased**<br><br>Then the system does not support segment refresh |
|Segment refresh failed |Mandatory<br><br>**If GMP + VeCDP or GMP + finder were purchased:** <br><br>**If the selected segment is 'Refresh on demand'** : You may choose to send using the segment data currently obtained by the system after a refresh failure, or choose not to send<br><br>**If the selected segment is "updated daily"** : If the refresh fails, the system will default to the last obtained segment for sending.<br><br>**If GMP + VeCDP or GMP + finder is not purchased**<br><br>then this option is not available. |


**Event\-Triggered: Completion of Event A Meaning**


|Field |Meaning and purpose of the field |
|---|---|
|Trigger event |Mandatory.<br><br>**Represents the event a user completes to trigger this process**, and users who complete this event will be filtered by "target users". Only those who meet both "trigger conditions + target users" will actually receive the message.<br><br><span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/73d3dfa0982c4760b5d1c378c44f19a4~tplv-goo7wpa0wc-image.image) </span><br><br>**Accumulate Completion of A / After Each Completion of A**: Accumulate completion of A 3 times means a user, after completing the event, will only be contacted once; every completion of A 3 times means the process is triggered each time a user completes A three times.<br><br>**Immediate Reach / Delayed Reach / Delay for a Specified Time / Delay until a Specific Day to Reach**:<br><br>Immediate reach means to reach out immediately after the event is completed<br><br>Delayed reach represents a relative delay in time to reach, delaying 1 day means delaying 24 hours; it can be delayed up to 365 days<br><br>Delay until a specified time reach means you need to wait until the specified time after the event occurs to reach out<br><br>Delay to a specific weekday reach means waiting until the nearest specific weekday after the event occurs For example, if set to delay until Tuesday and the event occurs on Monday, it will be reached this Tuesday; if set to delay until Tuesday and the event occurs on Wednesday, it will be reached the following Tuesday |
|Event A Start and End Time |Mandatory This field will trigger the process for all Event A occurrences during this period |
|Message Delivery Task End Time |System default fill<br><br>After the end time is reached, the status of the message delivery task changes to 'completed', and even if Event A arrives late, the system will no longer continue the message delivery. |
|Refresh segment before execution |**If GMP + VeCDP or GMP + finder is purchased**<br><br>**If the selected segment is 'update on demand'** , the segment will not be refreshed.<br><br>**If the selected segment is 'update daily'** , the system will refresh according to the set time. If 'rule creation segment' is used, the segment is set to refresh daily at 06:00 by default.<br><br>Specifically, **for Event\-Triggered: Completion of Event A, accompanied by rule creation segment, a 'daily update' segment will be created by default.** <br><br><span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/5c5fb6e9cdc946d7b906513d926b5d84~tplv-goo7wpa0wc-image.image) </span><br><br>**If GMP + VeCDP or GMP + finder is not purchased**<br><br>Then the system does not support segment refresh. |
|Segment refresh failed |Required.<br><br>**If GMP + VeCDP or GMP + finder is purchased**: Data will still be judged using the most up\-to\-date information after a refresh failure.<br><br>**If GMP + VeCDP or GMP + finder is not purchased:**  This option is not available. |


**Event\-Triggered: Event A Completed & Event B Incomplete Meaning**


|Field |Field Meaning and Usage |
|---|---|
|Trigger Event |Required.<br><br>**Completing Event A signifies which event the user must complete to trigger this process**, and users who complete the event will be filtered based on "Target Audience" criteria. Only those who meet both "Trigger Condition + Target Audience" will actually proceed with the outreach.<br><br>**Uncompleted Event B**: Unlike "Event\-Triggered: Completion of Event A", this task type requires waiting for a period after Event A to ascertain whether Event B has been completed; if not, the process is triggered.<br><br><span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/a89bbe2ebd80420eadb1d43fe48c84a7~tplv-goo7wpa0wc-image.image) </span><br><br>**Cumulative Completion of A / Each Completion of A**: Cumulative Completion of A 3 times means the user will only be reached once after completing the event; Each Completion of A 3 times means that the user will trigger the execution of the process every time they complete A 3 times.<br><br>**Immediate Reach / Delayed Reach / Specified Time Delay/Delay to a Specific Day of the Week**:<br><br>Immediate reach means reaching out immediately after an event is completed.<br><br>Delayed reach refers to a relative time delay, where a delay of 1 day means a delay of 24 hours; the maximum delay can be up to 365 days.<br><br>Specified time delay reach means waiting until a specified time after an event occurs before reaching out.<br><br>Delay to a specific day of the week means waiting until the closest specified weekday after an event occurs to reach out. For example, if set to delay until Tuesday and the event occurs on Monday, it will reach out this Tuesday; if set to delay until Tuesday and the event happens on Wednesday, it will reach out next Tuesday. |
|Event A Start\-End Time |Mandatory. This field means that any occurrence of Event A within this time period will trigger the process. |
|Message Delivery Task End Time |The system fills in by default.<br><br>Once the end time is reached, the message delivery task status changes to completed. Even if Event A arrives late, the system will not continue the message delivery. |
|Refresh segment before execution. |**If GMP + VeCDP or GMP + finder were purchased,** <br><br>**If the selected segment is 'update on demand'** , the segment will not be refreshed.<br><br>**If the selected segment is 'refresh daily'** , the system will refresh according to the set time. If 'rule creation segment' is used, the segment will default to refreshing daily at 06:00.<br><br>Specifically, **for Event\-Triggered: Completion of Event A \- rule creation segment, a 'refresh daily' segment will be created by default.** <br><br><span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/250586798b5c436d9a1eaa51d5b0cea3~tplv-goo7wpa0wc-image.image) </span><br><br>**If GMP + VeCDP or GMP + finder were not purchased,** <br><br>then the system does not support refreshing segments. |
|Segment refresh failed |Mandatory.<br><br>**If GMP + VeCDP or GMP + finder is purchased**: After a refresh failure, the latest data will be used for evaluation.<br><br>**If GMP + VeCDP or GMP + finder is not purchased:**  This option will not be available. |


**Step4: Reach Configuration**

This step involves filling in the reach content and setting the frequency control/do not disturb/mutual exclusion conditions.

<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/7f89c8eda1164978a0abe3abe51426fd~tplv-goo7wpa0wc-image.image" width="439px" /></div>



|Field |Purpose and meaning of the field |
|---|---|
|Channels |The system will default to the channel selected in Step1, but it can be changed. After modification, the filled content will be cleared, but other data will be preserved. |
|Start split\-flow experiment |For detailed logic, please refer to the "A/B Experiment" section |
|Task Type |Mandatory, including regular campaigns, urgent campaigns, and notification campaigns.<br><br>**Task type affects task priority, and task priority affects the logic of which task is triggered first when multiple tasks are triggered simultaneously (when a message queue backlog occurs)** : Prioritize the task with the higher priority.<br><br>Priority: Notification messages \> Urgent campaigns \> Regular campaigns; each task trigger consumes one occurrence of the channel frequency control limit.<br><br>Specifically, notification message type tasks can still be triggered even after the channel frequency control limit has been exhausted. |
|Select Template |Mandatory, click to sync the WeChat Mini Program Subscription Message templates automatically. For new creation or modification, please operate on the WeChat public platform. The parameters in the template can be customized.<br><br><span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/e2ec0ded179247dfa85743ba484ffb3c~tplv-goo7wpa0wc-image.image) </span> |
|**Template Content** |If the template contains parameters, it is necessary to fill in the parameter content, supporting the insertion of user attributes, user ID, labels, and event attributes. Additionally, after inserting parameters, it is recommended to set default values to increase the success rate of message sending. When the system cannot retrieve parameter values, it will use default values instead. If no default values are set, the sending will be canceled.<br><br>When the variable value inserted exceeds the Template Content length limit on the WeChat side, you can choose to either "not send" or "send after truncation".<br><br><span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/8fd2dcfacdb046cf9eb6efc5b2a4f778~tplv-goo7wpa0wc-image.image) </span> |
|Opening Method |Mandatory, with three scenarios: H5 page, WeChat Mini Program, or none. This item determines how the redirection occurs after a user clicks on the "service number template message" card.<br><br>**If "H5" is chosen**: it means the user needs to be redirected to an H5 page after clicking the "service number template message" card. When configuring in GMP, it is necessary to enter the H5 link information.<br><br><span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/17f0c0d3636043019f61e441b10212c4~tplv-goo7wpa0wc-image.image) </span><br><br>**If "WeChat Mini Program" is chosen**: it signifies that after clicking the "service number template message" card, users need to be redirected to a Mini Program page. When configuring in GMP, it is necessary to choose which Mini Program to open and input the path to the Mini Program page. It's special: this applet needs prior authorization in the GMP Channel Management before it can be selected here.<br><br><span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/85bfc7fa30da46e085115cf1794c949a~tplv-goo7wpa0wc-image.image) </span><br><br>**If "No" is selected**: it means that the user does not need to make any redirection after clicking the "Service Number Template Message" card. |
|Test Send |Conduct an actual test of the push content; you need to fill in the target ID and variable values. |
|Global Reach Limits |That is, channel reach frequency control limits; the page will display the selected channel's frequency control, and if it does not meet requirements, you can click "View" \-\-\> go to "Management Center" to adjust the channel frequency control. Note, current adjustments to frequency control are not automatically reflected on the page; you must manually update the configuration page to sync with the latest frequency control situation.<br><br>If you turn off "Global Reach Limits," it means the message sent this time will not be subject to this channel's frequency control and cross\-channel frequency control restrictions. |
|Cross\-channel Frequency Control |The current version supports setting cross\-channel frequency control, such as Channel A + Channel B, with a maximum reach of once per day. The relevant configuration data will be displayed here. |
|Do Not Disturb Period |The SMS channel can ignore this field. |
|Do Not Disturb Settings |You can set a Do Not Disturb period. If the system plans to send a message during this period, it will be restricted. |
|Do Not Disturb Delivery Rules |If filtered due to hitting the Do Not Disturb condition, you can choose to either "abandon this delivery" or "continue delivery after the Do Not Disturb period ends." |
|Message Delivery Task Frequency Control |If the trigger conditions for the current task are 'Scheduled \- Repeated,' 'Event\-Triggered: Completion of Event A,' 'Event\-Triggered: Event A Completed & Event B Incomplete,' then a user may be reached multiple times. You can set how to control the frequency for this task.<br><br><span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/a626eb61f32d4def848b4289aaf85d84~tplv-goo7wpa0wc-image.image) </span> |
|Exclude Task |Optional<br><br>This task selection feature establishes an exclusive relationship with the current task, ensuring that a target user (with the same user ID) will only be reached by one of the tasks. That is, if Task A and Task B are mutually exclusive and a user is successfully reached by Task A, they will not be reached by Task B, and vice versa. Supports searching by task name or ID, currently displaying only the first 50 tasks; for more tasks, please use search. |


**Step5: Focus Metrics**

**This function can be used to count the subsequent conversion of reached users after being reached.**  "Set Focus Metrics" is off by default; switching it to on allows the setting of campaign’s focus metrics.

<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/ee03d9fa866c4b3eb2dc4c0e572c9cce~tplv-goo7wpa0wc-image.image" width="439px" /></div>



|Field |Field meaning and purpose |
|---|---|
|Setting mode |You can choose to "Create New Indicator" or use "Existing Indicators" |
|Indicator Name |Required.<br><br>Examples: Add to cart, generate orders, GMV. When creating a task, the entered indicator name will be reflected on the data analysis page.<br><br><span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/7962291369a045be9ab9a8ec28888c99~tplv-goo7wpa0wc-image.image) </span> |
|Manage Indicators |To the right of the indicator name is an "Manage Indicators" entry, which upon clicking, allows viewing of all indicators in the system, the configuration rules of the indicators, and also the deletion of indicators. Deleting an indicator does not affect the data already set in the task; it only impacts the inability to select when choosing existing indicators.<br><br><span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/570aa1c2d3bc489198f1f433c15e60bb~tplv-goo7wpa0wc-image.image) </span> |
|Calculation Conditions<br><br>Calculated through real\-time behavioral data |**Examples of Indicators**: Product detail page visits, cart additions, home page views on mini\-programs<br><br>**What conditions are required for use**: If a data source has "real\-time behavior messages," then it is possible to set the count/number of people statistics for real\-time behavior under this data source. If you are unsure whether the data source meets the conditions, you can consult a project manager or a client success manager.<br><br>**How to configure**: Select the data source and events, and if additional constraints are needed on the events, click "Filter Conditions" to add them. For example, to count the visits to a product detail page, you can use this function to limit the URL of the product detail page.<br><br><span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/d345a876fd7844fdb981f894b82a4bb8~tplv-goo7wpa0wc-image.image) </span><br><br>**What are the results of data analysis after configuration**:<br><br><br>* After configuration, the message delivery and Process Canvas tasks of this channel will automatically focus on this indicator.<br><br>* This indicator will track the user conversions within a specified window after being reached.<br><br>* After configuration, as soon as the conversion event occurs, the indicator will be updated in real\-time. |
|Calculation Conditions<br><br>Calculated through offline behavioral data |**Metric examples**: Visits to product detail pages, add\-to\-cart volume, homepage views on the mini\-program<br><br>**What conditions need to be met to use this**: If a behavioral data source is an "incremental table" updated daily, you can set metrics for the frequency/number of actions per person under this data source. If you are unsure whether the data source meets the requirements, you can consult the project manager or the client success manager.<br><br>**How to Configure**: Select the data source and events. To add restrictions to events, click "Filter Conditions" to make additions. For example, to count the visits to a product detail page, restrictions can be placed on the product detail page address using this functionality.<br><br><span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/a23e9142224a488688ebba312bf68a6b~tplv-goo7wpa0wc-image.image) </span><br><br>**What are the results of data analysis after configuration**:<br><br><br>* After configuration, the messages and tasks on the Process Canvas will automatically monitor this indicator.<br><br>* This indicator will track conversions occurring within a specified window after user contact.<br><br>* After configuration, as long as the conversion event occurs, the system will count the indicator data at 5, 11, 17, and 23 o'clock daily.<br><br><br>**Difference between this data source and 'Using Real\-time Behavioral Data' for statistics**: If there are 'real\-time behavior messages', prefer the 'Using Real\-time Behavioral Data' function; if not, use the 'Calculation Using Offline Behavioral Data' for statistics. |
|Calculation Conditions<br><br>Calculation through Detailed Data |**Indicator examples**: number of orders, GMV<br><br>**Conditions necessary for use**: If a detailed dataset is updated daily as an "incremental table", you can set up the data source for detailed behavioral data statistics. If unsure whether the data source meets the requirements, consult the project manager or customer success manager.<br><br>**How to configure**:<br><br>Select the data source and fields. If you need to add constraints on the event, click "Filter Conditions" to add them. For example, to count the number of orders, you can use this feature to limit product categories.<br><br>For counting the occurrences of fields, select "Number of people/counts".<br><br><span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/873dba679925448bb260c79d3f98d8bb~tplv-goo7wpa0wc-image.image) </span><br><br>For summing fields, simply choose "Sum". For instance, the GMV indicator requires summing the merchandise amounts.<br><br><span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/699a4fe16f004ce69b5729aca0dcde6a~tplv-goo7wpa0wc-image.image) </span><br><br>**What are the results of data analysis after configuration**:<br><br><br>* After configuration, message delivery and process canvas tasks on this channel will automatically monitor this indicator.<br><br>* This indicator will track the user's conversion within a specified window period after being reached.<br><br>* Once configured, whenever a conversion event occurs, the system will tally the indicator data at 5, 11, 17, and 23 o'clock every day. |
|Calculation Conditions<br><br>Composite Indicator |**Composite Indicator**<br><br>Indicator examples include: add\-to\-cart rate, customer spend per visit, and SMS sending cost.<br><br>After clicking, you can perform composite operations between indicators. You can select an indicator or enter a value.<br><br>Select an indicator: Only supports selecting delivery quantity, reception quantity **and the indicators already selected on the current page**.<br><br><span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/337edce4529d428ba49f5de5f5c2dfba~tplv-goo7wpa0wc-image.image) </span><br><br>Input numeric values: Click the selection box to directly input values for calculating indicators similar to "SMS sending cost".<br><br><span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/bd7ae10a32ea4dea9d475e2de57971f2~tplv-goo7wpa0wc-image.image) </span> |
|Window period |Refers to the period after reaching the user, during which data is collected. |
|Do not contact after completing the event |For timed repetitive and event\-triggered tasks, a user can be contacted multiple times. If you wish to stop contacting the user after they complete a certain action, you can select this option. This ability can only be set when "Real\-time Behavioral Data Source" is the selected event.<br><br><span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/247da6cec7264489aad171997ede7566~tplv-goo7wpa0wc-image.image) </span> |


You can add up to 7 focus metrics; after adding metrics, **full participation attribution statistics will be conducted, that is, as long as the user completes the behavior or generates order table data within the window period, it will be accounted for.**  For example: If a user is reached by both task A and task B, and both tasks set the "Mini Program Page View" as the focus metric, then the data will be counted in both tasks.

<span id="3b4fae4f"></span>
## **1.8 App Pop\-up**

<span id="f9c31289"></span>
### **1. Product Overview**

This feature enables millisecond response times, customizable templates, and provides visual editing capabilities.

<span id="2c9cc000"></span>
### **2. Usage Restrictions**


| |Detailed explanation |
|---|---|
|Complete pop\-up SDK integration |Clients need to complete SDK integration |
|Activate GMP Permissions |The administrator has enabled viewing permissions for the SMS channel, permission path: Management Center \- Channel Management \- APP Application Popup \- All Operations<br><br>The administrator has enabled the creation of Message Delivery Tasks through segmentation, permission path "Message Delivery \- Message Delivery Task \- Create/View/Edit/Delete" |
|Enable segmentation permission |Enable segmentation permission in 3 scenarios:<br><br>If VeCDP is purchased, permission needs to be enabled in VeCDP "Segmentation \- Private Domain Segmentation \- View/Add/Delete/Modify", after which the segmentation function in Task Creation can be used.<br><br>If VeCDP is not purchased and only Datafinder is purchased, permission needs to be enabled in Datafinder under "Segmentation", after which the segmentation function in Task Creation can be used.<br><br>If neither VeCDP nor Datafinder are purchased, this permission can be ignored. |


<span id="ec2505f2"></span>
### **3. Function Description**

**Step1: Create a new Message Delivery Task**

Add a new Message Delivery Task and select the app that needs the pop\-up.

Subject: The subject, also known as the entity/object, often refers to people, vehicles, or venues that can be targeted for operational growth or insight analysis. If there are multiple subjects of analysis or outreach, it is referred to as multi\-subject. **If you purchase VeCDP and also buy the "multi\-subject module," you can support reaching any subject in GMP**, such as targeting users or merchants would require enabling multi\-subject. If the module was not purchased, the concept and function description can be ignored.

<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/88d38a11bdca458088929430ac7c2d03~tplv-goo7wpa0wc-image.image" width="439px" /></div>


**Step 2: Fill in basic task information**

<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/813f797dccfe4e11a044b449c17e455a~tplv-goo7wpa0wc-image.image" width="439px" /></div>



|Field |Field Meaning and Usage |
|---|---|
|Task Name |Required, used to differentiate between tasks (strategies) and must not duplicate other task names |
|Task Grouping |Optional, allows different tasks to be grouped together for subsequent analysis based on task grouping. Grouping for Message Delivery and Process Canvas is isolated; data are not shared.<br><br>If existing grouping options do not meet the requirements, new groups can be created or edited via "Manage Groups". Only project administrators and group administrators can operate on adding new groups. If there are existing message delivery tasks in a group, the group cannot be "deleted". The group can only be deleted when there are zero message delivery tasks. |
|Associated Campaign |Optional, tasks can be attributed to different campaigns such as "Singles' Day Campaign" for subsequent analysis based on the associated campaign. Tasks related to Message Delivery, Process Canvas, or Placements can be linked to the same campaign. |
|Related application for this task |The behavior data generated by this task will be fed back to Datafinder under this application. If Datafinder is not purchased, this capability can be disregarded. |


**Step 3: Fill in target users**

Target users represent the range of users that this task needs to reach. Target users support four methods: rule creation segment, existing segments, uploaded segments, and all users. If different combinations are purchased, the capabilities of target users will also vary. If GMP is purchased along with VeCDP, new segments can be created in "rule creation segment". If GMP is purchased with Datafinder (without purchasing CDP), new segments can be created in existing segments; **if none are purchased, creating segments on the GMP side will not be supported.** 

<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/ec880b8423ca4c229da9651c77ce9079~tplv-goo7wpa0wc-image.image" width="439px" /></div>


 **(1) Rule creation segment**

**After purchasing VeCDP, segments can be created using "rule creation segment"** , which can be selected using labels, attributes, segment packages, detailed data, and behavioral data.


|Field |Meaning and purpose of the field |
|---|---|
|Segmentation conditions |**After purchasing VeCDP, segmentation can be created using 'rule creation segments' which combine labels, attributes, segment packs, detailed data, and behavioral data, and support filtering users by audience ID types.**  Detailed operation instructions for the segmentation can be found in the VeCDP operation manual (chapter: creating private domain segments). The functional permissions for this segmentation capability are consistent with the segmentation editing permissions on VeCDP side, hence using this segmentation capability requires activating the VeCDP 'Add/Delete/Edit Segment' permissions, otherwise no new segments can be created.<br><br><span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/80cf8ae9d91045d2b8fb543b60582b9d~tplv-goo7wpa0wc-image.image) </span> |
|Sync to the CDP Segments List |Turning on this switch will make the segments created here visible in the VeCDP segments list, with the default segment name being the Message Delivery Task Name + Message Delivery Task ID. Turning off this switch will make the segments created invisible in the VeCDP segments list, and they cannot be used again for segment selection. Administrators can set the default checked status.<br><br><span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/c253a84ecec449178479d5b81a16ca57~tplv-goo7wpa0wc-image.image) </span> |
|Audience Estimation |After configuring the segmentation conditions, click "Audience Estimation" to calculate the number of IDs in the segment in advance. The ID count includes two types: OneID count and the number of IDs sent by the current channel, allowing you to decide whether to adjust the segmentation settings based on the estimation results. |
|Segment Authorization |Optional, authorize the segments created by label and behavior rule creation to specific roles that can view the segment. If no authorization is granted, a lack of segmentation permission will be indicated when viewing, editing, or copying tasks. |
|Supplementary Sending |Optional, you can enter the ID information of the testers, and upon filling, it will automatically default to these users as the audience during task execution. Multiple IDs can be entered. |


When saving a draft or submitting for approval, the system will automatically create the segment, and the ID type of the segment will be the target ID type of that channel, such as a segment package consisting of appid+openid for the Public Account Active Message channel.

 **(2) Existing Segment**

Using this feature, you can directly select an already defined segment for contacting purposes.

**Permissions required to use this feature:** 

If you purchase GMP and VeCDP simultaneously, this feature will pull segments from VeCDP. To use this feature, you must enable the VeCDP "View Segment" permission.

If you purchase GMP and Datafinder (without purchasing VeCDP), this feature will pull segments from Datafinder. Using this feature requires enabling the Datafinder "Segment" permission.

<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/1e8ca2dca29945358931f5fa663d92cb~tplv-goo7wpa0wc-image.image" width="439px" /></div>



|Field |Field Meaning and Application |
|---|---|
|Segment List |Mandatory, must select the segment for this outreach. If the multi\-subject capability of VeCDP is purchased, this list will automatically fetch the segment list of the subject for this task. |
|Audience Estimation |After selecting a segment, the system will automatically calculate the number of send IDs for the current channel. |
|Create New Segment |If you have purchased GMP along with VeCDP, clicking this feature will redirect to the VeCDP segment list where you can create a new segment. If you have purchased GMP along with Datafinder (without purchasing VeCDP), clicking this feature will support the creation of new segments. If neither VeCDP nor Datafinder are purchased, this capability is not available.<br><br><span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/a297ec2643d14239ad1b64d80a121deb~tplv-goo7wpa0wc-image.image) </span> |
|Resend Supplement |Optional; you can enter the tester's ID information. Once entered, the stated user will be the default recipient during task execution. You can enter multiple IDs. |


 **(3) All Users**

Represents all users under the current project, **All users only support two types of message delivery tasks: Event\-Triggered: Completion of Event A, and Event\-Triggered: Event A Completed & Event B Incomplete**, meaning that after a user triggers an event, no further audience filtering is performed, and all users meeting the event conditions will be contacted.

<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/e6997da056e8488c8faeb3681ab72fa9~tplv-goo7wpa0wc-image.image" width="439px" /></div>


**Step 3: Configure Trigger Conditions**

The App Pop\-up only supports one method: "Event\-Triggered: Completion of Event A".

**Message Delivery Task Type**: Represents the timing of the trigger for this message delivery.

**Event\-Triggered: Completion of Event A**: Triggers when the user completes certain actions (either immediately or delayed), such as collecting, liking, or sharing a post. Within the valid task period, meeting the trigger condition can enable multiple triggers.

<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/1303e9f305ef4c2bb9fe51054d03ed03~tplv-goo7wpa0wc-image.image" width="439px" /></div>


 **(1) Field meaning for Event\-Triggered: Completion of Event A**


|Field |Meaning and Purpose of the Field |
|---|---|
|Trigger Event |Required.<br><br>**This process is triggered after the user completes a specific event**, and the users who complete this event will be filtered based on the 'target audience'. Only users meeting both 'trigger condition + target audience' will actually be reached.<br><br><span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/56b10275234e47b2a4af92b11c5ae98c~tplv-goo7wpa0wc-image.image) </span><br><br>**Cumulative completion of A / Each completion of A**: Cumulative completion of A 3 times means that the user will be reached only once after completing the event; Each completion of A 3 times means that the process will be triggered every time the user completes A 3 times.<br><br>Note: Do not select predefined properties of finder, and it is also recommended not to select pre\-set events of finder (such as launching an app, etc.)<br><br>The app pop\-up only supports **instant reach** |
|Event A duration |Mandatory. This field triggers the process for any Event A that occurs during this time period. |
|Message delivery task end time |The system fills this in by default.<br><br>After reaching the end time, the status of the message delivery task becomes 'ended', and the system will not continue to reach out, even if Event A is delayed. |
|Refresh segment before execution |**If GMP + VeCDP or GMP + finder was purchased**<br><br>**If the selected segment is 'updated on demand'** : the segment will not be refreshed.<br><br>**If the selected segment is "Refresh Daily"** : the system will refresh at the configured time. If "Label and Behavior Selection" is used, the segment will automatically refresh at 06:00 every day.<br><br>Specifically, **for trigger\-type \- complete A, with label and behavior selection, a "Refresh Daily" segment will be created by default.** <br><br><span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/4fe6a0d6ce484f77804b0f439c02d386~tplv-goo7wpa0wc-image.image) </span><br><br>**If GMP + VeCDP or GMP + Finder is not purchased**<br><br>then the system does not support segment refresh. |
|Segment refresh failed |Mandatory.<br><br>**If GMP + VeCDP or GMP + Finder is purchased**: the system will use the latest data to make a decision even if the refresh fails.<br><br>**If GMP + VeCDP or GMP + Finder is not purchased:**  this option is not available. |


**Step4: Configuration of Marketing Strategy**

This step involves filling in the content of the marketing strategy, setting frequency control, do\-not\-disturb conditions, and exclusion conditions.

<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/0b8ec13455284dd5b6ac68bac9d297a1~tplv-goo7wpa0wc-image.image" width="439px" /></div>



|Field |Field Meaning and Purpose |
|---|---|
|Channels |The system will, by default, preset the channel selected in Step1. Modifications can be made, and any entered content will be cleared, but other data will be retained. |
|Task Type |Mandatory, includes general campaigns, emergency campaigns, and notification campaigns.<br><br>**The task type impacts the task priority, which in turn influences which task triggers first when multiple tasks are activated simultaneously (when there's a backlog in the message delivery queue)** : the task with the higher priority triggers first.<br><br>Priority: Notification messages \> Emergency campaigns \> General campaigns. Each task activation consumes one frequency control count on the respective channel.<br><br>Specifically for notification message types of tasks, they can still be triggered even after the frequency control count on the channel is exhausted. |
|Pop\-up Priority |Mandatory, includes general campaigns, emergency campaigns, and notification campaigns.<br><br>**Task types affect task priority, and task priority affects which of multiple concurrently triggered tasks (when a backlog occurs in the messaging queue) gets executed first**: tasks with higher priority are triggered first.<br><br>Priority: notification messages \> urgent campaigns \> regular campaigns, where each task triggers once, consuming one frequency control count per channel.<br><br>For the special notification message type tasks, they can still be triggered even after the frequency control counts are depleted. |
|Initiate a Split Testing Experiment |For detailed logic, please refer to the "A/B Experiment" section. |
|Pop\-up Content Settings |Mandatory. Pop\-up content settings require selecting a template before detailed configuration. Pop\-up templates include standard templates (system\-built) and custom templates (created via visual drag\-and\-drop). **Pop\-up content settings include:**  overlay settings, component settings, and pop\-up settings.<br><br>**Overlay settings**: Support customizing background color, background image, overlay click actions, and close button position.<br><br><span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/f9fccdb5314f4421871eb2a09c327743~tplv-goo7wpa0wc-image.image) </span><br><br>**Popup settings**: Support customizing background color, background image, and border radius.<br><br>**Component settings**: Custom settings for image components, document components, and button components vary.<br><br><br>* **Image component**: Supports custom settings for uploading images and actions on click. The width and height cannot be customized, as they are determined by channel settings.<br><br>* **Text component**: Supports custom settings for font size, color, line spacing, indentation, text alignment, and text (can wrap). The maximum length cannot be customized, as determined by channel settings.<br><br>* **Button component**: Supports customizing border radius size, button color, button text size and color, button copy content, and click actions. Button type, button width and height, and horizontal alignment cannot be customized, as they are determined by channel settings.<br><br><br><span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/e5c41e616c2f439891c06e807d2f91cb~tplv-goo7wpa0wc-image.image) </span> |
|Test pop\-up |Actual testing of the pop\-up on the app is required, and it involves scanning a QR code with an app that has the pop\-up SDK integrated.<br><br><span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/3fa3ff3ff6f84ccebfbe473f8a987e18~tplv-goo7wpa0wc-image.image) </span> |
|Global Reach Restriction |The page displays the frequency control settings for the selected channel. If these do not meet the needs, you can adjust the channel's frequency control by clicking "View" \-\-\> "Settings Center". Note, the page will not automatically sync after adjusting frequency controls; manual updates to the configuration page are necessary to sync to the latest frequency settings.<br><br>If "Global Reach Restriction" is turned off, it means that the messages sent will not be subject to frequency controls specific to this channel or cross\-channel frequency controls. |
|Do Not Disturb Period for Channels |The SMS Channel can ignore this field. |
|Do Not Disturb Settings |You can set a Do Not Disturb period. If the system plans to send messages during this time, they will be restricted by the Do Not Disturb settings. |
|Message Delivery Task Frequency Control |If the trigger condition for the current task is "Scheduled \- Repeated," "Event\-Triggered: Completion of Event A," or "Event\-Triggered: Event A Completed & Event B Incomplete," multiple contacts with the user are possible. This field allows setting how to manage frequency control within this task.<br><br><span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/628a80c714644f568044d4e3300c6910~tplv-goo7wpa0wc-image.image) </span> |


**Step5: Focus Metrics**

**This function can be used to track, after being reached, the subsequent conversion rates of the users reached**. The "Set Focus Metrics" is off by default; it can be turned on to set the focus metrics for the task.

<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/acfd0959dea04051bff283b112db7d54~tplv-goo7wpa0wc-image.image" width="439px" /></div>



|Field |Field meaning and purpose |
|---|---|
|Setting method |You can choose to "Create New Indicator" or directly use "Existing Indicator" |
|Target Name |Mandatory.<br><br>Examples: Add to Cart, Create Order, GMV. |
|Calculation Conditions<br><br>Calculated using real\-time behavioral data |**Example Indicators**: Product detail page visits, add\-to\-cart counts, mini program home page views<br><br>**Criteria for Usability**: If a behavioral data source has "real\-time behavior messages," real\-time behavior count/number of people metrics can be set under this data source. If you're unsure whether the data source meets the criteria, you can consult either the project manager or the customer success manager.<br><br>**How to Configure**: Select the data source and events. If limiting conditions need to be added to the event, click "Filter Conditions" to add them. For instance, to count product detail page visits, you can use this feature to limit the product detail page URLs.<br><br><span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/68662f0061ac413e848f9f4157faf666~tplv-goo7wpa0wc-image.image) </span><br><br>**Results of Data Analysis After Configuration**:<br><br><br>* After configuration, the channel's message delivery and process canvas tasks will automatically monitor this indicator.<br><br>* This indicator will track the user conversion during the designated window period after reaching them.<br><br>* Once the conversion event occurs, this indicator will be updated in real time. |
|Calculation Conditions<br><br>Calculate using offline behavior data |**Example metrics**: product detail page visits, add\-to\-cart quantity, mini\-program home page views<br><br>**Conditions for use**: If a behavioral data source is updated daily as an "incremental table", it can set metrics for counting the number of occurrences/people under that data source. If you're unsure whether the data source meets the requirements, you can consult the project manager or customer success manager.<br><br>**How to configure**: Select the data source and events, and if there is a need to add restrictions to the events, you can click "Filter Conditions" to add them. For instance, to count visits to a product detail page, you can use this feature to restrict it to specific page addresses.<br><br><span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/d441b344bf9c4e7b85256aff3005457c~tplv-goo7wpa0wc-image.image) </span><br><br>**What the results look like after configuration**:<br><br><br>* After configuration, the channel's message delivery and process canvas tasks will automatically monitor this metric.<br><br>* This metric will count the user's conversions within a specified window of time after being reached.<br><br>* After configuration, as long as the conversion event occurs, the system will compile data on the metric daily at 5 AM, 11 AM, 5 PM, and 11 PM.<br><br><br>**The difference between this data source and "Real\-time Behavior Data Source"** : If there are "real\-time behavior messages", prioritize using the "Real\-time Behavior Data Source" feature; if not, use "Calculate Stats with Offline Behavior Data". |
|Calculation Conditions<br><br>Calculation through Detailed Data |**Indicator Examples**: Number of Orders, GMV<br><br>**Conditions Required for Use**: If a detailed data is updated daily as an "incremental table," you can set the indicators for detailed behavior data under this data source. If you’re unsure whether this data source meets the requirements, consult the project manager or customer success manager.<br><br>**How to Configure**:<br><br>Select data sources and fields, and if needed, you can add restrictions to the event by clicking "Filter Conditions". For example, to calculate the volume of orders, you can restrict the product category using this feature.<br><br>To tally the frequency of fields, select "Counts/Instances".<br><br><span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/f84232594a934088b2f5264dc5ed81de~tplv-goo7wpa0wc-image.image) </span><br><br>To sum a field, simply select "Sum". For instance, the GMV metric requires summing up the amounts of the products.<br><br><span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/9113d1f2943440aead415f62a0b44202~tplv-goo7wpa0wc-image.image) </span><br><br>**What are the results of the data analysis after configuration?** :<br><br><br>* After configuration, the channel's message delivery and process canvas tasks will automatically focus on this metric.<br><br>* This metric will track the user's conversion during a specified window period after being reached.<br><br>* After configuration, as long as a conversion event occurs, the system will summarize the metric data at 5, 11, 17, and 23 o'clock daily. |
|Calculation Conditions<br><br>Composite Metrics |**Composite Metrics**<br><br>Metric examples: Add\-to\-cart rate, per customer transaction value, SMS sending cost<br><br>Clicking it allows you to perform combination calculations between indicators. You can select indicators or enter values.<br><br>Select indicators: only supports selecting "delivery volume", "Message Delivery"**and indicators already selected on the current page**.<br><br><span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/db42e83e13934b8486ecb705e597c817~tplv-goo7wpa0wc-image.image) </span><br><br>Enter values: Clicking on the selection box also allows direct entry of values for calculating metrics similar to "SMS sending cost".<br><br><span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/98fa2d390d2b4858b4c52af7bcb31c56~tplv-goo7wpa0wc-image.image) </span> |
|The window period |Refers to the period of time after a user is reached for which data within the window period is counted. |


&nbsp;
