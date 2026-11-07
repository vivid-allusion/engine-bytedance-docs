---
title: "Viewing historical events"
product: "Document Database for MongoDB"
product_code: "mongodb"
source: "https://docs.byteplus.com/en/docs/mongodb/view-historical-event"
---

MongoDB provides historical events feature. You can view O&M operation events related to MongoDB instances through the console, such as creating instances or performing manual backups.

<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure


1. Log in to the [MongoDB console](https://console.byteplus.com/db/region:db+cn-beijing/mongodb).

2. In the upper\-left corner of the top menu bar, select the project and region for instance.

3. In the left navigation bar, select **NoSQL Databases \> MongoDB \> Historical event**.

4. On the **Historical event** page, you can filter details of historical events in the specified time range by instance ID or event operation, such as the ID of the primary account to which the event belongs, operation time, operation duration, event result, and event description.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">Currently, only the events of <a href="https://docs.byteplus.com/en/docs/mongodb/recovery-from-backup-file">recovery from backup files</a>, <a href="https://docs.byteplus.com/en/docs/mongodb/recovery-by-time-point">recovery by point in time</a> and <a href="https://docs.byteplus.com/en/docs/mongodb/recovery_from_a_deleted_instance">recovery from a deleted instance</a> (that is, the <strong>Event action</strong> named <code>RestoreToNewInstance</code>) support for displaying <strong>Event description</strong>, which contains the instance ID and name information of the source instance and the new instance.   </div>
