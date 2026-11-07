---
title: "Temporary instance specification upgrade"
product: "RDS for PostgreSQL"
product_code: "RDS_for_PG"
source: "https://docs.byteplus.com/en/docs/RDS_for_PG/temporary_instance_specification_upgrade"
---

This topic describes how to temporarily upgrade the specification of RDS for PostgreSQL yearly/monthly subscription instances.

<span id=".6IOM5pmv5L-h5oGv"></span>
## **Background information**

RDS for PostgreSQL supports two instance specification modification methods, namely standard modification and temporary modification.


* Standard modification includes modifying the instance specification or storage space and adding/deleting read\-only nodes. For more information about how to make a standard specification modification, refer to [Standard instance specification modification](https://docs.byteplus.com/en/docs/RDS_for_PG/standard_instance_specification_modification).

* Temporary specification upgrade is a specification modification exclusively for RDS for PostgreSQL yearly/monthly subscription instances to reduce the cost of upgrading the instance specification at business peaks. Temporarily upgraded specification is effective for a limited period of time and a recovery date must be specified at such upgrades. The configuration upgrade of temporary upgrade is short\-term, and a restore date needs to be specified when upgrading. Node specification upgrades are supported only during temporary specification upgrades.


<span id=".5YmN5o-Q5p2h5Lu2"></span>
## **Prerequisites**

The subscription instance has been created, and the instance state is **Running**. For details, see [Creating an instance](https://docs.byteplus.com/en/docs/RDS_for_PG/create_instance).

<span id=".5rOo5oSP5LqL6aG5"></span>
## **Precautions**


* The temporary specification upgrade feature is still in the preview stage. If you need to use them, [submit a ticket](https://console.byteplus.com/workorder/create) to apply.

* Temporary specification upgrade applies to yearly/monthly subscription instances only.

* The temporary specification upgrading period ranges from 5 days to 30 days.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">Temporary upgrades cannot be initiated when the subscription instance has less than 5 days until expiration.   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">The temporary specification upgrading period is up to the remaining available period of the instance if the yearly/monthly subscription instance is to expire in 5–30 days.   </div>
   

* The specifications of the primary and read\-only nodes can be upgraded through temporary specification upgrading only. The secondary node specification is automatically synced with the primary node, while the read\-only node specification must be equal to or higher than the primary node.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">You cannot upgrade the read\-only node specifications only through temporary specification upgrading.   </div>
   

* You cannot add or delete read\-only nodes or change their storage space through temporary specification upgrading. Before submitting a temporary specification upgrade order, you are recommended to fully estimate the business stress and storage space requirement during the temporary specification upgrading period to make sure the current storage capacity meets the service needs during the period. If the storage capacity is insufficient, please scale it up before initiating the temporary specification upgrade.

* You cannot perform standard specification modifications on instances currently in a temporary specification upgrading period.

* You can initiate temporary specification upgrading multiple times. However, the recovery time of each upgrade cannot be earlier than that of the last temporary specification modification. Besides, you must upgrade the node specification at each temporary specification upgrade.

* After you submit a temporary specification upgrade order, the specification modification is initiated based on your order.

   * During the specification modification period, most operations related to the database, account, and network cannot be executed, and the database may experience 3–4 transient disconnections. You are recommended to add an auto reconnection mechanism to your app to reduce the impacts of the disconnections on your services.

   * You do not need to manually restart the instance after a specification modification. The modification may take minutes depending on the number of nodes in the target specification, the current data size, and the write speed of service data.

   * Modifying the specification will not change the instance ID or connection address.

* You cannot unsubscribe from an instance in a temporary specification upgrading period.


<span id=".5pON5L2c5q2l6aqk"></span>
## **Procedure**


1. Login to the [RDS for PostgreSQL console](https://console.byteplus.com/db/rds-pg).

2. In the upper\-left corner of the top menu bar, select the project and region for the instance.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">If the project of the instance has not been set, the project should be selected as <strong>All resources</strong>.   </div>
   

3. Go to the **Modify configuration** page of the target instance through the following paths.

   1. On the **Instances** page, click **Modify configuration** in the **Actions** column of the target instance.

   2. Go to the **Summary** page and click **Modify configuration** in the upper\-right corner.

4. On the **Modify configuration** page of the Target instance, complete the following settings.

   
   |Parameters |Note |
   |---|---|
   |Type of specification modification |Select Temporary upgrade. |
   |Restore date |The temporary upgrade period can be set from 5 to 30 days. No need to manually set the restore time; the system will set it based on the submission time of the temporary upgrade order and the set temporary upgrade period.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">Temporary upgrades can be initiated multiple times to extend the temporary upgrade period, but the total duration cannot exceed 30 days (based on the time of the first temporary upgrade initiation).</div><br><br><br>   * <div data-tips="true" data-tips-type="tip">If it is the first temporary upgrade or the current time is earlier than the effective restore date, the temporary upgrade period can be set for up to 30 days.</div><br><br><br>   * <div data-tips="true" data-tips-type="tip">If the current time is later than the effective restore date, the temporary upgrade period can be set for up to 29 days.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">Multiple Temporary upgrades can be initiated, but the duration of the Temporary upgrade cannot be shortened. If the instance is already in the temporary upgrade period:</div><br><br><br>   * <div data-tips="true" data-tips-type="tip">The new restore date cannot be earlier than the effective restore date.</div><br><br><br>   * <div data-tips="true" data-tips-type="tip">When the subscription instance is within five days of expired, initiating another temporary upgrade is not allowed.</div><br> |
   |Node specification |Temporary upgrade only supports upgrading node specifications. The specifications of the secondary node automatically match those of the primary node, and the specifications of the read\-only node should be equal to or higher than those of the primary node. |
   |Estimated impact |Confirm the impact of changing the instance specification.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="default">The estimated impact is based on the resource state when the configuration is completed on the Modify configuration page. The resource status may change when the modification order is submitted or during the actual modification. The estimated impact is not guaranteed to occur, and the actual impact shall prevail.</div><br><br><br>* <div data-tips="true" data-tips-type="default">In some cases, the impact cannot be estimated due to system reasons. Click the button on the page to retry.</div><br> |
   

5. Click **Confirm order**

6. On the **Confirm order** page, confirm the order details, read and check the **Database Product and Services Terms**, and click **Submit the order**.

7. On the **Confirm order information** page, confirm the order information again and click **Next step**.

8. On the **Submit payment information** page, confirm the payment details and select the **Payment method**, click **Go to payment**, and complete the payment as prompted to complete the temporary upgrade of the instance.


<span id=".55u45YWz5o6l5Y-j"></span>
## Related APIs


|API |Interface description |
|---|---|
|[ModifyDBInstanceSpec](https://docs.byteplus.com/en/docs/RDS_for_PG/modifydbinstancespec) |Call ModifyDBInstanceSpec API to modify the instance configuration. |


&nbsp;
