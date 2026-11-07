---
title: "Configure print watermarks"
product: "SealSuite"
product_code: "sealsuite"
source: "https://docs.byteplus.com/en/docs/sealsuite/config-print-watermark"
---

Print watermark policies add identifying information to documents when users print them. Watermarks help trace the source of a document, deter unauthorized copying, and support document security and compliance.

Print watermarks are compatible with Windows clients and macOS clients. To use print watermarks on macOS clients, grant Full Disk Access.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Print watermarks are supported only in SealSuite 3.0.10 and later, and client 3.0.20 and later.</div>


<span id="4b2c3859"></span>
## Add a print watermark policy


1. Log in to the Admin Console.

2. In the left navigation pane, choose **DLP** \> **Watermark**.

3. Click the **Print Watermark** tab, then click **Add Policy** in the upper\-right corner.

   If you are using this feature for the first time, click **Configuration Policy**.

4. On the **New Print Watermark Policy** page, configure the parameters. The following table describes the parameters.

   Preview the watermark on the right side of the page. Rendering differences between Windows and macOS may cause the preview to differ from the printed output. Check an actual printout to confirm the result.

   <span>![图片](https://lf3-static.bytednsdoc.com/obj/eden-cn/809eh7uhkbd/topic-docs/swg-ndlp-en-20260923/print-watermark-en.png) </span>

   
   |**Area** |**Configuration item** |**Description** |
   |---|---|---|
   |**General** |**Policy name** |Custom name of the print watermark policy. You can enter Chinese characters, English letters, spaces, numbers, and special characters. The maximum length is 128 characters.<br><br>The policy name cannot duplicate an existing policy name and must be globally unique. |
   ||**Priority** |The priority of the current policy. The value ranges from 0 to 100. A larger value indicates a higher priority.<br><br>You can configure multiple policies at the same time. However, for a specific device or user, only the policy with the highest priority takes effect at a given time.<br><br>If two policies have the same priority, the policy with the latest modification time takes effect first. To view the policies with the latest modification times, set **Sort by edit time** in the sorting options at the top of the policy list. |
   ||**Manage labels** |Select a tag to associate with the current policy. This parameter is optional. The drop\-down list displays only the tags granted to the current administrator. Associated tags isolate policy permissions between administrators in different regions or business lines.<br><br>To add or adjust the tag options visible in the drop\-down list, a super administrator must modify the "Management tag scope" for your administrator role in **Enterprise Settings** \> **Administrator Permissions**. For more information, see [Editing Administrator Access](https://docs.byteplus.com/en/docs/sealsuite/docs-editing-or-deleting-administrator). |
   |**Watermark Style** |**Copywriting** |Select the text to display in the watermark, including username, email prefix, phone number suffix, device name, device serial number, private IP address, public IP address, time, or custom text.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">For a better watermark display effect, we recommend using no more than 5 watermark text items.</div><br> |
   ||**Newline rule** |Set the line break rule for the watermark text as needed. The following options are available:<br><br><br>* **Line wrap by field**: Each text field occupies a separate line. For example, the username occupies one line and the time occupies one line.<br><br>* **Line wrap by character count**: Set the maximum number of characters per line. A line break occurs when the character count reaches this limit. Fields in the text are separated by spaces, and each space counts as one character. The field order follows the order on the configuration page. |
   ||**Font size** |Set the font size of the watermark text. |
   ||**Color** |Set the font color of the watermark text. The default color is gray.<br><br>Click the color box to quickly select a color with your mouse, or manually enter the RGB value, such as `250,4,4`, or the hexadecimal HEX value, such as `#FA0404`, for precise color settings.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">The color displayed on the computer may differ slightly from the actual print color. Use the actual printout as the reference.</div><br> |
   ||**Rotation angle** |Set the rotation angle of the watermark text. The default angle is 45 degrees clockwise. |
   ||**Transparency** |Set the watermark transparency to **Vaguely**, **Medium**, or **Clear**, or select **Custom** to set your own value. |
   ||**Density** |Set the density of the watermark text. SealSuite provides three options: **Loose**, **Moderate**, and **Compact**, and displays the line spacing and column spacing for each option. You can also customize the line spacing and column spacing. |
   |**Scope** ||Set the effective scope by **User** or **Device**.<br><br><br>* If you select **User**, limit the employee scope by **Department** or **Role**.<br><br>* If you select **Device**, limit the device scope by **Device**, **Operating system**, or **Group**.<br><br><br>You can also exclude specific employees or roles. Users in the excluded objects are not subject to this policy. The final effective objects are **Assigned objects \- Excluded objects**.<br><br><br>1. Turn on the switch on the right of **Exclude object**.<br><br>2. Click **Add excluded object** and add excluded objects by device, device group, department, role, or employee as needed. You can add multiple excluded objects. |
   

5. Click **Confirm**.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">If watermark appearance is critical, test a small deployment on both Windows and macOS before rolling out the policy widely. Check that the printed results meet your requirements.</div>


<span id="6bb38850"></span>
## Manage print watermark policies

Enable or disable print watermark policies, and copy, edit, or delete print watermark policies.


1. Log in to the Admin Console.

2. In the left navigation pane, choose **DLP** \> **Watermark**.

3. Click the **Print Watermark** tab and perform the following management operations as needed:

   * **Filter and sort policies**: Use the filter conditions at the top of the policy list to search and filter policies. In the **Sorting method** drop\-down list, select a sorting method to sort policies by priority, edit time, and other rules.

   * **Enable or disable a watermark policy**: Use the switch next to the policy to enable or disable it. When enabled, the policy applies print watermarks to endpoints within its scope.

   * **Copy a watermark policy**: Click **Copy** on the right of the corresponding policy, modify the parameters, and then click **Confirm**.

   * **Edit a watermark policy**: Click **Edit** on the right of the corresponding policy, modify the parameters, and then click **Confirm**.

   * **Delete a watermark policy**: Click **Delete** on the right of the corresponding policy. In the confirmation dialog box, click **Confirm deletion**.

   <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="1">warning   </div>
   

   <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">After a policy is deleted, it cannot be restored, and SealSuite no longer applies print watermark protection to the endpoints in the policy.   </div>
