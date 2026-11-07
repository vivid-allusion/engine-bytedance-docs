---
title: "Feature Version Management"
product: "BytePlus DataTester"
product_code: "DataTester"
source: "https://docs.byteplus.com/en/docs/DataTester/Feature-Version-Management"
---

<span id="一、功能简介"></span>
# 1. Introduction to functions


* In order to facilitate the recording and management of Feature changes, a new version (identified by V1, V2, etc.) is generated for each change to Feature key information (variants, effective rules, etc.).

* The generated new version needs to be released to take effect.


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/240762c5a70b4e6fa7effcdec7e32513~tplv-goo7wpa0wc-image.image) </span>

<span id="二、如何使用"></span>
# 2. How to use


* Entrance: In Feature List, click on the name to enter the version list

* The version list is divided into released and unreleased versions

   * The left side of the version list displays all version lists, and you can view the status and valid time of each version, release traffic, etc.

   * Click on the right side of a version to display the details of that version (i.e. basic information, variants, and release audience, etc.)

* From the upper right corner of the version details page, you can do the following:

   * Create an experiment: create an AB testing with this feature

   * Release/Rollback: Release means incremental release operation for this version (if releasing/fully rolled back); Rollback means rollback operation for this version, (unreleased/reviewed/rolled back state cannot be rolled back)

   * Disable: That is, disable the version. After disabling, the version cannot be edited, released, or unbanned (unreleased/rolled back status can be disabled).

* Other features of Feature List:

   * Whitelist testing: that is, add a whitelist for testing, and create a new whitelist for the release version

   * Operation log: You can view the operation log for this feature by time

   * Life cycle management:

   * Metric monitoring:

* Version menu bar:

   * App selection: Different product lines can be selected for version details display

   * Feature status:

      * After clicking Close, the variant value will not be delivered, and all traffic will take effect according to the local default value.

      * After clicking Open, select a version to publish on the version list page of the current Feature.

   * Permission settings:

   * Delete: cannot be restored after deletion; deletion cannot be performed when the feature state is turned on

   * Edit: Click Edit and jump to the Feature creation page for editing. After saving the release, it will be incrementally released in the current version.
