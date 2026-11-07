---
title: "Label Details Page"
product: "BytePlus CDP"
product_code: "cdp"
source: "https://docs.byteplus.com/en/docs/cdp/Label_Details_Page"
---

<span id="_1-功能概述"></span>
# 1. Function Overview

In the tag details page, users can view tag information, including the tag's name, description, update method, basic information such as tag distribution, historical details, tag creation rules, and assignment logic, helping users to have a detailed understanding of the tag situation.

<span id="e9631ba4"></span>
# 2. Usage Restrictions


1. Project administrators need to enable the labeling system module permission for corresponding users in project center\-permissions. Once activated, users can utilize this function.

2. Users need to complete preparatory work in the **Data Fusion** module and create corresponding tags before using this function.


<span id="90267003"></span>
# 3. Operation Steps

<span id="8698ac4c"></span>
## 3.1 View Tag Basic Information


1. Click on the corresponding tag, and you can view basic tag information at the **top of the details page**.

   * **Tag Name**: Label Name.

   * **Collect**: Click to collect/cancel the tag.

   * **Creator**: Display information about the tag's creator.

   * **Creation Time/Last Update Time**: The tag's last edit time. If no modifications are made, the tag creation time is displayed.

   * **Update Method**: The tag's update method, categorized into offline update and real\-time update.

   * **Update Frequency**: Displays the update frequency of the tag, daily/weekly/monthly.

   * **Creation Method**: Displays the tag's creation type, such as rule tags, SQL tags, etc.

   * **Value Type**: Displays the data type of the tag value, such as text type.

   * **TTL Retention Period**: The validity period for retaining tag calculation results, divided into "Unlimited" and "Specified Duration."

   * **Online Service Switch**: Displays on or off. If open, it means the tag can be called for online services.

   * **Tag Description**: Shows the label description text entered when creating the tag.

2. Click the **edit** button in the upper right corner to enter the tag editing page and modify tag information.


<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">Only users with project editing or project management permissions have the authority to edit tags.</div>


<span id="794e6ccd"></span>
## **3.2 View Tag Distribution**


1. In the **Tag Distribution** card, users can view the distribution and proportion of tag values under the current tag, showing the total number and coverage rate, with the benchmark time as the data time.

2. Clicking **Save as Cluster** allows for quickly creating population rules corresponding to tag values, facilitating the conversion from tags to populations.

3. Clicking **View Individual Details** can navigate to the individual portrait list page, filtering out the corresponding population lists based on conditions.


**Calculation Basis for Tag Coverage:** 

Note: mautag = total id count under the current entity in the system.


|**Indicator** |**Indicator Definition** |**Calculation Method** |**Application Scenarios** |
|---|---|---|---|
|Effective Tag Coverage:<br><br>All Users = Latest Mautag Data<br><br>Total Number of IDs under the Current Subject in the System |Number of Users Tagged with This Label among All Users (under the Latest Mautag)<br><br>Not Affected by Row Permissions |Numerator: Tag Partition after Mautag \* Ready Label on this day<br><br>Denominator: Tag on this day Mautag |1. Tag System \- Tag Distribution<br><br>2. Label Management List<br><br>3. lookalike feature selection<br><br>4. Project Center \- Asset Valuation |
|Effective Tag Distribution:<br><br>All Users = Latest Data of Mautag |Among all users (under the latest data of Mautag), the distribution of different values of this tag;<br><br>Subject to Permission Restrictions |Numerator: The value of this tag in the tag partition after mautag \* c is ready on b that day<br><br>Denominator: The tag partition after mautag \* c is ready on b that day |Labeling System \- Tag Distribution |
|Tag Coverage on a Specific Date:<br><br>On the specified date, the total number of users = mautag on the specified date |When a = b, the statistical date is under the partition updated with mautag. The ratio of users with this label to the total number of users;<br><br>Not affected by row permissions |Numerator: On the statistical date a, after mautag\*c is ready, label partitions<br><br>Denominator: On date b, mautag |1. Label System \- Historical Details<br><br>2. Asset Valuation Assessment \- Historical Trends |
|Label distribution on the specified date:<br><br>On the specified date, the total number of users = mautag on the specified date |When a=b, the statistical date is under the partition updated by mautag.<br><br>The distribution of the tag values;<br><br>Affected by row permissions |Numerator: The value of this tag in the partition after the mautag*c\-ready label on statistical day a*<br><br>*Denominator: The partition after the mautag*c\-ready label on statistical day a |Label System \- Historical Details |


<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_c42ba80fbc3d66ab63174c1222d46425.png) </span>

The statistics for tag coverage numbers and rates will be calculated and displayed based on total data, unaffected by data permissions.

<span id="6a15ca96"></span>
## 3.3 Sort Labels

Label sorting can be set to sort tags by **ascending tag values**, **descending tag values**, **ascending tag coverage counts**, **descending tag coverage counts**, or **custom sorting**.

**Ascending/Descending tag values**: Sorted by Pinyin/English initials.

**Ascending/Descending tag coverage counts**: Sorted by the proportion of the tag value within the user range covered by the tag.

**Custom sorting**: Allows custom arrangement of tag orders.

**Authorization:**  Users need "edit" permission for that tag to operate the sorting button, with the time filter defaulting to showing historical details for a specific period.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/9a658af20c4649aaa3f581f734033c94~tplv-goo7wpa0wc-image.image) </span>

In the tag distribution view, you can customize the number of tags displayed, with a maximum recommended value of 100, making it easier for users to adjust the display quantity when there are too many enumerated values, enhancing user experience.

> Notice\*: The maximum number of tag values that can be displayed is supported only after the project administrator configures it in "Project Center\-Group Configuration\-Tag Value Maximum Display Quantity", allowing users to use it.

> <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/69c2cbc8cbda4c79866722177303e661~tplv-goo7wpa0wc-image.image) </span>


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/ecc46ebe9372443f96b9e8c985bbbfca~tplv-goo7wpa0wc-image.image) </span>

<span id="a59a94e2"></span>
## **3.4 View Label History Details**


1. In the **Label History Details** card, users can view the total number of tag coverages and the historical distribution of coverage numbers for each tag value within a specific time period.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">It contains related switch controls. After the switch is turned on, different users may see different data for the same tag under the same project. If there are switch requirements, please contact BytePlus's business personnel.</div>



2. Click on the upper right corner **time** filter box, users can display tag historical details by day, week, or month, or customize time selection to filter and observe the corresponding tag change trends (note: <ins>the calculation of historical period results will use the latest day's enumeration values for statistics</ins>).

   Reason for explanation:

* This counts the results based on the latest day tag enumeration, restoring the results of the past 7 days.

* For the same tag, the results of different user queries are different: affected by row\-level data permissions (for example: only departments 1, 2, 3 can query customer data responsible for their own departments), the statistical results are calculated based on the distribution of tag values calculated by the IDs that users have permission to.

* The chart represents the results of each user's queries on the day (can be cached if the tag value sorting, query time range, and tag ID remain unchanged)

3. By clicking on the tag value for a specific day, you can quickly create corresponding audience rules by **saving as a segment**, making it easier to convert tags to audiences.


<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_4041ebe09e6d440f1c7c3865c3831426.png) </span>

<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_12d74b863081ce232f48a15cd0741d9d.png) </span>

<span id="e58d6ef4"></span>
## 3.5 View tag creation rules

Display the creation rules for the current tag.

<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_47b7cdf7a574a25fce1d6980866c4979.png) </span>

<span id="439b1702"></span>
## 3.6 Label Execution Log


1. Click **Run Record**.

2. On the **Operation Records** page, users can view the detailed operation records of the current tag within a certain period, including dates, operation status, duration, etc.

3. Users can individually or in batches select operation tasks to perform **rerun/stop operations**.

4. For tasks that fail to run, users can **view the operation** and **operation view**.


<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_de3a0f636f70d322bf13d5ea5b116d95.png) </span>


5. Tag operation tasks support **manual refresh**, but only users with IDMapping administrator configuration permissions can operate.


<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/ab4f404c60d5440db48bad8983e7da17~tplv-goo7wpa0wc-image.image" width="2580px" /></div>


<span id="a91cc4ba"></span>
## 3.7 Tag Authorization

**Usage Restrictions**: This feature is only available for Tag Resource Administrators, Project Administrators, and System Administrators.

The authorization steps are as follows:


1. Click on the **Authorize** button in the top right corner.

2. Users can search for authorized objects, grant permissions to the current tag, including viewing, editing, management permissions, and remove user permissions for the current tag.



|Tag permission |Functional Details Provided |
|---|---|
|View Tags |View tag details & operation records, you can use this tag to create tags, grouping circle selection, image insights, operation records \- running/stopping/batch running/batch stopping capabilities |
|Label Edit |On top of view permissions, the following capabilities are also available:<br><br><br>* Edit<br><br>* Rename/Copy from the left\-side tree<br><br>* Publish tags<br><br>* Upload manual tag values for individual profiles<br><br>* Upload data for manual tags |
|Label Management |On the basis of editing permissions, it also has the ability to authorize labels and delete labels. |


<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_a2f5fc191cc7b633f3c5b2982c4fcc5b.png) </span>

<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_6c4d18b4c1f98d5550709ddfd944b789.png) </span>

<span id="0ca584ca"></span>
## 3.8 Tag Lineage

Click on the "Tag Lineage" tab to view the upstream and downstream dependency relationships of the tag (each showing up to 7 layers).


* You can switch between graph or list views

* You can limit upstream/downstream dependencies

* You can filter dependencies by asset type (data source, tag, group)

* Click the "Download" button to download lineage tables in different formats


<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_cfd8db9d6dbf7f22afa3d9818a143aab.png) </span>

<span id="318f6811"></span>
## 3.9 Tag Valuation

Click on the "Valuation" tab to view tag frequency statistics and tag performance\-related metrics


* A single dimension card can display statistics for the past 7 or 30 days

* Days since last use: number of days since the last use of the current tag

* Total internal uses: number of times the current tag has been referenced or queried internally (CDP platform modules) such as tags/clusters/analytical insights

   * Reference: Establishes upstream and downstream dependencies with this tag, such as creating a group based on this tag.

   * Query: Searched for this tag in CDP, not necessarily establishing upstream and downstream dependencies.

* Total Calls from Other Platforms: The number of times this tag is called by external platform systems, such as ABI/GMP/finder and API interfaces, etc.


<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_55567811a2c227f16a760a363021c524.png) </span>

<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_4ae94543be35acd592f752025957f0cc.png) </span>

<span id="7224f855"></span>
## 3.10 Historical Operations Record

Click the 'Historical Operations Record' tab to view the historical **operation time**, **operator**, **operational point**, and **specific content** of this tag.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/f8fa895e917b4117a35f012894b36edb~tplv-goo7wpa0wc-image.image) </span>

After changing the 'Tag Calculation Rules', you can check the 'comparison before and after the changes', click 'Restore Rules and Rerun' to restore the content before the changes.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/f2ce2472069a4fb0b83394d341e88752~tplv-goo7wpa0wc-image.image) </span>

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/2d05ce2c18bc4c01a42327aaca855013~tplv-goo7wpa0wc-image.image) </span>
