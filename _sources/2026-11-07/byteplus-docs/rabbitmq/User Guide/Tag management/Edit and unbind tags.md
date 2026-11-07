---
title: "Edit and unbind tags"
product: "Message Queue for RabbitMQ"
product_code: "rabbitmq"
source: "https://docs.byteplus.com/en/docs/rabbitmq/Edit_and_unbind_tags"
---

After binding tags to a specified instance, you can modify the tag key or tag value anytime according to business needs. If you need to adjust the classification of an instance, you can also directly unbind instance tags. This section is a guide for editing and unbinding tags.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Supports batch unbinding of instances and tags, with up to 20 tags unbound at once.</div>


<span id=".5Li65Y2V5Liq5a6e5L6L5L-u5pS55oiW6Kej57uR5qCH562-"></span>
## Modify or unbind tags for a single instance


1. Log in to [Message Queue for RabbitMQ Console](https://console.byteplus.com/rabbitmq).

2. Select the region where the instance is located from the top menu bar.

3. Find the specified instance and click the edit icon in the **Tags** column.

   You can also click the instance name, then click the edit icon in the **Tag** row within the **Basic Information** section.

4. Edit or unbind tags based on business needs.

   * Edit tags: reset **Tag Key** or **Tag Value**. Follow tag setting rules when setting tags. For details, please refer to [Tag Setting Rules](https://docs.byteplus.com/en/docs/rabbitmq/Bind_tags#.5qCH562-6K6-572u6KeE5YiZ).

   * Unbind tags: find the specified tag key and click **Delete**.

5. Click **Confirm**.


<span id=".5om56YeP6Kej57uR5qCH562-"></span>
## Bulk unbind tags


1. Log in to [Message Queue for RabbitMQ Console](https://console.byteplus.com/rabbitmq).

2. Select the region where the instance is located from the top menu bar.

3. Select all instances to set tags and click **Unbind Tags** at the top left of the page.

4. Select the tag key to delete from the dropdown or enter the tag key to filter.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">The page shows the number of selected instances associated with the specified tag. It indicates how many instances in the selected list are bound to that tag key. When unbinding tags, all tags corresponding to the specified tag key in the selected instance list will be unbound. Instance tags outside the selected list are not adjusted.   </div>
   

5. Click **Confirm**.
