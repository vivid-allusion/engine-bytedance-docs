---
title: "SMS Template"
product: "Byteplus GMP"
product_code: "datagmp"
source: "https://docs.byteplus.com/en/docs/datagmp/SMS_Template"
---

<span id="常规短信模板"></span>
### **1. Product Overview**

Entrance for creating SMS templates: Marketing Strategy \- Content Management \- SMS Template, the prerequisite for using this feature is to have the following permissions activated.

<span id="61b62ca8"></span>
### **2. Usage Restrictions**


| **[ 📢 Prerequisite for using this feature ]**  ||
|---|---|
|**Prepare SMS account** |Provide an account on any platform such as "Byteplus messaging, Yunpian SMS, Aliyun SMS, Tencent Cloud SMS, Jiguang SMS, Dreamnet SMS" |
|**Configure the SMS Channel in GMP** |In the GMP "Management Center \- Channel Management \- SMS" interface, complete the channel settings. Additionally, fill in the receipt address on the corresponding SMS platform to receive the delivery receipt messages. This step is completed by technical personnel. Refer to the "Technical Integration Document" for the necessary configurations. |
|**Activate GMP permissions** |Administrator activates SMS template permissions; access path: Content Management \- SMS Template |


<span id="0dd74d03"></span>
### **3. Function Description**

 **(1) If the SMS channel is "BytePlus Messaging" channel**

**Add New Template**

<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/7469051fe58e4918b66ae11eae64a4b9~tplv-goo7wpa0wc-image.image" width="439px" /></div>



|Fields |Field meanings and purposes |
|---|---|
|**Template Name** |Character limit is within 50 characters. This field is for internal use to differentiate templates. |
|**Template Type** |Supports notification SMS, marketing SMS, and verification code |
|Template Purpose |Describe the purpose of the template for reference during review, with a character limit of 300. |
|Template Content |Within 1000 characters, supports placeholders ${xxxx}, where xxxx is the content to be replaced. SMS of verification code type supports only one verification code placeholder ${}. Note: SMS content must end with "To opt out, reply with R". |
|SMS Count |70 characters per entry, placeholders excluded. The character count includes "Signature + Template content + Variable content". SMS of up to 70 characters are charged as one SMS; exceeding 70 characters are considered long SMS, charged for every 67 characters. |
|Template Preview |The right side displays the SMS template preview, with the default signature included. |


**The review process after adding a new template**: The SMS template must undergo two approvals

<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/f94d9a01ceef4df8838bd464c71f327f~tplv-goo7wpa0wc-image.image" width="688px" /></div>


**Meaning of fields in the template list:** 

<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/b0d5e1a2fdb1421f8d789e15ed6ef229~tplv-goo7wpa0wc-image.image" width="696px" /></div>



|Field |Field Meaning and Purpose |
|---|---|
|Template Status |**Under review by business administrator**<br><br>**Under review by SMS service provider**<br><br>**Effective**: After passing all review processes, the review status will change to effective. When creating an SMS task, only signatures marked as 'effective' can be used.<br><br>**Rejected**: Hover to view the rejection steps and reasons. You can perform the "Edit" operation, and after editing, resubmit for approval.<br><br>**Disabled**: For templates that are in the active state, performing the "disable" action changes their status to disabled.<br><br>**Approval Withdrawn**: Only SMS signatures under review support this operation. After withdrawal, if resubmission is desired, a new signature must be created for approval. |
|Operation |**Rejected**: Hover to view the rejection steps and reasons. You can perform the "Edit" operation, and after editing, resubmit for approval.<br><br><span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/cd02f237cd5144bdb1bfee4340e07f34~tplv-goo7wpa0wc-image.image) </span><br><br>**Disable**: For templates that are in the active state, performing the "disable" action changes their status to disabled.<br><br>**Delete**: There will be a confirmation popup, and when deleting a template, it checks if the template is being used. If so, deleting it will terminate ongoing tasks, meaning any outreach tasks or process canvases using this SMS template will not execute properly.<br><br><span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/5b75322578ac4b1cbbb1d7852870102b~tplv-goo7wpa0wc-image.image) </span><br><br>**Enable**: No confirmation is needed, clicking "enable" makes it effective immediately; only templates in the "disabled" status support this operation. Only SMS templates that are enabled can be selected normally in message delivery tasks or the process canvas. |


&nbsp;
