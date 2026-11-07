---
title: "User Testing Whitelist"
product: "BytePlus DataTester"
product_code: "DataTester"
source: "https://docs.byteplus.com/en/docs/DataTester/User-Testing-Whitelist"
---

Before the experiment is officially launched, it is usually necessary to select a few users to enter the testing phase to observe whether the experiment can normally obtain the data to be collected, or whether there are bugs on the client side. Users who participate in this step are called "whitelisted users". This article introduces the application scenarios and added operation steps for testing whitelisted users.

<span id="1d080e5f"></span>
# Background information

Before the experiment is launched, it is necessary to ensure that the integration process of the SDK is correct, and only after the experiment is launched can the scientific and effective results be guaranteed. The whitelisted users added are mainly used to debug experiments/features and check whether the whitelisted users can hit the experiments/features.

You can manually enter the UUID/SSID of the whitelisted user during the experiment/feature creation process, or you can add the commonly used test user to the test user whitelist first, and then directly select it when creating the experiment/feature.


* Whitelist and SSID/UUID are one\-to\-one correspondence, you can alias each difficult to remember SSID/UUID, play several categorization labels, easy to understand/remember.

* In the process of creating experiments/features, you can directly add commonly used whitelists to avoid errors caused by manually filling in long strings of SSIDs/UUIDs multiple times, and also reduce administrative costs.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip"><strong>UUID and SSID:</strong> Both are unique identifiers of the user, the main difference is that UUID is assigned and managed by you and the team for the user, and SSID is assigned and managed by BytePlus A/B test.</div>



* <div data-tips="true" data-tips-type="tip"><strong>UUID:</strong> User Unique Id, generally corresponding to the user's login id (such as mobile phone number, email). UUID is maintained by the customer;</div>


* <div data-tips="true" data-tips-type="tip"><strong>SSID:</strong> that is, Standardized Service ID (Standardized Service Id), is the user ID provided by BytePlus Growth Marketing Suite series products to mark and identify users. SSIDs are generated and maintained by BytePlus Growth Marketing Suite, which can be used by customers as needed.</div>



<span id="f1ddd3cf"></span>
# Go to the whitelist page

You can log in to the Tester console and go to the whitelist page in **Global Settings** \> **Audience Management** \> **User Test Whitelist** in the left navigation bar. The whitelist list shows you the basic situation of the whitelist, as shown below:

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/8a743526bd4f42eeb47556ac1472ec48~tplv-goo7wpa0wc-image.image) </span>

The actionable content is as follows:


* **Search:**  You can enter "whitelist name, creator, SSID/UUID, label" to search the whitelist.

* **Add test whitelist:**  Click "+ test whitelist" and fill in "whitelist name, description, and other whitelist user information to create. Whitelist names and SSIDs/UUIDs cannot be modified after being added.

* **Associated Experiments and Features:**  Click on a specific number to view the details of the "Experiments and Features" associated with the whitelist.

* **Operation**:

   * **Edit:**  Only the person in charge of the whitelist can modify the corresponding whitelist information. After editing and modifying the whitelist, the experiments or features that have used the whitelist will also take effect immediately.

   * **Delete:**  After deleting the whitelist, the resident whitelist will not be visible to the created experiment or feature. Experiments and features that have used this whitelist are not affected.


<span id="6acfc505"></span>
# New whitelist

Click on the  **+ test whitelist** of the whitelist list to configure the parameters of the new whitelist in the pop\-up window.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/1025ba5b40c94234a5d5d81faba303f5~tplv-goo7wpa0wc-image.image) </span>


|**Parameter** |**Configuration instructions** |
|---|---|
|**Name** & **Description** |Customize the name and description of the whitelist to identify the whitelist. |
|**Person in charge** |The person in charge of whitelist maintenance. |
|**User whitelist** |Enter the user ID (SSID/UUID) that needs to participate in the debugging in the future. The maximum user ID character cannot exceed 100 characters.<br><br><br>* If it is a client side experiment and Features: Enter the unified ssid.<br><br>* If it is server level experiment and Feature: Please enter according to the type of decision_id (shunt ID), if the server level SDK configuration decision_id corresponding ID is the type of uuid, the whitelist needs to configure uuid, if decision_id use ssid, the whitelist needs to configure ssid.<br><br>   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div><br>   <br><br>   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">If the user is a real\-name user, use uuid as decision_id, if there are anonymous users, it is recommended to use ssid as decision_id, because anonymous users do not have uuid.   </div><br>   <br><br>You can enter it manually in the text box, or you can click the QR code logo after the text box to enter it by scanning the code.<br><br><br>* **Manual entry**<br><br>   * Enter the user's UUID/SSID manually, separated by a comma (,) or the Enter key, up to 1000 entries are supported.<br><br>   * SSID acquisition method: By [User Details](https://docs.byteplus.com/docs/DataTester/User-Details)entering UUID, SSID can be queried. To obtain the SSID, please refer to the [Data Access Overview](https://docs.byteplus.com/docs/DataTester/Data-Access-Overview)documentation.<br><br>* **Scan code entry**<br><br>   Manually entered UUID and SSID numbers are long (eg: ssid = "a0166a58\-137a\-410c\-af02\-04acc905\*\*\*\*"), which is prone to errors and inconvenient. Therefore, for mobile applications (iOS, Android), support scanning QR code to enter device ID. For details see: [Scan the Code to Enter the Device ID](https://docs.byteplus.com/docs/DataTester/Scan-the-Code-to-Enter-the-Device-ID). |


<span id="b2172e32"></span>
## Use a whitelist


* **Create an experiment:**  In the process of creating an experiment, the "Add whitelist" position, drop down to select the commonly used whitelist, or you can create a commonly used whitelist.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/b67bdcd3b70348a7a5d37608a460dac1~tplv-goo7wpa0wc-image.image) </span>

* **Create Feature:**  In the process of creating Feature, "Publish Audience" location, drop down to select the commonly used whitelist, you can also create a commonly used whitelist.


If a user is a whitelisted user for a certain version, then experimental offloading has no impact on that user and is fixed to that version.

For users on the whitelist, the data after the experiment is started will also be calculated into the experiment report.
