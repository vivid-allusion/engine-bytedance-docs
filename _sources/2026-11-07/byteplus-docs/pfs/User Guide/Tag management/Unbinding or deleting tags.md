---
title: "Unbinding or deleting tags"
product: "Parallel File Storage"
product_code: "pfs"
source: "https://docs.byteplus.com/en/docs/pfs/Unbinding-or-deleting-tags"
---

Parallel File Storage adds support for tag management, tags can be used to identify resources. When an instance no longer needs a certain tag, you can remove the binding between the instance and the tag. This topic explains how to unbind tags from instances.

<span id=".5rOo5oSP5LqL6aG5"></span>
## **Note**


* Each operation supports unbinding up to 20 tags at most.

* After unbinding the tag, if the number of resources bound to the tag is zero, it will be automatically deleted.


<span id=".5pON5L2c5q2l6aqk"></span>
## **Procedure**

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">Tip</div>


<div data-tips="true" data-tips-type="tip">Unbinding tag pairs has no impact on the running of instances.</div>



1. Log on to the [PFS console](https://console.byteplus.com/pfs).

2. At the top left corner of the menu bar, select the target region.

3. Find the target instance on the instance list page and click edit icon in the **Tag** column.

   You can also click target instance to enter the instance information page, and in the Basic Information section, click the edit icon in the **Tag** column.

4. In the pop\-up dialog box, first confirm the instance information, find the label that needs to be unbound, and click delete icon on the right side of the label.

5. Click **OK**.
