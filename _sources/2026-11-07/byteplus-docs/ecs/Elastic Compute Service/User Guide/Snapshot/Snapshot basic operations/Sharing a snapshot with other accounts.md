---
title: "Sharing a snapshot with other accounts"
product: "Elastic Compute Service"
product_code: "ecs"
source: "https://docs.byteplus.com/en/docs/ecs/Cross-account-snapshot-sharing"
---

EBS lets you share a snapshot with other accounts. Then, the recipient can use the snapshot to create a volume. This topic explains how to do so.

<span id="3hOvkwKU"></span>
## Prerequisites


* If you are sharing with a BytePlus account, you will need the account ID.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">To view the ID of a BytePlus account, log in to the <a href="https://console.byteplus.com/home">BytePlus console</a> and click the avatar in the upper\-right corner.   </div>
   

* To share within an organization, you must first get the ID of that organization or of a department within it.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">To get the organization ID: Log in to the <a href="https://console.byteplus.com/organization/basic/">Organization console</a>, and select "Organization settings \> Basic information" in the left navigation pane. The organization ID is located under the organization name.   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">To get the department ID: Log in to the <a href="https://console.byteplus.com/organization/basic/">Organization console</a>, and select "Organizational structure \> Member management" in the left navigation pane. Click the department name in the organization tree, and find the department ID in the upper\-left corner of the right panel.   </div>
   


<span id="3pVcnqQM"></span>
## Notes


|**Category** |Description |
|---|---|
|Quantity |* You can share a snapshot with up to 64 accounts.<br><br>* You can share up to 1,024 snapshots per account. |
|Billing |* Sharing snapshots is free. After a snapshot is shared, the billing responsibility remains with the sharer. In other words, the user who shares the snapshot is responsible for paying for it, not the recipient.<br><br>* If the recipient uses the shared snapshot to create a volume, however, the recipient is billed for the corresponding volume fees. |
|Sharing restrictions |Sharing is only possible for snapshots in the "Available" or "Rolling back" status. |
|Supported operations |The following operations are supported for shared snapshots:<br><br><br>* Creating a volume<br><br>* Viewing snapshot information |
|Snapshot restrictions |* Snapshots that have been shared cannot be shared again.<br><br>* Sharing snapshots is not supported if your account is overdue. |
|Project and region restrictions |* Shared snapshots are stored in the default project.<br><br>* Snapshots can only be shared with accounts in the same region. It is not allowed to share them with accounts in other regions. |


<span id="b5z8MUJk"></span>
## Sharing a snapshot

<span id="AdbcRydM"></span>
### Sharing a snapshot


1. Log in to the [Resource management console](https://console.byteplus.com/resourcemanager/resource_center/grant_permission).

2. In the top menu bar, select the region where the snapshot resides.

3. In the left navigation pane, select "Resource sharing \> Shared by me".

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">Alternatively, navigate to the "Snapshots" page in the <a href="https://console.byteplus.com/ecs/instance">ECS console</a> and click "..." \> "Shared snapshot" in the "Actions" column of the snapshot you want to share. This will take you to the "Shared unit" tab.   </div>
   

4. On the "Shared unit" tab, click "Create shared unit".

5. In the "Specify resource share details" wizard, enter a "Unit name" and set "Product" to "storage_ebs \- snapshot". Then, select the desired snapshot ID and click "Next".

6. In the "Associated sharing permission" wizard, review the actions that the recipient can perform on the shared snapshot. Then, click "Next".

7. In the "Associated shared user" wizard, configure the following parameters. Then, click "Next".

   
   |**Parameter** |**Description** |
   |---|---|
   |Resource user |Select the scope for snapshot sharing. The options include:<br><br><br>* Allow sharing with any account: You can share the snapshot with any account. If your account belongs to an organization, you can share the snapshot with the entire organization, its departments, or its member accounts.<br><br>* Only allow sharing with enterprises and organizations: You can only share the snapshot within the organization to which your account belongs. This includes the entire organization, its departments, and its member accounts.<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">An organization is a structured grouping of multiple accounts that maintains relationships among them. For more information, see <a href="https://docs.byteplus.com/en/docs/organization/BasicConcepts">Organization</a>.</div><br> |
   |Adding resource users |Specify the user with whom you want to share the snapshot. There are two ways to add a user:<br><br><br>* Add by organization: The sharer and recipient must belong to the same organization. Turn on "Add by business organization" and select the account from the organization tree.<br><br>* Add manually: Select a "User type", enter the "User id", and click "Add".<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">When setting "User type", you can choose "Master account", "Enterprise organization as a whole", or "Enterprise organization department".</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">Account: To share the snapshot with another account, set "User type" to "Master account" and enter the account ID.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">Entire organization: To share the snapshot with the entire organization of the recipient, set "User type" to "Enterprise organization as a whole" and enter the organization ID. After setup, all accounts within this organization will have access to the snapshot.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">Organization department: To share the snapshot with a department within the recipient's organization, set "User type" to "Enterprise organization department" and enter the department ID. After setup, all accounts within this department will have access to the snapshot.</div><br> |
   

8. In the "Confirm and submit" wizard, verify the information. If it is correct, click "Confirm".


<span id="xfENZg8s"></span>
### Using a shared snapshot


1. Accept the shared snapshot.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">This step is required when "User type" is set to "Master account" for the shared snapshot. When a snapshot is shared with an organization, department, or member account, the recipient does not need to accept it. They can use it directly in the ECS console.   </div>
   

   1. Log in to the [Resource management console](https://console.byteplus.com/resourcemanager/resource_center/grant_permission).

   2. In the top menu bar, select the region where the snapshot resides.

   3. In the left navigation pane, select "Resource sharing \> Share with me".

   4. On the "Share with me" page, click "Accept" in the "Actions" column of the snapshot.

      The "Shared Snapshots" tab on the "Snapshots" page in the ECS console will automatically display the snapshot once the recipient has accepted it.

2. Use the shared snapshot.

   1. Log in to the [ECS console](https://console.byteplus.com/ecs/instance).

   2. In the top menu bar, set "Project" to "default（默认项目）" and select the region where the snapshot resides.

   3. In the left navigation pane, select "Storage \> Snapshots".

   4. On the "Shared Snapshots" tab, click "Create new volume" in the "Actions" column of the snapshot. Follow the instructions to create a new volume from the snapshot. For more information about the parameters, see [Creating a volume from a snapshot](https://docs.byteplus.com/en/docs/ecs/Create-a-volume-through-snapshot).

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">On the "Shared Snapshots" tab, click the snapshot to view its details, including the snapshot ID and volume specifications.   </div>
   

<span id="EkY2r3kf"></span>
## Canceling sharing

<span id="Wwnvux0I"></span>
### By removing the recipient

Recipients cannot delete snapshots that have been shared with them. However, the sharer can remove the recipient from the shared unit, which automatically cancels the sharing of the snapshot with that recipient. The shared snapshot will also automatically be deleted on the recipient's end.


1. Log in to the [Resource management console](https://console.byteplus.com/resourcemanager/resource_center/grant_permission).

2. In the top menu bar, select the region where the snapshot resides.

3. In the left navigation pane, select "Resource sharing \> Shared by me".

4. On the "Shared unit" tab, click "View details" in the "Actions" column of the shared unit you want to manage.

5. On the details page, click "Edit shared unit" in the upper\-right corner.

6. In the "Specify resource share details" wizard, click "Next".

7. In the "Associated sharing permission" wizard, click "Next".

8. In the "Associated shared user" wizard, click "Remove" in the "Actions" column of the user you want to remove.

9. In the "Confirm and submit" wizard, click "Confirm".


<span id="ugHx8Asf"></span>
### By deleting the shared unit

Recipients cannot delete snapshots that have been shared with them. However, the sharer can delete the shared unit, which automatically cancels the sharing of the snapshot with that recipient. The shared snapshot will also automatically be deleted on the recipient's end.


1. Log in to the [Resource management console](https://console.byteplus.com/resourcemanager/resource_center/grant_permission).

2. In the top menu bar, select the region where the snapshot resides.

3. In the left navigation pane, select "Resource sharing \> Shared by me".

4. On the "Shared unit" tab, click "View details" in the "Actions" column of the shared unit you want to manage.

5. On the details page, click "Delete shared unit" in the upper\-right corner.

6. In the box that appears, click "OK".
