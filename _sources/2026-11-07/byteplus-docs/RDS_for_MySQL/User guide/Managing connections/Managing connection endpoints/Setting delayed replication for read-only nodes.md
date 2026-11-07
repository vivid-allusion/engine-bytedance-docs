---
title: "Setting delayed replication for read-only nodes"
product: "RDS for MySQL"
product_code: "RDS_for_MySQL"
source: "https://docs.byteplus.com/en/docs/RDS_for_MySQL/setting_delayed_replication_for_read-only_nodes"
---

RDS for MySQL allows you to set the delayed replication time for a read\-only node so that the read\-only node can delay for a period of time before synchronizing data from the primary node.

<span id="precautions"></span>
## Precautions


* After the delayed replication function of the read\-only node is enabled, the read\-only node can only be used as the only node of a read\-only connection endpoint, so you must authorize us to cancel the association of the read\-only node with other endpoints.

* After the delayed replication function of the read\-only node is disabled, you can choose whether to associate this read\-only node with the default endpoint. If you must associate the read\-only node with a custom endpoint, you can do it by editing the endpoint. For more information on the association of the node with the connection endpoint, refer to [Editing connection endpoints](https://docs.byteplus.com/en/docs/RDS_for_MySQL/editing_connection_endpoints).

* Disabling delayed replication can trigger a shutdown failure event notification due to excessive delay. After triggering, you can turn it off again or wait for the system to retry automatically. You cannot set the replication delay for this node again before the successful shutdown of delayed replication.


<span id="prerequisites"></span>
## Prerequisites


* A double\-node instance has been created and is in the **Running** status.For specific operations, refer to [Creating an instance](https://docs.byteplus.com/en/docs/RDS_for_MySQL/creating_an_instance_1).

* The instance has at least one read\-only node. If you must add read\-only nodes to the instance, refer to [Modifying an instance specification](https://docs.byteplus.com/en/docs/RDS_for_MySQL/changing_an_instance_configuration).

* The status of the instance's database agent feature is **Enabled**. To turn it on, refer to [Enabling the database agent](https://docs.byteplus.com/en/docs/RDS_for_MySQL/enable_database_agent).


<span id="procedure"></span>
## Procedure


1. Log on to the [RDS for MySQL console](https://console.byteplus.com/db/rds-mysql).

2. In the upper\-left corner of the top menu bar, select the project and region for the instance.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">说明   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">If no project is set, you should select the option <strong>All resources</strong> at this step.   </div>
   

3. Click **Instances** at the left\-side navigation bar to go to the **Instances** page.

4. Go to the **Instances** page and click on the target instance name to open the **Summary** page.

5. Click **Connectivity** tab on the **Summary** page to go to the **Connectivity** page.

6. In the **Instance topology** area of the **Connectivity** page, hover the cursor over the target read\-only node.

7. In the pop\-up read\-only node card, click **Set replication delay**.

8. In the **Set replication delay** window, complete the following to turn the delayed replication feature on or off.

   * Turn on delayed replication

      1. Turn on the **Replication delay** switch.

      2. Set the data delay time. The value range of the data delay time is 1–604,800, with a step size of 1, in seconds.

      3. Confirm endpoint information and click **OK**.

      <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="2">说明      </div>
      

      <div data-tips="true" data-tips-type="tip" data-wrapper-indent="2">After the delayed replication function of the read\-only node is enabled, more log files can be kept locally. Set the data delay time as appropriate and reserve enough storage space to prevent the delayed replication function of the read\-only node from being suspended due to excessive storage space usage. You can enable the <strong>Maximum available storage space</strong> function in the log backup policy. After this function is enabled, the instance can automatically clear binlogs when the disk space is higher than 80% to ensure sufficient storage space. For more information on the adjustment of the log backup policy, refer to <a href="https://docs.byteplus.com/en/docs/RDS_for_MySQL/modifying_data_backup_policies">Customizing log backup policies</a>.      </div>
      

   * Turn off delayed replication

      Turn off the **Replication delay** switch in the **Set replication delay** window, and confirm whether the node is re\-associated with the default connection endpoint, and then click **OK**.


<span id="relevant-apis"></span>
## Relevant APIs


|API |**Description** |
|---|---|
|[DescribeReadOnlyNodeDelay](https://docs.byteplus.com/en/docs/RDS_for_MySQL/describereadonlynodedelay) |Call DescribeReadOnlyNodeDelay to query the delayed replication configuration of read\-only nodes. |
|[ModifyReadOnlyNodeDelayReplicationTime](https://docs.byteplus.com/en/docs/RDS_for_MySQL/modifyreadonlynodedelayreplicationtime) |Call ModifyReadOnlyNodeDelayReplicationTime to configure the delayed replication function for read\-only nodes. |
