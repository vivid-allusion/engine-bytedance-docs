---
title: "Label Management"
product: "BytePlus CDP"
product_code: "cdp"
source: "https://docs.byteplus.com/en/docs/cdp/Label_Management"
---

<span id="_1-产品概述"></span>
# 1. **Product Overview**

Label Management supports viewing and managing the current operational tasks of labels from a task perspective. It also allows focusing on key content that roles need to pay attention to through view configuration to enhance label management efficiency.

<span id="d5222bb2"></span>
# 2. **Feature Introduction**

Click on **Labeling System \-\> Label Management** in the navigation bar to access this feature.

By filtering and searching, you can view specific operational tasks of labels, manage specific labels and operational tasks, and download complete content. The label management team can analyze, summarize, and inspect files.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/09876cee187b4a318a6cd1732b91d9a0~tplv-goo7wpa0wc-image.image) </span>

<span id="8d38f9be"></span>
# 3. **Usage Restrictions**

Project administrators need to enable the corresponding users to have the permission to View Label Tasks in Project Cen**View Label Tasks in Project Center\-Permissions\-Modules**. Once enabled, users can utilize this function.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/a0034bca82e34afb91caae2272e7737b~tplv-goo7wpa0wc-image.image) </span>

<span id="6c9b031d"></span>
# 4. Function Description

<span id="89e5ef0e"></span>
## 4.1 **Label Filtering and Search**

On the left side of the tag management page, the tag management list supports **multiple selections,**  which enables tag searching through tag directory categorization, or searching for target tags by tag name or creator; it also allows filtering tags based on specific creation methods to view corresponding tag tasks; the test search bar under custom view supports **retrieving custom fields,**  improving search efficiency.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/320f45830f9a4240845457d125464689~tplv-goo7wpa0wc-image.image) </span>

<span id="8025ae18"></span>
## 4.2 Label Management

On the right side of the page, you can view an overview of the tag tasks, including tag name, ID, creation method, tag value type, shelf status, etc.


1. You can switch at the top to view tags in different activity states, including: listed, unlisted, draft tags.

2. You can switch at the top to view tags in different operation states, including: running, successful, failed, waiting, ready, others.

> Attention\*: The three states of successful operation, failed operation, and waiting do not participate in **manual tags, real\-time tags** statistics. Manual tags, real\-time tags are automatically classified under the "Others" state.


Operations supported in tag management:


| |Operation Instructions |
|---|---|
|Modify Tag Name |Click on the **edit** button next to the tag name to modify the tag name |
|View Execution Records |Click on **Execution Records** button to jump to the corresponding label's execution records page and check the detailed information of the execution task |
|Manually Update Task |Click on **Update** button, select the date range to be executed in the pop\-up box, click OK to trigger the task update |
|Copy Label |For label types that support copying, you can click the **Copy** button to duplicate a label |
|Label Authorization |For labels with management authorization, click **Authorize to** button to grant authorization to other objects |
|View Resource Managers |Click on **View Resource Managers** button to view the current resource managers for that label |
|On\-Shelf Tags |For **on\-Shelf/draft** status tags, click the **On\-Shelf Tags** button to trigger the update task for the tags |
|Off\-Shelf Tags |For tags in off\-Shelfstatus, click the **Off\-Shelf Tags** button to stop the task execution |
|Service Configuration |For tags that require online calls, you can toggle the service configuration switch |
|Delete Tags |For tags with management permissions, click the 'Delete' button to delete the tags |


<span id="6120fa89"></span>
## 4.3 Batch Operations

Batch operations supported in tag management include the following:


| |Operation Instructions |Illustration |
|---|---|---|
|Batch Shelf Management |1. You need to first go to **Project Center\-Permissions\-Modules** to enable the **Tag Shelf Management** permission for the corresponding user to use this feature.<br><br>2. Check the tags that need to be shelved, and click the **Batch Shelf/Management** button. |<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_f3c106648169288582180da3cd2ea790.png) </span> |
|Move Groups |1. Check the tags that need to be regrouped, and click the **Move Groups** button.<br><br>2. Select the group you want to move to, and click the **Confirm** button. |<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_098b864c7d9f14f9825fc14fe882538d.png) </span> |
|Rename |1. Check the tags that need to be renamed, and click the **Rename** button.<br><br>2. Download the template provided by the system.<br><br>3. Open the template, enter a new name (Note: Do not modify the tag ID and original name).<br><br>4. After completing the document upload, click save, and the system will rename in batches |<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_a540be32d4ac0a52f172af1b49bdc73e.png) </span> |
|Batch Authorization |1. Need to have the label\-resource administrator permissions<br><br>2. Check the tags that need authorization, click **Batch Authorization**, to proceed with the authorization |<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_7d2b79d84445a043c80e6bf7fa91ba67.png) </span> |
|Modify Metadata |1. Choose the "metadata field" to be modified, supplement the corresponding label descriptions after downloading the template, and then upload to batch upload label descriptions.<br><br>2. Users with **label resource editing permissions** can perform this operation |<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/f4887c29bfa840468dcb903b5787ac26~tplv-goo7wpa0wc-image.image) </span><br><br><span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/be9544c5cb494a7fb3944e7f67a55a94~tplv-goo7wpa0wc-image.image) </span> |
|Batch Display/Hide |1. Configure first in "Project Center\-Group Configuration\-Tag Control Display Switch" and only project administrators can operate.<br><br>2. Check the tags that need to be displayed/hidden, click **Batch Display/Hide** button |<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/0ba6f7493b0b47d798b6159268ea489b~tplv-goo7wpa0wc-image.image) </span><br><br><span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/d132132ca6bf43268f54c67561185142~tplv-goo7wpa0wc-image.image) </span> |
|Pager magnifier |Default 20 items/page, supports magnification to 100 items/page |<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_372e342fd8432a16206d75745eddaa41.png) </span> |


<span id="8e2194e8"></span>
## **4.4 Tag Synchronization**

In the tag management page, it supports batch synchronizing tags to other projects. After synchronization, the target project can directly use these tags in the user segmentation module, facilitating data sharing and collaboration across projects.

> \*Note: Real\-time tags, tags in unreleased/synchronized/draft states, etc., are temporarily not supported for synchronization.


Creating tag synchronization: On the tag management list page, check the tags that need to be synchronized to other projects, then click on the **synchronize to other projects** button and select the **project to synchronize to**.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/42a0d3a8e7694da7a0adea0088720846~tplv-goo7wpa0wc-image.image) </span>

Effective scenarios after synchronization: In the **target project \- user segmentation \- create segmentation** page, select tag data, and you will see the synchronized tags.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/a7f6ae142e1e4f50aa78545110c15d70~tplv-goo7wpa0wc-image.image) </span>

<span id="1efcec7e"></span>
## **4.5 File Download**

Content on the tag management page supports downloading for viewing. Click the **download** button at the top right to start downloading a CSV file containing details of the label tasks in the current filtered projects. This file can be used for local analysis and processing.

<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_d2dfe84eb9b59578a762a7f934632665.png) </span>

<span id="52bf27ec"></span>
## **4.6 View Selection**

The displayed content (columns) in the task overview can be switched through different views. Two views are configured by default:


* Operations View: This view includes 10 projects commonly used from an operational perspective. You can adjust the column order by dragging, and clicking reset restores the default configuration.

* Business View: Compared to the Operations View, the Business View has fewer contents, including 6 commonly used projects. You can adjust the column order by dragging, and clicking reset restores the default configuration.


At the same time, the view supports custom content, allowing you to save the required content as a custom view in the project. You can adjust the column order by dragging and clicking "Reset" to restore the default configuration.

<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_f4bf3dae6609a2ba5a6fa59cf5b3b576.png) </span>

<span id="c0da3a72"></span>
## 4.7 Metadata Management

Metadata refers to data that describes other data, typically used to provide information about data such as format, structure, content, and source. Metadata can help people better understand data and provide support for processing and analyzing data. CDP's labeling system supports the setting and application of label metadata.

**1) Create Label Metadata (Administrator)** 


1. Go to **Labeling System\>Label Management,**  click the **Metadata Management** button in the upper right corner to enter the management page.


<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_17b21c53bf65773cc816e36d62fed941.png) </span>


2. Click the **Create Label Metadata** button in the upper right corner, and configure the content of the label metadata in the pop\-up box. After configuration, this label metadata will take effect on label creation, editing, management lists, and label metadata APIs.

   1. Data Types: Support setting text, single\-choice, and multiple\-choice as three types.

   2. Required: support setting whether this metadata is a required field;


<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_b174f50959c9d55a56889c2e17986531.png) </span>

**2) Scenarios where the tag metadata takes effect**


|Scenario |Illustration |
|---|---|
|Create/Edit Tags |<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_25bf123bc2e65443cfde6b4714365124.png) </span> |
|Tag Management List |Prerequisite: Need to select a custom view in the operations view and check this metadata field<br><br><span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_17d1d077a915cee58a2ed1b317d937c1.png) </span><br><br><span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_d3bdd4e42df3da798ca78ef5811c461f.png) </span> |


<span id="630859eb"></span>
## 4.8 Tag Applied Configuration

In the tag metadata management page, you can configure the metadata field with enumerated values as selection scenarios downstream. When using tags in the current "By Tag Directory," "My Commonly Used," "My Favorites" sections, you can expand the quick filtering method to help users quickly locate the target tags.

> \*Note: Supports configuring up to 3 quick conditions at most.


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/5402e1a8b25542248e5c59b5e5b88b82~tplv-goo7wpa0wc-image.image) </span>

**Example Explanation:**  Taking "Data Collection Method" as an example of a quick filter condition, the configuration is as shown in the figure below:

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/d34dd3ef6fea41348d332bb4c13d1a49~tplv-goo7wpa0wc-image.image) </span>

Effective scenarios after configuration: In the user segmentation \- Create Rule Segmentation page, when selecting tag data sources, you can view the tag metadata that was configured just now, as shown in the figure below:

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/943f5a5f2f0e4d8d91366754fd0af548~tplv-goo7wpa0wc-image.image) </span>
