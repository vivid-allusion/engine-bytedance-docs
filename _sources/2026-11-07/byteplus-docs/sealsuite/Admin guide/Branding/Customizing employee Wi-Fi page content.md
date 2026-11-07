---
title: "Customizing employee Wi-Fi page content"
product: "SealSuite"
product_code: "sealsuite"
source: "https://docs.byteplus.com/en/docs/sealsuite/docs-customizing-employee-wi-fi-page"
---

You can create and display custom instructional text on the employee Wi\-Fi screen in the SealSuite client for mobile. This feature is useful for providing targeted guidance to users in specific situations.

For example, if a certain network configuration requires users to manually disconnect from Wi\-Fi under certain conditions, you can create a message explaining how to do so and display it only to the relevant users, devices, or operating systems.

<span id="edb3ab85"></span>
# How to Add New Instructions


1. Log in to the Admin Console.

2. In the left navigation bar, click **Branding**.

3. In the **Function Configuration** section, click the **Employee Network Access Page Content** card.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/752ae7334adb4aa086a82567e6fd1613~tplv-goo7wpa0wc-image.image) </span>

4. On the page, click  **+ New message**.

5. In the **Basic information** section, configure the following:

   1. Enter a descriptive **Title** for this set of instructions.

   2. Choose how the text will be displayed:

      * **Rotate text based on connections status**: Allows you to show one message when the user is **Not Connected** and a different message when they are **Connected**.

      * **Fixed text**: Shows a single, consistent message regardless of the Wi\-Fi connection status.

   3. Enter the instructional text in the **Chinese** and **English** fields. Both languages are required.

      <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="2">tip      </div>
      

      <div data-tips="true" data-tips-type="tip" data-wrapper-indent="2">You can see a live preview for the Chinese text on the right. The English text can be previewed by changing the mobile device's system language to English.      </div>
      

      <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/144e518ef8934ae3a89ec0214f96a49b~tplv-goo7wpa0wc-image.image) </span>

6. In the **Scope** section, define who will see these instructions:

   1. Choose to target by **Employee** or **Device**.

      * **Employee**: Scope by **Department** or **Role**.

      * **Device**: Scope by **Device**, **OS**, and **Group**.

   2. Set a **Priority** (0\-100). Higher numbers have higher priority. If a user or device matches multiple policies, only the one with the highest priority will be applied.

7. Click **Save as Draft** or **Save and Publish**.

   * **Save as Draft**: Only save the current configuration, but will not take effect immediately. The effective status switch can be turned on on the **Employee Network Access Page Content** page.

   * **Save and Publish**: Save the current configuration and take immediate effect.


<span id="bb0774d8"></span>
# How to Manage Existing Instructions


1. Log in to the Admin Console.

2. In the left navigation bar, click **Branding**.

3. In the **Function Configuration** section, click the **Employee Network Access Page Content** card.

4. On the management page, you can perform the following actions:

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/88ed3538c42f4befb924f96474f15d3d~tplv-goo7wpa0wc-image.image) </span>

   * **Enable/Disable**: Use the toggle switch in the Actions column to activate or deactivate a set of instructions.

   * **Edit**: Click Edit to modify the content or scope.

   * **Delete**: Click Delete to permanently remove the instructions.

   * **Filter**: Use the filters at the top of the list to find instructions by Status, User, Device, or Text message.


<span id="f20a2a89"></span>
# Verifying the Results

After a policy is enabled, the custom text will appear at the bottom of the Employee Wi\-Fi screen in the SealSuite client for all targeted mobile users.
