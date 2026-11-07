---
title: "Managing device groups"
product: "SealSuite"
product_code: "sealsuite"
source: "https://docs.byteplus.com/en/docs/sealsuite/docs-managing-device-groups"
---

The devices logged into the SealSuite client will be counted and displayed in the asset list, allowing you to collectively manage these devices in accordance with the enterprise's device management requirements. This article explains how to organize the grouping of devices.

<span id="d5c0d44a"></span>
# Adding groups


1. Log in to the SealSuite Admin Console.

2. In the left navigation bar, select **Endpoint** \> **Assets** \> **Asset List**.

3. At the bottom of the device grouping area, click **Add New Device Group**.

4. In the **Add New Device Group** dialog box, complete the following configurations and click **Confirm**.

   * **Group name**: Custom name. You also need to click the multilingual icon on the right side of the input box to configure the multilingual **Default** display and **English**. The **Default** display configuration item is mandatory. If the corresponding language is empty after filling, the default value will be displayed.

   * **Grouping method**:

      * **Automatic grouping**: Set filtering conditions based on the device's basic fields or custom attributes. Devices that meet the filtering conditions will be automatically classified into this group. This grouping method does not allow manual addition or removal of devices.

         For example, the filtering conditions set for automatic grouping are shown below, indicating that all devices with Windows operating systems are grouped.

         <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/6d69ac839a764e469e548825dac61429~tplv-goo7wpa0wc-image.image) </span>

         <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="3">tip         </div>
         

         <div data-tips="true" data-tips-type="tip" data-wrapper-indent="3">The data in Automatic grouping is updated every hour. If a single device reports its status, SealSuite will refresh the group for that specific device.         </div>
         

      * **Manual grouping**: Manually select specified devices for grouping. This method allows manual addition or deletion of devices within the group.

         After selecting the group, you need to set the **Expiration**. Instructions for setting:

         * If a validity period is set, it represents the valid duration of the device within the group. After expiration, the device will be removed from the group.

         * Not setting an expiration period means there is no expiration.

   * **Manage Labels**: (Optional) Select one or more tags to implement tag\-based permission isolation. Only administrators whose permission scope includes these tags can view and manage the group in the endpoint list. This prevents unauthorized or accidental modifications to critical groups.

      * Available tags: Includes tags in the tag library where the effective module is set to **Device Group** or **Global**. For details on creating tags, see [Managing the tag Library](https://docs.byteplus.com/docs/sealsuite/managing-the-tag-library).

      * Compatibility: If no tags are specified, the group remains globally visible by default with no data permission restrictions.


<span id="380ceedf"></span>
# Viewing and editing a group

In the left\-hand group list on the **Asset List** page, click a group name to enter its \*\*\*\* details page.


* **View group details**: View configuration info including the Group Name, Grouping Method (Automatic/Manual), bound Management Tags, Last Modified By, and Modification Time.

* **Edit group**: Modify the group name, policy configurations, and management tags. The requirements are the same as for creating a new group.

* **Delete group**: Perform deletions from either the details page or the group list.


<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>



* <div data-tips="true" data-tips-type="warning">Group deletion is permanent and cannot be undone.</div>


* <div data-tips="true" data-tips-type="warning">If a device belongs only to the deleted group, it automatically moves to <strong>Ungrouped Devices</strong>.</div>


* <div data-tips="true" data-tips-type="warning">Deleting a group associated with SealSuite policies or rule groups may affect their functionality.</div>



<span id="ebc31239"></span>
# Changing device grouping

On the **Asset List** page, locate the specified device within the designated group, click on **Edit Group** in the **Action** column, and the following modifications can be made in the dialog box:

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">Only the <strong>Manual grouping</strong> type device group can be changed. The device group of type <strong>Automatic grouping</strong> associated with this device cannot be removed manually. Furthermore, manually adding <strong>Automatic grouping</strong> type device group is not supported.</div>



* The newly added **Manual grouping** type device grouping allows you to click **Remove** to delete the grouping.

* Click **Add New** to facilitate adding multiple manual grouping type device groups.

* The expiration period for a **Manual grouping** type device group can be modified.

   * If an expiration period is set, the device will be removed from the group once that period expires.

   * Not setting an expiration period means there is no expiration.


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/902bb26bab524676b72ecf5fb47a366e~tplv-goo7wpa0wc-image.image) </span>

<span id="7a951912"></span>
# Removing devices from the group

On the **Asset List** page within the specified group, find the specified device information and click **Remove** in the **Action** column to remove the device from the current group.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>



* <div data-tips="true" data-tips-type="warning">Only devices of the <strong>Manual grouping</strong> type can be removed within the device group. In device groups of type <strong>Automatic grouping</strong>, devices cannot be added or removed.</div>


* <div data-tips="true" data-tips-type="warning">Deleting a group will move any devices that belong exclusively to it to the "<strong>Unidentified</strong> <strong>Devices</strong>" list.</div>



<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/9b36bb0536bb4314a79590f6c2e5de39~tplv-goo7wpa0wc-image.image) </span>

<span id="7f94db84"></span>
# **Cleaning up inactive devices**


1. Log in to the SealSuite Admin Console.

2. In the left navigation bar, select **Endpoint** \> **Assets** \> **Asset List**.

3. In the upper right corner of the **Asset List** page, click **More** \> **Inactive Device Cleanup**.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/d29dafb41da6462389a7005eb78feac9~tplv-goo7wpa0wc-image.image) </span>

4. In the **Inactive Device Cleanup** dialog box, complete the following configurations and click **Confirm**.

   * **Data Clean\-up Rule**: Select the number of days to wait before cleaning up the data after the device status has become inactive. Options include **Do not clean** (selected by default), **7 days**, **14 days**, **30 days**, or **Custom** (allows entries from 0\-365 days, where 0 indicates immediate cleanup).

   * **Data Type**: Supports multiple selections, with none selected by default. Options include **Device list and device grouping information**, **Software statistics**, **Software distribution record**, **Device approval record**, and **Patch statistics**.


<span id="63e422fc"></span>
# Related documentation

[Managing endpoint devices](https://docs.byteplus.com/docs/sealsuite/docs-viewing-device-information)

[Adding custom attributes to devices](https://docs.byteplus.com/docs/sealsuite/docs-adding-custom-attributes-to-devices)
