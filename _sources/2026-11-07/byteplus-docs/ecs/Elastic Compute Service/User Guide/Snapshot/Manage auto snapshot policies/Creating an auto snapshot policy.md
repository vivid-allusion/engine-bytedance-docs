---
title: "Creating an auto snapshot policy"
product: "Elastic Compute Service"
product_code: "ecs"
source: "https://docs.byteplus.com/en/docs/ecs/Create-an-auto-snapshot-policy"
---

You can configure an automatic snapshot policy to regularly back up your volume data using snapshots. This topic explains how to create an automatic snapshot policy in the BytePlus console.

<span id=".5rOo5oSP5LqL6aG5"></span>
## Notes


|Category |Considerations |
|---|---|
|Quantity |* You can create up to 1,024 automatic snapshots for each volume. Once you reach the maximum, the system will automatically delete the oldest snapshot.<br><br>* You can create up to 32 auto snapshot policies per account and region. |
|Time |* The time you set for the auto snapshot policy may differ from when the snapshot is actually created. The actual creation time will take precedence.<br><br>* If creating an automatic snapshot takes longer than the interval between two scheduled time points, the system automatically skips creating a snapshot at the next time point. For example, if you set creation time points at 1:00, 2:00, and 3:00, and the snapshot scheduled at 1:00 takes until 2:30 to finish, the 2:00 snapshot will be skipped and the next one will be created at 3:00. |
|Restriction |You cannot create both automatic and manual snapshots for a volume simultaneously. |


<span id=".5pON5L2c5q2l6aqk"></span>
## Steps


1. Log in to the [ECS console](https://console.byteplus.com/ecs/instance).

2. In the left navigation pane, select "Storage \> Snapshots".

3. In the top menu bar, select the project and region where you want to create an auto snapshot policy.

4. On the "Snapshots" page, click the "Auto Snapshot Policies" tab.

5. On the "Auto Snapshot Policies" tab, click "Create policy". In the box that appears, set the policy parameters.



|Parameter |Description |
|---|---|
|Policy name |Enter the name for the auto snapshot policy. Requirements:<br><br><br>* The name must start with a Chinese character, a letter or an underscore (_).<br><br>* The name can contain Chinese characters, letters, numbers, periods (.), underscores (_), or hyphens (\-).<br><br>* The name must be between 1 and 128 characters long. |
|Creation time point |Select one or more time points to create automatic snapshots.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">Creating snapshots reduces storage performance, so we recommend doing it during off\-peak hours.</div><br> |
|Backup cycle |Select the days on which you would like auto snapshots to be created. Options:<br><br><br>* By week: Select one or more days from Monday to Sunday.<br><br>* By day: Specify the interval of days for the backup cycle. The valid range is between 1 and 30 days. |
|Retention time |Specify how long the automatic snapshots should be retained. The default retention period is 30 days.<br><br><br>* Custom retention: 1 to 65,536 days.<br><br>* It will be permanently retained and will not be automatically deleted until the number of automatic snapshots reaches the upper limit: The system automatically deletes the oldest snapshot when the number of automatic snapshots reaches the upper limit.<br><br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">Each volume can have up to 1,024 automatic snapshots.</div><br> |
|Project |(Optional) Select the project to which the snapshots belong.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">A project is a virtual concept that comprises a set of resources, users, and roles. It provides a unified view of and access to resources, as well as control over user and role permissions within the project. </div><br><br><br>* <div data-tips="true" data-tips-type="tip">To create a project, click "Create new projects" on the right. This will take you to the <a href="https://console.byteplus.com/iam/resourcemanage/project">IAM console</a>.</div><br> |
|Tag |A tag is a key\-value pair used to identify cloud resources. Tags help you categorize cloud resources by purpose, owner, environment, and other criteria for easy searching and aggregation.<br><br>To add a tag to a policy, click the <span>![图片](https://lf3-volc-editor.volccdn.com/obj/volcfe/sop-public/upload_745f4ea6f3f698cebd9adc96c9240260.png) </span> icon and enter the tag key and value. For more information, see [Tag management](https://docs.byteplus.com/en/docs/ecs/Tag-overview). |



6. Once you have finished configuring, click "Create policy".


<span id=".5ZCO57ut5pON5L2c"></span>
## Next steps

After creating an auto snapshot policy, associate it with a volume to activate it. For more information, see [Associating an auto snapshot policy with a volume](https://docs.byteplus.com/en/docs/ecs/Associate-Cancel-an-auto-snapshot-policies-for-volume).

<span id=".5YW25LuW5pON5L2c"></span>
## Other operations


* [Modifying an auto snapshot policy](https://docs.byteplus.com/en/docs/ecs/Modify-an-auto-snapshot-policy)

* [Deleting an auto snapshot policy](https://docs.byteplus.com/en/docs/ecs/Delete-an-auto-snapshot-policies)
