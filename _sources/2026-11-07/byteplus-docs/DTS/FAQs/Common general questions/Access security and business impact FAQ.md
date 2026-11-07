---
title: "Access security and business impact FAQ"
product: "Database Transmission Service"
product_code: "DTS"
source: "https://docs.byteplus.com/en/docs/DTS/will_the_data_in_the_source_database_be_deleted_when_using_DTS_for_data_migration"
---

Before accessing Database Transmission Service (DTS), you may be concerned about its impact on source database data security and business operations. This topic answers key questions about data integrity, table\-locking mechanisms, and resource usage:

<span id="eCc2tAEu"></span>
## Will the source database data be deleted or modified?

No.


* Read\-only actions: DTS only executes `SELECT` read operations on the source end and will never write, update, or delete source database data.

* Data security: the migration process does not change any content in the source database, ensuring absolute safety of source end data.


<span id="hV2ybkEz"></span>
## Will tables be locked during migration?

No.


* Lock\-free migration: DTS will not lock tables in the source database during the entire lifecycle of full migration and incremental synchronization.

* Business transparency: the source end's data tables always maintain normal read and write access, with very low business awareness.


<span id="GBSQJy7h"></span>
## Does incremental migration or synchronization affect business continuity?

No, it actually helps ensure continuity.


* Real\-time synchronization: incremental migration captures and synchronizes source end change data in real time, allowing business to continue running on the source end during migration.

* Smooth switching: you can perform final cutover during off\-peak hours, reducing downtime to minutes and minimizing business impact.


<span id="kZeCbdfl"></span>
## Can i manually end a migration task during a full migration?

Not recommended/not allowed.


* System managed: full migration tasks automatically flow and end by the system.

* Risk prompt: do not forcibly manually terminate tasks during full execution, as this likely causes incomplete or abnormal destination data states.

* Correct action: if termination is needed, wait for the full migration phase to complete automatically before stopping.


<span id="fuKtiiqV"></span>
## Will the pressure on the source database increase during migration? How to optimize?

During the full migration phase, data is mainly pulled through `SELECT`, which does cause certain I/O and network overhead. To reduce the impact on core business, the following measures are recommended:


* Off\-peak execution: start the full migration task during business off\-peak hours (such as late night).

* Rate limiting: adjust the full migration rate in Database Transmission Service (DTS) configuration to proactively limit read pressure on the source database.

* Resource isolation: ensure the source database has dedicated connections and bandwidth resources to avoid competing with core business for maximum bandwidth.
