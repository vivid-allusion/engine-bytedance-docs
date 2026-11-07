---
title: "Managing tag retention rules"
product: "Container Registry"
product_code: "cr"
source: "https://docs.byteplus.com/en/docs/cr/manage-tag-retention-rules"
---

This topic describes how to execute, disable, edit, and delete a created tag retention rule.

<span id="3HhXNww1"></span>
## Manual execution of rules

Clean up the images by triggering the retention rule immediately. Corresponding storage space is released within 1\-5 hours after the task is completed.


1. Log in to the CR consoleCR console.

2. Select the target region in the top navigation bar.

3. In the left navigation bar, click **Tag retention**.

4. In the **Actions** column of the target rule, click **Execute**.

5. In the confirmation dialog box, click **Confirm**.


<span id="3I9HGWlm"></span>
## Disable/enable rules

You can free up quota by deleting existing rules. Disabled rules can be enabled again.


1. Log in to the CR consoleCR console.

2. Select the target region in the top navigation bar.

3. In the left navigation bar, click **Tag retention**.

4. In the **Actions** column of the target rule, click **Disable** or **Enable**.

5. On the secondary confirmation page, click **Confirm**.


<span id="haIc3O93"></span>
## Edit rules

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">You cannot update the instance to which the rule applies.</div>



1. Log in to the CR consoleCR console.

2. Select the target region in the top navigation bar.

3. In the left navigation bar, click **Tag retention**.

4. In the **Actions** column of the target rule, click ** ...**  \> **Edit**.

5. Modify the rule configuration information. For parameter description, see [Create tag retention rules](https://docs.byteplus.com/en/docs/cr/create-a-tag-retention-rule?lang=en).

6. Click**Confirm**.


<span id="CHepn0Mr"></span>
## Delete a rule

You can delete currently unused rules to free up quota slots. You can free up quota by deleting existing rules.


1. Log in to the CR consoleCR console.

2. Select the target region in the top navigation bar.

3. In the left navigation bar, click **Tag retention**.

4. In the **Actions** column of the target rule, click ** ...**  \> **Delete**.

5. In the confirmation dialog box, click **Delete**.
