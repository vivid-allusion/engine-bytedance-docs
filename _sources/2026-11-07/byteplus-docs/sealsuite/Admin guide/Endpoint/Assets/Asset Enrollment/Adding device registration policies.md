---
title: "Adding device registration policies"
product: "SealSuite"
product_code: "sealsuite"
source: "https://docs.byteplus.com/en/docs/sealsuite/docs-adding-device-registration-rules"
---

The device registration rule enables you to differentiate between personal and work devices, as well as to label device attributes. After you add one or more rules, users within the rule scope can initiate requests to change device groups or attributes through the SealSuite client. For example, users can apply to change their personal devices to work devices.

<span id="Instructions for use"></span>
# Instructions for use

You can create multiple device registration rules. If multiple rules are enabled, they will be assessed sequentially based on their priorities, providing flexibility in configuring the registration rule that best meets your organization's needs.

<span id="Procedure"></span>
# Procedure


1. Log in to the Admin Console.

2. In the left navigation bar, click **Endpoint** \> **Assets** \> **Enrollment**.

3. Choose **Policy Management** tab, and use one of the following methods to add a device registration rule.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/b67087509154418b8454fb16f824031a~tplv-goo7wpa0wc-image.image) </span>

   * **Method 1**: Add a registration rule based on a template.

      <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="2">tip      </div>
      

      <div data-tips="true" data-tips-type="tip" data-wrapper-indent="2">SealSuite offers registration rule templates by copying, which you can quickly add a registration rule.      </div>
      

   * **Method 2**: Add a registration rule from scratch.

      Click  **+Add New Rule** to add a new registration rule.

4. Complete the following configurations and click **Confirm**.

   * **General**: Customize rule name and priority.

      Rule priority is assigned a value between 0 and 100, with higher values indicating higher priority. If multiple rules are enabled for a user, they will be assessed sequentially based on their priorities. The assessment process stops after a match is found. In the event of two rules having the same priority, the one with the latest updated time will be executed.

      <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/e0d4ecb938a24b819958e7ad1e928b35~tplv-goo7wpa0wc-image.image) </span>

   * **Registration Conditions**: Select **Device Group** or **Device properties**. To set the registration condition, follow the instructions below.

      * After selecting **Device Group**, you need to specify device groups.

         <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/241d9aacfbe54b8493c96fc1b80716f9~tplv-goo7wpa0wc-image.image) </span>

      * After selecting **Device properties**, you need to specify the basic or the custom attributes along with their values.

         For example, the registration condition shown in the figure below indicates that the device of a user whose employee number is lower than 1,000 will trigger the rule.

         <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/c82bfa16807d43a69af0bdde73540597~tplv-goo7wpa0wc-image.image) </span>

      * Click **Add new** to add more registration conditions, and their relationships can be **And** or **Or**.

         <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/1a357a8371774007ba472b7782797b14~tplv-goo7wpa0wc-image.image) </span>

   * **Registration Details**: Set the content displayed in the device registration dialog box of the SealSuite client.

      During setup, you can preview the dialog box on the right.

      * **Title**: Enter the desired title of the dialog box.

      * **Description**: Add a description for the dialog box.

      * (Optional) **Application** **Reasoning**: SealSuite offers a default prompt and supports custom editing. You can enter a prompt to ask users to provide an application reason when registering the device in the SealSuite client.

      * **Prompt Content**: Customize the global prompt content that will be displayed as a banner at the top of the SealSuite client interface.

   * **Approval Method**: Select either **Automatic approval** or **Manual approval.** 

      <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/49d15716059142559fc3ec911653a0c2~tplv-goo7wpa0wc-image.image) </span>

      * **Automatic approval**: User\-initiated applications are automatically approved, and the Admin Console simply logs the approval record.

      * **Manual approval**: User\-initiated applications require your approval on the **Device Registration** page in the Admin Console.

         You can choose between two notification methods: **Third party notification to approver** and **Third party notification to applicant**. After being selected, a third\-party robot must be set up so that the designated personnel can receive approval messages or results.

         <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="3">tip         </div>
         

         <div data-tips="true" data-tips-type="tip" data-wrapper-indent="3">SealSuite offers default <strong>Third</strong> <strong>Party</strong> <strong>Notification</strong> <strong>Content</strong>, which includes variables, including Employee, Department, approver, and Operation Time. These values will be automatically populated based on actual information. You can also customize the content and reset it to the default value if needed by clicking <strong>Reset</strong> <strong>Content</strong>.         </div>
         

   * **Scope**: Select either **All employees** or **Selected employees**, with the latter requiring setting the effective range by the department dimension.

5. Go back to the **Device Registration** page, and toggle the rule's switch in the **Action** column to activate it.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/0eb358876c6944f09db91860367e147f~tplv-goo7wpa0wc-image.image) </span>
