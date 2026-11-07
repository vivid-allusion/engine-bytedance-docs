---
title: "Modify an auto snapshot policy"
product: "Elastic Compute Service"
product_code: "ecs"
source: "https://docs.byteplus.com/en/docs/ecs/Modify-an-auto-snapshot-policy"
---

This topic describes how to modify an auto snapshot policy on the BytePlus console.

<span id="before-you-begin"></span>
## Before you begin

Create an auto snapshot policy. For information on the related steps, refer to [Create an auto snapshot policy](https://docs.byteplus.com/en/docs/ecs/Create-an-auto-snapshot-policy).

<span id="procedure"></span>
## Procedure


1. Log on to the [ECS console](https://console.byteplus.com/ecs).

2. In the left\-side navigation pane, click **Storage** \> **Snapshots**.

3. In the top menu bar, choose the project and the Region of the target auto snapshot policy.

4. On the **Snapshots** page. click the **Auto snapshot policy** tab.

5. On the **Auto snapshot policy** tab, find the target policy, click **Modify policy** in the **Actions** column, and modify policy parameters in the dialog box that appears. The following table describes the parameters.

   
   |Parameter |Description |
   |---|---|
   |Policy name |Specify the name of an auto snapshot policy. Valid values:<br><br><br>* The value starts with a Chinese character, a letter, or an underscore ( _ ).<br><br>* The value can contain Chinese characters, letters, digits, periods ( . ), underscores ( _ ), and hyphens ( \- ).<br><br>* The name is 1 through 128 characters in length. |
   |Creation time point |Specify one or more points in time at which snapshots are automatically created.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">We recommend that you specify a time during off\-peak periods because the storage performance is affected when the system creates a snapshot.</div><br> |
   |Backup cycle |Specify an interval or days on which snapshots are automatically created. Details:<br><br><br>* **By week**: Specify one or more days in a week.<br><br>* **By day**: Specify an interval as the backup period. You can specify an interval from 1 day to 30 days. |
   |Retention time |Specify a retention period for auto snapshots. By default, the retention period is 30 days.<br><br><br>* Customize retention time: Specify a retention period from 1 day to 65,536 days.<br><br>* Continuously retain will be automatically deleted until the number of automatic snapshots reaches the upper limit: The system automatically deletes the earliest auto snapshot once the number of auto snapshots reaches the upper limit.<br><br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">A modified retention period applies to snapshots created after the modification.</div><br> |
   

6. After you modify all target parameters, click **Modify policy**.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">After you modify an auto snapshot policy that is associated with a volume, the policy automatically takes effect.   </div>
