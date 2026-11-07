---
title: "Private Segment Management"
product: "BytePlus CDP"
product_code: "cdp"
source: "https://docs.byteplus.com/en/docs/cdp/Private_Segment_Management"
---

<span id="_1-产品概述"></span>
# **1. Product Overview**

In actual business scenarios, it is usually desired to accurately and quickly implement user segmentation through tags and user details/behaviors data to meet diverse analysis and operational needs.

In this module, users focus on creating and managing segment, as well as performing more operations based on the crowd. In this section, we will provide detailed operational instructions combined with application scenarios in actual business operations.

<span id="60b50f7f"></span>
# **2. Operation Steps**

<span id="d9b1882c"></span>
## 2.1 Manage Segment List Page

Click the "Edit Columns" button on the right to edit and manage the fields displayed on the group list page:


* Check the field names that need to be displayed, click OK, and the content displayed on the list will be updated

* Click "Restore Default" to only select the fields displayed by default. Click OK to restore the default state.


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/b3b8da697d9546748786f45fdea9d1cd~tplv-goo7wpa0wc-image.image) </span>

<span id="c2d6fd1f"></span>
## 2.2 View Segment List


1. You can quickly find the target audience package on the segment list page through filtering, searching, and other methods:

* Enter the segment name or creator in the search box to quickly locate the specific audience package.

* Checking "Created by me" quickly filters out the audience packages created by me.


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/d735d414438d446fa9eba759c0596038~tplv-goo7wpa0wc-image.image) </span>


2. You can search for segment package IDs, filter ID types, encryption methods, segment quantities, groups, states, affiliated entities, update methods, segment types, data expiration TTL, creation channels, etc...


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/c8759433ce7e4ca6a7bd2decf5674a57~tplv-goo7wpa0wc-image.image) </span>

In the user segmentation module, **group filtering supports filtering "belonging to any/belonging to all groups" segments (similar to the logic of "and/or"):** 


* **Belonging to any group**: When filtering multiple groups, as long as users belong to any of these groups, they can be selected.

* **Belonging to all groups**: When filtering multiple groups, only when users belong to all specified groups at the same time can they be selected.


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/51959072dbc44ea6b29b373d7545583b~tplv-goo7wpa0wc-image.image) </span>


3. Click on the segment package name to view detailed information about the segment.


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/e376967e3ccc431c818dc852346477ea~tplv-goo7wpa0wc-image.image) </span>


4. Click on the number of segments to view the running records, historical performance, and trends of the segments, helping users to promptly understand the latest status of segment tasks.


<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_d71a22936ed7ec76ecea84d4ce17fd1f.png) </span>

<span id="857f71a1"></span>
## 2.3 Manage Groups

Private domain segments support grouping, helping users to label and organize segments, and quickly filter effective information.


1. Click the **Manage Groups** button on the segmented list page.


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/af8b7bfda8f14117a7164348311e8a1c~tplv-goo7wpa0wc-image.image) </span>


2. The user segment group management page displays information on all existing groups currently.


<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_4c199eacc1b4c3be3b02672528bdb6c3.png) </span>


* Project creators and administrators have the authority to delete and edit groups. Project administrators can grant users group management permissions in the project center's authorization module.


<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_e97df6a22e76726897b3c9b6f4dec9bd.png) </span>


* Once a group is created, it can be used by all members under the project.

* A segment allows multiple groups.

* Subpackages inherit groups from parent packages, and do not support modifying groups in subpackages.


<span id="c3b1930b"></span>
## 2.4 Segment Application

In the segmentation application section, support pushing segments to other products, understanding segment insights, and knowing the application scenarios of segments across various channels:

<span id="d4124f39"></span>
### 2.4.1 Private Domain Audience Profiling

Click "Analytical Insights \- Private Domain Audience Profiling" to jump to the "User Insights" module for a deeper understanding of the current segment package's profile and significant features.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/3ccf3f95c0fe4c2eb5a96b662751e0a3~tplv-goo7wpa0wc-image.image) </span>

<span id="ab6fc9b8"></span>
### 2.4.2 GMP Reach Task

Note: Only customers who have simultaneously deployed CDP and GMP can use this function.

In the CDP "User Segmentation" list, each segment can choose "More Applications" \- "GMP Reach Tasks." Clicking will directly jump to the GMP Reach Tasks page, automatically selecting the segment. Operators can directly use this as a basis to complete other information for the reach task.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/086fed859e894defb949157a0c737131~tplv-goo7wpa0wc-image.image) </span>

<span id="005ad5c5"></span>
## 2.5 Segmentation Management

In the more operations of user packets, support various operations and management of user packets, including the following:

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/f3f3cb808cc44ead91b54493978dffb0~tplv-goo7wpa0wc-image.image) </span>

<span id="a539e86c"></span>
### 2.5.1 Free Analysis

Note: This function can only be used by customers who have purchased both the Customer Data Platform (CDP) and Intelligent Data Insights(ABI), and have the right to use it. Click "..." \- "Free Analysis" to enter this feature.

<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_ea7b5a7d86e729525f58905853060195.png) </span>

When switching to Intelligent Data Insight Visualization Query, automatically select the current group as filtering criteria, focusing on in\-depth analysis of the crowd.

<span>![图片](https://lf6-volc-editor.volccdn.com/obj/volcfe/sop-public/upload_216ba8042e23863b7723a481251df96d) </span>

<span id="905b66e8"></span>
### 2.5.2 Experiment Creation

Click "Segment Application\-Experiment Creation" to support pushing the groups in CDP to A/B testing for creating experiments.

**Attention:**  When users have deployed both Customer Data Platform and A/B Testing at the same time and have permission to use them, they can use this feature.

<span id="9b4f0a34"></span>
### 2.5.3 Download Group Package

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/0e119b08325d4f26a9157698fe22ba4c~tplv-goo7wpa0wc-image.image) </span>

Private domain segment are available for download, including two types of data:


* Download ID list

   * Click the Download ID List button, choose a specific file format, support: .txt, .csv, .gz

   * For the mobile ID\-generated group package, users can choose to download data encrypted or unencrypted.


**Attention:** 

To enable the download of segment files, go to Project Center\>Permissions\>Modules to enable the download grouping file permission.

<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_2fde0067166fbc769edeaec8005eec54.png) </span>


* If the download of segment files needs to be encrypted, please encrypt the information and configure the strategy in "Project Center\-Privacy and Security\-Data Encryption", refer to: [Data Encryption](https://www.volcengine.com/docs/6356/1108537)


<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_a4991c25d5d4496ba8950f00582e9b54.png) </span>


* If the download of segment files requires data desensitization, please configure it in "Project Center"\-"Privacy and Security"\-"Data Desensitization", refer to [Data Desensitization](https://www.volcengine.com/docs/6356/434788) (This function is an additional purchase feature)


<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_4b1c935ce1145edd932d0b3790fcdd94.png) </span>


* The encryption and desensitization strategies are executed based on the priority of the output encryption, project data encryption, and privacy data desensitization strategies when creating segment files. If all three strategies are configured simultaneously, only the output encryption strategy when creating will be executed.


When creating a group, if the ID type is stored encrypted and another encryption algorithm is chosen for output, **the system supports decryption before encryption**.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">Prior to the ID encryption and decryption information registration, it is necessary to complete the encryption and decryption process in the <strong>privacy security module</strong>.</div>



<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_94786c022702fbb50058c0f5638e6317.png) </span>

<span id="e7018ec3"></span>
### 2.5.4 Update Segment Files

Supports **batch update of** **Segment files,**  click to update segment files, and manually update the conditions of the group to the latest data.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/df12490705bb4bf1ac9e118bda150c23~tplv-goo7wpa0wc-image.image) </span>

<span id="d18e8858"></span>
### 2.5.5 Copy Segment Files

Supports copying existing audience groups, but currently only supports the copy of audience groups created with tag rules.

<span id="b1b956a5"></span>
### 2.5.6 Modify Group

Support modifying the group in which the group package is located, and multiple groups can be selected for the group

<span id="60c2eff5"></span>
### 2.5.7 Group Package Authorization

Project administrators and group creators can quickly authorize the current group to others through the operation bar. The authorized person will have group viewing permissions.

<span id="b5e338cd"></span>
### 2.5.8 Service Configuration

Support quick enabling of online API services through service configuration, making it easier to call audience packages in other systems.

<span id="0ad67054"></span>
### 2.5.9 TTL Configuration

TTL configuration supports configuring the data lifecycle for individual groups, including the number of retained versions of the group data. Any historical versions exceeding the limit will be deleted the next day.

<span id="16524ce1"></span>
### 2.5.10 Unpack

Random unpack supports choosing from 3 methods:


1. Limit the number of sub\-packages. Support configuring the maximum number of sub\-packages for splitting

2. Limit the number of packages. Support configuring the number of sub\-packages to be split, which will be evenly divided according to the set number

3. Split packages by proportion. Support configuring the proportion of the number of sub\-packages to the total number, and split according to the proportion


<div style="text-align: center">
<img src="https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_4999405d8720afcbf83cd4d200af5ad3.png" width="2878px" /></div>


After configuration, click the small triangle icon in front of the crowd package to expand and see the sub\-packages.

<div style="text-align: center">
<img src="https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_7048ff96c93028777d061bc1bdb214dc.png" width="2878px" /></div>


<span id="7c0b5223"></span>
### 2.5.11 Delete the audience package

Support deleting the selected audience package. Users can only delete audience packages they created, while administrators can delete all audience packages

<span id="fd790182"></span>
## 2.6 Batch Operation

Batch operations support batch editing of audience packages, including deletion, authorization, and group modification, etc.

Check the target audience package and select the specific batch operation needed below

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/f025ffc7c1d9422985a6d1f488fc8f17~tplv-goo7wpa0wc-image.image) </span>


* Batch Delete

   * Tick the box and click on batch delete—force delete.

* Batch Authorization

   * Select batch authorization after checking, select the authorization object, and confirm to proceed.

* Batch Management Group

   * After selecting, click "Batch Grouping", select the group to be added, then confirm (currently only support selecting 1 group).
