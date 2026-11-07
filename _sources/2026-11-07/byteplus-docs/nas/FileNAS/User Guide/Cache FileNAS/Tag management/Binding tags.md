---
title: "Binding tags"
product: "FileNAS"
product_code: "nas"
source: "https://docs.byteplus.com/en/docs/nas/Binding_tags"
---

FileNAS supports tag\-based resource management. Tags help you categorize file systems by purpose, type, owner, environment or other criteria, making filtering and managing resources easier. This topic explains how to bind tags to a file system.

<span id="50923dab"></span>
## Tagging rules

The rules for FileNAS tags are explained below.


|**Category** |**Description** |
|---|---|
|Tag key |* Valid characters include: Unicode letters (e.g., Chinese characters and English letters), numbers, spaces, and special characters such as `_.:/=+-@`<br><br>* Length: 1\-128 characters.<br><br>* Case sensitivity: `Type` and `type` are considered two different tag keys. |
|Tag value |* Valid characters include: Unicode letters (e.g., Chinese characters and English letters), numbers, spaces, and special characters such as `_.:/=+-@`<br><br>* Case sensitivity: `Extreme` and `extreme` are considered two different tag values.<br><br>* Length: 0\-256 characters. The tag value can be empty. |
|Quantity |* Each FileNAS file system can have up to 50 tags, but there is no global limit on total tags.<br><br>* You can add up to 20 tags at a time. |


<span id="e3f903f3"></span>
## Notes

Within a single file system, each tag key must be unique and can only have one tag value.

<span id="66c10c51"></span>
## Steps

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">This section only covers the steps to bind tags to an existing file system. You can also bind tags when creating a file system.</div>


* <div data-tips="true" data-tips-type="tip">Binding a tag does not affect the operation of the file system.</div>


1. Log in to the [FileNAS console](https://console.byteplus.com/filenas/).

2. In the top menu bar, select the region where the target file system is located.

3. In the left navigation pane, click **File System** \> **File System list**.

4. On the **File System list** page, click the edit icon in the **Tag** column for the file system you want to edit.

   Alternatively, click the target file system to enter File System details page, then click the edit icon next to **Tag** in the **Basic information** section.

5. In the dialog box, verify the file system information, and enter the tag key and tag value as needed.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">The tag key and value must follow certain rules. For details, see the tagging rules in this document.   </div>
   

6. Click **OK**.
