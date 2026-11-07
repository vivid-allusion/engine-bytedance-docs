---
title: "Binding tags"
product: "FileNAS"
product_code: "nas"
source: "https://docs.byteplus.com/en/docs/nas/efs_Binding_tags"
---

EFS supports tag\-based resource management. Tags help you categorize file systems by purpose, type, owner, environment or other criteria, making filtering and managing resources easier. This topic explains how to add tags to a file system.

<span id="h38kUesA"></span>
## Tagging rules

The rules for EFS tags are explained below.


|**Category** |**Description** |
|---|---|
|Tag key |* Valid characters include: Unicode characters (for example, Chinese characters and English letters), numbers, spaces, underscores (_), periods (.), colons (:), forward slashes (/), equal signs (=), plus signs (+), hyphens (\-), and at symbols (@).<br><br>* Length: 1–128 characters.<br><br>* Case sensitivity: Tag keys are case\-sensitive. For example, `Type`and`type`are treated as different tag keys. |
|Tag value |* Valid characters include: Unicode characters (for example, Chinese characters and English letters), numbers, spaces, underscores (_), periods (.), colons (:), forward slashes (/), equal signs (=), plus signs (+), hyphens (\-), and at symbols (@).<br><br>* Case sensitivity: `Extreme` and `extreme` are considered two different tag values.<br><br>* Length: 0–256 characters. The tag value can be empty. |
|Quantity |* Each EFS file system can have up to 50 tags, but there is no global limit on total tags.<br><br>* You can add up to 20 tags at a time. |


<span id="PB9UFAFA"></span>
## Notes

Within a single file system, each tag key must be unique and can only have one tag value.

<span id="4lyWWkJF"></span>
## Steps

<div data-tips="true" data-tips-type="tip">Note</div>



* <div data-tips="true" data-tips-type="tip">This section only covers the steps to bind tags to an existing file system. You can also bind tags when creating a file system.</div>


* <div data-tips="true" data-tips-type="tip">Adding tags does not affect file system operations.</div>


1. Log in to the [EFS console](https://console.byteplus.com/efs).

2. In the top menu bar, select the region of the file system you want to manage.

3. In the left navigation pane, select **File System**.

4. On the **File System** page, click the edit icon in the **Tag** column for the file system whose tags you want to edit.

   <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">Note   </div>
   

   <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">Alternatively, click the file system name to go to the <strong>Overview</strong> page. Then, click the edit icon next to <strong>Tag</strong> in the <strong>Advanced Information</strong> section.   </div>
   

5. In the **Edit tag** dialog, verify the file system information, and enter the tag key and tag value as needed.

   <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">Note   </div>
   

   <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">The tag key and value must follow certain rules. For more information, see <a href="https://docs.byteplus.com/en/docs/nas/efs_Binding_tags#h38kUesA">Tagging rules</a>.   </div>
   

6. Click **OK**.
