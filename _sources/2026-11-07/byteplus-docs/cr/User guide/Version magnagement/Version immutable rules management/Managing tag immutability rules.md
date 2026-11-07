---
title: "Managing tag immutability rules"
product: "Container Registry"
product_code: "cr"
source: "https://docs.byteplus.com/en/docs/cr/manage-version-immutable-rules"
---

This topic describes how to modify and delete existing tag immutability rules.

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">When modifying a tag immutability rule, you cannot update the namespace to which the rule applies.</div>


<span id="7xvH44Ca"></span>
## Modify a rule

Update the configuration of a tag immutability rule.


1. Log in to the target instance.

   1. Log in to the [CR console](https://console.byteplus.com/cr).

   2. Select the target region in the top navigation bar.

   3. In the left navigation bar, click **List of instances**, find the target instance, and click **Enter instance**.

2. In the left navigation bar of the instance page, click **tag immutability**.

3. In the Actions column of the target rule, click **Modify**.

4. Modify the rule configuration information. For parameter description, see [Create tag immutability rule](https://docs.byteplus.com/en/docs/cr/create-a-version-immutable-rule?lang=en).

5. Click **confirm** to complete the operation.


<span id="CF06ozZp"></span>
## Delete a rule

You can delete currently unused rules to free up quota slots. You can free up quota by deleting existing rules.


1. Log in to the target instance.

   1. Log in to the [CR console](https://console.byteplus.com/cr).

   2. Select the target region in the top navigation bar.

   3. In the left navigation bar, click **List of instances**, find the target instance, and click **Enter instance**.

2. In the left navigation bar of the instance page, click **tag immutability**.

3. In the Actions column of the target rule, click **Delete**.

4. On the secondary confirmation page, click **Delete** to complete the operation.
