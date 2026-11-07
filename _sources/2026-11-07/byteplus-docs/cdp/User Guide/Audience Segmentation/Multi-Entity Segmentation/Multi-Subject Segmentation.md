---
title: "Multi-Subject Segmentation"
product: "BytePlus CDP"
product_code: "cdp"
source: "https://docs.byteplus.com/en/docs/cdp/Multi-Subject_Segmentation"
---

<span id="_1-功能概述"></span>
# 1. Function Overview

Multi\-Subject segmentation refers to segmenting by user, product, store, and other different subjects and relationships. It can segment through the labels of multiple subjects and relationships between subjects, connecting the relationships between people, goods, and stores (supports selecting up to **three subjects** simultaneously).

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>



1. <div data-tips="true" data-tips-type="warning">This function is a <strong>paid feature</strong>, please contact your account manager if needed.</div>


2. <div data-tips="true" data-tips-type="warning">Differences between subject segment transformation and multi\-subject segmentation function:</div>


   <div data-tips="true" data-tips-type="warning">a. <strong>Subject Segment Transformation</strong>: Supports inputting segment files of <strong>any</strong> subject, converting them into a different subject's segment file, achieving various matching scenarios.   </div>
   

   <div data-tips="true" data-tips-type="warning">b. <strong>Multi\-subject Segmentation (Paid Feature)</strong>: After the function is deployed, users can directly create segment based on <strong>multiple subjects</strong>, transforming the relationships between up to three subjects on the same page, and flexibly choose the final target audience, shortening the operation process of multi\-subject segmentation.   </div>
   


<span id="bc7aa418"></span>
# 2. Application Scenarios


* Multi\-Subject segmentation is commonly used in recommendation, matching, and asset use scenarios, easily achieving precise "person\-product matching," "person\-store matching," and "product\-store matching."

* Differentiated Marketing: Analyze the user portraits for a certain car to push suitable marketing information, thereby improving lead conversion rates.

* **Precision Marketing**: Reach **car owners** through commuting time, hobbies, occupations, and other related conditions on the **car terminal**, providing accurate maintenance, upgrades, and other **value\-added services**.


<span id="61504fcf"></span>
# 3. Explanation of Terms

**Subject**: Refers to the active behavior log data / operational log, which actively generates data objects, such as: users / stores / cars / leads, etc.

**Relationship**: The condition that produces data correlation between subjects, such as: there may be test drive / purchase relationships between users and cars.

**Target Output Subject**: The subject of the segmented package that users ultimately hope to output.

Multi\-Subject Segment: When creating segments, select different subjects, such as users / cars / stores, and relationships to make segments, such as selecting the group of "users who visited a certain store and purchased a certain car".

<span id="81b27bb6"></span>
# 4. Operating Instructions

Click on **Segmentation\-Create Private Domain Segmentation\-Multi\-Subject Segment\-Select the Target Output Subject Type** to enter the interface for creating multi\-subject rules for segmentation.

<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_3f35a38fd29df629db80cb41be79fe5f.gif) </span>

<span id="1eb60d01"></span>
## 4.1 Creating Segmentation Rules for Multiple Subjects

Select the target output subject type, click ok, and enter the segment page.

<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_d0a9af69ad35713f049f4e142d3638fb.png) </span>

<span id="7aeb11a5"></span>
### 4.1.1 Subject and Relationship Configuration

First configure the subject and relationship.


1. Determine which subjects are involved in the , and what the target output subject is (switching freely during the creation process).

2. Determine the relationship among the three subjects: the system will calculate the intersection based on the selected subject transformation relationship, thus calculating the ID retained by the subject.


<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_e79226477c16753513c37d22abf8d79c.png) </span>

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Users want to select groups of users based on the relationships between products, stores, and users as follows:</div>


<div data-tips="true" data-tips-type="tip">Visited <strong>Flagship store of a certain car brand in Huangpu District, Shanghai</strong>, test drove a <strong>Car X model</strong> by <strong>male high\-income users</strong>.</div>


**Participating subjects**: users, stores, products (cars)｜**Output segmenting subjects:**  users

This segmentation can be represented by a relationship diagram.

<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_a8422f1a5a9d7da363aa544d36324a1f.png) </span>

When creating a segment, the logic of subject relationship configuration should be as follows:

<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_ff58aa00c21788237908bea574158f40.png) </span>

Subsequently, a segment centered around **users** can be generated.

Notes: The multi\-subject function supports up to three subjects simultaneously. Users can choose to establish connections based on only two subjects (such as stores\-cars).

<span id="26014350"></span>
### 4.1.2 Setting Subject Filter Conditions

Users need to filter all participating subjects according to the established conditions, with the same range of filterable conditions.

<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_0a95be248be6d5490d3b707f55fce237.png) </span>

New exclusion function added to the main filter conditions, allowing users to filter out the segment of people who do not belong to the "segment." "Match" and "exclude" components are arranged at the same layer. Other than the opposite calculation logic, the selectable ranges for filter conditions are entirely the same.

<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_bc8bad10ba28a35c2c634b01af93d2a5.png) </span>

<span id="daaa4389"></span>
### 4.1.3 Segmentation Information Input and Task Configuration

After configuring the main filter conditions, fill in the segmentation name, authorization object (supports custom authorization objects), output main subject ID type, encryption method, and optional field can be selected or filled in based on actual business needs.

<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_decf3e0f29c4b1f1578a1bd1c217f3bf.png) </span>

Select task configuration, update frequency type.

Notes: Daily updates may cause cluster queue congestion and slow down the update speed. It is not recommended to use this type unless necessary.

<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_9e5e94ce9df93137344a7f27a1c213be.png) </span>

After configuration, click **Save** in the upper right corner to find the newly created segmentation package in the user segmentation and put it into subsequent use.

<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_4a8773de157cc3bba1b8661d2a4663ef.png) </span>

<span id="348e6608"></span>
## 4.2 Downloading Multi\-Subject Rules Segmentation

When downloading multi\-subject rules segments, you can choose to download the segmentation of the target subject or **download all segments (including all process segments generated by participating in the selected subjects).** 

> \*This feature is controlled by the product switch and is off by default.


<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/cc9b7e702b944ad0872e5aa7651d424a~tplv-goo7wpa0wc-image.image" width="2744px" /></div>


<span id="4179d135"></span>
## 4.3 Dynamic Demonstration

Only **two main subject segments** are displayed here.

<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_905ac6801a27672bbbcc01c17629801a.gif) </span>
