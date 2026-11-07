---
title: "Filtering file systems by tag"
product: "FileNAS"
product_code: "nas"
source: "https://docs.byteplus.com/en/docs/nas/efs_Filtering_file_systems_by_tag"
---

After binding tags to file systems, you can filter file systems by tag to quickly find those with specified tags. This topic explains how to filter file systems by tag.

<span id="t7XSm02I"></span>
## Notes


* Filtering requires a tag key, but the tag value is optional. If the tag value is left empty, the search will include all file systems with the specified tag key.

* You can set up to 10 tags for filtering, and different filter conditions are combined using **OR** logic.


<span id="T2557c8Y"></span>
## Steps


1. Log in to the [EFS console](https://console.byteplus.com/efs).

2. In the top menu bar, select the region of the file system you want to manage.

3. In the left navigation pane, select **File System**.

4. On the **File System** page, click **Tag filter** in the upper\-right corner.

5. In the box that appears, enter the tag key and tag value to filter.

   Click **Add tag** to enter multiple tag keys for filtering. Multiple filter conditions are combined using **OR** logic.

6. Click **OK** to view all file systems that meet the filter conditions in the file system list.

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">Note   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">To reset the filters, click <strong>Reset</strong> to clear all conditions, and then set them again to apply your desired filters.   </div>
   

<span id="AMLRlXTT"></span>
## Examples


|Filter method |Description |Example |
|---|---|---|
|Filter by tag key |Limiting tag keys but not tag values helps with fuzzy search scenarios.<br><br><br>* Filtering by tag key alone returns all file systems where the specific tag key exists and the corresponding tag value may be any valid string.<br><br>* You can select multiple tag keys to view file systems that match any of the filtering conditions. |* Filter example 1<br><br>   * Filter condition: Set the tag key `department` with an empty tag value.<br><br>   * Filter result: The result will include all EFS file systems containing the tag key `department`.<br><br>* Filter example 2<br><br>   * Filter condition: Set the tag keys `department` and `owner` with no tag values.<br><br>   * Filter result: The result will include all EFS file systems containing the tag keys `department` or `owner`. |
|Filter by tag key + tag value |Filtering by both tag key and tag value is effective for precise search operations.<br><br><br>* Specifying both tag keys and tag values displays all file systems bound to those tags.<br><br>* You can select multiple tags to view file systems that match any of the filtering conditions. |* Filter example 1<br><br>   * Filter condition: Set the tag `department:game`.<br><br>   * Filter result: The result will include all EFS file systems containing the tag `department:game`.<br><br>* Filter example 2<br><br>   * Filter condition: Set the tags `department:game` and `owner:Ben`.<br><br>   * Filter result: The result will include all EFS file systems containing the tag `department:game` or `owner:Ben`. |
