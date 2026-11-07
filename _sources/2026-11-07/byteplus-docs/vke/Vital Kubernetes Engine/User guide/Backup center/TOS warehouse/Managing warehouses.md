---
title: "Managing warehouses"
product: " Vital Kubernetes Engine"
product_code: "vke"
source: "https://docs.byteplus.com/en/docs/vke/Managing_warehouse"
---

After a TOS warehouse is added, you can go to the TOS warehouses page to manage the warehouse. This topic describes the scenarios, impacts, and procedures of TOS warehouse management operations.

<span id="ErLTwfUO"></span>
## Editing warehouses

You can edit the access key ID and secret access key of an existing TOS warehouse. This allows you to update the access key ID and secret access key of the source TOS bucket or correct the information specified when the TOS warehouse was added.


1. Log in to the [VKE console](https://console.byteplus.com/vke).

2. In the left navigation bar, choose **Backup center \> TOS warehouse** to enter the TOS warehouse page.

3. Click **Edit** in the Actions column to update the information. When you finish, click **Confirm**.


<span id="aV1vdPeu"></span>
## Deleting warehouses

If you no longer need a TOS warehouse and the contained data, you can delete the TOS warehouse to release resources.

<div data-tips="true" data-tips-type="danger" data-tips-is-title="true">danger</div>


<div data-tips="true" data-tips-type="danger">TOS warehouses provide necessary resources for application backup and restore. After warehouse deletion, backup data cannot be restored. Exercise caution when you perform this operation.</div>



1. Log in to the [VKE console](https://console.byteplus.com/vke).

2. In the left navigation bar, choose **Backup center \> TOS warehouse** to enter the TOS warehouse page.

3. Click **Delete** in the Actions column. In the pop\-up window, confirm the information. If no risk arises from the deletion, click **Confirm**.
