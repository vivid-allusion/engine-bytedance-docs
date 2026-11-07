---
title: "Request Management"
product: "BytePlus DataFinder"
product_code: "DataFinder"
source: "https://docs.byteplus.com/en/docs/DataFinder/Request_Management"
---

DataFinder provides you with event tracking request management function. You can create and manage event tracking requests on the request management page, and clarify the version of this event tracking request, associated applications, event tracking scheme and other information in the requests. In the future, you can directly enter event tracking directly into DataFinder through publishing requests to improve the management efficiency of event tracking; you can also select the corresponding requests in the "event tracking real\-time verification" module. The system will automatically verify the consistency of the data with the event tracking scheme, so as to find out whether there is an event tracking error or leakage.

<span id="512b16e9"></span>
# Precautions


* The current request management function is a value\-added function, and you need to pay an amount to open it. If you want to use this function, you can contact BytePlus technical support staff or your account manager/customer success manager for consultation. You can use it after purchasing and opening this function.

* At present, this feature is only supported by SaaS\-cloud\-native.


<span id="35844196"></span>
# Create and edit requests

<span id="586ab40a"></span>
## Requests creation and event tracking


1. After logging in and entering the DataFinder console, click **New event tracking request** in the upper right corner of the data management \> metadata management \> request management page.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/7adb1abfd0964044acb41ea9f84764f8~tplv-goo7wpa0wc-image.image) </span>

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/0a44a17bb97e4c86b5f9abb32343fa58~tplv-goo7wpa0wc-image.image) </span>

2. Configure the event tracking requests parameter in the pop\-up sidebar.

   1. Basic information for configuring event tracking requests.

      <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/03310e54b10a406bb4289b22853e93ee~tplv-goo7wpa0wc-image.image) </span>

      
      |**Parameter** |**Configuration instructions** |
      |---|---|
      |Requests Name & Requests Remarks |Customize request names and request notes for easy subsequent identification of requests. |
      |associated app |Select the app associated with the current event tracking request in the drop\-down box. When the subsequent event tracking is entered into the DataFinder by publishing requests, the entered event tracking will be automatically bound to the current application. |
      |reporting platform |Select the event tracking in the current event tracking request in the drop\-down box, and the platform type will be reported later. |
      |version number |Set the version number based on your event tracking requests. |
      |Person in charge & related persons |Select the person in charge and associated with the event tracking request in the drop\-down box. |
      |launch method |Select the event tracking demand online method. If you need to review the online, you also need to configure the demand reviewer in the drop\-down box. Attention: Reviewers need to have approval authority. |
      

   2. Configure event tracking scheme design. Support manual entry of event tracking and properties in the page, and also support bulk import of event tracking by uploading Excel files.

      <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/30545cd35dd94047ae19fd416784e6fc~tplv-goo7wpa0wc-image.image) </span>

      
      |**Manual entry** |**Bulk import** |
      |---|---|
      |Click the **Add event tracking** button to manually add a custom event to the interface and select the event property associated with the event.<br><br><br>* Support directly uploading event tracking screenshots to assist in explaining the event tracking events in the event tracking scheme. After the request is approved, the added event tracking screenshot can take effect in the event tracking scheme.<br><br>* An event can add event properties associated with multiple events; when adding event properties, it is supported to set whether the properties must be passed and whether dictionary enumeration values need to be set for the properties.<br><br>* You can add multiple events by clicking the **Add event tracking** button multiple times. |Click the **Bulk Import** button, download the batch import template in the interface, fill in the event, event attributes and other information into the form according to the input prompts in the template, and click the Upload button after completion to enter the batch into the requests.<br><br><span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/364fe71884554f99b190626bfe42e78c~tplv-goo7wpa0wc-image.image) </span> |
      

3. Next steps: After the requests and event tracking are created, it is recommended to verify the data, and then submit the online requests after there is no problem.


<span id="ea6485e1"></span>
## **Editing requests and event tracking**

Find the corresponding request in the request management list page and click the "Edit" button to modify the created request.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/ba3c2764c5cc44c8a8bd727e19781acc~tplv-goo7wpa0wc-image.image) </span>

<span id="55149370"></span>
# **Submit an on\-line & withdraw & off\-line request**

After the request is created, it needs to be submitted online before it will be synchronized to the event tracking search list, which can be queried and used.


1. On the request list page, click **Confirm** after matching the request to launch the request.

   When submitting a request, the system will verify your current request configuration results. If no event information is registered, submitting a request is not supported.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/ced1319f6cc844fe9252baa9ce75817f~tplv-goo7wpa0wc-image.image) </span>

2. Approval Requests Pushonline. If you choose "Review Online" for the online method of your previous requests, the approver needs to complete the online approval of the requests, and the requests will not be truly submitted online until the approval is completed; the review requests support the withdrawal of the online.

3. You can click the "Download" button to download the created requests locally.


<span id="076f3dc6"></span>
# Delete requests

At present, only the request creator and the project administrator can delete the request.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/1c8d02a7a3b949c59656f1ec9c913ec4~tplv-goo7wpa0wc-image.image) </span>

<span id="847e4dc8"></span>
# Next steps

After creating the event tracking request and submitting it online, you can perform event tracking verification based on the request. Please see for details [Event Tracking Real-Time Verification](https://docs.byteplus.com/docs/DataFinder/Event_Tracking_Real-Time_Verification).
