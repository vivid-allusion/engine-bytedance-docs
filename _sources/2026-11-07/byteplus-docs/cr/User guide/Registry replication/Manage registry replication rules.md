---
title: "Manage registry replication rules"
product: "Container Registry"
product_code: "cr"
source: "https://docs.byteplus.com/en/docs/cr/manage-registry-replication"
---

This topic describes the management operations related to registry replication, including viewing, modifying, disabling, enabling, and deleting registry replication rules.

<span id="meaOiKrz"></span>
## Modify a registry replication rule


1. Log in to the CR consoleCR console.

2. In the left navigation pane, select **Registry replication**. The **Registry replication** page is displayed.

3. Select the target registry replication rule and click the **Edit** button in the "Actions" column to modify the registry replication rule.


<span id=".56aB55So5ZCM5q2l6KeE5YiZ"></span>
## Disable a registry replication rule

You can change a registry replication rule from the enabled state to the disabled state. After you disable a registry replication rule, it will stop taking effect immediately.


1. Log in to the CR consoleCR console.

2. In the left navigation pane, select **Registry replication**. The **Registry replication** page is displayed.

3. Select the target registry replication rule and click the **Disable** button in the "Actions" column to disable the registry replication rule.


<span id=".5ZCv55So5ZCM5q2l6KeE5YiZ"></span>
## Enable a registry replication rule

You can re\-enable a registry replication rule that is currently disabled. After you enable a registry replication rule, you can choose whether to trigger it immediately based on your needs.


1. Log in to the CR consoleCR console.

2. In the left navigation pane, select **Registry replication**. The **Registry replication** page is displayed.

3. Select the target registry replication rule and click the **Enable** button in the "Actions" column. The **Enable synchronization rules?**  dialog box is displayed.

4. Select whether to trigger it immediately or not based on your needs.

   1. Trigger immediately: For existing images, the rule will be triggered as soon as the conditions are met.

   2. Don't trigger for now: Synchronization will be triggered only once when a new image is updated and the rule conditions are met.

5. Click **Confirm** to enable the rule.


<span id=".5Yig6Zmk5ZCM5q2l6KeE5YiZ"></span>
## Delete a registry replication rule

After a registry replication rule is deleted, historical logs cannot be viewed.


1. Log in to the CR consoleCR console.

2. In the left navigation pane, select **Registry replication**. The **Registry replication** page is displayed.

3. Select the target registry replication rule and click the **Delete** button in the "Actions" column. The **Delete synchronization rule?**  dialog box is displayed.

4. Click **confirm** to delete the registry replication rule.


<span id="2oDxSEiZ"></span>
## Terminate a synchronization task

If a synchronization task fails to complete for an extended period, you can terminate the task to stop subsequent image synchronization for it.

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">After a task is terminated, images that are being synchronized will continue to be synchronized, while images that have not yet started synchronization will no longer be synchronized. The image list only shows images that have been synchronized as expected.</div>



1. Log in to the CR consoleCR console.

2. In the left navigation pane, click **Registry replication**.

3. Click the name of the target registry replication rule.

4. In the synchronization log list, click **Terminate** in the **Actions** column.

5. On the secondary confirmation page, click **Terminate** to complete the operation.
