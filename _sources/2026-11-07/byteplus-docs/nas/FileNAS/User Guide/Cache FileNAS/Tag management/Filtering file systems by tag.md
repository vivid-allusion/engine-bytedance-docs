---
title: "Filtering file systems by tag"
product: "FileNAS"
product_code: "nas"
source: "https://docs.byteplus.com/en/docs/nas/Filtering_file_systems_by_tag"
---

After binding tags to file systems, you can filter file systems by tag to quickly find those with specified tags. This topic explains how to filter file systems by tag.

<span id="9708a4cb"></span>
## Notes


* Filtering requires a tag key, but the tag value is optional. If the tag value is left empty, the search will include all file systems with the specified tag key.

* You can set up to 10 tags for filtering, and different filter conditions are combined using **OR** logic.


<span id="e9d50037"></span>
## Steps


1. Log in to the [FileNAS Console](https://console.byteplus.com/filenas/).

2. In the top menu bar, select the region where the target file system is located.

3. In the left navigation pane, click **File System ** \> **File System list**.

4. On the **File System list** page, click the **Tag filter** in the upper right corner.

5. In the dialog box, enter the tag key and tag value to filter.

   You can click **Add tag** to enter multiple tag keys for filtering. Multiple filter conditions are combined using OR logic.

6. Click **OK** to view all file systems that meet the filter conditions in the file system list.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">To reset the filters, click <strong>Reset</strong> to clear all conditions, then set them again to apply your desired filters.   </div>
   

<span id="f3c62272"></span>
## Examples


|**Filter method** |**Description** |**Example** |
|---|---|---|
|Filter by tag key |Filtering by tag key alone returns all file systems where the specific tag key exists and the corresponding tag value may be any valid string. You can select multiple tag keys to view file systems that match any of the filtering conditions. Limiting tag keys but not tag values helps with fuzzy search scenarios. |* Filter example 1<br><br>   * Filter condition: Set the tag key `department` with an empty tag value.<br><br>   * Filter result: The result will include all FileNAS file systems containing the tag key `department`.<br><br>* Filter example 2<br><br>   * Filter criteria: Set the tag keys `department` and `owner` with no tag values.<br><br>   * Filter result: The result will include all FileNAS file systems containing the tag keys `department` or `owner`. |
|Filter by tag key + tag value |Specifying both tag keys and tag values displays all file systems bound to those tags. You can select multiple tags to view file systems that match any of the filtering conditions. Filtering by both tag key and tag value is effective for precise search operations. |* Filter example 1<br><br>   * Filter condition: Set the tag `department:game`.<br><br>   * Filter result: The result will include all FileNAS file systems containing the tag `department:game`.<br><br>* Filter example 2<br><br>   * Filter condition: Set the tags `department:game` and `owner:Ben`.<br><br>   * Filter result: The result will include all FileNAS file systems containing the tag `department:game` or `owner:Ben`. |
