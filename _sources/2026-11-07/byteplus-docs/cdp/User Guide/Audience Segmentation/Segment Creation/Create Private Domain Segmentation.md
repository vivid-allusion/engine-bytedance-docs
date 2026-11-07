---
title: "Create Private Domain Segmentation"
product: "BytePlus CDP"
product_code: "cdp"
source: "https://docs.byteplus.com/en/docs/cdp/Create_Private_Domain_Segmentation"
---

<span id="_1-产品概述"></span>
# 1. Product Overview

Private domain segment function allows the creation of target segment packages with specific needs and a series of features through rule creation or data upload. After creating the target segment package, it can be used for insights or pushed to downstream marketing channels. It also supports viewing the workflow application details of the segment to achieve precise contact with the target customers.

<span id="6e9615d4"></span>
# 2. Feature Introduction

There are 2 ways to create private domain segments:


* Rule Creation: Supports the visual components to flexibly create segments using tags, behaviors, segment, detailed data, and user attribute data. It also supports setting cycles for automatic data updates.

* Upload Creation: Quickly create a target segmentation package in CDP by uploading local files.


<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_06988a864709acbff08fbff3df558089.png) </span>

<span id="e168f78c"></span>
# 3. Usage Constraints


* Project administrators need to enable the permission for corresponding users to manage the **Private Domain Segmentation \- Add/Delete/Modify Segmentation in Project Center\-Permissions**

* Project administrators need to grant corresponding users access to resources such as **Tags and Datasets in Project Center\-Permissions**

* Creating segment must be within the **Total Resource Quota**. When the resource quota is exhausted, users need to delete tags or segments to release resources before they can create new tags or contact their account manager to purchase additional computing resources.


<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_e47e143c280bb016885f779bd0217762.jpg) </span>

\***Attention: Only routine updates of tags and segments will consume resource quotas. The detailed consumption rules are as follows:** 


|**Resource Type** |**Resource Construction Method** |**Update Method** |||
|---|---|---|---|---|
|||**Manual Update** |**Regular Update** |**Real\-time Update** |
|Tag |Rule tag |Consumption |Consumption |Not consumed here according to real\-time resource restrictions |
||First and last tag |Consumption |Consumption ||
||Statistical tag |Consumption |Consumption ||
||Preference Tags |Consumption |Consumption ||
||Sorting Tags |Consumption |Consumption ||
||Operational Tags |Consumption |Consumption ||
||Lifecycle Labels |Consumption |Consumption ||
||RFM Labels |Consumption |Consumption |/ |
||SQL Labels |Consumption |Consumption |According to real\-time resource constraints, statistical consumption is not done here |
||Import Tags |/ |Consumption |/ |
||Manually Enter Tags |On Demand |/ |/ |
||Intelligent Outbound Call Tags |/ |Consumption |/ |
||Smart Listening Tag |/ |Consumption |/ |
||Custom Model Tags |Not Consumed |Not Consumed |/ |
|Segment |Segment Rules (Private Domain) |Not Consumed |Consumption |Based on real\-time resource constraints, statistics are not consumed here. |
||User Segment |Not Consumed |/ | |
||Private Domain Lookalike Create Audience |No consumption |/ | |
||Segment model generates audience |No consumption |/ | |
||Insight report exports audience |No consumption |/ | |
||Subject switching audience |No consumption |Consumption | |
||Multidimensional Feature Analysis Exported Audience |Not Consumed |/ | |
||Linkage Product Synchronous Audience (e.g., ABI/Finder Synchronous Audience) |Not Consumed |/ | |


<span id="858b4118"></span>
# 4. Operation Steps

<span id="24a6906d"></span>
## 4.1 Create Segment

Go to the **User Segmentation** module, click the **Create Private Domain Segmentation** button, and select **Create Segment Package\>Offline Segment Package**.

<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_35f0055dc62d100434e1dd1dc108aa32.png) </span>

<span id="ace20092"></span>
### 4.1.1 Rule Setting

Once you enter the configuration page, you need to create a rule first. Click **Add Condition** to configure specific rules.

<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_786ccef679ca2d5de7df51d86a19a124.png) </span>


|Category |Description |Example |
|---|---|---|
|Label |Keyword used to mark a certain feature, event, or status of a user |Tagging users who have visited the product detail page as interest users |
|Behavior |Data for analyzing user online behaviors, such as online behavior tracking |User visiting a specific page on the website |
|Audience Segment |User lists (user ID or device ID, etc.) generated based on specific rules or uploads |People who have placed orders selected through tags |
|Detailed Data |Other detailed data for business access |Such as orders, etc. |
|User data |Used to analyze user attributes |Such as constellations, gender, age, etc. |



* When using "tags" for selection, you can choose from the following rules:

   * Include: select users who have been tagged with this label and the tag value matches the option.

   * Exclude: users who have been tagged with this label and the tag value does not include the option.

   * Global exclude: exclude users with this tag value in the full user list (including users who have not been tagged with this label).

   * Empty: the tag value is empty, meaning users who have not been tagged with this label.

   * Not empty: the tag value is not empty, meaning users who have been tagged with this label (any tag value).

   * By using the filtering component, you can choose to use the tag data of a specific day, including historical sections.

* Example: If there are 100 total users, with 10 users tagged "Is Senior": 4 are "Yes", 5 are "No", and 1 is "Other", then:

   * Selecting "Is" in this tag includes 4 people.

   * Selecting "Is" not in this tag includes the other 6 people.

   * Selecting "Is" globally not in this tag includes 96 people.

* If the tag is numeric/decimal, support selecting the id of the before/after n items or the data of the before/after n entries

   * Before/after n item id: select n unique user ids

   * Before/after n data: select unique users from the top n data. For example, if the top 10 data entries are all generated by 3 users, then these 3 users will be selected in the end

* If the tag is text/multi\-text, support finding the tag values that meet the conditions through like or regular matching

   * like: conduct fuzzy search by replacing a keyword with a wildcard (% or _), where % represents a string of characters and _ represents a single character.

   * Regular matching: support fuzzy matching using regular expressions, which describe a pattern for string matching. Common syntax includes:

* **Wildcard**



|Character |Meaning |Example |
|---|---|---|
|. |Matches any single character |byte.plus matches byteplus and byte3plus |
|*  |Matches 0 or more preceding items |The default preceding item is the previous character. byte\*plus matches byteplus and bytecplus |
|*  |Used the same way as an asterisk, but the plus sign must match at least one preceding item |byte+lus matches bytelus, but not byteplus |
|? |Matches 0 or 1 preceding item |byte?nlus matches bytelus and byteplus |
|∣ |Perform "or" matching |a∣b matches a or b |



* **Anchor**



|Character |Meaning |Example |
|---|---|---|
|^ |Requires your data to be at the beginning of the field |^byteplus matches byteplus but not superbyteplus |
|$ |Your data should be at the end of the field. |When matched with byteplus$, it matches with byteplus but not with byteplusyes. |



* Add Segment Conditions:

   * By clicking the "Add Segment Conditions" button, you can add another rule segment, where specific rules can be added and combined with the existing condition segments using AND or OR

   * Rename support for condition segments to facilitate differentiation and understanding of different condition segment contents

* Click on "AND/OR" to switch rule logic;

   * AND: Tags, behaviors, detailed data, audience baks, etc., conditions take intersections

   * OR: Tags, behaviors, detailed data, audience packs, etc., conditions take unions

* ID Type:

   * Select the ID type of the output subject, such as baseline ID, mobile number, etc. Here, all ID types introduced in the ID graph construction can be selected from the drop\-down menu by users;

   * ID Quantity Estimation: After selecting specific audience rules, the estimated baseline ID quantity information will be displayed on the top right of the page;

      * Support the **real\-time trigger function** on this page. If turned on, the system will automatically estimate the number of segments; if turned off, users can manually estimate the quantity by clicking **Query**. (Administrators can, in [项目中心-集团设置](https://docs.byteplus.com/docs/undefined/66cd3eaa66e3df0303ac680e), set users' query methods)

      * If you need to view the quantity of other ID types, click **View More ID Types**. The page will display the estimated baseline ID quantity and comprehensive estimates of other ID types within the system for users to refer to and make adjustments based on the estimated values.

* Encryption method: Supports setting ID encryption, such as SHA256 encryption. Please note that the encrypted audience package cannot be used on platforms like GMP, etc.

* Sampling results: Support random sampling by users and setting a reserve number. After setting, the quantity of the resulting audience package will be the same as the reserve number. Furthermore, when other segment refer to this audience package, the random results will prevail (when the sampling data set value \> actual value, the actual value will be used);


<span id="764354d1"></span>
### 4.1.2 Basic Information Settings

<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_b05d6bc8285f0c00141a2e26d5cb43c7.png) </span>

<span id="9e8238d6"></span>
### 4.1.3 Task Configuration

Segments created by rule creation can choose two update methods:


* On\-demand update: After creation, you can choose one\-time updates (manually trigger the audience package update according to requirements) or set scheduled updates (supports setting 10 scheduled updates).

* Update daily: After creation, you can set the execution time for each day, automatically updating the data in the audience package daily. Daily updates support "specified effective update period" and can specify a **start date** and **end date**.


<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/44a7948caf6b4c7da9c05304fd3b69cc~tplv-goo7wpa0wc-image.image" width="703px" /></div>


When selecting daily updates, you need to configure the execution time and upstream data task dependencies:


* Execution time: Mandatory field, can be selected down to the minute.

* Upstream data tasks depend on



| |Detailed Explanation |Schematic diagram |
|---|---|---|
|Recommended Configuration |System administrators can configure system recommendations in Project Center\>Segment Settings\>Feature Configuration[分群推荐依赖类型](https://docs.byteplus.com/docs/undefined/66cd3eaa66e3df0303ac680e#_3-2-%E5%88%86%E7%BE%A4%E6%8E%A8%E8%8D%90%E4%BE%9D%E8%B5%96%E7%B1%BB%E5%9E%8B). |<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_b05857335eb5aa3ca1fcec62db110788.png) </span> |
|Custom Configuration |Users can select custom configuration dependent projects, which take effect for this segment only when all dependencies are ready before tasks can be executed.<br><br>> Dependency on ID means that the segment will start updating only after the ID tasks for that day are ready.<br><br>> If the current segment rule depends on updates by week or month from the upstream, there is currently no dependency established. The daily updated segment package will use the latest data partition from the upstream that has data. |<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_4ac5785a178dc88c6fba611f5f684f89.png) </span> |



* Storage rule for calculation results: Users can set the number of historical versions to retain and any versions exceeding this limit will be deleted the next day.


<span id="01597bbe"></span>
## 4.2 Creating and Using the Segment Template

Segment rules can be created in two templates and support quick creation using templates.

<span id="af1a7c76"></span>
### 4.2.1 Personal Template


1. 


<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_dfe08baf397c25e1ed51d508864c24d2.png) </span>

After creating common rules, click the "Save as Template" button, enter the template name and description in the pop\-up box, click OK to save. Only the creator can use personal templates.


2. Create rules to support segment functions **excluding features**, enabling users to quickly filter out segments of people who do not belong. Both the "satisfy" and "exclude" components are arranged at the same level. That is, **matching condition A and excluding condition A**.

   After entering the segment creation interface, you can perform conditional filtering. Segment characteristics created by the case picture conditions: **Interacted with the** **mini\-app in the last 1 day** and **did not invite friends to share**.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_4d4513767f3292d32b49bd30005dde36.png) </span>


<span id="da8fb332"></span>
### 4.2.2 System Template

System administrators can configure segment templates for members to share within the project center.

Go to the project center \- function configuration \- segment system template configuration, click on "Create Template", set specific rules, click "OK" to save.

<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_9cfadb9217de7aab614c9aa8aa15c2a9.png) </span>

<span id="0e7d3d60"></span>
### 4.2.3 Create Audience Package Using Template

In the configuration creation page, click on "Switch Template" to view the system\-shared templates and personal templates. Click on the required template \- confirm, to quickly start creating an audience package with corresponding rules.

<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_b0c6d9a122f04d41b8fd66e215f372bd.png) </span>

<span id="84bfa001"></span>
## **4.3 Upload Audience Package**

Click **Segmentation\> Create Private Domain Segmentation**, select **Upload Segmentation Package**. Supports two ways of upload: "Upload Segmentation" and "Advanced Manual Segmentation".

<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_91c0401adaa04ee276ba5df5e6c25bbc.png) </span>

<span id="73d8f122"></span>
### **4.3.1 Upload Segmentation**


1. Click on **the original "Upload Segments"** , choose the corresponding subject, and click **OK** to enter the configuration page.

2. **Create rules**

* Enter the ID type: Select the corresponding ID type in the uploaded file.

* Generate ID type: Convert the ID type in the file and choose the type needed for final use.

   * For example, if the uploaded ID is user ID and you need to generate a device ID segment, select user ID in the ID type entry and device ID in the generated ID type entry.

* ID matching strategy: Choose between matching all users and allowing incremental OneID for unmatched IDs. If neither is selected, the system will only deduplicate the uploaded segment IDs (which will prevent insights and can only be used for pushing to other platforms).

   * Match all users: Match the uploaded segment with all users, save the matched results as segmented users, and exclude unmatched users (which may affect push or insight effectiveness).

   * Allow incremental OneID for unmatched IDs (this is not a default feature and needs to be enabled during deployment if required): If the uploaded segment doesn't match the system's ID mapping, the unmatched users will be added to the ID graph.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Unmatched ID allows for the incremental preparation of OneID: users need to go to <strong>ID Graph Construction</strong> module, and in real\-time OneID strategy generation strategy section, add the real\-time data reporting channel for <strong>segment upload</strong>.</div>


<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_37d1b6153533563910c5976707a8692b.jpg) </span>


* Add file: Upload a local file in txt or csv format, up to 1G in size. By clicking on "Download Template," you can understand the file format requirements. Please upload the file according to the template to avoid errors.

3. **Configure basic information.** 

* Fill in the audience package name, configure the audience's authorization object and segment, and support adding sub\-segment descriptions.


<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_1d421c87c975d79627f2d30580fcf390.png) </span>

4. **Modify the uploaded audience package.** 


* After the audience package is successfully uploaded, click on the audience package name to view the audience package details.

* Click the "Edit Details" button. In the audience package source file location, you can upload a new file to **overwrite and update** the original data.

* Click **Save** to complete the modification.


<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_a8ab6b1d01abc13c18a3061fecbcdca0.gif) </span>

<span id="344f89fc"></span>
### 4.3.2 Advanced manual segmentation (additional paid feature).


1. Click **Advanced manual segmentation**, select the corresponding subject, then click **Confirm** to enter the configuration page.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_740c94c3b82d8a9007fc74c7b9725ba2.png) </span>

2. **Create rules**

* Enter ID Type: Select the corresponding ID type in the uploaded file.

* Generating ID types: Supports conversion of ID types in files, and the generated ID type can be selected for final use

   * For example: If the user ID is uploaded and the audience package that needs to generate the device ID, then select the user ID in the input ID type position and select the device ID in the generated ID type position

* Match all users:

   * If selected, the uploaded audience package will be matched with all users, and the matching results will be retained as segmented users (users that are not matched will be excluded, and push/insight may be affected);

* By clicking on "Download Template," you can learn about the format requirements of the file. Please upload the file following the template to avoid errors;


<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_3bb58fd657056ce0a59f68b65eaacc87.png) </span>

**3.Configure basic information**


* Fill in the segment name, which can configure the crowd's authorization objects and segment, and support adding sub\-segment descriptions.


<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_608d95c5776a678c4f2e0faccf30c1d6.png) </span>

**4.Edit the uploaded advanced manual segmentation**


* After the segment is uploaded successfully, click on the segment name to view the details of the segment.

* Click the "Edit Details" button to change the location of the segmented package and support **replace all original segment IDs, append segment IDs, remove segment IDs**.

* Click **Save** to complete the modifications.


<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_8e00894bc1ff74a69ef4bd32fea77498.png) </span>

<span id="d0cf83f6"></span>
## Appendix:


|Steps |Features |Upload segment<br><br>(Supports only cover updates, cannot be updated in api creation) ||Advanced manual segment<br><br>(Supports append, remove, update via api) ||
|---|---|---|---|---|---|
|||**Initial creation** |**Edit existing** segment |**First Time Creation** |**Edit Existing Segments** |
|Create Segment Rules |Enter ID Type |√ |√ |√ |Only support overlays |
||Upload plaintext to encrypt for users<br><br>> IDs in the system are encrypted; enter the key |√ |√ |Unsupported<br><br>ck function is not supported |Not supported |
||Generation ID Type |√ |√ |√ |Only when covering the change ID is allowed to be modified |
||Upload file |√ |√ |√ |√ |
||Match all users |When the input ID type and output ID type are different, it must be turned on |When inputting ID type and output ID type, it must be turned on<br><br>When editing \- selecting an existing audience package is inconsistent with the current input ID type, it must be turned on |Not support using the original ID<br><br>*Only open, cannot close* |Not supported |
||Efficient upload |/ |View status support |/ |Viewing mode is not supported |
||Api creates audience |√ |/ |√ |/ |
|Changing the way of ID |Coverage |/ |Upload file |/ |* View Mode \- Download Recently Uploaded Files<br><br>* Upload File<br><br>> When editing, if an existing user segment package with a different ID type is selected, it needs to be converted to baseID.<br><br><br>* Select an existing user segment package |
||Append |/ |Not supported |/ ||
||Remove |/ |Not supported |/ ||
||Changes were made to the original audience package in the API. |/ |Not supported |/ |√ |
|Advanced Configuration |Update daily |√1.21 |√1.21 |Not supported |Not supported |
|Metadata |Name |√ |√ |√ |√ |
||Authorization |√ |√ |√ |√ |
||Description |√ |√ |√ |√ |
||Partition |√ |√ |√ |√ |
