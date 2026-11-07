---
title: "Creating snapshots automatically"
product: "Cloud Search"
product_code: "cloudsearch"
source: "https://docs.byteplus.com/en/docs/cloudsearch/creating_snapshots_automatically"
---

Automatic snapshot creation means that snapshots are automatically created at a specified time according to the configured rule. On the snapshot management page, you can configure automatic snapshot rule for all instances in the current account and region.

<span id="d0b89dd8"></span>
## **Precautions**


* The first snapshot of an instance is a full replica of the instance's data. The execution time depends on the specific amount of data. Subsequent snapshots retain the content of the incremental differences between the existing snapshot and the new data.

* The operations of restarting the cluster, deleting the cluster, deleting the snapshot being created or restored, and creating or restoring the snapshot again are not supported during the creation and restoration process.

* It is recommended not to perform manual and automatic snapshots on the same instance at the same time, as it affects the performance of the instance because data backups consume the read and write bandwidth of the node's hard disk.

   Check the read and write bandwidth of the node's disk first. If the read and write bandwidth of the disk is close to saturation, it is recommended to stop the snapshot operation to avoid any impact on the read and write performance. How to view the read and write bandwidth of the node's disk, refer to [Viewing monitoring overview](https://docs.byteplus.com/docs/cloudsearch/viewing-monitoring).

    &nbsp;


<span id="enabling-automatic-snapshot-creation"></span>
## Enabling automatic snapshot creation


1. Log on to the [Cloud Search console](https://console.volcengine.com/es).

2. In the top menu bar, select the **Project** and **Region** where the desired instance resides.

3. On the left navigation bar, select **Snapshot management**, then \*\*\*\* click **automatic snapshot** at the top of the page.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">You can also click <strong>automatic snapshot</strong> at the top of the page in the <strong>Instance management \> Snapshot management</strong> page of an instance details page.   </div>
   

4. In the **automatic snapshot** panel, click **Create automatic rules**.

5. In the **Create automatic snapshot rules** dialog box, select the target instance, set parameters such as snapshot period, snapshot retention days, and then click **OK**.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/56a6031af9884f998fdecfeb88a00327~tplv-goo7wpa0wc-image.image) </span>

   
   |**Configuration** |**Description** |
   |---|---|
   |Instance name |Select the target instance for which automatic snapshot creation rule needs to be configured from the drop\-down list.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">If you are entering the snapshot management page from the instance details page, turning on this switch indicates that automatic snapshot creation is enabled for the instance.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">If an instance has already been configured with an automatic snapshot rule, it cannot be configured further and modification of the automatic snapshot rule is not supported.</div><br> |
   |Snapshot period setting |Set the automatic snapshot period as needed.<br><br><br>* Every day: Create a snapshot at a specified time point every day.<br><br>* Per hour: Create a snapshot at a specified minute every hour.<br><br>* User\-defined: Creates a snapshot at a specified time point on the specified day of the week. |
   |Select time point |When the snapshot period is set to Every day, a specific time point needs to be selected, such as 20:30 every day. |
   |Select minute |When the snapshot period is set to Per hour, a specific minute needs to be selected, such as 30 minutes every hour. |
   |Set user\-defined time |When the snapshot period is set to User\-defined, a specific date and time need to be specified, such as 20:00 on Monday.<br><br><br>* Select week: The date for creating a snapshot, such as Monday.<br><br>* Select time: The time (on the hour) for creating a snapshot, such as 20:00. |
   |Snapshot retention days |Set the number of days for snapshot data retention. The range is 1 to 365. The default is 7 days.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">A new instance configured for automatic snapshots uses the default storage bucket of the system. It is possible for an existing instance to use the storage bucket of the current account. For details, see <a href="https://docs.byteplus.com/docs/cloudsearch/36401#87dfd1a5">Snapshot storage</a>.</div><br> |
   |Remarks |Set the remark information for the automatic snapshot. |
   

6. Return to the **automatic snapshot** panel, you can view the automatic snapshot creation rule for the target instance.

   <div style="text-align: center">
   <img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/ff9f1c5915034d1db0c91906fc56dc61~tplv-goo7wpa0wc-image.image" width="1525px" />   </div>
   


<span id="53656882"></span>
## Disabling automatic snapshot creation

When an instance no longer needs to automatically create snapshots, you can disable this feature.


1. Log on to the [Cloud Search console](https://console.volcengine.com/es).

2. In the top menu bar, select the **Project** and **Region** where the desired instance resides.

3. On the left navigation bar, select **Snapshot management**, then \*\*\*\* click **automatic snapshot** at the top of the page.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">You can also select <strong>Instance management \> Snapshot management</strong> in the left navigation bar of the instance details page, and turn off the switch on the <strong>automatic snapshot</strong> page.   </div>
   

4. In the **automatic snapshot** panel, filter the automatic snapshot rule for the target instance by instance name or instance ID, and then click **Delete** behind the snapshot rule.

   <div style="text-align: center">
   <img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/c9a257ba50654d50ad7497a03038d5e5~tplv-goo7wpa0wc-image.image" width="1525px" />   </div>
   

5. In the pop\-up dialog box, review the note for disabling automatic snapshot creation, and then click **OK**.
