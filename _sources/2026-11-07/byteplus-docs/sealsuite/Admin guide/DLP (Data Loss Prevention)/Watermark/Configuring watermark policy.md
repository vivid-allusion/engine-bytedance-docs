---
title: "Configuring watermark policy"
product: "SealSuite"
product_code: "sealsuite"
source: "https://docs.byteplus.com/en/docs/sealsuite/docs-configuring-watermark-rules"
---

To enhance enterprise data security and enable traceability in case of data leaks, you can apply watermarks to user devices by configuring watermark policies in SealSuite. This guide provides step\-by\-step instructions on how to create, enable, edit, copy, and delete these policies to fit your security requirements.

<span id="d5df95e4"></span>
# Function introduction

A watermark is a visible or invisible watermark applied to a user's device. The main function of watermarks is to enhance the security of enterprise data. When a data leak occurs, you can quickly track the origin based on the watermark information.

<span id="f67ee0f3"></span>
# Creating a watermark policy


1. Log in to the Admin Console.

2. In the left navigation bar, click **DLP** \> **Watermark**.

3. On the **Watermark** page, click the **Screen Light and Dark Watermark** tab.

4. In the **Screen Light and Dark Watermark** tab, click  **+ New policy** to enter the **Add Watermark Policy** page and complete the following configurations.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/b5471e43918a49989e1eeaac4766dcd1~tplv-goo7wpa0wc-image.image) </span>

   
   |**Area** |**Item** |**Description** |
   |---|---|---|
   |General |Policy Name |Create a custom name to identify the policy. |
   ||Priority |Specify the priority of the current policy. The value can range from 0 to 100, with a higher value indicating a higher priority. You can have multiple policies in effect at the same time. When SealSuite applies watermarks to devices, it matches the policies in order according to the priority value. Once a matching policy is found, SealSuite stops the detection process. If no matching policy is found, the detection process stops after all policies have been evaluated. If two policies have the same priority, the one with the most recent modification time is applied first. |
   ||Manage labels |Associate the current policy with specific tags (optional). The drop\-down list only displays tags that the current administrator has been granted. By associating tags, you can enforce policy permission isolation between administrators of different regions or business lines. To add or adjust the visible tag options in the drop\-down list, a super administrator must modify the Managed tag scope for your administrator role under **Settings** \> **Admin Access**. |
   |Watermark Type |Visible Watermark |Visible watermark refers to a watermark that always floats above the screen. When you choose a visible watermark, you need to customize the **Watermark Styles**, including the **Font Size**, **Watermark Opacity**, **Watermark Density**, **Rotation Angle**, and **Content**.<br><br>After customizing the **Watermark Styles**, you can click on **Preview watermark** to see if the visible watermark appears as you expect. |
   ||Invisible Watermark |Invisible watermark refers to a watermark that is not visible to the naked eye. This type of watermark requires the use of SealSuite's invisible watermark extraction function to obtain the watermark information. For invisible watermarks, you do not need to configure custom watermark styles. Instead, you need to select **Watermark Strength** as needed. The watermark strength can be set to Low, Medium, or High. The options are as follows:<br><br><br>* **Low Intensity**: The watermark is invisible to the naked eye and has a lower extraction success rate. It is suitable for scenarios with high requirements for watermark concealment.<br><br>* **Medium Intensity**: The watermark is not obvious, and the extraction success rate is between that of low and high strength.<br><br>* **High Intensity**: Slight color blocks are visible to the naked eye in some cases with higher extraction success rate. It is suitable for scenarios with high requirements for extraction rate.<br><br><br>In addition, you can view the **Watermark Report Preview** when configuring invisible watermarks. The preview displays watermark report information obtained through the SealSuite invisible watermark extraction function, including image information, device information, and user information. |
   |**Scope** | |Limit the scope by **Employee** or **Device**.<br><br><br>* When selecting **Employee**, you need to limit the employee range by **Department** or **Role**.<br><br>* When selecting **Device**, you need to limit device range by **Device**, **Operating System (OS)** , or **Group**.<br><br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning"><strong>Linux device requirements</strong></div><br><br><br><br>* <div data-tips="true" data-tips-type="warning">Only supports <strong>Ubuntu 18.04</strong> and later.</div><br><br><br>* <div data-tips="true" data-tips-type="warning">Linux endpoints must run SealSuite client version <strong>3.3.13</strong> or later.</div><br><br><br>* <div data-tips="true" data-tips-type="warning">After receiving the screen watermark policy, Linux devices <strong>must be restarted</strong> for the watermark to take effect.</div><br> |
   


<span id="a08ee188"></span>
# Enabling or disabling a watermark policy


1. Log in to the Admin Console.

2. In the left navigation bar, click **DLP** \> **Watermark**.

3. On the **Watermark** page, click the **Screen Light and Dark Watermark** tab.

4. Locate your target policy, and toggle the switch as shown in the picture below to enable or disable the specified policy.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/dfd18f824da8481ca1ed9efca4ce189b~tplv-goo7wpa0wc-image.image) </span>

   * If the switch is on, the policy is active, and SealSuite will apply watermarks to all devices within the policy's scope.

   * If the switch is off, the policy is inactive, and SealSuite will not apply watermarks using this policy.


<span id="2b3356fa"></span>
# Editing a watermark policy


1. Log in to the Admin Console.

2. In the left navigation bar, click **DLP** \> **Watermark**.

3. On the **Watermark** page, click the **Screen Light and Dark Watermark** tab.

4. On the right side of your target policy, click **Edit**.

5. On the **Edit Watermark Policy** page, edit the configuration items of the policy and click **Save**.

   For instructions on how to configure each item, please refer to [Creating a watermark policy](https://docs.byteplus.com/docs/sealsuite/docs-configuring-watermark-rules#f67ee0f3).


<span id="8f35f7cf"></span>
# Copying a watermark policy


1. Log in to the Admin Console.

2. In the left navigation bar, click **DLP** \> **Watermark**.

3. On the **Watermark** page, click the **Screen Light and Dark Watermark** tab.

4. On the right side of your target policy, click **Copy**.

5. SealSuite will copy the configuration of the current policy to the **Add Watermark Policy** page. You can keep or adjust the current configuration, then click **Add** to create a new watermark policy.

   For instructions on how to configure each item, please refer to [Creating a watermark policy](https://docs.byteplus.com/docs/sealsuite/docs-configuring-watermark-rules#f67ee0f3).


<span id="72cb6395"></span>
# Deleting a watermark policy

The policy cannot be restored after being deleted, and SealSuite will no longer apply watermarks to users' devices through this policy.


1. Log in to the Admin Console.

2. In the left navigation bar, click **DLP** \> **Watermark**.

3. On the **Watermark** page, click the **Screen Light and Dark Watermark** tab.

4. On the right side of your target policy, click **Delete**.

5. In the **Warning** dialog box, click **Delete**.
