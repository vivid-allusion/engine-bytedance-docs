---
title: "Modifying log backup policies in batches"
product: "RDS for MySQL"
product_code: "RDS_for_MySQL"
source: "https://docs.byteplus.com/en/docs/RDS_for_MySQL/modifying_log_backup_policies_in_batches"
---

RDS for MySQL supports batch modifying the log backup policy for multiple instances. You can set the log backup policy for multiple instances with the same business needs at once. This topic describes how to set the log backup policy for multiple instances.

<span id="prerequisites"></span>
## Prerequisites


* The instance has been created and is in the **Running** status.For specific operations, refer to [Creating an instance](https://docs.byteplus.com/en/docs/RDS_for_MySQL/creating_an_instance_1).

* When batch modifying the log backup policy, make sure that all instances have the same requirements for the log backup policy.


<span id="precautions"></span>
## Precautions


* Read\-only nodes do not support backup settings.

* You can batch modify the log backup policy for up to 50 instances at the same time.


<span id="procedure"></span>
## Procedure


1. Log on to the [RDS for MySQL console](https://console.byteplus.com/db/rds-mysql).

2. In the upper\-left corner of the top menu bar, select the project and region for the instance.

3. On the **Instances** page, select multiple target instances.

4. Click  **... \> Modify local binlog retention policy** in the lower\-left of the **Instances** page.

5. Set the following parameters on the pop\-up **Modify local binlog retention policy** page, and then click **OK** after the parameters are set.

   
   |Parameters |**Description** |
   |---|---|
   |Local binlog retention period |The retention time can be set to 0–168 hours. The local logs beyond the retention time are automatically deleted.When it is set to 0, local logs will not be automatically deleted. |
   |Maximum storage usage ratio |20%–50% can be set. Local Binlog space utilization rate = Local Binlog size / Total available (purchased) space of the instance. The oldest Binlog files will be deleted automatically when the space utilization rate above is exceeded until the space utilization rate is lower than this rate. A large number of Binlogs can be generated during peak hours. We recommend you adjust the maximum storage space utilization rate in advance to avoid Binlog files being deleted and not being synchronized to the secondary node in time. |
   |Maximum number of files to be retained |Enable or disable the function of limiting the number of local binlog retention. When you turn it on, you need to set **Number of local Binlog retained**. |
   |Number of local Binlog retained |The number of local binlog files to keep. 6–1,000 can be set. The local logs beyond the number retained will be automatically deleted.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">The frequency of binlog file switching depends on the log size and log duration, when the binlog file exceeds 500MB or exceeds 1 hour, it will be switched to a new binlog file to continue writing.</div><br> |
   |Available storage space |Enable or disable the protection of the local available storage space. When this feature is turned on, the system will automatically start to clean up the earliest local binlogs when the total storage space occupancy of the instance exceeds 80% or the remaining space is less than 5GB, until the total space occupancy is less than 80% and the remaining space is more than 5GB. |
   

6. In the pop\-up **Batch tasks have been initiated** dialog box, view **Task progress**, and click **OK** after a task is completed.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">You can click <strong>Terminate</strong> in the <strong>Batch tasks have been initiated</strong> dialog box. After termination, the instance change tasks that have not yet started will not be executed and also cannot be resumed. To make changes again, you must initiate the batch task again.</div>


* <div data-tips="true" data-tips-type="tip">If the task fails, hover the cursor on <strong>Failed</strong> in the <strong>Execution result</strong> column to view the causes of failure.</div>
