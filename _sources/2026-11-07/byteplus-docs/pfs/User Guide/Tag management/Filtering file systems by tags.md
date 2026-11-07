---
title: "Filtering file systems by tags"
product: "Parallel File Storage"
product_code: "pfs"
source: "https://docs.byteplus.com/en/docs/pfs/Filtering-file-systems-by-tags"
---

After binding tags to instances, you can use tags to filter instances in the instance list on the Parallel File Storage console, which helps you quickly find instances with specific tags. This topic describes the specific steps to filter instances by tags.

<span id=".5rOo5oSP5LqL6aG5"></span>
## **Note**


* When filtering, the tag key (Key) is required, and the tag value (Value) is optional. If the tag value is not filled, it means there is no restriction on the tag value, and it will search for all instances that are bound to the specified tag key.

* Up to 10 tags can be set simultaneously for filtering, and there is an **OR** relationship between different filtering conditions.


<span id=".5pON5L2c5q2l6aqk"></span>
## **Procedure**


1. Log on to the [PFS console](https://console.byteplus.com/pfs).

2. At the top left corner of the menu bar, select the target region.

3. On the **Instances** page, click **Tag filter** at the top right corner of the page.

4. In the pop\-up text box, set the tag keys and tag values that need to be filtered. You can click **Add tag** to enter multiple tag keys for filtering, and multiple filtering conditions are connected with OR.

5. After clicking **OK**, you can view all instance information that meets the filtering criteria in the example list below. If you need to reset the filtering criteria, please click **Reset** first to clear all filtering conditions, and then set the conditions again for filtering according to step 4.


<span id="6587b8d3"></span>
## Tag filtering example


|Filtering method |Description |Example |
|---|---|---|
|Filter by tag key |When filtering, only set the tag key to view all instances with the specified tag key and any tag value. You can also specify multiple tag keys for filtering to view instances that meet any of the filtering conditions. When retrieving, only the tag key is restricted, and the tag value is not restricted, which is suitable for fuzzy search scenarios. |* Filter Example 1<br><br>   * Filter condition: Set the tag key as department and the tag value as empty.<br><br>   * Filter result: It will filter out all PFS instances that contain the tag key department.<br><br>* Filter Example 2<br><br>   * Filter condition: Set the tag keys as department and owner and the tag values as empty.<br><br>   * Filter result: It will filter out all PFS instances that contain either the tag key department or owner. |
|Filter by tag key + tag value |When filtering, specifying both the tag key and tag value means to view all instances that are bound with the specified tag. You can also specify multiple tags simultaneously to view instances that meet any of the filtering conditions. Specifying both the tag key and tag value is suitable for precise search scenarios. |* Filter Example 1<br><br>   * Filter condition: Set tag department:game.<br><br>   * Filter result: It will filter out all PFS instances that contain the tag department:game.<br><br>* Filter Example 2<br><br>   * Filter condition: Set tag keys department:game and owner:Ben.<br><br>   * Filter result: It will filter out all PFS instances that contain either the tag department:game or owner:Ben. |
