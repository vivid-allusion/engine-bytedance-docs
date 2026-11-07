---
title: "Binding or adding tags"
product: "Parallel File Storage"
product_code: "pfs"
source: "https://docs.byteplus.com/en/docs/pfs/Binding-or-adding-tags"
---

Parallel File Storage has added support for tag management, allowing tags to be used to identify resources and help you tag and categorize instances with similar characteristics from different perspectives such as usage, type, owner, and environment. This facilitates filtering and management. This topic describes how to bind tags to instances.

<span id=".5qCH562-6K6-572u6KeE5YiZ"></span>
## Tag Setting Rules

The rules for setting up the PFS tag for file storage are shown in the following table.


|**Limitations** |**Description** |
|---|---|
|Tag Key |* Support any language letters or characters (such as Chinese, English letters, etc.), numbers, spaces, and the following special characters: `_.:/=+-@`.<br><br>* The length of the tag key should be 1 to 128 characters.<br><br>* The tag key is case\-sensitive, for example, `Type` and `type` are two different tag keys.<br><br>* `volc:` is a reserved tag key for the system. When adding tags, you cannot set `volc:` in any uppercase or lowercase form as the beginning of the tag key. |
|Tag Value |Support any language letters or characters (such as Chinese, English letters, etc.), numbers, spaces, as well as the following special characters: `_.:/=+-@`.<br><br><br>* Tag values are case\-sensitive, for example, `Extreme` and `extreme` are two different tag values.<br><br>* The length of the tag key should be 0 to 256 characters, which means the tag value can be empty. |
|Quantity |* There is no limit to the total number of tags, but each PFS instance can be bound to a maximum of 50 tags.<br><br>* A maximum of 20 tags can be added each time they are set. |


<span id=".5rOo5oSP5LqL6aG5"></span>
## **Note**

Multiple tags with the same tag key are not allowed within the same instance, and each tag key can only have one tag value.

<span id=".5pON5L2c5q2l6aqk"></span>
## **Procedure**

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">Tip</div>



* <div data-tips="true" data-tips-type="tip">This article only introduces the steps to bind tags to existing instances. You can also bind tags when creating instances. For specific operation steps, please refer to <a href="https://docs.byteplus.com/docs/pfs/Creating-a-file-system">Creating a file system</a>.</div>


* <div data-tips="true" data-tips-type="tip">Binding tag pairs has no impact on the running of the instance.</div>


1. Log on to the [PFS console](https://console.byteplus.com/pfs).

2. At the top left corner of the menu bar, select the target region.

3. Find the target instance on the instance list page and click edit icon in the **Tag** column.

   You can also click target instance to enter the instance information page, and in the Basic Information section, click edit icon in the **Tag** column.

4. In the pop\-up dialog box, confirm the instance information and set the tag key and tag value according to business needs.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">Tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">The tag key\-value needs to meet certain configuration rules. For detailed rule information, please refer to <a href="https://docs.byteplus.com/docs/pfs/Binding-or-adding-tags#%E6%A0%87%E7%AD%BE%E8%AE%BE%E7%BD%AE%E8%A7%84%E5%88%99">Tag Setting Rules</a>.   </div>
   

5. Click **OK**.
