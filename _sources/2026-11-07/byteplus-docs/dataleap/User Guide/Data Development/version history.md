---
title: "version history"
product: "DataLeap"
product_code: "dataleap"
source: "https://docs.byteplus.com/en/docs/dataleap/version_history"
---

Version history records the versions of the task submitted to production. It supports viewing version details and restoring a specific version as draft. You can also select two versions and click version comparison in the top right corner to see the differences between versions.

<span id="f7180522"></span>
## 1 prerequisites

The data development task has been submitted and published to multiple production versions.

<span id="_2-功能入口"></span>
## 2 access points


1. Log in to the [DataLeap Tenant Console](https://console.byteplus.com/dataleap/console/region:dataleap-console+ap-southeast-1/project/list?administrator=mine&current=1&isMine=true&pageSize=20&projectName=&projectOrOwnerName=&sortColumn=createTime&sortOrder=desc)

2. On the **Overview** page, under the project, enter **IDE Development**.

3. On the **Data Development** page, open the edit page of a specific task.

4. Click **Versions** in the right sidebar to enter.


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/7450264f31064b1bb5a5f8c42a81cda1~tplv-goo7wpa0wc-image.image) </span>

<span id="_3-功能介绍"></span>
## 3 function introduction

Display the list of versions, including records of historically deployed versions:


* Version number:

   * The draft value represents the most recently saved version, indicated by \-1;

   * Historical deployed versions are marked starting from version number 1 in the order they were deployed;

   * The version with the highest version number is the current production version.

* Committer: records the person responsible for submitting the historical deployed version

* Reviewer: records the person responsible for reviewing the historical deployed version

* Deploy instructions: records the description provided when submitting the historical deployed version

* Update time: records the specific update time of the historical deployed version

* Change: change types include task draft updated, task deployed

* Action:

   * View: Select a version and click **View** to see the basic info, scheduling information, dependencies, input/output parameters, and code configuration of that historical version for the current node.

   * Restore as draft: Select a version and click **Restore as draft** to revert the configuration information of the specified version to the task’s configuration page.

* Version comparison: Check two versions and click **Version comparison** at the top right to view the differences between the versions.
