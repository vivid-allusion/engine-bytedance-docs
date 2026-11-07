---
title: "Policy configuration"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/policy-management_en"
---

<span id="overview"></span>
## Overview

To safely manage and update your CDN policy configurations without impacting live services, you can use the policy versioning feature. This feature allows you to create draft versions to modify settings, publish them once you are ready, and easily roll back to a previous stable configuration if needed. This guide explains the concept of policy versions and provides step\-by\-step instructions for the entire lifecycle, from creation to deletion.

Additionally, policy versioning allows you to roll back policy configurations to a previous version. You can also duplicate a specific version and update policy configurations in the duplicate version. When publishing or rolling back policy versions, it's recommended to add meaningful descriptions for future maintenance. For example, when you need to view, duplicate, or delete a version later, version descriptions can help you find the version you want to manage.

<span id="version-status"></span>
### **Version Status**

Policy versions have the following statuses:


* Published: Indicates the version is published and its policy configurations are in effect.

* Unpublished: Indicates the version was previously published but has been revoked. The policy configurations in this version are no longer in effect.

* Draft: Indicates the version hasn't been published.


You can only modify policy configurations when the version status is "Draft".

The following table lists the operations allowed for each status.


|**Version Status** |**Allowed Operations (Y means allowed)**  ||||||
|---|---|---|---|---|---|---|
||**View** |**Modify** |**Roll Back** |**Publish** |**Delete** |**Duplicate** |
|Draft | |Y | |Y |Y | |
|Published |Y | | | | |Y |
|Unpublished |Y | |Y | |Y |Y |


<span id="version-number"></span>
### **Version Number**

When you publish a version, CDN generates a version number for it. When you [roll back a version](https://docs.byteplus.com/en/docs/18/40496#roll-back-version), CDN generates and publishes a new version and assigns a version number to the published version.

Version numbers follow the format `P-<first_publish_date>-<random_5_digits>`. For example, `P-250224.44093`.

Draft versions don't have version numbers and display `draft` in the **Version** column.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Each policy records a maximum of 50 published versions.</div>


<span id="operation-instructions"></span>
## Operation Instructions

<span id="view-policy-configurations-in-a-version"></span>
### View Policy Configurations in a Version

For versions with the status "Published" or "Unpublished", you can view the policy configurations in the version. The policy configurations are displayed as API parameters. To understand the meaning of each parameter, see [UpdateServiceTemplate](https://docs.byteplus.com/en/docs/byteplus-cdn/reference-updateservicetemplate) and [UpdateCipherTemplate](https://docs.byteplus.com/en/docs/byteplus-cdn/reference-updateciphertemplate-ac087).

There are two methods to view policy configurations in a specific version.

<span id="method-1-view-on-the-policy-details-page"></span>
#### **Method 1: View on the Policy Details Page**


1. In the policy list, find the policy you want to view and click its ID.

2. In the version list at the top right of the policy details page, select the version you want to view.


After you select a version, the policy details page displays the policy configurations in that version.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">Versions in the version list are sorted by creation time. The most recently created version appears first.</div>


* <div data-tips="true" data-tips-type="tip">The version list displays version numbers without version descriptions. If you need to select a version based on version descriptions, use Method 2.</div>



<span id="method-2-view-in-the-policy-versions-tab"></span>
#### **Method 2: View in the "Policy Versions" Tab**


1. In the policy list, find the policy you want to view.

2. In the **Actions** column, click **History**.

3. In the **Version Management** tab, click **Policy Versions**.

4. In the version list, find the version you want to view.

5. In the **Actions** column, click **View**.


<span id="create-version"></span>
### Create Version

To create a policy version, follow these steps:


1. In the policy list, find the policy you want to operate on.

2. Click the policy ID to open the policy details page.

3. At the top right of the page, click **Create Version**.


After clicking **Create Version**, CDN duplicates the published version to generate a draft version, which is identified by the label `draft`. At the same time, the **Create Version** button becomes disabled.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">After you click <strong>Create Version</strong>, the policy details page displays the policy configurations in the "Published" version, not the policy configurations in the draft version.</div>


* <div data-tips="true" data-tips-type="tip">Because a policy can have only one draft version at a time, the <strong>Create Version</strong> button is disabled if a draft already exists.</div>



<span id="modify-policy-configurations-in-version"></span>
### Modify Policy Configurations in Version

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">You can only modify policy configurations in versions with "Draft" status.</div>


To modify policy configurations in a version, follow these steps:


1. In the policy list, find the policy you want to operate on.

2. In the **Actions** column, click **History**.

3. In the **Version Management** tab, click **Policy Versions**.

4. In the version list, find the version you want to operate on.

5. In the **Actions** column, click **Modify**.

6. On the policy details page, click the **Policy Configuration** tab.

7. Modify the policy configurations.

8. After modification, click **Save** at the bottom right of the page.


<span id="publish-version"></span>
### Publish Version

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">You can only publish versions with "Draft" status.</div>


To apply the configurations in a draft version, you must publish it. Once published, the version's policy configurations will apply to all domains that use the policy.

To publish a version, follow these steps:


1. In the policy list, find the policy you want to operate on.

2. In the **Actions** column, click **History**.

3. In the **Version Management** tab, click **Policy Versions**.

4. In the version list, find the version you want to operate on.

5. In the **Actions** column, click **Publish**.

6. In the **Publish Policy** dialog box, enter a meaningful version description, then click **OK**.


After publish, the version status changes from "Draft" to "Published". The previously published version's status changes from "Published" to "Unpublished".

<span id="roll-back-version"></span>
### Roll Back Version

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">You can only roll back versions with "Unpublished" status.</div>


To apply the policy configurations in an "Unpublished" version, you can roll back to it. Rolling back to an "Unpublished" version immediately republishes it.

To roll back a version, follow these steps:


1. In the policy list, find the policy you want to operate on.

2. In the **Actions** column, click **History**.

3. In the **Version Management** tab, click **Policy Versions**.

4. In the version list, find the version you want to roll back.

5. In the **Actions** column, click **Roll Back**.

6. In the **Publish Policy** dialog box, enter a meaningful version description, then click **OK**.


<span id="duplicate-version"></span>
### Duplicate Version

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">You can only duplicate versions with "Published" or "Unpublished" status.</div>


If you need to modify policy configurations based on a specific version, you can duplicate it.

When you duplicate a version, CDN performs these operations:


* Creates a new draft version that is an identical copy of the one you duplicated.


To duplicate a version, follow these steps:


1. In the policy list, find the policy you want to operate on.

2. In the **Actions** column, click **History**.

3. In the **Version Management** tab, click **Policy Versions**.

4. In the version list, find the version you want to duplicate.

5. In the **Actions** column, click **Duplicate**.


Note that if a draft version already exists, this duplicate operation will overwrite it.

<span id="delete-version"></span>
### Delete Version

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">You can only delete versions with "Unpublished" or "Draft" status.</div>


* <div data-tips="true" data-tips-type="tip">Deleted versions cannot be recovered.</div>



If you no longer need a version, you can delete it.
