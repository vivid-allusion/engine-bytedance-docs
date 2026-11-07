---
title: "User Sending Details"
product: "Byteplus GMP"
product_code: "datagmp"
source: "https://docs.byteplus.com/en/docs/datagmp/User_Sending_Details"
---

<span id="4e776e8c"></span>
### **1. Product Overview**

User Sending Details allow viewing past message deliveries, process canvas, and detailed send records for each individual user, including send time, content, send status, arrival status, and more. Meanwhile, the system can support resending.

<span id="388ff22c"></span>
### **2. Usage Restrictions**


| **[ 📢 Prerequisite for using this feature ]**  ||
|---|---|
|**Activate GMP** |Administrator activates permissions: Data Analysis \- User Sending Details \- View/Advanced Operations |


<span id="89c6eb45"></span>
### **3. Feature Description**

 **(1) View User Sending Details**

In the filtering area, you can filter based on user ID, message delivery task type, task name, task ID, policy name, policy ID, message delivery channels, send status, arrival status, start time, and end time. In the list area, you can view the results of sending details.

<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/289baa4108d24699bd742f94cf44c560~tplv-goo7wpa0wc-image.image" width="864px" /></div>



| |Field Meaning and Usage |
|---|---|
|baseid |User baseid in sending details, if VeCDP is purchased, clicking it will lead to the VeCDP Individual Portrait page. |
|Sending ID |The sending ID at the time of sending; if it's an SMS, it displays the phone number; if it's a WeChat reach, it displays the appid+openid. |
|Message Delivery Task Type |Refers to the type of the task, including Message Delivery, Process Canvas, and Intelligent Reach. |
|Channels |Refers to the channels associated with the task. |
|Message Delivery Task |This refers to the name of the task. Clicking it will lead to the task detail page. |
|Subtask/Strategy Engine |If it is a recurring scheduled task, the system will display the subtask ID. If it’s a Process Canvas, the Strategy Engine ID will be displayed. |
|Send content |This refers to the content used when actually reaching each user. |
|Send status |Includes three statuses: send successful, send failed, and not sent. |
|Send time |The time this system sent the message. |
|Send Failure Reason |If the sending fails, the Send Failure Reason will be displayed. Filter by failure reason in the table header.<br><br><span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/d4fd397eedb046d595ce3a2ee4363dce~tplv-goo7wpa0wc-image.image) </span> |
|Arrival Status |Includes three statuses: Arrival Success, Arrival Failure, and No Receipt from Channel. |
|Arrival Time |The time this system delivered the message. |
|Failure Reason for Arrival |If the arrival fails, the Failure Reason for Arrival will be displayed. Filtering by failure reasons can be done in the table title row.<br><br><span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/7ba2d7dde0964973a0cb566daac4ce77~tplv-goo7wpa0wc-image.image) </span> |
|Uplink Message Time |If this channel interfaces with uplink messages (reply messages), the reply time will be displayed. For example, if an SMS was sent to a user via a Webhook and the user replied, after the system integration, this section will display the user's reply time. |
|Upstream Message Content |If this channel interfaces with uplink messages (reply messages), the reply content will be displayed. For example, if an SMS was sent to a user via Webhook and the user replied, after system integration, this section will display the user's reply content. |
|Resend Record |If the message has been resent, the system will display the resend record. |


 **(2) Resend**

If sending fails, you can resend through the GMP system. You need to first filter the data that needs to be resent, operate the resend after filtering, and then you can view the progress of the send.

 **(2.1) Filter the data that needs to be resent**

There are two ways to filter: one is to resend for 'selected items', suitable for individual resends, such as when 5 users report not receiving a message, you can manually select them for resending. Another is to 'resend all based on the current filter conditions', suitable for bulk resending, such as if 5000 users experience sending failure, you can filter by this reason for bulk resending.

<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/2295a0db54a240c98bb76c6a0ceae40e~tplv-goo7wpa0wc-image.image" width="439px" /></div>


 **(2.2) Proceed with resending**

After clicking 'Resend', the system will pop up a confirmation. If you select 'Confirm Resend', the system will immediately start resending. The content sent is configured in the task, and if labels, properties, or other variables are inserted into the task, the latest data will be fetched for sending. In some cases, resending is not possible:

When the contact channel is a 'pop\-up' type

Message Delivery \- Triggered Task. The filter reason is "Entry conditions not met, completed B".

Process Canvas strategist, the filter reason is "Segment mismatch".

AB Split Testing, set as "Experimental group not reached".

<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/d781c462fe7040a5a3b4b90e3e3bbda4~tplv-goo7wpa0wc-image.image" width="860px" /></div>


 **(2.3) View Resend Record**

<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/643c7fcd67f7458ab1d6778a02f9f400~tplv-goo7wpa0wc-image.image" width="864px" /></div>


Click the resend record to view the progress of each resend, as shown in the image on the right. Under normal circumstances, the resend will be completed within an hour. If no progress is made, you can contact Volcano staff to confirm the issue.

Data after resending will also be reflected inunder "Manual Resend Data". As shown in the image below.

<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/8963fd36210842309445340235020a8b~tplv-goo7wpa0wc-image.image" width="542px" /></div>


<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/0801479bc24840d78fdff99dd5d83446~tplv-goo7wpa0wc-image.image" width="548px" /></div>


&nbsp;
