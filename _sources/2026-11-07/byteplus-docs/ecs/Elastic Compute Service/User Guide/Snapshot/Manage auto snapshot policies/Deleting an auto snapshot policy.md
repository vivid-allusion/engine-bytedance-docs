---
title: "Deleting an auto snapshot policy"
product: "Elastic Compute Service"
product_code: "ecs"
source: "https://docs.byteplus.com/en/docs/ecs/Delete-an-auto-snapshot-policies"
---

You can delete an auto snapshot policy if you no longer need it. This topic explains how to delete an auto snapshot policy in the BytePlus console.

<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites

You have created an auto snapshot policy. For more information, see [Creating an auto snapshot policy](https://docs.byteplus.com/en/docs/ecs/Create-an-auto-snapshot-policy).

<span id=".5rOo5oSP5LqL6aG5"></span>
## Notes

Deleted policies cannot be recovered. If an auto snapshot policy is associated with volumes, this policy will no longer apply to them after deletion. Proceed with caution.

<span id=".5pON5L2c5q2l6aqk"></span>
## Steps


1. Log in to the [ECS console](https://console.byteplus.com/ecs/instance).

2. In the left navigation pane, select "Storage \> Snapshots".

3. In the top menu bar, select the project and region where the auto snapshot policy resides.

4. On the "Snapshots" page, click the "Auto Snapshot Policies" tab.

5. On the "Auto Snapshot Policies" tab, click "Delete policy" in the "Actions" column of the policy you want to remove.

6. In the box that appears, click "Delete policy".
