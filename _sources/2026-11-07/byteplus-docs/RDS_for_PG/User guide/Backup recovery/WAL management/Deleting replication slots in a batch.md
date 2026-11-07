---
title: "Deleting replication slots in a batch"
product: "RDS for PostgreSQL"
product_code: "RDS_for_PG"
source: "https://docs.byteplus.com/en/docs/RDS_for_PG/deleting_replication_slots_in_a_batch"
---

This topic introduces the procedure for deleting replication slots in batches for instances in the RDS for PostgreSQL console.

<span id=".5rOo5oSP5LqL6aG5"></span>
## Precautions


* Deleting physical replication slots in the ACTIVE state is not supported at this time.

* Deleting replication slots in ACTIVE status may cause abnormalities in downstream consumption; operate with caution.

* Only replication slots with the same active status can be deleted in a single batch deletion operation.


<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites


* Instances have been created and the instance is in **Running** state, for more details please see [Creating an instance](https://docs.byteplus.com/en/docs/RDS_for_PG/creating_an_instance).

* The instance contains logical replication slots or physical replication slots in the **Inactive** state.


<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure


1. Login to the [RDS for PostgreSQL console](https://console.byteplus.com/db/rds-pg).

2. In the upper\-left corner of the top menu bar, select the project and region for the instance.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">If the project of the instance has not been set, the project should be selected as <strong>All resources</strong>.   </div>
   

3. Click on **Instances** in the left navigation bar.

4. On the **Instances** page, click on the target instance name.

5. At the top of the page, click **Backups**.

6. On the **Backups** tab, click the **WAL management** subtab to access the replication slot list.

7. In the replication slot list, select multiple slots to delete, then click **Delete** in the lower\-left corner of the list.

8. In the pop\-up **Are you sure to delete the selected slot?**  In the dialog, after confirming the replication slot information to be deleted is correct, click **Delete**.


<span id=".55u45YWzIEFQSQ=="></span>
## Related APIs


|API |Description |
|---|---|
|[DeleteSlot](https://docs.byteplus.com/en/docs/RDS_for_PG/deleteslot) |Call DeleteSlot API to delete the replication slot. |
